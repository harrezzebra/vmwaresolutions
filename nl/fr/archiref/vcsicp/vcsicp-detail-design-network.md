---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-10"

---

# Accès réseau et flux

## Accès d'application conteneur – ICP

Il existe trois méthodes principales pour obtenir un trafic/accès externe dans vos applications en cluster Kubernetes :
- NodePort
- LoadBalancer
- Ingress

### NodePort
Les ports Nodeport permettent d'exposer facilement l'accès externe à une charge de travail à des fins de développement initial et de tests, mais ils ne sont pas recommandés pour la production. La fonction Ingress ou l'équilibreur de charge sont recommandés. 

### LoadBalancer
Actuellement, la plateforme ICP prend en charge un équilibreur de charge externe pour la charge de travail d'application. 

### Ingress
La fonction Ingress est une collection de règles qui permettent aux connexions entrantes d'atteindre les services de cluster. La fonction Ingress peut être configurée afin d'octroyer aux services des URL accessibles en externe, d'effectuer l'équilibrage de charge pour le trafic, de terminer SSL, d'offrir un hébergement virtuel basé sur le nom, etc. Le noeud proxy dans l'infrastructure ICP exécute cette fonction. 

## Accès d'application conteneur – IKS
Il existe trois méthodes principales pour obtenir un trafic/accès externe dans vos applications en cluster Kubernetes :
- NodePort
- LoadBalancer
- Ingress

### NodePort
Les ports Nodeport permettent d'exposer facilement l'accès externe à une charge de travail à des fins de développement initial et de tests, mais ils ne sont pas recommandés pour la production. La fonction Ingress ou l'équilibreur de charge sont recommandés. 

### LoadBalancer
Chaque cluster IKS est mis à disposition avec un équilibreur de charge d'application (ALB) public/privé. L'ALB utilise un point d'entrée public ou privé unique et sécurisé pour acheminer les demandes entrantes vers vos applications.

### Ingress
La fonction Ingress est une collection de règles qui permettent aux connexions entrantes d'atteindre les services de cluster. La fonction Ingress peut être configurée afin d'octroyer aux services des URL accessibles en externe, d'effectuer l'équilibrage de charge pour le trafic, de terminer SSL, d'offrir un hébergement virtuel basé sur le nom, etc. 

## Flux de trafic
Les flux de trafic suivants seront décrits :
- Utilisateur externe sur Internet vers un niveau Web hébergé dans un conteneur dans ICP.
- Niveau Web hébergé dans un conteneur dans ICP vers un groupe de serveurs d'application de base de données hébergé dans une machine virtuelle dans VCS.
- Utilisateur d'entreprise sur l'accès au réseau d'entreprise vers une machine virtuelle dans VCS.

### Utilisateur externe sur Internet vers un niveau Web hébergé dans un conteneur dans ICP.
1. L'utilisateur externe émet une demande vers le niveau Web à l'aide de l'URL.
2.	Le serveur de noms de domaine est utilisé pour déterminer l'adresse IP. Cette adresse IP sera une adresse publique IBM Cloud sur un sous-réseau portable qui a été affecté à l'instance VCS. 
3.	Le réseau public acheminera automatiquement la demande vers l'hôte vSphere ESXi qui héberge la passerelle ESG.
4.	La passerelle ESG acheminera la demande vers l'adresse IP de cluster interne et le numéro de port de l'ALB ou du service Ingress. Le paquet IP sera encapsulé dans un cadre VXLAN si la passerelle ESG et l'ALB ou le service Ingress figurent sur des hôtes vSphere ESXi différents. Cette adresse IP de cluster interne est accessible uniquement dans le cluster. 
5.	Au sein du noeud worker, le proxy kube achemine la demande vers l'ALB ou le service Ingress. 
6.	Si l'application figure sur le même noeud worker, iptables est utilisé pour déterminer quelle interface interne est utilisée pour acheminer la demande. Si l'application figure sur un autre noeud worker, Calico vRouter est acheminé vers le noeud worker qui s'applique à l'aide de l'encapsulation IP-in-IP. Le paquet IP-in-IP sera encapsulé dans un cadre VXLAN pour le transport vers l'hôte vSphere ESXi sur lequel figure le noeud worker. 

