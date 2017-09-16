---
title: "InfoMessage 事件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f1e479b4dfb5b9cb557030e03afeac3f6278720
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="infomessage-event-ado"></a>InfoMessage 事件 (ADO)
**InfoMessage**期間發生警告時，會呼叫事件**ConnectionEvent**作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 這個參數會包含會傳回任何錯誤。 如果傳回多個錯誤，列舉**錯誤**來尋找客戶的集合。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 發生警告*adStatus*設**adStatusOK**和*pError*含有警告。  
  
 這個事件會傳回之前，請將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pConnection*  
 A[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 發生警告的連接。 例如，開啟時可能會發生警告**連接**物件或執行[命令](../../../ado/reference/ado-api/command-object-ado.md)上**連接**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)