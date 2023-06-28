---
title: Utilizzo del CAPTCHA in Adaptive Forms
seo-title: Using CAPTCHA in Adaptive Forms
description: Scopri come configurare il servizio AEM CAPTCHA o Google reCAPTCHA in Adaptive Forms.
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in Adaptive Forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 63f6e7c6df7404062aa0d209496506bdabcf564c
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---

# Utilizzare il CAPTCHA in Adaptive Forms{#using-captcha-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o scopi dannosi.

[!DNL AEM Forms] supporta il CAPTCHA in Adaptive Forms. Puoi utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA.

>[!NOTE]
>
>* [!DNL AEM Forms] supporta solo reCaptcha v2. Qualsiasi altra versione non è supportata.
>* Il CAPTCHA in Forms adattivo non è supportato in modalità offline su [!DNL AEM Forms] app.
>

## Configurare il servizio reCAPTCHA con Google {#google-reCAPTCHA}

Gli autori di moduli possono utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA in Adaptive Forms. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, consulta [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![reCAPTCHA](assets/recaptcha_new.png)

Per implementare il servizio reCAPTCHA in [!DNL AEM Forms]:

1. Ottenere [coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include una chiave del sito e un segreto.
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
      * Consulta la [Browser configurazioni](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#introduction) per ulteriori informazioni.
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

      1. Nel browser configurazioni, seleziona la **[!UICONTROL globale]** cartella e tocca **[!UICONTROL Proprietà]**.

      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   1. Nel browser configurazioni, tocca **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Tocca **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

1. Configura il servizio cloud per reCAPTCHA.

   1. Nell’istanza Autore dell’Experience Manager, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato nel passaggio precedente e tocca **[!UICONTROL Crea]**.
   1. Specifica nome, chiave del sito e chiave segreta per il servizio reCAPTCHA e tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente, specifica il sito e le chiavi segrete ottenuti nel passaggio 1. Tocca **[!UICONTROL Salva impostazioni]** e quindi tocca **[!UICONTROL OK]** per completare la configurazione.

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo in Adaptive Forms. Per ulteriori informazioni, consulta [Utilizzo del CAPTCHA in Adaptive Forms](#using-captcha).

## Utilizzare il CAPTCHA in Adaptive Forms {#using-captcha}

Per utilizzare il CAPTCHA in Adaptive Forms:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   > Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. Puoi anche modificare le proprietà del modulo adattivo per cambiare il contenitore di configurazione associato al modulo.

1. Dal browser Componenti, trascina **[!UICONTROL Captcha]** nel modulo adattivo.

   >[!NOTE]
   >
   > * L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.
   > * Il Captcha è sensibile al tempo e scade tra circa un minuto. Pertanto, si consiglia di inserire il componente Captcha subito prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e tocca ![cmppr](assets/configure-icon.svg) per modificarne le proprietà.
1. Specificate un titolo per il widget CAPTCHA. Il valore predefinito è **[!UICONTROL Captcha]**. Seleziona **[!UICONTROL Nascondi titolo]** se non desideri che il titolo venga visualizzato.
1. Dalla sezione **[!UICONTROL Servizio Captcha]** a discesa, seleziona **[!UICONTROL reCAPTCHA]** per abilitare il servizio reCAPTCHA se è stato configurato come descritto in [Servizio reCAPTCHA di Google](#google-reCAPTCHA). Seleziona una configurazione dal menu a discesa Impostazioni.
1. Seleziona il tipo come **[!UICONTROL Normale]** o **[!UICONTROL Compatto]** per il widget reCAPTCHA. È inoltre possibile selezionare **[!UICONTROL Invisibile]** per mostrare la richiesta CAPTCHA solo nel caso di attività sospetta. Il badge protetto da reCAPTCHA, visualizzato di seguito, viene visualizzato nei moduli protetti.

   ![Google protetto da badge reCAPTCHA](assets/google-recaptcha-v2.png)

   >[!NOTE]
   >
   > Non selezionare **[!UICONTROL Predefinito]** dall’elenco a discesa del servizio Captcha come servizio CAPTCHA di Experience Manager predefinito è obsoleto.

1. Salva le proprietà.

Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere il CAPTCHA che funziona.

### Mostrare o nascondere il componente CAPTCHA in base alle regole {#show-hide-captcha}

Puoi scegliere di mostrare o nascondere il componente CAPTCHA in base alle regole applicate a un componente in un modulo adattivo. Tocca il componente, seleziona ![modifica regole](assets/edit-rules-icon.svg), e tocca **[!UICONTROL Crea]** per creare una regola. Per ulteriori informazioni sulla creazione delle regole, consulta [Editor regole](rule-editor.md).

Ad esempio, il componente CAPTCHA deve essere visualizzato in un modulo adattivo solo se il campo Valore valuta nel modulo ha un valore superiore a 25000.

Tocca il **[!UICONTROL Valore valuta]** nel modulo e creare le regole seguenti:

![Mostra o nascondi regole](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Quando selezioni una configurazione reCAPTCHA v2 e la dimensione è impostata su [!UICONTROL Invisibile], l&#39;opzione mostra/nascondi rimane disattivata.

### Convalida CAPTCHA {#validate-captcha}

È possibile convalidare il CAPTCHA in un modulo adattivo quando si invia il modulo oppure basare la convalida CAPTCHA sulle azioni e condizioni dell’utente.

#### Convalida CAPTCHA all’invio del modulo {#validation-form-submission}

Per convalidare automaticamente un CAPTCHA quando si invia un modulo adattivo:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. In **[!UICONTROL Convalida CAPTCHA]** sezione, seleziona **[!UICONTROL Convalida CAPTCHA all’invio del modulo]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

#### Convalida CAPTCHA per azioni e condizioni dell’utente {#validate-captcha-user-action}

Per convalidare un CAPTCHA in base a condizioni e azioni dell’utente:

1. Tocca il componente CAPTCHA e seleziona ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. In **[!UICONTROL Convalida CAPTCHA]** sezione, seleziona **[!UICONTROL Convalida CAPTCHA per azione dell’utente]**.
1. Tocca ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

[!DNL Experience Manager Forms] fornisce `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando condizioni predefinite. Puoi richiamare l’API utilizzando un’azione di invio personalizzata o definendo regole sui componenti in un modulo adattivo.

Di seguito è riportato un esempio di `ValidateCAPTCHA` API per convalidare CAPTCHA utilizzando condizioni predefinite:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

L&#39;esempio indica che `ValidateCAPTCHA` L’API convalida il CAPTCHA nel modulo solo se il numero di cifre nella casella numerica specificata dall’utente durante la compilazione del modulo è maggiore di 5.

**Opzione 1: utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare CAPTCHA tramite un’azione di invio personalizzata**

Per utilizzare il `ValidateCAPTCHA` API per convalidare CAPTCHA tramite un’azione di invio personalizzata:

1. Aggiungi lo script che include `ValidateCAPTCHA` API per personalizzare l’azione di invio. Per ulteriori informazioni sulle azioni di invio personalizzate, consulta [Creare un’azione di invio personalizzata per Adaptive Forms](custom-submit-action-form.md).
1. Selezionare il nome dell&#39;azione di invio personalizzata dalla **[!UICONTROL Azione di invio]** elenco a discesa in **[!UICONTROL Invio]** proprietà di un modulo adattivo.
1. Tocca **[!UICONTROL Invia]**. Il CAPTCHA viene convalidato in base alle condizioni definite in `ValidateCAPTCHA` API dell’azione di invio personalizzata.

**Opzione 2: utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare CAPTCHA su un’azione utente prima di inviare il modulo**

Puoi anche richiamare `ValidateCAPTCHA` tramite l’applicazione di regole su un componente in un modulo adattivo.

Ad esempio, puoi aggiungere un’ **[!UICONTROL Convalida CAPTCHA]** in un modulo adattivo e crea una regola per richiamare un servizio facendo clic su un pulsante.

Nella figura seguente viene illustrato come richiamare un servizio facendo clic su un **[!UICONTROL Convalida CAPTCHA]** pulsante:

![Convalida CAPTCHA](assets/captcha-validation1.gif)

Puoi richiamare il servlet personalizzato che include `ValidateCAPTCHA` tramite l’editor di regole e abilita o disabilita il pulsante di invio del modulo adattivo in base al risultato della convalida.

Allo stesso modo, puoi utilizzare l’editor di regole per includere un metodo personalizzato per convalidare il CAPTCHA in un modulo adattivo.

### Aggiungere servizi CAPTCHA personalizzati {#add-custom-captcha-service}

[!DNL Experience Manager Forms] fornisce reCAPTCHA come servizio CAPTCHA. Tuttavia, puoi aggiungere un servizio personalizzato da visualizzare nel **[!UICONTROL Servizio CAPTCHA]** elenco a discesa.

Di seguito è riportato un esempio di implementazione dell’interfaccia per aggiungere un servizio CAPTCHA aggiuntivo al modulo adattivo:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` fa riferimento al percorso della risorsa del componente CAPTCHA nell’archivio Sling. Utilizzare questa proprietà per includere dettagli specifici del componente CAPTCHA. Ad esempio: `captchaPropertyNodePath` include informazioni sulla configurazione cloud reCAPTCHA configurata sul componente CAPTCHA. Le informazioni sulla configurazione cloud forniscono **[!UICONTROL Chiave sito]** e **[!UICONTROL Chiave segreta]** impostazioni per l’implementazione del servizio reCAPTCHA.

`userResponseToken` fa riferimento al `g_recaptcha_response` che viene generato dopo la risoluzione di un CAPTCHA in un modulo.

### Modifica dominio del servizio reCAPTCHA {#reCAPTCHA-service-domain}

Il servizio reCAPTCHA utilizza `https://www.recaptcha.net/` come dominio predefinito. È possibile modificare le impostazioni da impostare `https://www.google.com/` o qualsiasi nome di dominio personalizzato per il caricamento, il rendering e la convalida del servizio reCAPTCHA.

Imposta il **[!UICONTROL af.cloudservices.recaptcha.domain]** proprietà del **[!UICONTROL Configurazione di un modulo adattivo e di un canale web di comunicazione interattiva]** configurazione da specificare `https://www.google.com/` o qualsiasi altro nome di dominio personalizzato. Il seguente file JSON mostra un esempio:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

Per impostare i valori di una configurazione: [Generare configurazioni OSGi utilizzando l’SDK per AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all’istanza di Cloud Service.
