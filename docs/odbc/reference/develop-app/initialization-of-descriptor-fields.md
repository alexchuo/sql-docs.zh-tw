---
title: 描述元欄位初始化 |Microsoft 文件
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
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c3a5d7a6abe5f7f21da802b1daeda8df9dd3e6c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定
當應用程式的資料列描述項配置時，其欄位接收起始值所示[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 SQL_DESC_TYPE 欄位的初始值為 SQL_DEFAULT。 如此可提供標準的處理方式來呈現給應用程式的資料庫資料。 應用程式可以設定欄位的描述項記錄，以指定不同的處理方式的資料。  
  
 描述項標頭中的 SQL_DESC_ARRAY_SIZE 初始值為 1。 應用程式可以修改此欄位，以啟用多重資料列擷取。  
  
 預設值的概念的 IRD 欄位無效。 應用程式可以存取的 IRD 欄位時，才與它相關聯的已備妥或已執行的陳述式。  
  
 在 IPD 自動填入驅動程式之後，才定義 IPD 的某些欄位。 如果不是，它們是未定義。 這些欄位是 SQL_DESC_CASE_SENSITIVE、 SQL_DESC_FIXED_PREC_SCALE、 SQL_DESC_TYPE_NAME、 SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
