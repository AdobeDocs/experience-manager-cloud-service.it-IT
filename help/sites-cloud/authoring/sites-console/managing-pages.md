---
title: Gestione delle pagine
description: Scopri come gestire le pagine del sito web in AEM, incluso lo spostamento, la copia e l’eliminazione.
exl-id: 355b60c5-a82e-4bbb-98ea-bfcc0126b7fd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 45805d4baa8b93df2225b44152fee1457b421150
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 61%

---

# Gestione delle pagine {#managing-pages}

Scopri come gestire le pagine del sito web in AEM, incluso lo spostamento, la copia e l’eliminazione.

>[!TIP]
>
>Prima di iniziare a gestire le pagine, acquisisci familiarità con [l&#39;organizzazione delle pagine in AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md).

>[!TIP]
>
>Esistono diverse [scelte rapide da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) che è possibile utilizzare dalla console dei siti Web per organizzare le pagine in modo più efficiente.

## Privilegi di accesso {#access-privileges}

Il tuo account necessita dei diritti di accesso e delle autorizzazioni adeguati per intervenire sulle pagine, ad esempio per creare, copiare, spostare, modificare ed eliminare elementi.

Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

## Apertura di una pagina per la modifica {#opening-a-page-for-editing}

Dopo aver [creato una pagina](/help/sites-cloud/authoring/sites-console/creating-pages.md) o aver visitato una pagina esistente utilizzando [la console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), puoi aprirla per la modifica.

1. Apri [la console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Passa alla pagina da modificare.
1. Seleziona la pagina mediante:

   * [Azioni rapide](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) e barra degli strumenti

1. Tocca o fai clic sull&#39;icona **Modifica**.

   Pulsante ![Modifica](/help/sites-cloud/authoring/assets/edit.png)

1. La pagina viene aperta e puoi modificarla come necessario. A seconda della modalità di creazione della pagina selezionata, l&#39;azione **Modifica** aprirà l&#39;editor appropriato.
   * [Editor pagina](/help/sites-cloud/authoring/page-editor/introduction.md) - Per le pagine create con l&#39;Editor pagina di AEM
   * [Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md) - Per le pagine create con l&#39;editor universale

## Copiare e incollare una pagina    {#copying-and-pasting-a-page}

Puoi copiare una pagina e tutte le relative sottopagine in una nuova posizione:

1. Apri [la console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Individuare la pagina da copiare.
1. Seleziona la pagina mediante:

   * [Azioni rapide](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) e barra degli strumenti

1. Tocca o fai clic sull&#39;icona della pagina **Copia**.

   ![Copia](/help/sites-cloud/authoring/assets/copy.png)

1. Passa al percorso in cui desideri inserire la nuova copia della pagina.
1. Seleziona l&#39;icona **Incolla** che è diventata disponibile.

   ![Incolla](/help/sites-cloud/authoring/assets/paste.png)

1. La finestra di dialogo Incolla presenta un riepilogo della transazione della funzione incolla e la possibilità di:
   * **Nuovo nome sito:** modificare il nome della pagina incollata
   * **Incolla senza elementi secondari:** ometti le pagine secondarie della pagina selezionata quando si incollano (per impostazione predefinita le pagine secondarie vengono incollate)

   ![Finestra di dialogo Incolla](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Seleziona il pulsante **Incolla** per confermare la transazione e creare le nuove pagine.

>[!NOTE]
>
>Se copi la pagina in un percorso in cui esiste già una pagina con lo stesso nome dell’originale, viene automaticamente generata una variante del nome aggiungendo un numero. Ad esempio, se `beach` esiste già, una nuova pagina con il nome `beach` diventerà `beach1`.

>[!NOTE]
>
>Se si avvia l’azione incolla in modalità selezione, questa viene chiusa automaticamente non appena la pagina viene copiata.

## Spostamento o ridenominazione di una pagina {#moving-or-renaming-a-page}

La procedura per spostare o rinominare una pagina è sostanzialmente la stessa ed entrambe le azioni sono gestite dalla procedura guidata Sposta pagina. Con questa procedura guidata è possibile:

* Rinominare una pagina senza spostarla.
* Sposta la pagina senza rinominarla.
* Spostarsi e rinominare contemporaneamente.

In AEM è disponibile una funzionalità che consente di aggiornare eventuali collegamenti interni che rimandano alla pagina da rinominare/spostare. Questa operazione può essere eseguita a livello di singola pagina, per assicurare la massima flessibilità.

1. Apri [la console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Individuare la pagina da spostare.
1. Seleziona la pagina mediante:

   * [Azioni rapide](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) e barra degli strumenti

1. Tocca o fai clic sull&#39;icona della pagina **Sposta** per aprire la procedura guidata Sposta pagina.

   ![Pulsante Sposta](/help/sites-cloud/authoring/assets/move.png)

1. Il passaggio **Rinomina** della procedura guidata fornisce **informazioni** sulla pagina, inclusa la data di creazione, il percorso e il numero di riferimenti diretti. Da qui puoi effettuare le seguenti operazioni:

   * Specifica il nome da assegnare alla pagina spostata, quindi seleziona **Avanti** per continuare.
   * Seleziona **Annulla** per interrompere la procedura.

   ![Spostare e rinominare la pagina](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * Il nome della pagina può rimanere invariato se si sta solo spostando la pagina.

   >[!NOTE]
   >
   >Se sposti la pagina in una posizione in cui esiste già una pagina con lo stesso nome, il sistema genera automaticamente una variante del nome aggiungendo un numero. Ad esempio, se `beach` esiste già, una nuova pagina con il nome `beach` diventerà `beach1`.

1. Dal passaggio **Seleziona destinazione** della procedura guidata puoi effettuare le seguenti operazioni:

   * Utilizza la [vista a colonne](/help/sites-cloud/authoring/basic-handling.md#column-view) per accedere alla nuova posizione della pagina:

      * Seleziona la destinazione facendo clic sulla miniatura della destinazione.
      * Fai clic su **Avanti** per continuare.

   * Utilizza **Indietro** per specificare di nuovo il nome della pagina.

   >[!NOTE]
   >
   >Per impostazione predefinita, l’elemento principale della pagina che stai spostando/rinominando viene selezionato come destinazione.

   ![Selezionare la destinazione di spostamento della pagina](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Se sposti la pagina in una posizione in cui esiste già una pagina con lo stesso nome, il sistema genera automaticamente una variante del nome aggiungendo un numero. Se, ad esempio, `winter` esiste già, `winter` diventerà `winter1`.

1. Se la pagina è collegata o utilizzata in un riferimento, oppure se è stata pubblicata, i dettagli saranno elencati nel passaggio **Regola/Ripubblica**.

   * Puoi quindi indicare cosa deve essere regolato e/o ripubblicato in base alle necessità.

   >[!NOTE]
   >
   >* Se la pagina non è collegata né è soggetta a riferimenti, questo passaggio non sarà disponibile.
   >* Questo passaggio elenca riferimenti diretti e indiretti. Questo valore può essere diverso dalla quantità riportata nel passaggio **Rinomina** della procedura guidata e dai riferimenti riportati dalla barra dei riferimenti, che in entrambi i casi segnalano solo riferimenti diretti per motivi di prestazioni.

   ![Ripubblica pagina in spostamento](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Tocca o fai clic su **Sposta** per definire quando deve essere eseguita l&#39;azione di spostamento.

   * **Ora** attiverà un [processo asincrono](#asynchronous-actions) per spostare immediatamente la pagina.
   * **Più tardi** ti consentirà di pianificare una data per l&#39;elaborazione dello spostamento.

   ![Definizione di quando spostare](assets/managing-pages-move-page-now-later.png)

1. Tocca o fai clic su **Continua** per completare lo spostamento della pagina.

>[!NOTE]
>
>Se la pagina è già stata pubblicata, lo spostamento ne determina automaticamente l’annullamento della pubblicazione. Per impostazione predefinita, viene ripubblicata al termine dello spostamento, ma questo comportamento può essere modificato deselezionando il campo **Ripubblica** nel passaggio **Regola/Ripubblica**.

>[!NOTE]
>
>La ridenominazione di una pagina è inoltre soggetta a [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nuovo nome della pagina.

>[!NOTE]
>
>Una pagina può essere spostata solo in una posizione in cui è consentito il modello su cui si basa la pagina. Per ulteriori informazioni consulta la sezione dedicata alla [disponibilità dei modelli](/help/implementing/developing/components/templates.md#template-availability).

### Azioni asincrone {#asynchronous-actions}

Le azioni di spostamento delle pagine vengono sempre elaborate in modo asincrono, consentendo all’utente di continuare a creare nell’interfaccia utente senza ostacoli.

Lo stato dei processi asincroni può essere controllato nel dashboard [**Stato processi asincroni**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) in **Navigazione globale** > **Strumenti** > **Operazioni** > **Processi**

>[!TIP]
>
>Per ulteriori informazioni sull’esecuzione asincrona dei processi e su come configurare il limite per le azioni di spostamento o ridenominazione delle pagine, consulta il documento [Processi asincroni](/help/operations/asynchronous-jobs.md) nella guida utente per le operazioni.

### Eliminazione di una pagina {#deleting-a-page}

1. Apri [la console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Passare alla pagina che si desidera eliminare.
1. Utilizza la [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) per selezionare la pagina richiesta, quindi utilizza **Elimina** dalla barra degli strumenti:

   ![Pulsante Elimina](/help/sites-cloud/authoring/assets/delete.png)

1. Una finestra di dialogo chiederà una conferma.

   ![Finestra di dialogo Elimina](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Intendi archiviare le pagine prima di eliminarle?** - Se questa opzione è selezionata, al momento dell’eliminazione verranno create versioni delle pagine selezionate da eliminare.
      * [Le versioni possono essere ripristinate in un momento successivo](/help/sites-cloud/authoring/sites-console/page-versions.md).
      * Le pagine eliminate senza versioni precedenti non possono essere ripristinate.
1. Tocca o fai clic su **Annulla** per interrompere l&#39;azione o su **Elimina** per confermare l&#39;azione.
   * Se la pagina non contiene riferimenti, viene eliminata.
   * Se la pagina contiene riferimenti, verrà visualizzata una finestra di messaggio per informare che **Si fa riferimento a una o più pagine.** È possibile selezionare **Forza eliminazione** o **Annulla**.

>[!NOTE]
>
>Se una pagina è già stata pubblicata, prima di eliminarla ne verrà automaticamente annullata la pubblicazione.

### Blocco di una pagina   {#locking-a-page}

È possibile [bloccare/sbloccare una pagina](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page) da una console o quando si modifica una singola pagina. L’indicazione relativa al fatto che una pagina sia bloccata o meno è visualizzata in entrambe le posizioni.

![Pulsante Blocca](/help/sites-cloud/authoring/assets/lock.png)
![Pulsante Sblocca](/help/sites-cloud/authoring/assets/unlock.png)

### Creazione di una nuova cartella {#creating-a-new-folder}

Puoi creare cartelle per organizzare file e pagine.

1. Apri [la console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Passa alla posizione desiderata.
1. Per aprire l’elenco delle opzioni, seleziona **Crea** dalla barra degli strumenti
1. Seleziona **Cartella** per aprire la finestra di dialogo. Nella finestra puoi immettere il **Nome** e il **Titolo**:

   ![Crea cartella](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Seleziona **Crea** per creare la nuova cartella.

>[!NOTE]
>
>* Le cartelle sono inoltre soggette a [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nome della nuova cartella.
>* Le cartelle possono essere create solo direttamente in **Sites** o in altre cartelle. Non possono essere create sotto una pagina.
>* Le azioni standard Sposta, Copia, Incolla, Elimina, Modifica, Pubblica, Annulla pubblicazione e Visualizza/Modifica proprietà possono essere eseguite in una cartella.
>* Le cartelle non sono disponibili per la selezione all’interno di una Live Copy.
