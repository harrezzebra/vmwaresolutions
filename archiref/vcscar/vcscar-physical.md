---

copyright:

  years:  2016, 2018

lastupdated: "2018-11-01"

---

# Skate Advisor components

{{site.data.keyword.vmwaresolutions_full}} provides automation to deploy VMware
technology components in {{site.data.keyword.CloudDataCents_notm}} across the globe. The
architecture consists of a single cloud region and supports the ability
to extend into more cloud regions that are located in another
geography and/or into another {{site.data.keyword.cloud_notm}} pod within the same data center.

The {{site.data.keyword.cloud_notm}} Private (ICP) and Cloud Automation Manager (CAM) products
can be manually deployed into your on-premises virtualization platform,
enabling cloud management from on-premises locations. Alternatively, ICP
and CAM are offered as service extensions to an existing or new VMware
vCenter Server on {{site.data.keyword.cloud_notm}} (VCS) deployment, via automation, enabling
cloud management from {{site.data.keyword.cloud_notm}}.

ICP is an application platform for developing and managing on-premises,
containerized applications. It is an integrated environment for managing
containers that includes the container orchestrator Kubernetes, a
private image repository, a management console, and monitoring
frameworks.

IBM Multi-cluster Manager provides user visibility, application-centric
management (policy, deployments, health, operations), and policy-based
compliance across clouds and clusters. With IBM Multi-Cluster Manager,
you have control of your Kubernetes clusters. You can ensure that your
clusters are secure, operating efficiently, and delivering the service
levels that applications expect.

{{site.data.keyword.cloud_notm}} Automation Manager is a multi-cloud, self-service management
platform running on {{site.data.keyword.cloud_notm}} Private that empowers developers and
administrators to meet business demands. Cloud Automation Manager
Service Composer allows you to expose hybrid cloud services in the IBM
Cloud Private catalog.

## Skate Advisor components

The following diagram describes the reference implementation of the Acme
Skate Advisor application in an application modernization infrastructure
implementation.

Figure 1. Skate Advisor physical components
![Skate Advisor physical components](vcscar-physical.svg)

The Skate Advisor application extends the existing Acme web application
with a micro-services based component that interacts with Watson and an
nginx container to proxy requests to the web and micro-services
container.

The Skate Advisor application takes advantage of the application
modernization platform that provides the necessary hosting
infrastructure.

### Application packaging and deployment

The application is deployed as a CAM Orchestration which containers the
following elements:

Figure 2. CAM orchestration
![CAM orchestration](vcscar-cam.svg)

These elements are described as follows:
* Service Orchestration - A CAM service orchestration is a workflow
resource that describes the Terraform templates and Helm charts to
deploy as a facet of a service. A service can be published and is the
controlling artifact from which the entire deployment is orchestrated.
* Helm Chart - The Helm chart resides in the local ICP
Repository and deploys containers and other resources to ICP. A Helm
chart is a description of Kubernetes resources including:
 - Container deployments
 - Services
 - Ingress
 - Rules
 - Endpoints

* Docker Images - Docker images contain the operating system (ubuntu),
the middleware (WebSphere Liberty, nginx), and the Skate Advisor and
Skate Store code. Docker images are static objects that are deployed
into running containers.
* Terraform Template - A Terraform template is a file that describes
cloud resources to be deployed. For Skate Advisor, a ubuntu
template, which has been pre-loaded with mysql and the database schema is
described.
* VMWare Template - The VMWare template is an Ubuntu template with mysql
and the database schema pre-loaded.

### Load balancing and proxying

Load balancing and proxying are implemented via the ICP Ingress
Controller component. This component handles the container scaling
and failover in a seamless manner.

Application proxying is provided by the nginx container which load
balances in the following manner.

Table 1. Skate Advisor reverse proxy rules

URL	|EndPoint
---|---
/acme	|Acme Web Container Service
/acme/api	|Skate Advisor Service
/acme/api/explorer	|Skate Advisor Service

Containers have unpredictable IP address that might scale in and out as
the system demands. To overcome this, the ICP services are utilized to
perform real-time IP address resolution within the system.

### Acme skate web application
The Acme Skate web application is a Java Platform, Enterprise Edition (J2EE) application based on the Spring
Framework. The application is deployed on a WebSphere Liberty container.

### Acme Skate Advisor application
The Acme Skate Advisor application is a micro-service based application that is deployed on a WebSphere Liberty container. An nginx web server provides
a front end to the micro-services.

### Acme Skate database
The Acme Skate database is a MySQL database that is deployed on a
vSphere managed virtual machine.

### Communications overview
The Skate Advisor requires the following communications:
-	From the web container to the system user.
-	From the Advisor and web container to Watson services.
-	Between the container and the virtual machine aspects of the
implementation.

The application modernization platform has been designed with the
following components to achieve this goal.

Figure 3. Public network access
![Public network access](vcscar-network.svg)

{{site.data.keyword.cloud_notm}} has two networks. The public network allows servers to be
reached from the Internet and the private network allows servers to
communicate with each other over a high-speed backbone in all {{site.data.keyword.CloudDataCents_notm}}.

The Virtual Routing Appliance (VRA) allows customers to route private
and public network traffic by associating the VLANs with the appliance.
Both the vCenter Server NSX Edge and IKS infrastructure are configured
with a default route to the public network and with a standard
10.0.0.0/8 route to the private network.

A static route is required on the IKS infrastructure to the VRA
appliance for any NSX VXLANs defined. From the NSX Edge, we configure
BGP peering with the VRA over the private network, enabling route
advertisement/interjection of the NSX VXLANs. This peering allows the
NSX VXLAN overlay network to communicate with the {{site.data.keyword.cloud_notm}} backbone and
vice versa.

### Software Component Mapping

The Skate Advisor application utilized the following software
components.

Figure 4. Skate Advisor software mapping
![Skate Advisor software mapping](vcscar-sw-mapping.svg)

The following software components are utilized:

* nginx	- Provides reverse proxy services to the application.
Micro-services and application requests are distributed to the correct
container endpoints.
* WebSphere Liberty - hosts the Acme application, which is a Spring-based
J2EE application.
* Node.js - Provides the micro-services framework to the chatbot. This
application consumes services from Watson.
* mysql - The application database is provided by Oracle Mysql.
* JavaScript - The chatbot is a JavaScript based
application that is hosted in the client Browser. The chatbot
communicates with Watson via the Node.js based micro-services.

## Management overview

The Acme Skate Advisor resides on the {{site.data.keyword.cloud_notm}} and as such is a
critical aspect of the Architecture. The {{site.data.keyword.cloud_notm}} has the following
architecture.

Figure 5. Cloud management
![On-cloud management](vcscar-cloud-management.svg)

The diagram above represents ICP and CAM deployed on a vCenter
Server instance, with connections to the on-premises vCenter and the IKS
service. Using CAM, system administrators and developers are able to
deploy virtual machines on-premises or into the vCenter Server instance
and containers to the ICP and IKS clusters.

In the diagram, CAM logically creates cloud connections to the vCenters,
cloud providers, and ICP and IKS environments. ICP Clusters are
deployed to each datacenter/cloud environment, with MCM providing the
mechanism to connect the ICP clusters into a single management view.

### Related links

* [VCS Hybridity Bundle overview](../vcs/vcs-hybridity-intro.html)
