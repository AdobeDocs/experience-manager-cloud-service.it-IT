---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 47%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 17098 {#release-17098}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 17098, rilasciata pubblicamente il mercoledì 16 luglio 2024. La versione di manutenzione precedente era 16971.

L’attivazione della funzione 2024.7.0 fornirà il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-17098}

- SKYOPS-79817: abilita l’attività di Sling Feature Analyzer per le mappature degli utenti del servizio

### Problemi risolti {#fixed-issues-17098}

- ASSETS-39665: Smart Crops Sync non funziona dopo la migrazione da 6.5 ad AEMCS
- FORMS-14993: l’API Forms restituisce 500 per il materiale collaterale precedentemente funzionante
- GRANITE-52120: CRXDE restituisce 500 quando vengono visualizzati i dati di controllo di accesso
- GRANITE-52573: richieste che restituiscono 400 quando si utilizza // in URL riscritti
- GRANITE-52746: tutti i tipi di nodo non caricati nella finestra di dialogo Crea nodo
- GRANITE-52777: manipolazione interrotta di 404 secondi quando la richiesta viene racchiusa
- GRANITE-52871: assicurati che publish-worker sia sincronizzato con golden-publish e venga completato prima della compattazione
- SKYOPS-79173: il replicatore non esegue la replica su più agenti che corrispondono a un AgentIdFilter specificato
- SKYOPS-80075: problemi relativi agli umlaut nei nomi delle risorse che causano il blocco della coda di pubblicazione (Mac)
- SKYOPS-81032: escludi i registri generati dalle richieste per ottenere i registri quando utilizzi la registrazione avanzata

### Problemi noti {#known-issues-17098}

Nessuno

### Notifica di modifica {#change-notice-17098}

- A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-17098}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte in dettaglio nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-17098}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,66,0 | [API Oak API 1.66.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
