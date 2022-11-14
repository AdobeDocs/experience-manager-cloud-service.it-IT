---
title: Creazione di programmi sandbox
description: Scopri come creare un programma sandbox personalizzato da usare per formazione, demo, POC o altre finalità non di produzione con Cloud Manager.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 100%

---

# Creazione di programmi sandbox {#create-sandbox-program}

Un programma sandbox viene tipicamente creato per scopi di formazione, esecuzione di demo, attivazione, POC o documentazione e non è quindi destinato a contenere traffico in tempo reale.

Per ulteriori informazioni sui tipi di programmi, consulta il documento [Informazioni su programmi e tipi di programmi.](program-types.md)

## Creazione di un programma sandbox {#create}

Per creare un programma sandbox, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Dalla pagina di destinazione di Cloud Manager, fai clic su **Aggiungi programma** nell’angolo in alto a destra della schermata.

   ![Pagina di destinazione di Cloud Manager](assets/first_timelogin1.png)

1. Dalla procedura guidata Crea programma, seleziona **Configura programma sandbox**, assegna un nome al programma, quindi fai clic su **Crea**.

   ![Creazione dei tipi di programmi](assets/create-sandbox.png)

Nella pagina di destinazione viene visualizzata una nuova scheda del programma sandbox e un indicatore di stato che mostra l’avanzamento del processo di configurazione.

![Creazione di un programma sandbox dalla pagina Panoramica](assets/program-create-setupdemo2.png)

## Accesso al programma sandbox {#access}

Visualizzando la pagina di panoramica del programma, è possibile visualizzare i dettagli della configurazione sandbox e accedere all’ambiente (non appena disponibile).

1. Dalla pagina di destinazione di Cloud Manager, fai clic sul pulsante con i puntini di sospensione del programma appena creato.

   ![Panoramica sull’accesso al programma](assets/program-overview-sandbox.png)

1. Dopo aver completato la procedura di creazione del progetto, puoi utilizzare l’archivio Git accedendo al collegamento **Accedi a dati archivio**.

   ![Configurazione del programma](assets/create-program4.png)

   >[!TIP]
   >
   >Per ulteriori informazioni sull’accesso e la gestione dell’archivio Git, consulta il documento [Accesso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Dopo aver creato l’ambiente di sviluppo, è possibile utilizzare il collegamento **Accedi a AEM** per accedere a AEM.

   ![Collegamento per l’accesso a AEM](assets/create-program-5.png)

1. Dopo aver completato la distribuzione della pipeline non di produzione nell’ambiente di sviluppo, la procedura guidata indica di accedere all’ambiente di sviluppo AEM o di distribuire il codice.

   ![Distribuzione del programma sandbox](assets/create-program-setup-deploy.png)

Se in qualsiasi momento è necessario passare a un altro programma o tornare alla pagina della panoramica per crearne uno nuovo, fai clic sul nome del programma nella parte superiore sinistra della schermata per visualizzare l’opzione **Accedi a**.

![Accedi a](assets/create-program-a1.png)
