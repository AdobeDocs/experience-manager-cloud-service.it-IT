---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ca9b5965dbfade36763e2432601559c9abcd2d41
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 17689 {#release-17689}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 17689, rilasciata al pubblico il 10 settembre 2024. La precedente versione di manutenzione era la 17569.

Con la versione di attivazione funzioni 2024.9.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-17689}

* ASSETS-41404: modifiche al supporto dei miglioramenti DRM.
* ASSETS-41621: processo di copia delle risorse asincrone aggiornato.
* ASSETS-32166: processo di spostamento delle risorse asincrone aggiornato.
* ASSETS-41429: supporto dei predefiniti immagine in DM OpenAPI.
* ASSETS-38968: miglioramento della rappresentazione dei riferimenti ai frammenti di contenuto.
* ASSETS-41787, ASSETS-41183: miglioramenti per il framework di operazioni in blocco delle risorse.
* GRANITE-52917: ottimizzazioni per migliorare i tempi di installazione dei pacchetti di copia dei contenuti.
* SCRNS-3980: rilevamento della schermata grigia nei lettori che hanno sotto-sequenze senza risorse pianificate.

### Problemi risolti {#fixed-issues-17689}

* ASSETS-40875: NPE spuria registrata da AssetDeleteHandler.
* ASSETS-42422: attivazione del percorso asincrono per lo spostamento di una singola risorsa evitata.
* ASSETS-41234: Unified Shell - La navigazione globale potrebbe non funzionare se viene aperta quando la barra di ricerca è aperta.
* ASSETS-42256: Unified Shell - Tag/Badge che indica che l’ambiente funziona solo in modo intermittente.
* ASSETS-41271: la ripubblicazione non necessaria di Risorse durante le operazioni di spostamento è stata impedita.
* ASSETS-38894: limitazione dei nuovi tentativi elaborando il watchdog.
* ASSETS-40815: utilizzo dell’anteprima del rendering PDF per visualizzare il file PPT nell’interfaccia utente di condivisione collegamenti .
* ASSETS-37123: impossibile caricare l’anteprima delle risorse nella finestra di dialogo Condivisione collegamenti.
* CQ-4358156: aggiornamento dei collegamenti precedenti del tag da eliminare.
* SCRNS-4495: il pulsante Incolla fisso non funziona correttamente per diversi gruppi di utenti.
* SCRNS-4512: rimozione dei componenti relativi al dispositivo dagli schermi AEMaaCS.
* SCRNS-4466: nella dashboard del canale, nascondi - visualizza manifesto, genera contenuto offline, aggiorna cache manifesto, pannello di visualizzazione.
* SCRNS-4513: aggiunte intestazioni di colonna per la pagina dei risultati di ricerca nella vista a elenco.

### Problemi noti {#known-issues-17689}

* FORMS-14340: errore nella creazione di un’istanza di FormsAndDocumentOmniSearchHandler e CloudStorageSubmitActionInserter. Queste sono innocue istruzioni di registro.
* FORMS-15818: le istruzioni della voce del descrittore del componente “OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml” non trovate nei registri del server. Queste sono innocue istruzioni di registro.
* SITES-23662: l’utente che attiva una pubblicazione non può essere estratto dalle istruzioni di registro JCR nei registri del server. Questo è per una funzione in fase di sviluppo che potrebbe causare errori intermittenti e innocui di tipo “Impossibile trovare un ID utente valido nel batch di eventi OSGI” nel registro.

### Notifica di modifica {#change-notice-17689}

* A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-17689}

Si noti che è in corso l’aggiornamento di `com.day.cq.wcm.api` e con la versione corrente sono stati contrassegnati come `@Deprecated` alcuni dei relativi metodi e classi. Questi verranno rimossi nelle versioni future, quindi se utilizzi uno di questi, valuta di passare alle alternative suggerite.

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-17689}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 4 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-17689}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak API 1.68.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.26.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
