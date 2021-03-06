---
title: XML 資料類型 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c52717a6f061f4708b2d3e46c6d34f837b2039af
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34573780"
---
# <a name="xml-data-types-xmla"></a>XML 資料類型 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  除了 XML 1.0 建議所定義的標準基本和衍生類型以外，XML for Analysis (XMLA) 1.1 規格還定義了其他資料類型，可支援多維度和表格式資料的表示。  
  
 XMLA 會使用下表所列的資料類型。  
  
|資料類型|描述|  
|----------------|-----------------|  
|布林|標準的 XML**布林**資料型別。|  
|Decimal|標準的 XML**十進位**資料型別。|  
|[EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|命名空間上的**根**項目。 XMLA 命令不會傳回結果，因為 XMLA 命令通常也不會傳回結果或錯誤時發生 Analysis Services 執行個體執行 XMLA 命令時，會傳回此命名空間。|  
|[EnumString](../../../analysis-services/xmla/xml-data-types/enumstring-data-type-xmla.md)|給定列舉值的具名字串常數集合。|  
|Integer|標準的 XML **int**資料型別。|  
|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)|所傳回的多維度資料*結果*參數[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。|  
|[結果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|自我描述 XML 結果集所傳回**Execute**方法。|  
|[Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|傳回資料列從資料來源，內嵌 XML 結構描述，結構化[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。|  
|String|XML**字串**資料型別。|  
|UnsignedInt|XML **unsignedInt**結構描述型別。|  
  
 如需標準 XML 資料類型的完整描述，請參閱全球資訊網協會 (WC3) 的候選建議。  
  
## <a name="see-also"></a>另請參閱
 [XML 項目&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML for Analysis &#40;XMLA&#41;參考](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
