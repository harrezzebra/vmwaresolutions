---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

# Atualizando clusters vSAN

O vSAN gera linhas de base do sistema e grupos de linhas de base para uso com o VUM e é possível usar essas linhas de base recomendadas para atualizar software, correções e extensões para os hosts vSphere ESXi em sua instância do VCS usando vSAN. O vSAN 6.6.1 e mais recente gera recomendações de construção automatizada para clusters vSAN. O vSAN combina informações no VMware Compatibility Guide e no catálogo de liberações do vSAN com informações sobre as liberações do vSphere ESXi instaladas.

Essas atualizações recomendadas fornecem a melhor liberação disponível para manter seu hardware em um estado suportado.
* **Linhas de base do sistema vSAN** - as recomendações de construção do vSAN são fornecidas por meio das linhas de base do sistema vSAN para VUM. O vSAN gera um grupo de linhas de base para cada cluster vSAN e elas são listadas na área de janela Linhas de base da guia Linhas de base e grupos. O VUM varre automaticamente cada cluster vSAN para verificar a conformidade com relação ao grupo de linhas de base. No entanto, para fazer upgrade do cluster vSAN, deve-se corrigir manualmente a linha de base do sistema por meio do VUM, é possível corrigir a linha de base do sistema vSAN em um único host ou no cluster inteiro.
* **Catálogo de liberações do vSAN** - o catálogo de liberações do vSAN mantém informações sobre as liberações disponíveis, a ordem de preferência para liberações e as correções críticas necessárias para cada liberação. O vSAN requer conectividade de Internet para acessar o catálogo de liberações. Você não precisa estar inscrito no Customer Experience Improvement Program (CEIP) para vSAN para acessar o catálogo de liberações.
* Trabalhando com **Recomendações de construção do vSAN** - o VUM verifica as liberações do vSphere ESXi instaladas com relação às informações no Hardware Compatibility List (HCL) no VMware Compatibility Guide. Isso determina o caminho de upgrade correto para cada cluster vSAN, com base no catálogo atual de Liberações do vSAN. O vSAN também inclui os drivers necessários e as atualizações de correção para a liberação recomendada em sua linha de base do sistema. As recomendações de construção do vSAN asseguram que cada cluster vSAN permaneça no status de compatibilidade de hardware atual ou melhor. Se o hardware no cluster vSAN não estiver incluído no HCL, o vSAN recomendará um upgrade para a liberação mais recente.

O upgrade do cluster vSAN continua na sequência de tarefas a seguir:
* **Ativar o fluxo de trabalho Funcionamento on-line do vSAN** - esse fluxo de trabalho ativa as linhas de base do vSAN no VUM para que as atualizações possam ser revisadas e corrigidas. Isso precisa ser realizado inicialmente somente para ativar o vSAN com o VUM
* **Pré-requisitos** – entenda os pré-requisitos, o processo e as restrições
* ** Fazer upgrade do vCenter Server Appliance **. Para obter mais informações, consulte [Atualização do VCSA e vCenters vinculados por SSO](vum-updating-vcsa.html).
* **Fazer upgrade dos hosts vSphere ESXi** – para obter mais informações, veja [Criando linhas de base e anexando a objetos de inventário](vum-baselines.html).
* **Fazer upgrade do formato de disco vSAN** - consulte Fazer upgrade do formato de disco vSAN. O upgrade do formato de disco é opcional, mas, para obter melhores resultados, faça upgrade dos objetos para usar a versão mais recente. O formato no disco expõe seu ambiente ao conjunto de recursos completo de vSAN.

## Ativar o fluxo de trabalho de funcionamento on-line do vSAN

