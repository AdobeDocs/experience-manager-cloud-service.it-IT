---
title: Dashboard delle licenze
description: Cloud Manager fornisce una dashboard per visualizzare facilmente i diritti dei prodotti AEMaaCS disponibili per la tua organizzazione o tenant.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: eae5c75e1bf4f7201fe2c01d08737d36489ca3e4
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 31%

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

## Visualizza dettagli utilizzo {#view-usage-details}

Il pulsante **Visualizza dettagli sull&#39;utilizzo** consente di accedere alla finestra **Dettagli sull&#39;utilizzo** della soluzione scelta. Questa finestra fornisce una suddivisione dettagliata che include grafici per mostrare l’utilizzo della soluzione. Il modo in cui viene misurato l’utilizzo dipende dalla soluzione scelta.

### Dettagli sull’utilizzo dei siti {#sites-usage-details}

La finestra **Dettagli sull&#39;utilizzo di Sites** presenta grafici che offrono una panoramica dell&#39;utilizzo delle licenze Sites in base a [richieste di contenuto.](#what-is-a-content-request)

![Finestra dettagli utilizzo siti](assets/sites-usage-details.png)

Il lato sinistro della finestra presenta un grafico a torta che mostra il raggruppamento del contratto per l&#39;anno contrattuale selezionato nel menu a discesa **Visualizza anno contrattuale**.

Il lato destro della finestra presenta un grafico ad area che mostra l&#39;utilizzo suddiviso per programma nel tempo per l&#39;anno di contratto selezionato. Al passaggio del mouse viene visualizzata una finestra a comparsa con i dettagli del programma per il momento selezionato.

### Dettagli sull’utilizzo di Assets {#assets-usage-details}

La finestra **Dettagli sull&#39;utilizzo di Assets** presenta grafici che offrono una panoramica sull&#39;utilizzo delle licenze Assets in base a [storage](#storage) e [utenti standard.](#standard-users) Selezionare la scheda appropriata per alternare le visualizzazioni.

Sia per le visualizzazioni di archiviazione che per quelle degli utenti standard, è possibile utilizzare il menu a discesa **Tipo di ambiente** per alternare la visualizzazione tra gli ambienti di produzione, stage e sviluppo.

#### Archiviazione {#storage}

![Finestra dei dettagli sull&#39;utilizzo di Assets per l&#39;archiviazione](assets/assets-usage-details-storage.png)

Il lato sinistro della finestra presenta un grafico a torta che mostra il raggruppamento del contratto per l&#39;anno contrattuale selezionato nel menu a discesa **Visualizza anno contrattuale**.

Il lato destro della finestra presenta un grafico ad area che mostra l&#39;utilizzo suddiviso per programma nel tempo per l&#39;anno di contratto selezionato. Al passaggio del mouse viene visualizzata una finestra a comparsa con i dettagli del programma per il momento selezionato.

#### Utenti standard {#standard-users}

![Finestra dei dettagli sull&#39;utilizzo di Assets per gli utenti standard](assets/assets-usage-details-standard-users.png)

Il lato sinistro della finestra presenta un grafico a torta che mostra il raggruppamento del contratto per l&#39;anno contrattuale selezionato nel menu a discesa **Visualizza anno contrattuale**.

Il lato destro della finestra presenta un grafico ad area che mostra l&#39;utilizzo suddiviso per programma nel tempo per l&#39;anno di contratto selezionato. Al passaggio del mouse viene visualizzata una finestra a comparsa con i dettagli del programma per il momento selezionato.

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
