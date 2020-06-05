---
title: Smart tag migliorati
description: Applica tag business contestuali e descrittivi utilizzando i servizi AI e ML di Adobe Sensei, per migliorare l'individuazione delle risorse e la velocità dei contenuti.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b5af8cad55c8644ba613370cf65b6a04b3abf9ed
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 12%

---


# Configurare Experience Manager per l’assegnazione di smart tag alle risorse {#configure-aem-for-smart-tagging}

L’assegnazione di tag alle risorse mediante il vocabolario controllato dalla tassonomia consente di identificare e recuperare facilmente le risorse mediante ricerche basate sui tag. Adobe fornisce Smart Content Service (SCS) che utilizza algoritmi di intelligenza artificiale e di machine learning per la formazione delle immagini. Smart Content Service utilizza un framework di intelligenza artificiale di [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) per formare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e sulla tassonomia aziendale.

Smart Content Service è disponibile per l&#39;acquisto come componente aggiuntivo per [!DNL Experience Manager]. Dopo l&#39;acquisto, viene inviata un&#39;e-mail all&#39;amministratore dell&#39;organizzazione con un collegamento ad Adobe I/O. L&#39;amministratore accede al collegamento per integrare Smart Content Service con [!DNL Experience Manager].

<!-- TBD: 
1. Create a similar flowchart for how training works in CS. ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integrazione con Adobe I/O {#aio-integration}

Prima di poter assegnare tag alle immagini mediante SCS, è necessario integrare [!DNL Adobe Experience Manager] con Smart Content Service mediante l&#39;I/O di Adobe. Utilizzate questa configurazione per accedere a Smart Content Service dall&#39;interno [!DNL Experience Manager].

L&#39;articolo descrive le seguenti attività chiave necessarie per configurare Smart Content Service. Sul lato posteriore, il [!DNL Experience Manager] server autentica le credenziali del servizio con il gateway di I/O Adobe prima di inoltrare la richiesta a Smart Content Service.

* Create una configurazione di Smart Content Service in [!DNL Experience Manager] modo da generare una chiave pubblica. Ottenete un certificato pubblico per l&#39;integrazione OAuth.
* Create un&#39;integrazione in Adobe I/O e caricate la chiave pubblica generata.
* Configurate l&#39; [!DNL Experience Manager] istanza utilizzando la chiave API e altre credenziali dall&#39;I/O di Adobe.
* Se necessario, abilitate l’assegnazione automatica di tag al caricamento delle risorse.

### Prerequisiti per l&#39;integrazione di I/O Adobe {#prerequisite-for-aio-integration}

Prima di poter utilizzare Smart Content Service, accertatevi quanto segue per creare un&#39;integrazione su Adobe I/O:

* Un account Adobe ID con privilegi di amministratore per l’organizzazione.
* Il servizio Smart Content Service è abilitato per la vostra azienda.

### Obtain a public certificate {#obtain-public-certificate}

Un certificato pubblico consente di autenticare il profilo sull&#39;I/O di Adobe.

1. Nell&#39;interfaccia [!DNL Experience Manager] utente, accedi a **[!UICONTROL Strumenti]** > Servizi **** Cloud > Servizi **[!UICONTROL cloud]** legacy.

1. On the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]** , specificate un titolo e un nome per la configurazione Smart Tags. Fai clic su **[!UICONTROL Crea]**.

