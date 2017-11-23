---
title: "sys.function_order_columns (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs: TSQL
helpviewer_keywords: sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 151d91a53092b9303f576d5b650abdc71a797039
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，每個資料行的一部分**順序**屬於 common language runtime (CLR) 資料表值函數的運算式。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|定義順序所在之物件的識別碼 (CLR 資料表值函式)。|  
|**order_column_id**|**int**|排序資料行的識別碼。 **order_column_id**只有在是唯一**object_id**。<br /><br /> **order_column_id**表示此資料行的位置依順序排列。|  
|**column_id**|**int**|中的資料行的識別碼**object_id**。<br /><br /> **column_id**只有在是唯一**object_id**。|  
|**is_descending**|**bit**|1 = 排序資料行是以遞減方式排序。<br /><br /> 0 = 排序資料行是以遞增方式排序。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  