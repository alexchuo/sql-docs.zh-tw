---
title: 集合 (ADO-WFC 語法) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c77a41ae0474d9b917dbe551ef3e217f667930b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="collections-ado---wfc-syntax"></a>集合 (ADO-WFC 語法)
**封裝 com.ms.wfc.data**  
  
## <a name="parameters"></a>參數  
  
### <a name="methods"></a>方法  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>欄位  
  
### <a name="methods"></a>方法  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>錯誤  
  
### <a name="methods"></a>方法  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>另請參閱  
 [錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
