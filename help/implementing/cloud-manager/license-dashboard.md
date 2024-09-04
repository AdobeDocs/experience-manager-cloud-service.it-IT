---
title: Dashboard delle licenze
description: Cloud Manager fornisce una dashboard per visualizzare facilmente i diritti dei prodotti AEMaaCS disponibili per la tua organizzazione o tenant.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 57fb7a011cb2da853cdca4f3233cd56775f4a459
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 37%

---


# Dashboard delle licenze {#license-dashboard}

Cloud Manager fornisce una dashboard per visualizzare facilmente i diritti dei prodotti AEMaaCS disponibili per la tua organizzazione o tenant.

>[!IMPORTANT]
>
>La dashboard delle licenze si applica solo ai programmi AEM as a Cloud Service. [I programmi AMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction) non sono inclusi nel dashboard delle licenze.
>
>Per determinare il tipo di servizio di cui dispone il programma (AMS o AEMaaCS), consulta il documento [Navigazione nell&#39;interfaccia utente di Cloud Manager.](/help/implementing/cloud-manager/navigation.md#program-cards)

## Panoramica {#overview}

Con la dashboard delle licenze di Cloud Manager è possibile accedere facilmente alle seguenti informazioni:

1. Le adesioni alle soluzioni sono disponibili per tutti i programmi, inclusi quelli utilizzati e quelli disponibili
1. Metriche sul consumo delle richieste di contenuto con trend mensili per la soluzione Sites

## Utilizzo della dashboard delle licenze {#using-dashboard}

Per accedere alla dashboard delle licenze, segui la procedura riportata di seguito.

>[!NOTE]
>
>Un utente con il ruolo **Proprietario business** deve aver effettuato l&#39;accesso per visualizzare la dashboard delle licenze.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.
1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, tocca o fai clic sul pulsante del menu hamburger nell&#39;intestazione [Cloud Manager.](/help/implementing/cloud-manager/navigation.md#cloud-manager-header) Mostra le schede.
1. Tocca o fai clic sull&#39;opzione **Licenza** nella scheda.

![Dashboard delle licenze](assets/license-dashboard.png)

La dashboard è divisa in tre sezioni:

* **Soluzioni**: in questa sezione vengono riepilogate le soluzioni per le quali si dispone di una licenza, come ad esempio Sites o Assets.
* **Componenti aggiuntivi**: in questa sezione vengono riepilogati i componenti aggiuntivi disponibili per le soluzioni concesse in licenza.
* **Altri diritti**: in questa sezione vengono riepilogati la sandbox e l&#39;ambiente di sviluppo nonché altri diritti utilizzabili all&#39;interno del tenant.

Ogni sezione riepiloga ciò che è disponibile e come viene utilizzato, se del caso. Attualmente, anche se nel tenant sono presenti altre soluzioni, vengono visualizzate solo quelle Sites e Assets.

* La colonna **Stato** visualizza il numero di diritti inutilizzati rispetto al totale disponibile per il tenant.
* La colonna **Configurato per** indica i programmi ai quali il diritto per la soluzione è stato applicato.
   * Un diritto viene considerato utilizzato solo quando è stato creato un ambiente di produzione o, se ne esiste uno, se su di esso è stata eseguita una pipeline di aggiornamento.
   * Solo un numero limitato di programmi è elencato singolarmente nella colonna con il resto rappresentato da una voce `+x`.
   * Passa il puntatore del mouse sulla voce `+x` per visualizzare un popup con i dettagli di tutti i programmi.
* La colonna **Utilizzo** visualizza un pulsante **[Visualizza dettagli sull&#39;utilizzo](#view-usage-details)** per visualizzare le statistiche di utilizzo per la soluzione.

>[!TIP]
>
>Per informazioni su come gestire i diritti Adobe in tutta l&#39;organizzazione da Admin Console, consulta la [panoramica Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

## Visualizza i dettagli sull’utilizzo {#view-usage-details}

<!--
The **View usage details** button gives access to the chosen solution's **Usage Details** window. This window gives a detailed breakdown including charts to show your solution's usage. How that usage is measured depends on the chosen solution. -->

Il pulsante **Visualizza dettagli sull&#39;utilizzo** nell&#39;area Licenza di Cloud Manager fornisce un&#39;analisi dettagliata dell&#39;utilizzo corrente delle risorse. Se cliccato, si apre un report o un dashboard che mostra metriche importanti relative alla licenza. <!-- ADD THIS SENTENCE IF ASSETS USAGE DETAILS GETS REINSTATED ", such as the number of users, storage consumption, or bandwidth usage, depending on the type of services you're using." --> Questa funzionalità consente di monitorare e assicurarsi di rimanere entro i limiti del contratto, offrendo al contempo informazioni approfondite per una migliore pianificazione e ottimizzazione delle risorse.

### Dettagli sull’utilizzo di Sites {#sites-usage-details}

La finestra **Dettagli sull&#39;utilizzo di Sites** presenta grafici che offrono una panoramica dell&#39;utilizzo delle licenze Sites in base a [richieste di contenuto.](#what-is-a-content-request)

![Finestra dettagli utilizzo siti](assets/sites-usage-details.png)

Il lato sinistro della finestra presenta un grafico a torta che mostra il raggruppamento del contratto per l&#39;anno contrattuale selezionato nel menu a discesa **Visualizza anno contrattuale**.

Il lato destro della finestra presenta un grafico ad area che mostra l&#39;utilizzo suddiviso per programma nel tempo per l&#39;anno di contratto selezionato. Al passaggio del mouse viene visualizzata una finestra a comparsa con i dettagli del programma per il momento selezionato.

<!-- REMOVED AS PER CQDOC-21983
### Assets usage details {#assets-usage-details}

The **Assets usage details** window, presents graphs giving an overview of the usage of your Assets licenses based on [storage](#storage) and [standard users.](#standard-users) Select the appropriate tab to toggle between the views.

For both storage and standard users views, you can use the **Environment Type** dropdown to toggle the view between production, stage, and development environments.

#### Storage {#storage}

![Assets usage details window for storage](assets/assets-usage-details-storage.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time.

#### Standard Users {#standard-users}

![Assets usage details window for standard-users](assets/assets-usage-details-standard-users.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time. -->

## Domande frequenti {#faq}

### Che cos’è una richiesta di contenuto? {#what-is-a-content-request}

Una richiesta di contenuto è una richiesta pervenuta in AEM Sites o in qualsiasi sistema di caching fornito dal cliente, ad esempio una rete di distribuzione di contenuti, per distribuire contenuti o dati in formato HTML come vista pagina o in formato JSON come chiamata API.

Viene conteggiata una richiesta di contenuto per ogni visualizzazione di pagina o per ogni cinque chiamate API, misurate all’ingresso del primo sistema di caching che riceve una richiesta di contenuto. Le richieste di contenuto vengono conteggiate solo per gli ambienti di produzione.

Le richieste di contenuto escludono le richieste o le attività avviate da o per conto di Adobe al solo scopo di fornire prodotti e servizi. È escluso anche il traffico dell’agente utente identificato da Adobe come proveniente da bot, crawler e spider relativi ai comuni motori di ricerca e servizi di social media.

Vedi anche [Informazioni sulle richieste di contenuto del Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### In che modo Adobe Experience Manager misura le richieste di contenuto? {#how-are-content-requests-measured}

Le richieste di contenuto vengono tracciate sui server Edge di AEM as a Cloud Service. Il traffico di origine non viene conteggiato per le richieste di contenuto. La rete CDN integrata in AEM as a Cloud Service traccia le richieste HTML e JSON valide.

AEM inoltre offre regole per escludere bot noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio.

Vedi anche [Informazioni sulle richieste di contenuto del Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### Perché il rapporto di Analytics mostra risultati diversi rispetto alle richieste di contenuto di AEM? {#why-are-reports-different}

Le richieste di contenuto possono presentare varianze con gli strumenti di reporting di Analytics di un’organizzazione. Per ulteriori informazioni, vedere [Informazioni sulle richieste di contenuto di Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### Come posso ottenere ulteriori informazioni sul volume di richieste di contenuto? {#current-request-volumes}

Se desideri ulteriori informazioni sul volume di richieste di contenuto visualizzato nella dashboard delle licenze, il team di Adobe può fornirti un rapporto che mostra i principali driver di volume delle richieste dei contenuti. Rivolgiti al tuo team di Adobi o all’Assistenza clienti di Adobe per richiedere un rapporto sull’utilizzo ottimale.

### Cosa succede se utilizzo una mia rete CDN? {#using-own-cdn}

La Dashboard delle licenze mostra solo i dati tracciati dalla rete CDN del Cloud Service. Se scegli di usare una tua rete CDN (BYOCDN), devi riportare il volume di richieste di contenuto all’Adobe su base annuale, come indicato nel contratto.
