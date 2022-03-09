---
title: Creazione guidata progetto
description: Scopri la procedura guidata di creazione del progetto per velocizzare la configurazione del progetto dopo la creazione del programma di produzione.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: 93cb0ffa87f2338518c2a23de4e0a692031e1a71
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Creazione guidata progetto {#project-creation-wizard}

Dopo aver creato il programma di produzione, Cloud Manager offre una procedura guidata per creare un progetto AEM minimo basato su [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) per iniziare rapidamente.

Segui questi passaggi per creare un progetto di applicazione AEM in Cloud Manager utilizzando la procedura guidata.

1. Crea un programma di produzione seguendo i passaggi del documento [Creazione di programmi di produzione](creating-production-programs.md)

1. Una volta completata la configurazione del programma, accedi al **Panoramica** dello schermo del programma e visualizzare **Crea ramo e progetto** scheda call-to-action nella parte superiore.

   ![Assistenza telefonica per la procedura guidata](assets/create-wizard1.png)

1. Fai clic su **Crea** per avviare la procedura guidata e confermare l’impostazione del progetto **Titolo** e **Nuovo nome della filiale** in **Creare un ramo e un progetto** finestra.

   ![Creare un ramo e un progetto](assets/create-wizard2.png)

1. Facoltativamente, fai clic sul divisore per visualizzare i parametri aggiuntivi del progetto. I valori predefiniti vengono forniti dall’Archetipo di progetto AEM e in genere non è necessario modificarli.

   ![Parametri di progetto aggiuntivi](assets/create-wizard5.png)

1. Fai clic su **Crea** per avviare il processo di creazione del progetto.


A **Creazione di progetti in corso** la scheda ora sostituisce la **Crea ramo e progetto** scheda call-to-action come parte superiore del **Panoramica del programma** schermo.

![Creazione del progetto in corso](assets/create-wizard3.png)

Una volta completata la creazione del programma, un **Aggiungi ambiente** la carta sostituisce **Creazione di progetti in corso** scheda nella parte superiore della **Panoramica del programma** schermo.

![Aggiungi ambiente](assets/create-wizard4.png)

Ora disponi di un progetto AEM basato sull’archetipo AEM aggiunto all’archivio Git per fungere da base di sviluppo per il tuo progetto. Ora puoi creare gli ambienti in cui puoi distribuire il codice del progetto.

Fare riferimento al documento [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) per scoprire come aggiungere o gestire gli ambienti.

>[!NOTE]
>
>La procedura guidata è disponibile solo per i programmi di produzione. Perché [programmi sandbox](introduction-sandbox-programs.md#auto-creation) include la creazione automatica del progetto. La procedura guidata non è necessaria.