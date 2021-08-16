---
title: Configurare le regole di traduzione
description: Scopri come definire le regole di traduzione per identificare i contenuti per la traduzione.
index: false
hide: true
hidefromtoc: true
source-git-commit: 142c49b6b98dc78c3d36964dada1cfb900afee66
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# Configurare le regole di traduzione {#configure-translation-rules}

Scopri come definire le regole di traduzione per identificare i contenuti per la traduzione.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di traduzione senza testa AEM, [Configura connettore di traduzione](configure-connector.md) hai imparato a installare e configurare il connettore di traduzione e ora devi:

* Comprendi gli importanti parametri del framework di integrazione della traduzione in AEM.
* È possibile impostare la propria connessione al servizio di traduzione.

Ora che il connettore è configurato, questo articolo illustra il passaggio successivo per identificare il contenuto da tradurre.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come utilizzare AEM regole di traduzione per identificare il contenuto di traduzione. Dopo aver letto questo documento è necessario:

* Comprendi cosa fanno le regole di traduzione.
* Puoi definire le tue regole di traduzione.

## Regole di traduzione {#translation-rules}

I frammenti di contenuto, che rappresentano il contenuto headless, possono contenere molte informazioni organizzate in campi strutturati. A seconda delle esigenze del progetto, è probabile che non tutti i campi all’interno di un frammento di contenuto debbano essere tradotti.

Le regole di traduzione identificano il contenuto incluso o escluso nei progetti di traduzione. Quando il contenuto viene tradotto, AEM estrae o raccoglie il contenuto in base a queste regole. In questo modo solo il contenuto da tradurre viene inviato al servizio di traduzione.

Le regole di traduzione includono le seguenti informazioni:

* Percorso del contenuto a cui si applica la regola
   * La regola si applica anche ai discendenti del contenuto
* Nomi delle proprietà che contengono il contenuto da tradurre
   * La proprietà può essere specifica per un tipo di risorsa specifico o per tutti i tipi di risorsa

Poiché i modelli per frammenti di contenuto, che definiscono la struttura dei frammenti di contenuto, sono unici nel tuo progetto, è fondamentale impostare le regole di traduzione in modo AEM conoscere gli elementi dei modelli di contenuto da tradurre.

>[!TIP]
>
>Generalmente l&#39;architetto dei contenuti fornisce allo specialista della traduzione i **Nome proprietà** s di tutti i campi necessari per la traduzione. Questi nomi sono necessari per configurare le regole di traduzione. In qualità di specialista della traduzione, [è possibile trovare questi **Nome proprietà**&#x200B;è se stessi](getting-started.md#content-modlels) come descritto in precedenza in questo percorso.

## Creazione di regole di traduzione {#creating-rules}

È possibile creare più regole per supportare requisiti di traduzione complessi. Ad esempio, un progetto su cui si sta lavorando richiede la traduzione di tutti i campi del modello, ma su un altro solo campo di descrizione deve essere tradotto mentre i titoli non vengono tradotti.

Le regole di traduzione sono progettate per gestire tali scenari. Tuttavia, in questo esempio viene illustrato come creare regole concentrandoci su una configurazione semplice e singola.

Per configurare le regole di traduzione è disponibile una console **Configurazione traduzione** . Per accedervi:

1. Passa a **Strumenti** -> **Generale**.
1. Tocca o fai clic su **Configurazione traduzione**.

Nell&#39;interfaccia utente **Configurazione traduzione** sono disponibili diverse opzioni per le regole di traduzione. Qui vengono evidenziati i passaggi più necessari e tipici necessari per una configurazione di base della localizzazione headless.

1. Tocca o fai clic su **Aggiungi contesto** per aggiungere un percorso. Percorso del contenuto interessato dalla regola.
   ![Aggiungi contesto](assets/add-translation-context.png)
1. Usa il browser percorsi per selezionare il percorso richiesto e tocca o fai clic sul pulsante **Conferma** per salvare. I frammenti di contenuto, che contengono contenuto headless, si trovano generalmente in `/content/dam/<your-project>`.
   ![Selezionare il percorso](assets/select-context.png)
1. AEM salva la configurazione.
1. Seleziona il contesto appena creato, quindi tocca o fai clic su **Modifica**. Viene aperto **Editor regole di traduzione** per configurare le proprietà.
   ![Editor regole di traduzione](assets/translation-rules-editor.png)
1. Per impostazione predefinita, tutte le configurazioni vengono ereditate dal percorso padre, in questo caso `/content/dam`. Deseleziona l’opzione **Eredita da`/content/dam`** per aggiungere ulteriori campi alla configurazione.
1. Una volta deselezionata, nella sezione **Generale** dell’elenco aggiungere i nomi delle proprietà dei modelli di frammento di contenuto [identificati in precedenza come campi da tradurre.](getting-started.md#content-models)
   1. Immetti il nome della proprietà nel campo **Nuova proprietà** .
   1. Le opzioni **Traduci** e **Eredita** vengono selezionate automaticamente.
   1. Tocca o fai clic su **Aggiungi**.
   1. Ripetere questi passaggi per tutti i campi da tradurre.
   1. Tocca o fai clic su **Salva**.
      ![Aggiungi proprietà](assets/add-property.png)

Hai configurato le regole di traduzione.

## Utilizzo avanzato {#advanced-usage}

È possibile configurare una serie di proprietà aggiuntive come parte delle regole di traduzione. Inoltre, è possibile specificare le regole manualmente come XML, il che consente maggiore specificità e flessibilità.

Queste funzioni non sono generalmente necessarie per iniziare a localizzare i contenuti headless, ma se ti interessa puoi trovare ulteriori informazioni nella sezione [Risorse aggiuntive](#additional-resources) .

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di traduzione headless dovresti:

* Comprendi cosa fanno le regole di traduzione.
* Puoi definire le tue regole di traduzione.

Sviluppa questa conoscenza e continua il tuo percorso di traduzione senza testa AEM esaminando il documento [Traduci contenuto](translate-content.md) dove potrai scoprire come il connettore e le regole funzionano insieme per tradurre contenuti headless.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di traduzione headless esaminando il documento [Traduci contenuto,](translate-content.md) sono riportate di seguito alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino nel percorso headless.

* [Identificazione del contenuto da tradurre](/help/sites-cloud/administering/translation/rules.md)  - Scopri come le regole di traduzione identificano il contenuto da tradurre.
