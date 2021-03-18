---
title: Implementazione di un connettore AEM
description: Implementazione di un connettore AEM
translation-type: tm+mt
source-git-commit: b77113ccc55f2063c684d49e2babdd7563b9d6fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


Implementazione di un connettore AEM
=============================

Di seguito sono riportati alcuni riferimenti utili per la creazione di [connettori AEM](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html), che devono essere letti insieme alle indicazioni relative all’[invio](submit.md) e alla [manutenzione](maintain.md) dei connettori.

Si noti che è possibile ottenere una licenza sviluppatore per AEM tramite il [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).

Modelli di integrazione comuni
---------------------------

AEM è una soluzione di gestione dell’esperienza web all’avanguardia e offre molte aree potenziali di integrazioni. I modelli di integrazione comuni includono:

* Estrazione di dati da un sistema esterno in AEM. Ad esempio, esportando le informazioni di contatto da un CRM per renderle disponibili a un pubblico più ampio che visita un sito web basato su AEM.  Le implementazioni devono utilizzare i [Processi pianificati di Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs), che garantiscono l&#39;esecuzione del processo anche se i contenitori scadono. Il codice deve essere progettato per presumere che il processo possa essere attivato potenzialmente più di una volta.
* Esportazione di dati da AEM in un sistema esterno. Ad esempio, le impostazioni di abbonamento a una newsletter sono state inviate su un sito web basato su AEM a un CRM.
* Recupero risorse da AEM. Ad esempio, un sistema di gestione dei contenuti esterno (CMS) che fa riferimento a una risorsa memorizzata in AEM Assets. Oppure, come altro esempio, un sistema PIM che si collega a un&#39;immagine in AEM Assets.
* Memorizzazione delle risorse nell’infrastruttura AEM. Ad esempio, un sistema di gestione delle risorse di marketing (MRM) che memorizza una risorsa approvata in AEM Assets.
* Configurazione e rendering di un componente dell’interfaccia utente personalizzato. Ad esempio, puoi consentire all’autore di trascinare e rilasciare un componente video e configurare un video specifico da riprodurre sul sito live.
* Funzionamento su una risorsa con un servizio partner. Ad esempio, l’invio di una risorsa a una piattaforma video quando viene pubblicata una pagina.
* Analisi di un sito, di una pagina o di una risorsa in AEM Admin Console. Ad esempio, l’elaborazione di consigli SEO per una pagina esistente o non pubblicata.
* Accesso a livello di pagina ai dati utente gestito da un servizio esterno. Ad esempio, sfrutta le informazioni demografiche per personalizzare l’esperienza del sito. Scopri ContextHub, un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali.
* Traduzione della copia del sito o dei metadati della risorsa. Per il codice di esempio che utilizza AEM Translation Framework, che è l&#39;implementazione preferita dei connettori di traduzione, consulta [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) .


Documentazione utile
--------------------

Experience Manager come Cloud Service [documentazione](../overview/introduction.md) fornisce informazioni utili sullo sviluppo in AEM. Di seguito sono riportati alcuni argomenti tecnici e riferimenti specifici che possono essere utili durante l&#39;implementazione di un connettore AEM:

