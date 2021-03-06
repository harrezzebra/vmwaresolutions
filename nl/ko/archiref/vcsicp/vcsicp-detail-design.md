---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-10"

---

# 자세한 디자인

## 공통 서비스 컴포넌트
공통 서비스는 클라우드 관리 플랫폼의 기타 서비스에서 사용하는 서비스를 제공합니다. 여기에는 ID 및 액세스 서비스, Domain Name Service, NTP 서비스가 포함됩니다.

그림 1. ICP 공통 서비스

![ICP 공통 서비스](vcsicp-icp-commonservices.svg)

### ID 및 액세스 서비스
VCS 자동화의 일부로 Microsoft Active Directory(AD)는 ID 관리에 사용됩니다. 단일 AD VSI(Virtual Server Instance)가 배치됩니다. vCenter는 MS AD 인증을 이용하도록 구성되며 ICP도 LDAP 인증에 대해 구성할 수 있습니다.

###	Domain Name Service
VCS 배치에서는 배치된 Microsoft Active Directory(AD) VSI를 인스턴스에 대한 DNS 서버로 이용합니다. 배치된 모든 컴포넌트(vCenter, PSC, NSX 및 ESXi 호스트)는 기본 DNS로 MS AD를 가리키도록 구성됩니다. 

###	NTP 서비스
VCS 배치는 IBM Cloud 인프라 NTP 서버를 활용합니다. 배치된 모든 컴포넌트는 이러한 NTP 서버를 활용하도록 구성됩니다. 동일한 NTP 서버를 활용하여 디자인 내에 모든 컴포넌트를 보유하는 것은 인증서와 MS AD 인증이 올바르게 작동하기 위해 반드시 필요합니다.

## 네트워킹

### NSX-V 네트워킹

NSX-V는 단일 NSX-V 관리자 플랫폼이 단일 vCenter Server 인스턴스에 연결되도록 설계되었습니다. vSphere 환경 내에서 실행 중인 애플리케이션에 네트워킹 서비스를 제공합니다.

VCS 배치에 포함된 NSX-V 네트워킹을 활용하면 ICP를 VXLAN 오버레이 네트워크에 배치할 수 있습니다.

ICP는 Kubernetes에 대한 기본 Calico 네트워킹 스택을 사용하여 배치되며, 클러스터 내에서 네트워크 격리를 제공합니다.

그림 2. NSX-V 네트워킹을 사용하는 ICP

![NSX-V 네트워킹을 사용하는 ICP](vcsicp-nsxv-networking.svg)

자세한 정보는 [IBM Cloud VCS 네트워킹 참조 아키텍처](../vcsnsxt/vcsnsxt-intro.html)를 참조하십시오. 

### NSX-T 네트워킹

NSX-T는 모든 유형의 애플리케이션에 연결할 수 있는 단일 네트워킹 플랫폼이 가상 머신 또는 컨테이너 기반이 되고, vSphere 환경 내부 또는 외부에서 실행할 수 있도록 설계되었습니다. 

ICP는 Calico 네트워킹을 NSX-T 인스턴스로 대체하기 위한 옵션을 제공하며 네트워킹 및 보안 관리를 위한 단일 위치를 제공합니다. 

그림 3. NSX-T 네트워킹을 사용하는 ICP

![NSX-T 네트워킹을 사용하는 ICP](vcsicp-icp-nsxt-networking.svg)

### 관련 링크

* [VMware vCenter Server on IBM Cloud with Hybridity Bundle](../vcs/vcs-hybridity-intro.html)
