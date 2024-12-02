---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: Integrazione di AEM Forms OneDrive, connessione a Microsoft OneDrive, configurazione di OneDrive con moduli AEM
feature: Adaptive Forms, Core Components
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---

# Inviare un modulo adattivo a Microsoft® OneDrive

L&#39;azione di invio **[!UICONTROL Invia a OneDrive]** collega un modulo adattivo a Microsoft® OneDrive. È possibile inviare i dati del modulo, i file, gli allegati o il documento di record all&#39;archivio Microsoft® OneDrive collegato.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

## Vantaggi

Alcuni dei vantaggi dell&#39;integrazione diretta di AEM Forms e Microsoft® OneDrive sono:

* L&#39;accessibilità cross-device di OneDrive garantisce che i dati dei moduli archiviati siano prontamente disponibili su piattaforme diverse. Gli utenti possono accedere ai dati, agli allegati e ai documenti inviati da desktop, notebook, tablet e dispositivi mobili, migliorando l&#39;accessibilità e la flessibilità.
* L&#39;integrazione di OneDrive con i moduli AEM fornisce una soluzione affidabile e scalabile per l&#39;archiviazione efficiente dei dati. Tutti gli invii di moduli adattivi, come file, allegati e documenti di record, possono essere salvati in OneDrive in modo semplice, garantendo dati organizzati e accessibili.

## Connessione di OneDrive a un modulo adattivo

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

La configurazione di OneDrive per l&#39;invio di AEM Forms prevede i seguenti passaggi:

1. [Crea una configurazione di OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): connette AEM Forms al tuo archivio Microsoft® OneDrive.
2. [Utilizzare l&#39;azione Invia a OneDrive in un modulo adattivo](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): il modulo adattivo viene collegato a Microsoft® OneDrive configurato.

### Crea una configurazione OneDrive {#create-onedrice-configuration}

Per collegare AEM Forms allo storage Microsoft® OneDrive:

1. Vai all&#39;istanza di **AEM Forms Author** > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® OneDrive]**.
1. Dopo aver selezionato **[!UICONTROL Microsoft® OneDrive]**, sei reindirizzato a **[!UICONTROL OneDrive Browser]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Verrà visualizzata la configurazione guidata di OneDrive.

   ![Schermata Configurazione OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l&#39;ID client, il segreto client e l&#39;ID tenant per l&#39;URL OAuth, consulta la [documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Puoi recuperare `Client ID` e `Client Secret` dell&#39;app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungere l&#39;URI di reindirizzamento come `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l&#39;URL dell&#39;istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Files.ReadWrite.All` per fornire le autorizzazioni di lettura/scrittura.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale di Microsoft® Azure.

   >[!NOTE]
   >
   > Il campo **segreto client** è obbligatorio oppure facoltativo in base alla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Fai clic su **[!UICONTROL Connetti]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.

1. Selezionare **[!UICONTROL Contenitore OneDrive]** > **[Cartella OneDrive]** per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel contenitore OneDrive.
   > * Creare una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente, facendo clic su **Crea cartella**.

Ora puoi utilizzare questa configurazione di archiviazione OneDrive per l&#39;azione di invio in un modulo adattivo.

### Usa configurazione OneDrive in un modulo adattivo {#use-onedrive-configuartion-in-af}

È possibile utilizzare la configurazione di archiviazione di OneDrive creata in un modulo adattivo per salvare dati o documenti di record generati in una cartella di OneDrive. Per utilizzare la configurazione di archiviazione OneDrive in un modulo adattivo, effettua le seguenti operazioni:
1. Crea un [modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selezionare lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stato creato lo spazio di archiviazione di OneDrive.
   > * Se non è selezionato alcun contenitore di configurazione [!UICONTROL Contenitore di configurazione], nella finestra delle proprietà dell&#39;azione di invio vengono visualizzate le cartelle globali [!UICONTROL Configurazione archiviazione].

1. Seleziona **Invia azione** come **[!UICONTROL Invia a OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio Microsoft® OneDrive specificato.
La struttura di cartelle per il salvataggio dei dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Articoli correlati

{{af-submit-action}}
