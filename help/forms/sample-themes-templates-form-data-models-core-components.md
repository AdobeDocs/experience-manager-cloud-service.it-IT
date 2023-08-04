---
title: Temi di esempio, modelli e modelli di dati dei moduli nei componenti core
description: I componenti core di AEM Forms forniscono esempi di temi, modelli e modelli di dati per moduli adattivi
solution: Experience Manager Forms
topic: Administration
role: Admin, User
hide: true
hidefromtoc: true
level: Intermediate
source-git-commit: 2b290be134be05bc15891082e8b54efef62076d0
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 3%

---


# Temi di esempio, modelli e modelli di dati dei moduli nei componenti core {#sample-themes-templates-and-data-models}

[!DNL AEM Forms] I Componenti core forniscono temi di esempio, modelli e modelli di dati per moduli pronti all’uso per creare moduli adattivi versatili in modo rapido. Questi consentono inoltre agli autori dei moduli di apprendere l’estensibilità, l’adattabilità e la reattività di [Componenti core di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per creare moduli semplici in poco tempo e moduli complessi in modo semplice e senza interruzioni, collegandosi al database.

I temi di esempio, i modelli e i modelli di dati dei moduli inclusi nel pacchetto di contenuto di riferimento sono:

| Modelli | Temi | Modelli dati modulo |
---------|----------|---------
| Base | Area di lavoro | Microsoft® Dynamics 365 |
| Vuoto | WKND | Salesforce |
| Contattaci | Semaforo |  |
| Aggiornamento dei dettagli di contatto |   |   |
| Modulo di consenso | |  |
| Richiesta servizio di registro |  |  |
| Invia feedback |  |  |
| Iscrizione benefit |  |   |
| Sintetico benefit dipendenti |   |   |
| Richiesta di estratto conto |   |   |
| Modulo di ispezione di sicurezza |   |   |
| Ispezione del controllo di qualità |   |   |
| Richiesta di acquisto |  |  |

## Temi di esempio {#Sample-Themes}

I temi di esempio di riferimento aiutano gli autori a definire e personalizzare lo stile dei moduli; gli autori con conoscenze di base su CSS possono personalizzare il tema in base alle esigenze.

**Come ottenere questi temi?**
* Per attivare questi temi **Forms as a Cloud Service** ambiente, [abilitare i componenti core Adaptive Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html) e utilizza [pipeline front-end](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) per distribuire questi temi.
* Per inserire questi temi in una **AEM 6.5 Forms** ambiente, [abilitare i componenti core Adaptive Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) e utilizza [gestione pacchetti](https://experienceleague.corp.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components) per distribuire questi temi.

Il **pronto all’uso** [Componenti core modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) I temi sono descritti come segue:

![Temi inclusi](assets/OOTB-themes.png)

### Area di lavoro {#Canvas}

Il tema Area di lavoro è il tema predefinito per le maschere e sottolinea l&#39;utilizzo di colori di base, trasparenza e icone piatte. Nella schermata seguente puoi vedere come si presenta il tema Canvas.

![Tema area di lavoro](assets/Safety-Inspection-Theme-Canvas.png)

### WKND {#WKND}

Il tema WKND incarna un design vivace, fantasioso e coinvolgente per mostrare un aspetto elegante alle tue forme. Il tema è basato sull&#39;aspetto e lo stile di [Sito WKND](https://wknd.site/us/en.html) che è un sito web di viaggi e avventura basato su [Componenti core di Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it).

![Tema WKND](assets/Safety-Inspection-Form-Theme.png)


### Semaforo {#Easel}

Il tema semplice consente di creare un aspetto del modulo accattivante e facile da impostare, personalizzato per la semplicità e la facilità d’uso. Il tema di Easel è basato sul concetto di un supporto portatile utilizzato dagli artisti per sostenere una tela mentre lavorano sui loro dipinti.

![Tema Easy](assets/Safety-Inspection-Theme-Easel.png)

## Modelli di esempio {#Sample-templates}

I modelli definiscono la struttura iniziale del modulo, il contenuto e le azioni da replicare nel modulo oppure utilizzano una struttura di modelli simile al modulo, ad esempio Modulo di consenso, Modulo di iscrizione benefit e molto altro ancora.

**Come si ottengono questi modelli?**
Per ottenere i modelli, distribuisci un [Progetto basato su Archetipo AEM 43 o versione successiva](https://github.com/adobe/aem-project-archetype) al tuo **AEM Forms as a Cloud Service** o **AEM 6.5** ambiente Forms.

Il **pronto all’uso** [Componenti core modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) I modelli sono descritti come segue:

![Modelli di riferimento](assets/reference-templates-core-components.png)

### Base {#Basic}

Il modello di base consente di creare rapidamente un modulo per l’esperienza di iscrizione. Puoi utilizzarlo anche per visualizzare in anteprima la funzionalità di [Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction). Fornisce un layout guidato per la presentazione sezione per sezione dei dati.

![Modello di base](assets/Basic-template-desktop-view.png)

### Vuoto {#Blank}

Un modello di area di lavoro vuoto consente di creare da zero una struttura di moduli adattivi, un contenuto e regole. Nessun componente modulo viene pre-incorporato nel modello vuoto.

![Modello vuoto](assets/Blank-temp-desktop-view.png)

### Contattaci {#Contact-Us}

Il modello di modulo Contattaci viene utilizzato per creare un modulo per facilitare la comunicazione tra i visitatori del sito Web e gli amministratori dei moduli. Gli utenti possono inviare query, feedback o richieste di supporto tramite il modulo.

![Modello per contattarci](assets/Contact-us-desktop-view.png)

### Aggiornamento dei dettagli di contatto {#Contact-Details-Update}

Il modello di aggiornamento dei dettagli di contatto consente agli autori di creare un modulo per l’aggiornamento dell’indirizzo e dei dettagli di contatto dei clienti. Il modulo aiuta inoltre i clienti ad aggiornare le informazioni personali relative all’abbonamento o ai vantaggi per garantire una comunicazione fluida e un accesso ininterrotto ai servizi o ai vantaggi.

![Contact-details-update](assets/Contact-details-update.png)

### Modulo di consenso {#Consent-Form}

Il modello di modulo di consenso viene utilizzato per creare un modulo per l’acquisizione di un documento legale da parte di partecipanti che partecipano a un’attività specifica, a uno studio di ricerca, a una procedura medica o a qualsiasi situazione in cui possano essere coinvolti dati o diritti personali. Il modulo garantisce la trasparenza, tutela i diritti dei partecipanti e stabilisce una chiara comprensione di ciò che l&#39;individuo sta accettando.

![Modulo di consenso](assets/Consent-form-desktop-view.png)

### Registra richiesta servizio {#Log-Service-Request}

Il modello di richiesta del servizio di registro consente di creare un modulo che richiede a un provider di servizi servizi servizi di registrazione specifici del registro. Il modulo funge da richiesta formale per creare un ticket per eventi, attività o dati registrati per il monitoraggio o il tracciamento dello stato.

![Modello di richiesta servizio di registro](assets/Log-service-request-desktop-view.png)


### Invia feedback {#Give-Feedback}

Fornire un modello di modulo di feedback consente di creare un modulo per fornire un feedback costruttivo a un&#39;altra persona o team. Il modulo contribuisce a garantire un feedback chiaro, specifico e actionable, promuovendo una comunicazione aperta e miglioramenti.

![Dai un modello di feedback](assets/Give-feedback-desktop-view.png)


### Iscrizione benefit {#Benefits-Enrollment}

Il modello di modulo di iscrizione ai benefit viene utilizzato per creare un modulo per raccogliere informazioni essenziali dai dipendenti in merito ai benefit e alle opzioni di copertura preferiti. In genere accompagna il periodo di iscrizione ai benefit annuali.

![Modello iscrizione benefit](assets/Benefits-enrollment-form-template.png)


### Sintetico benefit dipendenti {#Employee-Benefits-Summary}

Il modello di modulo Riepilogo benefit dipendente consente di creare un modulo per raccogliere dettagli essenziali sui vantaggi di un singolo utente. Consente di valutare la copertura in modo rapido e accurato, fornendo una panoramica completa per assistenza e supporto efficienti.
![Sintetico benefit dipendenti](assets/Employee-benefits-summary.png)


### Richiesta estratto conto {#Request-for-Account-Statement}

Il modello di estratto conto della richiesta consente di creare un modulo che avvia il processo di ottenimento di un estratto conto accurato e aggiornato dei clienti. Il rendiconto fornisce una registrazione dettagliata di transazioni finanziarie, attività o altre informazioni rilevanti sui clienti che utilizzano questo modulo.

![Request-for-account-statment](assets/Request-for-account-statment.png)

### Ispezione di sicurezza {#Safety-Inspection}

Il modello di modulo per le ispezioni di sicurezza consente di creare un modulo per l&#39;immissione di dettagli per un ambiente di lavoro sicuro. Effettuando ispezioni regolari utilizzando questo modulo è possibile identificare potenziali rischi. Il modulo copre vari aspetti come le uscite di emergenza, la sicurezza antincendio, la sicurezza elettrica, i materiali pericolosi, i dispositivi di protezione personale, l&#39;ergonomia delle postazioni di lavoro per la sicurezza e il benessere di dipendenti, visitatori e clienti.

![Modulo di ispezione di sicurezza](assets/Safety-inspection-form.png)

### Ispezione del controllo qualità {#Quality-Control-Inspection}

Il modello di modulo per l&#39;ispezione del controllo qualità consente di creare un modulo per valutare e documentare l&#39;aspetto visivo, le dimensioni, la funzionalità, la documentazione, i risultati dei test e la qualità complessiva di un prodotto o di un elemento. Consente di identificare i difetti, le non conformità e le azioni correttive necessarie per garantire il rispetto degli standard di qualità.

![Ispezione del controllo qualità](assets/Quality-Control-Inspection.png)


### Richiesta di acquisto {#Purchase-Request}

Il modello di modulo per la richiesta di acquisto consente di creare un modulo per avviare il processo di approvvigionamento e consentire ai dipendenti di richiedere formalmente l&#39;acquisto di beni o servizi necessari per il proprio lavoro. Il modulo acquisisce dettagli essenziali come la descrizione dell&#39;articolo, la quantità, il fornitore preferito (se applicabile), l&#39;allocazione del budget, la giustificazione per l&#39;acquisto, le informazioni di consegna e le approvazioni richieste.

![purchase-request-form](assets/Purchase-request-form.png)

## Modelli dati modulo di riferimento {#reference-models}

Dopo aver creato un’ [Modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#adaptive-forms-core-components) in base a [Componente core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction#adaptive-forms-core-components), è possibile connettere il modulo con i server di database Microsoft® Dynamics 365 e Salesforce per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivi dati in Microsoft® Dynamics 365 e Salesforce all’invio di moduli adattivi.
* Scrivi dati in Microsoft® Dynamics 365 e Salesforce tramite entità personalizzate definite in Modello dati modulo e viceversa.
* Effettua query sui server Microsoft® Dynamics 365 e Salesforce per i dati e precompila Forms adattivo.
* Leggi i dati da Microsoft® Dynamics 365 e dal server Salesforce.

È possibile ottenere i seguenti modelli di dati del modulo installando [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

Per informazioni sull’utilizzo di questi modelli, consulta [Configurazione di Microsoft® Dynamics 365 e dei servizi cloud Salesforce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html#configure-dynamics-cloud-service)