### Niveau Web hébergé dans un conteneur dans ICP vers un groupe de serveurs d'application de base de données hébergé dans une machine virtuelle dans VCS.
La façon dont les tables de routage dans la passerelle et les routeurs vRouter sont renseignées varient en fonction de la méthode d'intégration. Voir l'intégration ICP et VCS. 
1.	Le niveau Web qui s'exécute dans un conteneur dans ICP émet une demande vers une base de données qui s'exécute sur une machine virtuelle dans la même instance VCS. 
2.	Le serveur de noms de domaine est utilisé pour résoudre la demande vers l'adresse IP de la base de données. 
3.	Le conteneur envoie la demande à Calico vRouter.
4.	La table de routage de vRouter est alimentée par les plages d'adresses IP hébergées sur l'instance VCS. 
5.	vRouter achemine la demande mais utilise SNAT pour remplacer l'adresse IP source, qui correspond à l'adresse IP du pod, par l'adresse IP du noeud worker. 
6.	Le noeud worker qui héberge vRouter envoie la demande à la passerelle ESG.
7.	La passerelle ESG achemine ensuite la demande vers le routeur DLR.
8.	Le routeur DLR place la demande sur le réseau VXLAN requis.
9.	La machine virtuelle de base de données reçoit la demande. 

### 	Utilisateur d'entreprise sur l'accès au réseau d'entreprise vers une machine virtuelle dans VCS
1.	Un utilisateur d'entreprise connecté au réseau interne de l'entreprise émet une demande d'une ressource sur une machine virtuelle hébergée dans VCS.
2.	Le serveur de noms de domaine est utilisé pour déterminer l'adresse IP de la machine virtuelle. Cette adresse IP figure sur un réseau qui a été étendu à IBM Cloud.
3.	Le routeur local dirige le trafic vers l'hôte vSphere qui héberge le concentrateur L2.
4.	Le concentrateur L2 encapsule la demande dans un tunnel sécurisé et la transmet au concentrateur L2 distant qui est hébergé dans IBM Cloud à l'aide de l'adresse IP de sous-réseau portable privé affectée à l'unité, via le routeur local. 
5.	La route locale examine sa table de routage et s'aperçoit que l'adresse IP pour le concentrateur L2 distant doit être envoyé à l'interface WAN. L'acheminement vers l'interface WAN est réalisé par le biais du routeur IBM Cloud XCR, via le routeur BCR.
6.	Le concentrateur L2 reçoit la demande et la place sur le réseau VXLAN qui héberge le réseau étendu. 
7.	La machine virtuelle reçoit la demande. 

## Réseau d'accès public
Par défaut, ICP et CAM nécessitent une connectivité internet pour extraire des images Docker, des chartes Helm, des modèles Terraform et des gestionnaires de packages de système d'exploitation.
Dans les dernières éditions, des installations basées sur un proxy sont prises en charge pour les installations qui ne sont pas directement connectées à Internet et qui proposent des options d'installation en mode hors ligne. 

###	Pare-feu NSX
Le pare-feu ICP NSX Edge est configuré avec des règles permettant :
*	d'activer l'accès des réseaux VXLAN à un accès public ;
*	d'activer l'accès des réseaux VXLAN à un accès réseau IBM Cloud privé ;
*	d'activer l'accès réseau IBM Cloud privé à des réseaux VXLAN.

### NSX NAT
ICP NSX NAT est configuré avec les NAT suivants :
*	SNAT pour l'accès des réseaux VXLAN à un accès public
*	SNAT pour l'accès des réseaux VXLAN à un accès réseau IBM Cloud privé
*	DNAT pour des adresses IP virtuelles de cluster ICP

### Liens connexes

* [VMware vCenter Server on IBM Cloud with Hybridity Bundle](../vcs/vcs-hybridity-intro.html)
