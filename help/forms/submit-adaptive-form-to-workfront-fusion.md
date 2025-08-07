---
title: Integrazione di Adobe Workfront Fusion con l’invio di AEM Forms
description: Adobe Workfront Fusion consente di concentrarsi su nuove attività anziché su attività ripetitive. Puoi collegare Adobe Workfront Fusion a un modulo adattivo utilizzando Invio modulo.
keywords: Inviare un modulo adattivo ad Adobe Workfront Fusion, Integrazione di Adobe Workfront Fusion con AEM Forms Invio, Adobe Workfront Fusion con AEM Forms, Workfront Fusion con AEM Forms, Connessione di Workfront Fusion a AEM Forms, AEM Forms e Workfront Fusion, Come collegare Workfront Fusion con AEM Forms?, Connessione di Workfront Fusion a un modulo
topic-tags: author, developer
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 3%

---

# Inviare un modulo adattivo ad Adobe Workfront Fusion

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html?lang=it) automatizza il processo di ripetizione delle stesse attività, ad esempio i flussi di lavoro di approvazione dei documenti, il filtro e l&#39;ordinamento delle e-mail, consentendo di concentrarsi su nuove attività anziché su quelle ricorrenti. Adobe Workfront Fusion include più scenari. Uno scenario è costituito da una serie di moduli che esegue il trasferimento di dati tra applicazioni e servizi web. In uno scenario, puoi aggiungere vari passaggi (moduli) per automatizzare un’attività.

Utilizzando Workfront Fusion, ad esempio, puoi creare uno scenario per raccogliere dati con un modulo adattivo, elaborarli e inviarli a un archivio dati per l’archiviazione. Una volta configurato uno scenario, Workfront Fusion esegue automaticamente le attività ogni volta che un utente compila un modulo, aggiornando senza problemi l’archivio dati.

AEM Forms as a Cloud Service fornisce un connettore OOTB per connettersi e inviare un modulo adattivo ad Adobe Workfront Fusion. L’invio di un modulo ad Adobe Workfront Fusion può offrire diversi vantaggi:
* Ha consentito il trasferimento senza soluzione di continuità dei dati di invio dei moduli ai flussi di lavoro di Workfront Fusion.
* Consente di automatizzare varie attività attivate dall’invio dei moduli. Ciò può includere l&#39;avvio di progetti, l&#39;assegnazione di attività a specifici membri del team, l&#39;invio di notifiche e l&#39;aggiornamento degli stati del progetto, il tutto senza alcun intervento manuale.
* Tutti i moduli inviati acquisiti in Workfront Fusion forniscono un’unica fonte di verità per le informazioni relative al progetto


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

<span> Questo video è applicabile solo ai Componenti core. Per i componenti UE/Foundation, fare riferimento all&#39;articolo.</span>

## Prerequisiti per integrare AEM Forms con Adobe Workfront Fusion {#prerequisites}

Per stabilire una connessione tra Workfront Fusion e AEM Forms, sono necessari i seguenti elementi:

* [Licenza Workfront e Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html?lang=it) valida.
* Un utente di AEM con il diritto di accedere a [Dev Console](https://my.cloudmanager.adobe.com/) per [recuperare le credenziali del servizio](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=it).

## Integrare AEM Forms con Adobe Workfront Fusion

### &#x200B;1. Creare uno scenario Workfront {#workflow-scenario}

Per creare uno scenario Workfront, effettuare le seguenti operazioni:

1. [Creare uno scenario](#create-scenario)
1. [Aggiungere un hook web a uno scenario](#add-webhook)
1. [Aggiungere una connessione a un hook web](#add-connection)

#### Creare uno scenario {#create-scenario}

Per creare uno scenario:

1. Accedi al tuo [account Workfront Fusion](https://app-qa.workfrontfusion.com/).
1. Fai clic su **[!UICONTROL Scenari]** ![Icona Condividi](/help/forms/assets/Smock_ShareAndroid_18_N.svg) nel pannello a sinistra.
1. Fai clic su **[!UICONTROL Crea un nuovo scenario]** nell&#39;angolo superiore destro della pagina. Sullo schermo viene visualizzata una pagina per creare un nuovo scenario.
1. Seleziona **[!UICONTROL Nuovo scenario]** nell&#39;angolo superiore sinistro della pagina e digita un nome appropriato per lo scenario.
1. Fai clic sul punto interrogativo e accertati di aggiungere il primo modulo come **[!UICONTROL AEM Forms]**.

   ![Aggiungi un modulo AEM Forms](/help/forms/assets/workfront-aemforms.png)

   Viene visualizzata la finestra di dialogo **[!UICONTROL Controlla eventi modulo]**.

   >[!NOTE]
   >
   > È obbligatorio aggiungere il primo modulo come **[!UICONTROL AEM Forms]**.

1. Selezionare la finestra di dialogo **[!UICONTROL Controlla eventi modulo]** e viene visualizzata una finestra per aggiungere un webhook.

#### Aggiungi un webhook {#add-webhook}

![Aggiungi un webhook](/help/forms/assets/workfront-add-webhook.png)

Per aggiungere un webhook:

1. Fai clic su **[!UICONTROL Aggiungi]** per visualizzare una finestra di dialogo **[!UICONTROL Aggiungi webhook]**.
1. Specifica un nome per il webhook.

   >[!NOTE]
   >
   > Si consiglia di scegliere con attenzione il nome del webhook, in quanto il nome del webhook specificato viene visualizzato nell’istanza di AEM.

1. Fai clic su **[!UICONTROL Aggiungi]** per aggiungere una nuova connessione. Viene visualizzata la finestra di dialogo **[!UICONTROL Crea connessione]**.

>[!NOTE]
>
> Assicurati che l&#39;account tecnico sia un membro del gruppo **utenti-moduli**; in caso contrario, l&#39;aggiunta di un webhook non riuscirà.

#### Aggiungere una connessione a un webhook {#add-connection}

![Aggiungi una connessione](/help/forms/assets/workfront-add-connection.png)

Per aggiungere una connessione:

1. Specificare un **[!UICONTROL Nome connessione]** nella finestra di dialogo **[!UICONTROL Crea connessione]**.

1. Selezionare **Ambiente** e **Tipo** dall&#39;elenco a discesa.

1. Immetti l&#39;**URL istanza**.

   >[!NOTE]
   >
   > L’URL dell’istanza è l’indirizzo web univoco che punta a un’istanza AEM Forms specifica.

   È possibile recuperare le credenziali del servizio [dalla Console sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=it) necessarie per creare una connessione.

1. Sostituisci `ims-na1.adobelogin.com` nell&#39;endpoint **IMS** con il valore di **imsEndpoint** dalle credenziali del servizio nella console per sviluppatori.

   >[!NOTE]
   >
   > Durante l&#39;aggiunta dell&#39;URL `https://`, mantieni **nella casella di testo** endpoint IMS`imsEndpoint`.

1. Specificare i valori seguenti nella finestra di dialogo **[!UICONTROL Crea connessione]**:
   * Specificare **ID client** con valore di **clientId** dalle credenziali del servizio nella console per sviluppatori.
   * Specificare **Segreto client** con valore di **clientSecret** dalle credenziali del servizio nella console per sviluppatori.
   * Specificare **ID account tecnico** con valore **id** dalle credenziali del servizio nella console Sviluppatore.
   * Specifica **ID organizzazione** con valore di **org** dalle credenziali del servizio nella console per sviluppatori.
   * **Meta ambiti** con valore di **metascopi** dalle credenziali del servizio nella console per sviluppatori.
   * **Chiavi private** con valore di **chiave privata** dalle credenziali del servizio nella console per sviluppatori.

   >[!NOTE]
   >
   >* Per **Chiave privata**, rimuovere `\r\n` dal relativo valore.
   >  Ad esempio, se il valore della chiave privata è:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, quindi dopo aver rimosso `\r\n` dalla chiave privata, la chiave avrà l&#39;aspetto seguente, con entrambi i valori visualizzati in una riga separata:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* È inoltre possibile recuperare una chiave privata o un certificato dal file selezionando il pulsante **Estrai**.

1. Fai clic su **Continua**.

   La connessione creata inizia a essere visualizzata nell&#39;elenco a discesa della **[!UICONTROL Connessione]** nella finestra di dialogo **[!UICONTROL Aggiungi webhook]**.

1. Selezionare la connessione creata **[!UICONTROL Connessione]** dall&#39;elenco a discesa.
1. Fai clic su **[!UICONTROL Salva]**.
1. Fare clic su **[!UICONTROL OK]** e salvare le modifiche per lo scenario.
1. Per attivare lo scenario, fai clic sul pulsante di attivazione/disattivazione nell’editor dello scenario.

>[!NOTE]
>
> Se non attivi lo scenario Workfront, l’invio del modulo non viene rilevato e l’impostazione dell’azione di invio su Workfront genera un invio non riuscito.

### &#x200B;2. Configurare l’azione di invio di un modulo adattivo per Workfront Fusion

>[!BEGINTABS]

>[!TAB Componente di base]

Per configurare l’azione di invio di un modulo adattivo basato su Componenti di base per Workfront Fusion:

1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Invio]** delle proprietà Contenitore modulo adattivo.
1. Dall&#39;elenco a discesa **[!UICONTROL Azione invio]**, selezionare **[!UICONTROL Richiama uno scenario di Workfront Fusion]**.
   ![Azione di invio per Workfront Fusion](/help/forms/assets/workfront-fusion-fc.png)

1. Selezionare **[!UICONTROL Workfront Fusion scenario]** dall&#39;elenco a discesa.
1. Fai clic su **[!UICONTROL Fine]**.


>[!TAB Componente core]

Per configurare l’azione di invio di un modulo adattivo basato su Componenti core per Workfront Fusion:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Azione invio]**, selezionare **[!UICONTROL Richiama uno scenario di Workfront Fusion]**.

   ![Azione di invio per Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)
1. Selezionare **[!UICONTROL Workfront Fusion scenario]** dall&#39;elenco a discesa.
1. Fai clic su **[!UICONTROL Fine]**.

>[!TAB Editor universale]

Per configurare l’azione di invio di un modulo adattivo creato con l’editor universale:

1. Apri il modulo adattivo per la modifica.
1. Fai clic sull&#39;estensione **Modifica proprietà modulo** nell&#39;editor.
Viene visualizzata la finestra di dialogo **Proprietà modulo**.

   >[!NOTE]
   >
   > * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
   > * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

1. Fai clic sulla scheda **Invio** e seleziona **[!UICONTROL Richiama un&#39;azione di invio Scenario di Workfront Fusion]**.

   ![Azione di invio per Workfront Fusion](/help/forms/assets/workfront-fusion-ue.png)

1. Selezionare **[!UICONTROL Workfront Fusion scenario]** dall&#39;elenco a discesa.
1. Fai clic su **[!UICONTROL Salva&amp;Chiudi]**.

>[!ENDTABS]

## Best practice {#best-practices}

* Si consiglia di scegliere con attenzione il nome del webhook, in quanto non è possibile ottenere il nome dello scenario nell’istanza di AEM. Nel caso in cui modificassi il nome del webhook in futuro, questo non verrà più visualizzato nell’elenco a discesa delle azioni di invio di AEM Forms.
* Uno scenario può avere più collegamenti a un webhook, ma alla volta è attivo un solo collegamento a un webhook. Si consiglia di eliminare il webhook non collegato, in modo che non venga visualizzato nell’elenco a discesa delle azioni di invio di AEM Forms.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## Articoli correlati

{{af-submit-action}}