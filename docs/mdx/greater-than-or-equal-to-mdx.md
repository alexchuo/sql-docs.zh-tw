---
title: '&gt;= (大於或等於) (MDX) |Microsoft 文件'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: db81285593b04a2b82c5eed87c3747a1f9450e42
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579120"
---
# <a name="gt-greater-than-or-equal-to-mdx"></a>&gt;= (大於或等於) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行比對作業，判定某個多維度運算式 (MDX) 運算式的值是否大於或等於另一個 MDX 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
MDX_Expression >= MDX_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值根據以下條件而定：  
  
-   **true**第一個參數是否大於或等於第二個參數的值的值。  
  
-   **false**如果第一個參數的值小於第二個參數的值。  
  
-   **true**如果這兩個參數都是 null，或是一個參數是 null，且另一個參數為 0。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is greater than or equal to 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] >= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
    NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[HighGPM])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
