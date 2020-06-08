---
title: Utilizzo dei flussi di lavoro per i progetti
description: La soluzione offre diversi flussi di lavoro per progetti già pronti all’uso.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 78%

---


# Utilizzo dei flussi di lavoro per i progetti {#working-with-project-workflows}

I flussi di lavoro per progetti disponibili includono i seguenti:

* **Flusso** di lavoro di approvazione del progetto: questo flusso di lavoro consente di assegnare contenuti a un utente, rivedere e quindi approvare.
* **Richiedi lancio** - Un flusso di lavoro per il quale viene richiesto un avvio.
* **Richiedi pagina** di destinazione - Questo flusso di lavoro richiede una pagina di destinazione.
* **Richiedi e-mail**: flusso di lavoro per la richiesta di un’e-mail.
* **Crea e traduci copia DAM e Crea copia per lingua DAM:** consentono di creare dati binari, metadati ed etichette tradotti per risorse e cartelle.

A seconda del modello di progetto selezionato, hai determinati flussi di lavoro disponibili:

|  | **Progetto semplice** | **Progetto multimediale** | **Progetto di traduzione** |
|---|:-:|:-:|:-:|
| Richiedi copia |  | x |  |
| Servizio fotografico per prodotto |  | x |  |
| Approvazione progetto | x |  |  |
| Richiedi lancio | x |  |  |
| Richiedi pagina di destinazione | x |  |  |
| Richiedi e-mail | x |  |  |
| Copia&amp;amp lingua per la creazione di DAM;ast; |  |  | x |
| Copia&amp;amp lingua per la creazione e la traduzione di DAM;ast; |  |  | x |

>[!NOTE]
>
>&amp;ast; These workflows are not started from the **Workflow** tile in Projects. Consulta Creazione di copie per lingua per le risorse.
<!--
>&ast; These workflows are not started from the **Workflow** tile in Projects. See [Creating Language Copies for Assets.](/help/sites-administering/tc-manage.md)
-->

I passaggi per avviare e completare i flussi di lavoro sono sempre gli stessi, indipendentemente dal flusso di lavoro che scegli. Cambiano solo i passaggi intermedi.

Puoi avviare un flusso di lavoro direttamente da Progetti (eccetto Crea copia per lingua DAM e Crea e traduci copia DAM). Le informazioni relative a tutte le operazioni in sospeso di un progetto sono elencate nella sezione **Attività**. Le notifiche per le attività che devono essere completate appaiono accanto all&#39;icona utente.

Per ulteriori informazioni sull’utilizzo dei flussi di lavoro in AEM, consulta:

* [Partecipare ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md)
* [Applicazione dei flussi di lavoro alle pagine](/help/sites-cloud/authoring/workflows/applying.md)
* Configurare i flussi di lavoro <!--* [Configuring workflows](/help/sites-administering/workflows.md)-->

Questa sezione descrive i flussi di lavoro disponibili per Progetti.

## Flusso di lavoro Richiedi copia {#request-copy-workflow}

Questo flusso di lavoro consente di richiedere un manoscritto ad un utente, e poi approvarlo. Per avviare il flusso di lavoro Richiedi copia:

1. Nel progetto Media, seleziona il segno **+** nella sezione **Flussi di lavoro** e fai clic su **Request Copy Workflow (Richiedi copia flusso di lavoro)**.
1. Immetti il titolo del manoscritto e un breve riassunto della tua richiesta. Se necessario, puoi immettere il numro delle parole di destinazione, impostare la priorità e la scadenza.

   ![Richiedi copia, flusso di lavoro](/help/sites-cloud/authoring/assets/projects-request-copy.png)

1. Fai clic su **Crea**. Il flusso di lavoro inizia. L’attività viene visualizzata nella sezione **Attività**.

   ![Richiesta copia aggiunta](/help/sites-cloud/authoring/assets/projects-request-copy-add.png)

## Flusso di lavoro di approvazione progetto {#project-approval-workflow}

Nel flusso di lavoro di approvazione progetto, assegni i contenuti ad un utente, li revisioni e poi li approvi.

1. In your Simple project, select the **`+`** sign in the **Workflows** tile and select **Project Approval Workflow**.
1. Inserisci un titolo e seleziona la persona a cui affidare il compito dall&#39;elenco Team. Se necessario, puoi aggiungere una descrizione, il percorso del contenuto, impostare la priorità e la scadenza.

   ![Richiesta approvazione](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Fai clic su **Crea**. Il flusso di lavoro inizia. L’attività viene visualizzata nella sezione **Attività**.

   ![Richiesta approvazione aggiunta](/help/sites-cloud/authoring/assets/projects-approval-add.png)

## Flusso di lavoro Richiedi lancio {#request-launch-workflow}

Questo flusso di lavoro consente di richiedere un lancio.

1. Nel progetto Semplice, seleziona il segno **+** nella sezione **Flussi di lavoro** e fai clic su **Request Launch Workflow (Richiedi flusso di lavoro di Launch)**.
1. Inserisci un titolo per il lancio e inserisci il percorso origine del lancio. Se necessario, puoi anche aggiungere una descrizione e una data di inizio. Seleziona Eredita i dati live della pagina sorgente o Escludi pagine secondarie, a seconda di come vuoi che si comporti il lancio.

   ![Richiesta avvio](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Fai clic su **Crea**. Il flusso di lavoro inizia. The workflow appears in the **Workflows** list (click ellipses **...** on the **Workflows** tile to access this list).

## Flusso di lavoro Crea (e traduci) copia per lingua per le risorse {#create-and-translate-language-copy-workflow-for-assets}

I flussi di lavoro **Crea copia per lingua** e **Crea e traduci copia lingua** sono descritti in modo dettagliato nella creazione di copie in lingua per le risorse.
