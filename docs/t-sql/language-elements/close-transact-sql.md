---
title: "關閉 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs:
- TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7315b45fa3b13b96fa01c7833ed1370f72e4bab8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="close-transact-sql"></a>CLOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  釋出目前結果集，再釋放對資料指標所在的資料列所保留的任何資料指標鎖定，來關閉開啟的資料指標。 CLOSE 會保留資料結構仍可重新開啟的狀態，但在重新開啟資料指標之前，不允許提取和定位更新。 必須對開啟的資料指標發出 CLOSE；對於只是宣告過或已關閉的資料指標，不允許發出 CLOSE。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>引數  
 GLOBAL  
 指定*cursor_name*參考全域資料指標。  
  
 *cursor_name*  
 這是開啟的資料指標名稱。 如果全域和本機資料指標同時存在，且*cursor_name*做為其名稱， *cursor_name* GLOBAL 時指定，否則是指全域資料指標*cursor_name*參考本機資料指標。  
  
 *cursor_variable_name*  
 這是與開啟的資料指標相關聯的資料指標變數名稱。  
  
## <a name="examples"></a>範例  
 下列範例會顯示在以資料指標為基礎的處理序中，`CLOSE` 陳述式的正確放置方式。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料指標](../../relational-databases/cursors.md)   
 [資料指標 &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [解除配置 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [擷取 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [開啟 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  