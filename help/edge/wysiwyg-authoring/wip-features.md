---
title: Funzioni dei siti in esecuzione per i Edge Delivery Services
description: Scopri le funzioni e i casi d’uso di AEM Sites come sono ancora in fase di lavorazione e come trovare soluzioni alternative quando utilizzi i Edge Delivery Services.
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: dbe4cd619f4dc680e6fc4826f6a4fea92bab9707
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Funzioni dei siti in esecuzione per i Edge Delivery Services {#wip-sites-features}

Scopri le funzioni e i casi d’uso di AEM Sites come sono ancora in fase di lavorazione e come trovare soluzioni alternative quando utilizzi i Edge Delivery Services.

>[!TIP]
>
>Il lavoro in corso non significa la fine della strada. Se hai bisogno di una funzione o di un caso d’uso elencato come work-in-progress nel presente documento, contatta il tuo rappresentante Adobe. Tu e Adobe potete lavorare insieme per comprendere le vostre esigenze particolari e trovare soluzioni alternative.

## Funzioni in corso di lavorazione {#wip-features}

Quando si utilizzano Edge Delivery Services con AEM Sites, è disponibile la maggior parte delle funzioni di Sites. Quasi tutte le azioni disponibili nella console [Sites](/help/sites-cloud/authoring/sites-console/introduction.md) sono ad esempio applicabili ai Edge Delivery Services.

Tuttavia, alcune feature sono in corso di lavorazione (WIP). Le funzioni WIP sono funzioni della console Sites non ancora disponibili per i Edge Delivery Services con AEM Sites o solo parzialmente disponibili. Per questo motivo, le funzionalità WIP possono essere presentate in modo diverso rispetto alle corrispondenti funzionalità Sites oppure possono esistere soluzioni alternative per il caso d&#39;uso.

Nell&#39;elenco seguente vengono illustrate le feature WIP e le soluzioni alternative. Se il progetto richiede una funzione WIP, consulta le alternative suggerite di seguito e rivolgiti a Adobe per capire insieme il tuo caso d’uso.

| Funzione Sites | Stato su Edge | Note | Documentazione di Edge |
|---|---|---|---|
| [Ereditarietà pagina](/help/sites-cloud/administering/msm-and-translation.md) | Disponibile |  | [Ereditarietà dei contenuti nell&#39;editor universale](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Ereditarietà componente](/help/sites-cloud/administering/msm-and-translation.md) | Parzialmente disponibile | I componenti ereditano il contenuto, ma l’ereditarietà può essere ripristinata solo a livello di pagina | [Ereditarietà dei contenuti nell&#39;editor universale](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Copia lingua](/help/sites-cloud/administering/translation/overview.md) | Parzialmente disponibile | I componenti ereditano il contenuto, ma l’ereditarietà può essere ripristinata solo a livello di pagina | [Ereditarietà dei contenuti nell&#39;editor universale](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Gestione multisito](/help/sites-cloud/administering/msm/overview.md) | Parzialmente disponibile | I componenti ereditano il contenuto, ma l’ereditarietà può essere ripristinata solo a livello di pagina | [Ereditarietà dei contenuti nell&#39;editor universale](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Lanci](/help/sites-cloud/authoring/launches/overview.md) | Parzialmente disponibile | I componenti ereditano il contenuto, ma l’ereditarietà può essere ripristinata solo a livello di pagina | [Ereditarietà dei contenuti nell&#39;editor universale](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Modelli di pagina](/help/sites-cloud/authoring/page-editor/templates.md) | In arrivo! | Le pagine create da modelli sono copie indipendenti del modello originale. | [Utilizzo dei modelli di pagina con Universal Editor](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Hub di contesto e destinazione](/help/sites-cloud/authoring/personalization/overview.md) | Non disponibile |  |  |
| [Timewarp](/help/sites-cloud/authoring/launches/preview.md) | Non disponibile |  |  |
| [Contenuto associato](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | Non disponibile |  |  |
| [Frammenti esperienza](/help/sites-cloud/authoring/fragments/experience-fragments.md) | Alternativa | Creare una pagina e utilizzare un componente frammento |  |

## Casi d’uso work-in-progress {#wip-use-cases}

Poiché i Edge Delivery Services sono basati su uno stack tecnologico completamente nuovo e moderno, i seguenti casi di utilizzo di AEM Sites non sono ancora completamente coperti e sono ancora in fase di elaborazione. Se il progetto richiede un caso d’uso WIP, contatta Adobe per lavorare insieme e comprendere le esigenze del progetto.

| Caso di utilizzo: Sites | Dettagli |
|---|---|
| Logica lato server per il rendering delle pagine | Utilizzo del runtime AEM come server app |
| Pagine dinamiche | SSI o qualsiasi tecnica Dynamic Include |
| Gestione degli utenti | Utilizzo di AEM come IdP |
| Autenticazione | Utilizzo dell’AEM per la sicurezza dei contenuti |
| Autorizzazione dei contenuti | AEM come extranet sicura |
