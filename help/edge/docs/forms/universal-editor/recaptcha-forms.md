---
title: Utilizzare reCAPTCHA con Edge Delivery Services per AEM Forms as a Cloud Service
description: Utilizzare Google reCAPTCHA in un modulo per Edge Delivery Services per AEM Forms
feature: Edge Delivery Services
keywords: reCAPTCHA nei moduli, Utilizzo di reCAPTCHA nell’editor universale, Aggiunta di reCAPTCHA nei moduli
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 96%

---


# Utilizzare reCAPTCHA nell’authoring WYSIWYG

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l&#39;accesso, invia un&#39;e-mail dal tuo indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio. Ad esempio, se l&#39;URL del repository è https://github.com/adobe/abc, il nome dell&#39;organizzazione è adobe e il nome del repository è abc.</span>


Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un popolare strumento utilizzato per proteggere i siti web da attività fraudolente, spam e uso improprio.

Ad esempio, prendi in considerazione un modulo che calcola l’imposta in base alle detrazioni aggiuntive e all’aliquota. In tali casi, esiste il rischio che utenti malintenzionati sfruttino il modulo per scopi quali l’invio di e-mail di phishing o l’invio di contenuti irrilevanti o dannosi tramite spambot. L’integrazione di CAPTCHA offre maggiore sicurezza verificando che gli invii provengano da utenti autentici, riducendo in modo efficace gli attacchi di spam.

