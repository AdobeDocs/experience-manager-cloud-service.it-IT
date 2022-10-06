---
title: Dashboard della licenza
description: Cloud Manager fornisce una dashboard per visualizzare facilmente le adesioni ai prodotti AEMaaCS disponibili per la tua organizzazione o tenant.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: b5078c849c9fa088546f5df1fcbef1dec59f3cdb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Dashboard della licenza {#license-dashboard}

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

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella pagina di panoramica dei prodotti , passa alla pagina **Licenza** scheda .

![Dashboard della licenza](assets/license-dashboard.png)

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

Viene conteggiata una richiesta di contenuto per ogni visualizzazione di pagina o per ogni cinque chiamate API, misurate in base all’ingresso del primo sistema di memorizzazione in cache che riceve una richiesta di contenuto. Le richieste di contenuto vengono conteggiate solo per gli ambienti di produzione.

Le richieste di contenuto escludono le richieste o le attività avviate da o per conto dell’Adobe al solo scopo di fornire prodotti e servizi. Sono esclusi anche il traffico di agenti utente identificati da Adobi da bot, crawler e spider relativi a motori di ricerca comuni e servizi di social media.

### In che modo Adobe Experience Manager misura le richieste di contenuto? {#how-are-content-requests-measured}

Le richieste di contenuto vengono tracciate sui server perimetrali AEM as a Cloud Service. Il traffico di origine non viene conteggiato per le richieste di contenuto. La CDN integrata in AEM as a Cloud Service traccia le richieste HTML e JSON valide.

AEM inoltre ha delle regole per escludere bot ben noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare il loro indice di ricerca o servizio.

### Perché il mio rapporto di Analytics mostra risultati diversi rispetto alle richieste di contenuto AEM? {#why-are-reports-different}

Le richieste di contenuto avranno varianze con gli strumenti di reporting di Analytics di un&#39;organizzazione, come riepilogato in questa tabella.

| Motivo della varianza | Spiegazione |
|---|---|
| Assegnazione tag | Tutte le pagine tracciate come richieste di contenuto AEM possono o meno essere contrassegnate con il tracciamento di Analytics. Tutte le chiamate API tracciate come richieste di contenuto AEM non saranno taggate dallo strumento Analytics di un&#39;organizzazione.<br>Le pagine o le chiamate API possono essere taggate per tenere traccia delle azioni o solo delle visualizzazioni di pagina univoche invece di tutte le visualizzazioni. |
| Regole Tag Management | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che non sono stati pre-identificati e rimossi da AEM possono causare discrepanze nel tracciamento. |
| Suite per report | Le pagine che fanno parte della stessa istanza AEM e dello stesso dominio possono inviare dati a suite di rapporti Analytics diverse. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e scansione della sicurezza possono generare richieste di contenuto per AEM che non sono monitorate nei rapporti di Analytics. |
| Richieste di preacquisizione | L’utilizzo di un servizio di preacquisizione per precaricare le pagine per aumentare la velocità può causare un aumento significativo del traffico della richiesta di contenuto. |
| DDOS | Sebbene l&#39;Adobe faccia ogni sforzo per rilevare e filtrare automaticamente il traffico dagli attacchi DDOS, non c&#39;è alcuna garanzia che tutti i possibili attacchi DDOS vengano rilevati |
| Blocchi di traffico | L&#39;utilizzo di un tracker blocker in un browser può negare il tracciamento di alcune richieste. |
| Firewall | I firewall possono bloccare il tracciamento di Analytics. Ciò è più frequente con i firewall aziendali. |

### Cosa succede se voglio saperne di più sul volume di richiesta del contenuto? {#current-request-volumes}

Se desideri ulteriori informazioni sul volume di richiesta del contenuto visualizzato nel dashboard della licenza, il team di Adobe può fornire un rapporto che mostra i principali driver di volume delle richieste di contenuto. Rivolgiti al tuo team di Adobe o all’Assistenza clienti Adobe per richiedere un rapporto sull’utilizzo principale.

### Cosa succede se uso la mia rete CDN? {#using-own-cdn}

Il Dashboard licenze mostrerà solo i dati tracciati dal CDN del Cloud Service.  Se scegli di portare il tuo CDN (BYOCDN), segnalerai il volume della richiesta di contenuti all&#39;Adobe su base annuale, come indicato nel tuo contratto.
