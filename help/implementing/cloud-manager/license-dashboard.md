---
title: Dashboard delle licenze
description: Cloud Manager fornisce una dashboard per visualizzare facilmente i diritti dei prodotti AEMaaCS disponibili per la tua organizzazione o tenant.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: b5078c849c9fa088546f5df1fcbef1dec59f3cdb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 80%

---

# Dashboard delle licenze {#license-dashboard}

Cloud Manager fornisce una dashboard per visualizzare facilmente i diritti dei prodotti AEMaaCS disponibili per la tua organizzazione o tenant.

## Panoramica {#overview}

Con la dashboard delle licenze di Cloud Manager è possibile accedere facilmente alle seguenti informazioni:

1. Diritti delle soluzioni disponibili per tutti i programmi, compresi quelli utilizzati e quelli disponibili
1. Metriche sul consumo delle richieste di contenuto con trend mensili per la soluzione Sites

## Utilizzo della dashboard delle licenze {#using-dashboard}

Per accedere alla dashboard delle licenze, segui la procedura riportata di seguito.

>[!NOTE]
>
>Per visualizzare la dashboard delle licenze, l’utente con il ruolo **Proprietario business** deve aver effettuato l’accesso.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Dalla pagina di panoramica dei prodotti, passa alla scheda **Licenza**.

![Dashboard delle licenze](assets/license-dashboard.png)

La dashboard è divisa in tre sezioni:

* **Soluzioni**: in questa sezione vengono riepilogate le soluzioni per le quali si dispone di una licenza, come ad esempio Sites o Assets.
* **Componenti aggiuntivi**: in questa sezione vengono riepilogati i componenti aggiuntivi disponibili per le soluzioni concesse in licenza.
* **Ambienti sandbox e di sviluppo**: in questa sezione vengono riepilogati gli ambienti disponibili.

In ogni sezione vengono riepilogate le opzioni disponibili e come sono attualmente utilizzate, se del caso. Attualmente, anche se nel tenant sono presenti altre soluzioni, vengono visualizzate solo quelle Sites.

* La colonna **Stato** mostra il confronto tra il numero di diritti inutilizzati e quelli totali disponibili per il tenant.
* La colonna **Configurato per** indica i programmi ai quali il diritto per la soluzione è stato applicato.
   * Un diritto viene considerato utilizzato solo quando è stato creato un ambiente di produzione o, se ne esiste già uno, se al suo interno è stata eseguita una pipeline di aggiornamento.
* Una volta selezionata, la colonna **Utilizzo** visualizza le richieste di contenuto presentate negli ultimi 12 mesi sotto forma di grafico.

>[!TIP]
>
>Per ulteriori informazioni su come gestire i diritti Adobe in tutta l’organizzazione da Admin Console, consulta [Panoramica di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

## Domande frequenti {#faq}

### Che cos’è una richiesta di contenuto? {#what-is-a-content-request}

Una richiesta di contenuto è una richiesta che arriva in AEM Sites o in qualsiasi sistema di caching fornito dal cliente, ad esempio una rete di distribuzione di contenuti, per distribuire contenuto o dati in formato HTML come visualizzazione di pagina o in formato JSON come chiamata API.

Viene conteggiata una richiesta di contenuto per ogni visualizzazione di pagina o per ogni cinque chiamate API, misurate all’ingresso del primo sistema di caching che riceve una richiesta di contenuto. Le richieste di contenuto vengono conteggiate solo per gli ambienti di produzione.

Dalle richieste di contenuto sono escluse le richieste o le attività avviate da o per conto di Adobe al solo scopo di fornire prodotti e servizi. È escluso anche il traffico dell’agente utente identificato da Adobe come proveniente da bot, crawler e spider relativi ai comuni motori di ricerca e servizi di social media.

### In che modo Adobe Experience Manager misura le richieste di contenuto? {#how-are-content-requests-measured}

Le richieste di contenuto vengono tracciate sui server perimetrali AEM as a Cloud Service. Il traffico di origine non viene conteggiato per le richieste di contenuto. La CDN integrata in AEM as a Cloud Service traccia le richieste HTML e JSON valide.

AEM inoltre offre regole per escludere bot noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio.

### Perché il rapporto di Analytics mostra risultati diversi rispetto alle richieste di contenuto di AEM? {#why-are-reports-different}

Le richieste di contenuto presentano delle varianze rispetto agli strumenti di generazione rapporti di Analytics di un’organizzazione, come riepilogato in questa tabella.

| Motivo della varianza | Spiegazione |
|---|---|
| Assegnazione dei tag | Alle pagine tracciate come richieste di contenuto di AEM possono essere assegnati o meno dei tag per il tracciamento di Analytics. Alle chiamate API tracciate come richieste di contenuto di AEM non vengono assegnati tag dallo strumento Analytics di un’organizzazione.<br>Alle pagine o alle chiamate API possono essere assegnati dei tag per tenere traccia delle azioni o solo delle visualizzazioni di pagina univoche, anziché di tutte. |
| Regole di gestione dei tag | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che non sono stati pre-identificati e rimossi da AEM possono causare discrepanze nel tracciamento. |
| Suite per rapporti | Le pagine che fanno parte della stessa istanza di AEM e dello stesso dominio possono inviare dati a suite per rapporti di Analytics diverse. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e sicurezza possono generare richieste di contenuto per AEM che non vengono monitorate nei rapporti di Analytics. |
| Richieste di prelettura | L’utilizzo di un servizio di prelettura per precaricare le pagine al fine di aumentare la velocità può causare un aumento significativo del traffico delle richieste di contenuto. |
| DDOS | Sebbene Adobe si impegni al massimo per rilevare e filtrare automaticamente il traffico dagli attacchi DDOS, non c’è alcuna garanzia che tutti i possibili attacchi DDOS vengano rilevati. |
| Blocchi del traffico | L’utilizzo di un blocco del tracciamento in un browser può far sì che il tracciamento di alcune richieste non venga eseguito. |
| Firewall | I firewall possono bloccare il tracciamento di Analytics. Il problema è più frequente con i firewall aziendali. |

### Cosa succede se voglio saperne di più sul volume di richiesta del contenuto? {#current-request-volumes}

Se desideri ulteriori informazioni sul volume di richiesta del contenuto visualizzato nel dashboard della licenza, il team di Adobe può fornire un rapporto che mostra i principali driver di volume delle richieste di contenuto. Rivolgiti al tuo team di Adobe o all’Assistenza clienti Adobe per richiedere un rapporto sull’utilizzo principale.

### Cosa succede se utilizzo una rete CDN personalizzata? {#using-own-cdn}

Il Dashboard licenze mostrerà solo i dati tracciati dal CDN del Cloud Service.  Se scegli di portare il tuo CDN (BYOCDN), segnalerai il volume della richiesta di contenuti all&#39;Adobe su base annuale, come indicato nel tuo contratto.