![reCAPTCHA di Google](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

Nei moduli di Edge Delivery Services, il blocco modulo consente di [collegare Google reCAPTCHA con i moduli](#connect-forms-with-recaptcha-service-by-google) utilizzando il componente **CAPTCHA (Invisible)** per distinguere tra esseri umani e bot. Questa funzionalità consente agli autori di proteggere i moduli da spam e uso improprio.

## Connettere i moduli con il servizio reCAPTCHA di Google

Puoi utilizzare i moduli di Edge Delivery Services per implementare il servizio reCAPTCHA fornito da Google. A seconda delle tue esigenze, per i moduli di Edge Delivery Services puoi configurare uno dei seguenti servizi reCAPTCHA:

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> Per ulteriori informazioni sul funzionamento di reCAPTCHA, consulta [Google reCAPTCHA](https://developers.google.com/recaptcha/).

### Configurare reCAPTCHA Enterprise

reCAPTCHA Enterprise è un servizio premium di rilevamento e prevenzione delle frodi di livello enterprise offerto da Google. Si basa sui fondamenti di reCAPTCHA (basato su punteggi), ma offre funzioni aggiuntive, scalabilità e personalizzazione per soddisfare le complesse esigenze delle aziende.

#### Prima di iniziare

Prima di configurare il servizio reCAPTCHA Enterprise di Google per i moduli di Edge Delivery Services, assicurati di aver completato i seguenti passaggi:

1. Crea o seleziona un [progetto Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) e recupera l’[ID progetto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed).

1. [Abilita l’API reCAPTCHA Enterprise](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) per il tuo progetto Google Cloud e [crea una chiave API](https://console.cloud.google.com/apis/credentials).

1. Crea una [chiave del sito per il progetto Google Cloud](https://console.cloud.google.com/security/recaptcha) e copiala.

Una volta ottenute queste credenziali, puoi procedere con la configurazione di reCAPTCHA Enterprise per i moduli:

1. [Creare un contenitore di configurazione cloud](#1-create-cloud-configuration-container)
1. [Creare la configurazione del servizio cloud per reCAPTCHA Enterprise](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. Creare un contenitore di configurazione cloud

Per creare il contenitore di configurazione cloud, segui questi passaggi:

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** ![Strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.

   ![Contenitore della configurazione cloud](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Nel **[!UICONTROL Browser configurazioni]**, passa al modulo e seleziona **[!UICONTROL Proprietà]**.

   ![Proprietà della configurazione cloud](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   ![Abilitare le proprietà dellaconfigurazione cloud](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`Dopo aver creato il contenitore di configurazione cloud, pubblicalo.

   ![Pubblicare la configurazione cloud](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Creare la configurazione del servizio cloud per reCAPTCHA Enterprise

Per creare la configurazione del servizio cloud per reCAPTCHA Enterprise, segui questi passaggi:

1. Accedi all’istanza di authoring.
1. Passa a **[!UICONTROL Strumenti]** ![Strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL reCAPTCHA]**.

   ![Configurazione cloud reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Viene visualizzata la finestra di dialogo **Configurazioni**.

1. Passa al modulo e seleziona **[!UICONTROL Crea]**.

   ![Configurazione Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Viene visualizzata la finestra di dialogo **[!UICONTROL Crea configurazione reCAPTCHA]**.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Seleziona la versione [!DNL ReCAPTCHA Enterprise] e specifica Titolo, Nome, ID progetto, Chiave sito e Chiave API.

   >[!NOTE]
   >
   > Puoi ottenere l’ID del progetto, la chiave del sito e la chiave API dalla sezione [Prima di iniziare](#before-you-start) per reCAPTCHA Enterprise.

1. Per **[!UICONTROL Tipo di chiave]**, seleziona **Chiave del sito basata su punteggio**.
1. Specifica un [punteggio soglia compreso tra 0 e 1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). Un punteggio superiore o uguale al punteggio soglia identifica un’interazione umana; un punteggio inferiore viene invece considerato come proveniente da un’interazione da parte di un bot.
1. Seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

   Dopo aver creato la configurazione cloud reCAPTCHA, pubblicala.

   ![Pubblicare la configurazione Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

È ora possibile creare o modificare un modulo e aggiungere il componente reCAPTCHA utilizzando l’authoring basato su WYSIWYG. Per istruzioni dettagliate sull’integrazione di Google reCAPTCHA nel modulo, consulta [Utilizzare reCAPTCHA nel modulo](#use-recaptcha-in-your-form).

## Configurare reCAPTCHA

reCAPTCHA è un servizio gratuito offerto da Google che aiuta i siti web a rilevare e prevenire il traffico abusivo, inclusi bot e spam. Supporta una versione basata su punteggio che opera in background e assegna un punteggio di rischio (compreso tra 0,0 e 1,0) a ogni interazione da parte dell’utente. Un punteggio superiore o uguale al punteggio soglia identifica un’interazione umana; un punteggio inferiore viene invece considerato come proveniente da un’interazione da parte di un bot.

#### Prima di iniziare

Prima di configurare Google reCAPTCHA per i moduli Edge Delivery Services, recupera la [coppia di chiavi API reCAPTCHA dalla console Google](https://www.google.com/recaptcha/admin). La coppia include una chiave del sito e una chiave segreta.

>[!NOTE]
>
> * I moduli di Edge Delivery Services supportano solo la versione **reCAPTCHA basata su punteggio**.

Una volta ottenuta la coppia di chiavi API, puoi procedere con la configurazione di reCAPTCHA per i moduli:

1. [Creare un contenitore di configurazione cloud](#1-create-cloud-configuration-container-1)
1. [Creare la configurazione del servizio cloud per reCAPTCHA](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. Creare un contenitore di configurazione cloud

Per creare il contenitore di configurazione cloud, segui questi passaggi:

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** ![Strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.

   ![Contenitore della configurazione cloud](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Nel **[!UICONTROL Browser configurazioni]**, passa al modulo e seleziona **[!UICONTROL Proprietà]**.

   ![Proprietà della configurazione cloud](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   ![Abilitare le proprietà di configurazione cloud](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   Dopo aver creato il contenitore della configurazione cloud, devi pubblicarlo.

   ![Pubblicare la configurazione cloud](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Creare la configurazione del servizio cloud per reCAPTCHA

Per creare la configurazione del servizio cloud per reCAPTCHA, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring.
1. Passa a **[!UICONTROL Strumenti]** ![Strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL reCAPTCHA]**.

   ![Configurazione cloud reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Viene visualizzata la finestra di dialogo **Configurazioni**.

1. Passa al modulo e seleziona **[!UICONTROL Crea]**.

   ![Configurazione Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Viene visualizzata la finestra di dialogo **[!UICONTROL Crea configurazione reCAPTCHA]**.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Seleziona la versione come [!DNL ReCAPTCHA v2] e specifica Titolo e Nome.
1. Immetti la chiave sito e la chiave segreta.

   >[!NOTE]
   >
   > È possibile ottenere la chiave del sito e la chiave segreta dalla sezione [Prima di iniziare](#before-you-begin) di reCAPTCHA.

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

   Dopo aver creato la configurazione cloud reCAPTCHA, pubblicala.

   ![Pubblicare la configurazione reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Ora puoi creare e modificare un modulo e aggiungere il componente reCAPTCHA utilizzando l’authoring basato su WYSIWYG. Per istruzioni dettagliate sull’integrazione di Google reCAPTCHA nel modulo, consulta [Utilizzare reCAPTCHA in un modulo](#use-recaptcha-in-your-form).

### Utilizzare il servizio reCAPTCHA in un modulo

Per creare un modulo e aggiungere il componente reCAPTCHA (invisibile), segui i passaggi indicati:

1. Apri un modulo nell’editor universale per la modifica.
1. Passa alla sezione Modulo adattivo aggiunto nella Struttura contenuto.
1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi il componente **[!UICONTROL CAPTCHA (invisbile)]** dall’elenco **Componenti modulo adattivo**.

   ![Aggiungere un componente reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   È inoltre possibile trascinare i componenti dei Moduli adattivi richiesti, in quanto l’editor universale offre una funzione di trascinamento intuitiva.

1. Fai clic su **Pubblica** per pubblicare nuovamente il modulo dopo l’aggiunta del componente **[!UICONTROL CAPTCHA (invisibile)]**.

   ![ripubblica modulo](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

Ora puoi visualizzare il modulo con il servizio reCAPTCHA al seguente URL:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`.

![Modulo con reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Domande frequenti

* **Cosa succede se un utente non crea una configurazione cloud reCAPTCHA?**

  **R**: se un utente non crea una configurazione cloud reCAPTCHA, il server AEM cerca la configurazione cloud reCAPTCHA nel contenitore di configurazione globale. Se non esiste alcuna configurazione nel contenitore di configurazione globale, il server AEM genera un errore.

* **Cosa succede se un utente crea più configurazioni cloud reCAPTCHA?**
  **R**: se un utente crea più configurazioni cloud reCAPTCHA, il sistema seleziona automaticamente quella che è stata creata per prima.

* **Perché le modifiche o i cambiamenti non sono visibili nell’URL pubblicato?**
Se nell’URL pubblicato non sono visibili modifiche o cambiamenti, assicurati che il modulo venga ripubblicato per applicare gli aggiornamenti.

* **Quale servizio reCAPTCHA supporta i moduli di Edge Delivery Services?**
  **R**: i moduli di Edge Delivery Services supportano solo il servizio reCAPTCHA basato su punteggio fornito da Google.


## Consulta anche

{{universal-editor-see-also}}

