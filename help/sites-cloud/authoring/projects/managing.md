---
title: Gestione dei progetti
description: Progetti consente di organizzare un progetto raggruppando le risorse in un’unica entità, accessibile e gestibile nella console dedicata
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 82%

---

# Gestione dei progetti {#managing-projects}

La funzione Progetti consente di organizzare un progetto raggruppando le risorse in un’unica entità.

Nella console **Progetti** puoi accedere ai tuoi progetti e agire di conseguenza:

![Console Progetti](/help/sites-cloud/authoring/assets/projects-console.png)

Tramite Progetti è possibile creare un progetto e associarvi risorse, ma anche eliminarlo o eliminare i collegamenti alle risorse. È possibile aprire un riquadro per visualizzarne il contenuto e aggiungere elementi. In questo argomento vengono descritte tali procedure.

## Creazione di un progetto {#creating-a-project}

Con AEM vengono forniti i seguenti modelli tra cui scegliere alla creazione di un progetto:

* Progetto semplice
* Progetto multimediale
* Progetto di traduzione

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

La procedura di creazione di un progetto è la stessa per ciascun progetto. La differenza tra i tipi di progetti include i [ruoli utente](/help/sites-cloud/authoring/projects/overview.md) e i [flussi di lavoro](/help/sites-cloud/authoring/projects/workflows.md) disponibili.  Per creare un progetto:

1. In **Progetti**, seleziona **Crea** per aprire la procedura guidata **Crea progetto**:
1. Seleziona un modello e fai clic su **Avanti**.

   ![Creazione di un progetto](/help/sites-cloud/authoring/assets/projects-create.png)

1. Definisci **Titolo** e **Descrizione** e aggiungi un&#39;immagine **Miniatura**, se necessario. Puoi anche aggiungere o eliminare utenti e il gruppo a cui appartengono, o fare clic su **Avanzate** per aggiungere un nome da usare nell’URL.

   ![Aggiunta di dettagli al progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Seleziona **Crea**. Nella finestra di conferma ti viene richiesto se desideri aprire il nuovo progetto o tornare alla console.

### Associazione di risorse a un progetto {#associating-resources-with-your-project}

Poiché i progetti consentono di raggruppare risorse in un’unica entità, è possibile associare delle risorse a un progetto. Queste risorse sono chiamate **Riquadri**. I tipi di risorse che è possibile aggiungere sono descritti nella sezione [Riquadri progetto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

Per associare le risorse a un progetto:

1. Apri il progetto dalla console **Progetti**.
1. Seleziona **Aggiungi riquadro** e seleziona il riquadro da collegare al progetto. È possibile selezionare tra più tipi di riquadri.

   ![Aggiunta di un riquadro a un progetto](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >I riquadri associabili a un progetto sono descritti dettagliatamente nella sezione [Riquadri di progetto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

1. Seleziona **Crea**. La risorsa è ora collegata al progetto e accessibile da questo.

### Eliminazione di un progetto o di un collegamento di risorsa {#deleting-a-project-or-resource-link}

Per eliminare un progetto dalla console o una risorsa collegata dal progetto si applica lo stesso metodo:

1. Passa alla posizione appropriata:

   * Per eliminare un progetto, spostati nella parte superiore della console **Progetti**.
   * Per eliminare un collegamento di risorsa all’interno di un progetto, apri il progetto nella console **Progetti**.

1. Entra nella modalità di selezione facendo clic su **Seleziona** e scegli il progetto o collegamento di risorsa.
1. Seleziona **Elimina**.

1. È necessario confermare l’eliminazione in una finestra di dialogo. Se confermata, il progetto o il collegamento alla risorsa viene eliminato. Seleziona **Deseleziona** per uscire dalla modalità di selezione.

>[!NOTE]
>
>Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate. Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi: **Proprietari mioprogetto**, **Editor mioprogetto**, **Osservatori mioprogetto**. Tuttavia, se il progetto viene eliminato, tali gruppi non vengono rimossi automaticamente. Un amministratore deve eliminare manualmente i gruppi in **Strumenti** > **Sicurezza** > **Gruppi**.

### Aggiunta di elementi a un riquadro {#adding-items-to-a-tile}

Per alcuni riquadri, è possibile aggiungere più di un oggetto. Ad esempio, è possibile avere più flussi di lavoro o esperienze in esecuzione allo stesso tempo.

Per aggiungere elementi a un riquadro:

1. In **Progetti**, passa al progetto e seleziona la freccia giù nel riquadro a cui desideri aggiungere un elemento.

   ![Aggiungere un elemento a un riquadro](/help/sites-cloud/authoring/assets/project-workflows.png)

1. Aggiungi un elemento alla tessera come faresti quando crei una tessera. I riquadri di progetto sono descritti [qui](/help/sites-cloud/authoring/projects/overview.md#project-tiles). In questo esempio è stato aggiunto un altro flusso di lavoro.

### Apertura di un riquadro {#opening-a-tile}

È possibile visualizzare gli elementi inclusi nel riquadro selezionato, modificarli o eliminarli.

Per aprire un riquadro e visualizzare o modificare gli elementi:

1. Nella console Progetti, seleziona l’icona con i puntini di sospensione (...) nella parte inferiore della scheda.

   ![Apertura di un riquadro](/help/sites-cloud/authoring/assets/project-links.png)

1. AEM mostra l’elenco degli elementi inclusi nel riquadro. Per modificarli o eliminarli, entra nella modalità di selezione.

   ![Riquadro aperto](/help/sites-cloud/authoring/assets/projects-add-link.png)

## Visualizzazione delle statistiche di un progetto {#viewing-project-statistics}

È possibile visualizzare le statistiche del progetto nella console **Progetti**.

### Visualizzazione della timeline di un progetto {#viewing-a-project-timeline}

La timeline di un progetto fornisce informazioni sull’ultimo utilizzo delle risorse del progetto. Per visualizzare la sequenza temporale del progetto, seleziona **Sequenza temporale**, quindi entra nella modalità di selezione e seleziona il progetto. Le risorse vengono visualizzate nel riquadro a sinistra. Seleziona **Timeline** per tornare alla console **Progetti**.

![Timeline del progetto](/help/sites-cloud/authoring/assets/projects-timeline.png)

### Visualizzazione di progetti attivi e inattivi {#viewing-active-inactive-projects}

Per visualizzare i progetti attivi o inattivi, dalla console **Progetti** fai clic su **Mostra/nascondi progetti attivi**. Se l’icona è affiancata da un segno di spunta, stai visualizzando i progetti attivi.

![Pulsante Mostra/nascondi progetti attivi](/help/sites-cloud/authoring/assets/projects-active.png)

Se l’icona è affiancata da una x, stai visualizzando i progetti inattivi.

![Pulsante Mostra/nascondi progetti non attivi](/help/sites-cloud/authoring/assets/projects-inactive.png)

## Rendere i progetti inattivi o attivi {#making-projects-inactive-or-active}

Se hai completato un progetto ma desideri mantenere le informazioni ad esso associate, puoi renderlo inattivo.

Per rendere un progetto inattivo (o attivo):

1. Nella console **Progetti**, apri il progetto e quindi individua il riquadro **Informazioni progetto**.

   >[!NOTE]
   >
   Potrebbe essere necessario aggiungere questo riquadro, se non è già presente nel progetto. Consulta [Aggiunta di riquadri](#adding-items-to-a-tile).

1. Seleziona **Modifica**.
1. Cambia il selettore da **Attivo** a **Inattivo** (o viceversa).

   ![Attivazione di un progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Seleziona **Fine** per salvare le modifiche.