* Adobe Consulting Services (ACS) [AEM Samples](http://adobe-consulting-services.github.io/acs-aem-samples/) per codice ben commentato per aiutare gli sviluppatori AEM
* I vari collegamenti alla documentazione nella sezione Modelli di integrazione comuni di questo articolo

Risorse della community
--------------------

Oltre alla documentazione statica di cui sopra, la comunità degli Adobi e AEM offre risorse per contribuire a immettere sul mercato un connettore:

* Il forum [AEM della community di Adobi](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) è un sito attivo in cui i tuoi colleghi pongono e rispondono alle domande
* A determinati livelli dei partner sono disponibili risorse tecniche Adobi aggiuntive. Ulteriori informazioni sul [programma di scambio di Adobi](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Se la tua azienda desidera ricevere assistenza nell’implementazione, può consultare il team [Servizi professionali](http://www.adobe.com/it/experience-cloud/consulting-services.html) di Adobe o consultare [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) per ottenere un elenco dei partner Adobe presenti in tutto il mondo

Regole della struttura del pacchetto
-----------------------

Al fine di supportare le distribuzioni continue, AEM come pacchetti Cloud Service, di cui sono esempi i connettori, è presente una rigida separazione tra contenuti &quot;immutabili&quot; e contenuti &quot;mutabili&quot;. I pacchetti devono essere separati in modo pulito tra quelli che includono:

* `/apps`
* `/content` e `/conf`

I connettori devono attenersi alle presenti linee guida sugli imballaggi, descritte in [questo articolo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Anche i connettori esistenti devono essere riadattati per adeguarsi.

Inoltre, solo l&#39;Adobe deve scrivere il codice in `/libs`, con clienti e partner che scrivono in `/apps`.

È inoltre possibile che sia necessario eseguire il refactoring dei connettori esistenti per spostare le configurazioni eventualmente inserite `/etc` in altre cartelle di livello superiore, ad esempio `/conf`. Questa ristrutturazione è stata effettuata nell&#39;ambito della AEM 6.5 ed è descritta nella [AEM documentazione 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

Si consiglia di posizionare la maggior parte del codice del connettore in `/apps/connectors/<vendor>` per promuovere una struttura dell’archivio pulita per i clienti che dispongono di diversi connettori.

Configurazioni servizi cloud
-----------------------------

Un aspetto dell’implementazione del connettore è il codice che supporta la configurazione del connettore. Questo codice fa apparire una scheda con il nome del connettore in Strumenti > Operazioni > Cloud Services. Quando fai clic su , viene visualizzato un [browser di configurazione](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) in cui il cliente seleziona la cartella principale per contenere la configurazione del connettore. Il codice del connettore deve tradursi in un modulo con tutte le proprietà che devono essere configurate, in ultima analisi memorizzando i valori in una cartella di configurazione in `/conf`. Questa cartella può essere successivamente selezionata nella scheda Proprietà siti o nella scheda Proprietà risorse .


Configurazioni in base al contesto
-----------------------------

[Le ](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) configurazioni in base al contesto consentono di configurare i livelli in diverse cartelle, incluse  `/libs`,  `/apps`  `/conf` e sottocartelle in  `/conf`. Supporta l’ereditarietà in modo che un cliente possa configurare la configurazione globale mentre apporta modifiche specifiche a ciascun microsito. Poiché è possibile sfruttare questa funzione per le configurazioni dei Cloud Services, il codice del connettore dovrebbe fare riferimento alla configurazione utilizzando l’API di configurazione in base al contesto, invece di fare riferimento a un nodo di configurazione specifico.

Se nel connettore vengono utilizzate configurazioni modificate, architettare il connettore per gestire, inclusi/raggruppando eventuali aggiornamenti futuri alle configurazioni predefinite fornite dal connettore con eventuali configurazioni del cliente. Ricorda che la modifica del contenuto o della configurazione personalizzati (come modificata dal cliente) senza l’avviso e il consenso del cliente può interrompere (o creare un comportamento imprevisto) con il connettore.

Best practice di codifica
----------------------

Poiché AEM come Cloud Service è una soluzione nativa per il cloud, esistono alcune linee guida che possono influenzare le strategie di codice di un connettore. Per ulteriori informazioni, consulta [AEM come guida allo sviluppo di un Cloud Service](/help/implementing/developing/introduction/development-guidelines.md) .

Verifica del connettore AEM
-------------------------

È necessario creare nuovi connettori (o modificare i connettori esistenti) utilizzando tecniche di sviluppo dell’ambiente locale. Il Partner Team fornirà ai partner ISV un ambiente sandbox in cui possono implementare il Connettore AEM in un&#39;applicazione vaniglia per garantire che funzioni.
