---
title: Utilizzare reCAPTCHA con Edge Delivery Services per AEM Forms as a Cloud Service
description: Utilizzare Google reCAPTCHA in un modulo per Edge Delivery Services per AEM Forms
feature: Edge Delivery Services
keywords: reCAPTCHA nei moduli, Utilizzo di reCAPTCHA nell’Editor universale, Aggiunta di reCAPTCHA nei moduli
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 320ab86bc73e874705d985b927e90eec3cad1cf9
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 6%

---


# Utilizzare reCAPTCHA nell’authoring di WYSIWYG

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un popolare strumento utilizzato per proteggere i siti web da attività fraudolente, spam e uso improprio.

Si consideri, ad esempio, una maschera che calcola l&#39;imposta in base alle detrazioni aggiuntive e all&#39;aliquota. In tali casi, esiste il rischio che utenti malintenzionati sfruttino il modulo per scopi quali l’invio di e-mail di phishing o l’invio di contenuti irrilevanti o dannosi tramite spambot. L’integrazione del CAPTCHA offre maggiore sicurezza verificando che gli invii provengano da utenti autentici, riducendo in modo efficace le voci spam.

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

In Edge Delivery Services Forms, il blocco di modulo consente di [collegare Google reCAPTCHA con i moduli](#connect-forms-with-recaptcha-service-by-google) utilizzando il componente **Captcha(Invisible)** per distinguere tra esseri umani e bot. Questa funzionalità consente agli autori di proteggere i moduli da spam e utilizzo non corretto.

## Connettere Forms con il servizio reCAPTCHA di Google

Puoi creare Edge Delivery Services Forms per implementare il servizio reCAPTCHA fornito da Google. A seconda delle tue esigenze, puoi configurare uno dei seguenti servizi reCAPTCHA per il Forms Edge Delivery Services:

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> Per ulteriori informazioni sul funzionamento di reCAPTCHA, vedere [Google reCAPTCHA](https://developers.google.com/recaptcha/).

### Configurare reCAPTCHA Enterprise

reCAPTCHA Enterprise è un servizio premium di rilevamento e prevenzione delle frodi di livello enterprise offerto da Google. Si basa sulle basi di reCAPTCHA (basato su punteggi), ma offre funzioni aggiuntive, scalabilità e personalizzazione per soddisfare le complesse esigenze delle aziende.

#### Prima di iniziare

Prima di configurare Google reCAPTCHA Enterprise per Edge Delivery Services Forms, assicurati di aver completato i seguenti passaggi:

1. Crea o seleziona un [progetto Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) e recupera il [ID progetto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed).

1. [Abilita l&#39;API aziendale reCAPTCHA](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) per il tuo progetto Google Cloud e [crea una chiave API](https://console.cloud.google.com/apis/credentials).

1. Crea una [chiave del sito per il progetto Google Cloud](https://console.cloud.google.com/security/recaptcha) e copia la chiave del sito.

Una volta ottenute queste credenziali, puoi procedere con la configurazione di reCAPTCHA Enterprise per i moduli:

1. [Crea contenitore configurazione cloud](#1-create-cloud-configuration-container)
1. [Creare la configurazione del servizio cloud per reCAPTCHA Enterprise](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. Creare un contenitore di configurazione cloud

Per creare il contenitore di configurazione cloud, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** ![Strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.

   ![Contenitore configurazione cloud](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Nel **[!UICONTROL Browser configurazioni]**, passa al modulo e seleziona **[!UICONTROL Proprietà]**.

   ![Proprietà configurazione cloud](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   ![Abilita proprietà configurazione cloud](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
Dopo aver creato il contenitore di configurazione cloud, pubblicalo.

   ![Pubblica configurazione cloud](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Creare la configurazione del servizio cloud per reCAPTCHA Enterprise

Per creare la configurazione del servizio cloud per reCAPTCHA Enterprise, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring.
1. Passa a **[!UICONTROL Strumenti]** ![strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL reCAPTCHA]**.

   ![Configurazione cloud Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Viene visualizzata la finestra di dialogo **Configurazioni**.

1. Passa al modulo e seleziona **[!UICONTROL Crea]**.

   ![Configurazione Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Viene visualizzata la finestra di dialogo **[!UICONTROL Crea configurazione reCAPTCHA]**.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Selezionare la versione come [!DNL ReCAPTCHA Enterprise] e specificare Titolo, Nome, ID progetto, Chiave sito e Chiave API.

   >[!NOTE]
   >
   > Puoi ottenere l&#39;ID progetto, la chiave del sito e la chiave API dalla sezione [Prima di iniziare](#before-you-start) per l&#39;organizzazione reCAPTCHA.

1. Seleziona **[!UICONTROL Tipo chiave]** come **Chiave sito basata su punteggio**.
1. Specifica un punteggio di soglia [ compreso tra 0 e 1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). I punteggi superiori o uguali ai punteggi di soglia identificano l’interazione umana, altrimenti considerata come interazione da bot.
1. Seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

   Dopo aver creato la configurazione cloud reCAPTCHA, pubblicala.

   ![Pubblica configurazione Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

È ora possibile creare o modificare un modulo e aggiungere il componente reCAPTCHA utilizzando l’authoring basato su WYSIWYG. Per istruzioni dettagliate sull&#39;integrazione di Google reCAPTCHA nel modulo, consulta [Utilizzare reCAPTCHA nel modulo](#use-recaptcha-in-your-form).

## Configurare reCAPTCHA

reCAPTCHA è un servizio gratuito offerto da Google che aiuta i siti web a rilevare e prevenire il traffico abusivo, inclusi bot e spam. Supporta una versione basata su punteggio che opera in background e assegna un punteggio di rischio (compreso tra 0,0 e 1,0) a ogni interazione dell’utente. I punteggi superiori o uguali ai punteggi di soglia identificano l’interazione umana, altrimenti considerata come interazione da bot.

#### Prima di iniziare

Prima di configurare Google reCAPTCHA per Edge Delivery Services Forms, recupera la coppia di chiavi API [reCAPTCHA dalla console Google](https://www.google.com/recaptcha/admin). La coppia include una chiave del sito e una chiave segreta.

>[!NOTE]
>
> * Edge Delivery Services Forms supporta solo la versione **reCAPTCHA Score based**.

Una volta ottenuta la coppia di chiavi API, puoi procedere con la configurazione di reCAPTCHA per i moduli:

1. [Crea contenitore configurazione cloud](#1-create-cloud-configuration-container-1)
1. [Creare la configurazione del servizio cloud per reCAPTCHA](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. Creare un contenitore di configurazione cloud

Per creare il contenitore di configurazione cloud, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** ![Strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.

   ![Contenitore configurazione cloud](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Nel **[!UICONTROL Browser configurazioni]**, passa al modulo e seleziona **[!UICONTROL Proprietà]**.

   ![Proprietà configurazione cloud](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Nella finestra di dialogo **[!UICONTROL Proprietà configurazione]**, abilita **[!UICONTROL Configurazioni cloud]**.

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   ![Abilita proprietà configurazione cloud](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   Dopo aver creato il contenitore di configurazione cloud, pubblicalo.

   ![Pubblica configurazione cloud](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Creare la configurazione del servizio cloud per reCAPTCHA

Per creare la configurazione del servizio cloud per reCAPTCHA, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring.
1. Passa a **[!UICONTROL Strumenti]** ![strumenti-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL reCAPTCHA]**.

   ![Configurazione cloud Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Viene visualizzata la finestra di dialogo **Configurazioni**.

1. Passa al modulo e seleziona **[!UICONTROL Crea]**.

   ![Configurazione Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Viene visualizzata la finestra di dialogo **[!UICONTROL Crea configurazione reCAPTCHA]**.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Selezionare la versione come [!DNL ReCAPTCHA v2] e specificare Titolo e Nome.
1. Specifica la chiave del sito e la chiave segreta.

   >[!NOTE]
   >
   > È possibile ottenere la chiave del sito e la chiave segreta dalla sezione [Prima di iniziare](#before-you-begin) per reCAPTCHA.

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

   Dopo aver creato la configurazione cloud reCAPTCHA, pubblicala.

   ![Pubblica configurazione Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

È ora possibile creare e modificare un modulo e aggiungere il componente reCAPTCHA utilizzando l’authoring basato su WYSIWYG. Per istruzioni dettagliate sull&#39;integrazione di Google reCAPTCHA nel modulo, consulta [Utilizzare reCAPTCHA nel modulo](#use-recaptcha-in-your-form).

### Utilizzare reCAPTCHA nel modulo

Per creare un modulo e aggiungere il componente reCAPTCHA (invisibile), effettua le seguenti operazioni:

1. Apri un modulo nell’editor universale per la modifica.
1. Passa alla sezione Modulo adattivo aggiunto nella Struttura contenuto.
1. Fai clic sull&#39;icona **[!UICONTROL Aggiungi]** e aggiungi il componente **[!UICONTROL Captcha (invisibile)]** dall&#39;elenco **Componenti modulo adattivo**.

   ![Aggiungi componente reCaptcha](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   È inoltre possibile trascinare e rilasciare il componente Forms adattivo richiesto, in quanto Universal Editor offre una funzione di trascinamento intuitiva.

1. Fai clic su **Pubblica** per pubblicare nuovamente il modulo dopo l&#39;aggiunta del componente **[!UICONTROL Captcha (non visibile)]**.

   ![ripubblica modulo](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

Ora puoi visualizzare il modulo con il servizio reCAPTCHA al seguente URL:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`.

![Modulo con reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Domande frequenti

* **Cosa succede se un utente non crea una configurazione cloud reCAPTCHA?**

  **A**: se un utente non crea una configurazione cloud reCAPTCHA, il server AEM cerca la configurazione cloud reCAPTCHA nel contenitore di configurazione globale. Se non esiste alcuna configurazione nel contenitore di configurazione globale, il server AEM genera un errore.

* **Cosa succede se un utente crea più configurazioni cloud reCAPTCHA?**
  **A**: se un utente crea più configurazioni cloud reCAPTCHA, il sistema seleziona automaticamente la prima configurazione reCAPTCHA creata.

* **Perché le modifiche non sono visibili nell&#39;URL pubblicato?**
Se nell’URL pubblicato non sono visibili modifiche o modifiche, assicurati che il modulo venga ripubblicato per applicare gli aggiornamenti.

* **Quale servizio reCAPTCHA supporta Edge Delivery Services Forms?**
  **A**: Edge Delivery Services Forms supporta solo il servizio reCAPTCHA basato su punteggio fornito da Google.


## Consulta anche

{{see-more-forms-eds}}
