---
title: Come si utilizza hCaptcha&reg; in un componente core modulo adattivo AEM?
description: Migliora la sicurezza dei moduli con il servizio hCaptcha&reg; senza sforzo. Guida dettagliata all’interno!
topic-tags: Adaptive Forms, author
keywords: hCaptcha&reg; servizio, Forms adattivo, sfida CAPTCHA, prevenzione bot, componenti core, sicurezza invio moduli, prevenzione posta indesiderata moduli
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 24%

---

# Connetti il tuo ambiente AEM Forms con hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Questa funzione è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:

* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [Tornello Cloudflare](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## Integrare l’ambiente AEM Forms con hCaptcha Captcha

Il servizio hCaptcha® protegge i moduli da bot, spam e abusi automatizzati. Pone una sfida in un widget casella di controllo e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il modulo. Questo impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o praticare attività dannose.

AEM Forms as a Cloud Service supporta hCaptcha® nei componenti core di Forms adattivi. Puoi utilizzarlo per presentare una richiesta di verifica del widget casella di controllo all’invio del modulo.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Prerequisiti per integrare l’ambiente AEM Forms con hCaptcha® {#prerequisite}

Per configurare hCaptcha® con AEM Forms, è necessario ottenere il [hCaptcha® chiave del sito e chiave segreta](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) dal sito web hCaptcha®.

### Configurare hCaptcha® {#steps-to-configure-hcaptcha}

Per integrare AEM Forms con il servizio hCaptcha®, effettua le seguenti operazioni:

1. Crea un Contenitore di configurazione nell’ambiente AEM Forms as a Cloud Service. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un contenitore di configurazione per collegare il tuo ambiente AEM Forms con hCaptcha®:
   1. Apri la tua istanza di AEM Forms as a Cloud Service.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Nel Browser configurazioni, puoi selezionare una cartella esistente o crearne una. Puoi creare una cartella e abilitare per essa l’opzione Configurazioni cloud o Abilitare l’opzione Configurazioni cloud per una cartella esistente:

      * Per creare una cartella e abilitare l’opzione Configurazioni cloud:
         1. Nel browser configurazioni, fai clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica un nome e un titolo, quindi seleziona la **[!UICONTROL Configurazioni cloud]** opzione.
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare l’opzione Configurazioni cloud per una cartella esistente:
         1. Nel browser configurazioni, seleziona la cartella e fai clic su **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il Cloud Service:
   1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e seleziona **[!UICONTROL Captcha®]**.
      ![hCaptcha® nell’interfaccia utente](assets/hcaptcha-in-ui.png)
   1. Seleziona un Contenitore di configurazione, creato o aggiornato, come descritto nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
      ![hCaptcha di configurazione®](assets/config-hcaptcha.png)
   1. Specifica **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]**, e **[!UICONTROL Chiave segreta]** per il servizio hCaptcha® [ottenuto nel prerequisito](#prerequisite). Seleziona **[!UICONTROL Crea]**.

      ![Configura il Cloud Service per collegare il tuo ambiente AEM Forms con hCaptcha®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Gli utenti non devono modificare [URL di convalida JavaScript lato client](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) e [URL di convalida lato server](https://docs.hcaptcha.com/#verify-the-user-response-server-side) in quanto sono già precompilati per la convalida hCaptcha®.

   Una volta configurato, il servizio hCAPTCHA è disponibile per l’utilizzo in un [Modulo adattivo basato su componenti core](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Utilizzare hCaptcha® in un componente core di Forms adattivo {#using-hCaptcha®-core-components}

1. Apri la tua istanza di AEM Forms as a Cloud Service.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Proprietà]**. Per **[!UICONTROL Contenitore configurazione]** , seleziona il Contenitore di configurazione contenente la Configurazione cloud che connette AEM Forms con hCaptcha® quindi fai clic su **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un contenitore di configurazione di questo tipo, consulta la sezione [Connetti il tuo ambiente AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) per scoprire come creare un contenitore di configurazione.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser Componenti, trascina o aggiungi il **[!UICONTROL hCaptcha modulo adattivo®]** nel modulo adattivo.
1. Seleziona la **[!UICONTROL hCaptcha modulo adattivo®]** e fare clic su proprietà ![Icona Proprietà](assets/configure-icon.svg) icona. Apre la finestra di dialogo delle proprietà. Specifica le seguenti proprietà:

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL Nome]:** Specificando il nome del componente Captcha, puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell’editor di regole.
   * **[!UICONTROL Titolo]:** Specifica il titolo del componente Captcha.
   * **[!UICONTROL Impostazioni di configurazione]:** seleziona una configurazione cloud impostata per hCaptcha®.
   * **Dimensione Captcha:** Puoi selezionare la dimensione di visualizzazione della finestra di dialogo della sfida hCaptcha®. Utilizza l’opzione **[!UICONTROL Compatta]** per visualizzare una dimensione ridotta e **[!UICONTROL Normale]** per visualizzare una finestra di dialogo di verifica hCaptcha® di dimensioni relativamente grandi.<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL Messaggio di convalida]:** Fornisci un messaggio di convalida per la convalida Captcha al momento dell’invio del modulo.
   * **[!UICONTROL Messaggio di convalida script]**: questa opzione consente di inserire un messaggio da visualizzare in caso di errore di convalida dello script.
     >[!NOTE]
     >Puoi avere più configurazioni cloud nell’ambiente per uno scopo simile. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Connetti il tuo ambiente AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) per scoprire come creare un Cloud Service che colleghi il tuo ambiente AEM Forms al servizio hCaptcha®.
     <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. Seleziona **[!UICONTROL Fine]**.


Ora, solo i moduli legittimi, in cui il compilatore di moduli elimina con successo la sfida posta dal servizio hCaptcha® sono consentiti per l’invio del modulo. hCaptcha®

**hCaptcha® è un marchio registrato di Intuition Machines, Inc.**


## Domande frequenti

* **D: Posso utilizzare più di un componente Captcha in un modulo adattivo?**
* **Ans:** L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare un componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}
