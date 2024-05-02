---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 79dcf8a4e9834beeb466ed9270a3f5c6aa67aa9a
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 24%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 16145 {#release-16145}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 16145, rilasciata pubblicamente il giovedì 1 maggio 2024. La versione di manutenzione precedente era 15977.

Con l’attivazione delle funzioni 2024.4.0 viene fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-16145}

* ASSETS-23489: miglioramenti di informazioni sull’archivio.
* ASSETS-26926: miglioramenti al polling di caricamento di Dynamic Medie.
* ASSETS-30351: la finestra di dialogo per il download deve caricare le dimensioni del rendering di Dynamic Medie in modo asincrono.
* ASSETS-30379: migliora la risoluzione delle licenze DRM durante il download.
* ASSETS-31058: applica le rappresentazioni con ritaglio avanzato nell’interfaccia utente di AEM assets nella scheda delle rappresentazioni e genera immagini ritagliate automaticamente quando l’utente fa clic su di esse.
* ASSETS-31218: aggiungi il supporto per smartcrop denominato nell’api di consegna delle risorse.
* ASSETS-31979: aggiungi un indicatore visivo e disabilita le funzioni dell’interfaccia utente durante le operazioni di Async Assets.
* ASSETS-32735: miglioramenti all’evento di aggiornamento dei metadati delle risorse.
* ASSETS-34661: API per URL di anteprima e/o consegna DM da AEMaaCS Publish.
* ASSETS-37259: miglioramenti nell’analisi dell’XMP.
* ASSETS-37263: consenti l’annullamento di processi asincroni di Assets non riusciti.
* CNTBF-114: miglioramenti al flusso di ritorno dei contenuti.
* CNTBF-148: miglioramenti al flusso di ritorno dei contenuti.
* CQ-4356992: Ultime traduzioni per AEM e Granite.
* SITES-19326: aggiorna i collegamenti nell’interfaccia utente di Assets per aprire CF nel nuovo editor CF.
* SITES-20686: GraphQL - Espone l’URL di Dynamic Medie tramite _dmS7Url (per risorse non immagini).
* SKYOPS-68091: aggiornamento a Java 11.0.20.

### Problemi risolti {#fixed-issues-16145}

* ASSETS-32321: la risoluzione del flusso di lavoro di post-elaborazione non riesce se nella cartella predecessore manca il sottonodo &quot;jcr:content&quot;.
* ASSETS-33856: il predefinito per immagini JPEG scarica il file come TXT.
* ASSETS-34096: è stata corretta la vista dell’interfaccia utente touch per il rapporto sul download asincrono.
* ASSETS-34493: errore durante il caricamento della finestra di dialogo di download dopo l’attivazione della funzione per più società.
* ASSETS-34824: l’URL della copia risulta vuoto per le cartelle DM disabilitate.
* ASSETS-35226: il flusso di lavoro di post-elaborazione non è stato risolto se specificato nella directory principale DAM.
* ASSETS-35559: riduci il registro degli errori di caricamento batch DM a WARN.
* ASSETS-35860: conversione errata del fuso orario nella vista a colonne di AEM Assets.
* ASSETS-35935: navigazione errata nelle cartelle dopo la chiusura della revisione del payload.
* ASSETS-35961: il pulsante Aggiungi ritaglio non funziona nel profilo immagine.
* ASSETS-36227: disabilita il servizio FolderPreviewUpdaterImpl al momento della pubblicazione.
* ASSETS-36943: quando in una cartella nella vista a elenco sono presenti elementi CF e altri elementi non CF, non vengono allineate le colonne.
* ASSETS-36990: i processi di metadati esportati non riescono/sono lenti con un numero elevato di proprietà.
* ASSETS-37113: il processo Rielabora risorse termina immediatamente se la query restituisce solo risultati CF.
* ASSETS-37260: l’esportazione dei metadati nell’AEM può produrre un CSV non valido.
* ASSETS-37261: PPTx e PDF Annotation Problema su AEM Assets.
* ASSETS-37282: potenziale lentezza nella richiesta di apertura di una cartella di grandi dimensioni.
* ASSETS-37330: l&#39;importazione in blocco da OneDrive crea una struttura di cartelle AEM non corretta.
* ASSETS-37609: rimuovi la ricerca conf legacy scene7.
* ASSETS-38016: alcuni aggiornamenti dei metadati non vengono tracciati correttamente negli eventi.
* CQ-4357161: La schermata Payload casella in entrata AEM restituisce 404.
* GRANITE-50041: l’opzione Aggiungi rappresentazione non funziona se la risoluzione è superiore a 1440 px quando nel menu a discesa è presente solo l’opzione &quot;Aggiungi rappresentazione&quot;.
* GRANITE-50279: nomi delle settimane non ordinati nel componente Coral Datepicker.
* SCRNS-3949: il tempo della richiesta di recupero del canale degli schermi è troppo lungo.
* SCRNS-3981 [Canale sequenza] La schermata nera si verifica quando la sequenza degli eventi di caricamento/scaricamento dell’elemento viene distorta.
* SCRNS-4180 [Canale sequenza] La sequenza si interrompe con una schermata vuota per i canali con video di durata -1 al ripristino dalla miniatura di fallback.
* SCRNS-4245 [Canale sequenza] Durata limitata della schermata vuota quando un video viene caricato e cambiato dalla miniatura di fallback.
* SITES-16055: correggi i collegamenti alle origini Live Copy e Live Copy all’interno della rispettiva pagina delle proprietà.
* SCRNS-4243: pulsanti mancanti nel provider di contenuti per utenti non amministratori.

### Problemi noti {#known-issues-16145}

Nessuno.

### Funzioni e API obsolete {#deprecated-16145}

* [Credenziali JWT nella console Adobe Developer obsolete](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* A decorrere dal 1° maggio 2024, Adobe Dynamic Medie cesserà il supporto per i seguenti elementi:

   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 e 1.1
   * Le seguenti crittografie deboli in TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


Per sapere cosa è obsoleto o rimosso in AEM as a Cloud Service, vedi [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-16145}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.24.6 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
