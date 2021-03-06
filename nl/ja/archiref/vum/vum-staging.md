---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

{:tip: .tip}
{:note: .note}
{:important: .important}

# ステージングおよび修復

パッチおよび拡張機能は、即時に適用することなく VUM から vSphere ESXi ホストにダウンロードするように、オプションで修復前にステージングできます。 修復中に、VUM によってパッチ、拡張、およびアップグレードがインベントリー・オブジェクトに適用されます。 パッチおよび拡張機能をステージングしておくと、これらが既にホスト上でローカルに使用可能となるため、修復プロセスが加速されます。

修復プロセスでいずれかのホストが保守モードにならない場合、VUM でエラーが報告され、修復プロセスは停止して失敗します。 修復済みの vSphere ESXi ホストは、更新されたレベルのままとなります。

修復プロセスがスムーズに機能するためには、DPM、HA アドミッション制御、フォールト・トレランスなどの一部のクラスター機能を無効にし、取り外し可能なデバイスを仮想マシンから切断して、VM を他のホストにマイグレーションする際に DRS で問題が発生しないようにすることをお勧めします。
また、修復ウィザードの実行中に「レポートを生成」して、修復プロセスが失敗する原因となる不整合な設定がホスト/VM レベルに存在しないことを確認できます。

1.	vSphere Web Client を使用して、**「Home」** > **「Hosts and Clusters」**を選択します。
2.	データ・センター、クラスター、またはホストを右クリックし、**「Stage Patches」**をクリックします。
3.	ステージ・ウィザードの「Baseline Selection」ページで、ステージングするパッチと拡張機能のベースラインを選択します。
4.	パッチおよび拡張機能を適用するホストを選択し、**「Next」**をクリックします。 単一のホストにパッチおよび拡張機能をステージングすることを選択した場合は、デフォルトでそれが選択されています。
5.	オプションで、ステージ操作から除外するパッチおよび拡張機能を選択解除します。 パッチおよび拡張機能のリスト内を検索するには、「Filter」ボックスのテキスト・ボックスにテキストを入力します。 **「次へ」**をクリックします。
6.	「Ready to Complete」ページを確認して、**「Finish」**をクリックします。

特定のホストについてステージングされたパッチと拡張機能の数は、「Update Manager」タブの下部ペインにある「Patches and Extensions」列に表示されます。 修復が正常に完了すると、修復中にインストールされたかどうかにかかわらず、ステージングされたすべてのパッチおよび拡張機能はホストから削除されます。
修復とは、スキャンの完了後に、VUM によりパッチ、拡張機能、およびアップグレードを vSphere ESXi ホスト、仮想マシン、または仮想アプライアンスに適用し、選択したオブジェクトを準拠させるプロセスです。 単一ホスト、仮想マシン、または仮想アプライアンスを修復することも、フォルダー、クラスター、またはデータ・センター・レベルで修復することもできます。 VUM では、手動修復またはスケジュールされた修復のいずれかを使用して、以下のインベントリー・オブジェクトの修復がサポートされます。
*	パッチ、拡張機能、およびアップグレードの修復の場合には、ESXi ホスト。
*	VMware Tools と仮想マシンのハードウェア・アップグレードの場合には、電源オン、中断、または電源オフの状態の仮想マシンおよびテンプレート。
*	仮想アプライアンス・アップグレードの場合は、VMware Studio 2.0 以降で作成された電源オンの状態の仮想アプライアンス。

更新に必要な場合、ホストは修復前に保守モードになります。 VCSA では、ホストが保守モードになる前に、仮想マシンを VCS インスタンス内の他のホストにマイグレーションします。

## vSAN クラスター内のホストの場合
vSAN クラスターの一部であるホストについて、以下の動作に注意してください。
* ホスト修復プロセスは、完了するまでに非常に時間がかかる場合があります。
* 設計上、VSAN クラスターから保守モードにできるホストは常に 1 つのみです。
* VUM は、ホストを並行して修復するオプションを設定した場合でも、VSAN クラスターの一部であるホストを順次修復します。
* ホスト上のいずれかの仮想マシンで「Number of failures to tolerate=0」が設定された VM ストレージ・ポリシーを使用している場合、ホストが保守モードになると異常な遅延が発生する可能性があります。 この遅延は、vSAN で、仮想マシン・データを vSAN データ・ストア・クラスター内のディスク間でマイグレーションする必要があり、この処理に長時間かかる可能性があるため発生します。 これを回避するには、VM ストレージ・ポリシーで「Number of failures to tolerate=1」を設定します。これにより、vSAN データ・ストア内に仮想マシン・ファイルのコピーが 2 つ作成されます。
* ホスト上のいずれかの仮想マシンで「Number of failures to tolerate=1」が設定された VM ストレージ・ポリシーを使用している場合、ホストが保守モードになると VM は非冗長になります。 これを許容できない場合は、[仮想マシン vSAN の冗長性](vum-vsan-redundancy.html)を参照してください。

