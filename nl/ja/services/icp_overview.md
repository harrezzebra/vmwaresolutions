---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-26"

---

{:tip: .tip}
{:note: .note}
{:important: .important}

# IBM Cloud Private Hosted の概要

{{site.data.keyword.cloud}} Private Hosted サービスは、自動的に {{site.data.keyword.cloud_notm}} Private Hosted を VMware vCenter Server インスタンスにデプロイします。このサービスは、マイクロサービスとコンテナーの機能を {{site.data.keyword.cloud_notm}} 上の VMware 環境で利用できるようにします。 このサービスを利用することで、使い慣れたオンプレミスの VMware と {{site.data.keyword.cloud_notm}} Private の操作モデルとツールを、{{site.data.keyword.cloud_notm}} に拡張できます。

このサービスは次の環境で使用できます。
* V2.5 以降にデプロイ、または V2.5 以降にアップグレードされた vCenter Server インスタンス
* V2.7 以降にデプロイ、または V2.7 以降にアップグレードされた vCenter Server with Hybridity Bundle インスタンス。
{:note}

## IBM Cloud Private Hosted の技術仕様

**「実動対応 (Production-Ready)」**環境および**「開発/テスト (Development/Test)」**環境用に IBM Cloud Private Hosted サービスを注文するための最小要件を以下の表にリストします。

表 1. 実動対応環境および開発/テスト環境での最小要件

|環境 | Core | メモリー | ホスト | ストレージ |
|:---------- |:---- |:------ |:---- |:------- |
| 実動対応 | 52 | 640 | 3 | 8000 |
| 開発/テスト | 30 | 200 | 3 | 4000 |

### IBM Cloud Privated Hosted のリソース要件

実動対応環境および開発/テスト環境での {{site.data.keyword.cloud_notm}} Private Hosted サービスのリソース要件を次の表にリストします。

表 2. 実動対応環境での {{site.data.keyword.cloud_notm}} Private Hosted のリソース要件

| ノード・タイプ  | CPU コア   | メモリー (GB) | ディスク 1 (GB) | ディスク 2 (GB) | VM の数 |
|:---------- |:----------- |:------------ |:----------- |:----------- |:------------- |
| ブート       | 8 | 16 | 100 | 1 | 1 |   
| 管理 | 8 | 64 | 500 | 3 | 3 |
| マスター     | 8 | 64 | 200 | 3 | 3 |  
| プロキシー      | 2 | 4  | 150 | 3 | 3 |
| ワーカー     | 4 | 16 | 200 | 300 | 6 |
| Vulnerability Advisor | 8 | 16 | 500 | 3 | 3 |
| GlusterFS  | 8 | 16 | 150 | 50 | 3 |
| ブートストラップ ICP/CAM | 16 | 32 | 250 | 1 | 1 |
| NFS サーバー | 8 | 4  | 350 | 1 | 1 |
| Edge | 2 | 1 | 0.5 | 0.5 | 2 |
| 合計 | 162 | 642 | 6401 | 1951 | 26 |
| 文書化された制約 | 52 | 640 |  | 8000 |   |
|   | 1:3 比率 | 1:1 比率 |  | 1:1 比率 |  |

表 3. 開発/テスト環境での {{site.data.keyword.cloud_notm}} Private Hosted のリソース要件

| ノード・タイプ  | CPU コア   | メモリー (GB) | ディスク 1 (GB) | ディスク 2 (GB) | VM の数 |
|:---------- |:----------- |:------------ |:----------- |:----------- |:------------- |
| ブート       | 8 | 16 | 100 | 1 | 1 |   
| 管理 | 8 | 16 | 150 | 1 | 1 |
| マスター     | 8 | 16 | 200 | 1 | 1 |  
| プロキシー      | 2 | 4  | 150 | 1 | 1 |
| ワーカー     | 4 | 16 | 200 | 300 | 3 |
| Vulnerability Advisor | 8 | 16 | 150 | 1 | 1 |
| GlusterFS  | 8 | 16 | 150 | 50 | 3 |
| ブートストラップ ICP/CAM | 16 | 32 | 250 | 1 | 1 |
| NFS サーバー | 8 | 4  | 350 | 1 | 1 |
| Edge | 1 | 0.5 | 0.5 | 2 | 2 |
| 合計 | 96 | 201 | 2401 | 1050 | 15 |
| 文書化された制約 | 30 | 200 |  | 4000 |  |
|  | 1:3 比率 | 1:1 比率 |  | 1:1 比率 |  |

### IBM Cloud Private Hosted のスペース所要量の計算式

IBM Cloud Private および管理オーバーヘッドのスペース所要量を計算するには、以下の計算式を使用します。

計算式 1: `AvailableCores = [ HostCoreCount - HostOverheadCores - ( HostVSanOverheadCorePercentage * HostCoreCount) ] * ( HostCount - vSphereHAHostTolerance ) - MgmtOverheadCores`

表 4. 計算式 1 の変数の説明

