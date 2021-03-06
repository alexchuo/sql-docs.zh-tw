---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM |Microsoft 文件
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
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11e7151dea1e522b1c265313043f840c2cced8a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
針對 RDS[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，指定非同步擷取資料的執行緒的執行優先順序。  
  
 使用這些常數**資料錄集**"**背景執行緒優先順序**"動態屬性，其參考 ADO-OLE DB 動態屬性的索引中，並記載於[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文件。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|設定一般和最高優先順序。|  
|**adPriorityBelowNormal**|2|設定優先順序最低和標準之間。|  
|**adPriorityHighest**|5|設定的最高的可能優先權。|  
|**AdPriorityLowest**|1|設定最低的可能優先權。|  
|**adPriorityNormal**|3|設定為 normal 的優先權。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
