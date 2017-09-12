---
title: "BEGIN TRANSACTION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BEGIN_TRANSACTION_TSQL
- TRANSACTION_TSQL
- TRANSACTION
- BEGIN TRANSACTION
- BEGIN TRAN
- BEGIN_TRAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction logs [SQL Server], BEGIN TRANSACTION statement
- marked transactions [SQL Server], BEGIN TRANSACTION statement
- BEGIN TRANSACTION statement
- local transactions [SQL Server]
- marking transactions [SQL Server]
- transactions [SQL Server], starting
- transaction names [SQL Server]
- starting point marked for transactions
- starting transactions
ms.assetid: c6258df4-11f1-416a-816b-54f98c11145e
caps.latest.revision: 56
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f52f237795de00f4ad78403bed986ac571005c31
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="begin-transaction-transact-sql"></a>BEGIN TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  標示明確本機交易的起點。 外顯交易 BEGIN TRANSACTION 陳述式的開頭和結尾的 COMMIT 或 ROLLBACK 陳述式。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
--Applies to SQL Server and Azure SQL Database
 
BEGIN { TRAN | TRANSACTION }   
    [ { transaction_name | @tran_name_variable }  
      [ WITH MARK [ 'description' ] ]  
    ]  
[ ; ]  
```  
 
```  
--Applies to Azure SQL Data Warehouse and Parallel Data Warehouse
 
