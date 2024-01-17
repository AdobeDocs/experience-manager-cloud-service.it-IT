---
title: Creazione di programmi sandbox
description: Scopri come creare un programma sandbox personalizzato da usare per formazione, demo, POC o altre finalità non di produzione con Cloud Manager.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 86%

---

# Creazione di programmi sandbox {#create-sandbox-program}

Un programma sandbox viene tipicamente creato per scopi di formazione, esecuzione di demo, attivazione, POC o documentazione e non è quindi destinato a contenere traffico in tempo reale.

Per ulteriori informazioni sui tipi di programmi, consulta il documento [Informazioni su programmi e tipi di programmi.](program-types.md)

## Creazione di un programma sandbox {#create}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** schermo, tocca o fai clic su **Aggiungi programma** nell&#39;angolo superiore destro dello schermo.

   ![Pagina di destinazione di Cloud Manager](assets/cloud-manager-my-programs.png)

1. Dalla procedura guidata Crea programma, seleziona **Configura una sandbox** e assegna un nome al programma.

   ![Creazione del tipo di programmi](assets/create-sandbox.png)

1. Facoltativamente, puoi aggiungere un’immagine al programma trascinando un file di immagine sul target **Aggiungi un’immagine del programma** o facendo clic su di esso per aggiungere un’immagine da un browser del file. Seleziona **Continua**.

   * L’immagine funge solo da titolo nella finestra di panoramica del programma e aiuta a identificarlo.

1. In **Configurare la sandbox** selezionare le soluzioni da abilitare nel programma sandbox selezionando le opzioni nella finestra di dialogo **Soluzioni e componenti aggiuntivi** tabella.

   * Utilizza le frecce accanto ai nomi delle soluzioni per visualizzare ulteriori componenti aggiuntivi facoltativi per le soluzioni.

   * Le soluzioni **Sites** e **Assets** sono sempre incluse nei programmi sandbox e non possono essere deselezionate.

   ![Selezionare soluzioni e componenti aggiuntivi per una sandbox](assets/sandbox-solutions-add-ons.png)

1. Dopo aver selezionato le soluzioni e i componenti aggiuntivi per il programma sandbox, fai clic su **Crea**.

Nella pagina di destinazione viene visualizzata una nuova scheda del programma sandbox e un indicatore di stato che mostra l’avanzamento del processo di configurazione.

![Creazione di un programma sandbox dalla pagina Panoramica](assets/sandbox-setup.png)

## Accesso alla sandbox {#access}

Dalla pagina di panoramica del programma, è possibile visualizzare i dettagli della configurazione sandbox e accedere all’ambiente (non appena disponibile).

1. Dalla pagina di destinazione di Cloud Manager, fai clic sul pulsante con i puntini di sospensione del programma creato.

   ![Accesso alla panoramica del programma](assets/program-overview-sandbox.png)

1. Dopo aver completato la procedura di creazione del progetto, puoi utilizzare l’archivio Git accedendo al collegamento **Accedi alle informazioni sull’archivio**.

   ![Configurazione del programma](assets/create-program4.png)

   >[!TIP]
   >
   >Per ulteriori informazioni sull’accesso e la gestione dell’archivio Git, consulta [Accesso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Dopo aver creato l’ambiente di sviluppo, è possibile utilizzare il collegamento **Accedi a AEM** per accedere a AEM.

   ![Collegamento per l’accesso a AEM](assets/create-program-5.png)

1. Dopo aver completato la distribuzione della pipeline non di produzione nell’ambiente di sviluppo, la procedura guidata indica di accedere all’ambiente di sviluppo AEM o di distribuire il codice.

   ![Distribuzione del programma sandbox](assets/create-program-setup-deploy.png)

Se devi passare a un altro programma o tornare alla pagina della panoramica per crearne uno nuovo, fai clic sul nome del programma in alto a sinistra nella schermata per visualizzare l’opzione **Accedi a**.

![Accedi a](assets/create-program-a1.png)
