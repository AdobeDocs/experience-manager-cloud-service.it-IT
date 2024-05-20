---
title: Come si utilizza hCaptcha® in un componente core modulo adattivo AEM?
description: Migliora la sicurezza dei moduli con il servizio hCaptcha®. Guida passo passo all'interno!
topic-tags: Adaptive Forms, author
keywords: Servizio hCaptcha®, Forms adattivo, sfida CAPTCHA, prevenzione dei bot, componenti core, sicurezza dell’invio dei moduli, prevenzione della posta indesiderata dei moduli
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
source-git-commit: a8a31bae0f937aa8941d258af648d6be030a9fac
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 3%

---

# Connetti il tuo ambiente AEM Forms con hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Questa funzione è disponibile nel programma di adozione anticipata. Puoi scrivere a aem-forms-ea@adobe.com dal tuo ID e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità. </span>

Il servizio hCaptcha® protegge i moduli da bot, spam e abusi automatizzati. Crea una sfida al widget di casella di controllo e valuta la risposta dell’utente per determinare se è un utente o un bot che interagisce con il modulo. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o attività dannose.

AEM Forms as a Cloud Service supporta hCaptcha® nei componenti core di Forms adattivi. Puoi utilizzarlo per presentare una richiesta di verifica del widget casella di controllo all’invio del modulo.

<!-- ![hCaptcha®](assets/hCaptcha®-challenge.png)-->


## Prerequisiti per integrare l’ambiente AEM Forms con hCaptcha® {#prerequisite}

Per configurare hCaptcha® con AEM Forms, è necessario ottenere il [hCaptcha® chiave del sito e chiave segreta](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) dal sito web hCaptcha®.

## Passaggi per configurare hCaptcha® {#steps-to-configure-hcaptcha}

Per integrare AEM Forms con il servizio hCaptcha®, effettua le seguenti operazioni:

1. Crea un Contenitore di configurazione nell’ambiente as a Cloud Service AEM Forms. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un contenitore di configurazione per collegare il tuo ambiente AEM Forms con hCaptcha®:
   1. Apri l’istanza as a Cloud Service di AEM Forms.
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

1. Apri l’istanza as a Cloud Service di AEM Forms.
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
   * **[!UICONTROL Impostazioni di configurazione]:** Seleziona una configurazione cloud configurata per hCaptcha®.
   * **Dimensione Captcha:** Puoi selezionare la dimensione di visualizzazione della finestra di dialogo della sfida hCaptcha®. Utilizza il **[!UICONTROL Compatto]** per visualizzare una dimensione ridotta e il **[!UICONTROL Normale]** per visualizzare una finestra di dialogo di verifica hCaptcha® di dimensioni relativamente grandi.<!-- or **[!UICONTROL Invisible]** to validate hCaptcha® without explicitly rendering the checkbox widget on the user interface. -->
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
