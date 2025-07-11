---
title: Creazione di un sito
description: Scopri come utilizzare AEM per creare un sito utilizzando i modelli di sito per definire lo stile e la struttura del sito.
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 80%

---

# Creazione di un sito {#creating-site}

{{traditional-aem}}

Scopri come utilizzare AEM per creare un sito utilizzando i modelli per definire lo stile e la struttura del sito.

## Panoramica {#overview}

Prima che gli autori dei contenuti possano creare pagine con contenuti, è necessario creare il sito. Questo viene generalmente eseguito da un amministratore AEM che definisce la struttura iniziale del sito. L’utilizzo dei modelli di sito rende la creazione del sito veloce e flessibile.

Lo strumento Creazione rapida sito di AEM consente ai non sviluppatori di creare rapidamente un sito da zero utilizzando i modelli di sito.

Una volta creato, lo strumento Creazione rapida sito consente inoltre di personalizzare velocemente il tema e lo stile del sito AEM (risorse JavaScript, CSS e statiche). In questo modo lo sviluppatore front-end, che non ha bisogno di conoscere AEM, può lavorare in maniera autonoma e in parallelo ai creatori di contenuti. L’amministratore AEM scarica semplicemente il tema del sito e lo fornisce allo sviluppatore front-end. Quest&#39;ultimo lo personalizza utilizzando i propri strumenti preferiti e successivamente conferma le modifiche nell’archivio del codice AEM, che viene quindi distribuito.

Questo documento si concentra sulla creazione del sito utilizzando lo strumento Creazione rapida sito. Per una panoramica del flusso di lavoro di creazione e personalizzazione del sito, consulta [Percorso di creazione di siti rapidi AEM](/help/journey-sites/quick-site/overview.md)

## Struttura di pianificazione del sito {#structure}

Prendi in considerazione lo scopo del tuo sito e i contenuti pianificati con largo anticipo. Questo ti guiderà su come progettare la struttura del sito. Una buona struttura del sito supporta una facile navigazione e l’individuazione dei contenuti per i visitatori e supporta varie funzioni di AEM come la [gestione e traduzione multisito](/help/sites-cloud/administering/msm-and-translation.md).

>[!TIP]
>
>[Il sito di riferimento WKND](https://wknd.site) fornisce un’implementazione delle best practice di un sito web completamente funzionale di un marchio di esperienze outdoor. Esploralo per vedere come è strutturato un sito AEM ben costruito.

## Modelli per siti {#site-templates}

Poiché la struttura del sito è così importante per il successo di un sito, è opportuno disporre di strutture predefinite per distribuire rapidamente un nuovo sito in base a un insieme di standard esistenti. I modelli di sito consentono di combinare i contenuti di base del sito in un pacchetto comodo e riutilizzabile.

Per consentire un rapido avvio del nuovo sito, i modelli di sito generalmente contengono il contenuto e la struttura di base del sito e informazioni sul suo stile. I modelli sono efficaci perché sono riutilizzabili e personalizzabili. Inoltre, poiché è possibile disporre di più modelli durante l’installazione di AEM, è possibile creare siti diversi per soddisfare le varie esigenze aziendali.

>[!TIP]
>
>Per ulteriori dettagli sui modelli di sito, consulta [Modelli di sito](site-templates.md).

>[!NOTE]
>
>Il modello di sito non deve essere confuso con i modelli di pagina. I modelli di sito definiscono la struttura complessiva di un sito. Un modello di pagina definisce la struttura e il contenuto iniziale di una singola pagina.

## Creazione di un sito {#create-site}

L’utilizzo di un modello per creare un sito è semplice.

1. Accedi all’ambiente di authoring di AEM e passa alla console Sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Seleziona **Crea** in alto a destra dello schermo e, dal menu a discesa, seleziona **Sito da modello**.

   ![Creazione di un sito da un modello](../assets/create-site-from-template.png)

1. Nella procedura guidata Crea sito, seleziona un modello esistente nel pannello a sinistra o in **Importa** nella parte superiore della colonna di sinistra per importare un nuovo modello.

   ![Creazione guidata sito](../assets/site-creation-wizard.png)

   1. Se hai scelto di importare, individua il modello da utilizzare nel browser dei file e seleziona **Carica**.

   1. Una volta caricato, viene visualizzato nell’elenco dei modelli disponibili.

1. Quando si seleziona un modello, vengono visualizzate informazioni sul modello nella colonna di destra. Con il modello desiderato selezionato, seleziona **Avanti**.

   ![Seleziona un modello](../assets/select-site-template.png)

1. Immetti un titolo per il sito. Puoi specificare un nome per il sito o generarlo dal titolo.

   * Il titolo del sito viene visualizzato nella barra del titolo del browser.
   * Il nome del sito diventa parte dell’URL.
   * Il nome del sito deve rispettare [le convenzioni di denominazione delle pagine di AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices).

1. Selezionare **Crea** e il sito verrà creato dal modello di sito.

   ![Dettagli del nuovo sito](../assets/create-site-details.png)

1. Nella finestra di dialogo di conferma, seleziona **Fine**.

   ![Finestra di dialogo di successo](../assets/success.png)

1. Nella console Sites, il nuovo sito è visibile ed è possibile visitarlo per esplorarne la struttura di base definita dal modello.

   ![Nuova struttura del sito](../assets/new-site.png)

Gli autori dei contenuti possono ora iniziare a creare.

## Personalizzazione del sito {#site-customization}

Se il sito richiede una personalizzazione oltre ai modelli disponibili, sono disponibili diverse opzioni.

* Se è necessario modificare la struttura del sito o il contenuto iniziale, [il modello di sito può essere personalizzato in base alle proprie esigenze](site-templates.md).
* Se è necessario modificare lo stile del sito, [il tema del sito può essere scaricato e personalizzato](/help/journey-sites/quick-site/overview.md).
* Se è necessario modificare la funzionalità del sito, [il sito può essere completamente personalizzato](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

Qualsiasi personalizzazione deve essere effettuata con il supporto di un team di sviluppo.
