---
title: 設定 SQL Server 可用性群組的 Ubuntu 叢集 |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: d9e41a09fdd76f060fcf34d33d7463984ae942a6
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>設定 Ubuntu 叢集和可用性群組資源

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文件說明如何在 Ubuntu 上建立三個節點叢集並加入先前建立的可用性群組為叢集中的資源。 高可用性，Linux 上的可用性群組需要三個節點-請參閱[的可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)。

> [!NOTE] 
> 此時，不是與使用 Windows 上的 WSFC 為結合與 Pacemaker Linux 上的 SQL Server 的整合。 從 SQL、 內沒有存在叢集的認知、 所有協調流程中，超出和服務由 Pacemaker 控制做為獨立執行個體。 此外，虛擬網路名稱是屬於 WSFC、 沒有對等的 Pacemaker 中相同。 在 alwayson 動態管理檢視的查詢叢集資訊傳回空的資料列。 您仍然可以建立來做為透明的重新連線到容錯移轉之後，接聽程式，但您必須手動註冊接聽程式名稱在 DNS 伺服器 IP 用來建立虛擬 IP 資源 （如下列各節所述）。

下列各節逐步解說的步驟來設定容錯移轉叢集解決方案。 

## <a name="roadmap"></a>藍圖

在高可用性的 Linux 伺服器上建立可用性群組的步驟會與不同的 Windows Server 容錯移轉叢集的步驟。 下列清單描述的概要步驟： 

