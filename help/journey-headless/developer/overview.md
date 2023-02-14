---
title: AEM Percorso di sviluppatori CMS headless
description: Scopri lo sviluppo headless utilizzando Adobe Experience Manager (AEM) come CMS headless. Scopri come utilizzare funzioni quali Modelli di contenuto, Frammenti di contenuto e un’API GraphQL per fornire contenuti headless.
landing-page-description: Scopri la distribuzione e l’implementazione headless dei contenuti. Ulteriori informazioni sullo sviluppo della strategia all'interno dell'azienda.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 39a8b505ebf323ea18d014d9603356239dc39646
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 16%

---

# AEM Percorso di sviluppatori CMS headless {#aem-headless-developer-journey}

Benvenuto nella documentazione per gli sviluppatori che sono nuovi di Adobe Experience Manager headless CMS!

Scopri le funzioni headless potenti e flessibili, le loro funzionalità e come sfruttarle nel tuo primo progetto di sviluppo headless. Questo percorso fornisce tutte le informazioni necessarie per sviluppare la tua prima applicazione headless.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="Risorse per sviluppatori AEM Headless e documentazione avanzata"
>abstract="Tutto ciò che ti serve per scoprire AEM CMS headless e creare e distribuire applicazioni migliori ed esperienze più veloci."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it" text="Risorse per sviluppatori AEM Headless"

## Introduzione {#introduction}

L’implementazione headless di AEM utilizza modelli di frammenti di contenuto e frammenti di contenuto per concentrarsi sulla creazione di frammenti di contenuto strutturati, neutri rispetto ai canali e riutilizzabili e sulla loro distribuzione cross-channel. A questo scopo, dimentica la gestione delle pagine e dei componenti come avviene nelle soluzioni stack complete. Si tratta di un modello di sviluppo moderno e dinamico per l&#39;implementazione delle esperienze digitali.

Questa guida ti guida attraverso gli argomenti di implementazione headless in AEM, così al termine:

* Comprendi appieno cosa è la distribuzione di contenuti headless e i relativi vantaggi.
* Scopri AEM funzioni headless e come funzionano insieme per offrire un’esperienza headless.
* Avere la possibilità di compiere i primi passi per implementare il primo progetto senza testa AEM.

