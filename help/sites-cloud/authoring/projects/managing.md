---
title: Gestione dei progetti
description: Progetti consente di organizzare un progetto raggruppando le risorse in un’unica entità, accessibile e gestibile nella console dedicata
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 49%

---

# Gestione dei progetti {#managing-projects}

Progetti consente di organizzare il progetto raggruppando le risorse in un’unica entità.

In **Progetti** , puoi accedere ai tuoi progetti e intervenire su di essi:

![Console Progetti](/help/sites-cloud/authoring/assets/projects-console.png)

In Progetti puoi creare un progetto, associare risorse al progetto ed eliminare anche un progetto o collegamenti a risorse. È possibile aprire una tessera per visualizzarne il contenuto e aggiungere elementi a una tessera. In questo argomento vengono descritte tali procedure.

## Creazione di un progetto {#creating-a-project}

Per impostazione predefinita, AEM fornisce questi modelli tra cui scegliere quando si crea un progetto:

* Progetto semplice
* Progetto multimediale
* Progetto di traduzione

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

La procedura di creazione di un progetto è la stessa per ciascun progetto. La differenza tra i tipi di progetti include i [ruoli utente](/help/sites-cloud/authoring/projects/overview.md) e i [flussi di lavoro](/help/sites-cloud/authoring/projects/workflows.md) disponibili.  Per creare un nuovo progetto:

1. In **Progetti**, tocca o fai clic su **Crea** per aprire la procedura guidata **Crea progetto**:
1. Seleziona un modello e fai clic su **Avanti**.

   ![Creazione di un progetto](/help/sites-cloud/authoring/assets/projects-create.png)

