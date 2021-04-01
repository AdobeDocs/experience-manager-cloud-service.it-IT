---
title: Tag avanzati migliorati
description: Applica tag aziendali contestuali e descrittivi utilizzando i servizi di intelligenza artificiale e machine learning di Adobe Sensei per migliorare l’individuazione delle risorse e velocizzare la realizzazione dei contenuti.
contentOwner: AG
feature: Tag avanzati, assegnazione tag
role: Administrator
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 83%

---


# Configurare [!DNL Experience Manager] per l’assegnazione di tag avanzati alle risorse {#configure-aem-for-smart-tagging}

L’assegnazione dei tag alle risorse mediante un vocabolario controllato dalla tassonomia consente di individuare e recuperare facilmente le risorse tramite ricerche basate sui tag. Adobe fornisce Tag avanzati che utilizzano l’intelligenza artificiale e algoritmi di apprendimento automatico per addestrare le immagini. Grazie a un framework di intelligenza artificiale di [Adobe Sensei](https://www.adobe.com/it/sensei/experience-cloud-artificial-intelligence.html), l’algoritmo di riconoscimento delle immagini viene addestrato in base alla tua struttura dei tag e alla tassonomia aziendale.

La funzionalità Tag avanzati è acquistabile come componente aggiuntivo per [!DNL Experience Manager]. Dopo l’acquisto, viene inviata un’e-mail all’amministratore dell’organizzazione con un collegamento ad Adobe Developer Console. L’amministratore accede al collegamento per integrare Tag avanzati con [!DNL Experience Manager] tramite Adobe Developer Console.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

>[!IMPORTANT]
>
>Se le distribuzioni [!DNL Experience Manager Assets] sono state create dopo la versione [di agosto 2020](/help/release-notes/release-notes-cloud/2020/release-notes-2020-8-0.md#assets), [!DNL Adobe Developer Console] è integrato per impostazione predefinita. Consente di configurare più rapidamente la funzionalità dei tag avanzati. Nelle implementazioni precedenti, gli amministratori possono configurare manualmente l’integrazione seguendo le istruzioni riportate di seguito.

## Integrare con Adobe Developer Console {#aio-integration}

Prima di poter assegnare tag alle immagini tramite SCS, è necessario integrare [!DNL Adobe Experience Manager] con il servizio Tag avanzati tramite Adobe Developer Console. Nel back-end, il server di [!DNL Experience Manager] autentica le credenziali del servizio con il gateway di Adobe Developer Console prima di inoltrare la richiesta al servizio.

* Crea una configurazione in [!DNL Experience Manager] per generare una chiave pubblica. [Ottieni un certificato pubblico](#obtain-public-certificate) per l’integrazione di OAuth.
* [Crea un’integrazione in Adobe Developer Console](#create-aio-integration) e carica la chiave pubblica generata.
* [Configura tag avanzati](#configure-smart-content-service) nella tua istanza di [!DNL Experience Manager] utilizzando la chiave API e altre credenziali di Adobe Developer Console.
* [Verifica la configurazione](#validate-the-configuration).
* [Riconfigura dopo la scadenza del certificato](#certrenew).

### Prerequisiti per l’integrazione con Adobe Developer Console {#prerequisite-for-aio-integration}

Prima di poter utilizzare Tag avanzati, verifica quanto segue per creare un’integrazione su Adobe Developer Console:

* Devi disporre di un account Adobe ID con privilegi di amministratore dell’organizzazione.
* Il servizio Tag avanzati deve essere abilitato per la tua organizzazione.

### Ottenere un certificato pubblico {#obtain-public-certificate}

Un certificato pubblico ti consente di autenticare il profilo su Adobe Developer Console. Puoi creare un certificato da [!DNL Experience Manager].

1. Nell’interfaccia utente di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

1. Nella pagina [!UICONTROL Configurazioni Adobe IMS], fai clic su **[!UICONTROL Crea]**. Dal menu **[!UICONTROL Soluzione cloud]**, seleziona **[!UICONTROL Tag avanzati]**.

1. Seleziona **[!UICONTROL Crea nuovo certificato]**. Immetti un nome e fai clic su **[!UICONTROL Crea certificato]**. Fai clic su **[!UICONTROL OK]**.

1. Fai clic su **[!UICONTROL Scarica chiave pubblica]**.

   ![[!DNL Experience Manager] Creare una chiave pubblica tramite tag avanzati](assets/aem_smarttags-config1.png)

### Creare un’integrazione {#create-aio-integration}

Per utilizzare Tag avanzati, crea un’integrazione in Adobe Developer Console per generare la chiave API, l’ID account tecnico, l’ID organizzazione e il segreto client.

1. Accedi a [https://console.adobe.io](https://console.adobe.io/) in un browser. Seleziona l’account appropriato e verifica che il ruolo aziendale associato sia quello di amministratore di sistema.
1. Crea un progetto con il nome desiderato. Fai clic su **[!UICONTROL Aggiungi API]**.
1. Nella pagina **[!UICONTROL Aggiungi un API]**, seleziona **[!UICONTROL Experience Cloud]**, quindi seleziona **[!UICONTROL Contenuto avanzato]**. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona **[!UICONTROL Carica la chiave pubblica]**. Fornisci il file del certificato scaricato da [!DNL Experience Manager]. Viene visualizzato il messaggio [!UICONTROL Chiavi pubbliche caricate correttamente]. Fai clic su **[!UICONTROL Avanti]**.
1. [!UICONTROL Nella pagina delle ] credenziali Crea un nuovo account di servizio (JWT) viene visualizzata la chiave pubblica per l’account di servizio. Fai clic su **[!UICONTROL Avanti]**.
1. Nella pagina per la **[!UICONTROL selezione dei profili di prodotto]**, seleziona **[!UICONTROL Servizi di contenuti avanzati]**. Fai clic su **[!UICONTROL Salva API configurata]**. In una pagina vengono visualizzate ulteriori informazioni sulla configurazione. Tieni aperta questa pagina per copiare e aggiungere questi valori in [!DNL Experience Manager] durante l’ulteriore configurazione di Tag avanzati in [!DNL Experience Manager].

   ![Nella scheda Panoramica, puoi esaminare le informazioni fornite sull’integrazione.](assets/integration_details.png)

### Configurare Tag avanzati {#configure-smart-content-service}

Per configurare l’integrazione, utilizza i valori dei campi Payload, Segreto client, Server autorizzazioni e Chiave API dall’integrazione di Adobe Developer Console.

1. Nell’interfaccia utente di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.
1. Accedi alla pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** e specifica il **[!UICONTROL Titolo]** desiderato.
1. Nel campo **[!UICONTROL Server autorizzazioni]**, inserisci l’URL `https://ims-na1.adobelogin.com`.
1. Nel campo **[!UICONTROL Chiave API]**, inserisci l’**[!UICONTROL ID client]** di [!DNL Adobe Developer Console].
1. Nel campo **[!UICONTROL Segreto client]**, inserisci il **[!UICONTROL Segreto client]** di [!DNL Adobe Developer Console]. Fai clic su **[!UICONTROL Recupera segreto client]** per visualizzarlo.
1. In [!DNL Adobe Developer Console], nel tuo progetto, fai clic su **[!UICONTROL Account di servizio (JWT)]** a sinistra. Fai clic sulla scheda **[!UICONTROL Genera JWT]**. Fai clic su **[!UICONTROL Copia]** per copiare il **[!UICONTROL Payload JWT]** visualizzato. Immetti tale valore nel campo **[!UICONTROL Payload]** in [!DNL Experience Manager]. Fai clic su **[!UICONTROL Crea]**.

### Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, segui questi passaggi per convalidarla.

1. Nell’interfaccia utente di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

1. Seleziona la configurazione di Tag avanzati. Fai clic su **[!UICONTROL Verifica stato]** nella barra degli strumenti. Fai clic su **[!UICONTROL Verifica]**. Una finestra di dialogo con il messaggio [!UICONTROL Configurazione integra] conferma il corretto funzionamento della configurazione.

![Convalidare la configurazione di Tag avanzati](assets/smart-tag-config-validation.png)

### Effettuare la riconfigurazione in caso di scadenza del certificato {#certrenew}

Quando il certificato scade, non è più attendibile. Per aggiungere un certificato, effettua le seguenti operazioni. Non è possibile rinnovare un certificato scaduto.

1. Accedi alla tua implementazione di [!DNL Experience Manager] come amministratore. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individua e fai clic sull’utente **[!UICONTROL dam-update-service]**. Fare clic sulla scheda **[!UICONTROL Registro chiavi]**.
1. Elimina il registro chiavi esistente **[!UICONTROL similaritysearch]** con il certificato scaduto. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![Elimina la voce di ricerca per similarità esistente in Registro chiavi per aggiungere un nuovo certificato di sicurezza](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Elimina la  `similaritysearch` voce esistente in Registro chiavi per aggiungere un certificato di sicurezza.*

1. Nell’interfaccia utente di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**. Apri la configurazione di Tag avanzati disponibile. Per scaricare un certificato pubblico, fai clic su **[!UICONTROL Scarica certificato pubblico]**.

1. Accedi a [https://console.adobe.io](https://console.adobe.io) e naviga fino al servizio esistente nel progetto. Carica il nuovo certificato ed effettua la configurazione. Per ulteriori informazioni sulla configurazione, consulta [Creare un’integrazione con Adobe Developer Console](#create-aio-integration).

## Abilita l’assegnazione tag automatica quando le risorse vengono caricate (facoltativo) {#enable-smart-tagging-for-uploaded-assets}

1. In [!DNL Experience Manager], passa a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/chlimage_1-105.png)

   *Figura: Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM.*

1. Apri il passaggio da configurare. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Impostazione del gestore per passare al passaggio successivo nel flusso di lavoro.](assets/smart-tags-workflow-handler-setting.png)

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se desideri che il flusso di lavoro ignori gli errori durante la previsione dei tag. Per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

1. Fai clic su **[!UICONTROL OK]**. Chiude la fase del processo. Salva il flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

>[!MORELIKETHIS]
>
>* [Assegnare i tag alle risorse utilizzando il servizio di tag avanzati](smart-tags.md)