>[!TIP]
>
> Se preferisci **imparare facendo** e dispongono delle conoscenze già acquisite su AEM, visita le esercitazioni AEM Headless, organizzate per API e framework e disponibili in [Sezione Risorse aggiuntive](#additional-resources) alla fine del presente documento.

## Pubblico {#audience}

Questo percorso è progettato per l’utente tipo sviluppatore, esponendo i requisiti, i passaggi e l’approccio di un progetto AEM Headless dal punto di vista dello sviluppatore. Il percorso definisce gli utenti tipo aggiuntivi con cui lo sviluppatore deve interagire per un progetto di successo, ma il punto di vista del percorso è quello dello sviluppatore.

Di seguito sono riportati gli utenti tipo che interagiscono in questo percorso.

| Persona | Descrizione | Ruolo in questo Percorso |
|---|---|---|
| Sviluppatore (pubblico target) | Ha esperienza nello sviluppo di applicazioni headless che utilizzano contenuti provenienti da diverse fonti | Pubblico di destinazione di questo percorso |
| Autore del contenuto | Crea e gestisce contenuti distribuiti senza problemi | Gli autori dei contenuti creano contenuti che lo sviluppatore offre senza problemi. |
| Administrator | Gestisce l’impostazione e la configurazione di base di AEM | Lo sviluppatore collabora con l’amministratore per apportare le modifiche di configurazione necessarie per lo sviluppo. |
| Architetto dei contenuti | Analizza i requisiti dei dati che devono essere consegnati senza problemi e definisce la struttura di tali dati | Gli sviluppatori lavorano con l’architetto dei contenuti per comprendere la struttura dei dati e i requisiti necessari per distribuirli senza problemi. |

## Percorso di sviluppatori headless {#the-journey}

Ci occuperemo di molti argomenti in questo percorso, che vi fornirà la conoscenza fondamentale di headless in AEM.

Anche se puoi passare direttamente a una particolare parte del percorso, molti concetti sono basati su quelli degli articoli precedenti. È consigliabile iniziare dall’inizio e procedere in sequenza.

| # | Articolo | Descrizione |
|---|---|---|
| 0 | AEM Percorso di sviluppatori headless | Questo documento |
| 1 | [Informazioni sullo sviluppo headless di CMS](learn-about.md) | Scopri la tecnologia headless e quando usarla. |
| 2 | [Guida introduttiva ad AEM Headless as a Cloud Service](getting-started.md) | Scopri AEM prerequisiti headless |
| 3 | [Percorso della tua prima esperienza con AEM Headless](path-to-first-experience.md) | Imposta l’ambiente di sviluppo e scopri come integrare un’app semplice con AEM Headless |
| 4 | [Come modellare il contenuto](model-your-content.md) | Scopri come modellare la struttura del contenuto. |
| 5 | [Come accedere ai contenuti tramite API di consegna AEM](access-your-content.md) | Scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto. |
| 6 | [Come aggiornare i contenuti tramite API di AEM Assets](update-your-content.md) | Scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto. |
| 7 | [Come mettere tutto insieme - la tua app e il tuo contenuto in AEM Headless](put-it-all-together.md) | Scopri come prendere il progetto AEM e prepararlo per diventare live con l’SDK senza titolo AEM. |
| 8 | [Come vivere con la tua applicazione headless](go-live.md) | Scopri come distribuire l’applicazione in tempo reale e prendere il codice locale in Git e spostarlo nella pipeline CI/CD di Cloud Manager Git. |
| 9 | [Facoltativo - Come creare applicazioni a pagina singola (SPA) con AEM](create-spa.md) | Scopri come combinare consegna headful e headless e come creare SPA modificabili utilizzando AEM framework dell’editor SPA. |

{style=&quot;table-layout:auto&quot;}

## Passaggio successivo {#what-is-next}

Per iniziare, controlla il prossimo articolo: [Scopri lo sviluppo headless di CMS.](learn-about.md)

### Scegli la tua avventura {#choose-your-path}

Preferisci imparare con i tuoi tempi? Consulta le seguenti opzioni:

* Se preferisci continuare a **scopri i concetti senza testa e le tecnologie senza testa AEM**, dovresti continuare il tuo percorso AEM headless come consigliato nella prossima revisione del documento [Come modellare il contenuto come modelli di contenuto AEM](model-your-content.md) dove viene illustrato come modellare la struttura del contenuto in AEM.
* Se preferisci **imparare facendo**, puoi passare alla [Guida introduttiva a AEM tutorial pratico headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=it) dove puoi passare direttamente AEM sviluppo Headless implementando un semplice progetto per esporre AEM contenuto headless.

## Risorse aggiuntive {#additional-resources}

I percorsi di documentazione mostrano come AEM risolvere un problema aziendale fornendo una descrizione che ti guidi attraverso i processi e le funzionalità correlati. Un percorso illustra il funzionamento congiunto di più funzioni per soddisfare le esigenze di un&#39;unica azienda.

Consulta questi percorsi aggiuntivi per ulteriori informazioni su come AEM funzioni avanzate funzionano insieme.

* [Esercitazioni AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it) - Se preferisci imparare facendo e avere la conoscenza esistente di AEM, segui i nostri tutorial pratici organizzati da API e framework, che esplorano la creazione e l&#39;utilizzo di applicazioni create su AEM Headless.
* [AEM Percorso di traduzione headless](/help/journey-headless/translation/overview.md) - Questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, di come AEM i contenuti headless e di come tradurli.
* [Percorso di authoring headless](/help/journey-headless/author/overview.md): inizia qui un percorso guidato attraverso le potenti e flessibili funzionalità headless di AEM, le potenzialità e i modi in cui modellare i contenuti sul tuo primo progetto headless.
* [Percorso architetto headless](/help/journey-headless/architect/overview.md): fai clic qui per un’introduzione alle potenti e flessibili funzionalità headless di Adobe Experience Manager as a Cloud Service e per vedere come modellare i contenuti per il tuo progetto.
* [AEM documentazione tecnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) - Se hai già una comprensione ferma delle tecnologie AEM e headless, consulta i nostri documenti tecnici approfonditi.