ホストおよびクラスターを修復するには、以下の手順を実行します。
1.	vSphere Web Client を使用して、**「Home」** > **「Hosts and Clusters」**を選択します。
2.	インベントリー・オブジェクト・ナビゲーターから、データ・センター、クラスター、またはホストを選択し、**「Update Manager」**タブをクリックして、**「Remediate」**をクリックします。 コンテナー・オブジェクトを選択した場合、選択したオブジェクトの下のすべてのホストが修復されます。 修復ウィザードが開きます。
3.	ホストで実行する更新のタイプに応じて、**「Patch Baselines」**または**「Extension Baselines」**を選択します。 修復ウィザードの「Select baseline」ページで、適用する**ベースライン・グループ**および**ベースライン**を選択します。
4.	修復するターゲット・ホストを選択し、**「Next」**をクリックします。 コンテナー・オブジェクトではなく単一ホストを修復することを選択した場合は、デフォルトでホストが選択されています。
5.	オプションで、**「Patches and Extensions」**ページで修復プロセスから除外する特定のパッチまたは拡張機能を選択解除して、**「Next」**をクリックします。
6.	オプションで、**「Advanced options」**ページで後で実行するように修復をスケジュールするオプションを選択し、タスクに固有の名前とオプションの説明を指定します。 スケジュールされたタスクに設定する時刻は、VCSA 上での時刻になります。 オプションで、ホスト上のサポートされないデバイスまたはサポートされなくなった VMFS データ・ストアに関する警告を無視して修復を続行するオプションを選択します。 **「次へ」**をクリックします。
7.	ホストの **「Remediation Options」**ページの**「VM Power state」**ドロップダウン・メニューから、修復するホスト上で実行されている仮想マシンおよび仮想アプライアンスの電源状態の変更を選択できます。 ホスト上の仮想マシンが電源オフまたは中断の状態になるか、vMotion を使用して DRS クラスター内の他のホストにマイグレーションされるまで、ホストを保守モードにすることはできません。 一部の更新では、修復前にホストを保守モードにする必要があります。 ホストが保守モードのときに、仮想マシンおよびアプライアンスを実行することはできません。 仮想マシンの可用性よりもホストの修復ダウン時間の短縮を優先する場合は、仮想マシンおよび仮想アプライアンスを修復前にシャットダウンまたは中断することを選択できます。 DRS クラスターでは、仮想マシンの電源をオフにしない場合、修復にかかる時間は長くなりますが、仮想マシンは vMotion を使用して他のホストにマイグレーションされるため、修復プロセス全体を通して使用可能です。 選択項目は以下のとおりです。

  - **Power Off virtual machines** - 修復前に、すべての仮想マシンおよび仮想アプライアンスの電源をオフにします。
  - **Suspend virtual machines** - 修復前に、実行中のすべての仮想マシンおよび仮想アプライアンスを中断します。
  - **Do Not Change VM Power State** - 仮想マシンおよび仮想アプライアンスを現在の電源状態のままにします。