Seguir as tarefas nesta seção tornarão as linhas de base do vSAN disponíveis no VUM. O vSAN 6.6.1 e mais recente fornece um processo de atualização automatizada contínua para assegurar que um cluster vSAN esteja atualizado com a melhor liberação disponível para manter a sua instância do VCS em um estado suportado com:
* **Recomendações de versão do vSAN** - geradas automaticamente usando informações do VMware Compatibility Guide, do catálogo de liberações do vSAN e do reconhecimento da configuração de hardware subjacente. Isso também inclui os drivers necessários e as atualizações de correção para a liberação recomendada em sua linha de base do sistema.
* **Recomendações de construção do vSAN** - assegura que os clusters permaneçam no status de compatibilidade de hardware atual ou melhor.

Assegure-se de que o VCSA seja o vCenter 6.5 Correção 2 ou a versão mais recente antes de continuar, pois isso corrige alguns problemas de uso de proxy. Para obter mais informações, consulte [Atualização do VCSA e vCenters vinculados por SSO](vum-updating-vcsa.html).

Para ver as atualizações do vSAN no VUM, o fluxo de trabalho Funcionamento on-line do vSAN é seguido. Portanto, o Funcionamento on-line do vSAN precisa se conectar aos sites `vcsa.vmware.com` e `vmware.com` para executar essas verificações de funcionamento on-line. Para ativar o fluxo de trabalho Funcionamento on-line do vSAN, precisamos:
* Configurar o VCSA para usar o proxy.
* Configurar o vSAN para usar o proxy.
* Ativar o Customer Experience Improvement Program (CEIP).
* Executar um upload de teste e validar se o upload funcionou.

A primeira etapa é incluir suas credenciais do my.vmware.com no vSAN Build Recommendation Engine. Após o login bem-sucedido, o vSAN gerará um grupo de linhas de base de atualizações recomendadas para cada cluster vSAN. As linhas de base do sistema vSAN são listadas na área de janela Linhas de base da guia Linhas de base e grupos.

### Configurar o VCSA para usar o proxy

1.	Em seu navegador da web do servidor de salto, conecte-se ao VCSA Management Interface ` https://<vCenter ip>: 5480 `
2.	Usando as credenciais do Console do IC4VS, efetue login no VCSA Management Interface como raiz.
3.	No vCenter Server Appliance Management Interface, clique em **Rede** e clique em **Gerenciar**.
4.	Para configurar um servidor proxy, na área de janela Configurações de proxy, clique em **Editar**.
5.	Selecione **Usar um servidor proxy**, insira as configurações do servidor proxy e clique em **OK**.

Observe que houve relatórios em que parece que as informações de proxy estão configuradas somente para HTTP, mas não para HTTPS. Para configurar as informações de proxy também para o tráfego HTTPS, ele deve ser ativado primeiro. Depois de efetuar login no VCSA via SSH, use o comando proxy.get para visualizar a configuração e confirme que os parâmetros HTTPS não estão configurados.

Se os parâmetros HTTPS não estiverem configurados, use o comando a seguir:
   `proxy.set --protocol https --server ``<proxy ip>` `  -- port 3128 `

### Configure o vSAN para usar o proxy
1. Navegue para **Página inicial** > **Hosts e clusters**, selecione o **Cluster vSAN** na área de janela de Navegação e, em seguida, selecione a **guia Configurar** e navegue para **vSAN** e, em seguida, **Geral**. Role para a seção **Conectividade de Internet** e clique em **Editar**.
2. Insira o endereço IP e o número da porta do proxy, clique em **OK**.

### Ativar o Customer Experience Improvement Program (CEIP)

Esta é uma etapa opcional. Usando o vSphere Web Client, navegue para **Página inicial** > **Administração** > **Customer Experience Improvement Program** e, em seguida, clique em **Associar**.

