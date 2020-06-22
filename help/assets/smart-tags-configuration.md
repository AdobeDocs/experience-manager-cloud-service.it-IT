---
title: Tag avanzati migliorati
description: Applica tag aziendali contestuali e descrittivi utilizzando i servizi di intelligenza artificiale e machine learning di Adobe Sensei per migliorare l’individuazione delle risorse e velocizzare la realizzazione dei contenuti.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 41684858f1fe516046b9601c1d869fff180320e0
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 35%

---


# Configurare Experience Manager per l’assegnazione di tag avanzati alle risorse {#configure-aem-for-smart-tagging}

L’assegnazione dei tag alle risorse mediante un vocabolario controllato dalla tassonomia consente di individuare e recuperare facilmente le risorse tramite ricerche basate sui tag. Adobe fornisce Smart Tags che utilizza algoritmi di intelligenza artificiale e machine learning per formare le immagini. Smart Tags uses an artificial intelligence framework of [Adobe Sensei](https://www.adobe.com/it/sensei/experience-cloud-artificial-intelligence.html) to train its image recognition algorithm on your tag structure and business taxonomy.

The Smart Tags functionality is available for purchase as an add-on to [!DNL Experience Manager]. Dopo l’acquisto, viene inviata un’e-mail all’amministratore dell’organizzazione con un collegamento ad Adobe Developer Console. L&#39;amministratore accede al collegamento per integrare i tag avanzati con [!DNL Experience Manager] Adobe Developer Console.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integrazione con Adobe Developer Console {#aio-integration}

Prima di poter assegnare tag alle immagini tramite SCS, è necessario integrare [!DNL Adobe Experience Manager] con il servizio Smart Tags tramite Adobe Developer Console. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the service.

* Create a configuration in [!DNL Experience Manager] to generate a public key. Ottieni un certificato pubblico per l’integrazione di OAuth.
* Create un&#39;integrazione in Adobe Developer Console e caricate la chiave pubblica generata.
* Configure your [!DNL Experience Manager] instance using the API key and other credentials from Adobe Developer Console.
* Se necessario, abilita l’assegnazione tag automatica al caricamento delle risorse.

### Prerequisiti per l&#39;integrazione con Adobe Developer Console {#prerequisite-for-aio-integration}

Prima di poter utilizzare i tag avanzati, accertatevi quanto segue per creare un&#39;integrazione in Adobe Developer Console:

* Disponi di un account Adobe ID con privilegi di amministratore dell’organizzazione.
* I tag avanzati sono abilitati per la vostra organizzazione.

### Ottenere un certificato pubblico {#obtain-public-certificate}

Un certificato pubblico consente di autenticare il profilo in Adobe Developer Console. Create un certificato dall&#39;interno [!DNL Experience Manager].

1. Nell&#39;interfaccia [!DNL Experience Manager] utente, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > Configurazioni **** Adobe IMS.

1. Nella pagina [!UICONTROL Adobe IMS Configurations] , fate clic su **[!UICONTROL Create (Crea)]**. Dal menu **[!UICONTROL Cloud Solution]** , selezionate **[!UICONTROL Smart Tags]**.

1. Selezionate **[!UICONTROL Crea nuovo certificato]**. Immettete un nome e fate clic su **[!UICONTROL Crea certificato]**. Fai clic su **[!UICONTROL OK]**.

1. Fate clic su **[!UICONTROL Scarica chiave]** pubblica.

   ![Experience Manager Smart Tags creare una chiave pubblica](assets/aem_smarttags-config1.png)

### Effettuare la riconfigurazione in caso di scadenza del certificato {#certrenew}

Quando il certificato scade, non è più attendibile. Per aggiungere un nuovo certificato, effettua le seguenti operazioni. Non è possibile rinnovare un certificato scaduto.

1. Accedi alla tua implementazione di [!DNL Experience Manager] come amministratore. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individua e fai clic sull’utente **[!UICONTROL dam-update-service]**. Fai clic sulla scheda **[!UICONTROL Registro chiavi]**.
1. Elimina il registro chiavi esistente **[!UICONTROL similaritysearch]** con il certificato scaduto. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![Per aggiungere un nuovo certificato di sicurezza, elimina la voce esistente similaritysearch in Registro chiavi](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Eliminate la`similaritysearch`voce esistente in Keystore per aggiungere un nuovo certificato di protezione.*

1. Nell&#39;interfaccia [!DNL Experience Manager] utente, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > Configurazioni **** Adobe IMS. Aprite la configurazione di Smart Tags disponibile. To download a public certificate, click **[!UICONTROL Download Public Certificate]**.

1. Accedete a [https://console.adobe.io](https://console.adobe.io) e andate al servizio esistente nel progetto. Caricate il nuovo certificato e configurate. Per ulteriori informazioni sulla configurazione, consulta le istruzioni riportate in [Creazione dell’integrazione](#create-aio-integration)di Adobe Developer Console.

### Creare un’integrazione {#create-aio-integration}

Per utilizzare i tag avanzati, create un&#39;integrazione in Adobe Developer Console per generare la chiave API, l&#39;ID account tecnico, l&#39;ID organizzazione e il Segreto cliente.

1. Accedete a [https://console.adobe.io](https://console.adobe.io/) in un browser. Selezionate l&#39;account appropriato e verificate che il ruolo organizzazione associato sia l&#39;amministratore di sistema.
1. Create un progetto con il nome desiderato. Fate clic su **[!UICONTROL Aggiungi API]**.
1. Nella pagina **[!UICONTROL Aggiungi un&#39;API]** , selezionate **[!UICONTROL Experience Cloud]** e selezionate **[!UICONTROL Smart Content]**. Fai clic su **[!UICONTROL Avanti]**.
1. Selezionate **[!UICONTROL Carica la chiave]** pubblica. Fornite il file del certificato scaricato da [!DNL Experience Manager]. Viene visualizzato un messaggio di chiave [!UICONTROL pubblica caricata correttamente] . Fai clic su **[!UICONTROL Avanti]**.
1. [!UICONTROL Nella pagina Crea una nuova credenziale] account di servizio (JWT) viene visualizzata la chiave pubblica per l&#39;account di servizio appena configurato. Fai clic su **[!UICONTROL Avanti]**.
1. Nella pagina **[!UICONTROL Seleziona profili]** di prodotto, selezionate **[!UICONTROL Smart Content Services]**. Fate clic su **[!UICONTROL Salva API]** configurata. Una pagina visualizza ulteriori informazioni sulla configurazione. Tenete aperta questa pagina per copiare e aggiungere questi valori in  Experience Manager durante l&#39;ulteriore configurazione dei tag avanzati in [!DNL Experience Manager].

   ![Nella scheda Panoramica, puoi esaminare le informazioni fornite sull’integrazione.](assets/integration_details.png)

### Configurare i tag avanzati {#configure-smart-content-service}

Per configurare l&#39;integrazione, utilizzate i valori dei campi Payload, Segreto cliente, Server di autorizzazione e Chiave API dall&#39;integrazione di Adobe Developer Console.

1. Nell&#39;interfaccia [!DNL Experience Manager] utente, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > Configurazioni **** Adobe IMS.
1. Accedete alla pagina Configurazione **[!UICONTROL account tecnico]** Adobe IMS e specificate il **[!UICONTROL Titolo]** desiderato.
1. Nel campo **[!UICONTROL Server]** di autorizzazione, fornite `https://ims-na1.adobelogin.com` l’URL.
1. Nel campo Chiave **** API, fornite l&#39;ID **** client dal [!DNL Adobe Developer Console].
1. Nel campo Segreto **** cliente, fornire il Segreto **** cliente dal [!DNL Adobe Developer Console]. Fate clic su **[!UICONTROL Recupera Segreto]** cliente per visualizzarlo.
1. Nel [!DNL Adobe Developer Console]progetto, fai clic su Account **[!UICONTROL servizio (JWT)]** dal margine sinistro. Fate clic sulla scheda **[!UICONTROL Genera JWT]** . Fate clic su **[!UICONTROL Copia]** per copiare il payload **[!UICONTROL JWT visualizzato]**. Immettete questo valore nel campo **[!UICONTROL Payload]** in [!DNL Experience Manager]. Fai clic su **[!UICONTROL Crea]**.

### Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, segui questi passaggi per convalidare la configurazione.

1. Nell&#39;interfaccia [!DNL Experience Manager] utente, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > Configurazioni **** Adobe IMS.

1. Selezionate la configurazione Smart Tags. Fare clic su **[!UICONTROL Verifica stato]** dalla barra degli strumenti. Fai clic su **[!UICONTROL Verifica]**. Una finestra di dialogo con un messaggio di configurazione  sano conferma il funzionamento della configurazione.

![Convalida della configurazione dei tag avanzati](assets/smart-tag-config-validation.png)

## Abilitare l’assegnazione tag avanzati per le nuove risorse caricate (facoltativo) {#enable-smart-tagging-for-uploaded-assets}

1. In [!DNL Experience Manager], passa a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/chlimage_1-105.png)

   *Figura: Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM.*

1. Apri il passaggio da configurare. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Impostazione per il gestore per passare al passaggio successivo nel flusso di lavoro.](assets/smart-tags-workflow-handler-setting.png)

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se desideri che il flusso di lavoro ignori gli errori durante la previsione dei tag. Per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

1. Fai clic su **[!UICONTROL OK]** per chiudere il passaggio del processo, quindi salva il flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

>[!MORELIKETHIS]
>
>* [Assegnare i tag alle risorse utilizzando il servizio di tag avanzati](smart-tags.md)