8.	オプションで、**「Disable any removable media devices connected to the virtual machine on the host」**を選択します。 VUM では、CD ドライブ、DVD ドライブ、またはディスケット・ドライブが接続された仮想マシンが存在するホストは修復しません。 クラスター環境では、メディア・デバイスが接続されていると、宛先ホストに同一のデバイスまたはマウントされた ISO イメージが存在しない場合に vMotion が動作しなくなる可能性があり、これにより、ソース・ホストを保守モードにすることもできなくなります。 修復後、VUM は、取り外し可能メディア・デバイスがまだ使用可能であれば、それらのデバイスを再接続します。
9.	オプションで、**「Retry entering maintenance mode in caseof failure」**を選択し、再試行回数および再試行間の待機時間を指定します。 VUM では、再試行遅延期間を待機し、「Number of retries」フィールドに指定した回数だけホストを保守モードにすることを試行します。
10.	VCS インスタンスでは、「ESXi Patch Settings」の下のチェック・ボックスを選択して、Update Manager により、PXE ブートされた電源オンの状態の ESXi ホストにパッチを適用できるようにする必要はありません。
11.	**「次へ」**をクリックします。
12.	クラスター内のホストを修復する場合は、クラスター修復オプションを編集します。 **「Cluster remediation options」**ページは、クラスターを修復する場合にのみ使用できます。 以下のオプションを選択できます。

*	**Disable Distributed Power Management (DPM)** - 選択されたいずれかのクラスターについてこのオプションが有効になっている場合、VUM では、DPM がアクティブになっているクラスターを修復しません。 DPM では、クラスター内で実行中の仮想マシンのリソース使用をモニターします。 容量が十分余っている場合、DPM は、仮想マシンをクラスター内の他のホストに移動し、元のホストをスタンバイ・モードにして電力を節約することを推奨します。 ホストをスタンバイ・モードにすると、修復が中断される可能性があります。
*	**Disable High Availability admission control** - 選択されたいずれかのクラスターについてこのオプションが有効になっている場合、VUM では、HA アドミッション制御がアクティブになっているクラスターを修復しません。 アドミッション制御は、クラスター内のフェイルオーバー容量を確保するために VMware HA によって使用されるポリシーです。 修復時に HA アドミッション制御が有効になっている場合、クラスター内の仮想マシンは、vMotion を使用してマイグレーションされない可能性があります。
*	**Disable Fault Tolerance (FT)** - このオプションが有効になっている場合、 選択されたクラスター内のすべてのフォールト・トレラント仮想マシンに影響を及ぼします。ホスト上のいずれかの仮想マシンについて FT がオンになっている場合、VUM では、そのホストを修復しません。 FT を有効にするには、プライマリー仮想マシンとセカンダリー仮想マシンが実行されている各ホストのバージョンが同じで、インストールされているパッチが同じである必要があります。 これらのホストに異なるパッチを適用すると、FT を再度有効にすることはできなくなります。
*	**Enable parallel remediation for the hosts in the selected clusters** - クラスター内のホストを並行して修復します。 この設定が選択されていない場合、VUM では、クラスター内のホストを順次修復します。 並列修復について、以下のオプションのいずれかを選択できます。
    - VUM で、DRS 設定を中断することなく並行して修復可能なホストの最大数を継続的に評価できるように設定できます。
    - 修復するクラスターごとに、並行して修復するホストの数の制限を指定できます。 VUM では、仮想マシンが電源オフまたは中断の状態になっているホストのみを並行して修復することに注意してください。 「Host Remediation Options」ページの「Maintenance Mode Options」ペインの「VM Power State」メニューから、仮想マシンの電源をオフにするか、仮想マシンを中断するかを選択できます。 設計上、vSAN クラスターから保守モードにできるホストは常に 1 つのみです。 VUM では、ホストを並行して修復するオプションを選択した場合でも、vSAN クラスターの一部であるホストを順次修復します。
*	ホストを保守モードにする必要がある場合は、**電源オフおよび中断の状態にある仮想マシンをクラスター内の他のホストにマイグレーションします**。 Update Manager では、中断および電源オフの状態にある仮想マシンを、保守モードにする必要があるホストからクラスター内の他のホストにマイグレーションします。 **「Maintenance Mode Settings」**ペインで、修復前に仮想マシンの電源をオフにするか、仮想マシンを中断するかを選択できます。
13.	「Ready to complete」ページで、オプションで**「Pre-check Remediation」**をクリックし、クラスター修復オプション・レポートを生成して、**「OK」**をクリックします。 「Cluster Remediation Options Report」ダイアログ・ボックスが開きます。 このレポートをエクスポートするか、独自のレコードに対するエントリーをコピーするかを選択して、**「Next」**をクリックします。
14.	「Ready to Complete」ページを確認して、**「Finish」**をクリックします。

### 関連リンク

* [VMware HCX on IBM Cloud Solution Architecture](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [VMware Solutions on IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware) (デモ)
