---

copyright:

  years:  2016, 2018

lastupdated: "2018-11-01"

---

# Use cases

## VMware workload migration to IBM Cloud

Acme Skateboards wants to seamlessly extend their on-premises VMware SDDC instance into a VCS instance on {{site.data.keyword.cloud}}. They must keep their business up and running and minimize their downtime. Reconfiguring their applications to run in the cloud is not an optimal solution.

The {{site.data.keyword.cloud_notm}} vCenter Server with Hybridity Bundle enables the creation of a seamless connection between VCS instances and an on-premises VMware virtualized datacenter.

The VMware HCX components, which are deployed as virtual machines (VMs) in the VCS target site enable the establishment of a connection with the VMware HCX components installed in the peer on-premises source site.

Figure 1. VMware Hybrid Cloud Extension service
![VMware Hybrid Cloud Extension service](vcsnsxt-hcx-1.svg)

The loosely coupled interconnectivity between on-premises and {{site.data.keyword.cloud_notm}} enables capabilities such as:
-	**Simple interconnectivity** – logical network connections are established easily over any physical connection including public Internet, private VPN, or direct link.
-	**Layer 2 extension** – on-premises networks are extended into the cloud including on-premises subnets and IP addressing.
-	**Encryption** – network traffic is securely encrypted between the two sides.
-	**Optimized network** – selects the best connection and efficiently floods the connection so that network traffic is moved as fast as possible.
-	**Data deduplication** – as much as 50% reduction in network traffic can be achieved.
-	**Intelligent routing** – when a workload is moved, proximity routing can change the network path (that is, gateway) so that network traffic uses the target site gateway and does not “hairpin” back to the originating site.
-	**Zero downtime migration** – a running system can be moved to (or back from) the cloud using vMotion.
-	**Scheduled migration** – any number of VMs can be replicated to the destination site and then activated on that site at a designated time replacing the systems running on the originating site.
-	**Migration of security policies** – if NSX is used on-premises any security policies, firewalls, and so on, are moved along with the workload.

## Hybrid architecture deployment

Acme Skateboards wants to deploy a hybrid architecture on the {{site.data.keyword.cloud_notm}} consisting of vCenter Server with Hybridity Bundle (VCS) and {{site.data.keyword.cloud_notm}} Private (ICP) for their journey to application modernization. Their requirements are to run their databases on VMs, the apps and web interfaces in containers, and would like to use a common set of tools for network and security management.

{{site.data.keyword.vmwaresolutions_short}} provides automation to deploy VMware technology components in {{site.data.keyword.CloudDataCents_notm}} across the globe. The architecture consists of a single cloud region and supports the ability to extend into more cloud regions that are located in another geography and/or into another {{site.data.keyword.cloud_notm}} pod within the same data center.

The ICP and Cloud Automation Manager (CAM) products can be manually deployed into your on-premises virtualization platform enabling cloud management from the on-premises location. Alternatively, ICP and CAM are offered as a service extension to an existing or new VCS deployment enabling cloud management from the {{site.data.keyword.cloud_notm}}.

The following diagram represents ICP running on a VCS instance. NSX-V is configured with a dedicated switch/VXLAN, Distributed Logical Router (DLR), and an Edge Services Gateway (ESG) specifically for the ICP overlay network. Routing is set up through the ESG for access to the underlay network.

Using {{site.data.keyword.cloud_notm}} automation, Acme Skateboards can provision a hybrid solution that encompasses VCS to run their database VMs and ICP on VCS to run their applications and front end web services in containers. NSX gives them a common set of management tools for networking and security in the overlay network.

For more information about NSX-V, see [NSX-V overview](vcsnsxt-overview-ic4vnsxv.html). For more information about the VCS and ICP offering, see [vCenter Server and {{site.data.keyword.cloud_notm}} Private](../vcsicp/vcsicp-intro.html).

Figure 2. VCS with ICP
![VCS with ICP](vcsnsxt-nsxvhl.svg)

This creates a loosely coupled interconnectivity between on-premises and {{site.data.keyword.cloud_notm}} and enables capabilities such as:
-	**Simple interconnectivity** – logical network connections are established easily over any physical connection including public Internet, private VPN, or direct link.
-	**Layer 2 extension** – on-premises networks are extended into the cloud including on-premises subnets and IP addressing.
-	**Encryption** – network traffic is securely encrypted between the two sides.
-	**Optimized network** – selects the best connection and efficiently floods the connection so that network traffic is moved as fast as possible.
-	**Data deduplication** – as much as 50% reduction in network traffic can be achieved.
-	**Intelligent routing** – when a workload is moved, proximity routing can change the network path (that is, gateway) so that network traffic uses the target site gateway and does not “hairpin” back to the originating site.
-	**Zero downtime migration** – a running system can be moved to (or back from) the cloud by using vMotion.
-	**Scheduled migration** – any number of VMs can be replicated to the destination site and then activated on that site at a designated time replacing the systems running on the originating site.
-	**Migration of security policies** – if NSX is used on-premises any security policies, firewalls, and so on, are moved along with the workload.

Using this solution Acme Skateboards was successfully able to migrate their on-premises VMware workloads to the {{site.data.keyword.cloud_notm}} meeting their requirements of little to no downtime and no application reconfiguration. For more information about vCenter Server with Hybridity Bundle, see [VMware HCX on {{site.data.keyword.cloud_notm}} Solution Architecture](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf).

### Related Links

* [VCS Hybridity Bundle overview](../vcs/vcs-hybridity-intro.html)
