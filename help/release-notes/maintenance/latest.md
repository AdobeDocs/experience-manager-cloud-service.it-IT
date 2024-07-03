---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 20%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 16971 {#release-16971}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 16971, rilasciata pubblicamente l’giovedì 3 luglio 2024. La versione di manutenzione precedente era 16799.

Con la versione di attivazione funzioni 2024.7.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-16971}

* SITES-22948: rimuovi i riferimenti commerce nel contenuto di base per AEM CS.
* SITES-22141: [Frammenti di contenuto] SegmentNotFoundException da CFM ModelChangeRepositoryImpl dopo OnRC.
* SITES-21893: Problema di ritaglio immagine nell’istanza di authoring.
* SITES-21788: [Frammenti di contenuto] Visualizzare NOTE nell&#39;editor di modelli CF e CF quando uiSchema è abilitato per il modello.
* SITES-21688: il rollout di MSM non aggiorna il percorso del frammento di esperienza (XF) sulle pagine Live Copy.
* SITES-21659: restituisce il nome completo dell’utente che crea, modifica o replica una risorsa modello.
* SITES-21609: Endpoint OpenAPI per migrare frammenti di contenuto da un modello all’altro.
* SITES-21598: [Apri API] Crea CFM: errore restituito se il percorso di configurazione specificato non esiste.
* SITES-21491: [Apri API] L’endpoint CF PATCH deve rispettare le relazioni live a livello di campo.
* SITES-21434: [Apri API] L’endpoint del GET CF deve rispettare le relazioni live a livello di campo.
* SITES-21415: CF Editor - supporta riferimenti UUID.
* SITES-21326: [Apri API] Fornisci informazioni sulla presenza di riferimenti per un frammento di contenuto.
* SITES-21310: [Apri API] Aggiungi l’ID del frammento di contenuto nella risposta API per le traduzioni.
* SITES-20859: CF Open API - Restituisce i riferimenti durante il recupero di un frammento in base al percorso.
* SITES-20687: [Apri API] Endpoint per il recupero dello stato di elaborazione batch.
* SITES-20657: [Apri API] Fornisci l’opzione per match parola intera quando sostituisci una stringa utilizzando `FindAndReplace` endpoint.
* SITES-20587: [Apri API] Crea `COPY` endpoint per frammenti di contenuto.
* SITES-20584: [Apri API] Ottimizza il recupero dei riferimenti.
* SITES-20308: [Apri API] Abilita l’elaborazione batch nell’API.
* SITES-19976: [Apri API] Schema generico dell’interfaccia utente per i campi condizionali.
* SITES-19556: [Frammenti di contenuto] Aggiorna uiSchema se esiste quando il modello viene modificato.
* SITES-18056: [Apri API] Quando pubblichi un frammento di contenuto in Anteprima, includi i riferimenti.
* SITES-16898: [Schema] Endpoint OpenAPI per migrare i frammenti di contenuto da un modello all’altro.
* SITES-16609: Endpoint elenco lanci.
* SITES-16606: Creare un endpoint per Launch.
* SITES-21617: [Xwalk] Rendi modificabili le proprietà o i metadati della pagina in UE.
* SITES-19614: [Xwalk] Paginazione dell’editor di fogli di calcolo e scorrimento infinito.
* SITES-22163: [Xwalk] È stato migliorato il supporto per i contenuti distribuiti dal livello di pubblicazione per Edge Delivery Sites.
* SITES-22109: [Xwalk] È stata migliorata la gestione del post-elaborazione del markup richtext.
* SITES-22035: [Xwalk] Gestione migliorata di MSM e Launches.
* SITES-21839: [Xwalk] Mappatura del percorso e bonifica migliorate per i contenuti non gestiti da Edge Delivery.

### Problemi risolti {#fixed-issues-16971}

