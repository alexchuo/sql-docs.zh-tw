---
title: "輸入元素 (MeasureGroupAttribute) (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (MeasureGroupAttribute)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 93740504-297a-4a06-ab3e-b598e466eebb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 966c5e29b9f6f2569260ea90dd32f76cab4b064d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-measuregroupattribute-assl"></a>Type 元素 (MeasureGroupAttribute) (ASSL)
  包含的型別[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupAttribute>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroupAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*規則*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*規則*|代表一般屬性。|  
|*資料粒度*|代表資料粒度屬性。|  
  
 列舉型別對應至允許的值**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>。  
  
 對應目的父代的項目**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [Attributes 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [RegularMeasureGroupDimension 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  