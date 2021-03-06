---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-03"

---

# Zerto

修復中に vSphere ESXi ホストを保守モードにできない場合、Zerto が妨げている可能性があります。 初期デプロイメント以降に Zerto を更新した場合は、以下の手順を実行してこれを修正します。 更新していない場合は、[How to place a host with an associated VRA into maintenance mode](https://www.zerto.com/myzerto/knowledge-base/place-host-into-maintenance-mode-with-vra/) の指示に従ってください。

1. Zerto Web UI にログインします。
2. ドロップダウン・メニューから、**「Site Settings」**を選択します。
3. **「policies」タブ**を選択して、**「Allow Zerto to always enter hosts to maintenance mode during remediation」**が選択されていることを確認します。
4. Zerto からログアウトします。

### 関連リンク

* [VMware HCX on IBM Cloud Solution](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [VMware Solutions on IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware) (デモ)
