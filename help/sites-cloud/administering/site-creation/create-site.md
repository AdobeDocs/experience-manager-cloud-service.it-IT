---
title: Creazione di un sito
description: Scopri come utilizzare AEM per creare un sito utilizzando i modelli di sito per definire lo stile e la struttura del sito.
feature: Administering
role: Admin
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 1%

---


# Creazione di un sito {#creating-site}

Scopri come utilizzare AEM creare un sito utilizzando i modelli di sito per definire lo stile e la struttura del sito.

## Panoramica {#overview}

Prima che gli autori dei contenuti possano creare pagine con contenuti, è necessario creare il sito. Questo viene generalmente eseguito da un amministratore AEM che definisce la struttura iniziale del sito. L’utilizzo dei modelli di sito rende la creazione di siti rapida e flessibile.

Lo strumento AEM Creazione rapida siti consente agli sviluppatori di creare rapidamente un nuovo sito da zero utilizzando i modelli di sito.

Una volta creato, lo strumento di creazione rapida del sito consente inoltre di personalizzare rapidamente il tema e lo stile del sito AEM (risorse JavaScript, CSS e statiche). In questo modo lo sviluppatore front-end, che necessita di una conoscenza di AEM pari a zero, può lavorare separatamente rispetto ai creatori di contenuti e in parallelo ad essi. L’amministratore AEM semplicemente scarica il tema del sito e lo fornisce allo sviluppatore front-end che lo personalizzerà utilizzando i propri strumenti preferiti e quindi commette le modifiche all’archivio del codice AEM, che viene quindi distribuito.

Questo documento si concentra sulla creazione del sito utilizzando lo strumento Creazione rapida sito. Per una panoramica del flusso di lavoro di creazione e personalizzazione del sito, consulta la sezione [AEM Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md)

## Struttura del sito di pianificazione {#structure}

Prenditi del tempo per prendere in considerazione lo scopo del tuo sito e i contenuti pianificati con largo anticipo. Questo ti guiderà come progettare la struttura del sito. Una buona struttura del sito supporta una facile navigazione e l’individuazione dei contenuti per i visitatori del tuo sito e supporta varie funzioni AEM come [gestione e traduzione multisito.](/help/sites-cloud/administering/msm-and-translation.md)

>[!TIP]
>
>[Sito di riferimento WKND](https://wknd.site) fornisce un’implementazione delle best practice per un sito web completo di brand per esperienze in esterni. Esploralo per vedere come è strutturato un sito AEM ben costruito.

## Modelli per siti {#site-templates}

Poiché la struttura del sito è così importante per il successo di un sito, è opportuno disporre di strutture predefinite per distribuire rapidamente un nuovo sito in base a un insieme di standard esistenti. I modelli di sito consentono di combinare i contenuti di base del sito in un pacchetto comodo e riutilizzabile.

I modelli di sito generalmente contengono il contenuto e la struttura di base del sito, nonché informazioni sullo stile del sito per consentire un rapido avvio del nuovo sito. I modelli sono potenti perché sono riutilizzabili e personalizzabili. Inoltre, poiché è possibile disporre di più modelli nell&#39;installazione di AEM, è possibile creare siti diversi per soddisfare le varie esigenze aziendali.

>[!TIP]
>
>Per maggiori dettagli sui modelli di sito, consulta la sezione [Modelli di sito](site-templates.md) articolo.

>[!NOTE]
>
>Il modello di sito non deve essere confuso con i modelli di pagina. I modelli di sito definiscono la struttura complessiva di un sito. Un modello di pagina definisce la struttura e il contenuto iniziale di una singola pagina.

## Creazione di un sito {#create-site}

L&#39;utilizzo di un modello per creare un sito è semplice.

1. Accedi all’ambiente di authoring AEM e passa alla console Sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Tocca o fai clic su **Crea** in alto a destra dello schermo e dal menu a discesa seleziona **Sito da modello**.

   ![Creazione di un sito da un modello](../assets/create-site-from-template.png)

1. Nella procedura guidata Crea sito , tocca o fai clic su un modello esistente nel pannello a sinistra o su **Importa** nella parte superiore sinistra della colonna per importare un nuovo modello.

   ![Creazione guidata sito](../assets/site-creation-wizard.png)

   1. Se hai scelto di importare, individua il modello da utilizzare nel browser dei file e tocca o fai clic su **Carica**.

   1. Una volta caricato, viene visualizzato nell’elenco dei modelli disponibili.

1. Quando si seleziona un modello, vengono visualizzate informazioni sul modello nella colonna di destra. Con il modello desiderato selezionato, tocca o fai clic su **Successivo**.

   ![Seleziona un modello](../assets/select-site-template.png)

1. Specifica un titolo per il sito. Se omesso, è possibile specificare un nome di sito o generarlo dal titolo.

   * Il titolo del sito viene visualizzato nella barra del titolo del browser.
   * Il nome del sito diventa parte dell’URL.
   * Il nome del sito deve rispettare [AEM convenzioni di denominazione delle pagine.](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)

1. Tocca o fai clic su **Crea** e il sito viene creato dal modello di sito.

   ![Dettagli del nuovo sito](../assets/create-site-details.png)

1. Nella finestra di dialogo di conferma visualizzata, tocca o fai clic su **Fine**.

   ![Finestra di dialogo di successo](../assets/success.png)

1. Nella console Sites, il nuovo sito è visibile e può essere navigato per esplorarne la struttura di base definita dal modello.

   ![Nuova struttura del sito](../assets/new-site.png)

Gli autori dei contenuti possono ora iniziare a creare.

## Personalizzazione del sito {#site-customization}

Se il sito richiede una personalizzazione oltre ai modelli disponibili, sono disponibili diverse opzioni.

* Se è necessario modificare la struttura del sito o il contenuto iniziale, [il modello di sito può essere personalizzato in base alle tue esigenze.](site-templates.md)
* Se è necessario regolare lo stile del sito, [il tema del sito può essere scaricato e personalizzato.](/help/journey-sites/quick-site/overview.md)
* Se è necessario modificare la funzionalità del sito, [il sito può essere completamente personalizzato.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

Qualsiasi personalizzazione deve essere effettuata con il supporto di un team di sviluppo.
