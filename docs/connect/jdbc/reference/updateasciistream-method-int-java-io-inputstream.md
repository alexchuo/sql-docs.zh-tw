---
title: updateAsciiStream 方法 (java.io.InputStream) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1dcc3d4f-ae30-45c0-afad-a531358807af
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a98f78397a2bd9b86b788c696ad13c11f5e9dbe9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updateasciistream-method-int-javaioinputstream"></a>updateAsciiStream 方法 (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 ASCII 資料流值，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateAsciiStream 方法 java.sql.ResultSet 介面中所指定此 updateAsciiStream 方法。  
  
 這個方法將 ASCII 字元 （位元組） 從 InputStream 物件傳遞至轉換字元資料行，也就是 ASCII 範圍 [0x00 – 0x7F] 的 Unicode，以及 874、 932、 936、 949、 950 和 1250 到 1258年的字碼頁。 這個方法會執行轉換，直到目的地定序頁面。 嘗試更新無法轉換的目的地資料行，將擲回例外狀況。 若是處理二進位資料行，則會傳遞未經處理位元組。  
  
 使用這個方法來**映像**，**文字**，和**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別可能會影響效能。  
  
## <a name="see-also"></a>另請參閱  
 [updateAsciiStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
