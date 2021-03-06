---
title: 維度的資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b34e3104d41124fe4a348d663e073bb40a3e8ccf
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dimension-data-type-assl"></a>Dimension 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表資料庫維度的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Source>...</Source>  
   <MiningModelID>...</MiningModelID>  
   <Type>...</Type>  
   <UnknownMember>...</UnknownMember>  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   <ErrorConfiguration>...</ErrorConfiguration>  
   <StorageMode>...</StorageMode>  
   <WriteEnabled>...</WriteEnabled>  
   <ProcessingPriority>...</ProcessingPriority>  
   <LastProcessed>...</LastProcessed>  
   <DimensionPermissions>...</DimensionPermissions>  
   <DependsOnDimensionID>...</DependsOnDimensionID>  
   <Language>...</Language>  
   <Collation>...</Collation>  
   <UnknownMemberName>...</UnknownMemberName>  
   <UnknownMemberTranslations>...</UnknownMemberTranslations>  
   <State>...</State>  
   <ProactiveCaching>...</ProactiveCaching>  
   <ProcessingMode>...</ProcessingMode>  
   <CurrentStorageMode>...</CurrentStorageMode>  
   <Translations>...</Translations>  
   <Attributes>...</Attributes>  
   <AttributeAllMemberName>...</AttributeAllMemberName>  
   <AttributeAllMemberTranslations>...</AttributeAllMemberTranslations>  
   <Hierarchies>...</Hierarchies>  
   <Relationships>...</Annotations>  
   <Annotations>...</Annotations>  
</Dimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md)[AttributeAllMemberName](../../../analysis-services/scripting/properties/attributeallmembername-element-assl.md)、[AttributeAllMemberTranslations](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)、[Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md)、[Collation](../../../analysis-services/scripting/properties/collation-element-assl.md)、[CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)、[CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)、[DependsOnDimensionID](../../../analysis-services/scripting/properties/dependsondimensionid-element-assl.md)、[Description](../../../analysis-services/scripting/properties/description-element-assl.md)、[DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)、[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)、[Hierarchies](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)、[ID](../../../analysis-services/scripting/properties/id-element-assl.md)、[Language](../../../analysis-services/scripting/properties/language-element-assl.md)、[LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)、[LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)、[MdxMissingMemberMode](../../../analysis-services/scripting/properties/mdxmissingmembermode-element-assl.md)、[MiningModelID](../../../analysis-services/scripting/properties/miningmodelid-element-assl.md)、[Name](../../../analysis-services/scripting/properties/name-element-assl.md)、[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)、[ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)[ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)、[Relationships](../../../analysis-services/scripting/collections/relationships-element-assl.md)[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)、[State](../../../analysis-services/scripting/properties/state-element-assl.md)、[StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md)、[Translations](../../../analysis-services/scripting/collections/translations-element-assl.md)、[Type](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)、[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)、[UnknownMemberName](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)、[UnknownMemberTranslations](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)、[WriteEnabled](../../../analysis-services/scripting/properties/writeenabled-element-assl.md)|  
|衍生的元素|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 此資料類型在 DeploymentMode 值 1 (SharePoint) 和 2 (表格式) 下，擁有下列驗證。  
  
-   *WriteEnabled* 子元素必須設定為 **False**  
  
-   *UnknownMember* 子元素必須設定為 **AutomaticNull**  
  
-   所有唯一屬性都必須將 *NullProcessing* 子元素設為 **Error**  
  
 DeploymentMode 值 1 (SharePoint) 和 2 (表格式) 不支援下列子屬性。  
  
-   *DimensionPermissions*  
  
-   *MiningModelID*  
  
-   *ProactiveCaching*  
  
 分析管理物件 (AMO) 物件模型中對應的元素是<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.AggregationDimension>， <xref:Microsoft.AnalysisServices.AggregationDesignDimension>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupDimension>，和<xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
