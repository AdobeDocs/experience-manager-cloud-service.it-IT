---
title: Come si utilizza hCaptcha&reg; in un modulo adattivo per AEM?
description: Migliora la sicurezza dei moduli con il servizio hCaptcha&reg; senza sforzo. Guida dettagliata all’interno!
topic-tags: Adaptive Forms, author
keywords: hCaptcha&reg; service, Forms adattivo, CAPTCHA challenge, prevenzione bot, sicurezza invio modulo, prevenzione spam modulo
feature: Adaptive Forms, Foundation Components
role: User, Developer
source-git-commit: 553f456f0eab43cee11fb9e66ce9e1dbacdc2b5c
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 19%

---

# Connetti il tuo ambiente AEM Forms con hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Questa funzione è in fase di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:

* [hCaptcha](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Tornello Cloudflare](/help/forms/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)

## Integrare l’ambiente AEM Forms con hCaptcha Captcha

Il servizio hCaptcha® protegge i moduli da bot, spam e abusi automatizzati. Pone una sfida in un widget casella di controllo e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il modulo. Questo impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o praticare attività dannose.

AEM Forms as a Cloud Service supporta hCaptcha® in Adaptive Forms. Puoi utilizzarlo per presentare una richiesta di verifica del widget casella di controllo all’invio del modulo.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->

## Prerequisiti per integrare l’ambiente AEM Forms con hCaptcha® {#prerequisite}

Per configurare hCaptcha® con AEM Forms, è necessario ottenere la chiave del sito [hCaptcha® e la chiave segreta](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) dal sito Web hCaptcha®.

## Passaggi per configurare hCaptcha® {#steps-to-configure-hcaptcha}

1. Crea un Contenitore di configurazione nell’ambiente AEM Forms as a Cloud Service. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un contenitore di configurazione per collegare il tuo ambiente AEM Forms con hCaptcha®:
   1. Apri la tua istanza di AEM Forms as a Cloud Service.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Nel Browser configurazioni, puoi selezionare una cartella esistente o crearne una. Puoi creare una cartella e abilitare per essa l’opzione Configurazioni cloud oppure abilitare l’opzione Configurazioni cloud per una cartella esistente:

      * **Per creare una cartella e abilitare l&#39;opzione Configurazioni cloud**:
         1. Nel browser configurazioni fare clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica un nome e un titolo, quindi seleziona l&#39;opzione **[!UICONTROL Configurazioni cloud]**.
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

      ![Configura il Cloud Service per connettere il tuo ambiente AEM Forms con hCaptcha®](assets/create-hcaptcha-config.png)

>[!NOTE]
> Gli utenti non devono modificare [URL di convalida JavaScript lato client](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) e [URL di convalida lato server](https://docs.hcaptcha.com/#verify-the-user-response-server-side) in quanto sono già precompilati per la convalida hCaptcha®. Per alcuni paesi, gli endpoint possono essere diversi. Per ulteriori informazioni, visita [hCaptcha® Domande frequenti](https://docs.hcaptcha.com/faq#does-hcaptcha-support-access-by-users-in-china).

Una volta configurato, il servizio hCAPTCHA è disponibile per l’utilizzo in un modulo adattivo.

## Utilizzare hCaptcha® in un modulo adattivo{#using-hCaptcha®-foundation-components}

1. Apri la tua istanza di AEM Forms as a Cloud Service.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Proprietà]**. Per l&#39;opzione **[!UICONTROL Contenitore configurazione]**, selezionare il Contenitore configurazione che contiene la configurazione cloud che connette AEM Forms con hCaptcha®, quindi selezionare **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un Contenitore di configurazione di questo tipo, consulta la sezione [Connettere il tuo ambiente AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) per scoprire come creare un Contenitore di configurazione.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser componenti, trascina il componente **[!UICONTROL Captcha]** nel modulo adattivo.
1. Seleziona il componente **[!UICONTROL Captcha]** e fai clic sull&#39;icona ![Proprietà](assets/configure-icon.svg). Apre la finestra di dialogo delle proprietà.

   ![testo alternativo](assets/hcaptcha-properties.png)

   Specifica le seguenti proprietà:

   * **[!UICONTROL Titolo]:** Specifica il titolo del componente Captcha. Puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell&#39;editor di regole.
   * **[!UICONTROL Messaggio di convalida]:** Fornisci un messaggio di convalida per la convalida Captcha al momento dell&#39;invio del modulo.
   * **[!UICONTROL Convalida Captcha]:** È possibile selezionare una delle opzioni per la convalida Captcha:
      * All’invio del modulo
      * Su un’azione dell’utente.
   * **[!UICONTROL Servizio Captcha]:** Seleziona il servizio Captcha, qui selezioni il servizio hCaptcha®.
   * **[!UICONTROL Configurazione Captcha]:** Seleziona una configurazione cloud configurata per hCaptcha®.
     >[!NOTE]
     >Puoi avere più configurazioni cloud nell’ambiente per uno scopo simile. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Connettere l&#39;ambiente AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) per scoprire come creare un Cloud Service che colleghi l&#39;ambiente AEM Forms al servizio hCaptcha®.

   * **Messaggio di errore:** Fornisci il messaggio di errore da visualizzare all&#39;utente quando l&#39;invio Captcha non riesce.
   * **Dimensione Captcha:** È possibile selezionare la dimensione di visualizzazione della finestra di dialogo di verifica hCaptcha®. Utilizza l&#39;opzione **[!UICONTROL Compact]** per visualizzare una finestra di dialogo di verifica hCaptcha® di piccole dimensioni e l&#39;opzione **[!UICONTROL Normal]** per visualizzare una finestra di dialogo di verifica hCaptcha di dimensioni relativamente grandi oppure **[!UICONTROL Invisible]** per convalidare hCaptcha® senza eseguire il rendering esplicito del widget della casella di controllo nell&#39;interfaccia utente.

1. Seleziona **[!UICONTROL Fine]**.

Ora, solo i moduli legittimi, in cui il compilatore di moduli elimina con successo la sfida posta dal servizio hCaptcha® sono consentiti per l’invio del modulo.

**hCaptcha® è un marchio registrato di Intuition Machines, Inc.**

## Domande frequenti

* **Q: posso utilizzare più di un componente Captcha in un modulo adattivo?**
* **Ans:** L&#39;utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare un componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}
