---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-25"

---

# Pedindo, visualizando e removendo serviços para instâncias do Cloud Foundation

É possível pedir serviços para suas instâncias do VMware Cloud Foundation, como uma solução de recuperação de desastre. Quando você não precisar mais desses serviços, será possível removê-los de suas instâncias.

## Serviços disponíveis para instâncias do Cloud Foundation

A tabela a seguir mostra os serviços que estão disponíveis para instâncias do Cloud Foundation, junto com as versões de serviço instaladas.

Tabela 1. Serviços disponíveis para instâncias do Cloud Foundation

| Nome do Serviço | Versão do Serviço | Versão da instância |
|----------------------------------------------------------------------------------------|------------------|
| [F5 on {{site.data.keyword.cloud}}](../services/f5_considerations.html)                                 | BIG-IP VE v13.1 | V1.9 e mais recentes |
| [FortiGate Security Appliance on {{site.data.keyword.cloud_notm}}](../services/fsa_considerations.html)       | Série 300 | V1.8 e mais recentes |
| [FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}}](../services/fortinetvm_considerations.html) | 6.0.3 | V2.0 e mais recentes |
| [HyTrust CloudControl on {{site.data.keyword.cloud_notm}}](../services/htcc_considerations.html)              | 5.4.0 | V2.3 e mais recentes |
| [HyTrust DataControl on {{site.data.keyword.cloud_notm}}](../services/htdc_considerations.html)              | 4.2.1 | V2.3 e mais recentes |
| [HyTrust KeyControl on {{site.data.keyword.cloud_notm}}](../services/htkc_considerations.html)              | 4.2 | V2.5 e mais recente |
| [IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}}](../services/spp_considerations.html)  | 10.1.1 Correção 1 | V2.2 e mais recentes |
| [KMIP for VMware on {{site.data.keyword.cloud_notm}}](../services/kmip_considerations.html)                  |   | V2.2 e mais recentes |
| [Veeam on {{site.data.keyword.cloud_notm}}](../services/veeam_considerations.html)                          | 9.5u3 | V1.8 e mais recentes |
| [Zerto on {{site.data.keyword.cloud_notm}}](../services/addingzertodr.html)                                 | 6.0 atualização 3 | V1.2 e mais recentes |

## Procedimento para incluir serviços em instâncias do Cloud Foundation

Para incluir um serviço em sua instância do Cloud Foundation, clique no link de serviço apropriado na tabela anterior para revisar as considerações para o serviço e verifique os componentes que estão implementados. Depois, siga as instruções no tópico apropriado de serviços de solicitação para incluir o serviço em sua instância.

### Resultados da instalação de serviço

Quando a instalação do serviço for concluída com êxito, você será notificado por e-mail e o serviço será exibido na página **Serviços** da instância com o status **Instalado**.

## Procedimento para visualizar serviços para instâncias do Cloud Foundation

1. No console do {{site.data.keyword.vmwaresolutions_short}}, clique em **Instâncias implementadas** na área de janela de navegação esquerda.
2. Na tabela **Instâncias do Cloud Foundation**, clique na instância para a qual você deseja visualizar serviços.
3. Clique em **Serviços** na área de janela de navegação esquerda.
4. Na página **Serviços**, clique em um serviço para revisar informações sobre ele, como o status de serviço e outros detalhes.
5. Dependendo do serviço visualizado, é possível acessar os consoles de serviço usando as credenciais fornecidas nos detalhes do serviço e gerenciar o serviço por meio deles.

## Procedimento para remover serviços para instâncias do Cloud Foundation

1. No console do {{site.data.keyword.vmwaresolutions_short}}, clique em **Instâncias implementadas** na área de janela de navegação esquerda.
2. Na tabela **Instâncias do Cloud Foundation**, clique na instância para a qual você deseja remover serviços.
3. Clique em **Serviços** na área de janela de navegação esquerda.
4. Na página **Serviços**, localize a instância de serviço que você deseja remover e clique no ícone **Excluir**.
5. Na janela **Excluir serviços**, revise as considerações ou os avisos, se houver algum. Selecione **Eu entendo** e clique em **Excluir**.

### Resultados da remoção de serviço

Depois que sua solicitação para remoção do serviço for aceita, o status do serviço mudará para **Removendo**.

Quando a remoção do serviço for concluída com êxito, você será notificado por e-mail e o serviço será removido da página **Serviços** da instância.

**Atenção:** você é cobrado até o término do ciclo de faturamento do {{site.data.keyword.cloud_notm}} pelos serviços removidos.

### Links relacionados

* [Perguntas mais frequentes](../vmonic/faq.html)
