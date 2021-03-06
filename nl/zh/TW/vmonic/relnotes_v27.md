---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

# 2.7 版的版本注意事項

此版本包括新增特性、元件更新、可用性加強功能及錯誤修正程式。如需不同版本的已修正問題、產品的已知問題以及使用 {{site.data.keyword.vmwaresolutions_full}} 之提示的清單，請參閱 [{{site.data.keyword.vmwaresolutions_short}} dW Answers](https://developer.ibm.com/answers/topics/cloudvmw/){:new_window}。

## SAP 認證的 6140 伺服器支援

從 2.7 版開始，下列新的 {{site.data.keyword.cloud_notm}} {{site.data.keyword.baremetal_short_sing}} CPU 型號可用於部署 VMware vCenter Server on {{site.data.keyword.cloud_notm}} 及 VMware vSphere on {{site.data.keyword.cloud_notm}} 實例和叢集：
* 雙重 Intel Xeon Gold 6140 處理器 / 總計 36 核心，2.3 GHz / 192 GB RAM
* 雙重 Intel Xeon Gold 6140 處理器 / 總計 36 核心，2.2 GHz / 384 GB RAM
* 雙重 Intel Xeon Gold 6140 處理器 / 總計 36 核心，2.3 GHz / 768 GB RAM

如需相關資訊，請參閱下列主題中的 *{{site.data.keyword.baremetal_short_sing}} 設定* 小節：
* [訂購 vCenter Server 實例](../vcenter/vc_orderinginstance.html#bare-metal-server-settings)
* [訂購新的 vSphere 叢集](../vsphere/vs_orderinginstances.html#bare-metal-server-settings)

## 附加服務的更新

### IBM Cloud Private Hosted

{{site.data.keyword.cloud_notm}} Private Hosted 服務不僅可用於部署在（或升級至）2.5 版或更新版本的 VMware vCenter Server 實例，現在還可用於 VMware vCenter Server with Hybridity Bundle 實例。您現在可以訂購內含該服務的 vCenter Server 實例或 vCenter Server with Hybridity Bundle 實例，也可以在起始部署之後，將該服務新增至現有的 vCenter Server 實例或 vCenter Server with Hybridity Bundle 實例。

如需相關資訊，請參閱：
* [{{site.data.keyword.cloud_notm}} Private Hosted 概觀](../services/icp_overview.html)
* [訂購 {{site.data.keyword.cloud_notm}} Private Hosted](../services/icp_ordering.html)

### Mission Critical VMware on IBM Cloud

Mission Critical VMware on {{site.data.keyword.cloud_notm}} 服務現在可用於部署在（或升級至）2.7 版或更新版本的實例。

Mission Critical VMware on {{site.data.keyword.cloud_notm}} 提供多區域雲端架構，可協助企業避免雲端應用程式的關閉，以及在雲端地區內自動失效接手。與使用內部部署環境或競爭雲端平台的大部分 VMWare 用戶端相較，此雲端架構可讓您達到更高的可用性和失效接手成功率。

如需相關資訊，請參閱 [Mission Critical VMware on {{site.data.keyword.cloud_notm}} 概觀](../services/mcv_overview.html)。

### F5 on IBM Cloud

現在當您訂購 F5 on {{site.data.keyword.cloud_notm}} 服務時，可以選擇要讓 F5 透過公用網路還是透過具有 Proxy 伺服器的專用網路來套用授權。如需相關資訊，請參閱[訂購 F5 on {{site.data.keyword.cloud_notm}}](../services/f5_ordering.html)。

### FortiGate Virtual Appliance on IBM Cloud

Fortinet 已於 2018 年第三季變更其訂閱組合。如需相關資訊，請參閱[訂購 FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}}](../services/fortinetvm_ordering.html)。

對於部署在 2.7 版及更新版本 Cloud Foundation 實例和 vCenter Server 實例中的 FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}} 服務，會佈建 FortiOS 6.0.3。

此外，當您訂購 FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}} 服務時，可以選擇要讓 FortiGuard 透過公用網路還是透過具有 Proxy 伺服器的專用網路來套用授權和安全更新項目。如需相關資訊，請參閱[訂購 FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}}](../services/fortinetvm_ordering.html)。

### Zerto on IBM Cloud 服務元件更新

對於部署在 2.7 版及更新版本 Cloud Foundation 實例和 vCenter Server 實例中的 Zerto on {{site.data.keyword.cloud_notm}} 服務，會佈建 Zerto Virtual Replication 6.0 更新 3。如需相關資訊，請參閱 [Zerto on {{site.data.keyword.cloud_notm}} 概觀](../services/addingzertodr.html)。

### KMIP for VMware on IBM Cloud 與 IBM Cloud Activity Tracker 的整合

除了 VMware 實例事件之外，現在 KMIP for VMware on {{site.data.keyword.cloud_notm}} 實例的事件（例如金鑰建立、金鑰刪除及金鑰存取）也會與 {{site.data.keyword.cloud_notm}} Activity Tracker 實例整合。如需 KMIP for WMware on {{site.data.keyword.cloud_notm}} 的相關資訊，請參閱 [KMIP for VMware on {{site.data.keyword.cloud_notm}} 概觀](../services/kmip_considerations.html)。

## 新文件與更新的文件

### 參照架構文件

現在可於使用者說明文件的*參照* 小節中取得下列技術文件：

* [NSX Edge Services Gateway 解決方案架構](../archiref/nsx/nsx_overview.html)
* [VMware Update Manager 手冊](../archiref/vum/vum-intro.html)
* [vCenter Server 網路手冊](../archiref/vcsnsxt/vcsnsxt-intro.html)
* [vCenter Server 和 {{site.data.keyword.cloud_notm}} Private 手冊](../archiref/vcsicp/vcsicp-intro.html)
* [vCenter Server 和 IBM Kubernetes 服務手冊](../archiref/vcsiks/vcsiks-intro.html)
* [VMware 和 Skate Advisor 概念汽車手冊](../archiref/vcscar/vcscar-intro.html)
* [VMware：Stock Trader 的現代化旅程](../archiref/vcscontent/vcscontent-modjourney.html)

上述部分參照架構文件僅提供英文版。

## 使用者介面更新和加強功能

使用者介面已更新，並提供下列加強功能：

* 當您訂購實例時，用來為 {{site.data.keyword.baremetal_short_sing}} 設定指定 CPU 型號和 RAM 的原始**自訂**標籤，會根據伺服器類型分成 **Skylake** 標籤和 **Broadwell** 標籤，以協助您選取伺服器。
* 現在**類型**直欄內含在**已部署的實例**頁面上的 **vCenter Server 實例**表格中，用來識別 vCenter Server、vCenter Server with Hybridity Bundle 和 vCenter Limited Test Drive 實例。
* 提供各種錯誤訊息及工具提示加強功能，以協助您在使用者介面上選取適當的設定。
