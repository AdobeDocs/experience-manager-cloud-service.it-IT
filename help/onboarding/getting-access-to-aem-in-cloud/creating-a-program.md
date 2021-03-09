---
title: Creazione di un programma - Cloud Service
description: Creazione di un programma - Cloud Service
translation-type: tm+mt
source-git-commit: d85c0e9035ee09cf86aeea1cae20d545823eaca0
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---


# Creazione di un programma {#create-a-program}

La soluzione nativa per il cloud fornisce all&#39;utente le autorizzazioni necessarie e la possibilità di creare un programma su un modello self-service.

Una procedura guidata di creazione del programma chiederà all’utente di inviare i dettagli, a seconda dell’obiettivo dell’utente nella creazione del programma entro i limiti di ciò che è disponibile per il cliente o l’organizzazione specifici.

In caso di accesso a Cloud Manager per la prima volta o se nel tenant non esiste alcun programma, l’utente visualizzerà la schermata **Crea il tuo primo programma** . Se l&#39;utente seleziona *Esc* o fa clic fuori dalla finestra di dialogo, viene visualizzata la seguente schermata:

![](assets/create-program1.png)


## Creazione guidata programma {#using-create-program-wizard}

A seconda dell’obiettivo dell’utente nella creazione del programma entro i limiti di ciò che è disponibile per il cliente o l’organizzazione specifici, una procedura guidata di creazione del programma chiederà all’utente di inviare uno o più dettagli.

![](assets/create-sandbox.png)


## Creazione di un programma sandbox {#create-sandbox-program}

Per creare un programma sandbox, effettua le seguenti operazioni:

1. Dalla procedura guidata di creazione del programma, seleziona **Imposta una sandbox**. L&#39;utente invia il nome del programma prima di selezionare **Crea**.

   ![](assets/create-sandbox.png)

1. L’utente visualizza la nuova scheda del programma sandbox sulla pagina di destinazione e può passare il cursore sopra di essa per selezionare l’icona Cloud Manager per passare alla pagina di panoramica di Cloud Manager. La scheda informerà l&#39;utente sullo stato di configurazione automatica del programma sandbox appena creato. L&#39;utente vedrà la progressione.

   ![](assets/program-create-setupdemo2.png)

1. Al termine della configurazione del programma e della fase di creazione del progetto, l’utente può accedere al collegamento **Manage Git** , come illustrato nella figura seguente:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni sull’accesso e la gestione dell’archivio Git tramite Gestione account Git self-service dall’interfaccia utente di Cloud Manager, consulta [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).


1. Una volta creato l&#39;ambiente di sviluppo, l&#39;utente può accedere al collegamento **AEM di accesso** , come illustrato nella figura seguente:

   ![](assets/create-program-5.png)

1. Una volta completata la distribuzione della pipeline non di produzione allo sviluppo, la procedura guidata guida l’utente ad accedere AEM (in fase di sviluppo) o a distribuire il codice nell’ambiente di sviluppo:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >Puoi anche modificare, cambiare o aggiungere un programma dalla pagina Panoramica di Cloud Manager, come illustrato di seguito:

   ![](assets/create-program-a1.png)

## Eliminazione di un programma sandbox {#delete-sandbox-program}

Un utente del programma sandbox con il ruolo *Proprietario business* o *Gestione distribuzione* in Cloud Manager può eliminare il proprio ambiente di produzione e stage impostato tramite l’interfaccia utente di Cloud Manager.

>[!NOTE]
>Selezionando l’opzione Elimina in Produzione o Stage, viene eliminato anche l’altro nel set.

L’opzione Elimina è disponibile dalla pagina di destinazione, come illustrato di seguito:

![](assets/delete-sandbox1.png)

Oppure,

Seleziona **Elimina programma** dalla pagina **Panoramica programma** per eliminare il programma sandbox.

![](assets/delete-sandbox2.png)


## Creazione di un programma regolare {#create-regular-program}

Un programma *Regular* è destinato a un utente che ha dimestichezza con AEM e Cloud Manager ed è pronto per iniziare a scrivere, creare e testare il codice allo scopo di distribuirlo in Produzione.

Segui i passaggi riportati di seguito per creare un programma regolare:

1. Seleziona **Imposta per produzione** nella procedura guidata Crea programma per creare un programma regolare. L&#39;utente può accettare il nome predefinito del programma o modificarlo prima di selezionare **Continua**.

   ![](assets/create-prod1.png)

1. L&#39;utente selezionerà le soluzioni da includere nel programma nella schermata che verrà presentata dopo la schermata precedente.



   >[!NOTE]
   >
   >La schermata seguente viene visualizzata solo per il segmento di clienti che hanno acquistato più di una soluzione. Per i clienti che hanno acquistato una sola soluzione, la schermata di selezione della soluzione sottostante non verrà visualizzata.

   ![](assets/set-up-prod2.png)

1. Dopo aver selezionato le soluzioni, fai clic su **Crea**.

   ![](assets/set-up-prod3.png)

1. Una volta visualizzata la scheda del programma nella pagina di destinazione, passa il puntatore del mouse su di essa per selezionare l’icona Cloud Manager per passare alla pagina Cloud Manager **Panoramica**.

   ![](assets/set-up-prod4.png)

1. La scheda di chiamata all’azione principale guiderà l’utente a creare un ambiente, creare una pipeline non di produzione e, infine, una pipeline di produzione.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Un programma normale non dispone della funzione **Configurazione automatica**.