| 変数	| 説明 |	単位 |	vSAN の例 | NFS の例 |
|:--------- |:----------- |:---- |:------------- |:----------- |
| AvailableCores |	環境内のワークロードとサービスに使用可能な実際のコア数 |	コア数 |	38	| 43 |
| HostCount	| デフォルト・クラスター内のホストの数	| ホスト数 | 4	| 4 |
| HostCoreCount	| デフォルト・クラスター内の各ホストで使用可能なロー・コアの数 |	コア数 |	16 | 16 |
| HostOverheadCores	| ESXi サーバーによってオーバーヘッドとして予約されているコアの数 (0.1 コア)	| コア数	| 0.1 |	0.1 |
| MgmtOverheadCores | vCenter Server 管理コンポーネント (vCenter Server、PSC、AD/DNS、Edge) によって予約されているコアの数 (5 コア)	| コア数	| 5	| 5 |
| vSphereHAHostTolerance |	vSphere HA 構成で許容されるホストの数 (1 ホスト) |	ホスト数	 | 1 | 1 |
| HostVsanOverheadCorePercentage | vSAN によって使用されるホストのコアの割合 (10%。vSAN ホスト以外の場合は 0%) | % | 10% |	0% |

計算式 2: `AvailableMemory = [ HostMemory - HostOverheadMemory - HostVsanOverheadMemory - ( HostVsanOverheadMemoryDiskPercentage * HostVsanCapacityDiskSize) ] * ( HostCount - vSphereHAHostTolerance ) - MgmtOverheadMemory`

表 5. 計算式 2 の変数の説明

| 変数	| 説明 |	単位 |	vSAN の例 | NFS の例 |
|:--------- |:----------- |:---- |:------------- |:----------- |
| AvailableMemory	|環境内のワークロードとサービスに使用可能なメモリーの GB 数 | GB | 	693	| 860 |
| HostCount	| デフォルト・クラスター内のホストの数	| ホスト数 | 6	| 6 |
| HostMemory |	 デフォルト・クラスター内の各ホストで使用可能なメモリーの未加工容量 (GB 単位) |	GB	| 192 |	192 |
| HostVsanCapacityDiskSize | このホストの各 vSAN 容量 SSD ディスクの容量の GB 数 (960、1946、または 3891 GB。vSAN 以外の場合は 0 GB) | GB |	960 | 0 |
| HostOverheadMemory |	ESXi サーバーによってオーバーヘッドとして予約されているメモリーの GB 単位での容量 (4.6 GB) |	GB	| 4.6 |	4.6 |
| MgmtOverheadMemory |	vCenter Server 管理コンポーネント (vCenter Server、PSC、AD/DNS、Edge) によって予約されているメモリーの GB 単位の容量 (77 GB) | GB | 77 | 77 |
| vSphereHAHostTolerance |vSphere HA 構成で許容されるホストの数 (1 ホスト) |ホスト数	| 1 | 1 |
| HostVsanOverheadMemoryDiskPercentage | vSAN 管理によって予約されているメモリーの GB 単位の容量 (いずれかの容量 vSAN ディスクの割合で表される) (2.75%) |	% | 2.75%	| 2.75% |
| HostVsanOverheadMemory | ディスク・サイズに関係なく vSAN 管理によって予約されているメモリーの GB 単位の容量 (7 GB。VSAN 以外の場合は 0 GB)	| GB |  7	| 0 |

## IBM Cloud Private Hosted をインストールする際の考慮事項

{{site.data.keyword.cloud_notm}} Private Hosted サービスをインストールする前に、必要なライセンスを収集してください。ライセンスでは、{{site.data.keyword.cloud_notm}} Private Hosted の初期デプロイメントだけではなく、インフラストラクチャー内の将来の {{site.data.keyword.cloud_notm}} Private Hosted のサイズ拡張もサポートできるようにすることをお勧めします。

## IBM Cloud Private Hosted を削除する際の考慮事項

* {{site.data.keyword.cloud_notm}} は、{{site.data.keyword.cloud_notm}} Private Hosted サービスの初期インストール時にデプロイされた仮想マシン (VM) のみを削除します。インストール後にデプロイされたノードはクリーンアップされません。
* {{site.data.keyword.cloud_notm}} は、{{site.data.keyword.cloud_notm}} Private Hosted サービスの初期デプロイメント時に作成された VXLAN、DLR、およびエッジ・ゲートウェイを削除します。VXLAN にデプロイされた VM は、{{site.data.keyword.cloud_notm}} Private Hosted サービスの削除が開始すると、接続を失います。

### 関連リンク

* [IBM Cloud Private Hosted の注文](../services/icp_ordering.html)
* [IBM Cloud Private Hosted](https://www.ibm.com/developerworks/community/files/form/anonymous/api/library/eafb752c-55f3-4b07-9b20-b61c8ea980b9/document/af203658-30c0-40ba-81b5-46c393fb723f/media/IBM_Cloud_Private_Hosted-IBM_Cloud.pdf) (PDF のダウンロード)
* [IBM Cloud Private のチケットをオープン](https://www.ibm.com/mysupport/s/?language=en_US)
