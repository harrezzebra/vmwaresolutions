---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-25"

---

# vCenter Server および IBM Cloud Private の概要

このドキュメントでは、アプリケーション・モダナイゼーションの手順を経て IBM Cloud に移行する方法について説明します。統合されたマルチクラウド環境をアプリケーション・モダナイゼーションで活用できるようにするクラウド管理コンポーネントを中心に説明します。

- **VMware vCenter Server on IBM Cloud** - VCS は、IBM Cloud for VMware Solutions のオファリングであり、IBM Cloud 上で自動的にプロビジョンされる VMware ベースのプラットフォームです。

- **IBM Cloud Private** - ICP は、仮想化インフラストラクチャー・プラットフォーム (VMware など) にデプロイするように設計されたコンテナー化アプリケーションを開発および管理するためのアプリケーション・プラットフォームです。

- **IBM Kubernetes Services** - IKS は、シングル・テナント・クラスターを対象としたアプリケーション・コンテナーのデプロイメント自動化、スケーリング、および運用を行うオーケストレーション・エンジンとして Kubernetes を活用する、IBM Cloud 上の管理対象サービスです

- **IBM Multi-Cluster Manager** – MCM は、複数のクラウドおよびクラスターにおけるユーザー可視性、アプリケーション中心の管理 (ポリシー、デプロイメント、正常性、操作)、ポリシー・ベースのコンプライアンスを提供します。MCM を使用することで、Kubernetes クラスターを制御できます。

- **IBM Cloud Automation Manager** – CAM は、ICP 上で実行されるマルチクラウド・セルフサービス管理プラットフォームであり、開発者と管理者がビジネス要求に対応できるようにします。

## IBM Cloud でのアプリケーション・モダナイゼーション
アプリケーション・モダナイゼーションとは、既存のアプリケーションを移行してクラウド上の新しいアプローチを活用するプロセスを表す用語です。昨今のお客様は、ビジネスやアプリケーションの複雑さに基づいてこの移行を行うために役立つ革新的で効率的なアプローチを模索しています。

ビジネスのプレッシャーにより、市場投入までの時間を短縮することが求められています。お客様の既存の資産には、アプリケーションだけでなく、データ、プロセス、ビジネス・ロジック、ユーザー・インターフェースが含まれ、これらはすべて、新しいビジネス要求に対応するための変更が必要になっています。

アプリケーション・モダナイゼーションの利点には、以下が含まれます。
- 開発者の生産性の向上。
- 運用効率の向上。
- 新しい機能を構築するためのコストの削減。
- 短時間でのキャパシティー拡張の実現。

IBM では、プライベート・クラウドの 70% がアプリケーション環境をモダナイズする必要性に迫られて導入されたものであると認識していますが、ほとんどの組織では段階的なアプローチでアプリケーション・モダナイゼーションが進んでいるため、以下のようにハイブリッド環境とマルチクラウド環境が必要になっています。
- メインフレームまたは UNIX システムで通常実行される一体構造の複雑なレガシー・アプリケーションは、オンプレミスのまま運用されます。
- SoR (Systems of Record、定型業務処理システム) で使用される x86 環境、あるいは、セキュリティー・センシティブなワークロードまたは規制されたワークロードのアプリケーションは、仮想化インフラストラクチャーまたはプライベート・クラウドに配置されます。
- SAP やハイパフォーマンス・コンピューティングなどのアプリケーションは、ベアメタル・リソースを消費します。
- パブリック・クラウドに移行できる、セキュリティー・センシティブなワークロードと規制されたワークロードは、専用の環境に移行します。
- Web、モバイル、IoT、AI、ビデオなどの SoE (Systems of Engagement、協働のための情報活用システム) は、パブリック・クラウドに移動します。

例えば、一般的なパターンとして、フロントエンド SOE アプリケーションをコンテナーとしてデプロイし、データベースとレガシー・ミドルウェアをプライベート・クラウド上の VM にデプロイします。

お客様の IT インフラストラクチャー・ニーズとビジネス・ニーズはそれぞれ固有であるため、ビジネス価値の提供を促進し、リスクを軽減し、既存の投資をむだにしないようにするモダナイゼーションへのアプローチが必要になります。IBM は、アプリケーション・モダナイゼーションに関連するお客様固有のビジネス・ニーズとテクノロジー・ニーズに対応するようにカスタマイズできる、まさにそのようなアプローチを提供しています。

