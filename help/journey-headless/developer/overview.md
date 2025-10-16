---
title: Percorso per sviluppatori CMS headless di AEM
description: Scopri lo sviluppo headless utilizzando Adobe Experience Manager (AEM) come un CMS headless. Scopri come utilizzare funzioni quali Modelli di contenuto, Frammenti di contenuto e un’API GraphQL per fornire contenuti headless.
landing-page-description: Scopri la distribuzione e l’implementazione headless dei contenuti. Ulteriori informazioni sullo sviluppo della strategia all’interno dell’azienda.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 95%

---

# Percorso per sviluppatori CMS headless di AEM {#aem-headless-developer-journey}

Benvenuto nella documentazione per gli sviluppatori che sono nuovi nel CMS headless di Adobe Experience Manager!

Scopri le funzioni headless potenti e flessibili, le loro funzionalità e come utilizzarle nel tuo primo progetto di sviluppo headless. Questo percorso fornisce tutte le informazioni necessarie per sviluppare la tua prima applicazione headless.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="Risorse per sviluppatori headless di AEM e documentazione avanzata"
>abstract="Tutto il necessario per scoprire il CMS headless di AEM e per creare e distribuire applicazioni migliori ed esperienze più veloci."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it" text="Risorse per sviluppatori headless di AEM"


## Introduzione {#introduction}

L’implementazione headless di AEM utilizza modelli di frammenti di contenuto e frammenti di contenuto per concentrarsi sulla creazione di frammenti di contenuto strutturati, neutri rispetto ai canali e riutilizzabili e sulla loro distribuzione cross-channel. A questo scopo, dimentica la gestione delle pagine e dei componenti come avviene nelle soluzioni stack complete. Si tratta di un modello di sviluppo dinamico e moderno per implementare esperienze digitali.

Questa guida ti orienta attraverso gli argomenti di implementazione headless in AEM, così al termine:

* Comprenderai appieno cosa è la distribuzione di contenuti headless e i relativi vantaggi.
* Scoprirai le funzioni headless di AEM e come funzionano insieme per offrire un’esperienza headless.
* Sarai in grado di iniziare a implementare il primo progetto headless AEM.

## Pubblico {#audience}

Questo percorso è progettato per l’utente tipo sviluppatore, esponendo i requisiti, i passaggi e l’approccio di un progetto AEM Headless dal punto di vista dello sviluppatore. Il percorso definisce gli utenti tipo aggiuntivi con cui lo sviluppatore deve interagire per un progetto di successo, ma il punto di vista del percorso è quello dello sviluppatore.

Di seguito sono riportati gli utenti tipo che interagiscono in questo percorso.

| Persona | Descrizione | Mansione in questo percorso |
|---|---|---|
| Sviluppatore (pubblico target) | Ha esperienza nello sviluppo di applicazioni headless che utilizzano contenuti provenienti da diverse fonti | Pubblico target di questo percorso |
| Autore del contenuto | Crea e gestisce contenuti che vengono distribuiti in modo headless | Gli autori dei contenuti creano contenuti che lo sviluppatore distribuisce in modo headless. |
| Amministratore | Gestisce l’impostazione e la configurazione di base di AEM | Lo sviluppatore collabora con l’amministratore per apportare le modifiche di configurazione necessarie per lo sviluppo. |
| Architetto dei contenuti | Analizza i requisiti dei dati che devono essere distribuiti in modo headless e definisce la struttura per questi dati | Gli sviluppatori lavorano con l’architect dei contenuti per comprendere la struttura dei dati e i requisiti necessari per distribuirli in modo headless. |

## Percorso per sviluppatori headless {#the-journey}

Ci occuperemo di molti argomenti in questo percorso, che vi fornirà le informazioni essenziali sul sistema headless in AEM.

Anche se puoi andare direttamente a una particolare parte del percorso, molti concetti sono creati individualmente negli articoli precedenti. Adobe consiglia di iniziare dall’inizio e procedere in sequenza.

| # | Articolo | Descrizione |
|---|---|---|
| 0 | Percorso per sviluppatori headless di AEM | Questo documento |
| 1 | [Informazioni sullo sviluppo headless di CMS](learn-about.md) | Scopri la tecnologia headless e quando usarla. |
| 2 | [Guida introduttiva ad AEM Headless as a Cloud Service](getting-started.md) | Scopri i prerequisiti headless di AEM |
| 3 | [Percorso della tua prima esperienza con AEM Headless](path-to-first-experience.md) | Imposta l’ambiente di sviluppo e scopri come integrare un’app semplice con AEM Headless |
| 4 | [Come modellare il contenuto](model-your-content.md) | Scopri come modellare la struttura del contenuto. |
| 5 | [Come accedere al contenuto tramite API di consegna AEM](access-your-content.md) | Scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto. |
| 6 | [Come aggiornare il contenuto tramite API di AEM Assets](update-your-content.md) | Scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto. |
| 7 | [Come raggruppare la tua app e i tuoi contenuti in AEM Headless](put-it-all-together.md) | Scopri come prendere il progetto AEM e prepararlo per pubblicare con l’SDK headless di AEM. |
| 8 | [Come effettuare il Go Live con la tua applicazione headless](go-live.md) | Scopri come distribuire l’applicazione in tempo reale e prendere il codice locale in Git per spostarlo nella pipeline CI/CD di Cloud Manager Git. |
| 9 | [Facoltativo - Come creare applicazioni a pagina singola (SPA) con AEM](create-spa.md) | Scopri come combinare consegna headful e headless e come creare SPA modificabili utilizzando il framework dell’editor SPA di AEM. |

{style="table-layout:auto"}

## Passaggio successivo {#what-is-next}

Per iniziare, consulta il prossimo articolo: [Informazioni sullo sviluppo CMS headless](learn-about.md).

## Risorse aggiuntive {#additional-resources}

I percorsi di documentazione mostrano come AEM risolve un problema aziendale fornendo una descrizione che ti guida attraverso i processi e le funzionalità correlati. Un percorso illustra il funzionamento congiunto di più funzioni per soddisfare le esigenze di un’unica azienda.

Se preferisci imparare facendo e hai una conoscenza esistente di AEM, segui i nostri tutorial pratici organizzati per API e framework, che esplorano la creazione e l’utilizzo di applicazioni create su AEM Headless. Consulta [Tutorial per Headless in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it).

Dai un’occhiata ai percorsi aggiuntivi per ulteriori informazioni su come interagiscono le potenti funzioni di AEM.

* Il [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Percorso di traduzione headless AEM](/help/journey-headless/translation/overview.md) - questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, di come AEM si serve di contenuti headless e di come tradurli.
* [Percorso di authoring headless](/help/journey-headless/author/overview.md): inizia qui un percorso guidato attraverso le potenti e flessibili funzionalità headless di AEM, le potenzialità e i modi in cui modellare i contenuti sul tuo primo progetto headless.
* [Percorso architetto headless](/help/journey-headless/architect/overview.md): fai clic qui per un’introduzione alle potenti e flessibili funzionalità headless di Adobe Experience Manager as a Cloud Service e per vedere come modellare i contenuti per il tuo progetto.
* [Documentazione tecnica di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it): se hai già un’azienda che conosce AEM e le tecnologie headless, dai un’occhiata ai documenti tecnici approfonditi.
   * [Introduzione ad AEM come CMS headless](/help/headless/introduction.md)
