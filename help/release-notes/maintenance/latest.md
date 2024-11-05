---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c638039ea957f5f7ae0dc64f49c3ace4381cb040
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 29%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18459 {#18459}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18459, rilasciata pubblicamente il mercoledì 5 novembre 2024. La versione di manutenzione precedente era la 18311.

Con la versione di attivazione funzioni 2024.11.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18459}

* CQ-4357471: aggiungi il supporto per la traduzione dei dizionari i18n in AEMaaCS.
* SITES-23591: Frammenti di contenuto: aggiornamento del frammento di contenuto per il supporto UUID.
* SITES-25440: Frammenti di contenuto: API di ricerca CFM per mostrare lo stato di replica.
* SITES-24369: Frammenti di contenuto: miglioramenti alla documentazione OpenAPI.
* SITES-25478: Frammenti di contenuto: aggiungi il supporto back-end per riferimenti a risorse esterne.
* SITES-26119: Frammenti di contenuto: aggiungi il supporto di riferimenti a risorse esterne nel tipo di riferimento.
* SITES-21199: Edge Delivery con Universal Editor: aggiunta del supporto per modelli creati da pagine.
* SITES-20311: Edge Delivery con Universal Editor: aggiunta del supporto per l’importazione di CSV in fogli di calcolo.
* SITES-24821: Edge Delivery con Universal Editor: imposta aem.page/aem.live come impostazione predefinita per l’integrazione con Edge Delivery.

### Problemi risolti {#fixed-issues-18459}

* CQ-4358730: CQPagePreviewGenerator ha esito negativo quando sono presenti più di 10 chiavi da tradurre.
* FORMS-14978: abilitazione del caricamento della pagina per un modulo basato su Componente core per l’editor di temi.
* FORMS-16596: problema di accessibilità: i pulsanti disattivati non sono riconosciuti dal Reader dello schermo.
* SITES-10575: MSM: Blueprint Bloomfilter Loader tenta di caricare più di 100.000 righe.
* SITES-20755: Frammenti di contenuto: il riferimento della risorsa con aggiornamento UUID non mostra la miniatura.
* SITES-26253: Frammenti di contenuto: migrazione UUID: cambia l’argomento del processo sling in generico.
* SITES-21338: Frammenti di contenuto: l’endpoint referencedBy non restituisce il riferimento di pagina corretto.
* SITES-24421: Frammenti di contenuto: l’endpoint di modifica del CF non funziona per il CF recuperato tramite GET CF.
* SITES-25461: Frammenti di contenuto: il filtro per modello nella ricerca di CF deve fare distinzione tra maiuscole e minuscole.
* SITES-25471: Frammenti di contenuto: corregge la convalida dei modelli globali in ModelValidatorServlet.
* SITES-25795: Frammenti di contenuto: l’API del modello CF non riesce se non è impostata alcuna data cq.
* SITES-25817: Frammenti di contenuto: Migliora la promozione di Launch: aggiorna l’ultima promozione per Launches CF.
* SITES-26030: Frammenti di contenuto: Endpoint /referencesTree non restituisce l’intestazione necessaria.
* SITES-26031: Frammenti di contenuto: lo stato della replica non viene restituito sull’endpoint di ricerca CFM.
* SITES-26213: Frammenti di contenuto: i frammenti di contenuto con annullamento della pubblicazione devono convalidare solo i riferimenti pubblicati.
* SITES-26226: Frammenti di contenuto: avvia un problema del flusso di lavoro quando nessuno dei percorsi specificati è utilizzabile.
* SITES-26238: Frammenti di contenuto: i riferimenti alle risorse restituiti dall’API hanno un ordine diverso rispetto a quello di JCR.
* SITES-25456: Eventi: quando si sposta una pagina, oltre all’evento di spostamento della pagina viene generato un evento di eliminazione della pagina.
* SITES-25658: Eventi: il livello e sourceUrl non vengono popolati negli eventi di stato del contenuto della pagina.
* SITES-6497: Lanci: la pagina Crea in lancio non funziona.
* SITES-25393: Edge Delivery con Universal Editor: nodi di testo persi durante il rendering del testo RTF formattato con un singolo paragrafo.
* SITES-24643: Edge Delivery con Universal Editor: gli attributi di metadati OpenGraph e twitter non funzionano nel modello di metadati della pagina.

### Problemi noti {#known-issues-18459}

Nessuno.

### Funzioni e API obsolete {#deprecated-18459}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-18459}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
