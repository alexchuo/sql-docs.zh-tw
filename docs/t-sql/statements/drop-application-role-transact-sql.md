---
title: DROP APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_APPLICATION_ROLE_TSQL
- DROP APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- dropping application roles
- deleting application roles
- removing application roles
- application roles [SQL Server], removing
- DROP APPLICATION ROLE statement
ms.assetid: 44121ee7-ef40-405d-b03b-f8ddb4e3c559
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6e793400429dcbb74ff5ae09f25613a351c3aede
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="drop-application-role-transact-sql"></a>DROP APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從目前資料庫移除應用程式角色。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP APPLICATION ROLE rolename  
```  
  
## <a name="arguments"></a>引數  
 *rolename*  
 指定要卸除之應用程式角色的名稱。  
  
## <a name="remarks"></a>Remarks  
 如果應用程式角色擁有任何安全性實體，則無法將之卸除。 在卸除擁有安全性實體的應用程式角色之前，必須先傳送或卸除安全性實體的擁有權。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。  
  
## <a name="examples"></a>範例  
 從資料庫卸除應用程式角色 "weekly_ledger"。  
  
```  
DROP APPLICATION ROLE weekly_ledger;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
