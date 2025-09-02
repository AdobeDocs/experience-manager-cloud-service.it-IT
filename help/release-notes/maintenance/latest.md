---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 67%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 22171 {#22171}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 22171, rilasciata al pubblico il mercoledì 2 settembre 2025. La versione di manutenzione precedente era la 21994.

Con la versione di attivazione funzioni 2025.9.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nuove funzioni  {#new-features-22171}

* ASSETS-53136: Supporto per Vanity ID in Dynamic Media con OpenAPI.

### Miglioramenti {#enhancements-22171}

Nessuna.

### Problemi risolti {#fixed-issues-22171}

* ASSETS-52510: il rilevamento di nomi file duplicati non riesce per i nomi file contenenti Unicode `U+202F`.
* ASSETS-53489: l’eliminazione della cartella dall’interfaccia utente di visualizzazione di Assets non annulla l’approvazione di tutte le risorse contenute.
* ASSETS-54821: &quot;Errore server&quot; intermittente in Asset Link.
* ASSETS-55024: immagine danneggiata nel modello AEM Assets &quot;Download per e-mail&quot;.
* ASSETS-55325: gli URL statici di Dynamic Media omettono l’estensione file dopo la ridenominazione della risorsa.
* ASSETS-55334: la finestra di dialogo Condivisione collegamenti lampeggia brevemente e scompare o non viene mai visualizzata.
* ASSETS-55382: i processi di risorse asincrone riavviati creano una cartella di destinazione duplicata.
* ASSETS-55472: opzione Gestisci pubblicazione &quot;Solo pagine già pubblicate&quot; ignorata.
* SITES-31600: errore di Contexthub js che interrompe la personalizzazione.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-22171}

Nessuna.

### Funzioni e API obsolete {#deprecated-22171}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-22171}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 7 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-22171}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,84,0 | [API Oak API 1.84.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
