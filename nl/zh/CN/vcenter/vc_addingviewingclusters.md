---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

{:tip: .tip}
{:note: .note}
{:important: .important}

# 添加、查看和删除 vCenter Server 实例的集群

缺省情况下，订购实例时配置的 ESXi 服务器会分组为 **cluster1**。

可以向 VMware vCenter Server 实例添加您自己的集群以扩展计算和存储容量。在集群中，可以管理 ESXi 服务器以获得更佳的资源分配和高可用性。不再需要添加的集群时，请从实例中将其删除。

删除集群功能仅可用于部署在（或已升级到）V2.3 和更高版本中的实例。
{:note}

## 向 vCenter Server 实例添加集群

可以添加到实例的集群数取决于实例版本：
* 对于部署在（或已升级到）V2.2 和更高版本中的实例，最多可以添加 10 个集群。
* 对于部署在 V2.1 或更低版本中的实例，最多可以添加 5 个集群。

### 系统设置

为 vCenter Server 实例添加集群时，必须指定以下设置。

#### 集群名称

集群名称必须满足以下需求：
* 只允许使用字母数字字符和短划线 (-) 字符。
* 集群名称必须以字母数字字符开头和结尾。
* 最大字符数为 30。
* 集群名称在 vCenter Server 实例中必须唯一。

#### 数据中心位置

