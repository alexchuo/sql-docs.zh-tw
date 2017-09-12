---
title: "ALTER DATABASE SET HADR (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET HADR
- SET_HADR_TSQL
- HADR_TSQL
- HADR
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE statement, AlwaysOn Availability Group
- ALTER DATABASE statement, SET HADR options
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
- Availability Groups [SQL Server], databases
ms.assetid: 20e6e803-d6d5-48d5-b626-d1e0a73d174c
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3799bc24ab3cfa9f0d65c961f69b72210c6cccef
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-transact-sql-set-hadr"></a>ALTER DATABASE (TRANSACT-SQL) SET HADR 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主題包含設定的 ALTER DATABASE 語法[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]次要資料庫的選項。 只有一個 SET HADR 選項會允許每個 ALTER DATABASE 陳述式。 只有在次要複本上才支援這些選項。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER DATABASE database_name  
   SET HADR   
   {  
        { AVAILABILITY GROUP = group_name | OFF }  
   | { SUSPEND | RESUME }  
   }  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是要修改的次要資料庫名稱。  
  
 SET HADR  
 在指定的資料庫上執行所指定的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 命令。  
  
 {可用性群組** = ** *group_name* |OFF}  
 從指定的可用性群組中加入或移除可用性資料庫，方法如下：  
  
 *群組名稱*  
 將次要複本 (由執行此命令的伺服器執行個體所主控) 上指定的資料庫，聯結到 group_name 所指定的可用性群組中。  
  
 此作業的必要條件如下：  
  
-   資料庫必須已加入主要複本上的可用性群組。  
  
-   主要複本必須處於作用中狀態。 如需有關如何疑難排解非作用中的主要複本，請參閱 <<c0> [ 疑難排解一律在可用性群組組態 (SQL Server)](http://go.microsoft.com/fwlink/?LinkId=225834)。  
  
-   主要複本必須在線上，而次要複本必須連接至主要複本。  
  
-   次要資料庫必須已使用 WITH NORECOVERY 從主要資料庫最近的資料庫備份和記錄備份進行還原，並於還原結束時建立記錄備份檔，且其時間點必須足以讓次要資料庫趕上主要資料庫。  
  
    > [!NOTE]  
    >  若要將資料庫加入至可用性群組中，連接到裝載主要複本的伺服器執行個體，並使用[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name*將資料庫加入*database_name*陳述式。  
  
 如需詳細資訊，請參閱 [將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
 OFF  
 從可用性群組中移除指定的次要資料庫。  
  
 若次要資料庫已落後主要資料庫過多，而您不想等候它趕上時，移除次要資料庫將有所助益。 移除次要資料庫之後, 您可以加以更新藉由還原一系列的備份結尾新的記錄備份 （使用 RESTORE... 使用 WITH NORECOVERY)。  
  
> [!IMPORTANT]  
>  若要完全移除可用性資料庫從可用性群組，請連接到裝載主要複本的伺服器執行個體，並使用[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name*移除資料庫*availability_database_name*陳述式。 如需詳細資訊，請參閱[移除主要資料庫從可用性群組 & #40;SQL Server & #41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 SUSPEND  
 暫停次要資料庫上的資料活動。 一旦裝載目標資料庫的複本接受 SUSPEND 命令之後，就會將其傳回，但暫停資料庫實際上是以非同步方式進行。  
  
 影響的範圍取決於您執行 ALTER DATABASE 陳述式的位置。  
  
-   若您在次要複本上暫停了次要資料庫，只會暫停本機次要資料庫。 可讀取次要複本上的現有連接會保持可用狀態。 在資料移動繼續執行之前，不允許可讀取次要複本上已暫停之資料庫的新連接。  
  
-   若您在主要複本上暫停了次要資料庫，則會暫停所有次要複本上對應的次要資料庫之資料活動。 可讀取的次要複本上的現有連接會保持可用狀態，以及新的讀取意圖連接將無法連線至可讀取次要複本。  
  
-   如果資料移動因強制手動容錯移轉而暫停，則在資料移動暫停時不允許建立與新次要複本的連接。  
  
 暫停次要複本上的資料庫時，該資料庫與其複本皆會變成不同步，並會標示為 NOT SYNCHRONIZED。  
  
> [!IMPORTANT]  
>  次要資料庫暫停期間，所對應之主要資料庫的傳送佇列將會累積未傳送的交易記錄。 次要複本的連接會傳回在資料移動暫停時可用的資料。  
  
> [!NOTE]  
>  暫停和繼續 Alwayson 次要資料庫不會直接影響可用性的主要資料庫，不過暫停次要資料庫可能影響主要資料庫的備援和容錯移轉功能直到暫停次要資料庫會繼續執行。 相反的，在資料庫鏡像中，鏡像狀態會在鏡像資料庫和主體資料庫上暫停，直到鏡像繼續為止。 暫停 AlwaysOn 主要資料庫會暫停所有對應次要資料庫上的資料移動，而且該資料庫的備援和容錯移轉功能也會停止，直到主要資料庫繼續為止。  
  
 如需詳細資訊，請參閱[暫止可用性資料庫 & #40;SQL Server & #41;](../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md).  
  
 RESUME  
 繼續指定之次要資料庫上暫停的資料活動。 一旦裝載目標資料庫的複本接受 RESUME 命令之後，就會將其傳回，但繼續資料庫實際上是以非同步方式進行。  
  
 影響的範圍取決於您執行 ALTER DATABASE 陳述式的位置。  
  
-   若您在次要複本上繼續次要資料庫，只會繼續本機次要資料庫。 除非資料庫也已在主要複本上暫停，否則將會繼續資料活動。  
  
-   若您在主要複本上繼續資料庫，則會繼續所有所對應之次要資料庫未個別暫停的次要複本之資料活動。 若要繼續在次要複本上個別暫停的次要資料庫，請連接至主控次要複本的伺服器執行個體，然後於該處繼續資料庫。  
  
     在同步認可模式下，資料庫的狀態將會變更為 SYNCHRONIZING。 如果沒有其他正在暫停的資料庫，複本狀態也會變更為 SYNCHRONIZING。  
  
     如需詳細資訊，請參閱本主題稍後的＜ [繼續可用性資料庫 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)中的可用性資料庫。  
  
## <a name="database-states"></a>資料庫狀態  
 次要資料庫加入可用性群組時，本機次要複本會將該次要資料庫的狀態從 RESTORING 變更為 ONLINE。 從可用性群組中移除次要資料庫之後，本機次要複本會將該次要資料庫的狀態改回 RESTORING。 如此可讓您將後續的記錄備份從主要資料庫套用至次要資料庫。  
  
## <a name="restrictions"></a>限制  
 在交易與批次之外執行 ALTER DATABASE。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER 權限。 將資料庫聯結至可用性群組需要的成員資格**db_owner**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會將次要資料庫 `AccountsDb1` 聯結至 `AccountsAG` 可用性群組的本機次要複本。  
  
```  
ALTER DATABASE AccountsDb1 SET HADR AVAILABILITY GROUP = AccountsAG;  
```  
  
> [!NOTE]  
>  若要查看內容中使用的這個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，請參閱 [建立可用性群組和 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [AlwaysOn 可用性群組 & #40; 的概觀SQL Server & #41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) [疑難排解 AlwaysOn 可用性群組組態 & #40;SQL Server & #41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md) 
  
  