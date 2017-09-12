---
title: "維度儲存體 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], storage
- storing data [Analysis Services]
- storage [Analysis Services], dimensions
- relational OLAP
- multidimensional OLAP
- MOLAP
- storing data [Analysis Services], dimensions
- ROLAP
ms.assetid: 8d74b932-2174-4e1f-8414-636455880b6a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b45ab57b151c2cdab5ae7aa133befd06893037bd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions---storage"></a>維度-儲存體
  中的維度[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援兩種儲存模式：  
  
-   關聯式 OLAP (ROLAP)  
  
-   多維度 OLAP (MOLAP)  
  
 儲存模式決定維度之資料的位置和形式。 維度的預設儲存模式為 MOLAP。 **相關主題：**[磁碟分割儲存模式及處理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 使用 MOLAP 的維度資料，會儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的多維度結構中。 在處理維度時，會建立及擴展這種多維度結構。 MOLAP 維度提供比 ROLAP 維度更好的查詢效能。  
  
## <a name="rolap"></a>ROLAP  
 使用 ROLAP 的維度資料，實際上是儲存在用來定義該維度的資料表中。 ROLAP 儲存模式可用於在不複製大量資料的情況下支援大型維度，但需要犧牲查詢效能。 因為維度會直接依賴用來定義該維度之資料來源檢視中的資料表，所以 ROLAP 儲存模式也可以支援即時 OLAP。  
  
> [!IMPORTANT]  
>  如果維度使用 ROLAP 儲存模式，而且該維度包含在使用 MOLAP 儲存的 Cube 中，則對於其來源資料表進行任何結構描述變更之後，必須立即處理此 Cube。 如果沒有這樣做，則在查詢 Cube 時，可能會產生不一致的結果。 **相關的主題：**[自動化 Analysis Services 系統管理工作與 SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割儲存模式及處理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  