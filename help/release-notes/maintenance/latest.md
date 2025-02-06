---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f7aa50d8a2fa80489c56571caa9a75bc50715368
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 21%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 19352 {#19352}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 19352, rilasciata pubblicamente il giovedì 5 febbraio 2025. La versione di manutenzione precedente era la 19149.

Con la versione di attivazione funzioni 2025.2.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-19352}

* FORMS-13998: Aggiungi componente Pannello a soffietto.
* FORMS-17913: Aggiungi variante schede per gruppo pulsanti di scelta.
* FORMS-17333: Abilitazione dei modelli e-mail di HTML nell’invio del modulo AEM.
* FORMS-17702: abilita il caricamento nell’archiviazione BLOB di Azure dei PDF generati nelle API di sincronizzazione dell’output.
* SITES-28282: Edge Delivery con Universal Editor: fornisce il percorso di base, il nome del sito e l’organizzazione come informazioni pagina per qualsiasi pagina.
* SITES-27055: Edge Delivery con Universal Editor: supporta i parametri di query nel servlet proxy inverso.
* SITES-26796: Edge Delivery con Universal Editor: supporta colonne personalizzate per il foglio di calcolo Tassonomia.
* SITES-26087: Edge Delivery con Universal Editor: supportano l’esportazione CSV per i fogli di calcolo.
* SITES-26265: Edge Delivery con Universal Editor: visualizza l’account TA da integrare con Edge Delivery nell’interfaccia utente di configurazione.
* SITES-20372: Edge Delivery con Universal Editor: abilita casi d’uso MSM di base per i fogli di calcolo.
* SITES-26681: Edge Delivery con Universal Editor: supporta il parametro ?sheet= per i fogli di calcolo di tassonomia dell’autore.
* SITES-26479: [Schema] Endpoint di stato della pubblicazione pianificata per il modello di frammento di contenuto.
* SITES-25944: [Panoramica Live Copy] aggiungi lo stato &quot;Live Copy aggiornata con ereditarietà limitata&quot;.
* SITES-28713: [V2] Aggiungi il supporto per dati strutturati allo scraper del contenuto.
* SITES-27896: CommentsTab si apre automaticamente alla notifica.
* SITES-26720: l’utente non deve essere autorizzato a selezionare un’intera raccolta dal selettore delle risorse.
* SITES-27875: per impostazione predefinita, rende spostabili tutte le modifiche all’interno di un contenitore.
* SITES-28340: Plug-in del servizio Universal Editor di Dark Alley.
* SITES-26098: possibilità di evitare la pubblicazione di pagine a cui si fa riferimento durante la pubblicazione di un frammento di contenuto.
* SITES-27789: supporto di data attribute data-aue-component nel DOM.
* SITES-25997: migliora le varianti per supportare la data di modifica.
* SITES-28023: output GraphQL per riferimenti a risorse remote (archivio + ID risorsa).
* SITES-26058: Endpoint per lo stato della pubblicazione pianificata del modello per frammenti di contenuto.
* SITES-25108: Migrazione del modello per riferimenti UUID.
* SITES-26630: Endpoint di stato pubblicazione pianificata per frammenti di contenuto multiplo.
* SITES-23432: Migliora la funzionalità di eliminazione dei riferimenti.
* SITES-25797: Supporto per riferimenti a risorse esterne - GraphQL.
* SITES-17514: miglioramento dell’eliminazione dell’endpoint per annullare la pubblicazione di Frammento di contenuto.
* SITES-14633: Convalidare il modello per frammenti di contenuto creare payload prima dell’installazione - Dry Run.

### Problemi risolti {#fixed-issues-19352}

* SITES-28415: Edge Delivery con Universal Editor: Correggi pulsante Apri proprietà per fogli di calcolo.
* SITES-26669: Edge Delivery con Universal Editor: Correggi i problemi durante il caricamento di file CSV codificati in UTF-8 con una distinta base come foglio di calcolo.
* SITES-26543: Edge Delivery con Universal Editor: Correggi i blocchi vuoti senza che un modello riproduca un markup errato.
* SITES-26857: Edge Delivery con Universal Editor: correggi il token di autenticazione del sito che è visibile nell’interfaccia utente per le configurazioni basate su file.
* SITES-26662: Edge Delivery con Universal Editor: risolvere i problemi relativi ai metadati in blocco sensibili a maiuscole e minuscole.
* SITES-28133: da Publish a &quot;Anteprima&quot; i contenuti sono disponibili in produzione.
* SITES-27187: Attivazione pagina/risorsa pianificata, inclusi riferimenti (sperimentali) mancanti per la pubblicazione dei riferimenti.
* SITES-27264: 2 i test Selenium correlati a Content-Fragment-LiveCopy-Creation hanno esito negativo in modo coerente sulla pagina mastro.
* SITES-26559: aggiungi la query per i modelli Content-Fragment all’indice cqPageLucene.
* SITES-24469: l’elemento interattivo non è accessibile da tastiera.
* SITES-24518: i pulsanti Nome e Modello nella tabella Riferimento padre non sono accessibili da tastiera.
* SITES-27937: dopo l’aggiornamento del modello, i vincoli UISchema vengono impostati su null.
* SITES-27852: Categorizzazioni mancanti nel modello UISchema.
* SITES-27904: MetadataSchema mancante nell’elenco/ricerca Modelli per frammenti di contenuto per la proiezione completa.
* SITES-26827: Elenco di frammenti finisce in un ciclo infinito.
* SITES-27678: [Prestazioni] Impedisci il recupero non necessario dei _riferimenti.
* SITES-27589: errore di aggiornamento UUID per modelli di frammenti di contenuto con più campi di riferimento a contenuto/frammento.
* SITES-26679: i modelli per frammenti di contenuto di annullamento della pubblicazione devono convalidare solo i riferimenti pubblicati.
* SITES-26666: referencesTree e il punto finale di riferimento restituiscono con risultati diversi.
* SITES-26499: Ordine errato del valore del campo tag nei frammenti di GET e in PATCH.
* SITES-26585: correggi un piccolo errore di descrizione nello schema.
* SITES-26647: la convalida dell’eliminazione dell’endpoint e del riferimento UnpublishFragments può non riuscire per gli utenti non amministratori.
* SITES-26458: [Cerca modello per frammenti di contenuto] Correggi il filtro in base allo stato di replica.
* SITES-23513: [La convalida dell&#39;Editor modello per frammenti di contenuto] non riesce per la proprietà &quot;Riferimento frammento&quot; - &quot;Modello per frammenti di contenuto consentiti&quot;.
* SITES-26575: l’annullamento della pubblicazione di un frammento da preview dovrebbe aggiornare previewStatus.
* SITES-26571: i riferimenti di pagina non possono essere salvati se FT_SITES-12435 è abilitato.
* SITES-26660: il confronto delle versioni dei frammenti di contenuto potrebbe essere interrotto se il @ContentType è di tipo &quot;stringa&quot;.
* SITES-26626: CustomErrorMessage mancante nei campi numerici e booleani.
* SITES-26268: Se durante la creazione di un frammento viene restituito un codice di stato errato, viene restituito un riferimento non valido.
* FORMS-18098, FORMS-17954: impossibile caricare Forms adattivo in modalità Internet Explorer nel browser Microsoft Edge.
* FORMS-17162: la pubblicazione di una risorsa comporta l’esecuzione di query OOTB che riducono le prestazioni di pubblicazione.

### Problemi noti {#known-issues-19352}

Nessuno.

### Funzioni e API obsolete {#deprecated-19352}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-19352}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 36 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-19352}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