BEGIN { TRAN | TRANSACTION }   
[ ; ]  
```  

  
## <a name="arguments"></a>引數  
 *transaction_name*  
 **適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database
 
 這是指派給交易的名稱。 *transaction_name*必須符合的規則識別碼，但超過 32 個字元不允許的識別項。 請只在巢狀 BEGIN...COMMIT 或 BEGIN...ROLLBACK 陳述式的最外一組使用交易名稱。 *transaction_name*一律區分大小寫，即使是執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不區分大小寫。  
  
 @*tran_name_variable*  
 **適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database
 
 這是包含有效交易名稱之使用者定義變數的名稱。 變數必須宣告與**char**， **varchar**， **nchar**，或**nvarchar**資料型別。 如果有 32 個以上的字元傳給變數，只會使用前 32 個字元，其餘字元會截斷。  
  
 WITH MARK ['*描述*']  
**適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database

指定在記錄中標示交易。 *描述*是說明標示的字串。 A*描述*長度超過 128 個字元，會先儲存在 msdb.dbo.logmarkhistory 資料表截斷成 128 個字元。  
  
 如果使用 WITH MARK，必須指定交易名稱。 WITH MARK 可讓您將交易記錄還原到具名標記。  
  
## <a name="general-remarks"></a>一般備註
BEGIN TRANSACTION 會遞增@TRANCOUNT1。
  
BEGIN TRANSACTION 代表連接所參考的資料在邏輯和實體上都一致的點。 如果發生錯誤，可以回復 BEGIN TRANSACTION 之後的所有資料修正，使資料返回這個已知的一致狀態。 每項交易都會持續到它完成無誤，且發出 COMMIT TRANSACTION 使修正成為資料庫的永久部分為止，或持續到發生錯誤，且利用 ROLLBACK TRANSACTION 陳述式來清除所有修正為止。  
  
BEGIN TRANSACTION 會針對發出陳述式的連接來啟動一項本機交易。 依照目前的交易隔離等級設定而定，此時會取得許多資源來支援交易鎖定的連接所發出的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，直到利用 COMMIT TRANSACTION 或 ROLLBACK TRANSACTION 陳述式來完成它為止。 交易長時間未完成會使其他使用者無法存取這些鎖定的資源，也會使記錄無法截斷。  
  
 雖然 BEGIN TRANSACTION 會啟動一項本機交易，但它並不會記錄在交易記錄中，直到應用程式後來執行必須記錄的動作 (如執行 INSERT、UPDATE 或 DELETE 陳述式) 為止。 應用程式可以執行取得鎖定來保護 SELECT 陳述式的交易隔離等級之類的動作，但在應用程式執行修改動作之前，不會在記錄檔案留下任何記錄。  
  
 利用交易名稱在一系列巢狀交易中命名多項交易對交易的影響不大。 系統只會登錄第一個 (最外層) 交易名稱。 回復任何其他名稱 (不是有效的儲存點名稱) 都會產生錯誤。 事實上在發生這個錯誤時，並不會回復在回復之前所執行的任何陳述式。 只有當外部交易回復時，才會回復陳述式。  
  
 如果在認可或回復陳述式之前執行下列動作，BEGIN TRANSACTION 陳述式所啟動的本機交易會擴大到分散式交易：  
  
-   執行參考連結伺服器上遠端資料表的 INSERT、DELETE 或 UPDATE 陳述式。 如果用來存取連結的伺服器的 OLE DB 提供者不支援 ITransactionJoin 介面，INSERT、 UPDATE 或 DELETE 陳述式將會失敗。  
  
-   當 REMOTE_PROC_TRANSACTIONS 選項設為 ON 時，呼叫遠端預存程序。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機複本會成為交易控制器，且會利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 來管理分散式交易。  
  
 您可以利用 BEGIN DISTRIBUTED TRANSACTION，將交易明確當做分散式交易來執行。 如需詳細資訊，請參閱[BEGIN DISTRIBUTED TRANSACTION &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 當 SET IMPLICIT_TRANSACTIONS 設定為 ON 時，BEGIN TRANSACTION 陳述式會建立兩筆巢狀交易。 如需詳細資訊，請參閱[SET IMPLICIT_TRANSACTIONS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)  
  
## <a name="marked-transactions"></a>標示的交易  
 WITH MARK 選項會使交易名稱出現在交易記錄中。 當您將資料庫還原到較早的狀態時，可以利用標示的交易來取代日期和時間。 如需詳細資訊，請參閱[使用標示的異動以一致復原相關資料庫 &#40;完整復原模式 &#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)和[還原 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 另外，如果您必須將一組相關資料庫復原到邏輯一致的狀態，交易記錄標示便是必要的。 分散式交易可以將標示放在這組相關資料庫的交易記錄中。 將這組相關資料庫復原到這些標示會產生一組交易一致的資料庫。 將標示放在相關資料庫中需要特殊程序。  
  
 只有當標示的交易更新資料庫時，才會將標示放在交易記錄中。 未修改資料的交易不會有標示。  
  
 BEGIN TRAN *new_name* WITH MARK 可以巢狀未標記為現有交易內。 在這麼做， *new_name*變成標示名稱對於交易而言雖然交易可能已有給定的名稱。 在下列範例中，標示的名稱是 `M2`。  
  
```  
BEGIN TRAN T1;  
UPDATE table1 ...;  
BEGIN TRAN M2 WITH MARK;  
UPDATE table2 ...;  
SELECT * from table1;  
COMMIT TRAN M2;  
UPDATE table3 ...;  
COMMIT TRAN T1;  
```  
  
 當建立巢狀交易時，試圖標示已標示的交易會產生一則警告 (不是錯誤) 訊息：  
  
 "BEGIN TRAN T1 WITH MARK ...;"  
  
 "UPDATE table1 ...;"  
  
 "BEGIN TRAN M2 WITH MARK ...;"  
  
 "Server: Msg 3920, Level 16, State 1, Line 3"  
  
 "WITH MARK 選項只可套用至第一個 BEGIN TRAN WITH MARK。"  
  
 "已忽略選項。"  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-an-explicit-transaction"></a>A. 使用明確交易
**適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database、 Azure SQL 資料倉儲、 Parallel Data Warehouse

這個範例會使用 AdventureWorks。 

```
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```

### <a name="b-rolling-back-a-transaction"></a>B. 回復交易
**適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database、 Azure SQL 資料倉儲、 Parallel Data Warehouse

下列範例顯示回復交易的效果。 在此範例中，ROLLBACK 陳述式將會回復 INSERT 陳述式，但仍會存在建立的資料表。

```
 
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  

```

### <a name="c-naming-a-transaction"></a>C. 命名交易 
**適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database

下列範例顯示如何命名交易。  
  
```  
DECLARE @TranName VARCHAR(20);  
SELECT @TranName = 'MyTransaction';  
  
BEGIN TRANSACTION @TranName;  
USE AdventureWorks2012;  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
  
COMMIT TRANSACTION @TranName;  
GO  
```  
  
### <a name="d-marking-a-transaction"></a>D. 標示交易  
**適用於：** （從 2008年起） 的 SQL Server、 Azure SQL Database

下列範例顯示如何標示交易。 已標示交易 `CandidateDelete`。  
  
```  
BEGIN TRANSACTION CandidateDelete  
    WITH MARK N'Deleting a Job Candidate';  
GO  
USE AdventureWorks2012;  
GO  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
GO  
COMMIT TRANSACTION CandidateDelete;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [認可工作 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
