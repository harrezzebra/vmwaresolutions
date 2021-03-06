---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

#	收集 meta 資料

VUM 會透過您可以修改的預先定義自動處理程序，下載有關升級、修補程式或延伸規格的 meta 資料。VUM 會依一般可配置的間隔聯絡 VMware 或協力廠商來源，以收集有關可用升級、修補程式或延伸規格的最新 meta 資料。不過，可接受 VMware 中的預設值以用於 VCS 實例，您可以視需要針對企業需求變更它們。

VUM 會顯示 vSAN 所產生的系統管理基準線。系統管理的基準線會定期自動更新其內容，這需要 VUM 固定存取網際網路。vSAN 系統基準線通常每 24 小時會重新整理一次。

您可以使用系統管理的基準線，將您的 vSAN 叢集升級為建議的重要修補程式、驅動程式、更新或適用於 vSAN 的最新支援 ESXi 主機版本。

對於大部分企業，VUM 的 VMware 預設值視為適合。如果您的企業要使用不同的設定，則下列提供如何變更這些設定的說明。

##	下載排程
更新是虛擬應用裝置升級、主機修補程式及延伸規格，而且依預設 VUM 會每天下載更新。此作業的變更方式是存取 vSphere Web Client，導覽至**首頁** > **Update Manager** > **管理** > **設定**，然後選取**下載排程**，再按一下**編輯**。

##	通知檢查排程
通知是修補程式取消、新修正程式及警示的相關資訊，而且依預設 VUM 會每小時下載通知。此作業的變更方式是存取 vSphere Web Client，導覽至**首頁** > **Update Manager** > **管理** > **設定**，然後選取**通知檢查排程**，再按一下**編輯**。

##	VM 設定
若要變更「VM 設定」，請存取 vSphere Web Client，導覽至**首頁** > **Update Manager** > **管理** > **設定**及 **VM 設定**，然後按一下**編輯**。

##	主機/叢集設定
若要變更「主機/叢集設定」，請存取 vSphere Web Client，導覽至**首頁** > **Update Manager** > **管理** > **設定**及**主機/叢集設定**，然後按一下**編輯**。

### 相關鏈結

* [VMware HCX on IBM Cloud 解決方案架構](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [VMware Solutions on IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware)（展示）
