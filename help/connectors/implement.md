---
title: Implementazione di un connettore AEM
description: Implementazione di un connettore AEM
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 9%

---


Implementazione di un connettore AEM
=============================

Di seguito sono riportati alcuni riferimenti utili per la creazione di [connettori AEM](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html), che devono essere letti insieme alle indicazioni relative all’[invio](submit.md) e alla [manutenzione](maintain.md) dei connettori.

Notare che è possibile ottenere una licenza Developer per AEM tramite il programma [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Modelli di integrazione comuni
---------------------------

AEM è una soluzione all&#39;avanguardia per la gestione dell&#39;esperienza Web e offre numerose aree potenziali di integrazioni. I pattern di integrazione comuni includono:

* Estrazione di dati da un sistema esterno in AEM. Ad esempio, l&#39;esportazione delle informazioni di contatto da un CRM per renderle disponibili a un pubblico più ampio che visita un sito Web AEM.  Le implementazioni devono utilizzare i processi [](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)pianificati di Sling, che garantiscono l&#39;esecuzione del processo anche se i contenitori si disattivano. Il codice deve essere progettato in modo da presupporre che il processo possa essere attivato più di una volta.
* Esportazione di dati da AEM a un sistema esterno. Ad esempio, le impostazioni di iscrizione alla newsletter inviate a un CRM su un sito Web AEM.
* Recupero delle risorse da AEM. Ad esempio, un CMS (Content Management System) esterno che fa riferimento a una risorsa memorizzata in  AEM Assets. Oppure, come altro esempio, un sistema PIM che collega un&#39;immagine in  AEM Assets.
* Memorizzazione delle risorse nell&#39;infrastruttura AEM. Ad esempio, un sistema Marketing Resource Management (MRM) che memorizza una risorsa approvata in  AEM Assets.
* Configurazione e rendering di un componente dell’interfaccia utente personalizzata. Ad esempio, potete consentire a un autore di trascinare e rilasciare un componente video e configurare un video specifico da riprodurre sul sito dal vivo.
* Funzionamento su una risorsa con un servizio partner. Ad esempio, l’invio di una risorsa a una piattaforma video quando viene pubblicata una pagina.
* Analisi di un sito, una pagina o una risorsa nella console di amministrazione AEM. Ad esempio, la creazione di raccomandazioni SEO per una pagina esistente o non pubblicata.
* Accesso a livello di pagina ai dati utente gestito da un servizio esterno. Ad esempio, potete sfruttare le informazioni demografiche per personalizzare l&#39;esperienza del sito. Leggi ContextHub, un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali.
* Traduzione dei metadati di una copia del sito o di una risorsa. Vedere il connettore [Bootstrap](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) AEM Framework di traduzione per il codice di esempio utilizzando AEM Translation Framework, che è l&#39;implementazione preferita dei connettori di traduzione.


Documentazione utile
--------------------

 Experience Manager come [documentazione](../overview/introduction.md) Cloud Service fornisce informazioni utili sullo sviluppo in AEM. Di seguito sono riportati alcuni argomenti tecnici e riferimenti specifici che possono essere utili durante l&#39;implementazione di un connettore AEM:

*  Adobe Consulting Services (ACS) [AEM Esempi](http://adobe-consulting-services.github.io/acs-aem-samples/) per codice ben commentato per aiutare AEM sviluppatori
* I vari collegamenti della documentazione nella sezione Modelli comuni di integrazione di questo articolo

Risorse della community
--------------------

Oltre alla documentazione statica di cui sopra,  Adobe e la comunità AEM offrono risorse per aiutare a immettere sul mercato un connettore:

* Il forum [](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) AEM della comunità di Adobi  è un sito attivo in cui i colleghi fanno e rispondono alle domande
* A determinati livelli di partner sono disponibili ulteriori risorse tecniche  Adobe. Scopri di più sul [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Se la tua azienda desidera ricevere assistenza nell’implementazione, può consultare il team [Servizi professionali](http://www.adobe.com/it/experience-cloud/consulting-services.html) di Adobe o consultare [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) per ottenere un elenco dei partner Adobe presenti in tutto il mondo

Regole di struttura del pacchetto
-----------------------

Per supportare distribuzioni continue, AEM come pacchetti di Cloud Service, di cui i connettori sono esempi, esiste una netta separazione tra contenuti &quot;immutabili&quot; e contenuti &quot;mutabili&quot;. I pacchetti devono essere separati in modo pulito tra quelli che includono:

* `/apps`
* `/content` e `/conf`

I connettori devono attenersi alle presenti linee guida sugli imballaggi, descritte in [questo articolo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Anche i connettori esistenti devono essere adattati.

Inoltre, solo  Adobe dovrebbe scrivere il codice in `/libs`, con clienti e partner che scrivono in `/apps`.

I connettori esistenti potrebbero inoltre dover essere reinseriti per spostare qualsiasi configurazione eventualmente inserita `/etc` in altre cartelle di livello superiore, ad esempio `/conf`. Questo è descritto nella [AEM documentazione](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html).

Si consiglia di inserire la maggior parte del codice di connessione `/apps/connectors/<vendor>` per promuovere una struttura di repository pulita per i clienti che dispongono di diversi connettori.

Configurazioni servizi cloud
-----------------------------

Un aspetto dell&#39;implementazione del connettore è il codice che supporta la configurazione del connettore. Questo codice causa la visualizzazione di una scheda con il nome del connettore in Strumenti > Operazioni > Cloud Services. Quando un utente fa clic su di esso, viene visualizzato un browser [di](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) configurazione in cui il cliente seleziona la cartella padre per la configurazione del connettore. Il codice del connettore deve generare un modulo con tutte le proprietà che devono essere configurate, memorizzando i valori in una cartella di configurazione in `/conf`. Questa cartella può essere selezionata in un secondo momento nella scheda Proprietà siti o nella scheda Proprietà risorse.


Configurazioni basate sul contesto
-----------------------------

[Configurazioni](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) in base al contesto consente di effettuare la configurazione dei livelli tra diverse cartelle, incluse `/libs`, `/apps``/conf` e sottocartelle in `/conf`. Supporta l&#39;ereditarietà, in modo che un cliente possa configurare la configurazione globale mentre apporta modifiche specifiche per ogni microsito. Poiché è possibile sfruttare questa funzione per Configurazioni di Cloud Services, il codice del connettore dovrebbe fare riferimento alla configurazione utilizzando l&#39;API di configurazione in base al contesto invece di fare riferimento a un nodo di configurazione specifico.

Se le configurazioni modificate vengono utilizzate nel connettore, architettare il connettore per gestire, inclusi/uniti eventuali aggiornamenti futuri alle configurazioni predefinite fornite dal connettore con qualsiasi configurazione cliente. Ricorda che la modifica del contenuto o della configurazione personalizzati (come modificato dal cliente) senza preavviso e consenso da parte del cliente potrebbe interrompere (o creare un comportamento imprevisto) con il connettore.

Tecniche consigliate per la codifica
----------------------

Poiché AEM come Cloud Service è una soluzione nativa di Cloud, esistono alcune linee guida che possono influenzare le strategie di codice di un connettore. Per ulteriori informazioni, vedere [AEM come guida](/help/implementing/developing/introduction/development-guidelines.md) allo sviluppo Cloud Service.

Verifica del connettore AEM
-------------------------

È necessario creare nuovi connettori (o modificare i connettori esistenti) utilizzando tecniche di sviluppo dell&#39;ambiente locale. Il Partner Team fornirà ai partner ISV un ambiente sandbox in cui possono implementare il proprio connettore AEM in un&#39;applicazione vaniglia per assicurarsi che funzioni.
