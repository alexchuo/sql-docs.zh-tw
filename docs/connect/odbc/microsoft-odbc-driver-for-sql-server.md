---
title: Microsoft ODBC Driver for SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5142268f69db446dc588af17d7b532ba680c24d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

ODBC 是在 SQL Server 的 C 和 c + + 撰寫的應用程式的主要原生料存取 API。 沒有多數資料來源的 ODBC 驅動程式。 其他可以使用 ODBC 的語言包括 COBOL、 Perl、 PHP 和 Python。 ODBC 廣泛用於資料整合案例。

ODBC 驅動程式隨附工具例如[ **sqlcmd** ](../../tools/sqlcmd-utility.md)和[ **bcp**](../../tools/bcp-utility.md)。 **Sqlcmd**公用程式可讓您執行 TRANSACT-SQL 陳述式、 系統程序和 SQL 指令碼。 **Bcp**公用程式之間大量複製資料的 Microsoft SQL Server 執行個體和資料檔案中您所選擇的格式。 您可以使用**bcp**許多新的資料列匯入 SQL Server 資料表或資料表的資料匯出至資料檔。  

## <a name="code-example-in-c"></a>在 c + + 程式碼範例

下列 c + + 範例示範如何使用 ODBC Api 來連接到並存取資料庫：

- [使用 ODBC 的 c + + 程式碼範例](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>下載

- ![下載 DownArrow Circled](../../ssdt/media/download.png)[若要下載 ODBC 驅動程式](download-odbc-driver-for-sql-server.md)

## <a name="documentation"></a>文件集

### <a name="features"></a>功能

- [自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)
- [資料來源名稱和連接字串關鍵字和屬性](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) （可用的功能也會套用，而 OLEDB，適用於 SQL Server ODBC 驅動程式不）
- [使用永遠加密](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [使用 Azure Active Directory](../../connect/odbc/using-azure-active-directory.md)
- [使用透明網路 IP 解析](../../connect/odbc/using-transparent-network-ip-resolution.md)

### <a name="linux-and-macos"></a>Linux 及 macOS

- [安裝驅動程式](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [連線到 SQL Server](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [使用連接**bcp**](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [使用連接**sqlcmd**](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [資料存取追蹤](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [常見問題集](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [安裝驅動程式管理員](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [已知問題](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [程式設計指導方針](../../connect/odbc/linux-mac/programming-guidelines.md)
- [版本資訊](../../connect/odbc/linux-mac/release-notes.md)
- [支援高可用性和災害復原](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [使用整合式的驗證 (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>視窗

- [非同步執行 (通知方法) 範例](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Windows ODBC 驅動程式中的連接恢復功能](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [可感知驅動程式的連接共用](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [功能與行為變更](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [版本資訊](../../connect/odbc/windows/release-notes.md)
- [系統需求、安裝和驅動程式檔案](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)



## <a name="community"></a>社群  
- [Microsoft ODBC Driver For SQL Server 小組部落格](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server Data Access Forum](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
