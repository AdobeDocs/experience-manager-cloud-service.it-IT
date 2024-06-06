---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: de06178f66c95baef15de19296a654f1ed4a0387
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 43%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 16544 {#release-16544}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 16544, rilasciata pubblicamente il mercoledì 4 giugno 2024. La versione di manutenzione precedente era 16461.

Con la versione di attivazione funzioni 2024.6.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-16544}

* GRANITE-41133: supporta Jakarta Servlet API 5 e OSGi Servlet Whiteboard API.
* GRANITE-51355: Obsoleto org.slf4j.event.
* GRANITE-51565: l’AEM perde la relazione tra il gruppo locale e il gruppo esterno quando quest’ultimo viene pubblicato dall’AEM.
* GRANITE-51707: imposta il cookie saml_request_path durante il reindirizzamento http per l’autenticazione.
* GRANITE-52010: Aggiornare la versione di Jackrabbit al 2.20.16.
* GRANITE-52057: Aggiornare Filevault a 3.7.3-T20240514105118-694f6aea fissando JCRVLT-745.
* SKYOPS-35998: aggiornare le dipendenze &#39;Sling RepoInit&#39; : Repoinit Parser 1.9.0, Repoinit JCR 1.1.46.

### Problemi risolti {#fixed-issues-16544}

* GRANITE-51375: se non è specificato alcun percorso intermedio, la sincronizzazione idp genera un valore NPE.
* GUIDES-17171: l&#39;operazione di copia e incolla degli argomenti di dimensioni superiori a 15 KB non riesce e viene generato un errore imprevisto.
* GUIDES-17088: funzionalità per modificare lo stato del documento da **Proprietà file** il pannello non funziona correttamente e le modifiche apportate al *Bozza* stato.
* GUIDE-16931: le immagini collegate dagli argomenti non vengono visualizzate nella linea di base dopo la creazione della versione.
* GUIDES-16896: i pannelli di contenuto riutilizzabile non elencano gli elementi quando **Preferenze utente** sono impostati per la visualizzazione dei file **Nome file**.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in Experience Manager Guides, vedi [Roadmap sulla versione di Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-16544}

Nessuno.

### Notifica di modifica {#change-notice-16544}

A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Resource Resolver tramite il framework Sling Model Exporter. Consulta [la documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) per ulteriori dettagli.

### Funzioni e API obsolete {#deprecated-16544}

Per sapere cosa è obsoleto o è stato rimosso in AEM as a Cloud Service, consulta [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-16544}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,64,0 | [API Oak API 1.64.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
