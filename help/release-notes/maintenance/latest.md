---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 53%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 13173 {#release-13173}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 13173, rilasciata pubblicamente il 18 agosto 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 13099.

2023.8.0 Feature Activation fornirà il set completo di funzioni per questa versione di manutenzione. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-13173}

Nessuno.

### Problemi risolti {#fixed-issues-13173}

- SITES-15463: Modelli di siti - Non è possibile pubblicare modelli.

### Problemi noti {#known-issues-13173}

- SITES-15359: Frammenti di contenuto - Il modello del nome della variante non corrisponde correttamente alle varianti che hanno ```'_'``` nei nomi delle risorse.
- FORMS-10444: non è possibile pubblicare modelli di Forms adattivi (soluzione alternativa: utilizzare la console di distribuzione).
- CQ-4354191: Flussi di lavoro - Il modulo di avvio personalizzato può essere attivato molte volte a causa dei metadati di replica presenti sui nodi nt:unstructured (soluzione alternativa: aggiorna i moduli di avvio per escludere le proprietà dei metadati di replica per evitare sovrapposizioni).

### Tecnologie incorporate {#embedded-tech-13173}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
