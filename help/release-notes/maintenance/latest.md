---
title: Note sulla versione di manutenzione più recente di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione di manutenzione più recente di [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note tecniche di rilascio per l’ultima versione di manutenzione di Experience Manager as a Cloud Service.

## Versione 10912 {#release-10912}

Di seguito sono riepilogati i continui miglioramenti della versione di manutenzione 10912, rilasciata pubblicamente il 3 febbraio 2023. Questa versione di manutenzione è un aggiornamento della precedente release di manutenzione 9850.

L’abilitazione delle funzioni per questa versione di manutenzione fornisce l’intero set di funzioni. Consulta la sezione [note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md) per informazioni complete.

### Problemi noti {#known-issues}

Non eseguire l’aggiornamento se si utilizza CORS. Abbiamo identificato un problema che influisce sulla parte di consegna dei contenuti GraphQL in questa versione. Una modifica nella configurazione predefinita AEM dispatcher rispetto al modo in cui le query persistenti GraphQL vengono memorizzate nella cache può interrompere la distribuzione del contenuto GraphQL di query persistenti per i clienti che utilizzano una configurazione CORS.

### Tecnologie integrate {#embedded-tech}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM componenti core WCM | Versione 2.21.2 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
