---
title: 完成安裝後步驟 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: distributed-replay
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 12bdc7fbea96f7af42f7b2a1f175e58fc03c0b6c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="complete-the-post-installation-steps"></a>完成安裝後步驟
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  安裝 Distributed Replay 之後，必須修改 Distributed Replay 控制器及用戶端服務帳戶。  
  
### <a name="to-complete-the-post-installation-steps"></a>若要完成後續安裝步驟  
  
1.  **建立防火牆規則**：在控制器和用戶端電腦上，您必須允許輸入流量通過對應服務的防火牆。 請針對服務可執行檔 (位於安裝資料夾中) 指定防火牆規則。  
  
    1.  對於控制器服務，請為安裝資料夾中的 **DReplayController.exe**建立規則。 例如，下列命令會啟用這項規則，其中 `%InstallPath%` 是服務的安裝資料夾：  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  對於每部用戶端電腦上的用戶端服務，請為安裝資料夾中的 **DReplayClient.exe**建立規則。 例如，下列命令會啟用這項規則，其中 `%InstallPath%` 是服務的安裝資料夾：  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **將目標伺服器的權限授與每個用戶端**：當您已經完成在用戶端電腦上安裝用戶端服務的作業之後，就必須手動將用戶端服務帳戶加入目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的系統管理員角色。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 您必須具備管理權限，才可安裝各種 Distributed Replay 功能。 只有擁有系統管理員權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入能夠將用戶端服務帳戶加入測試伺服器的系統管理員伺服器角色。 如需 Distributed Replay 安全性考量的詳細資訊，請參閱 [Distributed Replay 安全性](../../tools/distributed-replay/distributed-replay-security.md)。  
  
  
