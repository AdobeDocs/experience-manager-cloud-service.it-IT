---
title: Creare programmi sandbox
description: Scopri come creare un programma sandbox personalizzato da usare per formazione, demo, POC o altre finalità non di produzione con Cloud Manager.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 15%

---

# Creare programmi sandbox {#create-sandbox-program}

Un programma sandbox viene generalmente creato a scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione e non è destinato a contenere traffico in tempo reale. Vedi [Introduzione ai programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).

Ulteriori informazioni sui tipi di programmi nel documento [Informazioni su programmi e tipi di programmi](program-types.md).

## Creare un programma sandbox {#create}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, nell&#39;angolo superiore destro, fare clic su **Aggiungi programma**.

   ![Pagina di destinazione di Cloud Manager](assets/log-in.png)

1. Nella procedura guidata *Crea il programma*, nel campo di testo **Nome programma**, digita il nome desiderato per il programma.

1. In **Obiettivo programma**, seleziona ![Icona bacchetta magica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MagicWand_18_N.svg) **Configura sandbox**.

   ![Creazione del tipo di programmi](assets/create-sandbox.png)

1. (Facoltativo) Nell&#39;angolo inferiore destro della finestra di dialogo della procedura guidata, effettuate una delle seguenti operazioni:

   * Trascina e rilascia un file di immagine sull&#39;![icona immagine](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **Aggiungi un&#39;immagine del programma** di destinazione.
   * Fai clic sull&#39;![icona immagine](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **Aggiungi un&#39;immagine del programma**, quindi seleziona un&#39;immagine da un browser di file.
   * Fai clic su ![Icona Elimina](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) per rimuovere un&#39;immagine aggiunta.

1. Fai clic su **Continua**.

1. Nella casella di riepilogo **Soluzioni e componenti aggiuntivi** selezionare una o più soluzioni da includere nel programma.

   * Fai clic sulla freccia a sinistra del nome di una soluzione per visualizzare eventuali componenti aggiuntivi opzionali disponibili che desideri includere con una soluzione selezionata.
   * Le soluzioni **Sites**, **Assets** e **Edge Delivery Services** sono sempre selezionate per impostazione predefinita quando si crea un programma sandbox. Non è possibile deselezionarli.

   ![Selezionare soluzioni e componenti aggiuntivi per una sandbox](assets/sandbox-solutions-add-ons.png)

1. Fai clic su **Crea**. Cloud Manager crea il programma sandbox e lo visualizza nella pagina di destinazione per la selezione.

![Creazione di un programma sandbox dalla pagina Panoramica](assets/sandbox-setup.png)

## Accesso alla sandbox {#access}

Al termine della creazione di un nuovo programma sandbox, puoi visualizzare i dettagli della configurazione sandbox e accedere all’ambiente visualizzando la pagina di panoramica del programma.

1. Nella pagina di destinazione di Cloud Manager, nel programma sandbox, fai clic sull&#39;icona ![Elenco più piccolo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) nel programma sandbox creato.

   ![Accesso alla panoramica del programma](assets/program-overview-sandbox.png)

1. Al termine della creazione del progetto, puoi fare clic sul collegamento **Accedi a dati archivio** per utilizzare l&#39;archivio Git.

   ![Configurazione del programma](assets/create-program4.png)

   >[!TIP]
   >
   >Per ulteriori informazioni sull&#39;accesso e la gestione dell&#39;archivio Git, vedere [Accesso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Dopo aver creato l&#39;ambiente di sviluppo, puoi fare clic su **Accedi ad AEM** e accedere ad AEM.

   ![Collegamento per l’accesso a AEM](assets/create-program5.png)

1. Al termine della distribuzione della pipeline non di produzione nell’ambiente di sviluppo, la procedura guidata di call-to-action ti guida ad accedere all’ambiente di sviluppo AEM o a distribuire il codice nell’ambiente di sviluppo.

   ![Distribuzione del programma sandbox](assets/create-program-setup-deploy.png)

>[!TIP]
>
>Consulta [Navigazione nell&#39;interfaccia utente di Cloud Manager](/help/implementing/cloud-manager/navigation.md) per informazioni dettagliate su come esplorare Cloud Manager e comprendere la console **Programmi personali**.
