---
title: 處理 SQL 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 603cb680e2986d484074a43d14f56de210da0b4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="processing-sql-statements"></a>處理 SQL 陳述式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 ODBC 資料指標程式庫所有 SQL 陳述式會直接都傳遞至驅動程式，但下列除外：  
  
-   定位 update 和 delete 陳述式  
  
-   **SELECT FOR UPDATE**陳述式  
  
-   批次的 SQL 陳述式  
  
 若要執行定位的 update 和 delete 陳述式，並將游標放在一個資料列呼叫**SQLGetData**該資料列，資料指標程式庫建構的資料列的搜尋陳述式。  
  
 此章節包含下列主題。  
  
-   [處理定位的 Update 和 Delete 陳述式](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [處理 SELECT FOR UPDATE 陳述式](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 陳述式的處理批次](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)
