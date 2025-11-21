---
title: Implementazione di un connettore AEM
description: Scopri i connettori, cosa possono fare e come implementare questi preziosi strumenti in Experience Manager.
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
feature: Operations
role: Admin
source-git-commit: a9cec66cf518a19a5a6152d431a052369b5b503a
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 71%

---


Implementazione di un connettore AEM
=============================

Di seguito sono riportati alcuni riferimenti utili per la creazione di connettori AEM. Tali riferimenti devono essere letti con istruzioni sull&#39;[invio](submit.md) e sulla [manutenzione](maintain.md) dei connettori.

È possibile ottenere una licenza per sviluppatori per AEM tramite il [programma Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).

Modelli di integrazione comuni
---------------------------

AEM è una soluzione di gestione dell’esperienza web all’avanguardia e offre molte aree potenziali di integrazioni. I modelli di integrazione comuni includono:

* Estrazione di dati da un sistema esterno in AEM. Ad esempio, esportando le informazioni di contatto da un CRM per renderle disponibili a un pubblico più ampio che visita un sito Web basato su AEM.  Le implementazioni devono utilizzare i [Processi pianificati](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs), che garantiscono l’esecuzione del processo anche in caso di esaurimento dei contenitori. Il codice deve essere progettato per presumere che il processo possa essere attivato potenzialmente più di una volta.
* Esportazione di dati da AEM in un sistema esterno. Ad esempio, le impostazioni di abbonamento a una newsletter vengono inviate su un sito web basato su AEM a un CRM.
* Recupero risorse da AEM. Ad esempio, un sistema di gestione dei contenuti esterno (CMS) che fa riferimento a una risorsa memorizzata in AEM Assets. Oppure, come altro esempio, un sistema PIM che si collega a un&#39;immagine in AEM Assets.
* Memorizzazione delle risorse nell’infrastruttura AEM. Ad esempio, un sistema di gestione delle risorse di marketing (MRM) che memorizza una risorsa approvata in AEM Assets.
* Configurazione e rendering di un componente dell’interfaccia utente personalizzato. Ad esempio, puoi consentire all’autore di trascinare e rilasciare un componente video e configurare un video specifico da riprodurre sul sito live.
* Intervento su una risorsa con un servizio partner. Ad esempio, l’invio di una risorsa a una piattaforma video quando viene pubblicata una pagina.
* Analisi di un sito, di una pagina o di una risorsa in AEM Admin Console. Ad esempio, l’elaborazione di consigli SEO per una pagina esistente o non pubblicata.
* Accesso a livello di pagina ai dati utente gestito da un servizio esterno. Ad esempio, utilizza le informazioni demografiche per personalizzare l’esperienza del sito. Scopri ContextHub, un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali.
* Traduzione della copia del sito o dei metadati della risorsa. Consulta la sezione [Connettore Bootstrap di AEM Translation Framework](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) per il codice di esempio che utilizza l&#39;AEM Translation Framework, che è l’implementazione preferita dei connettori di traduzione.


Documentazione utile
--------------------

La [documentazione](../overview/introduction.md) Experience Manager as a Cloud Service fornisce informazioni utili sullo sviluppo in AEM. Di seguito sono riportati alcuni argomenti tecnici e riferimenti specifici che possono essere utili durante l&#39;implementazione di un connettore AEM:

