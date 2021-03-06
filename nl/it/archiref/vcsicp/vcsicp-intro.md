---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-25"

---

# Introduzione a vCenter Server e IBM Cloud Private

Questo documento fornisce una panoramica del percorso di modernizzazione dell'applicazione a IBM Cloud, concentrandosi sui componenti di gestione cloud per consentire un multicloud integrato da utilizzare per la modernizzazione dell'applicazione:

- **VMware vCenter Server on IBM Cloud** - VCS è un'offerta da IBM Cloud for VMware Solutions ed è una piattaforma basata su VMware di cui viene automaticamente eseguito il provisioning su IBM Cloud.

- **IBM Cloud Private** - ICP è una piattaforma dell'applicazione per lo sviluppo e la gestione di applicazioni inserite nel contenitore, progettate per essere distribuite su piattaforme dell'infrastruttura virtualizzate, come ad esempio VMware.

- **IBM Kubernetes Services** - IKS è un servizio gestito su IBM Cloud che utilizza Kubernetes come motore di orchestrazione per l'automazione della distribuzione, del ridimensionamento e delle operazioni dei contenitori dell'applicazione in un solo cluster tenant.

- **IBM Multi-Cluster Manager** – MCM fornisce la visibilità utente, la gestione incentrata sull'applicazione (politica, distribuzioni, integrità, operazioni) e conformità basata sulle politiche tra i cloud e i cluster. Con MCM, hai il controllo dei tuoi cluster Kubernetes.

- **IBM Cloud Automation Manager** – CAM è una piattaforma di gestione self-service a più cloud in esecuzione su ICP che consente agli sviluppatori e agli amministratori di soddisfare le richieste di business.

## Modernizzazione dell'applicazione su IBM Cloud
La modernizzazione dell'applicazione è un termine che descrive il processo di transizione delle applicazioni esistenti per utilizzare nuovi approcci sul cloud. I clienti oggi cercano approcci innovativi ed efficienti che li aiutino a fare questa transizione in base alla complessità aziendale e dell'applicazione.

Le pressioni economiche richiedono un tempo più veloce per il mercato. Il tuo patrimonio esistente include non solo le applicazioni, ma i dati, i processi, la logica aziendale e le interfacce utente, che devono tutti adattarsi per tenere il passo con le nuove esigenze aziendali.

I vantaggi della modernizzazione dell'applicazione includono quanto segue:
- Migliore produttività degli sviluppatori.
- Aumento dell'efficienza operativa.
- Costi ridotti per la creazione di nuove funzionalità.
- Capacità espansa consegnata in breve tempo.

IBM comprende che il 70% delle adozioni cloud private è guidato dalla necessità di modernizzare gli ambienti dell'applicazione, tuttavia, la maggior parte delle organizzazioni si sta avvicinando all'ammodernamento dell'applicazione con un approccio a stadi, che necessita di uno scenario ibrido e multicloud, dove:
- Applicazioni legacy complesse e monolitiche che in genere vengono eseguite su mainframe o sistemi UNIX restino locali.
- Gli ambienti x86 utilizzati per i systems of record (SoR) o le applicazioni che sono carichi di lavoro sensibili o regolamentati siano ubicati su un'infrastruttura virtualizzata o su un cloud privato.
- Applicazioni come SAP o risorse bare metal di calcolo che utilizzano elevate prestazioni.
- Alcuni carichi di lavoro regolamentati e importanti per la sicurezza, che possono essere spostati nel cloud pubblico si stanno spostando negli ambienti dedicati.
- Systems of engagement (SoE) come; web, mobile, IoT, AI o Video si stanno spostando nei cloud pubblici.

Ad esempio, un modello comune è di disporre di applicazioni SOE di frontend distribuite come contenitori con database e middleware hardware distribuiti su VM su un cloud privato.

Poiché le tue infrastrutture IT e le esigenze aziendali sono uniche, hai bisogno di un approccio alla modernizzazione che aiuti ad accelerare la distribuzione del valore commerciale, che riduca i tuoi rischi e preservi i tuoi investimenti esistenti. IBM fornisce solo un approccio di questo tipo che può essere personalizzato per affrontare le tue esigenze di tecnologia e di business univoche correlate alla modernizzazione dell'applicazione.

