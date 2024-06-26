---
title: Come si utilizza Google reCAPTCHA in un modulo adattivo per AEM?
description: Migliora la sicurezza dei moduli con il servizio Google reCAPTCHA. Guida dettagliata all’interno!
topic-tags: Adaptive Forms, author
keywords: Servizio Google reCAPTCHA, Forms adattivo, sfida CAPTCHA, prevenzione dei bot, componenti core, sicurezza dell’invio dei moduli, prevenzione della posta indesiderata dei moduli
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 11%

---

# Utilizzare Google reCAPTCHA in un modulo adattivo AEM basato su componenti core {#using-reCAPTCHA-in-adaptive-forms}

| Applicabile a | Collegamento articolo |
| -------- | ---------------------------- |
| Modulo adattivo basato su componenti core | Questo articolo |
| Modulo adattivo basato su componenti di base | [Fai clic qui](/help/forms/captcha-adaptive-forms.md) |

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [Tornello Cloudflare](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Gli autori di moduli possono utilizzare il servizio reCAPTCHA di Google per implementare reCAPTCHA in Adaptive Forms. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, consulta [Google reCAPTCHA](https://developers.google.com/recaptcha/). [!DNL AEM Forms] as a [!DNL Cloud Service] supporta Google reCAPTCHA v2 in Adaptive Forms. Puoi utilizzarlo per presentare una sfida CAPTCHA all’invio del modulo. Per collegare il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google

1. Ottenere [coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include un **chiave del sito** e un **chiave segreta**.

   ![Crea la configurazione Google reCAPTCHA del sito web Google per ottenere le chiavi reCAPTCHA](/help/forms/assets/google-captcha.gif)
1. Crea un contenitore di configurazione nell’ambiente AEM Forms as a Cloud Service. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un Contenitore di configurazione per collegare il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google:
   1. Apri la tua istanza di AEM Forms as a Cloud Service.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Nel Browser configurazioni, puoi effettuare le seguenti operazioni:
   1. Seleziona una cartella esistente o creane una. Puoi creare una cartella e abilitare per essa l’opzione Configurazioni cloud o Abilitare l’opzione Configurazioni cloud per una cartella esistente:

      * Per creare una cartella e abilitare l’opzione Configurazioni cloud:
         1. Nel browser configurazioni, fai clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica nome, titolo e seleziona il **[!UICONTROL Configurazioni cloud]** opzione.
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare l’opzione Configurazioni cloud per una cartella esistente:
         1. Nel browser configurazioni, seleziona la cartella e fai clic su **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il Cloud Service:
   1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e seleziona **[!UICONTROL reCAPTCHA]**.
   1. Seleziona un Contenitore di configurazione, creato o aggiornato nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
   1. Specifica **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]**, e **[!UICONTROL Chiave segreta]** per il servizio reCAPTCHA (ottenuto nel passaggio 1). Seleziona **[!UICONTROL Crea]**.

   ![Configurare il Cloud Service per collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](/help/forms/assets/captcha-configuration.gif)

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo in un modulo adattivo. Per ulteriori informazioni, consulta [utilizzo di Google reCAPTCHA in un modulo adattivo](#using-reCAPTCHA).

## Utilizzare reCAPTCHA di Google in un modulo adattivo {#using-reCAPTCHA}

Per utilizzare reCAPTCHA in Adaptive Forms:

1. Apri la tua istanza di AEM Forms as a Cloud Service.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un Forms adattivo e seleziona **[!UICONTROL Proprietà]**. Per **[!UICONTROL Contenitore configurazione]** , seleziona il Contenitore di configurazione contenente la configurazione cloud che connette AEM Forms al servizio reCAPTCHA di Google e fai clic su **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un contenitore di configurazione di questo tipo, consulta la sezione [Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google) per scoprire come creare un Contenitore di configurazione di questo tipo.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un Forms adattivo e seleziona **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser Componenti, trascina **[!UICONTROL Modulo adattivo reCAPTCHA]** nel modulo adattivo.

   La convalida di Google reCAPTCHA è sensibile al tempo e scade tra circa un paio di minuti. Pertanto, l’Adobe consiglia di inserire **[!UICONTROL Modulo adattivo reCAPTCHA]** componente immediatamente prima del **[!UICONTROL Invia]** pulsante.

1. Seleziona la **[!UICONTROL Modulo adattivo reCAPTCHA]** e selezionare le proprietà ![Icona Proprietà](assets/configure-icon.svg) icona. Apre la finestra di dialogo delle proprietà. Specifica le seguenti proprietà obbligatorie:
   * **[!UICONTROL Nome]:** Puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell’editor di regole, ma il nome non deve contenere spazi o caratteri speciali.
   * **[!UICONTROL Configurazione CAPTCHA]:** Seleziona una configurazione cloud configurata per visualizzare la finestra di dialogo Google reCAPTCHA per il modulo. Puoi avere più configurazioni cloud nell’ambiente per scopi simili. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google) per scoprire come creare un Cloud Service che colleghi il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google.
   * **Dimensione Captcha:** Puoi selezionare la dimensione di visualizzazione della finestra di dialogo di sfida Google reCAPTCHA. Utilizza il **[!UICONTROL Compatto]** per visualizzare una dimensione ridotta e il **[!UICONTROL Normale]** per visualizzare una finestra di dialogo di sfida Google reCAPTCHA di dimensioni relativamente grandi.

1. Seleziona **[!UICONTROL Fine]**.

   Ora, il **protetto da reCAPTCHA** nel modulo adattivo. Viene visualizzato su tutti i Forms adattivi configurati per utilizzare il servizio Google reCAPTCHA.

   Ora, solo i moduli legittimi, in cui la compilazione del modulo risolve con successo la sfida posta dal servizio Google reCAPTCHA, sono consentiti per l’invio.
   ![Google protetto da badge reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Domande frequenti

**D: Posso utilizzare più di un componente Captcha in un modulo adattivo?**
**Ans:** L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}