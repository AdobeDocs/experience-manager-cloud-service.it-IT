---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 636183e0597bed24b3e437ed53a35c9e64ac0504
workflow-type: ht
source-wordcount: '950'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 19352 {#19352}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 19352, rilasciata pubblicamente il 5 febbraio 2025. La versione di manutenzione precedente era la 19149.

Con la versione di attivazione funzioni 2025.2.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-19352}

* FORMS-13998: aggiunta del componente Pannello a soffietto.
* FORMS-17913: aggiunta di una variante di schede per il gruppo pulsanti di scelta.
* FORMS-17333: abilitazione dei modelli e-mail di HTML nell’invio del modulo AEM.
* FORMS-17702: abilitazione del caricamento nell’archiviazione BLOB di Azure dei PDF generati nelle API di sincronizzazione dell’output.
* SITES-28282: Edge Delivery con editor universale: è stato fornito il percorso di base, il nome del sito e l’organizzazione come informazioni di pagina per qualsiasi pagina.
* SITES-27055: Edge Delivery con editor universale: supporto dei parametri di query nel servlet proxy inverso.
* SITES-26796: Edge Delivery con editor universale: supporto delle colonne personalizzate per il foglio di calcolo Tassonomia.
* SITES-26087: Edge Delivery con editor universale: supporto dell’esportazione CSV per i fogli di calcolo.
* SITES-26265: Edge Delivery con editor universale: visualizzazione dell’account TA da integrare con Edge Delivery nell’interfaccia utente di configurazione.
* SITES-20372: Edge Delivery con editor universale: abilitazione dei casi d’uso MSM di base per i fogli di calcolo.
* SITES-26681: Edge Delivery con editor universale: supporto del parametro ?sheet= per i fogli di calcolo di tassonomia dell’autore.
* SITES-26479: endpoint per lo stato della pubblicazione pianificata del modello per frammento di contenuto dello [schema].
* SITES-25944: [Panoramica Live Copy] aggiunta dello stato “Live Copy aggiornata con ereditarietà limitata”.
* SITES-28713: [V2] aggiunta del supporto per dati strutturati allo scraper dei contenuti.
* SITES-27896: apertura automatica della scheda Commenti alla notifica.
* SITES-26720: all’utente non deve essere consentita la selezione di un’intera raccolta dal selettore delle risorse.
* SITES-27875: tutti gli elementi modificabili all’interno di un contenitore sono resi mobili per impostazione predefinita.
* SITES-28340: plug-in del servizio dell’editor universale Dark Alley.
* SITES-26098: possibilità di evitare la pubblicazione di pagine a cui si fa riferimento durante la pubblicazione di un frammento di contenuto.
* SITES-27789: supporto dell’attributo dati data-aue-component nel DOM.
* SITES-25997: miglioramento delle varianti per il supporto della data di modifica.
* SITES-28023: output GraphQL per riferimenti a risorse remote (archivio + ID risorsa).
* SITES-26058: endpoint per lo stato della pubblicazione pianificata del modello per frammento di contenuto.
* SITES-25108: migrazione del modello per riferimenti UUID.
* SITES-26630: endpoint per lo stato della pubblicazione pianificata del frammento di contenuto per frammenti di contenuto multipli.
* SITES-23432: miglioramento della funzionalità di eliminazione dei riferimenti.
* SITES-25797: supporto per riferimenti a risorse esterne - GraphQL.
* SITES-17514: eliminazione del miglioramento dell’endpoint per annullare la pubblicazione di un frammento di contenuto.
* SITES-14633: convalida dei payload di creazione del modello per il frammento di contenuto prima dell’installazione - Prova.

### Problemi risolti {#fixed-issues-19352}

* CQ-4356756: il supporto per le risorse correlate non viene tradotto.
* CQ-4358206: il modulo di pianificazione per Ripeti traduzione non funziona per i progetti di traduzione.
* CQ-4358126: la sottocartella di configurazione nel servizio cloud di traduzione non può essere selezionata.
* FORMS-18098, FORMS-17954: i moduli adattivi non vengono caricati in modalità Internet Explorer nel browser Microsoft Edge.
* FORMS-17162: la pubblicazione di una risorsa comporta l’esecuzione di query OOTB che riducono le prestazioni di pubblicazione.
* SITES-28415: Edge Delivery con editor universale: correzione del pulsante Apri proprietà per fogli di calcolo.
* SITES-26669: Edge Delivery con editor universale: correzione dei problemi presenti durante il caricamento di file CSV codificati in UTF-8 con BOM come foglio di calcolo.
* SITES-26543: Edge Delivery con editor universale: correzione dei blocchi vuoti senza che un modello riproduca un markup errato.
* SITES-26857: Edge Delivery con editor universale: correzione del token di autenticazione del sito visibile nell’interfaccia utente per le configurazioni basate su file.
* SITES-26662: Edge Delivery con editor universale: risolti i problemi relativi ai metadati in blocco per la distinzione tra maiuscole e minuscole.
* SITES-28133: la pubblicazione in “Anteprima” causa la disponibilità del contenuto in Produzione.
* SITES-27187: attivazione pagina/risorsa pianificata, inclusi riferimenti (sperimentali) mancanti per la pubblicazione dei riferimenti.
* SITES-27264: 2 test Selenium correlati alla creazione della Live Copy del frammento di contenuto falliscono in modo costante nel master.
* SITES-26559: aggiunta della query per i modelli di frammento di contenuto all’indice cqPageLucene.
* SITES-24469: l’elemento interattivo non è accessibile da tastiera.
* SITES-24518: i pulsanti Nome e Modello nella tabella Riferimento principale non sono accessibili da tastiera.
* SITES-27937: dopo l’aggiornamento del modello, i vincoli UISchema vengono impostati su null.
* SITES-27852: categorizzazioni mancanti nel modello UISchema.
* SITES-27904: MetadataSchema mancante nell’elenco/ricerca Modelli per frammenti di contenuto per la proiezione completa.
* SITES-26827: l’elenco di frammenti termina in un ciclo infinito.
* SITES-27678: [Prestazioni] impedimento del recupero non necessario dei _references.
* SITES-27589: errore di aggiornamento UUID per modelli di frammento di contenuto con più campi di riferimento a contenuto/frammento.
* SITES-26679: i modelli di frammento di contenuto con annullamento della pubblicazione devono convalidare solo i riferimenti pubblicati.
* SITES-26666: referencesTree e endpoint di riferimento restituiscono risultati diversi.
* SITES-26499: l’ordine errato del valore del campo tag nei frammenti di GET e in PATCH randomizza l’ordine.
* SITES-26585: correzione di un piccolo errore di descrizione nello schema.
* SITES-26647: la convalida dell’eliminazione dell’endpoint e del riferimento UnpublishFragments può non riuscire per gli utenti non amministratori.
* SITES-26458: [Cerca modello per frammento di contenuto] Correzione del filtro per stato di replica.
* SITES-23513: [Editor modello per frammenti di contenuto] La convalida non riesce per la proprietà “Riferimento frammento” - “Modello per frammenti di contenuto consentiti”.
* SITES-26575: l’annullamento della pubblicazione di un frammento in anteprima deve aggiornare previewStatus.
* SITES-26571: i riferimenti di pagina non possono essere salvati se FT_SITES-12435 è abilitato.
* SITES-26660: il confronto tra versioni dei frammenti di contenuto può essere interrotto se il @ContentType è di tipo “stringa”.
* SITES-26626: CustomErrorMessage mancante nei campi numerici e booleani.
* SITES-26268: durante la creazione di un frammento, se un riferimento non è valido viene restituito un codice di stato di errore.

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
