---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-26"

---

{:tip: .tip}
{:note: .note}
{:important: .important}

# Single-node Trial for VMware vCenter Server on IBM Cloud インスタンスの注文と削除

Single-node Trial for VMware vCenter Server on {{site.data.keyword.cloud}} は、VMware vSphere スタックをサービスとして提供する単一テナントのホステッド・プライベート・クラウドです。クライアント管理環境は通常、最小で 3 つのノードを使用してデプロイされますが、この単一ノード・トライアルは、ハイブリッド・クラウド実装の利点を体験するために低コストのパスを提供しています。

このトライアル版は、初期デプロイメントについて IBM の高度な自動化の速度を明示したり、単純な非実稼働ワークロードをクラウドに簡単に移動できることを明示したりする PoC (概念検証) に理想的です。VMware Hybrid Cloud Extension (HCX) を使用すれば、{{site.data.keyword.CloudDataCent_notm}}にオンプレミス・データ・センター・ネットワークを安全に拡張できるとともに、相互接続を構成するネットワークの複雑さを低減できます。HCX は、仮想マシン (VM) に IP アドレスを割り振り直すことなくワークロードを双方向でシームレスに移動できるように、根底にあるネットワーキング・リソースを抽象化してパブリック・インターネットをトンネリングします。HCX を使用すれば、VMware NSX をオンプレミスにインストールする必要はなくなり、VMware NSX は vSphere の古いバージョンに対して後方互換となります。  

単一ノード・トライアルは PoC (概念検証) のみを目的としています。この環境では実動ワークロードを実行しないでください。ホストやクラスターの追加と削除、追加アドオン・サービスの注文、更新の適用などの管理機能はサポートされていません。
{:important}

このトライアル版は最大 90 日間使用できます。トライアル期間が終了したら、この環境を削除し、キャパシティーのニーズを満たす高可用性環境をプロビジョンできます。詳しくは、[vCenter Server with Hybridity Bundle インスタンスの注文](vc_hybrid_orderinginstance.html)を参照してください。

## Single-node Trial for vCenter Server インスタンスの技術仕様

Single-node Trial for vCenter Server インスタンスには以下のコンポーネントが含まれています。

標準化されたハードウェア構成の使用可否と価格は、デプロイメントに選択した {{site.data.keyword.CloudDataCent_notm}}によって異なる場合があります。
{:note}

### ベア・メタル・サーバー

Dual Intel Xeon Gold 5120 (28 コア、2.20 GHz) プロセッサー、384 GB の RAM を搭載。

### ネットワーキング

