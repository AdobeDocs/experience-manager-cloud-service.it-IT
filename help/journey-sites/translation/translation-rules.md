---
title: Configurare le regole di traduzione
description: Scopri come definire le regole di traduzione per identificare i contenuti per la traduzione.
index: true
hide: false
hidefromtoc: false
source-git-commit: 08127d72c84d6f47f5058ef631dc3128114f1953
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Configurare le regole di traduzione {#configure-translation-rules}

Scopri come definire le regole di traduzione per identificare i contenuti per la traduzione.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di traduzione di AEM Sites, [Configura connettore di traduzione](configure-connector.md) hai imparato a installare e configurare il connettore di traduzione e ora devi:

* Comprendi gli importanti parametri del framework di integrazione della traduzione in AEM.
* È possibile impostare la propria connessione al servizio di traduzione.

Ora che il connettore è configurato, questo articolo illustra il passaggio successivo per identificare il contenuto da tradurre.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come utilizzare AEM regole di traduzione per identificare il contenuto di traduzione. Dopo aver letto questo documento è necessario:

* Comprendi cosa fanno le regole di traduzione.
* Puoi definire le tue regole di traduzione.

## Regole di traduzione {#translation-rules}

Le pagine AEM Sites possono contenere molte informazioni. A seconda delle esigenze del progetto, è probabile che non tutte le informazioni all’interno di una pagina debbano essere tradotte.

Le regole di traduzione identificano il contenuto incluso o escluso nei progetti di traduzione. Quando il contenuto viene tradotto, AEM estrae o raccoglie il contenuto in base a queste regole. In questo modo solo il contenuto da tradurre viene inviato al servizio di traduzione.

Le regole di traduzione includono le seguenti informazioni:

* Percorso del contenuto a cui si applica la regola
   * La regola si applica anche ai discendenti del contenuto
* Nomi delle proprietà che contengono il contenuto da tradurre
   * La proprietà può essere specifica per un tipo di risorsa specifico o per tutti i tipi di risorsa

AEM crea automaticamente regole di traduzione per le pagine dei siti, ma poiché i requisiti di ciascun progetto sono diversi, è importante sapere come rivedere e adattare le regole in base alle esigenze del progetto.

## Creazione di regole di traduzione {#creating-rules}

È possibile creare più regole per supportare requisiti di traduzione complessi. Ad esempio, un progetto su cui si sta lavorando richiede la traduzione di tutte le informazioni di pagina, ma in un’altra pagina è necessario tradurre solo le descrizioni mentre i titoli non vengono tradotti.

Le regole di traduzione sono progettate per gestire tali scenari. Tuttavia, in questo esempio viene illustrato come creare regole concentrandoci su una configurazione semplice e singola.

Per configurare le regole di traduzione è disponibile una console **Configurazione traduzione** .

Per accedervi:

1. Passa a **Strumenti** -> **Generale**.
1. Tocca o fai clic su **Configurazione traduzione**.

AEM automaticamente le regole di traduzione per tutto il contenuto. Per visualizzare queste regole:

1. Seleziona il contesto `/content` e quindi l&#39;opzione **Modifica** dalla barra degli strumenti.
1. Viene aperto l’Editor regole di traduzione con le regole AEM create automaticamente per il percorso `/content` .

   ![Editor regole di traduzione](assets/translation-rules-editor.png)

1. Le proprietà di pagina che saranno tradotte si trovano nella sezione **Generale** dell’elenco. È possibile aggiungere o aggiornare i nomi di proprietà esistenti che si desidera includere esplicitamente nella traduzione.
   1. Immetti il nome della proprietà nel campo **Nuova proprietà** .
   1. Le opzioni **Traduci** e **Eredita** vengono selezionate automaticamente.
   1. Tocca o fai clic su **Aggiungi**.
   1. Ripetere questi passaggi per tutti i campi da tradurre.
   1. Tocca o fai clic su **Salva**.

Hai configurato le regole di traduzione.

>[!NOTE]
>
>AEM automaticamente le regole di traduzione. Per una configurazione di traduzione semplice o per testare un flusso di lavoro di traduzione, non è necessario creare nuove regole o persino modificare le regole esistenti create automaticamente. I dettagli di questi passaggi vengono presentati per spiegare come funzionano le regole e per dare contesto al modo in cui AEM elabora le traduzioni.

>[!TIP]
>
>È inoltre possibile creare regole solo per il percorso o il progetto in questione toccando o facendo clic sul pulsante **Aggiungi contesto** nella console Configurazione traduzione. Questo va oltre il campo di applicazione del percorso.

## Utilizzo avanzato {#advanced-usage}

È possibile configurare una serie di proprietà aggiuntive come parte delle regole di traduzione. Inoltre, è possibile specificare le regole manualmente come XML, il che consente maggiore specificità e flessibilità.

Queste funzioni non sono generalmente necessarie per iniziare a localizzare il contenuto, ma se ti interessa puoi trovare ulteriori informazioni nella sezione [Risorse aggiuntive](#additional-resources) .

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di traduzione di AEM Sites, devi:

* Comprendi cosa fanno le regole di traduzione.
* Puoi definire le tue regole di traduzione.

Sfrutta questa conoscenza e continua il tuo percorso di traduzione AEM Sites esaminando il documento [Traduci contenuto](translate-content.md), dove scoprirai come il connettore e le regole funzionano insieme per tradurre i contenuti.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di traduzione esaminando il documento [Traduci contenuto,](translate-content.md) sono riportate di seguito alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso.

* [Identificazione del contenuto da tradurre](/help/sites-cloud/administering/translation/rules.md)  - Scopri come le regole di traduzione identificano il contenuto da tradurre.
