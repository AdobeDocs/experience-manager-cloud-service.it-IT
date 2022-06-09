---
title: 'Creazione di programmi di produzione '
description: Scopri come utilizzare Cloud Manager per creare un tuo programma di produzione per ospitare il traffico live.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: 3557ddbc76ff21bcfe4ac0338f116b02b5135f2c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---


# Creazione di programmi di produzione {#create-production-program}

Un programma di produzione è destinato a un utente che ha dimestichezza con AEM e Cloud Manager ed è pronto per iniziare a scrivere, creare e testare il codice allo scopo di distribuirlo per ospitare il traffico live.

Ulteriori informazioni sui tipi di programma nel documento [Informazioni sui tipi di programma e di programma.](program-types.md)

## Tutorials video {#video-tutorials}

Puoi guardare questi due video tutorial per scoprire come creare un programma in Cloud Manager o [segui le nostre istruzioni documentate.](#create)

>[!VIDEO](https://video.tv.adobe.com/v/334953)

>[!VIDEO](https://video.tv.adobe.com/v/334954)

## Creare un programma di produzione {#create}

Segui questi passaggi per creare un programma di produzione.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Fai clic su **Aggiungi programma** dall’angolo in alto a destra dello schermo.

   ![Pagina di destinazione di Cloud Manager](assets/first_timelogin1.png)

1. Seleziona **Configurazione per la produzione** nella procedura guidata Crea programma per creare un programma di produzione. È possibile accettare il nome predefinito del programma o modificarlo prima di fare clic su **Continua**.

   ![Creazione guidata programma](assets/create-prod1.png)

1. Sulla **Soluzioni e componenti aggiuntivi** seleziona le soluzioni da includere nel programma.

   ![Selezionare le soluzioni](assets/setup-prod-select.png)

1. Fai clic sulla freccia prima dei nomi delle soluzioni per visualizzare i componenti aggiuntivi facoltativi, ad esempio selezionando la **Commerce** opzione add-on in **Sites**.

   ![Seleziona componenti aggiuntivi](assets/setup-prod-commerce.png)

1. Con le soluzioni e i componenti aggiuntivi selezionati, fai clic su **Continua**.

1. Sulla **Data di pubblicazione** , immetti la data in cui pianifichi la pubblicazione del programma di produzione.

   ![Definire la data di pubblicazione pianificata](assets/setup-go-live.png)

   * Questa data può essere modificata in qualsiasi momento.
   * Questa data è solo per uso informativo e attiva il widget Go Live sulla pagina di panoramica del programma per fornire collegamenti all’interno del prodotto alla documentazione sulle best practice as a Cloud Service in modo tempestivo per allinearsi con il percorso che culmina in un’esperienza Go Live di successo e fluida.

1. Fai clic su **Crea**.

Il programma viene creato da Cloud Manager e viene visualizzato e selezionato nella pagina di destinazione.

![Panoramica di Cloud Manager](assets/navigate-cm.png)

## Accedere al programma {#acessing}

1. Una volta visualizzata la scheda del programma nella pagina di destinazione, seleziona il pulsante dei puntini di sospensione per visualizzare le opzioni del menu disponibili.

   ![Panoramica del programma](assets/program-overview.png)

1. Seleziona **Panoramica del programma** per passare a Cloud Manager’s **Panoramica** pagina.

1. La scheda di chiamata all’azione principale nella pagina della panoramica ti guiderà attraverso la creazione di un ambiente, una pipeline non di produzione e, infine, una pipeline di produzione.

   ![Panoramica del programma](assets/set-up-prod5.png)

Se in qualsiasi momento è necessario passare a un altro programma o tornare alla pagina di panoramica per creare un altro programma, fai clic sul nome del programma in alto a sinistra dello schermo per visualizzare il **Passa a** opzione .

![Accedi a](assets/create-program-a1.png)

>[!NOTE]
>
>A differenza di [programma sandbox,](introduction-sandbox-programs.md#auto-creation) un programma di produzione richiederà all’utente il ruolo adeguato di Cloud Manager di creare il progetto e aggiungere un ambiente tramite l’interfaccia utente self-service.
