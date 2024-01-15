---
title: Integrazione di Adobe Workfront Fusion con l’invio di AEM Forms
description: Adobe Workfront Fusion consente di concentrarsi su nuove attività anziché su attività ripetitive. Puoi collegare Adobe Workfront Fusion a un modulo adattivo utilizzando Invio modulo.
keywords: Inviare un modulo adattivo ad Adobe Workfront Fusion, Integrazione di Adobe Workfront Fusion con AEM Forms Invio, Adobe Workfront Fusion con AEM Forms, Workfront Fusion con AEM Forms, Connessione di Workfront Fusion a AEM Forms, AEM Forms e Workfront Fusion, Come collegare Workfront Fusion con AEM Forms?, Connessione di Workfront Fusion a un modulo
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 975f767e75a268a1638227ae20a533f82724c80a
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Inviare un modulo adattivo ad Adobe Workfront Fusion

<span class="preview"> La funzione è disponibile nel programma per i primi utenti. Puoi scrivere a aem-forms-early-adopter-program@adobe.com dal tuo ID e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) automatizza il processo di ripetizione delle stesse attività, come i flussi di lavoro di approvazione dei documenti, il filtro e l’ordinamento delle e-mail, consentendo di concentrarsi su nuove attività invece di quelle ricorrenti. Adobe Workfront Fusion include più scenari. Uno scenario è costituito da una serie di moduli che esegue il trasferimento di dati tra applicazioni e servizi web. In uno scenario, puoi aggiungere vari passaggi (moduli) per automatizzare un’attività.

Utilizzando Workfront Fusion, ad esempio, puoi creare uno scenario per raccogliere dati con un modulo adattivo, elaborarli e inviarli a un archivio dati per l’archiviazione. Una volta configurato uno scenario, Workfront Fusion esegue automaticamente le attività ogni volta che un utente compila un modulo, aggiornando senza problemi l’archivio dati.

## Vantaggi dell&#39;utilizzo di Adobe Workfront Fusion{#advatages-of-workfront-fusion}

Alcuni dei vantaggi dell’utilizzo di Adobe Workfront Fusion con AEM Forms:

- Invio di dati acquisiti con Adaptive Forms a uno scenario Workfront Fusion
- Automatizzare le attività meno soggette a errori.
- Personalizzazione dei requisiti specifici di un&#39;organizzazione non inclusi direttamente in Workfront.
- Gestione di logiche semplici e decisioni semplici, ad esempio, istruzioni if/then.

## Prerequisiti per integrare AEM Forms con Adobe Workfront Fusion {#prerequisites}

I prerequisiti necessari per collegare Workfront Fusion ad AEM Forms sono:

