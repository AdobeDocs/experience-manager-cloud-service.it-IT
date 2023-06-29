---
title: Creazione di programmi sandbox
description: Scopri come creare un programma sandbox personalizzato da usare per formazione, demo, POC o altre finalità non di produzione con Cloud Manager.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 48%

---

# Creazione di programmi sandbox {#create-sandbox-program}

Un programma sandbox viene tipicamente creato per scopi di formazione, esecuzione di demo, attivazione, POC o documentazione e non è quindi destinato a contenere traffico in tempo reale.

Per ulteriori informazioni sui tipi di programmi, consulta il documento [Informazioni su programmi e tipi di programmi.](program-types.md)

## Creazione di un programma sandbox {#create}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Dalla pagina di destinazione di Cloud Manager, nell’angolo superiore destro della schermata, fai clic su **Aggiungi programma**.

   ![Pagina di destinazione di Cloud Manager](assets/cloud-manager-my-programs.png)

1. Dalla procedura guidata Crea programma, seleziona **Configurare una sandbox** e fornisci un nome per il programma.

   ![Creazione del tipo di programmi](assets/create-sandbox.png)

1. Facoltativamente, puoi aggiungere un’immagine al programma trascinando un file di immagine sul target **Aggiungi un’immagine del programma** o facendo clic su di esso per aggiungere un’immagine da un browser del file. Tocca o fai clic su **Continua**.

   * L’immagine funge solo da titolo nella finestra di panoramica del programma e aiuta a identificarlo.

1. In **Configurare la sandbox** selezionare le soluzioni da abilitare nel programma sandbox selezionando le opzioni nella finestra di dialogo **Soluzioni e componenti aggiuntivi** tabella.

   * Utilizza le virgolette acute accanto ai nomi delle soluzioni per visualizzare ulteriori componenti aggiuntivi facoltativi per le soluzioni.

   * Il **Sites** e **Risorse** le soluzioni sono sempre incluse nei programmi sandbox e non possono essere deselezionate.

   ![Selezionare soluzioni e componenti aggiuntivi per una sandbox](assets/sandbox-solutions-add-ons.png)

1. Dopo aver selezionato soluzioni e componenti aggiuntivi per il programma sandbox, fai clic su **Crea**.

Nella pagina di destinazione viene visualizzata una nuova scheda del programma sandbox con un indicatore di stato che mostra l’avanzamento del processo di configurazione.

![Creazione di un programma sandbox dalla pagina Panoramica](assets/sandbox-setup.png)

## Accesso alla sandbox {#access}

Una volta disponibile, puoi visualizzare i dettagli della configurazione sandbox e accedere all’ambiente visualizzando la pagina di panoramica del programma.

1. Dalla pagina di destinazione di Cloud Manager, fai clic sul pulsante con i puntini di sospensione del programma appena creato.

   ![Panoramica sull’accesso al programma](assets/program-overview-sandbox.png)

1. Al termine della fase di creazione del progetto, puoi accedere a **Accedi a dati archivio** per poter utilizzare l’archivio Git.

   ![Configurazione del programma](assets/create-program4.png)

   >[!TIP]
   >
   >Per ulteriori informazioni sull’accesso e la gestione dell’archivio Git, consulta [Accesso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Dopo aver creato l’ambiente di sviluppo, è possibile utilizzare il collegamento **Accedi a AEM** per accedere a AEM.

   ![Collegamento per l’accesso a AEM](assets/create-program-5.png)

1. Dopo aver completato la distribuzione della pipeline non di produzione nell’ambiente di sviluppo, la procedura guidata indica di accedere all’ambiente di sviluppo AEM o di distribuire il codice.

   ![Distribuzione del programma sandbox](assets/create-program-setup-deploy.png)

Se devi passare a un altro programma o tornare alla pagina della panoramica per crearne uno nuovo, fai clic sul nome del programma nella parte superiore sinistra della schermata per visualizzare **Accedi a** opzione.

![Accedi a](assets/create-program-a1.png)