Questo documento è uno dei cinque documenti che fornisce diverse panoramiche sulle tecnologie utilizzate nel percorso di modernizzazione dell'applicazione a IBM Cloud:

Guida all'architettura di riferimento, VCS – ICP e CAM - la sezione corrente.

Un'architettura di riferimento per la distribuzione delle seguenti piattaforme:
  - **VMware vCenter Server on IBM Cloud** - un'offerta da IBM Cloud for VMware Solutions ed è una piattaforma basata su VMware di cui viene automaticamente eseguito il provisioning su IBM Cloud.
  - **IBM Cloud Private** - una piattaforma dell'applicazione per lo sviluppo e la gestione delle applicazioni inserite nei contenitori. È un ambiente integrato che include l'orchestrazione del contenitore Kubernetes, nonché un repository di immagini privato, una console di gestione, i framework di monitoraggio e un'interfaccia utente grafica che fornisce un'ubicazione centralizzata da cui puoi distribuire, gestire, monitorare e ridimensionare le tue applicazioni. 
  - **IBM Cloud Automation Manager** - una piattaforma di infrastruttura pronta per le imprese come codice (IaC) che fornisce un unico pannello di controllo per eseguire il provisioning dei carichi di lavoro basati su VM insieme a carichi di lavoro basati su Kubernetes semplicemente utilizzando i modelli archiviati e forniti di versione in un repository.

[Guida all'architettura di riferimento, VCS - IKS](../vcsiks/vcsiks-intro.html)

  Un'architettura di riferimento per la distribuzione delle seguenti piattaforme:
  - **VMware vCenter Server on IBM Cloud** - un'offerta da IBM Cloud for VMware Solutions ed è una piattaforma basata su VMware di cui viene automaticamente eseguito il provisioning su IBM Cloud.
  - **IBM Cloud Kubernetes Service** – un servizio gestito su IBM Cloud che utilizza Kubernetes come motore di orchestrazione per l'automazione della distribuzione, del ridimensionamento e delle operazioni dei contenitori dell'applicazione in un solo cluster tenant.

[Guida all'architettura di riferimento, VCS – Rete](../vcsnsxt/vcsnsxt-intro.html)

Questo documento si concentra sulle tecnologie di rete utilizzate all'interno di VCS, ICP e IKS come NSX-V, NSX-T e Calico.

[Guida all'architettura di riferimento, Concept car Watson e Sk8boarding](../vcscar/vcscar-intro.html)

Questo documento utilizza un approccio “concept car” per dimostrare un'interazione tra l'intelligenza artificiale Watson e il machine learning.

Il documento mette in evidenza le seguenti tecnologie:
  - **Pepper** - un'interfaccia che include la capacità di integrare
  l'ambiente cloud ad eseguire le operazioni di ricerca e dell'applicazione.
  - **VMware vCenter Server on IBM Cloud** - utilizzato per ospitare gli elementi dell'applicazione
  come i carichi di lavoro del database.
  - **IBM Cloud Kubernetes Service** - utilizzato per ospitare
  gli elementi inseriti nel contenitore dell'applicazione.
  - **IBM Cloud Private** - utilizzato per fornire l'orchestrazione a livello di piattaforma e servizi, inclusa la capacità di ospitare e ridimensionare l'applicazione nelle piattaforme del contenitore e nella VM. Questo componente può inoltre abilitare i servizi di sviluppo Watson per la piattaforma, consentendo l'accesso alle funzionalità dell'intelligenza artificiale.

[Guida all'architettura di riferimento, VCS – Contenuto](../vcscontent/vcscontent-intro.html)

Questo documento si concentra sui seguenti tipi di contenuti disponibili in IBM Cloud Automation Manager:
- Contenuto del catalogo interno come grafici Helm “predefiniti”, modelli Terraform e ricette Chef.
- Contenuto dei servizi come i servizi Blockchain e Watson.

### Link correlati

  * [VMware vCenter Server on IBM Cloud with Hybridity Bundle](../vcs/vcs-hybridity-intro.html)