1. Definisci un **titolo** e una **descrizione**; se necessario, aggiungi un’immagine di **miniatura**. Puoi anche aggiungere o eliminare utenti e il gruppo a cui appartengono. Inoltre, fai clic su **Avanzate** per aggiungere un nome utilizzato nell&#39;URL.

   ![Aggiunta di dettagli al progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Tocca o fai clic su **Crea**. La conferma chiede se desideri aprire il nuovo progetto o tornare alla console.

### Associazione delle risorse al progetto {#associating-resources-with-your-project}

Poiché i progetti consentono di raggruppare le risorse in un’unica entità, è necessario associare le risorse al progetto. Queste risorse vengono chiamate **Riquadri**. I tipi di risorse che è possibile aggiungere sono descritti in [Riquadri progetto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

Per associare le risorse al progetto:

1. Apri il progetto da **Progetti** console.
1. Tocca o fai clic **Aggiungi sezione** e seleziona il riquadro da collegare al progetto. È possibile selezionare tra più tipi di riquadri.

   ![Aggiunta di un riquadro a un progetto](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >I riquadri associabili a un progetto sono descritti dettagliatamente nella sezione [Riquadri di progetto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

1. Tocca o fai clic su **Crea**. La risorsa è ora collegata al progetto e accessibile da questo.

### Eliminazione di un progetto o di un collegamento di risorsa {#deleting-a-project-or-resource-link}

Per eliminare un progetto dalla console o una risorsa collegata dal progetto si applica lo stesso metodo:

1. Passa alla posizione appropriata:

   * Per eliminare un progetto, vai al livello superiore della sezione **Progetti** console.
   * Per eliminare un collegamento di risorsa all’interno di un progetto, apri il progetto nella console **Progetti**.

1. Entra nella modalità di selezione facendo clic su **Seleziona** e scegli il progetto o collegamento di risorsa.
1. Tocca o fai clic su **Elimina**.

1. È necessario confermare l’eliminazione in una finestra di dialogo. Se confermato, il progetto o il collegamento di risorsa viene eliminato. Per uscire dalla modalità di selezione, tocca o fai clic su **Deseleziona**.

>[!NOTE]
>
>Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate. Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi: **Proprietari mioprogetto**, **Editor mioprogetto**, **Osservatori mioprogetto**. Tuttavia, se il progetto viene eliminato, tali gruppi non vengono rimossi automaticamente. Un amministratore deve eliminare manualmente i gruppi da **Strumenti** > **Protezione** > **Gruppi**.

### Aggiunta di elementi a una sezione {#adding-items-to-a-tile}

In alcuni riquadri, potrebbe essere necessario aggiungere più elementi. Ad esempio, puoi avere più di un flusso di lavoro in esecuzione alla volta o più di un’esperienza.

Per aggiungere elementi a un riquadro:

1. In **Progetti**, individua quello di tuo interesse e fai clic sulle freccette in basso del riquadro in cui desideri aggiungere un elemento.

   ![Aggiungere un elemento a un riquadro](/help/sites-cloud/authoring/assets/project-workflows.png)

1. Aggiungi un elemento alla sezione come faresti quando crei una nuova sezione. Sono descritte le tessere del progetto [qui](/help/sites-cloud/authoring/projects/overview.md#project-tiles). In questo esempio è stato aggiunto un altro flusso di lavoro.

### Apertura di una sezione {#opening-a-tile}

Puoi visualizzare gli elementi inclusi in una sezione corrente oppure modificare o eliminare gli elementi nella sezione.

Per aprire una tessera in modo da poter visualizzare o modificare gli elementi:

1. Nella console Progetti, tocca o fai clic sull’icona con i puntini di sospensione (...) nella parte inferiore della scheda.

   ![Apertura di un riquadro](/help/sites-cloud/authoring/assets/project-links.png)

1. L&#39;AEM elenca gli elementi di quella sezione. È possibile attivare la modalità di selezione per modificare o eliminare gli elementi.

   ![Riquadro aperto](/help/sites-cloud/authoring/assets/projects-add-link.png)

## Visualizzazione delle statistiche di un progetto {#viewing-project-statistics}

È possibile visualizzare le statistiche del progetto nella console **Progetti**.

### Visualizzazione della sequenza temporale di un progetto {#viewing-a-project-timeline}

La timeline del progetto fornisce informazioni sull’ultimo utilizzo delle risorse del progetto. Per visualizzare la timeline di un progetto, tocca o fai clic su **Timeline**, quindi entra nella modalità di selezione e scegli il progetto. Le risorse vengono visualizzate nel riquadro a sinistra. Per tornare alla console **Progetti**, tocca o fai clic su **Timeline**.

![Timeline del progetto](/help/sites-cloud/authoring/assets/projects-timeline.png)

### Visualizzazione di progetti attivi e inattivi {#viewing-active-inactive-projects}

Per visualizzare i progetti attivi o inattivi, dalla console **Progetti** fai clic su **Mostra/nascondi progetti attivi**. Se l’icona è affiancata da un segno di spunta, stai visualizzando i progetti attivi.

![Pulsante Mostra/nascondi progetti attivi](/help/sites-cloud/authoring/assets/projects-active.png)

Se l’icona è affiancata da una x, stai visualizzando i progetti inattivi.

![Pulsante Mostra/nascondi progetti non attivi](/help/sites-cloud/authoring/assets/projects-inactive.png)

## Rendere i progetti inattivi o attivi {#making-projects-inactive-or-active}

Potrebbe essere utile disattivare un progetto dopo averlo completato, ma si desidera comunque mantenere le informazioni relative al progetto.

Per rendere un progetto inattivo (o attivo):

1. In **Progetti** , apri il progetto e quindi individua **Informazioni progetto** affiancare.

   >[!NOTE]
   Potrebbe essere necessario aggiungere questo riquadro, se non è già presente nel progetto. Consulta [Aggiunta di riquadri](#adding-items-to-a-tile).

1. Tocca o fai clic su **Modifica**.
1. Modifica il selettore passando da **Attivo** a **Inattivo** (o viceversa).

   ![Attivazione di un progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Tocca o fai clic su **Fine** per salvare le modifiche apportate.