1. [設定 SQL Server 叢集節點上](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-configure-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 這些指示是本文件中。
   
   設定叢集資源管理員的方式取決於特定 Linux 發佈。 

   >[!IMPORTANT]
   >實際執行環境中需要隔離代理程式，例如 STONITH 高可用性。 在本文件示範請勿圍欄代理程式。 此示範的使用者是用於測試和驗證。 
   
   >Linux 叢集使用圍欄叢集回到已知狀態。 設定範圍的方式取決於分佈和環境。 此時，圍欄不適用於某些雲端環境中。 請參閱[RHEL 的高可用性叢集-而虛擬化平台的支援政策](https://access.redhat.com/articles/29440)如需詳細資訊。

5.  [新增可用性群組為叢集中資源](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝和設定每個叢集節點上 Pacemaker

1. 在所有節點上開啟防火牆連接埠。 開啟 Pacemaker 高可用性服務、 SQL Server 執行個體和可用性群組端點連接埠。 執行 SQL Server 伺服器的預設 TCP 通訊埠為 1433年。  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   或者，您可以只停用防火牆：
        
   ```bash
   sudo ufw disable
   ```

1. 安裝 Pacemaker 封裝。 所有節點上，執行下列命令：

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 在所有節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>啟用和啟動 pcsd 服務和 Pacemaker

下列命令會啟用，並啟動 pcsd 服務和 pacemaker。 所有節點上執行。 這可讓要重新開機後重新加入叢集的節點。 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>啟用 pacemaker 命令可能會完成，發生錯誤 'pacemaker 預設開始包含沒有 runlevels，正在中止'。 這是無害的可以繼續叢集組態。 

## <a name="create-the-cluster"></a>建立叢集

1. 從所有節點中移除任何現有的叢集設定。 

   執行 'sudo apt get 安裝電腦' 同時安裝 pacemaker、 corosync 和電腦，並開始執行所有 3 個服務。  啟動 corosync 產生範本 ' / etc/cluster/corosync.conf' 檔案。  若要將這個檔案會成功的下一個步驟應該不存在 – 所以因應措施是停止 pacemaker / corosync 和刪除 ' / etc/cluster/corosync.conf'，然後後續步驟已順利完成時。 '電腦叢集 destroy' 進行相同的工作，以及您可以將它當做一個時間最初的叢集安裝步驟。
   
   下列命令會移除任何現有的叢集組態檔，並停止所有的叢集服務。 這會永久終結叢集。 預先生產環境中的第一個步驟中執行它。 請注意，'電腦叢集 destroy' 已停用 pacemaker 服務和可重新啟用的需求。 在所有節點上執行下列命令。
   
   >[!WARNING]
   >此命令會破壞任何現有的叢集資源。

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. 建立叢集。 

   >[!WARNING]
   >由於已知的問題，叢集的廠商調查，啟動叢集 ('電腦叢集 start') 失敗，發生下列錯誤。 這是因為這建立叢集安裝命令時執行，此為錯誤 /etc/corosync/corosync.conf 中設定的記錄檔。 若要解決此問題，請將變更的記錄檔： /var/log/corosync/corosync.log。 或者，您可以建立 /var/log/cluster/corosync.log 檔案。
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
下列命令會建立三個節點叢集。 執行指令碼之前，請取代 `< ... >` 之間的值。 在主要節點上執行下列命令。 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2…> <node3>
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >如果您先前已在相同節點上設定叢集，執行 'pcs cluster setup' 時需要使用 '--force' 選項。 請注意，這相當於執行 'pcs cluster destroy'，而且需要使用 'sudo systemctl enable pacemaker' 來重新啟用 Pacemaker 服務。


## <a name="configure-fencing-stonith"></a>設定範圍 (STONITH)

Pacemaker 叢集廠商需要啟用 STONITH 和圍欄裝置設定為支援的叢集安裝。 當叢集資源管理員無法判斷狀態的節點或節點上的資源時，隔離會用於叢集讓已知狀態重新。 資源層級範圍主要是確保所設定的資源設定是中斷發生的任何資料損毀。 您可以使用資源層級的範圍，比方說，DRBD （分散式複寫區塊裝置） 來標示為過期時的節點上的磁碟使用的通訊連結中斷。 節點層級圍欄可確保節點不會執行任何資源。 這是藉由重設節點和它的 Pacemaker 實作稱為 STONITH （它代表"羊標頭中的另一個節點 」）。 Pacemaker 支援很棒的各種圍欄裝置，例如不斷電供應系統或管理介面卡的伺服器。 如需詳細資訊，請參閱[從頭 Pacemaker 叢集](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)和[圍欄和 Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

因為節點層級範圍組態高度取決於您的環境，我們停用它 （它可以設定在稍後） 在此教學課程。 在主要節點上執行下列指令碼： 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>停用 STONITH 只適用於測試目的。 如果您打算使用 Pacemaker 實際執行環境中，您應該規劃 STONITH 實作，根據您的環境，並保持啟用。 請注意，此時有任何雲端環境 （包括 Azure） 或 HYPER-V 沒有圍欄代理程式。 因此，叢集供應商不提供支援在這些環境中執行生產叢集。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定叢集屬性叢集重新檢查間隔

`cluster-recheck-interval` 指出的輪詢間隔的叢集檢查有變更的資源參數、 條件約束或其他叢集的選項。 如果複本關閉，叢集會嘗試重新啟動的時間間隔是由繫結的複本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`設為 60 秒及`cluster-recheck-interval`設定為 120 秒，超過 60 秒，但小於 120 秒的間隔嘗試重新啟動。 我們建議您將失敗逾時設定為 60 秒及叢集重新檢查的間隔為大於 60 秒的值。 建議您不要將叢集重新檢查間隔設定為較小的值。

若要更新的屬性值`2 minutes`執行：

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果您已經有由 Pacemaker 叢集管理可用性群組資源，請注意使用最新可用 Pacemaker 封裝 1.1.18-11.el7 的所有分佈都造成啟動失敗-是-嚴重的叢集設定時的行為變更其值為 false。 這項變更會影響容錯移轉工作流程。 如果主要複本發生中斷，叢集必須容錯移轉至其中一個可用的次要複本。 相反地，使用者會發現，叢集會嘗試啟動失敗的主要複本。 如果該主永遠不會上線時 （因為在永久中斷），叢集絕不會容錯移轉至另一個可用的次要複本。 由於此項變更，先前建議的設定，來設定開始失敗-是-嚴重已不再有效，此設定需要還原為其預設值`true`。 此外，必須更新，以包含 AG 資源`failover-timeout`屬性。 
>
>若要更新的屬性值`true`執行：
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>更新您現有的 AG 資源屬性`failure-timeout`至`60s`執行 (取代`ag1`具有可用性群組資源的名稱):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>使用 Pacemaker 安裝 SQL Server 資源的代理程式進行整合

在所有節點上執行下列命令。 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 建立的 SQL Server 登入

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>建立可用性群組資源

若要建立可用性群組資源，請使用`pcs resource create`命令，並設定資源屬性。 下列命令會建立`ocf:mssql:ag`主/從可用性群組名稱的型別資源`ag1`。 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>建立虛擬 IP 資源

若要建立虛擬 IP 位址資源，請在一個節點上執行下列命令。 使用 從網路可用的靜態 IP 位址。 執行指令碼之前，請將之間的值取代`< ... >`具有有效的 IP 位址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

沒有 Pacemaker 中相等的虛擬伺服器名稱。 若要使用連接字串指向字串伺服器名稱並不會使用 IP 位址，請在 DNS 中登錄所需的虛擬伺服器名稱與資源的 IP 位址。 DR 組態註冊所需的虛擬伺服器名稱和 IP 位址與主要和 DR 網站上的 DNS 伺服器。

## <a name="add-colocation-constraint"></a>加入共置條件約束

藉由比較分數是在 Pacemaker 叢集中，例如選擇應在何處資源執行，幾乎每個決策。 分數計算每個資源，並叢集資源管理員選擇特定資源的分數最高的節點。 （如果節點具有負數資源的分數，該節點上即無法執行資源）。若要設定叢集的決策中使用條件約束。 分數是條件約束。 如果條件約束的分數低於無限大，則僅供建議。 分數無限大的表示是強制性。 若要確保主要複本和虛擬 ip 資源位於相同的主機，定義分數為無限大的共置條件約束。 若要加入的共置條件約束，請在一個節點上執行下列命令。 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>加入排序條件約束

共置條件約束具有隱含的排序條件約束。 它會移動虛擬 IP 資源之前它會將可用性群組資源移動。 依預設事件的順序為：

1. 使用者發出`pcs resource move`至可用性群組主要複本從 node1 到 node2。
1. 虛擬 IP 資源停止 node1 上。
1. 在 node2 上，啟動虛擬 IP 資源。

   >[!NOTE]
   >這個時候的 IP 位址暫時指向 node2 當 node2 仍前容錯移轉時次要。 
   
1. 在 node1 上的主要可用性群組已降級為次要。
1. 在 node2 上的次要可用性群組會提升為主要。 

若要防止暫時指向與前容錯移轉的次要節點的 IP 位址，請加入排序條件約束。 

若要加入排序條件約束，請在一個節點上執行下列命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>您設定叢集，並新增為叢集資源的可用性群組之後，您無法使用 TRANSACT-SQL 來容錯移轉可用性群組資源。 在 Linux 上的 SQL Server 叢集資源不搭配嚴格作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的存在。 所有的協調流程會透過叢集管理工具。 在 RHEL 或 Ubuntu 使用`pcs`。 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>後續的步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)

