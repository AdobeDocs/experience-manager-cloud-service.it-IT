---
title: 'Creazione di programmi sandbox '
description: Scopri come utilizzare Cloud Manager per creare un tuo programma sandbox per scopi di formazione, demo, POC o per altri scopi non di produzione.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Creazione di programmi sandbox {#create-sandbox-program}

Generalmente, un programma sandbox viene creato per scopi di formazione, demo in esecuzione, abilitazione, POC o documentazione e non è destinato a trasportare traffico live.

Ulteriori informazioni sui tipi di programma nel documento [Informazioni sui tipi di programma e di programma.](program-types.md)

## Creare un programma sandbox {#create}

Segui questi passaggi per creare un programma sandbox.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Dalla pagina di destinazione di Cloud Manager, fai clic su **Aggiungi programma** nell’angolo in alto a destra dello schermo.

   ![Pagina di destinazione di Cloud Manager](assets/first_timelogin1.png)

1. Dalla procedura guidata Crea programma, seleziona **Configurare una sandbox**, specificare un nome di programma e quindi fare clic su **Crea**.

   ![Creazione del tipo di programma](assets/create-sandbox.png)

Nella pagina di destinazione verrà visualizzata una nuova scheda del programma sandbox con un indicatore di stato durante il processo di configurazione.

![Creazione di sandbox dalla pagina della panoramica](assets/program-create-setupdemo2.png)

## Accedere alla sandbox {#access}

Puoi visualizzare i dettagli della configurazione della sandbox e accedere all’ambiente (una volta disponibile) visualizzando la pagina di panoramica del programma.

1. Dalla pagina di destinazione di Cloud Manager, fai clic sul pulsante con i puntini di sospensione nel programma appena creato.

   ![Panoramica sull’accesso al programma](assets/program-overview-sandbox.png)

1. Al termine del passaggio di creazione del progetto, puoi accedere al **Accesso alle informazioni sul repository** per poter utilizzare il tuo archivio git.

   ![Configurazione del programma](assets/create-program4.png)

   >[!TIP]
   >
   >Per ulteriori informazioni sull’accesso e la gestione dell’archivio Git, consulta il documento [Accesso a Git.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. Una volta creato l’ambiente di sviluppo, puoi utilizzare la funzione **AEM di accesso** collegamento per accedere a AEM.

   ![Collegamento AEM accesso](assets/create-program-5.png)

1. Una volta completata l’implementazione della pipeline non di produzione per lo sviluppo, la procedura guidata ti guida ad accedere all’ambiente di sviluppo AEM o a distribuire il codice nell’ambiente di sviluppo.

   ![Distribuzione di sandbox](assets/create-program-setup-deploy.png)

Se in qualsiasi momento è necessario passare a un altro programma o tornare alla pagina di panoramica per creare un altro programma, fai clic sul nome del programma in alto a sinistra dello schermo per visualizzare il **Passa a** opzione .

![Accedi a](assets/create-program-a1.png)
