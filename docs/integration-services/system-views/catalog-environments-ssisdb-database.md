---
title: catalog.environments (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76054c01ad1e033e1ef5a190b133e3ee9b0035e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有環境顯示環境詳細資料。 環境包含可由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案參考的變數。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|環境的唯一識別碼 (ID)。|  
|NAME|**sysname**|環境的名稱。|  
|folder_id|**bigint**|環境所在資料夾的唯一識別碼。|  
|description|**nvarchar(1024)**|環境的描述。 此為選擇性的值。|  
|created_by_sid|**varbinary(85)**|建立環境之使用者的安全性識別碼 (SID)。|  
|created_by_name|**nvarchar(128)**|建立環境的使用者名稱。|  
|created_time|**datetimeoffset**|建立環境的日期和時間。|  
  
## <a name="remarks"></a>Remarks  
 這個檢視會顯示目錄中每個環境的資料列。 環境名稱的唯一性只需在其所處資料夾中成立。 例如，名為 `E1` 的環境可以存在於目錄中的多個資料夾，但每個資料夾只能有一個名為 `E1` 的環境。  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   環境的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
