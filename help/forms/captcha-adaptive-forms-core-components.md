---
title: Utilizzare Google reCAPTCHA in un modulo adattivo basato su componenti core
description: Migliora la sicurezza dei moduli con il servizio Google reCAPTCHA. Guida passo passo all'interno!
topic-tags: Adaptive Forms, author
hide: true
hidefromtoc: true
Keywords: Google reCAPTCHA service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
source-git-commit: a1689c61715f01cb4eb62882dbcd6e202b74ffc9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Utilizzare reCAPTCHA in Forms adattivo basato su componenti core {#using-reCAPTCHA-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o scopi dannosi.

[!DNL AEM Forms] as a [!DNL Cloud Service] supporta Google reCAPTCHA v2 in Adaptive Forms. Puoi utilizzarlo per presentare una sfida CAPTCHA all’invio del modulo. Per utilizzare reCAPTCHA in un modulo adattivo:

1. [Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [Configura il modulo adattivo per visualizzare la sfida CAPTCHA all’invio del modulo](#using-reCAPTCHA)

## Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Per collegare il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google

1. Ottenere [coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include un **chiave del sito** e un **chiave segreta**.

   ![Crea la configurazione Google reCAPTCHA del sito web Google per ottenere le chiavi reCAPTCHA](/help/forms/assets/google-captcha.gif){width="50%"}
1. Crea un contenitore di configurazione nell’ambiente as a Cloud Service AEM Forms. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un Contenitore di configurazione per collegare il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google:
   1. Apri l’istanza as a Cloud Service di AEM Forms.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Nel Browser configurazioni, puoi effettuare le seguenti operazioni:
   1. Seleziona una cartella esistente o creane una. Puoi creare una cartella e abilitare per essa l’opzione Configurazioni cloud o Abilitare l’opzione Configurazioni cloud per una cartella esistente:

      * Per creare una cartella e abilitare l’opzione Configurazioni cloud:
         1. Nel browser configurazioni, fai clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica nome, titolo e seleziona il **[!UICONTROL Configurazioni cloud]** opzione.
         1. Fai clic su **[!UICONTROL Crea]**
      * Per abilitare l’opzione Configurazioni cloud per una cartella esistente:
         1. Nel Browser configurazioni, seleziona la cartella e tocca **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il Cloud Service:
   1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** e tocca **[!UICONTROL reCAPTCHA]**.
   1. Seleziona un Contenitore di configurazione, creato o aggiornato nella sezione precedente. Tocca **[!UICONTROL Crea]**.
   1. Specifica **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]**, e **[!UICONTROL Chiave segreta]** per il servizio reCAPTCHA (ottenuto nel passaggio 1). Tocca **[!UICONTROL Crea]**.


   ![Configurare il Cloud Service per collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](/help/forms/assets/captcha-configuration.gif)



   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo in un modulo adattivo. Per ulteriori informazioni, consulta [utilizzo di Google reCAPTCHA in un modulo adattivo](#using-reCAPTCHA).


## Utilizzare Google reCAPTCHA in un modulo adattivo {#using-reCAPTCHA}

Per utilizzare reCAPTCHA in Adaptive Forms:

1. Apri l’istanza as a Cloud Service di AEM Forms.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un Forms adattivo e tocca **[!UICONTROL Proprietà]**. Per **[!UICONTROL Contenitore configurazione]** , seleziona il Contenitore di configurazione contenente la Configurazione cloud che collega AEM Forms al servizio reCAPTCHA tramite Google e tocca **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un contenitore di configurazione di questo tipo, consulta la sezione [Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google) per scoprire come creare un Contenitore di configurazione di questo tipo.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un Forms adattivo e tocca **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser Componenti, trascina **[!UICONTROL Modulo adattivo reCAPTCHA]** nel modulo adattivo.

   La convalida di Google reCAPTCHA è sensibile al tempo e scade tra circa un paio di minuti. Pertanto, l’Adobe consiglia di inserire **[!UICONTROL Modulo adattivo reCAPTCHA]** componente immediatamente prima del **[!UICONTROL Invia]** pulsante.

1. Seleziona la **[!UICONTROL Modulo adattivo reCAPTCHA]** e toccare le proprietà ![Icona Proprietà](assets/configure-icon.svg) icona. Apre la finestra di dialogo delle proprietà. Specifica le seguenti proprietà obbligatorie:
   * **[!UICONTROL Nome]:** Puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell’editor di regole, ma il nome non deve contenere spazi o caratteri speciali.
   * **[!UICONTROL Configurazione CAPTCHA]:** Seleziona una configurazione cloud configurata per visualizzare la finestra di dialogo Google reCAPTCHA per il modulo. Puoi avere più configurazioni cloud nell’ambiente per scopi simili. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Collegare l’ambiente AEM Forms con il servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google) per scoprire come creare un Cloud Service che colleghi il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google.
   * **Dimensione Captcha:** Puoi selezionare la dimensione di visualizzazione della finestra di dialogo di sfida Google reCAPTCHA. Utilizza il **[!UICONTROL Compatto]** per visualizzare una dimensione ridotta e il **[!UICONTROL Normale]** per visualizzare una finestra di dialogo di sfida Google reCAPTCHA di dimensioni relativamente grandi.

1. Tocca **[!UICONTROL Fine]**.

   Ora, il **protetto da reCAPTCHA** nel modulo adattivo. Viene visualizzato su tutti i Forms adattivi configurati per utilizzare il servizio Google reCAPTCHA.

   Ora, solo i moduli legittimi, in cui la compilazione del modulo risolve con successo la sfida posta dal servizio Google reCAPTCHA, sono consentiti per l’invio.
   ![Google protetto da badge reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Domande frequenti

**D: Posso utilizzare più di un componente Captcha in un modulo adattivo?**
**Ans:** L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

