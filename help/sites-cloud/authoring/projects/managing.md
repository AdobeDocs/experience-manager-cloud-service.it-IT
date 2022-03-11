---
title: Gestione dei progetti
description: I progetti consentono di organizzare il progetto raggruppando le risorse in un’unica entità accessibile e gestibile nella console Progetti
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 80%

---

# Gestione dei progetti {#managing-projects}

La funzione Progetti consente di organizzare un progetto raggruppando le risorse in un’unica entità.

La console **Progetti** consente di accedere ai progetti e di eseguire azioni su di essi:

![Console Progetti](/help/sites-cloud/authoring/assets/projects-console.png)

Tramite Progetti è possibile creare un progetto e associarvi risorse, ma anche eliminarlo o eliminare i collegamenti alle risorse. È possibile aprire una porzione per visualizzarne il contenuto e aggiungere elementi. In questo argomento vengono descritte le procedure.

## Creazione di un progetto {#creating-a-project}

Con AEM vengono forniti i seguenti modelli tra cui scegliere alla creazione di un progetto:

* Progetto semplice
* Progetto multimediale
* Progetto di traduzione

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

La procedura di creazione di un progetto è la stessa per ciascun progetto. La differenza tra i tipi di progetti include i [ruoli utente](/help/sites-cloud/authoring/projects/overview.md) e i [flussi di lavoro](/help/sites-cloud/authoring/projects/workflows.md) disponibili.  Per creare un nuovo progetto:

1. In **Progetti**, tocca o fai clic su **Crea** per aprire la procedura guidata **Crea progetto**:
1. Seleziona un modello e fai clic su **Successivo**.

   ![Creazione di un progetto](/help/sites-cloud/authoring/assets/projects-create.png)