缺省情况下，集群的 {{site.data.keyword.CloudDataCent}} 位置设置为 vCenter Server 实例的 {{site.data.keyword.CloudDataCent_notm}}。可以将集群部署到与所部署实例不同的 {{site.data.keyword.CloudDataCent_notm}}，但必须确保这两个 {{site.data.keyword.CloudDataCents_notm}} 之间的网络等待时间少于 150 毫秒。要检查网络等待时间，可以使用 [SoftLayer IP Backbone Looking Glass](http://lg.softlayer.com/) 等工具。

如果将集群部署到其他 {{site.data.keyword.CloudDataCent_notm}} 或 {{site.data.keyword.cloud_notm}} 基础架构 pod，那么可订购三个额外的 VLAN 以用于订购的 {{site.data.keyword.baremetal_short}}。

### 裸机服务器设置

您可以选择 **Skylake**、**SAP 认证**、**Broadwell** 或**预配置**。

#### Skylake

对于 **Skylake** 设置，您有多个 **CPU 型号**和 **RAM** 选项。可用选项可能有所不同，具体取决于初始部署实例的版本。

表 1. Skylake {{site.data.keyword.baremetal_short}} 的选项

| CPU 模型选项   |RAM 选项|
|:------------- |:------------- |
|双 Intel Xeon Silver 4110 处理器 / 共 16 个核心，2.1 GHz|64 GB、96 GB、128 GB、192 GB、384 GB、768 GB、1.5 TB|
|双 Intel Xeon Gold 5120 处理器 / 共 28 个核心，2.2 GHz|64 GB、96 GB、128 GB、192 GB、384 GB、768 GB、1.5 TB|
|双 Intel Xeon Gold 6140 处理器 / 共 36 个核心，2.3 GHz|64 GB、96 GB、128 GB、192 GB、384 GB、768 GB、1.5 TB|

#### SAP 认证

选择 **SAP 认证**后，无法变更 CPU 或 RAM 设置。

根据需求，选择裸机服务器配置：
* 双 Intel Xeon Gold 6140 处理器 / 共 36 个核心，2.3 GHz / 192 GB RAM
* 双 Intel Xeon Gold 6140 处理器 / 共 36 个核心，2.3 GHz / 384 GB RAM
* 双 Intel Xeon Gold 6140 处理器 / 共 36 个核心，2.3 GHz / 768 GB RAM

#### Broadwell

对于 **Broadwell** 设置，您有多个 **CPU 型号**和 **RAM** 选项。可用选项可能有所不同，具体取决于初始部署实例的版本。

表 2. Broadwell {{site.data.keyword.baremetal_short}} 的选项

| CPU 模型选项   |RAM 选项|
|:------------- |:------------- |
|双 Intel Xeon E5-2620 V4 / 共 16 个核心，2.1 GHz|64 GB、128 GB、256 GB、512 GB、768 GB、1.5 TB|
|双 Intel Xeon E5-2650 V4 / 共 24 个核心，2.2 GHz|64 GB、128 GB、256 GB、512 GB、768 GB、1.5 TB|
|双 Intel Xeon E5-2690 V4 / 共 28 个核心，2.6 GHz|64 GB、128 GB、256 GB、512 GB、768 GB、1.5 TB|

#### 预配置

对于**预配置**设置，可以根据需求选择**裸机服务器配置**：
* 小型（双 Intel Xeon E5-2620 V4 / 共 16 个核心，2.1 GHz / 128 GB RAM / 2 个磁盘）
* 中型（双 Intel Xeon E5-2650 V4 / 共 24 个核心，2.2 GHz / 256 GB RAM / 2 个磁盘）
* 大型（双 Intel Xeon E5-2690 V4 / 共 28 个核心，2.6 GHz / 512 GB RAM / 2 个磁盘）

#### 裸机服务器的数量

集群至少需要两个 {{site.data.keyword.baremetal_short}}。

对于在 V2.1 或更高版本中部署的 vCenter Server 实例，可以为一个集群最多添加 59 个 {{site.data.keyword.baremetal_short}}。一次可以添加 1 到 59 个 ESXi 服务器。

对于在 V2.0 或更低版本中部署的 vCenter Server 实例，可以为一个集群最多添加 32 个 {{site.data.keyword.baremetal_short}}。一次可以添加的 {{site.data.keyword.baremetal_short}} 数量如下：
* 对于**小型**、**中型**和**大型**裸机服务器配置，一次可以添加 1 到 10 个 ESXi 服务器。
* 对于 **Skylake** 或 **Broadwell** 裸机服务器配置，一次可以添加 1 到 20 个 ESXi 服务器。

部署后，最多可以再创建四个集群。如果选择使用 VMware vSAN 存储器的 **Skylake** 或 **Broadwell** 裸机服务器配置，那么初始集群和部署后集群都需要 4 个服务器。

### 存储设置

存储设置基于您选择的裸机服务器配置和存储类型。

#### vSAN 存储器

请指定以下 vSAN 选项：
* **vSAN 容量磁盘的磁盘类型和大小**：选择与所需容量磁盘相应的选项。
* **vSAN 容量磁盘数**：指定要添加的容量磁盘数。
* 如果要添加的容量磁盘数超过 8 个的限制，请选中**高性能 Intel Optane** 框。此选项用于提供两个额外的容量磁盘托架，总共可容纳 10 个容量磁盘；此选项对于需要更短等待时间和更高 IOPS 吞吐量的工作负载而言非常有用。**高性能 Intel Optane** 选项仅可用于双 Intel Xeon Gold 5120 和 6140 处理器。

* 查看 **vSAN 高速缓存磁盘的磁盘类型**和 **vSAN 高速缓存磁盘数**值。这些值依赖于是否选中了**高性能 Intel Optane** 框。
* **vSAN 许可证**：通过选择**购买时包含**对 vSAN 组件使用 IBM 提供的 VMware 许可证，或者通过选择**我将提供**并输入您自己的许可证密钥以自带许可证 (BYOL)。

如果初始集群为 vSAN 集群，那么其他任何 vSAN 集群都会使用与初始 vSAN 集群相同的 vSAN 许可证，并具有与初始 vSAN 集群相同的配置。如果实例中的任何集群选择了要部署 vSAN（初始或其他集群），也是如此。第一次系统会提示您提供 vSAN 许可证（BYOL 或购买的许可证）和版本。下次您为新集群选择 vSAN 时，将复用最初选择的许可证。

#### NFS 存储器

选择 **NFS 存储器**时，可以为实例添加文件级别的共享存储器，其中所有共享使用相同的设置，也可以对每个文件共享指定不同的配置设置。请指定以下 NFS 选项：

文件共享数必须在范围 1 到 32 之间。
{:note}

* **分别配置共享**：选择此项以对每个文件共享指定不同的配置设置。
* **共享数**：要对每个文件共享使用相同的配置设置时，请指定要添加的 NFS 共享存储器的文件共享数。
* **大小**：选择满足共享存储器需求的容量。
* **性能**：选择基于工作负载需求的 IOPS（每秒输入/输出操作数）/GB。
* **添加 NFS**：选择此项以添加使用不同配置设置的单个文件共享。

表 3. NFS 性能级别选项

|选项|详细信息|
  |:------------- |:------------- |
  |2 IOPS/GB|此选项旨在用于大多数通用工作负载。示例应用包括：托管小型数据库、备份 Web 应用程序或系统管理程序的虚拟机磁盘映像。|
  |4 IOPS/GB|此选项旨在用于同时活动数据百分比高的更高强度工作负载。示例应用包括：事务性数据库。|
  |10 IOPS/GB|此选项旨在用于要求最苛刻的工作负载类型（如分析）。示例应用包括：高事务数据库和其他性能敏感型数据库。此性能级别限制为每个文件共享的最大容量为 4 TB。|

### 许可证设置

为集群中的 VMware vSphere 组件指定许可选项：
* 对于业务合作伙伴用户，会包含 vSphere 许可证 (Enterprise Plus Edition)，该许可证以您的名义购买。
* 对于非业务合作伙伴用户，可以通过选择**购买时包含**对此组件使用 IBM 提供的 VMware 许可证，或者可以通过选择**我将提供**并输入您自己的许可证密钥以自带许可证 (BYOL)。

### 网络接口设置

网络接口卡 (NIC) 启用设置基于您选择的是**公用和专用网络**还是**仅专用网络**。以下附加组件服务需要公共 NIC，并且这些服务在您选择专用选项时不可用：

* F5 on {{site.data.keyword.cloud_notm}}
* Fortigate Security Appliance on {{site.data.keyword.cloud_notm}}
* Fortigate Virtual Appliance on {{site.data.keyword.cloud_notm}}
* Zerto on {{site.data.keyword.cloud_notm}}

### 订单摘要

根据为集群选择的配置，估算成本会立即生成并显示在**订单摘要**右侧窗格中。

## 向 vCenter Server 实例添加集群的过程

1. 在 {{site.data.keyword.vmwaresolutions_short}} 控制台中，单击左侧导航窗格中的**已部署的实例**。
2. 在 **vCenter Server 实例**表中，单击要添加集群的实例。

   确保实例处于**可供使用**状态。否则，无法向实例添加集群。
   {:note}
3. 单击左侧导航窗格上的**基础架构**，然后单击**集群**表右上角的**添加**。
4. 在**添加集群**页面上，输入集群名称。
5. 如果希望托管集群的 {{site.data.keyword.CloudDataCent_notm}} 与托管实例的不同，请在**裸机服务器**下选中**选择其他位置**复选框，然后选择要托管实例的 {{site.data.keyword.CloudDataCent_notm}}。
6. 填写裸机配置。
   * 如果选择的是 **Skylake** 或 **Broadwell**，请指定 **CPU 型号**、**RAM** 量和 **{{site.data.keyword.baremetal_short}} 数**。
   * 如果选择的是 **SAP 认证**，请指定 CPU 型号。
   * 如果选择的是**预配置**，请指定**裸机服务器配置**和 **{{site.data.keyword.baremetal_short}} 数**。如果计划将 vSAN 用作存储解决方案，那么至少需要 4 个 {{site.data.keyword.baremetal_short}}。
7. 填写存储配置。
  * 如果选择 **vSAN 存储器**，请指定容量和高速缓存磁盘的磁盘类型、磁盘数和 vSAN 许可证版本。如果需要更多存储器，请选中**高性能 Intel Optane** 框。
  * 如果选择 **NFS 存储器**，并且要向所有文件共享添加和配置相同设置，请指定**共享数**、**大小**和**性能**。
  * 如果选择 **NFS 存储器**，并且要单独添加和配置文件共享，请选择**单独配置共享**。接着，单击**添加 NFS** 标签旁边的 **+** 图标，然后为每个文件共享选择**大小**和**性能**。必须至少选择一个文件共享。
8. 指定 vSphere 许可证密钥的提供方式：
  * 对于业务合作伙伴用户，会包含 vSphere 许可证 (Enterprise Plus Edition)，该许可证以您的名义购买。
  * 对于非业务合作伙伴的用户，可以选择下列其中一个选项：
      * 如果希望以您自己的名义购买新许可证，请为组件选择**购买时包含**。
      * 如果要对组件使用您自己的 VMware 许可证，请选择**我将提供**并输入您的许可证密钥。
9. 选择网络设置**公用和专用网络**或**仅专用网络**。
10. 在**订单摘要**窗格上，验证集群配置，然后再添加集群。
   1. 复查集群的设置。
   2. 复查集群的估算成本。单击**定价详细信息**以生成 PDF 摘要。要保存或打印订单摘要，请单击 PDF 窗口右上角的**打印**或**下载**图标。
   3. 单击订单适用条款的链接，并在添加集群之前确认您同意这些条款。
   4. 单击**供应**。

### 向 vCenter Server 实例添加集群后的结果

1. 集群部署会自动启动，并且集群的状态会更改为**正在初始化**。可以通过在实例的**摘要**页面中查看部署历史记录，以检查部署的状态。
2. 集群准备就绪可供使用后，其状态会更改为**可供使用**。将对新添加的集群启用 vSphere 高可用性 (HA) 和 vSphere 分布式资源调度程序 (DRS)。

不能更改集群名称。更改集群名称可能会导致集群中添加或除去 ESXi 服务器的操作失败。
{:important}

## 查看 vCenter Server 实例中集群的过程

1. 在 {{site.data.keyword.vmwaresolutions_short}} 控制台中，单击左侧导航窗格中的**已部署的实例**。
2. 在 **vCenter Server 实例**表中，单击实例以查看其中的集群。
3. 在左侧导航窗格上，单击**基础架构**。在**集群**表中，查看有关集群的摘要：
  * **名称**：集群的名称。
  * **ESXi 服务器数**：集群中的 ESXi 服务器数。
  * **CPU**：集群中 ESXi 服务器的 CPU 规范。
  * **定制 vSAN 磁盘数**：集群中的 vSAN 磁盘数，包括磁盘类型和容量。
  * **内存**：集群中 ESXi 服务器的内存总大小。
  * **数据中心位置**：托管集群的 {{site.data.keyword.CloudDataCent_notm}}。
  * **pod**：在其中部署集群的 pod。
  * **状态**：集群的状态。状态可以是下列其中一个值：
    <dl class="dl">
        <dt class="dt dlterm">正在初始化</dt>
        <dd class="dd">正在创建并配置集群。</dd>
        <dt class="dt dlterm">正在修改</dt>
        <dd class="dd">正在修改集群。</dd>
        <dt class="dt dlterm">可供使用</dt>
        <dd class="dd">集群准备就绪，可供使用。</dd>
        <dt class="dt dlterm">正在删除</dt>
        <dd class="dd">正在删除集群。</dd>
        <dt class="dt dlterm">已删除</dt>
        <dd class="dd">集群已删除。</dd>
    </dl>
  * **操作**：单击**删除**图标以删除集群。
4. 单击集群名称以查看 ESXi 服务器及其存储的详细信息：

  * ESXi 服务器详细信息：
     * **名称**：ESXi 服务器名称的格式为 `<host_prefix><n>.<subdomain_label>.<root_domain>`，其中：

       `host_prefix` 是主机名前缀，

       `n` 是服务器的序列，

       `subdomain_label` 是子域标签，

       `root_domain` 是根域名。

     * **版本**：ESXi 服务器的版本。
     * **凭证**：用于访问 ESXi 服务器的用户名和密码。
     * **专用 IP**：ESXi 服务器的专用 IP 地址。
     * **状态**：ESXi 服务器的状态，可以是下列其中一个值：
        <dl class="dl">
        <dt class="dt dlterm">已添加</dt>
        <dd class="dd">ESXi 服务器已添加并准备就绪可供使用。</dd>
        <dt class="dt dlterm">正在添加</dt>
        <dd class="dd">正在添加 ESXi 服务器。</dd>
        <dt class="dt dlterm">正在删除</dt>
        <dd class="dd">正在删除 ESXi 服务器。</dd>
        </dl>
  * 存储详细信息：
    * **名称**：数据存储名称。
    * **大小**：存储器的容量。
    * **IOPS/GB**：存储器的性能级别。
    * **NFS 协议**：存储器的 NFS 版本。

## 从 vCenter Server 实例中删除集群

当不再需要集群时，您可能希望将其从实例中删除。

### 删除之前

* 使用此过程从部署在 V2.3 或更高版本中的实例中删除集群。
* 对于在 V2.2 或更低版本实例中部署的集群，如果要删除已添加到实例的集群，必须将实例升级到 V2.3。
* 一次可以删除一个集群。要删除多个集群，必须按顺序依次执行。请等待前一个集群删除后，再删除下一个集群。
* 删除集群之前，请确保集群中的所有节点都已打开电源且正常运行。
* 删除集群时，集群中的所有 VM（虚拟机）也会一起删除且无法恢复。如果要保留这些 VM，请将其迁移到其他集群。
* 无法删除缺省集群。

### 从 vCenter Server 实例中删除集群的过程

1. 在 {{site.data.keyword.vmwaresolutions_short}} 控制台中，单击左侧导航窗格中的**已部署的实例**。
2. 在 **vCenter Server 实例**表中，单击要从中删除集群的实例。

   确保实例处于**可供使用**状态。否则，无法从实例中删除集群。
   {:note}

3. 在左侧导航窗格上，单击**基础架构**。在**集群**表中，找到要删除的集群，然后单击**操作**列中的**删除**图标。
4. 确认已完成将虚拟机迁移到其他集群（如果需要），并确认要删除该集群。

### 相关链接

* [查看 vCenter Server 实例](vc_viewinginstances.html)
* [扩展和收缩 vCenter Server 实例的容量](vc_addingremovingservers.html)