1. Nella finestra di dialogo **[!UICONTROL AEM Smart Content Service]** , usate i seguenti valori:

   **[!UICONTROL URL servizio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Server autorizzazioni]**: `https://ims-na1.adobelogin.com`

   Lasciate vuoti gli altri campi per ora (da fornire successivamente). Fai clic su **[!UICONTROL OK]**. 

   ![Finestra di dialogo Experience Manager Smart Content Service per fornire l&#39;URL del servizio di contenuto](assets/aem_scs.png)

1. Fate clic su **[!UICONTROL Scarica certificato pubblico per l&#39;integrazione]** OAuth e scaricate il file del certificato pubblico `AEM-SmartTags.crt`.

   ![Una rappresentazione delle impostazioni create per il servizio di smart tag](assets/download_link.png)

### Riconfigura se un certificato scade {#certrenew}

Alla scadenza del certificato non è più attendibile. Per aggiungere un nuovo certificato, attenetevi alla procedura seguente. Non è possibile rinnovare un certificato scaduto.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individuate e fate clic su **[!UICONTROL dam-update-service]** user. Fate clic sulla scheda **[!UICONTROL Keystore]** .
1. Eliminate l&#39;archivio di chiavi di ricerca **[!UICONTROL per]** similarità esistente con il certificato scaduto. Click **[!UICONTROL Save &amp; Close]**.

   ![Per aggiungere un nuovo certificato di protezione, eliminate una voce di ricerca per similarità in Keystore](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Eliminate`similaritysearch`la voce esistente in Keystore per aggiungere un nuovo certificato di protezione.*

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**. Fai clic su **[!UICONTROL Tag avanzati risorse]** > **[!UICONTROL Mostra configurazioni]** > **[!UICONTROL Configurazioni disponibili]**. Seleziona la configurazione richiesta.

1. Per scaricare un certificato pubblico, fate clic su **[!UICONTROL Scarica certificato pubblico per l&#39;integrazione]** OAuth.
1. Accedete a [https://console.adobe.io](https://console.adobe.io) e andate a Smart Content Services nella pagina **[!UICONTROL Integrazioni]** . Caricate il nuovo certificato. Per ulteriori informazioni, consultate le istruzioni in [Creazione dell&#39;integrazione](#create-adobe-i-o-integration)I/O Adobe.

### Creare un&#39;integrazione {#create-aio-integration}

Per utilizzare le API Smart Content Service, create un&#39;integrazione in Adobe I/O per generare la chiave API, l&#39;ID account tecnico, l&#39;ID organizzazione e il Segreto cliente.

1. Accedete a [https://console.adobe.io](https://console.adobe.io/).
1. Nella pagina **[!UICONTROL Integrazioni]** , selezionate l&#39;account appropriato e verificate che il ruolo organizzazione associato sia amministratore di sistema.
1. Fate clic su **[!UICONTROL Nuova integrazione]**.
1. Nella pagina **[!UICONTROL Crea nuova integrazione]** , selezionate **[!UICONTROL Accedi a un&#39;API]**. Fate clic su **[!UICONTROL Continua]**.
1. In **[!UICONTROL Experience Cloud]**, seleziona **[!UICONTROL Smart Content]**. Fate clic su **[!UICONTROL Continua]**.
1. Nella pagina successiva, selezionate **[!UICONTROL Nuova integrazione]**. Fate clic su **[!UICONTROL Continua]**.
1. Nella pagina **[!UICONTROL Dettagli]** integrazione, specificate un nome per il gateway di integrazione e aggiungete una descrizione.
1. Nei certificati delle chiavi **[!UICONTROL pubbliche]**, caricate il `AEM-SmartTags.crt` file scaricato in precedenza.
1. Fai clic su **[!UICONTROL Create Integration]** (Crea integrazione).
1. Per visualizzare le informazioni sull&#39;integrazione, fate clic su **[!UICONTROL Continua con i dettagli]** sull&#39;integrazione.

   ![Nella scheda Panoramica è possibile esaminare le informazioni fornite per l&#39;integrazione.](assets/integration_details.png)

### Configurare Smart Content Service {#configure-smart-content-service}

Per configurare l&#39;integrazione, utilizzate i valori dei campi ID account tecnico, ID organizzazione, Segreto cliente, Server autorizzazioni e chiave API dall&#39;integrazione I/O di Adobe. La creazione di una configurazione cloud Smart Tags consente l&#39;autenticazione delle richieste API dall&#39; [!DNL Experience Manager] istanza.

1. In [!DNL Experience Manager]Strumenti > **[!UICONTROL Servizi cloud > Servizi]** cloud legacy per aprire la console Servizi  Cloud.
1. In Tag **[!UICONTROL avanzati]** risorse, apri la configurazione creata sopra. Nella pagina delle impostazioni del servizio, fate clic su **[!UICONTROL Modifica]**.
1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, utilizza i valori precompilati per i campi **[!UICONTROL URL servizio]** e **[!UICONTROL Server autorizzazioni]**.
1. Per i campi **[!UICONTROL Chiave API]**, **[!UICONTROL ID account tecnico]**, **[!UICONTROL ID organizzazione]** e **[!UICONTROL Segreto client]**, utilizza i valori generati sopra.

### Convalida della configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi usare un MBean JMX per convalidare la configurazione. Per eseguire la convalida, effettuare le seguenti operazioni.

1. Accedete al [!DNL Experience Manager] server all&#39;indirizzo `https://[aem_server]:[port]`.

1. Passate a **[!UICONTROL Strumenti > Operazioni > Console]** Web per aprire la console OSGi. Fate clic su **[!UICONTROL Principale > JMX]**.
1. Fate clic su **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Si apre **[!UICONTROL SimilaritySearch Attività varie.]**
1. Fare clic su **[!UICONTROL validateConfigs()]**. Nella finestra di dialogo **[!UICONTROL Convalida configurazioni]** , fare clic su **[!UICONTROL Richiama]**.

   Il risultato della convalida viene visualizzato nella stessa finestra di dialogo.

## Abilitare i tag avanzati per le nuove risorse caricate (facoltativo) {#enable-smart-tagging-for-uploaded-assets}

1. In [!DNL Experience Manager], passare a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Fare clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungi il passaggio di una risorsa smart tag dopo il passaggio della miniatura del processo nel flusso di lavoro DAM Update Asset](assets/chlimage_1-105.png)

   *Figura: Aggiungi il passaggio di una risorsa smart tag dopo il passaggio della miniatura del processo nel flusso di lavoro DAM Update Asset (Aggiorna risorsa DAM).*

1. Aprite il passaggio da configurare. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![chlimage_1-3](assets/smart-tags-workflow-handler-setting.png)

1. Nella scheda **[!UICONTROL Argomenti]** , selezionare **[!UICONTROL Ignora errori]** se si desidera che il flusso di lavoro ignori gli errori durante la previsione dei tag. Per assegnare tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione di tag avanzati sia abilitata o meno nelle cartelle, selezionate **[!UICONTROL Ignora contrassegno]** smart tag.

1. Fate clic su **[!UICONTROL OK]** per chiudere il passaggio del processo, quindi salvate il flusso di lavoro. Fate clic su **[!UICONTROL Sincronizza]**.

>[!MORELIKETHIS]
>
>* [Assegnare tag alle risorse mediante il servizio avanzato](smart-tags.md)