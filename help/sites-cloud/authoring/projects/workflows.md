---
title: Utilizzo dei flussi di lavoro per i progetti
description: Sono disponibili diversi flussi di lavoro di progetto pronti all’uso.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 46%

---

# Utilizzo dei flussi di lavoro per i progetti {#working-with-project-workflows}

I flussi di lavoro dei progetti disponibili includono:

* **Flusso di lavoro di approvazione progetto:** questo flusso di lavoro consente di assegnare dei contenuti a un utente, rivederli e approvarli.
* **Richiedi lancio**: flusso di lavoro per richiedere un lancio.
* **Richiedi pagina di destinazione**: flusso di lavoro per richiedere una pagina di destinazione.
* **Richiedi e-mail**: flusso di lavoro per la richiesta di un’e-mail.
* **DAM - Crea e traduci copia e DAM - Crea copia lingua** : crea binari tradotti, metadati e tag per risorse e cartelle.

A seconda del modello di progetto selezionato, sono disponibili alcuni flussi di lavoro:

|   | **Progetto semplice** | **Progetto di traduzione** |
|---|:-:|:-:|
| Flusso di lavoro di approvazione progetto | x |  |
| Richiedi lancio | x |  |
| Richiedi pagina di destinazione | x |  |
| Richiedi e-mail | x | |
| Creazione DAM copia in lingua &amp;ast; |  | x |
| Creazione DAM e traduzione copia in lingua &amp;ast; |   | x |

>[!NOTE]
>
>&amp;ast Questi flussi di lavoro non si trovano nella sezione **Flusso di lavoro** in Progetti. Consulta [Creazione di copie per lingua per Assets](/help/sites-cloud/administering/translation/managing-projects.md).

I passaggi per avviare e completare i flussi di lavoro sono gli stessi, indipendentemente dal flusso di lavoro scelto. Cambiano solo i passaggi.

Avvia un flusso di lavoro direttamente in Progetti (ad eccezione di Crea copia per lingua DAM o Crea e traduci copia per lingua DAM). Le informazioni su eventuali attività in sospeso in un progetto sono elencate nella sezione **Attività** affiancare. Le notifiche per le attività da completare vengono visualizzate accanto all’icona utente.

Per ulteriori informazioni sull&#39;utilizzo dei flussi di lavoro su AEM, consulta la seguente documentazione:

* [Partecipare ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md)
* [Applicazione dei flussi di lavoro alle pagine](/help/sites-cloud/authoring/workflows/applying.md)
* [Configurare i flussi di lavoro](/help/sites-cloud/administering/workflows-administering.md)

Questa sezione descrive i flussi di lavoro disponibili per Progetti.

## Flusso di lavoro di approvazione progetto {#project-approval-workflow}

Nel flusso di lavoro Approvazione progetto è possibile assegnare il contenuto a un utente, rivederlo e quindi approvarlo.

1. Vai su Progetto semplice e seleziona il simbolo **`+`**+ nella sezione **Flussi di lavoro**, poi fai clic su **Flusso di lavoro di approvazione progetto**.
1. Immettere un titolo e selezionare dall&#39;elenco Team l&#39;utente a cui assegnarlo. Se applicabile, immettere una descrizione, il percorso del contenuto, la priorità dell&#39;attività e una data di scadenza.

   ![Richiedi approvazione](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Fai clic su **Crea**. Il flusso di lavoro viene avviato. L’attività viene visualizzata nella sezione **Attività** affiancare.

## Richiedi flusso di lavoro di Launch {#request-launch-workflow}

Questo flusso di lavoro ti consente di richiedere un lancio.

1. Nel progetto Semplice, seleziona il segno **+** nella sezione **Flussi di lavoro** e fai clic su **Request Launch Workflow (Richiedi flusso di lavoro di Launch)**.
1. Inserisci un titolo per il lancio e fornisci il percorso di origine del lancio. Puoi anche aggiungere una descrizione e una data di attivazione, se applicabile. Seleziona Eredita i dati live della pagina di origine o escludi le sottopagine a seconda di come desideri che si comporti il lancio.

   ![Richiedi lancio](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Fai clic su **Crea**. Il flusso di lavoro viene avviato. Il flusso di lavoro viene visualizzato nell&#39;elenco **Flussi di lavoro** (fai clic sui puntini di sospensione **…** nella sezione **Flussi di lavoro** per accedere a questo elenco).

## Flusso di lavoro Crea (e traduci) copia per lingua per le risorse {#create-and-translate-language-copy-workflow-for-assets}

I flussi di lavoro **Crea copia per lingua** e **Crea e traduci copia lingua** sono descritti in modo dettagliato nella [creazione di copie in lingua per le risorse](/help/assets/translate-assets.md).
