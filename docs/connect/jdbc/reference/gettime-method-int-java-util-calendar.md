---
title: getTime 方法 （int，java.util.Calendar） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 87b7fbaf-7149-494f-b3b2-16b468a8ebf1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0e01aa8c9bb2f0f7e4f7ea38e9bcdda4dd128b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="gettime-method-int-javautilcalendar"></a>getTime 方法 (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的值來當做 java.sql.Time 物件在 Java 程式語言中，給定的參數索引，使用指定的行事曆物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Time getTime(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 指出參數索引的 **int**。  
  
 *cal*  
  
 行事曆物件。  
  
## <a name="return-value"></a>傳回值  
 Time 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetTime 方法 java.sql.CallableStatement 介面中所指定此 getTime 方法。  
  
 請參閱標題為 「 Getter 方法轉換 」 圖表[了解資料類型轉換](../../../connect/jdbc/understanding-data-type-conversions.md)查看哪些[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]採用這種方法可擷取的資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [getTime 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