* Servizi di consulenza Adobe (ACS) [esempi AEM](https://adobe-consulting-services.github.io/acs-aem-samples/) per un codice ben commentato per aiutare gli sviluppatori AEM
* I vari collegamenti alla documentazione nella sezione Modelli di integrazione comuni di questo articolo

Risorse della community
--------------------

Oltre alla documentazione statica di cui sopra, Adobe e la comunità AEM offrono risorse per aiutare a immettere un connettore sul mercato:

* La comunità di Adobe [AEM Forum](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) è un sito attivo in cui i tuoi colleghi chiedono e rispondono alle domande
* Ulteriori risorse tecniche Adobe sono disponibili per determinati livelli di partner. Scopri di più su [Adobe Exchange Program](https://partners.adobe.com/technologyprogram/experiencecloud.html).
* Se la tua azienda desidera ricevere assistenza nell’implementazione, può consultare il team [Servizi professionali](https://solutionpartners.adobe.com/s/directory) di Adobe o consultare [Solution Partner Finder](https://solutionpartners.adobe.com/s/directory/) per ottenere un elenco dei partner Adobe presenti in tutto il mondo

Regole della struttura del pacchetto
-----------------------

Per facilitare le distribuzioni continue, i pacchetti AEM as a Cloud Service, come i connettori, mantengono una rigida divisione tra contenuti &quot;immutabili&quot; e contenuti &quot;mutabili&quot;. I pacchetti devono essere organizzati in modo chiaro in modo da includere:

* `/apps`
* `/content` e `/conf`

I connettori devono attenersi alle presenti linee guida per la creazione di pacchetti, descritte in [Struttura di progetto AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Anche i connettori esistenti devono essere riadattati per adeguarsi.

Inoltre, solo Adobe dovrebbe scrivere il codice in `/libs`, con clienti e partner che scrivono in `/apps`.

È inoltre possibile che sia necessario eseguire il refactoring dei connettori esistenti per spostare eventuali configurazioni posizionate una volta `/etc` in altre cartelle di livello superiore, come `/conf`. La ristrutturazione è stata effettuata nell&#39;ambito di AEM 6.5 ed è descritta nella [documentazione di AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/deploying/restructuring/repository-restructuring).

Adobe consiglia di collocare la maggior parte del codice del connettore in `/apps/connectors/<vendor>` per mantenere una struttura dell&#39;archivio pulita, in particolare per i clienti che utilizzano più connettori.

Configurazioni servizi cloud
-----------------------------

Un aspetto dell’implementazione del connettore è il codice che ne supporta la configurazione. Questo codice fa apparire una scheda con il nome del connettore in Strumenti > Operazioni > Servizi cloud. Se cliccato, viene visualizzato un [browser di configurazione](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) in cui il cliente seleziona la cartella genitore per contenere la configurazione del connettore. Il codice del connettore deve tradursi in un modulo con tutte le proprietà che devono essere configurate, in ultima analisi memorizzando i valori in una cartella di configurazione in `/conf`. Questa cartella può essere successivamente selezionata nella scheda Proprietà siti o nella scheda Proprietà risorse.


Configurazioni in base al contesto
-----------------------------

[Configurazioni in base al contesto](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) consente la configurazione dei livelli in diverse cartelle, tra cui `/libs`, `/apps`, `/conf` e sottocartelle in `/conf`. Supporta l’ereditarietà in modo che un cliente possa impostare la configurazione globale mentre apporta modifiche specifiche a ciascun microsito. Poiché è possibile utilizzare questa funzione per le configurazioni dei servizi cloud, il codice del connettore deve fare riferimento alla configurazione utilizzando l’API di configurazione in base al contesto, invece di fare riferimento a un nodo di configurazione specifico.

Se le configurazioni modificate sono usate nel connettore, occorre architettare il connettore in modo da gestire l&#39;inclusione/unione di qualsiasi aggiornamento futuro delle configurazioni predefinite fornite dal connettore con le configurazioni del cliente. Tieni presente che la modifica di contenuti o configurazioni personalizzati dal cliente senza preavviso e consenso può interrompere o causare un comportamento imprevisto nel connettore.

Best practice di codifica
----------------------

Poiché AEM as a Cloud Service è una soluzione nativa per il cloud, esistono alcune linee guida che possono influire sulle strategie di codice di un connettore. Vedi [Linee guida per lo sviluppo in AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md) per ulteriori dettagli.

Verifica del connettore AEM
-------------------------

È necessario creare nuovi connettori (o modificare i connettori esistenti) utilizzando tecniche di sviluppo dell’ambiente locale. Il Partner Team fornisce ai partner ISV un ambiente sandbox in cui possono implementare il connettore AEM in un&#39;applicazione standard per garantire il corretto funzionamento.