### Executar um upload de teste e validar se o upload funcionou
1. Usando o vSphere Web Client, navegue para **Página inicial** > **Hosts e clusters**. Selecione o cluster necessário e, em seguida, selecione a **guia Monitorar** e a página **vSAN**, em seguida, clique em **Funcionamento**. Clique em  ** Ativar funcionamento on-line **.
2. Clique no botão **Retestagem** e aguarde até que o processo seja concluído.
3. Uma nova verificação aparece no Funcionamento chamado _"Conectividade de funcionamento on-line"_ e o botão Ativar funcionamento on-line muda para Retestagem com funcionamento on-line.
4. Clique no botão **Retestagem com funcionamento on-line** para acionar o primeiro upload e aguarde a conclusão do processo, revisando o status na área de janela Tarefas recentes. O Nome do teste deve mudar para o Funcionamento on-line (última verificação: apenas agora).
5. Quando concluído, na janela Funcionamento, role para vSAN Build Recommendation e expanda-o e clique em **vSAN Build Recommendation Engine Health**.
6. Clique em **Efetuar login em my.vmware.com** e insira suas credenciais. Quando o processo for concluído, o **Resultado do teste** mudará para um estado **Aprovado**.
7. Pressione a **guia Update Manager** e agora você deverá ver que o Cluster vSAN está incluído nas Linhas de base.

## Pré-requisitos

Antes de iniciar o processo de upgrade do vSAN, assegure-se de que os requisitos a seguir sejam atendidos:
* Revise os artigos de base de Conhecimento do VMware e revise quaisquer problemas de compatibilidade conhecidos entre sua versão atual do vSAN e a versão de destino do vSAN desejada
* ** O ambiente do vSphere está atualizado **:
  - O VCSA deve estar em um nível de correção igual ou maior do que os hosts vSphere ESXi. Atualize o VCSA se necessário
  - Todos os hosts devem estar executando a mesma construção de ESXi. Se as versões do host vSphere ESXi não forem correspondidas, atualize
* ** Todos os discos vSAN devem estar saudáveis **:
  - Nenhum disco deve estar com falha ou ausente. Isso pode ser determinado por meio da visualização **Gerenciamento de disco vSAN** no vSphere Web Client. **Página inicial** > **Hosts e clusters **, em seguida, selecione o **Cluster vSAN** e clique na **guia vSAN** e, em seguida, em **Discos físicos**. Role por todos os discos e revise o Status de funcionamento do vSAN.
  - Não deve haver objetos de vSAN inacessíveis. Isso pode ser verificado com o **Serviço de funcionamento do vSAN** clicando em **Página inicial** > **Hosts e clusters** e, em seguida, selecione o **Cluster vSAN**. Clique em **guia Monitorar**, **vSAN** e, em seguida, clique em **Funcionamento**. Revise os Resultados do Teste.
  - Não deve haver nenhuma ressincronização ativa no início do processo de upgrade. Isso pode ser verificado clicando em **Página inicial** > **Hosts e clusters**, em seguida, selecione o **Cluster vSAN** e clique na **guia vSAN** e, em seguida, clique em **Ressincronizar componentes**. _A contagem de componentes de Ressincronização deve ser 0_. Observe que alguma atividade de ressincronização é esperada durante o processo de upgrade, uma vez que os dados precisam ser sincronizados após as reinicializações do host.
* **Preparação do host vSphere ESXi** - ao mover um host para o modo de manutenção em um cluster vSAN, você tem três opções para escolher:
  - **Sem migração de dados** - se você selecionar essa opção, o vSAN não evacuará nenhum dado desse host. Se você desligar ou remover o host do cluster, algumas máquinas virtuais poderão se tornar inacessíveis.
  - **Assegurar disponibilidade** - se você selecionar essa opção, o vSAN permitirá mover o host para o modo de manutenção mais rápido do que a migração de dados integral e permitirá o acesso às máquinas virtuais no ambiente.
  - ** Migração de dados completa **
