---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f9f3d1fcb32445269e5ca4b9479b8e9075c73c10
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 92%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18598 {#18598}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18598, rilasciata pubblicamente il giovedì 13 novembre 2024. La versione di manutenzione precedente era la 18311. La versione 18459 è stata resa privata a causa di un problema.

Con la versione di attivazione funzioni 2024.11.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18598}

* CQ-4357471: aggiunta del supporto per la traduzione dei dizionari i18n in AEMaaCS.
* FORMS-11646: impostazione delle variabili globalContext per le pagine rilevanti di AEM Forms.
* FORMS-14833 - AEM Forms ora consente di includere frammenti di moduli adattivi nel documento record (DoR) finale.
* FORMS-14255 - Una funzione di salvataggio automatico consente di salvare automaticamente come bozza un modulo parzialmente completato. L’utente potrà quindi completare in un secondo momento la compilazione del modulo, anche da un altro dispositivo.
* SITES-23591: Frammenti di contenuto - aggiornamento del frammento di contenuto per il supporto UUID.
* SITES-25440: Frammenti di contenuto - API di ricerca CFM per mostrare lo stato di replica.
* SITES-24369 - Frammenti di contenuto: Miglioramenti alla documentazione OpenAPI.
* SITES-25478 - Frammenti di contenuto: aggiunta del supporto di back-end di riferimenti a risorse esterne.
* SITES-26119 - Frammenti di contenuto: aggiunta del supporto di riferimenti a risorse esterne nel tipo di riferimento.
* SITES-24609: Frammenti di contenuto: migliorare la convalida durante l’eliminazione dei frammenti di contenuto.
* SITES-21199 - Edge Delivery con editor universale: aggiunta del supporto per modelli creati da pagine.
* SITES-20311 - Edge Delivery con editor universale: aggiunta del supporto per l’importazione di CSV nei fogli di calcolo.
* SITES-24821 - Edge Delivery con editor universale : impostazione aem.page/aem.live come predefinita per l’integrazione con Edge Delivery.

### Problemi risolti {#fixed-issues-18598}

* CQ-4358730: CQPagePreviewGenerator non riesce quando sono presenti più di 10 chiavi da tradurre.
* CQ-4358028 - La creazione di un progetto AEM non riesce se utenti appartenenti solo al gruppo amministratori di progetto caricano una nuova miniatura nella pagina di creazione del progetto.
* FORMS-14978: abilitazione del caricamento della pagina per un modulo basato su componente core per l’editor di temi.
* FORMS-15682 - Il problema riguarda l’integrazione di AEM Forms e Dynamics FDM. Quando si invia un modulo, il documento di record (DOR) non viene inviato come allegato PDF al campo dell’entità specificato.
* FORMS-15799: nella pagina Adobe Sign GovCloud Signature il rendering è effettivamente visibile nell’iframe.
* FORMS-16113 - Se utenti con il ruolo di amministratore dell’account Adobe Sign tentano di accedere a un documento inviato da un’altra persona (anch’essa con ruolo di amministratore), l’API GET per l’accordo potrebbe restituire un ID di accordo diverso da quello generato inizialmente al momento della creazione dell’accordo in questione.
* FORMS-16596 - Problema di accessibilità: i pulsanti disattivati non sono riconosciuti dall’assistente vocale.
* GRANITE-53907: impossibile identificare l’utente del servizio come utente con privilegi avanzati del flusso di lavoro.
* SKYOPS-90560: la versione più recente del modello Sling influisce sulle prestazioni dell’esportazione del modello Sling.
* SITES-10575: MSM: Blueprint Bloomfilter Loader tenta di caricare più di 100.000 righe.
* SITES-20755 - Frammenti di contenuto: il riferimento della risorsa con aggiornamento UUID non mostra la miniatura.
* SITES-26253 - Frammenti di contenuto - Migrazione UUID: modifica dell’argomento del processo sling per essere generico.
* SITES-21338 - Frammenti di contenuto: l’endpoint referencedBy non restituisce il riferimento di pagina corretto.
* SITES-24421 - Frammenti di contenuto: l’endpoint di modifica del CF non funziona per il CF recuperato tramite GET CF.
* SITES-25461 - Frammenti di contenuto: il filtro per modello nella ricerca di CF deve fare distinzione tra maiuscole e minuscole.
* SITES-25471 - Frammenti di contenuto: correzione della convalida dei modelli globali in ModelValidatorServlet.
* SITES-25795 - Frammenti di contenuto: l’API del modello CF non riesce se non è impostata alcuna data cq.
* SITES-25817 - Frammenti di contenuto - Miglioramento di promoteLaunch: aggiornamento dell’ultima promozione per CF dei lanci.
* SITES-26030 - Frammenti di contenuto: endpoint/referencesTree non restituisce l’intestazione necessaria.
* SITES-26031 - Frammenti di contenuto: lo stato della replica non viene restituito sull’endpoint di ricerca CFM.
* SITES-26213 - Frammenti di contenuto: i frammenti di contenuto con annullamento della pubblicazione devono convalidare solo i riferimenti pubblicati.
* SITES-26226 - Frammenti di contenuto: viene avviato un problema del flusso di lavoro quando nessuno dei percorsi specificati è utilizzabile.
* SITES-26238 - Frammenti di contenuto: i riferimenti alle risorse restituiti dall’API hanno un ordine diverso rispetto a quello di JCR.
* SITES-25456 - Eventi: quando si sposta una pagina, oltre all’evento di spostamento della pagina viene generato un evento di eliminazione della pagina.
* SITES-25658 - Eventi: il livello e sourceUrl non vengono popolati negli eventi di stato del contenuto della pagina.
* SITES-6497 - Lanci: la pagina Crea in lancio non funziona.
* SITES-25938 - Lanci: eliminazione imprevista dopo un progetto di traduzione.
* SITES-25393 - Edge Delivery con editor universale: nodi di testo persi durante il rendering del testo RTF formattato con un singolo paragrafo.
* SITES-24643 - Edge Delivery con editor universale: gli attributi di metadati OpenGraph e Twitter non funzionano nel modello di metadati della pagina.
* SITES-25401: Frammenti esperienza: aggiornamento di riferimento XF lento.

### Problemi noti {#known-issues-18598}

Nessuno.

### Funzioni e API obsolete {#deprecated-18598}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-18598}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 21 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-18598}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
