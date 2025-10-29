---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9d081b468e42306c56238bee6117d92c6afd48d4
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 25%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 23122 {#23122}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 23122, rilasciata pubblicamente il giovedì 29 ottobre 2025. La versione di manutenzione precedente era la 22943.

Con la versione di attivazione funzioni 2025.11.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-23122}

* FORMS-21594: Abilita il blocco di contenuti e layout dei modelli di comunicazione interattiva per gli autori di contenuti.
* FORMS-20385: supporta l’editing XDP nell’editor di comunicazioni interattive.
* FORMS-10883: supporto per JSON con tag dello spazio dei nomi XHTML nella generazione DoR per garantire un rendering accurato dei dati in formato Rich Text inviati tramite API.
* FORMS-21751: Funzioni area di lavoro - Overflow del testo, interfaccia utente per interruzione pagina.
* FORMS-22049: Editor di comunicazioni interattive - Migrazione a Spectrum 2.
* FORMS-22050: supporto per la numerazione dinamica delle pagine nell&#39;editor di comunicazioni interattive.
* FORMS-21606: SPI di rendering OSGi pubblici per comunicazioni interattive.
* FORMS-21613: generazione di rapporti sulle transazioni e registrazione delle prestazioni per gli SPI di comunicazione interattiva di rendering.
* SITES-35092: Frammenti di contenuto - Nuova procedura di mixaggio e aggiornamento per la ricerca semantica.
* SITES-32319: Delivery OpenAPI - Riferimenti alla pagina di supporto.
* SITES-20123: GraphQL: supporta gli elementi in apice nella risposta JSON.
* SITES-34744: nuova proprietà &quot;card&quot; nella risposta Frammento di contenuto che contiene dati che può essere utilizzata per il rendering di una miniatura.
* SITES-34571: consenti che i campi di enumerazione siano vuoti.
* SITES-34812: è stata aggiunta la possibilità di recuperare un frammento di contenuto senza i relativi riferimenti, utilizzando il parametro &quot;references&quot; con il valore &quot;none&quot;.
* SITES-35176: Il Check-Out di un frammento di contenuto tramite l’interfaccia utente touch ora impedisce ad altri utenti di modificare il frammento di contenuto nel nuovo editor.
* SITES-30371: è stato aggiunto il supporto per campi di riferimento basati su UUID.
* SITES-19309: recupera un massimo di 150 riferimenti all’apertura della procedura guidata Sposta pagina.
* SITES-32515: Edge Delivery con Universal Editor - Aggiunta del supporto per più campi e più campi compositi (accesso anticipato).
* SITES-33784: Edge Delivery con Universal Editor - Aggiunta del supporto per ld-json nei metadati della pagina.
* SITES-34832: Edge Delivery con Universal Editor - Aggiungi il percorso pubblico di una pagina alla risposta del servlet di informazioni pagina.
* SITES-25893: Edge Delivery con Universal Editor - È stato aggiunto il supporto per il rendering di testo con caratteristiche avanzate ed enfasi nei blocchi.
* SITES-26158: Edge Delivery con Universal Editor - Aggiunta del supporto per il markup delle tabelle in blocchi e colonne (accesso anticipato).
* SITES-27949: Edge Delivery con Universal Editor - Rende facoltativa la mappatura del percorso.

### Problemi risolti {#fixed-issues-23122}

* CQ-4361144: è stato corretto ignorare i frammenti di contenuto dai processi di traduzione.
* CQ-4355446: è stata corretta la stringa non localizzata nel progetto di traduzione che si verificava nella finestra di dialogo Annulla processo di traduzione.
* SITES-34555: GraphQL - QueryValidationError dopo le distribuzioni.
* SITES-35077: Frammenti di contenuto - L’annullamento della pubblicazione non riesce per i frammenti con parentesi a causa di una codifica URL errata.
* SITES-35374: Frammenti Di Contenuto - Il Frammento Di Contenuto Modificato Scompare Dopo Essere Tornato Indietro.
* SITES-36130: NPE in `EditorRestrictionsStatusImpl`.
* SITES-35810: NullPointerException in Launches blocca la coda publishEdgeDeliverySubscriber.
* SITES-34368: AEM CIF genera 12 alias GraphQL e supera il limite di 10 di Magento 2.4.6-P12.
* SITES-36193: Correzioni al connettore CCS.
* SITES-35169: è stato risolto un problema che causava un’impaginazione errata quando la ricerca restituiva risorse di frammenti non valide.
* SITES-34574: è stato corretto un problema a causa del quale, in alcuni casi, il cursore non veniva restituito dall’API di ricerca per frammenti di contenuto.
* SITES-35520: è stato risolto un problema che causava ClassCastException o timeout durante il tentativo di pubblicazione del contenuto.
* SITES-35210: è stata corretta un’eccezione NullPointerException che si verificava durante il tentativo di pubblicare un frammento interrotto con un filtro dei riferimenti vuoto.
* SITES-35933: è stato corretto un bug a causa del quale venivano attivati flussi di lavoro vuoti &quot;Richiesta di attivazione&quot; dopo la pubblicazione del frammento di contenuto.
* SITES-35925: è stato corretto un bug correlato all’applicazione di patch ai modelli per frammenti di contenuto, a causa del quale le proprietà &quot;translatable&quot; e &quot;showThumbnail&quot; venivano eliminate dal modello.
* SITES-35409: è stato corretto un bug che impediva la ripubblicazione di frammenti corretti durante lo spostamento di una pagina.
* SITES-15757: è stato corretto un bug che impediva la ripubblicazione di pagine modificate durante lo spostamento di una pagina.
* SITES-34638: è stato corretto un bug a causa del quale le proprietà delle pagine padre non venivano incluse durante la creazione di nuove versioni.
* SITES-35071: l’esportazione CSV restituisce risultati non filtrati quando omnisearch utilizza una frase tra virgolette.
* SITES-32182: Edge Delivery con Universal Editor - Correzione di problemi di codifica con URL contenenti parametri di richiesta già codificati.
* SITES-34324: Edge Delivery con Universal Editor - corregge il rendering dei collegamenti con un protocollo tel:.
* SITES-35333: Edge Delivery con Universal Editor - corregge la selezione del rendering delle risorse per le immagini nei metadati della pagina.
* SITES-35549: Edge Delivery con Universal Editor - corregge le entità HTML con doppia codifica nei metadati della pagina.

### Problemi noti {#known-issues-23122}

Nessuna.

### Funzioni e API obsolete {#deprecated-23122}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-23122}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 18 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-23122}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.86.0 | [API Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.2. | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
