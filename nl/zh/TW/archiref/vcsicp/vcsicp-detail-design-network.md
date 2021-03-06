---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-10"

---

# 網路存取和流程

## 容器應用程式存取 – ICP

有三種主要方式可以取得外部資料流量/存取至您的 Kubernetes 叢集應用程式中：
- NodePort
- LoadBalancer
- Ingress

### NodePort
Nodeport 是公開外部存取工作負載的一種簡單方法，適用於起始開發和測試，但不建議用於正式作業。Ingress 或負載平衡器是建議的路徑。

### LoadBalancer
目前，「ICP 平台」可針對應用程式工作負載支援外部「負載平衡器」。

### Ingress
Ingress 是讓入埠連線聯繫叢集服務的規則集合。它可以配置為將下列項目提供給服務：可外部聯繫的 URL、負載平衡資料流量、終止 SSL、提供名稱型虛擬主機作業等等。ICP 基礎架構中的 Proxy 節點會執行此功能。

## 容器應用程式存取 – IKS
有三種主要方式可以取得外部資料流量/存取至您的 Kubernetes 叢集應用程式中：
- NodePort
- LoadBalancer
- Ingress

### NodePort
Nodeport 是公開外部存取工作負載的一種簡單方法，適用於起始開發和測試，但不建議用於正式作業。Ingress 或負載平衡器是建議的路徑。

### LoadBalancer
每個 IKS 叢集都會佈建一個公用/專用「應用程式負載平衡器 (ALB)」。ALB 使用安全且唯一的公用或專用進入點，將送入的要求遞送至您的應用程式。

### Ingress
Ingress 是讓入埠連線聯繫叢集服務的規則集合。它可以配置為將下列項目提供給服務：可外部聯繫的 URL、負載平衡資料流量、終止 SSL、提供名稱型虛擬主機作業等等。

## 資料傳輸流
將說明下列資料傳輸流：
- 網際網路上的外部使用者到 ICP 的容器中管理的 Web 層級。
- ICP 的容器中管理的 Web 層級到 VCS 的 VM 中管理的資料庫層級。
- 組織網路上的企業使用者存取 VCS 中的 VM。

### 網際網路上的外部使用者到 ICP 的容器中管理的 Web 層級。
1. 外部使用者使用 URL 向 Web 層級提出要求。
2.	使用 DNS 來判斷 IP 位址。此 IP 位址會是已指派給「VCS 實例」之可攜式子網路上的 IBM Cloud 公用位址。
3.	公用網路會自動將要求轉遞至管理 ESG 的 vSphere ESXi 主機。
4.	ESG 會將要求轉遞至 ALB 或 Ingress 服務的內部叢集 IP 位址和埠號。如果 ESG 和 ALB 或 Ingress 服務在不同的 vSphere ESXi 主機上，則會將 IP 封包封裝在 VXLAN 框架中。這個內部叢集 IP 位址只能在叢集內部存取。
5.	在工作者節點內，kube-proxy 會將要求遞送至 ALB 或 Ingress 服務。
6.	如果應用程式位於同一個工作者節點上，則會使用 iptables 來判定用來轉遞要求的內部介面。如果應用程式位於不同的工作者節點上，則 Calico vRouter 會使用 IP-in-IP 封裝，遞送至適用的工作者節點。IP-in-IP 封包會封裝在 VXLAN 框架中，以傳輸至工作者節點所在的 vSphere ESXi 主機。

### ICP 的容器中管理的 Web 層級到 VCS 的 VM 中管理的資料庫層級。
ESG 和 vRouters 中的路徑表格移入方式，取決於整合的方法。請參閱「ICP 與 VCS 整合」。
1.	在 ICP 的容器中執行的 Web 層級向在相同 VCS 實例中之 VM 上執行的資料庫提出要求。
2.	使用 DNS 將要求解析成資料庫的 IP 位址。
3.	容器將要求傳送至 Calico vRouter。
4.	vRouter 在其路徑表格中移入 VCS 實例上所管理的 IP 位址範圍。
5.	vRouter 轉遞要求，但會使用 SNAT 將來源 IP 位址從 Pod 的 IP 位址變更為工作者節點的 IP 位址。
6.	管理 vRouter 的工作者節點將要求傳送至 ESG。
7.	然後，ESG 轉遞至 DLR。
8.	DLR 將要求置於必要的 VXLAN 上。
9.	資料庫 VM 接收要求。

### 	組織網路上的企業使用者存取 VCS 中的 VM
1.	連接至企業內部網路的企業使用者要求 VCS 中管理之 VM 上的資源。
2.	使用 DNS 來判斷 VM 的 IP 位址。此 IP 位址位於已延伸至 IBM Cloud 的網路上。
3.	內部部署路由器將資料流量導向管理「L2 集中器」的 vSphere 主機。
4.	「L2 集中器」將要求封裝在安全通道中，並透過內部部署路由器，使用指派給裝置的專用可攜式子網路 IP 位址，將其轉遞至 IBM Cloud 中所管理的遠端「L2 集中器」。
5.	內部部署路徑會查看其遞送表，並分辨出遠端「L2 集中器」的 IP 位址需要而傳送至 WAN 介面，其藉由 BCR 透過 IBM Cloud XCR 路由器在 WAN 上轉遞。
6.	「L2 集中器」接收要求，並將其置於管理延伸網路的 VXLAN 上。
7.	VM 接收要求。

## 公用存取網路
依預設，ICP 和 CAM 需要網際網路連線功能，才能擷取 Docker 映像檔、Helm 圖表、Terrform 範本和作業系統套件管理程式。在最新版本中，現在可以支援以 Proxy 為基礎的安裝，可安裝未直接連接至網際網路的安裝，並可選擇以離線模式進行安裝。

###	NSX 防火牆
ICP NSX Edge 防火牆配置的規則可以：
*	讓 VXLAN 網路存取公用存取。
*	讓 VXLAN 網路存取專用 IBM Cloud 網路存取。
*	讓專用 IBM Cloud 網路存取 VXLAN 網路。

### NSX NAT
ICP NSX NAT 配置下列 NAT：
*	SNAT，讓 VXLAN 網路存取公用存取。
*	SNAT，讓 VXLAN 網路存取專用 IBM Cloud 網路存取。
*	DNAT，適用於 ICP 叢集 vIP。

### 相關鏈結

* [VMware vCenter Server on IBM Cloud with Hybridity Bundle](../vcs/vcs-hybridity-intro.html)
