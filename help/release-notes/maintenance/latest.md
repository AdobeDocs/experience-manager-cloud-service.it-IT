---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 17064d27dd34bbd5aad89f814481c29b0f6a7fe1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21484 {#21484}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21484, rilasciata pubblicamente l’venerdì 10 luglio 2025. La versione di manutenzione precedente era la 21331.

Con la versione di attivazione funzioni 2025.7.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21484}

Nessuna.

### Problemi risolti {#fixed-issues-21484}

Nessuna.

#### Guide AEM {#guides-21484}

* GUIDE-29781: quando un commento XML viene aggiunto all’interno di un elemento nella vista Origine, gli spazi iniziali e finali intorno al commento vengono persi al passaggio tra viste.
* GUIDE-29078: quando viene aperto un argomento nella vista Autore dopo un aggiornamento del browser, i tag applicati in precedenza nel pannello Proprietà file non vengono mantenuti e l’aggiunta di nuovi tag sovrascrive quelli esistenti, in particolare quando è disponibile un numero elevato di tag da selezionare.
* GUIDES-28214: i tentativi di creare attività di revisione tramite il flusso di lavoro di AEM hanno esito negativo in modo coerente perché il nodo di revisione non è stato creato.
* GUIDES-28104: la pubblicazione di una mappa DITA con l’attributo `chunk=to-content` crea nodi JCR duplicati nel nuovo output di AEM Sites, determinando una struttura di contenuto ridondante in AEM Sites.
* GUIDES-29065, GUIDES-28793: lavorando con raccolte di grandi dimensioni, vengono osservati problemi di prestazioni quali tempi di caricamento più lunghi e timeout intermittenti.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-21484}

Nessuna.

### Funzioni e API obsolete {#deprecated-21484}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21484}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 5 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-21484}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
