---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: c6acdd922c052d0db5bf1f05bc03329fbc44ca33
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 32%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note tecniche sulla versione per la versione di manutenzione corrente dell’Experience Manager as a Cloud Service.

## Versione 11382 {#release-11382}

Di seguito sono riepilogati i continui miglioramenti della versione di manutenzione 11382, rilasciata pubblicamente il 28 marzo 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 11289.

L’abilitazione delle funzioni per questa versione di manutenzione ti darà accesso al set di funzioni completo. Consulta le [note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md) per ottenere informazioni dettagliate.

### Problemi risolti {#fixed-issues}

- ASSETS-21023 - È stato corretto il rendering di ritaglio avanzato, che consentiva ai clienti di osservare un&#39;eccezione Null Pointer nell&#39;istanza di Publisher di tutti gli ambienti AEM quando tentavano di accedere a tali rappresentazioni tramite l&#39;API.
- SKYOPS-49280 - Quando si installa una configurazione o un aggiornamento del bundle utilizzando RDE in Pubblica, il risultato potrebbe non essere visibile perché la cache del dispatcher di pubblicazione non viene invalidata

#### Sites {#sites-issues}

- SITES-7796 - Possibilità per l’autore dei contenuti di pubblicare il frammento di contenuto principale e le rispettive varianti durante l’esportazione in target
- SITES-97 - GraphQL: Paginazione e ordinamento, filtro ibrido

>[!NOTE]
>
> In SITES-97 sono stati apportati alcuni miglioramenti all&#39;implementazione GraphQL che potrebbero causare un comportamento imprevisto. Vedi [Modifiche AEM GraphQL relative alla gestione dei valori nulli](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html) per ulteriori informazioni.

#### Risorse {#assets-issues}

- ASSETS-20076 - Aggiungi il supporto per la filigrana video che corrisponde al supporto per la filigrana delle immagini corrente
- ASSETS-21428 - Aggiunte esclusioni per le modifiche CSS

#### Forms {#forms-issues}

- CQ-4351502 - Aggiornamento della mappatura utente del servizio per consentire l&#39;accesso in lettura in Sites

#### Platform {#platform-issues}

- SITES-11040 - Abilitazione condizionale del caching delle query persistenti GraphQL nel dispatcher

### Tecnologie incorporate {#embedded-tech}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak API 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.21.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
