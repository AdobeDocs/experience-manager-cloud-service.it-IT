---
title: Creazione guidata di un progetto
description: Scopri la procedura guidata di creazione del progetto per velocizzare la configurazione del tuo progetto dopo aver creato il programma di produzione.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 96%

---

# Creazione guidata di un progetto {#project-creation-wizard}

Dopo aver creato il programma di produzione, Cloud Manager offre una procedura guidata per creare un progetto AEM minimo basato sull’[archetipo del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) e iniziare subito.

Segui questi passaggi per creare un progetto di applicazione AEM in Cloud Manager seguendo la procedura guidata.

1. Crea un programma di produzione seguendo i passaggi riportati nel documento [Creazione di programmi di produzione](creating-production-programs.md)

1. Dopo aver completato la configurazione del programma, accedi alla schermata **Panoramica** del programma e apri la scheda di invito all’azione **Crea ramo e progetto** nella parte superiore.

   ![Invito all’azione della procedura guidata](assets/create-wizard1.png)

1. Per avviare la procedura guidata, fai clic su **Crea** e, nella finestra **Crea ramo e progetto**, conferma **Titolo** e **Nome nuovo ramo** del progetto.

   ![Crea ramo e progetto](assets/create-wizard2.png)

1. Se necessario, fai clic sul divisore per visualizzare i parametri aggiuntivi del progetto. I valori predefiniti vengono forniti dall’archetipo del progetto AEM e in genere non è necessario modificarli.

   ![Parametri aggiuntivi del progetto](assets/create-wizard5.png)

1. Per avviare il processo di creazione del progetto, fai clic su **Crea**.


Ora la scheda **Creazione progetto in corso** sostituisce la scheda di invito all’azione **Crea ramo e progetto** nella parte superiore della schermata **Panoramica programma**.

![Creazione del progetto in corso](assets/create-wizard3.png)

Dopo aver completato la creazione del programma, la scheda **Aggiungi ambiente** sostituisce la scheda **Creazione del progetto in corso** nella parte superiore della schermata **Panoramica programma**.

![Aggiungi ambiente](assets/create-wizard4.png)

Ora hai aggiunto all’archivio Git un progetto AEM basato sull’archetipo AEM, da utilizzare come base di sviluppo per il tuo progetto. Ora puoi creare ambienti in cui distribuire il codice del progetto.

Per informazioni su come aggiungere o gestire gli ambienti, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md).

>[!NOTE]
>
>La procedura guidata è disponibile solo per i programmi di produzione. Per i [programmi sandbox](introduction-sandbox-programs.md#auto-creation), la procedura guidata non è necessaria in quanto già includono la creazione automatica del progetto.