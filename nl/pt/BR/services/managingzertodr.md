---

copyright:

  years:  2016, 2018

lastupdated: "2018-09-26"

---

# Gerenciando o Zerto on IBM Cloud

Depois que o serviço Zerto on {{site.data.keyword.cloud}} é implementado em sua instância, é possível configurar ou atualizar o Zerto Virtual Replication e implementar mais Dispositivos de Replicação Virtual nos servidores ESXi recém-incluídos.

## Usando seu próprio certificado para Zerto

Como uma melhor prática, use seu próprio certificado SSL para o Zerto Virtual Manager (ZVM). Depois de ter implementado o Zerto on {{site.data.keyword.cloud_notm}}, substitua o certificado SSL para o ZVM por seu próprio certificado. Para obter mais informações, veja [Como usar um certificado SSL do CER para substituir o certificado autoassinado para o ZVM, ZSSP ou ZCM](https://www.zerto.com/myzerto/knowledge-base/how-to-use-a-cer-ssl-certificate-to-replace-the-self-signed-certificate-for-the-zvm-zssp-or-zcm/){:new_window}.

## Gerenciando a configuração de replicações do Zerto

Para gerenciar a configuração de replicações do Zerto, efetue login no console do Zerto Virtual Replication usando as credenciais do vCenter com permissões de administrador. Por exemplo, reemparelhando instâncias do Zerto ou configurando grupos de proteção virtual para replicar máquinas virtuais.

Quando você está replicando entre as diferentes instâncias do {{site.data.keyword.cloud_notm}} Zerto, é possível configurar a replicação diretamente entre as instâncias do Zerto. Se você está replicando entre a instância do {{site.data.keyword.cloud_notm}} Zerto e seu próprio data center, você mesmo deve instalar o Zerto em seu próprio data center. Essa instância pode licenciar-se automaticamente quando você a emparelha com a instância do {{site.data.keyword.cloud_notm}} Zerto.

A replicação do Zerto não suporta a passagem de Conversão de Endereço de Rede (NAT). Estabelecer conectividade entre a instância do {{site.data.keyword.cloud_notm}} Zerto e seu próprio data center pode requerer a customização de rotas nos dispositivos Zerto Virtual Manager (ZVM) ou Zerto Virtual Replication Appliances (VRAs) em ambos os lados. Estabelecer conectividade também pode requerer tunelamento seguro entre os sites. Quando você está configurando ou reconfigurando rotas em dispositivos ZVM, deve-se assegurar que todos os dispositivos ZVM possam se conectar com êxito ao `zerto.com` para o relatório de uso. É possível verificar essa conexão abrindo uma sessão do navegador para `https://www.zerto.com` do dispositivo ZVM.

**Nota**: O Management VMware NSX Edge Services Gateway (ESG) de instâncias do Cloud Foundation e do vCenter Server no {{site.data.keyword.cloud_notm}} é pré-configurado para permitir comunicações HTTPS (TCP porta 443) de saída que se originam do ZVM.

## Atualizando o Zerto Virtual Replication

Para atualizar o Zerto Virtual Replication, efetue login no console do Zerto Virtual Replication.

## Implementando VRAs em servidores ESXi recém-incluídos

Quando você inclui ou remove servidores ESXi para o cluster primário de sua instância, os VRAs são automaticamente implementados ou removidos. Os VRAs não são implementados automaticamente em servidores ESXi nos clusters secundários de sua instância. Você mesmo pode implementar VRAs por meio do console do Zerto Virtual Replication.

### Links relacionados

* [ Zerto on  {{site.data.keyword.cloud_notm}}  visão geral ](addingzertodr.html)
* [Solicitando serviços gerenciados para o Zerto on {{site.data.keyword.cloud_notm}}](managing_zerto_services.html)
* [Website zerto.com](https://www.zerto.com){:new_window}
* [Documentação técnica do Zerto](https://www.zerto.com/myzerto/technical-documentation/){:new_window}
* [Recuperação de desastre Zerto](https://www.ibm.com/cloud/garage/architectures/virtualizationArchitecture/zerto){:new_window}
* [Explicação de alertas do Zerto Virtual Replication](https://www.zerto.com/myzerto/knowledge-base/explanation-of-zvr-alerts/)
