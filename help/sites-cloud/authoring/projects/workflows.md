---
title: Utilizzo dei flussi di lavoro per i progetti
description: La soluzione offre diversi flussi di lavoro per progetti già pronti all’uso.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 89972691dadb9573160ba16a220c5b7cb3ae9742
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 75%

---

# Utilizzo dei flussi di lavoro per i progetti {#working-with-project-workflows}

I flussi di lavoro per progetti disponibili includono i seguenti:

* **Flusso di lavoro di approvazione del progetto** - Questo flusso di lavoro ti consente di assegnare contenuti a un utente, rivederli e approvarli.
* **Richiedi lancio** - Un flusso di lavoro per richiedere un lancio.
* **Richiedi pagina di destinazione** - Questo flusso di lavoro richiede una pagina di destinazione.
* **Richiedi e-mail**: flusso di lavoro per la richiesta di un’e-mail.
* **Crea e traduci copia DAM e Crea copia per lingua DAM:** consentono di creare dati binari, metadati ed etichette tradotti per risorse e cartelle.

A seconda del modello di progetto selezionato, hai determinati flussi di lavoro disponibili:

|  | **Progetto semplice** | **Progetto di traduzione** |
|---|:-:|:-:|
| Flusso di lavoro di approvazione del progetto | x |  |
| Richiedi lancio | x |  |
| Richiedi pagina di destinazione | x |  |
| Richiedi e-mail | x |  |
| Crea copia &amp;ast in lingua DAM; |  | x |
| Crea e traduci copia&amp;ast in lingua DAM; |  | x |

>[!NOTE]
>
>&amp;ast; Questi flussi di lavoro non vengono avviati dalla **Flusso di lavoro** in Progetti. Consulta [Creazione di copie per lingua per le risorse.](/help/sites-cloud/administering/translation/managing-projects.md)

I passaggi per avviare e completare i flussi di lavoro sono sempre gli stessi, indipendentemente dal flusso di lavoro che scegli. Cambiano solo i passaggi intermedi.

Puoi avviare un flusso di lavoro direttamente da Progetti (eccetto Crea copia per lingua DAM e Crea e traduci copia DAM). Le informazioni relative a tutte le operazioni in sospeso di un progetto sono elencate nella sezione **Attività**. Le notifiche per le attività che devono essere completate appaiono accanto all&#39;icona utente.

Per ulteriori informazioni sulle operazioni con i flussi di lavoro in AEM, consulta quanto segue:

* [Partecipare ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md)
* [Applicazione dei flussi di lavoro alle pagine](/help/sites-cloud/authoring/workflows/applying.md)
* [Configurare i flussi di lavoro](/help/sites-cloud/administering/workflows-administering.md)

Questa sezione descrive i flussi di lavoro disponibili per Progetti.

## Flusso di lavoro di approvazione progetto {#project-approval-workflow}

Nel flusso di lavoro di approvazione progetto, assegni i contenuti ad un utente, li revisioni e poi li approvi.

1. Nel progetto Semplice, seleziona la **`+`** accedi a **Flussi di lavoro** piastrelle e seleziona **Flusso di lavoro di approvazione del progetto**.
1. Inserisci un titolo e seleziona la persona a cui affidare il compito dall&#39;elenco Team. Se necessario, puoi aggiungere una descrizione, il percorso del contenuto, impostare la priorità e la scadenza.

   ![Richiedi approvazione](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Fai clic su **Crea**. Il flusso di lavoro inizia. L’attività viene visualizzata nella sezione **Attività**.

## Flusso di lavoro Richiedi lancio {#request-launch-workflow}

Questo flusso di lavoro consente di richiedere un lancio.

1. Nel progetto Semplice, seleziona il segno **+** nella sezione **Flussi di lavoro** e fai clic su **Request Launch Workflow (Richiedi flusso di lavoro di Launch)**.
1. Inserisci un titolo per il lancio e inserisci il percorso origine del lancio. Se necessario, puoi anche aggiungere una descrizione e una data di inizio. Seleziona Eredita i dati live della pagina sorgente o Escludi pagine secondarie, a seconda di come vuoi che si comporti il lancio.

   ![Richiedi lancio](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Fai clic su **Crea**. Il flusso di lavoro inizia. Il flusso di lavoro viene visualizzato nella **Flussi di lavoro** elenco (fare clic su ellissi) **...** sulla **Flussi di lavoro** per accedere a questo elenco).

## Flusso di lavoro Crea (e traduci) copia per lingua per le risorse {#create-and-translate-language-copy-workflow-for-assets}

I flussi di lavoro **Crea copia per lingua** e **Crea e traduci copia lingua**[ sono descritti in modo dettagliato nella creazione di copie in lingua per le risorse.](/help/assets/translate-assets.md)
