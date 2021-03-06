---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

# Exigences et planification pour les instances vCenter Server

Passez en revue les exigences suivantes avant de commander vos instances VMware vCenter Server. Planifiez votre instance en fonction de l'emplacement de l'{{site.data.keyword.CloudDataCent}}, de vos besoins en capacité de charge de travail et de vos besoins en services complémentaires.

## Exigences liées au compte IBM Cloud

Le compte {{site.data.keyword.cloud_notm}} que vous utilisez doit répondre à certaines exigences. Pour plus d'informations, voir [Exigences liées au compte {{site.data.keyword.cloud_notm}}](../vmonic/slaccountrequirement.html).

## Disponibilité du centre de données IBM Cloud

Les déploiements unifiés vCenter Server ont des exigences strictes quant à l'infrastructure physique. Par conséquent, vous ne pouvez déployer des instances que dans des {{site.data.keyword.CloudDataCents_notm}} qui répondent à ces exigences. Les {{site.data.keyword.CloudDataCents_notm}} suivants sont disponibles pour un déploiement vCenter Server :

Tableau 1. {{site.data.keyword.CloudDataCents_notm}} disponibles pour les instances vCenter Server

| {{site.data.keyword.CloudDataCent_notm}} | Emplacement | Région | Options de serveur |
|:----------------------|:---------|:-------|:---------------|
| AMS03 | Amsterdam | Europe | Skylake, Broadwell |
| CHE01 | Chennai | Asie-Pacifique | Skylake, Broadwell |
| DAL09 | Dallas | Sud des Etats-Unis | Skylake, Broadwell |
| DAL10 | Dallas | Sud des Etats-Unis | Skylake, Broadwell, Petite, Moyenne, Grande |
| DAL12 | Dallas | Sud des Etats-Unis | Skylake, Broadwell |
| DAL13 | Dallas | Sud des Etats-Unis | Skylake, Broadwell |
| FRA02 | Francfort | Europe | Skylake, Broadwell, Petite, Moyenne, Grande |
| FRA04 | Francfort | Europe | Skylake, Broadwell |
| HKG02 | Hong Kong | Asie-Pacifique | Skylake, Broadwell |
| LON02 | Londres | Europe | Skylake, Broadwell |
| LON04 | Londres | Europe | Skylake, Broadwell |
| LON06 | Londres | Europe | Skylake, Broadwell, Petite, Moyenne, Grande |
| MEL01 | Melbourne | Asie-Pacifique | Skylake, Broadwell |
| MEX01 | Querétaro | Sud des Etats-Unis | Skylake, Broadwell |
| MIL01 | Milan | Europe | Skylake, Broadwell |
| MON01 | Montréal | Est des Etats-Unis | Skylake, Broadwell |
| OSL01 | Oslo | Europe | Skylake, Broadwell |
| PAR01 | Paris | Europe | Skylake, Broadwell |
| SAO01 | São Paulo | Amérique du Sud | Skylake, Broadwell |
| SEO01 | Séoul | Asie-Pacifique | Skylake, Broadwell |
| SJC03 | San José | Ouest des Etats-Unis | Skylake, Broadwell, Petite, Moyenne, Grande |
| SJC04 | San José | Ouest des Etats-Unis | Skylake, Broadwell |
| SNG01 | Singapour | Asie-Pacifique | Skylake, Broadwell |
| SYD01 | Sydney | Asie-Pacifique | Skylake, Broadwell |
| SYD04 | Sydney | Asie-Pacifique | Skylake, Broadwell |
| TOK02 | Tokyo | Asie-Pacifique | Skylake, Broadwell |
| TOR01 | Toronto | Est des Etats-Unis | Skylake, Broadwell, Petite, Moyenne, Grande |
| WDC04 | Washington, DC | Est des Etats-Unis | Skylake, Broadwell, Petite, Moyenne, Grande |
| WDC06 | Washington, DC | Est des Etats-Unis | Skylake, Broadwell |
| WDC07 | Washington, DC | Est des Etats-Unis | Skylake, Broadwell |

Un petit sous-ensemble d'{{site.data.keyword.CloudDataCents_notm}} offre des options de serveur bare metal **Petite**, **Moyenne** et **Grande** préconfigurées. Selon la disponibilité et l'approvisionnement du stock, les {{site.data.keyword.CloudDataCents_notm}} peuvent afficher un indicateur de statut sur la console {{site.data.keyword.vmwaresolutions_short}} pour vous aider à planifier vos déploiements.

Tableau 2. Indicateurs de statut pour les {{site.data.keyword.CloudDataCents_notm}} lors de la commande d'instances vCenter Server

| Statut | Détails du statut |
|:------------------------------|:--------------------------------------------------|
| Coming Soon                   | L'{{site.data.keyword.CloudDataCent_notm}} n'est pas disponible actuellement. |
| Temporarily Out of Inventory  | L'{{site.data.keyword.CloudDataCent_notm}} n'est pas disponible actuellement. |
| Limited Inventory             | L'{{site.data.keyword.CloudDataCent_notm}} a une disponibilité limitée et la commande risque de ne pas être honorée. |

## Sauvegarde des composants de gestion

Vous êtes chargé de gérer et d'assurer la disponibilité de tous les composants d'instance. Il est fortement recommandé de planifier la sauvegarde ou la haute disponibilité de tous les composants de gestion. Pour plus d'informations, voir [Sauvegarde des composants](../archiref/solution/solution_backingup.html).

## Services pour les instances vCenter Server

Vous pouvez commander des services complémentaires pour votre instance en fonction de vos besoins, par exemple, la reprise après incident. Pour plus d'informations, voir[Commande, affichage et retrait de services pour des instances vCenter Server](vc_addingremovingservices.html).

## Remarques sur la capacité

Pour plus d'informations sur la capacité, voir [Mise à l'échelle de la capacité](../archiref/solution/solution_scaling.html).

### Liens connexes

* [Présentation de vCenter Server](vc_vcenterserveroverview.html)
* [Commande d'instances vCenter Server](vc_orderinginstance.html)
* [Extension et réduction de capacité pour des instances vCenter Server](vc_addingremovingservers.html)
* [Commande, affichage et retrait de services pour des instances vCenter Server](vc_addingremovingservices.html)
