---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

# Application de pilotes NIC natifs

ESXi 6.5 contient de nombreux nouveaux pilotes natifs qui remplacent les anciens pilotes vmklinux. Alors que la plupart de ces nouveaux pilotes sont activés par défaut après l'installation ou la mise à niveau, trois de ces pilotes sont désactivés par défaut, car ils ne prennent pas en charge toutes les fonctions des pilotes vmklinux correspondants.

ixgben est un pilote natif qui remplace le pilote vmklinux net-ixgbe mais qui ne prend pas en charge SR-IOV et SW FcOE. L'automatisation ICVS n'aura pas permis d'activer ce pilote lors de la mise à disposition de votre hôte vSphere ESXi. Il est conseillé d'activer ce pilote pour les avantages qu'il offre en matière de performances. La procédure suivante présentée dans cette annexe vous montre comment activer et désactiver les pilotes natifs à l'aide de l'interface de ligne de commande de vSphere (vCLI).

Avant d'entreprendre cette tâche, récupérez les adresses IP IPMI, les ID de connexion et les mots de passe de tous les hôtes physiques sur le [portail de l'infrastructure IBM Cloud](https://control.softlayer.com/devices). C'est obligatoire dans le cadre d'un retour à l'état initial ou pour suivre la progression d'une mise à niveau lorsqu'il n'existe aucun accès réseau direct à l'hôte.

Pour chaque hôte, procédez comme suit :
1. Utilisez le client vSphere Web Client pour placer l'hôte vSphere ESXi en mode maintenance en cliquant sur **Home** > **Host and Clusters**. Dans le panneau de navigation, sélectionnez l'hôte vSphere ESXi et cliquez avec le bouton droit de la souris sur l'hôte et sélectionnez **Maintenance Mode** > **Enter Maintenance Mode**. Comme l'hôte fait partie d'un cluster DRS automatisé, les machines virtuelles sont migrées sur d'autres hôtes lorsque l'hôte bascule en mode maintenance.
2. Connectez vous avec SSH à l'hôte vSphere ESXi, en utilisant les détails issus de la console IC4VS.
3. Exécutez la commande vCLI suivante pour activer les pilotes ixgben natifs :
  `esxcli system module set --enabled=true --module=ixgben`
4. Exécutez la commande vCLI suivante pour redémarrer l'hôte vSphere ESXi :
  `system shutdown reboot --reason “Install ixgben driver”`
5. Dès que l'hôte vSphere ESXI a été redémarré, reconnectez-vous à l'hôte en utilisant SSH. Exécutez la commande vCLI suivante et vérifiez que le pilote ixgben est chargé (“loaded”) (dans la première colonne) et activé (“enabled”) (dans la seconde colonne) :
  `esxcli system module list |grep ixg`
6. Si les pilotes sont activés, dans vSphere Web Client, sélectionnez l'hôte dans le panneau de navigation, cliquez avec le bouton droit de la souris et sélectionnez **Maintenance Mode** > **Exit Maintenance Mode**. Sélectionnez l'hôte suivant et activez les pilotes jusqu'à que tous les hôtes soient traités.
7. Si la modification ne fonctionne pas, pour revenir à l'état antérieur, exécutez la commande suivante :
  `esxcli system module set --enabled=false --module=ixgben`

8. Si vous ne pouvez pas vous connecter à l'hôte sur le réseau, exécutez la commande précédente à partir de la console à l'aide de la fenêtre de contrôle d'IBM Cloud.
9. Après avoir redémarré l'hôte vSphere ESXi, vous pouvez observer que le pilote ixgbe par défaut est chargé et activé.

Si vous souhaitez revenir à l'état antérieur et que vous ne pouvez pas vous connecter via SSH à l'hôte vSphere ESXi, vous devez vous connecter à la console KVM pour l'hôte qui doit être rétabli via la fenêtre de contrôle d'IBM Cloud.

Utilisez l'ID et le mot de passe répertoriés dans la fenêtre de contrôle d'IBM Cloud avec l'adresse IP IPMI pour vous connecter à l'interface Web d'IPMI. Vous devez être connecté au centre de données dans lequel se trouve l'hôte via le réseau privé virtuel (VPN). Pour plus d'informations, voir [Initiation au VPN](../../../../infrastructure/iaas-vpn/getting-started.html).

1. Accédez à la section Détails de l'unité, page Gestion à distance correspondant à l'hôte vSphere ESXi et sélectionnez **Actions** > **Console KVM**. Une autre fenêtre s'affiche en vous demandant le nom d'utilisateur et le mot de passe IPMI.
2. Sélectionnez **Contrôle à distance** > **iKVM/HTML5** et cliquez sur **iKVM/HTML5** pour relancer. Vous pourrez maintenant accéder à la console de l'hôte vSphere ESXi.
3. Si l'hôte répond aux commandes, utilisez la combinaison de touches **ALT-F1** dans la console pour accéder à la console de l'hôte ESXi. Utilisez les données d'identification de l'hôte pour vous connecter.
4. Si l'hôte ne répond pas, utilisez les menus d'IPMI pour mettre l'hôte sous tension.
5. Observez attentivement la console HTML5 au redémarrage de l'hôte. Vous ne disposez que de quelques secondes pour passer en mode reprise lorsque ESXi commence à redémarrer.
6. Appuyez simultanément sur les touches **CMD + R** pour passer en mode reprise.
7. Entrez **“Y”** pour passer en mode reprise et démarrer le serveur ESXi avec la version précédente.
8. Surveillez sa progression dans la console. Cette opération peut prendre de 10 à 20 minutes.

### Liens connexes

* [VMware HCX on IBM Cloud Solution Architecture](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [VMware Solutions on IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware) (démonstrations)