1. Definisci la **Titolo** e **Descrizione** e aggiungi un **Miniatura** se necessario. Puoi anche aggiungere o eliminare gli utenti e il gruppo a cui appartengono, o fare clic su **Avanzate** per aggiungere un nome da usare nell’URL.

   ![Aggiunta di dettagli al progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Tocca o fai clic su **Crea**. Ti viene richiesto se desideri aprire il nuovo progetto o tornare alla console.

### Associazione di risorse a un progetto {#associating-resources-with-your-project}

Poiché i progetti consentono di raggruppare risorse in un’unica entità, è possibile associare delle risorse a un progetto. Tali risorse sono denominate **porzioni**. I tipi di risorse che è possibile aggiungere sono descritti nella sezione [Porzioni di progetto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

Per associare risorse a un progetto:

1. Apri il progetto dalla console **Progetti**.
1. Tocca o fai clic su **Aggiungi sezione**, quindi seleziona la porzione che desideri collegare al progetto. È possibile selezionare tra più tipi di porzioni.

   ![Aggiunta di una porzione a un progetto](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >Le porzioni associabili a un progetto sono descritte dettagliatamente nella sezione [Porzioni di progetto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

1. Tocca o fai clic su **Crea**. La risorsa è ora collegata al progetto e accessibile da questo.

### Eliminazione di un progetto o di un collegamento di risorsa {#deleting-a-project-or-resource-link}

Per eliminare un progetto dalla console o una risorsa collegata dal progetto si applica lo stesso metodo:

1. Passa alla posizione appropriata:

   * Per eliminare un progetto, spostati nella parte superiore della console **Progetti**.
   * Per eliminare un collegamento di risorsa all’interno di un progetto, apri il progetto nella console **Progetti**.

1. Entra nella modalità di selezione facendo clic su **Seleziona** e scegli il progetto o collegamento di risorsa.
1. Tocca o fai clic su **Elimina**.

1. È necessario confermare l’eliminazione in una finestra di dialogo. Se procedi, il progetto o collegamento di risorsa viene eliminato. Per uscire dalla modalità di selezione, tocca o fai clic su **Deseleziona**.

>[!NOTE]
>
>Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate. Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi: **Proprietari mioprogetto**, **Editor mioprogetto**, **Osservatori mioprogetto**. Tuttavia, se il progetto viene eliminato, tali gruppi non vengono rimossi automaticamente. Un amministratore deve eliminare manualmente i gruppi da **Strumenti** > **Protezione** > **Gruppi**.

### Aggiungere elementi a una porzione {#adding-items-to-a-tile}

Per alcune porzioni è possibile aggiungere più di un oggetto. Ad esempio, è possibile avere più flussi di lavoro o esperienze in esecuzione allo stesso tempo.

Per aggiungere elementi a una porzione:

1. In **Progetti**, accedi al progetto e tocca o fai clic sulla freccia giù sulla tessera a cui desideri aggiungere un elemento.

   ![Aggiungi un elemento a una tessera](/help/sites-cloud/authoring/assets/project-workflows.png)

1. Aggiungi un elemento alla porzione con la stessa procedura che usi quando crei una nuova porzione. Le porzioni di progetto sono descritte [qui](/help/sites-cloud/authoring/projects/overview.md#project-tiles). In questo esempio è stato aggiunto un altro flusso di lavoro.

### Aprire una porzione {#opening-a-tile}

È possibile visualizzare gli elementi inclusi nella porzione selezionata, modificarli o eliminarli.

Per aprire una porzione e visualizzare o modificare gli elementi:

1. Dalla console Progetti, tocca o fai clic sui puntini di sospensione (...) nella parte inferiore della scheda.

   ![Apertura di una tessera](/help/sites-cloud/authoring/assets/project-links.png)

1. AEM mostra l’elenco degli elementi inclusi nella porzione. Per modificarli o eliminarli, entra nella modalità di selezione.

   ![Riquadro aperto](/help/sites-cloud/authoring/assets/projects-add-link.png)

## Visualizzazione delle statistiche di un progetto {#viewing-project-statistics}

È possibile visualizzare le statistiche del progetto nella **Progetti** console.

### Visualizzazione della cronologia di un progetto {#viewing-a-project-timeline}

La cronologia di un progetto fornisce informazioni sull’ultimo utilizzo delle risorse associate. Per visualizzare la timeline del progetto, tocca o fai clic su **Timeline**, quindi entra in modalità di selezione e seleziona il progetto. Le risorse vengono visualizzate nel riquadro a sinistra. Tocca o fai clic **Timeline** per tornare al **Progetti** console.

![Timeline del progetto](/help/sites-cloud/authoring/assets/projects-timeline.png)

### Visualizzazione di progetti attivi e inattivi {#viewing-active-inactive-projects}

Per scegliere tra i progetti attivi e inattivi, nella **Progetti** console, fai clic su **Attiva/Disattiva progetti**. Se accanto all’icona è presente un segno di spunta, vengono visualizzati i progetti attivi.

![Pulsante Attiva progetti](/help/sites-cloud/authoring/assets/projects-active.png)

Se l’icona è affiancata da una x, stai visualizzando i progetti inattivi.

![Pulsante Attiva/Disattiva progetti](/help/sites-cloud/authoring/assets/projects-inactive.png)

## Rendere un progetto attivo o inattivo {#making-projects-inactive-or-active}

Se hai completato un progetto ma desideri mantenere le informazioni ad esso associate, puoi renderlo inattivo.

Per rendere un progetto attivo o inattivo:

1. Dalla console **Progetti**, apri il progetto e seleziona la porzione **Informazioni progetto**.

   >[!NOTE]
   È necessario aggiungere questa porzione nel caso in cui non sia già presente nel progetto. Consulta [Aggiunta di una porzione](#adding-items-to-a-tile).

1. Tocca o fai clic su **Modifica**.
1. Modifica il selettore passando da **Attivo** a **Inattivo** (o viceversa).

   ![Attivazione di un progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Tocca o fai clic su **Fine** per salvare le modifiche apportate.
