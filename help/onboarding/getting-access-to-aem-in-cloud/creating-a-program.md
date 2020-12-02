---
title: Creazione di un programma - Cloud Service
description: Creazione di un programma - Cloud Service
translation-type: tm+mt
source-git-commit: 5658b2cc853ff7e6222a7f35e56527577d2c7324
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 3%

---


# Creazione di un programma {#create-a-program}

La soluzione nativa del cloud fornisce all&#39;utente le autorizzazioni necessarie e la possibilità di creare un programma su un modello self-service.

Una procedura guidata di creazione del programma chiederà all&#39;utente di inviare i dettagli, a seconda dell&#39;obiettivo dell&#39;utente nella creazione del programma entro i limiti di ciò che è disponibile per il cliente o l&#39;organizzazione specifici.

In caso di accesso a Cloud Manager per la prima volta o se nel tenant non sono presenti programmi, l&#39;utente visualizzerà la schermata **Crea il tuo primo programma**. Se l&#39;utente seleziona *Esc* o fa clic fuori dalla finestra di dialogo, viene visualizzata la schermata seguente:

![](assets/create-program1.png)


## Creazione guidata programma {#using-create-program-wizard}

A seconda dell&#39;obiettivo dell&#39;utente di creare il programma entro i limiti di quanto disponibile per il cliente/organizzazione specifico, una procedura guidata di creazione del programma chiederà all&#39;utente di inviare uno o più dettagli.

![](assets/create-sandbox.png)

>[!NOTE]
>Se un programma esiste già, in alto a destra della pagina di destinazione verrà visualizzato **Aggiungi programma**, come illustrato nella figura riportata di seguito.

![](assets/create-program-add.png)

## Creazione di un programma sandbox {#create-sandbox-program}

Per creare un programma sandbox, effettuate le seguenti operazioni:

1. Nella procedura guidata di creazione del programma, selezionare **Imposta una sandbox**. L&#39;utente invia il nome del programma prima di selezionare **Crea**.

   ![](assets/create-sandbox.png)

1. L&#39;utente vedrà la nuova scheda del programma sandbox sulla pagina di destinazione e può passare il mouse sopra di essa per selezionare l&#39;icona Cloud Manager per passare alla pagina di panoramica di Cloud Manager. La scheda informerà l&#39;utente sullo stato dell&#39;impostazione automatica del programma sandbox appena creato. L&#39;utente vedrà la progressione.

   ![](assets/program-create-setupdemo2.png)

1. Al termine della configurazione del programma e della fase di creazione del progetto, l&#39;utente può accedere al collegamento **Manage Git**, come illustrato nella figura seguente:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni sull&#39;accesso e la gestione dell&#39;archivio Git tramite Gestione account Git self-service dall&#39;interfaccia utente di Cloud Manager, consultare [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).


1. Una volta creato l&#39;ambiente di sviluppo, l&#39;utente può accedere al collegamento **AEM**, come illustrato nella figura seguente:

   ![](assets/create-program-5.png)

1. Una volta completata la distribuzione per lo sviluppo della pipeline non di produzione, la procedura guidata consente all&#39;utente di accedere alle AEM (in fase di sviluppo) o di distribuire il codice all&#39;ambiente di sviluppo:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >Puoi anche modificare, cambiare o aggiungere un programma dalla pagina Panoramica di Cloud Manager, come mostrato di seguito:

   ![](assets/create-program-a1.png)

## Eliminazione di un programma sandbox {#delete-sandbox-program}

Un utente del programma sandbox in *Business Owner* o *Deployment Manager* ruolo in Cloud Manager può eliminare il proprio ambiente di produzione e fase impostato tramite l&#39;interfaccia utente di Cloud Manager.

>[!NOTE]
>Selezionando l’opzione Elimina in Produzione o Stage, viene eliminato anche l’altro nel set.

L’opzione Elimina è disponibile dalla pagina di destinazione, come illustrato di seguito:

![](assets/delete-sandbox1.png)

Oppure,

Selezionare **Elimina programma** dalla pagina **Panoramica programma** per eliminare il programma sandbox.

![](assets/delete-sandbox2.png)


## Creazione di un programma regolare {#create-regular-program}

Un programma *Regular* è destinato a un utente che ha familiarità con AEM e Cloud Manager ed è pronto per iniziare a scrivere, creare e testare il codice con l&#39;obiettivo di distribuirlo in Produzione.

Per creare un programma regolare, effettuate le seguenti operazioni:

1. Selezionare **Imposta per produzione** nella procedura guidata Crea programma per creare un programma regolare. L&#39;utente può accettare il nome predefinito del programma o modificarlo prima di selezionare **Continue**.

   ![](assets/create-prod1.png)

1. L&#39;utente selezionerà le soluzioni da includere nel programma sullo schermo che verrà presentato seguendo lo schermo qui sopra.



   >[!NOTE]
   >
   >La schermata seguente viene visualizzata solo per il segmento di clienti che hanno acquistato più soluzioni. Per i clienti che hanno acquistato una sola soluzione, la schermata di selezione della soluzione non viene visualizzata.

   ![](assets/set-up-prod2.png)

1. Dopo aver selezionato le soluzioni, fare clic su **Crea**.

   ![](assets/set-up-prod3.png)

1. Dopo aver visualizzato la scheda del programma sulla pagina di destinazione, passa il mouse sull&#39;icona di Cloud Manager per passare alla pagina di Cloud Manager **Overview**.

   ![](assets/set-up-prod4.png)

1. La scheda call-to-action principale guiderà l&#39;utente alla creazione di un ambiente, alla creazione di una pipeline non di produzione e, infine, a una pipeline di produzione.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Un programma normale non ha la funzione **Configurazione automatica**.