- Un valore valido [Licenza Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
- Un utente AEM con diritto di accesso [Console di sviluppo](https://my.cloudmanager.adobe.com/) a [recuperare le credenziali del servizio](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## Integrare AEM Forms con Adobe Workfront Fusion

Per connettersi [Workfront fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) in un modulo, effettuare le seguenti operazioni:

### 1. Creare uno scenario Workfront {#workflow-scenario}

Per creare uno scenario Workfront:
1. Accedi al tuo [Account Workfront Fusion](https://app-qa.workfrontfusion.com/).
1. Clic **[!UICONTROL Scenari]** ![Icona Condividi](/help/forms/assets/Smock_ShareAndroid_18_N.svg) nel pannello a sinistra.
1. Clic **[!UICONTROL Crea un nuovo scenario]** nell’angolo superiore destro della pagina. Sullo schermo viene visualizzata una pagina per creare un nuovo scenario.
1. Seleziona **[!UICONTROL Nuovo scenario]** nell’angolo in alto a sinistra della pagina e digita un nome appropriato per lo scenario.
1. Fai clic sul punto interrogativo e accertati di aggiungere il primo modulo come **[!UICONTROL AEM Forms]**.

   ![Aggiungere un modulo AEM Forms](/help/forms/assets/workfront-aemforms.png)

   Il **[!UICONTROL Osserva eventi modulo]** viene visualizzata.

   >[!NOTE]
   >
   > È obbligatorio aggiungere il primo modulo come **[!UICONTROL AEM Forms]**.

1. Seleziona la **[!UICONTROL Osserva eventi modulo]** e viene visualizzata una finestra per aggiungere un webhook.

#### 1.1 Aggiungere un webhook {#add-webhook}

![Aggiungi un webhook](/help/forms/assets/workfront-add-webhook.png)

Per aggiungere un webhook:

1. Clic **[!UICONTROL Aggiungi]** e un **[!UICONTROL Aggiungi un webhook]** viene visualizzata.
1. Specifica un nome per il webhook.

   >[!NOTE]
   >
   > Si consiglia di scegliere con attenzione il nome del webhook, in quanto il nome del webhook specificato viene visualizzato nell’istanza dell’AEM.

1. Clic **[!UICONTROL Aggiungi]** per aggiungere una nuova connessione. Il **[!UICONTROL Creare una connessione]** viene visualizzata.

#### 1.2 Aggiungere una connessione a un webhook {#add-connection}

![Aggiungi una connessione](/help/forms/assets/workfront-add-connection.png)

Per aggiungere una connessione:

1. Specifica un **[!UICONTROL Nome connessione]** nel **[!UICONTROL Creare una connessione]** .

1. Seleziona **Ambiente** e **Tipo** dall’elenco a discesa.

1. Inserisci il **URL istanza**.

   >[!NOTE]
   >
   > L’URL dell’istanza è l’indirizzo web univoco che punta a un’istanza AEM Forms specifica.

   È possibile recuperare [credenziali del servizio da Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) necessario per creare una connessione.

1. Sostituisci `ims-na1.adobelogin.com` nel **Endpoint IMS** con il valore di **imsEndpoint** dalle credenziali del servizio nella Console sviluppatori.

   >[!NOTE]
   >
   > Mantieni `https://` nel **Endpoint IMS** casella di testo durante l’aggiunta di `imsEndpoint` URL.

1. Specifica i seguenti valori nella **[!UICONTROL Creare una connessione]** finestra di dialogo:
   - Specifica **ID client** con valore di **clientId** dalle credenziali del servizio nella Console sviluppatori.
   - Specifica **Segreto client** con valore di **clientSecret** dalle credenziali del servizio nella Console sviluppatori.
   - Specifica **ID account tecnico**  con valore di **id** dalle credenziali del servizio nella Console sviluppatori.
   - Specifica **ID organizzazione**  con valore di **org** dalle credenziali del servizio nella Console sviluppatori.
   - **Meta ambiti**  con valore di **metascopi** dalle credenziali del servizio nella Console sviluppatori.
   - **Chiavi private**  con valore di **privateKey** dalle credenziali del servizio nella Console sviluppatori.

   >[!NOTE]
   >
   >- Per **Chiave privata**, rimuovere `\r\n` dal relativo valore.
   >  Ad esempio, se il valore della chiave privata è:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, quindi dopo aver rimosso `\r\n` dalla chiave privata, la chiave avrà l’aspetto seguente, con entrambi i valori visualizzati in una riga separata:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >- Puoi anche recuperare una chiave privata o un certificato dal file selezionando la **Extract** pulsante.

1. Fai clic su **Continua**.

   La connessione creata inizia a essere visualizzata nell’elenco a discesa del **[!UICONTROL Connessione]** nel **[!UICONTROL Aggiungi un webhook]** .

1. Seleziona la connessione creata **[!UICONTROL Connessione]** dall’elenco a discesa.
1. Fai clic su **[!UICONTROL Salva]**.
1. Clic **[!UICONTROL OK]** e salva le modifiche per lo scenario.

#### 1.3 Attivare lo scenario Workfront {#activate-scenario}

Per attivare lo scenario:

1. Clic **[!UICONTROL Scenari]** ![Icona Condividi](/help/forms/assets/Smock_ShareAndroid_18_N.svg) nel pannello a sinistra.
1. Fai clic su **[!UICONTROL Scenario inattivo]** scheda.
1. Fai clic su **ON/OFF** pulsante di attivazione/disattivazione per lo scenario AEM Forms.

Quando fai clic sul pulsante di attivazione/disattivazione, lo scenario Workfront inizia a essere visualizzato nel **[!UICONTROL Scenario attivo]** scheda.

>[!NOTE]
>
> Se non attivi lo scenario Workfront, l’invio del modulo non viene rilevato e l’impostazione dell’azione di invio su Workfront genera un invio non riuscito.

### 2. Configurare l’azione di invio di un modulo adattivo per Workfront Fusion

È possibile configurare l’azione di invio per Workfont Fusion per:
- [Nuovo Forms adattivo](#new-af-submit-action)
- [Moduli adattivi esistenti](#existing-af-submit-action)

#### Configurare l’azione di invio del nuovo modulo adattivo per Workfront Fusion {#new-af-submit-action}

Per configurare l’azione di invio del nuovo modulo adattivo per Workfront Fusion:

1. Accedi all’istanza AEM.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]** > **[!UICONTROL Crea]** > **[!UICONTROL Modulo adattivo]**. Il **[!UICONTROL Crea modulo]** viene visualizzata la procedura guidata.
1. Seleziona un modello di modulo adattivo dall’ **[!UICONTROL Sorgente]** scheda.
1. Seleziona un tema da **[!UICONTROL Stile]** scheda.

   ![Azione di invio per Workfront Fusion](/help/forms/assets/workfront-scenario-new-af.png)

1. Seleziona la **[!UICONTROL Richiama uno scenario Workfront Fusion]** dal **[!UICONTROL Invio]** scheda.
1. Seleziona il webhook creato da **[!UICONTROL Opzioni]** scheda in **[!UICONTROL Proprietà]** finestra.

   >[!NOTE]
   >
   > Il nome del webhook dello scenario Workfront viene visualizzato nel **Opzioni** elenco a discesa.

1. Fai clic su **[!UICONTROL Crea]**.
1. Specifica il nome per il nuovo modulo adattivo e fai clic su **[!UICONTROL Crea]**.

#### Configurare l’azione di invio del modulo adattivo esistente per Workfront Fusion {#existing-af-submit-action}

Per configurare l’azione di invio del modulo adattivo esistente per Workfront Fusion:

1. Accedi all’istanza AEM.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un modulo adattivo e apri il modulo in modalità di modifica.
1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).

   ![Azione di invio per Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)

1. Apri **[!UICONTROL Invio]** scheda.
1. Seleziona la **[!UICONTROL Azione di invio]** as **[!UICONTROL Richiama uno scenario Workfront Fusion]**
1. Seleziona **[!UICONTROL Scenario Workfront Fusion]** dall’elenco a discesa.
1. Clic **[!UICONTROL Fine]**.

## Best practice {#best-practices}

- Si consiglia di scegliere con attenzione il nome del webhook, in quanto non è possibile ottenere il nome dello scenario nell’istanza dell’AEM. Nel caso in cui modificassi il nome del webhook in futuro, questo non verrà più visualizzato nell’elenco a discesa delle azioni di invio di AEM Forms.
- Uno scenario può avere più collegamenti a un webhook, ma alla volta è attivo un solo collegamento a un webhook. Si consiglia di eliminare il webhook non collegato, in modo che non venga visualizzato nell’elenco a discesa delle azioni di invio di AEM Forms.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->