* CQ-4356898: [Traduzione] Errore outOfMemory per CF che contiene un numero insolitamente elevato di collegamenti.
* CQ-4357055: [Traduzione] La traduzione automatica non funziona con l’API REST.
* CQ-4353931: [Traduzione] Aggiungi jcr:uuid nella pagina sorgente di traduzione/xf/risorsa quando manca.
* CQ-4357591: [Traduzione] Modifica il flusso di lavoro &quot;Associa JCR:UUID&quot; in modo che funzioni per Pages/XF.
* FORMS-14844: Forms adattivo consente l’invio di moduli nonostante la verifica reCAPTCHA non riesca.
* FORMS-14984: Forms con CAPTCHA salta la convalida se &quot;submitMetaData&quot; è assente nei dati inviati.
* FORMS-14477: le opzioni &quot;È dopo&quot; e &quot;È prima&quot; nell’editor delle regole non funzionano correttamente nella convalida del selettore data.
* FORMS-14019: la funzionalità &quot;Invoke Service&quot; dell’editor di regole non funziona in Universal Editor.
* FORMS-14336: quando non è selezionato alcun campo modulo, l’editor deve aprirsi con lo stato attivo sull’intero elemento modulo.
* FORMS-15061: il cerchio del caricatore persiste a tempo indefinito quando si utilizza l’opzione richiama il servizio nell’editor di regole.
* SITES-22457: la promozione di un lancio non profondo non comporta l’aggiornamento del contenuto sorgente.
* SITES-22748: [Frammenti di contenuto] Migliorare la gestione degli errori per il processo di aggiornamento dei frammenti di contenuto
* SITES-22349: [Frammenti di contenuto] Impossibile modificare ContentType per elementi cf multilinea vuoti.
* SITES-22343: [Frammenti di contenuto] Il tipo semantico &quot;enumerazione&quot; è interrotto.
* SITES-22194: dopo aver impostato il reindirizzamento, model.json non funziona più.
* SITES-21953: [Apri API] Etag viene modificato in base all&#39;ordine di validationStatus.
* SITES-21894: [Apri API] Miglioramento della convalida del percorso padre durante la creazione di CF.
* SITES-21887: [Apri API] ETag non valido restituito dall&#39;endpoint delle varianti POST.
* SITES-21657: [Apri API] Migliora la convalida della proprietà Percorso di ricerca CF.
* SITES-21949: Il cursore non valido nelle API di ricerca restituisce 500.
* SITES-20927: quando la query non è presente, le API di ricerca restituiscono il valore 500.
* SITES-20544: [Apri API] Modifica la generazione dei nomi dei pacchetti di pubblicazione per evitare conflitti oak.
* SITES-19710: CVE-2022-47937 - Rimuovi tutti gli utilizzi di org.apache.sling.commons.json dall’Editor pagina.
* SITES-11992: [Accessibilità] Il pulsante di selezione del campione dell’annotazione non contiene un nome accessibile.
* SITES-10979: [Accessibilità] Etichetta non permanente.
* SITES-10962: [Accessibilità] Pulsante: il pulsante non ha un ruolo.
* SITES-10905: [Accessibilità] Lo stato del componente attivo non dispone di un rapporto di contrasto da 3 a 1.
* SITES-2974:  [Accessibilità] - Scorrimento orizzontale a una larghezza di 320 px.
* SITES-22026: Impossibile spostare frammenti di esperienza tra cartelle in AEM
* SITES-22106: Problema relativo alla funzionalità di cambio lingua nel nuovo editor di frammenti di contenuto
* SITES-21980: gestione incoerente per i tipi di riferimento basati su UUID.
* SITES-7257: NPE in ThumbnailServlet.

### Problemi noti {#known-issues-16971}

Nessuno.

### Notifica di modifica {#change-notice-16971}

* A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-16971}

Per sapere cosa è obsoleto o è stato rimosso in AEM as a Cloud Service, consulta [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-16971}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak API 1.64.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
