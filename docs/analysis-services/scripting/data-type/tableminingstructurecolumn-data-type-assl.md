---
title: "TableMiningStructureColumn 資料類型 (ASSL) |Microsoft 文件"
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
- TableMiningStructureColumn Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableMiningStructureColumn
helpviewer_keywords:
- TableMiningStructureColumn data type
ms.assetid: 350358b0-f2fc-43c3-957d-884c59fa879e
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7ba1195b1920625f8602a24f6ba8fa5879639fc5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="tableminingstructurecolumn-data-type-assl"></a>TableMiningStructureColumn 資料類型 (ASSL)
  定義衍生的資料類型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含巢狀的資料表，而不是與相關聯的純量值的項目[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)包含純量值的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TableMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <ForeignKeyColumn>..</ForeignKeyColumn>  
   <SourceMeasureGroup>..</SourceMeasureGroup>  
   <Columns>..</Columns>  
   <Translations>..</Translations>  
</TableMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[資料行](../../../analysis-services/scripting/collections/columns-element-assl.md)， [ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)， [SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|衍生的元素|[資料行](../../../analysis-services/scripting/objects/column-element-assl.md)([資料行](../../../analysis-services/scripting/collections/columns-element-assl.md)集合[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  