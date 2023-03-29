---
title: Note sulla versione di manutenzione più recente di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione più recente di  [!DNL Adobe Experience Manager]  as a Cloud Service.
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le fasi di rilascio tecnico per l’ultima versione di manutenzione di Experience Manager as a Cloud Service.

## Versione 11289 {#release-11289}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 11289, rilasciata al pubblico il 7 marzo 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 10912.

L’abilitazione delle funzioni per questa versione di manutenzione ti darà accesso al set di funzioni completo. Consulta le [note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md) per ottenere informazioni dettagliate.

### Problemi noti {#known-issues}

Non eseguire l’aggiornamento se utilizzi CORS. In questa versione è stato identificato un problema che influisce sulla funzionalità di distribuzione dei contenuti di GraphQL. Una modifica nella configurazione predefinita del dispatcher AEM riguardante il modo in cui le query persistenti di GraphQL vengono memorizzate nella cache può interrompere la distribuzione di contenuto GraphQL di tali query. Questo problema verrà risolto nella prossima versione di manutenzione.

### Problemi risolti {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 È stato risolto un problema con le Live Copy che non potevano essere create per le pagine con annotazioni
- SITES-11683 Sono state disabilitate le Live Copy MSM con ereditarietà parzialmente interrotta

#### Risorse {#assets-issues}

- ASSETS-20879 È stata corretta una regressione che impediva il corretto funzionamento dell’interfaccia utente Rapporti delle risorse e causava risultati errati nei rapporti generati.
- ASSETS-21020 È stato risolto un problema con il download di risorse interrotte: il profilo immagine non esiste dopo lo spostamento della risorsa
- ASSETS-21023 È stato risolto un problema relativo ai rendering delle immagini in Dynamic Media che impediva l’accesso tramite API

#### Forms {#forms-issues}

- Nessuno

#### Platform {#platform-issues}

- GRANITE-44467 - È stato risolto un problema che causava un errore di importazione. Durante l’aggiornamento di un nodo esistente, Filevault in alcune istanze non manteneva i tipi mixin e i nodi secondari

### Tecnologie incorporate {#embedded-tech}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak API 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.21.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
