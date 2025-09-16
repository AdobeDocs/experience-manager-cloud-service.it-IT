---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 24%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 22450 {#22450}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 22450, rilasciata al pubblico il mercoledì 16 settembre 2025. La versione di manutenzione precedente era la 22171.

Con la versione di attivazione funzioni 2025.9.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nuove funzioni {#new-features-22450}

* SITES-32595: ora è possibile identificare i flussi di lavoro completati con frammenti saltati o rifiutati. Nella risposta API del flusso di lavoro è disponibile una nuova proprietà che elenca i frammenti esclusi a causa di riferimenti non validi o non validi.
* SITES-33642: ora viene prodotto e utilizzato un nuovo evento API per i frammenti di contenuto modificati.
* SITES-33320: ora è possibile cercare un modello per frammenti di contenuto utilizzando il suo `technicalName` tramite l’API di ricerca.

### Miglioramenti {#enhancements-22450}

* SITES-34023: il campo `technicalName` è stato aggiunto alle risposte degli endpoint del modello per frammenti di contenuto per una migliore identificazione.
* SITES-32766: i riferimenti alle risorse di contenuto nei modelli per frammenti di contenuto ora supportano una più ampia gamma di tipi di file binari.
* SITES-33974: è stata migliorata la documentazione OpenAPI, rendendola più precisa e intuitiva.
* SITES-9173: Cache `ContentPolicyStatus`.
* SITES-9290: miglioramento della memorizzazione nella cache di `TouchEditContext`.
* SITES-33355: Apri un nuovo editor CF su &quot;Visualizza payload&quot; nella console del flusso di lavoro.
* SITES-33356: Apri un nuovo editor CF su Crea → CF Apri nell’interfaccia utente di amministrazione dell’interfaccia utente touch.
* SITES-32952: gestione incoerente dei valori predefiniti per i campi CFM quando si utilizza l’API di consegna.
* SITES-31539: Edge Delivery con Universal Editor: aggiunta del supporto per i metatag di configurazione di Universal Editor in `head.html`.
* SITES-20672: Edge Delivery con Universal Editor: aggiunta del supporto per fogli di calcolo aggiuntivi per metadati in blocco nell’authoring.
* SITES-32963: Edge Delivery con Universal Editor: aggiungi nuovi metadati di sperimentazione per il target di ottimizzazione, l’allocazione automatica e l’apprendimento automatico.
* SITES-30847: versione dei Componenti core 2.30.0.
* SITES-29617: l’endpoint referencedBy è stato aggiornato per utilizzare la classe ReferenceSearch, migliorandone le prestazioni e l’affidabilità.
* SITES-19308: sono state migliorate le prestazioni del processo di eliminazione delle pagine ottimizzando il passaggio di convalida dei riferimenti.
* SITES-34293: è stato implementato il caricamento lento per le risorse basate su modelli per migliorare le prestazioni.
* SITES-33892: aggiunta di una funzione per saltare i controlli di riferimento per le pseudo-pagine, che possono migliorare le prestazioni.

### Problemi risolti {#fixed-issues-22450}

* CQ-4360550: è stata corretta la scomparsa imprevista della copia in lingua dopo il ripristino dello spostamento della pagina in AEM Cloud Service.
* SITES-25232: i collegamenti Imposta data e Esci da Timewarp non hanno un indicatore visibile di stato attivo.
* SITES-25258: lo stato attivo non viene gestito con la finestra di dialogo modale Elimina annotazione.
* SITES-25305: la barra degli strumenti Demografia non riceve lo stato attivo in ordine logico.
* SITES-25366: lo stato di caricamento della modale del teaser non viene annunciato dallo screen reader.
* SITES-34276: Edge Delivery con Universal Editor: correggi i criteri CORS creati automaticamente non applicati al livello di pubblicazione.
* SITES-34811: Edge Delivery con Universal Editor: correggi il fatto che il selettore hlx non venga aggiunto ai collegamenti ai fogli di calcolo durante l’authoring.
* SITES-31669: Stringhe non localizzate &quot;Questa pagina viene reindirizzata a&quot; in Strumenti > Siti > Lanci.
* SITES-30879: Stringhe non localizzate in Sites > Editor pagina > Componente di ricerca.
* SITES-30959: Stringhe non localizzate nel componente Editor pagina > Immagine.
* SITES-21743: Unlocalizzato &quot;Selezionare un documento da visualizzare&quot;. stringa in Editor pagina > Visualizzatore PDF
* SITES-19785: le stringhe non sono localizzate in Componenti core, sito > Schede.
* SITES-22059: stringa &quot;File preview not available&quot; non localizzata in Componenti core sito > Visualizzatore PDF.
* SITES-33360: &quot;Errore durante l’operazione. Il percorso fornito non è una stringa &quot;launch&quot; in Lanci > Modifica.
* SITES-32975: Formato data non localizzato nell’interfaccia utente headless > Avvii > Confronta lancio con Source.
* SITES-32973: Stringhe codificate nell’interfaccia utente headless > Lanci > Rebase.
* SITES-13540: Stringhe non localizzate in Lanci > Promozione.
* SITES-13085: stringhe di errore non localizzate nella pagina Sites > Launch creation (Creazione del lancio).
* SITES-21499: la stringa non localizzata è Sites > Lanci > Modifica.
* SITES-14961: troncamento del campo data nella finestra di dialogo Sites > Proprietà > Blueprint > Rollout.
* SITES-33764: i filtri di avvio (Percorso Source / Avvii creati dal flusso di lavoro) non funzionano.
* SITES-33884: &quot;Promuovi la pagina corrente e le sottopagine&quot; promuove involontariamente le pagine al di fuori dell’ambito.
* SITES-33611: la panoramica Live Copy non funziona per i mercati con volumi elevati.
* SITES-34331: Timeout 503 durante il caricamento della sovrapposizione di rollout per utenti non amministratori.
* SITES-34403: `NullPointerException` in `GraphqlClientImpl deactivate()` durante l&#39;arresto.
* SITES-33817: sono stati risolti dei problemi di sincronizzazione tra lo schema dell’interfaccia utente e il modello JCR per garantire la coerenza.
* SITES-31141: I riferimenti ai contenuti che non sono rappresentati dal percorso ora vengono restituiti correttamente nella risposta API.
* SITES-34080: Il processo di creazione dei frammenti di contenuto è ora più solido e non avrà esito negativo se non vengono forniti campi alla richiesta.
* SITES-30773: L’espressione regolare per trovare parole utilizzando &quot;Trova e sostituisci&quot; è stata migliorata per corrispondere correttamente ai caratteri UTF-8.
* SITES-33742: è stato risolto un bug che impediva lo spostamento corretto di un frammento di contenuto quando si utilizzava l’API del flusso di lavoro.

### Problemi noti {#known-issues-22450}

Nessuna.

### Funzioni e API obsolete {#deprecated-22450}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-22450}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 18 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-22450}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.84.0 | [API Oak API 1.84.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
