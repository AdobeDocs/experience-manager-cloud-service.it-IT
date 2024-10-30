---
title: Come si utilizza hCaptcha&reg; in un componente core modulo adattivo AEM?
description: Migliora la sicurezza dei moduli con il servizio hCaptcha&reg; senza sforzo. Guida dettagliata all’interno!
topic-tags: Adaptive Forms, author
keywords: hCaptcha&reg; service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: bba5e5d283da616baa57b788181af73d59d86ee3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 25%

---

# Connect your AEM Forms environment with hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:

* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## Integrare l’ambiente AEM Forms con hCaptcha Captcha

Il servizio hCaptcha® protegge i moduli da bot, spam e abusi automatizzati. Pone una sfida in un widget casella di controllo e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il modulo. Questo impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o praticare attività dannose.

AEM Forms as a Cloud Service supporta hCaptcha® nei componenti core di Forms adattivi. Puoi utilizzarlo per presentare una richiesta di verifica del widget casella di controllo all’invio del modulo.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Prerequisiti per integrare l’ambiente AEM Forms con hCaptcha® {#prerequisite}

Per configurare hCaptcha® con AEM Forms, è necessario ottenere la chiave del sito [hCaptcha® e la chiave segreta](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) dal sito Web hCaptcha®.

### Configure hCaptcha® {#steps-to-configure-hcaptcha}

To integrate AEM Forms with hCaptcha® service, perform the following steps:

1. Create a Configuration Container on your AEM Forms as a Cloud Service environment. A Configuration Container holds Cloud Configurations used to connect AEM to external services. To create and configure a Configuration Container to connect your AEM Forms environment with hCaptcha®:
   1. Apri la tua istanza di AEM Forms as a Cloud Service.
   1. ****
   1. In the Configuration Browser, you can select an existing folder or create a folder. You can create a folder and enable the Cloud Configurations option for it or Enable the Cloud Configurations option for an existing folder:

      * To create a folder and enable the Cloud Configurations option for it:
         1. ****
         1. ****
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare l’opzione Configurazioni cloud per una cartella esistente:
         1. Nel Browser configurazioni, selezionare la cartella e selezionare **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il Cloud Service:
   1. Nell&#39;istanza dell&#39;autore AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e seleziona **[!UICONTROL hCaptcha®]**.
      ![hCaptcha® nell&#39;interfaccia utente](assets/hcaptcha-in-ui.png)
   1. Seleziona un Contenitore di configurazione, creato o aggiornato, come descritto nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
      ![Configurazione hCaptcha®](assets/config-hcaptcha.png)
   1. Specificare **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]** e **[!UICONTROL Chiave segreta]** per il servizio hCaptcha® [ottenuto nel prerequisito](#prerequisite). Seleziona **[!UICONTROL Crea]**.

      ![](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > [](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage)[](https://docs.hcaptcha.com/#verify-the-user-response-server-side)

   [](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)

## {#using-hCaptcha®-core-components}

1. Apri la tua istanza di AEM Forms as a Cloud Service.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Proprietà]**. Per l&#39;opzione **[!UICONTROL Contenitore configurazione]**, selezionare il Contenitore configurazione che contiene la configurazione cloud che connette AEM Forms con hCaptcha® e selezionare **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un Contenitore di configurazione di questo tipo, consulta la sezione [Connettere il tuo ambiente AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) per scoprire come creare un Contenitore di configurazione.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser dei componenti, trascina o aggiungi il componente **[!UICONTROL hCaptcha®]** del modulo adattivo al modulo adattivo.
1. Seleziona il componente **[!UICONTROL hCaptcha®]** del modulo adattivo e fai clic sull&#39;icona ![Proprietà icona](assets/configure-icon.svg). Apre la finestra di dialogo delle proprietà. Specifica le seguenti proprietà:

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL Nome]:** Specifica il nome per il componente Captcha. Puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell&#39;editor di regole.
   * ****
   * **[!UICONTROL Impostazioni di configurazione]:** seleziona una configurazione cloud impostata per hCaptcha®.
   * **** Utilizza l’opzione **[!UICONTROL Compatta]** per visualizzare una dimensione ridotta e **[!UICONTROL Normale]** per visualizzare una finestra di dialogo di verifica hCaptcha® di dimensioni relativamente grandi.<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * ****
   * **[!UICONTROL Messaggio di convalida script]**: questa opzione consente di inserire un messaggio da visualizzare in caso di errore di convalida dello script.
     >[!NOTE]
     >You can have multiple Cloud Configurations in your environment for a similar purpose. So, choose the service carefully. [](#connect-your-forms-environment-with-hcaptcha-service)
     <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. Seleziona **[!UICONTROL Fine]**.


Now, only legitimate forms, in which the form filler successfully clears the challenge posed by the hCaptcha® service are allowed for the form submission. hCaptcha®

**hCaptcha® è un marchio registrato di Intuition Machines, Inc.**


## Domande frequenti

* **Q: posso utilizzare più di un componente Captcha in un modulo adattivo?**
* **Ans:** L&#39;utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare un componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}