このドキュメントは、アプリケーション・モダナイゼーションの手順を経て IBM Cloud に移行するまでに使用されるテクノロジーに関するさまざまな情報を提供する以下の 5 つのドキュメントの 1 つです。

リファレンス・アーキテクチャー・ガイド、VCS – ICP および CAM - 現在のセクション。

以下のプラットフォームをデプロイするためのリファレンス・アーキテクチャー。
  - **VMware vCenter Server on IBM Cloud** - IBM Cloud for VMware Solutions のオファリングであり、IBM Cloud 上で自動的にプロビジョンされる VMware ベースのプラットフォームです。
  - **IBM Cloud Private** – コンテナー化されたアプリケーションを開発して管理するためのアプリケーション・プラットフォームです。これは、コンテナー・オーケストレーター Kubernetes、プライベート・イメージ・リポジトリー、管理コンソール、モニター・フレームワーク、グラフィカル・ユーザー・インターフェースを含む統合環境で、アプリケーションのデプロイ、管理、モニター、スケーリングを行うことができる一元的な場所を提供します。
  - **IBM Cloud Automation Manager** – エンタープライズ対応の Infrastructure as Code (IaC) プラットフォームであり、リポジトリーで保管およびバージョン管理されるテンプレートを使用するだけで、Kubernetes ベースのワークロードとともに VM ベースのワークロードをプロビジョンする単一画面を提供します。

[リファレンス・アーキテクチャー・ガイド、VCS - IKS](../vcsiks/vcsiks-intro.html)

  以下のプラットフォームをデプロイするためのリファレンス・アーキテクチャー。
  - **VMware vCenter Server on IBM Cloud** - IBM Cloud for VMware Solutions のオファリングであり、IBM Cloud 上で自動的にプロビジョンされる VMware ベースのプラットフォームです。
  - **IBM Cloud Kubernetes Service** – シングル・テナント・クラスターを対象としたアプリケーション・コンテナーのデプロイメント自動化、スケーリング、および運用を行うオーケストレーション・エンジンとして Kubernetes を活用する、IBM Cloud 上の管理対象サービス。

[リファレンス・アーキテクチャー・ガイド、VCS – ネットワーキング](../vcsnsxt/vcsnsxt-intro.html)

このドキュメントでは、VCS、ICP、および IKS 内で使用されるネットワーク・テクノロジー (NSX-V、NSX-T、Calico など) に的を絞って説明しています。

[リファレンス・アーキテクチャー・ガイド、Watson および Sk8boarding コンセプト・カー](../vcscar/vcscar-intro.html)

このドキュメントは、Watson AI と機械学習の間の相互作用を実演するために「コンセプト・カー」のアプローチを使用しています。

このドキュメントでは、以下のテクノロジーを主に説明しています。
  - **Pepper** - クラウド環境と統合してアプリケーション操作と検索操作を実行する機能が組み込まれたインターフェース。

  - **VMware vCenter Server on IBM Cloud** - アプリケーションのエレメント (データベース・ワークロードなど) をホストするために使用されます。

  - **IBM Cloud Kubernetes Service** - アプリケーションのコンテナー化されたエレメントをホストするために使用されます。

  - **IBM Cloud Private** - プラットフォームとサービス・レベルのオーケストレーションを提供するために利用され、VM プラットフォームとコンテナー・プラットフォームでアプリケーションをホストおよびスケーリングする機能が組み込まれています。また、このコンポーネントにより、Watson 開発者サービスがプラットフォームで使用可能になり、AI 機能を利用できるようになります。

[リファレンス・アーキテクチャー・ガイド、VCS – コンテンツ](../vcscontent/vcscontent-intro.html)

このドキュメントでは、IBM Cloud Automation Manager で使用可能な以下のタイプのコンテンツに焦点を当てています。
- 内部カタログ・コンテンツ。例えば、「事前設定済み」Helm チャート、Terraform テンプレート、および Chef レシピなど。
- サービス・コンテンツ。例えば、Blockchain サービスや Watson サービスなど。

### 関連リンク

  * [VMware vCenter Server on IBM Cloud with Hybridity Bundle](../vcs/vcs-hybridity-intro.html)
