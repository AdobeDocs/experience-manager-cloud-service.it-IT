---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 859af15f4038b28e6e1398e5168dc008d22985e9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 96%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

>[!NOTE]
>
> Le versioni 20936 e 20783 sono state rese private.

## Versione 20626 {#20626}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 20626, rilasciata pubblicamente il 29 aprile 2025. La versione di manutenzione precedente era la 20476.

L’attivazione della funzione 2025.5.0 fornisce il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-20626}

* ASSETS-46413, ASSETS-46580: è stato aggiunto un nuovo stato di revisione “Anteprima”.
* ASSETS-49542: espansione delle lingue supportate per la trascrizione e la traduzione di video e audio.
* ASSETS-48264: espansione del supporto della qualità PNG per le rappresentazioni.

### Problemi risolti {#fixed-issues-20626}

* ASSETS-50387: correzione della miniatura predefinita del frammento di contenuto da utilizzare in GenStudio.
* ASSETS-49006: visualizzazione delle proprietà video quando l’utente non dispone delle autorizzazioni di scrittura.
* ASSETS-46757, ASSETS-46997: miglioramento dell’accessibilità nell’editor di ritaglio avanzato.
* ASSETS-48018: miglioramento del tracciamento dei riferimenti delle risorse nel rapporto di pubblicazione di Assets.
* ASSETS-35846: miglioramento della coerenza dell’accesso tra il livello di authoring e quello di consegna.
* ASSETS-48171: miglioramento della coerenza dei modelli di Dynamic Media con area di lavoro.
* ASSETS-49813: miglioramento della notifica di scadenza.
* ASSETS-47768, ASSETS-49825, ASSETS-49008, ASSETS-48287: miglioramento della gestione e della visibilità nelle operazioni in blocco.
* ASSETS-50003, ASSETS-50004: miglioramento della denominazione e del controllo delle rappresentazioni incluse nel download di una risorsa.
* ASSETS-47939: miglioramento dell’organizzazione delle risposte per il Content Hub.
* ASSETS-46738: miglioramento delle prestazioni per raccolte molto grandi.
* ASSETS-50121: miglioramento dell’affidabilità degli eventi di pubblicazione delle risorse.
* ASSETS-48490: miglioramento della resilienza dell’elaborazione automatica durante l’acquisizione delle immagini.
* ASSETS-28106, ASSETS-49404: miglioramento della robustezza della ricerca testuale.
* ASSETS-50006, ASSETS-50423: miglioramento delle prestazioni di ricerca e attraversamento all’interno di una cartella di grandi dimensioni.
* ASSETS-46021: miglioramento della visualizzazione video per Safari e per i browser dei dispositivi mobili.
* ASSETS-49002: miglioramento della gestione della modifica dei modelli Dynamic Media.
* ASSETS-48376: vari miglioramenti nell’interfaccia utente di Content Hub.
* ASSETS-48504, ASSETS-49378: vari miglioramenti del comportamento dell’interfaccia utente.
* ASSETS-49540: spostamento di OpenAPI delle relazioni risorsa al di fuori della fase sperimentale.
* ASSETS-40284: aggiornamento della documentazione sull’integrazione di Adobe Stock.
* ASSETS-49739: attività per integrare Figma dal Selettore risorse.

#### Guide AEM {#guides}

* GUIDES-21734: impossibile generare nuovi ID per gli elementi quando questi vengono aggiunti tramite snippet o creati tramite modelli, anche quando l’opzione di generazione automatica dell’ID è abilitata in XMLEditorConfig.
* GUIDES-25969: se l’attributo `scope=external` non è presente nei collegamenti esterni di un argomento DITA, la pubblicazione di HTML5 non riesce senza indicare i file in cui questo attributo manca nei registri di errore, in particolare quando è abilitato il microservizio.
* GUIDES-27288: impossibile trasmettere le proprietà dei metadati per mappare le pagine di destinazione generate utilizzando la nuova pubblicazione AEM Sites.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-20626}

Nessuna.

### Funzioni e API obsolete {#deprecated-20626}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-20626}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 11 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-20626}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.78.0 | [API Oak API 1.78.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