* **Sair do modo de manutenção e ressincronizar** - quando o host vSphere ESXi for submetido a upgrade e movido para fora do modo de manutenção, uma ressincronização ocorrerá. É possível ver isso por meio do Web client. Assegure-se de que isso esteja completo antes de se mover para o próximo host. Uma ressincronização está ocorrendo porque o host que foi atualizado pode agora contribuir para o armazenamento de dados vSAN novamente. É vital esperar até que essa ressincronização seja concluída para assegurar que não haja perda de dados.
* ** Após iniciar um upgrade do cluster vSAN **:
  - Não tente fazer upgrade de um cluster introduzindo novas versões para o cluster e migrando cargas de trabalho.
  - Se estiver introduzindo novos hosts, assegure-se de que eles sejam da mesma versão inicial e faça upgrade deles juntamente com o resto do cluster.
  - Se você estiver incluindo ou substituindo discos durante um upgrade, assegure-se de que eles sejam formatados com a versão apropriada do formato no disco anterior, se aplicável.
  - Portanto, certas mudanças de comportamento do vSAN são controladas pelo formato no disco, então é importante que as versões do formato no disco mais recentes não sejam introduzidas em um cluster de versão mista.

## Fazer upgrade do vCenter Server Appliance

Para obter mais informações, consulte [Atualização do VCSA e vCenters vinculados por SSO](vum-updating-vcsa.html).

##	Fazer upgrade dos hosts do vSphere ESXi

Para obter mais informações, veja [Criando linhas de base e conectando a objetos de inventário](vum-baselines.html).

##	Fazer upgrade do formato de disco vSAN

O Ruby vSphere Console (RVC) é uma interface da linha de comandos baseada no Ruby para vSphere e pode ser usada para gerenciar o VMware vSphere ESXi e o vCenter. O inventário do vSphere é apresentado em uma estrutura em árvore, permitindo que você navegue e execute comandos com relação a objetos do vCenter.

Muitas tarefas administrativas básicas podem ser feitas muito mais eficientemente do que clicar por meio do vSphere Client. O RVC é totalmente implementado no VCSA e é acusado por uma conexão SSH com o dispositivo.
1. Use SSH para o VCSA e efetue login usando a raiz e a senha que são fornecidas no Console do ICVS.
2. No prompt, digite:
  `rvc Administrator@vsphere.local@localhost` e pressione **Enter**.
3. Insira a senha do Administrador fornecida no Console do ICVS. Agora você estará na raiz do sistema de arquivo virtual, digite ls e, em seguida, pressione **Enter**. Você deverá ver:
  `0 /
  1 localhost/``

5. Digite `cd 1`, pressione Enter e, em seguida, `ls` e pressione **Enter**. Você deverá ver:
  `0 / datacenter1 (datacenter)`

6. Digite `cd 0`, pressione Enter e, em seguida, `ls` e pressione **Enter**. Você deve ver:

  `0 storage/
  1 computers [host]/
  2 networks [network]/
  3 datastores [datastore]/
  4 vms [vm]/`

7. Digite `cd 1`, pressione **Enter** e, em seguida, `ls` e pressione **Enter**. Você deverá ver seu cluster:
   `0 cluster1 (cluster)``

8. Agora, vamos usar os comandos de VSAN com relação a esse cluster. Para verificar o status do disco, digite `vsan.disks_stats 0` e pressione **Enter**.

9. Certifique-se de que o Status de funcionamento para todos os discos seja OK. E, em seguida, inicie o upgrade digitando `vsan.ondisk_upgrade 0` e, em seguida, pressionando **Enter**.

10. Dependendo do tamanho de vSAN, essa tarefa pode levar muito tempo. Quando concluído, digite `vsan.objstatusreport 0` e, em seguida, pressione **Enter** para verificar se as versões do objeto são submetidas a upgrade para o novo formato no disco.

11. O upgrade do cluster VSAN agora está concluído. Digite `exit` e pressione **Enter** para sair do RVC.

### Links relacionados

* [VMware HCX on IBM Cloud Solution Architecture](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [Soluções VMware no IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware) (Demos)
