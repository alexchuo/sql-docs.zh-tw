---
title: jdbcCompliant 方法 (SQLServerDriver) |Microsoft 文件
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
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 357024153bb862ff369278096018dd544ead4ca8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>jdbcCompliant 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  確認[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]是否符合 JDBC 規格。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果 JDBC 驅動程式符合最低需求。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 這個 jdbcCompliant 方法是由 java.sql.Driver 介面中 jdbcCompliant 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成員](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 類別](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