以下のネットワーキング・コンポーネントが注文されます。
*  10 Gbps デュアル・ネットワーク・アップリンク (パブリックとプライベート)
*  VLAN (仮想 LAN) 3 つ: パブリック VLAN 1 つとプライベート VLAN 2 つ
*  レイヤー 2 (L2) ネットワークに接続されたローカル・ワークロード間で実行される可能性のある東西通信用の DLR (分散論理ルーター) を備えた VXLAN (仮想拡張可能 LAN) 1 つ。 この VXLAN は、サンプルのルーティング・トポロジーとしてデプロイされるので、変更したり、作成の基礎として使用したり、削除したりできます。 また、DLR の新しい論理インターフェースに追加の VXLAN を接続してセキュリティー・ゾーンを追加することもできます。
*  以下の 2 つの VMware NSX Edge Services Gateway
  * アウトバウンド HTTPS 管理トラフィック用のセキュアな管理サービス VMware NSX Edge Services Gateway (ESG)。これは、管理ネットワーキング・トポロジーの一部として IBM がデプロイします。 この ESG は、IBM 管理 VM が、自動化に関連する特定の外部 IBM 管理コンポーネントと通信するために使用します。 詳しくは、[ユーザー管理の ESG を使用するためのネットワークの構成](../vcenter/vc_esg_config.html#configuring-your-network-to-use-the-customer-managed-nsx-esg-with-your-vms)を参照してください。

    ユーザーは、この ESG にアクセスすることはできず、使用できません。 これを変更すると、{{site.data.keyword.vmwaresolutions_short}} コンソールから vCenter Server with Hybridity Bundle インスタンスを管理できなくなる可能性があります。 また、ファイアウォールを使用したり、外部 IBM 管理コンポーネントへの ESG 通信を無効にしたりすると、{{site.data.keyword.vmwaresolutions_short}} が使用不可になります。
    {:important}
  * アウトバウンドとインバウンドの HTTPS ワークロード・トラフィック用のユーザー管理のセキュアな VMware NSX Edge Services Gateway。これは、VPN アクセスまたはパブリック・アクセスを提供するためにユーザーが変更可能なテンプレートとして IBM がデプロイします。 詳しくは、[ユーザー管理の NSX Edge にはセキュリティーのリスクがありますか?](../vmonic/faq.html#does-the-customer-managed-nsx-edge-pose-a-security-risk-) を参照してください。

HCX on {{site.data.keyword.cloud_notm}} サービスのデプロイ時に注文するネットワーキング・コンポーネントについて詳しくは、[HCX on {{site.data.keyword.cloud_notm}} の概要](../services/hcx_considerations.html)を参照してください。

### 仮想サーバー・インスタンス

以下の仮想サーバー・インスタンス (VSI) が注文されます。

* IBM CloudBuilder の VSI。これは、インスタンスのデプロイメントが完了した後にシャットダウンされます。
* Microsoft Active Directory (AD) 用の Microsoft Windows Server VSI がデプロイされて参照可能になります。 この VSI がインスタンスの DNS として機能し、ここにホストと仮想マシンが登録されます。

### IBM 提供のライセンスおよび料金

Single-node Trial for vCenter Server インスタンスの注文には、以下のライセンスが含められます。

* VMware vSphere Enterprise Plus 6.5u1
* VMware vCenter Server 6.5
* VMware NSX Service Providers Advanced Edition 6.4

Single-node Trial for vCenter Server インスタンスは、ライセンス持ち込みをサポートしていません。
{:note}

追加のサポートとサービスの料金が適用される可能性があります。

## HCX on IBM Cloud の技術仕様

HCX on {{site.data.keyword.cloud_notm}} の技術仕様と考慮事項について詳しくは、[VMware HCX on IBM Cloud の概要](../services/hcx_considerations.html)を参照してください。

## Single-node Trial for vCenter Server インスタンスの注文の要件と計画

以下の作業を完了していることを確認してください。
* 使用する {{site.data.keyword.cloud_notm}} アカウントは、特定の要件を満たしている必要があります。 詳しくは、[{{site.data.keyword.cloud_notm}} アカウントの要件](../vmonic/slaccountrequirement.html)を参照してください。
*  **「設定」**ページで {{site.data.keyword.cloud_notm}} インフラストラクチャー資格情報を構成します。詳しくは、[ユーザー・アカウントと設定の管理](../vmonic/useraccount.html)を参照してください。
* インスタンス名の要件を確認します。  
 * 英数字とダッシュ (-) の文字だけを使用できます。
 * インスタンス名の先頭と末尾は英数字である必要があります。
 * インスタンス名の最大の長さは 10 文字です。
 * インスタンス名はアカウント内で固有である必要があります。
* 物理インフラストラクチャーの要件を満たす {{site.data.keyword.CloudDataCents_notm}}を確認します。詳しくは、[vCenter Server with Hybridity Bundle インスタンスの要件と計画](../vcenter/vc_hybrid_planning.html#ibm-cloud-data-center-availability)の *{{site.data.keyword.CloudDataCent_notm}}の使用可否*セクションを参照してください。
<!--* Ensure the that you meet the following prerequisites for the on-premises HCX instance:
 * VMware vSphere and vCenter 5.5 or higher
 * The VMware HCX Manager must reside in the same security zone as the on-premises vSphere environment
 * The VMware HCX Manager must be able to reach the public Internet to update firewall rules to allow outbound traffic
 * The vSphere environment must have distributed switches-->

## Single-node Trial for vCenter Server インスタンスを注文する手順

1. **「Single-node Trial for VMware vCenter Server on IBM Cloud (Single-node Trial for VMware vCenter Server on {{site.data.keyword.cloud_notm}})」**ページで、**「vCenter サーバー」**カードをクリックし、**「続行」**をクリックします。
2. **「Single-node Trial for VMware vCenter Server (Single-node Trial for VMware vCenter Server)」**ページで、{{site.data.keyword.cloud_notm}} インフラストラクチャー・アカウントを要求するステップを実行するか、既存の**「ユーザー名」**と**「API キー」**を指定して**「取得」**をクリックします。
3. インスタンス名を入力します。
4. インスタンスをホストする {{site.data.keyword.CloudDataCent_notm}}を選択します。  

 {{site.data.keyword.CloudDataCent_notm}}が事前選択されています。必要に応じて別の {{site.data.keyword.CloudDataCent_notm}}の場所を選択します。
 {:note}
5. **「発注要約」**ペインで、インスタンス構成を確認してから注文を実行します。
   1. インスタンスの設定を確認します。
   2. インスタンスの見積もりコストを確認します。 PDF のサマリーを生成するには、**「料金詳細」**をクリックします。 注文のサマリーを保存または印刷するには、PDF ウィンドウの右上にある**「印刷」**アイコンまたは **「ダウンロード」**アイコンをクリックします。
   3. 注文に適用される使用条件のリンクをクリックして、インスタンスを注文する前にそれらの条件に同意することを確認する必要があります。
   4. **「プロビジョン」**をクリックします。

### 結果

インスタンスのデプロイメントが自動的に開始され、オンプレミスの HCX on {{site.data.keyword.cloud_notm}} サービス・アクティベーション・キーが注文されます。

#### HCX on IBM Cloud のデプロイメント・プロセス

HCX on {{site.data.keyword.cloud_notm}} のデプロイメントは自動的に行われます。 以下の手順が {{site.data.keyword.vmwaresolutions_short}} 自動化プロセスによって実行されます。
1. {{site.data.keyword.cloud_notm}} インフラストラクチャー上の HCX 用に、次の 3 つのサブネットが注文されます。
   * HCX 管理用プライベート・ポータブル・サブネットを 1 つ。
   * HCX 相互接続用プライベート・ポータブル・サブネットを 1 つ。 このサブネットは、**「HCX interconnect type」**として**「Private network」**オプションを選択した場合に使用されます。
   * VMware でのアクティベーションやメンテナンスで使用されるパブリック・ポータブル・サブネットを 1 つ。 **「HCX interconnect type」**として**「Public network」**オプションを選択した場合、このサブネットは HCX 相互接続用としても使用されます。

   HCX 用に注文されたサブネット内の IP アドレスは、VMware on {{site.data.keyword.cloud_notm}} の自動化機能によって管理されるようになっています。 ユーザーが作成した VMware リソース (VM や NSX Edge など) にこれらの IP アドレスを割り当てることはできません。 VMware 成果物用に追加の IP アドレスが必要な場合は、{{site.data.keyword.cloud_notm}} 上の独自のサブネットを注文する必要があります。
   {:important}
2. **「HCX interconnect type」**に対して**「Private network」**が選択された場合、**SDDC-DPortGroup-HCX-Private** という名前のポート・グループがプライベート分散仮想スイッチ (DVS) に作成されます。
3. HCX アクティベーション・キーが VMware から注文されます。
4. HCX 用のリソース・プールと VM フォルダーが 3 つずつ作成されます。これらは、HCX 相互接続、ローカル HCX コンポーネント、リモート HCX コンポーネントに必要です。
5. HCX 管理トラフィック用の VMware NSX Edge Services Gateway (ESG) のペアがデプロイされ、構成されます。
   * 注文したサブネットに基づいて、パブリック・アップリンク・インターフェースとプライベート・アップリンク・インターフェースが構成されます。
   * ESG がエクストラ・ラージ・エッジ・アプライアンスのペアとして構成され、高可用性 (HA) が有効になります。
   * HCX Manager との間のインバウンドとアウトバウンドの HTTPS トラフィックが可能になるように、ファイアウォール・ルールとネットワーク・アドレス変換 (NAT) ルールが構成されます。
   * ロード・バランサー・ルールとリソース・プールが構成されます。 それらのルールとリソース・プールを使用して、HCX 関連のインバウンド・トラフィックが、HCX Manager、vCenter Server、Platform Services Controller (PSC) の該当する仮想アプライアンスに転送されます。
   * ESG を通ってくる HCX 関連のインバウンド HTTPS トラフィックを暗号化するための SSL 証明書が適用されます。

   HCX 管理エッジは、オンプレミスの HCX コンポーネントとクラウド・サイドの HCX コンポーネントの間の HCX 管理トラフィック専用です。 HCX 管理エッジは、変更したり、HCX ネットワーク拡張に使用したりしないでください。 ネットワーク拡張用には別のエッジを作成してください。 また、ファイアウォールを使用したり、プライベート IBM 管理コンポーネントやパブリック・インターネットへの HCX 管理エッジ通信を無効にしたりすると、HCX の機能に悪影響を与える恐れがあります。
   {:important}

6. {{site.data.keyword.cloud_notm}} 上の HCX Manager がデプロイされ、アクティブにされ、構成されます。
   * HCX Manager が vCenter Server に登録されます。
   * HCX Manager、vCenter Server、PSC、および NSX Manager が構成されます。
   * HCX フリートが構成されます。
   * ローカルとリモートの HCX デプロイメント・コンテナーが構成されます。
7. HCX Manager のホスト名と IP アドレスが {{site.data.keyword.cloud_notm}} 上の VMware vCenter Server の DNS サーバーに登録されます。

#### インスタンスの詳細の表示

インスタンスの詳細を表示して、デプロイメントの状況を確認できます。インスタンスの詳細の表示については、以下を参照してください。

* [vCenter Server インスタンスの表示](vc_viewinginstances.html)
* [オンプレミス VMware HCX on IBM Cloud インスタンスの参照](../services/standalone_viewingserviceinstances.html)

インスタンスが正常にデプロイされると、このトピックの*技術仕様*セクションで説明されているコンポーネントが VMware 仮想プラットフォームにインストールされ、オンプレミスの HCX on {{site.data.keyword.cloud_notm}} サービス・アクティベーション・キーがオンプレミスの HCX on {{site.data.keyword.cloud_notm}} の詳細ページで使用可能になります。

インスタンスの状況が**「使用可能」**に変わり、E メールで通知が届きます。

### 次に行うこと

HCX on {{site.data.keyword.cloud_notm}} サービスを構成し、オンプレミスのアクティベーション・キーをインストールします。

1. **「デプロイ済みインスタンス」**ページでオンプレミスのアクティベーション・キーを見つけます。
  1. {{site.data.keyword.vmwaresolutions_short}} コンソールで、左側のナビゲーション・ペインの**「デプロイ済みインスタンス」**をクリックします。
  2. **「vCenter Server インスタンス」**表で、**「タイプ」**列を確認して単一ノード・トライアル・インスタンスを見つけ、インスタンス名をメモします。
  3. **「オンプレミス HCX インスタンス」**表までスクロールし、**「名前」**列を確認して、単一ノード・インスタンスと同じ名前のインスタンスを見つけます。
  4. **「アクティベーション・キー」**フィールドの鍵をメモします。
2. [VMware HCX](https://hcx.vmware.com/#/vm-documentation) にアクセスし、アクティベーション・キーを使用してオンプレミスの VMware HCX on {{site.data.keyword.cloud_notm}} インスタンスをインストールし、セットアップ・プロセスを完了します。詳しくは、*Procedure coming soon* を参照してください。

{{site.data.keyword.cloud_notm}} アカウントで作成した {{site.data.keyword.vmwaresolutions_short}} インフラストラクチャー・コンポーネントは、{{site.data.keyword.vmwaresolutions_short}} コンソールから管理する必要があります。{{site.data.keyword.slportal}}やその他の手段でコンソール以外から管理することはできません。
これらのコンポーネントを {{site.data.keyword.vmwaresolutions_short}} コンソール以外で変更した場合、変更がコンソールと同期されず、環境が不安定になります。
{:important}

## Single-node Trial for vCenter Server インスタンスを削除する手順

Single-node Trial for vCenter Server インスタンスで注文したコンポーネントを解放するには、このインスタンスを削除します。

詳しくは、[vCenter Server インスタンスの削除](vc_deletinginstance.html)を参照してください。

### 関連リンク

* [{{site.data.keyword.cloud_notm}} アカウントへの登録](../vmonic/signing_softlayer_account.html)
* [HCX の用語集](../services/hcx_glossary.html)
* [VMware Hybrid Cloud Extension の資料](https://hcx.vmware.com/#/vm-documentation)
* [vCenter Server with Hybridity Bundle の概要](vc_hybrid_overview.html)
* [vCenter Server with Hybridity Bundle インスタンスのネットワーキングに関する考慮事項](vc_hybrid_networkingonvcenterserver.html)
* [vCenter Server with Hybridity Bundle インスタンスの注文](vc_hybrid_orderinginstance.html)
