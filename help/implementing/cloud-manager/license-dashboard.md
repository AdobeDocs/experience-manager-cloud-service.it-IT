---
title: Dashboard di licenza
description: Cloud Manager fornisce una dashboard per visualizzare facilmente le adesioni ai prodotti AEMaaCS disponibili per la tua organizzazione o tenant.
source-git-commit: 82b4a4c8da9f42de08c19eb3caf25ff3a1bad4d4
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---


# Dashboard di licenza {#license-dashboard}

Cloud Manager fornisce una dashboard per visualizzare facilmente le adesioni ai prodotti AEMaaCS disponibili per la tua organizzazione o tenant.

## Panoramica {#overview}

Il Dashboard di licenza di Cloud Manager fornisce un facile accesso alle seguenti informazioni:

1. Diritti alla soluzione disponibili in tutti i programmi, compresi quelli utilizzati e quelli disponibili
1. Metriche di consumo della richiesta di contenuto con tendenze mensili per la soluzione Sites

## Utilizzo del dashboard delle licenze {#using-dashboard}

Per accedere al dashboard delle licenze, segui questi passaggi.

>[!NOTE]
>
>Un utente in **Proprietario business** per visualizzare il dashboard della licenza è necessario accedere al ruolo.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Nella pagina di panoramica dei prodotti , passa alla pagina **Licenza** scheda .

![Dashboard di licenza](assets/license-dashboard.png)

Il dashboard è diviso in tre sezioni che ti mostrano:

* **Soluzioni** - Questa sezione riepiloga le soluzioni per le quali hai concesso la licenza, ad esempio Sites o Assets.
* **Componenti aggiuntivi** - In questa sezione vengono riepilogati i componenti aggiuntivi disponibili per le soluzioni concesse in licenza.
* **Sandbox e ambienti di sviluppo** - Questa sezione riepiloga gli ambienti disponibili.

Ogni sezione riepiloga le opzioni disponibili e il modo in cui viene attualmente utilizzata, se del caso. Attualmente vengono visualizzate solo le soluzioni Sites anche se nel tenant sono presenti altre soluzioni.

* La **Stato** visualizza il numero di adesioni non utilizzate rispetto al totale disponibile per il tenant.
* La **Configurato su** colonna indica i programmi in cui è stata applicata l&#39;adesione alla soluzione.
   * Un diritto viene considerato utilizzato solo quando è stato creato un ambiente di produzione o se esiste già, se è stata eseguita una pipeline di aggiornamento.
* La **Utilizzo** In questa colonna vengono visualizzate le richieste di contenuto utilizzate negli ultimi 12 mesi sotto forma di grafico quando si fa clic su di esse.

>[!TIP]
>
>Fai riferimento a [Panoramica di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per scoprire come gestire le adesioni agli Adobi in tutta l’organizzazione a partire dall’Admin Console.

## Domande frequenti  {#faq}

### Cos’è una richiesta di contenuto? {#what-is-a-content-request}

Una richiesta di contenuto è una richiesta che arriva in AEM Sites o in qualsiasi sistema di caching fornito dal cliente, ad esempio una rete di distribuzione di contenuti, per distribuire contenuto o dati in formato HTML come visualizzazione di pagina o in formato JSON come chiamata API.

Viene conteggiata una richiesta di contenuto per ogni visualizzazione di pagina o per ogni cinque chiamate API, misurate in base all’ingresso del primo sistema di memorizzazione in cache che riceve una richiesta di contenuto.

Le richieste di contenuto escludono le richieste o le attività avviate da o per conto dell’Adobe al solo scopo di fornire prodotti e servizi. Sono esclusi anche il traffico di agenti utente identificati da Adobi da bot, crawler e spider relativi a motori di ricerca comuni e servizi di social media.

### In che modo Adobe Experience Manager misura le richieste di contenuto? {#how-are-content-requests-measured}

Le richieste di contenuto sono monitorate lato server all&#39;interno del Cloud Service. La CDN integrata in AEM as a Cloud Service traccia le richieste HTML e JSON valide. AEM inoltre ha delle regole per escludere bot ben noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare il loro indice di ricerca o servizio.

Di seguito è riportato un elenco non esaustivo di esempi di servizi noti esclusi.

* AddSearchBot
* AhrefsBot
* Applebot
* Chiedi a Jeeves ragno aziendale
* Bingbot
* Anteprima bing
* BLEXBot
* BuiltWith
* Bytespider
* CrawlerKengo
* Facebookexternalhit
* Google AdsBot
* Google AdsBot Mobile

### Perché il mio rapporto di Analytics mostra risultati diversi rispetto alle richieste di contenuto AEM? {#why-are-reports-different}

Le richieste di contenuto avranno varianze con gli strumenti di reporting di Analytics di un’organizzazione, come riepilogato in questa tabella.

| Motivo della varianza | Spiegazione |
|---|---|
| Assegnazione tag | Tutte le pagine tracciate come richieste di contenuto AEM possono o meno essere contrassegnate con il tracciamento di Analytics.<br>Tutte le chiamate API tracciate come richieste di contenuto AEM non saranno taggate dallo strumento Analytics di un&#39;organizzazione.<br>Le pagine o le chiamate API possono essere taggate per tenere traccia delle azioni invece che delle visualizzazioni. |
| Regole Tag Management | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che non sono stati pre-identificati e rimossi da AEM possono causare discrepanze nel tracciamento. |
| Suite per report | Le pagine che fanno parte della stessa istanza AEM e dello stesso dominio possono inviare dati a suite di rapporti Analytics diverse. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e scansione della sicurezza possono generare richieste di contenuto per AEM che non sono monitorate nei rapporti di Analytics. |
| Richieste di preacquisizione | L’utilizzo di un servizio di preacquisizione per precaricare le pagine per aumentare la velocità può causare un aumento significativo del traffico della richiesta di contenuto. |
| DDOS | Mentre Adobe fa ogni sforzo per rilevare e filtrare automaticamente il traffico dagli attacchi DDOS, non c&#39;è alcuna garanzia che tutti i possibili attacchi DDOS vengano rilevati. |

### Cosa succede se uso la mia rete CDN? {#using-own-cdn}

Il dashboard di richiesta del contenuto in Cloud Manager non mostrerà il tracciamento per il tuo CDN.
