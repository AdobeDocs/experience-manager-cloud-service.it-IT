---
title: Come si utilizza CAPTCHA in Adaptive Forms?
description: Scopri come configurare o Google il servizio reCAPTCHA per un modulo adattivo.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 5%

---

# Utilizzare reCAPTCHA in Adaptive Forms {#using-reCAPTCHA-in-adaptive-forms}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |
| Applicabile a | Modulo adattivo basato su componenti di base. <br> Per il modulo adattivo basato su componenti core, [Fai clic qui](/help/forms/captcha-adaptive-forms-core-components.md). |


Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:

* [Google reCAPTCHA](#configure-recaptcha-service-by-google)
* [Tornello Cloudflare](/help/forms/integrate-adaptive-forms-turnstile.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## Configurare il servizio reCAPTCHA con Google {#google-reCAPTCHA}

Gli autori di moduli possono utilizzare il servizio reCAPTCHA di Google per implementare reCAPTCHA in Adaptive Forms. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, vedere [Google reCAPTCHA](https://developers.google.com/recaptcha/). AEM Forms supporta [!DNL reCAPTCHA v2] e [!DNL reCAPTCHA Enterprise]. Qualsiasi altra versione non è supportata. Inoltre, reCAPTCHA in Adaptive Forms non è supportato in modalità offline nell&#39;app [!DNL AEM Forms]. In base alle tue esigenze puoi configurare il servizio reCAPTCHA per abilitare:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [reCAPTCHA Enterprise in AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 in AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Configurare reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Crea o seleziona un [progetto Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) e abilita [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Ottieni l&#39;[ID progetto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) e crea una [chiave API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e una [chiave sito per siti Web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona una cartella o creane una e abilitala per le configurazioni cloud, come descritto di seguito:
      1. Nel Browser configurazioni, selezionare la cartella e selezionare **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il servizio cloud per [!DNL reCAPTCHA Enterprise].

   1. Nell&#39;istanza Autore Experience Manager, vai a ![strumenti-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**.
   1. Selezionare **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Selezionare il contenitore di configurazione creato e selezionare **[!UICONTROL Crea]**.
   1. Seleziona la versione come [!DNL reCAPTCHA Enterprise] e specifica Nome, ID progetto, Chiave sito e Chiave API (ottenuta nel passaggio 2) per il servizio Enterprise reCAPTCHA.
   1. Selezionare il tipo di chiave. Il tipo di chiave deve essere uguale alla chiave del sito configurata nel [progetto Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin), ad esempio **Chiave del sito di checkbox** o **Chiave del sito basata su punteggio**.
   1. Specifica un punteggio di soglia [&#x200B; compreso tra 0 e 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). I punteggi superiori o uguali ai punteggi di soglia identificano l’interazione umana, altrimenti considerata interazione da bot.
   1. Seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

Una volta abilitato, il servizio reCAPTCHA Enterprise è disponibile per l’utilizzo in moduli adattivi. Vedi [utilizzo del CAPTCHA nei moduli adattivi](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### Configurare Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Ottieni la coppia di chiavi API [reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include una **chiave del sito** e una **chiave segreta**.
1. Crea un contenitore di configurazione per i servizi cloud.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona una cartella o creane una e abilitala per le configurazioni cloud, come descritto di seguito:
      1. Nel Browser configurazioni, selezionare la cartella e selezionare **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configura il servizio cloud per reCAPTCHA v2.

   1. Nell&#39;istanza dell&#39;autore AEM, vai a ![strumenti-1](assets/tools-1.png) > **Cloud Service**.
   1. Selezionare **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Selezionare il contenitore di configurazione creato e selezionare **[!UICONTROL Crea]**.
   1. Seleziona la versione come [!DNL reCAPTCHA v2] , specifica il nome, la chiave del sito e la chiave segreta per il servizio reCAPTCHA (ottenuto nel passaggio 1), quindi seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente, specifica il sito e le chiavi segrete ottenuti nel passaggio 1. Seleziona **[!UICONTROL Salva impostazioni]**, quindi seleziona **OK** per completare la configurazione.

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo nei moduli adattivi. Per ulteriori informazioni, vedi [utilizzo del CAPTCHA nei moduli adattivi](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Utilizzare Google reCAPTCHA nei moduli adattivi {#using-reCAPTCHA}

Per utilizzare Google reCAPTCHA in un modulo adattivo:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. Puoi anche modificare le proprietà dei moduli adattivi per cambiare il contenitore di configurazione associato al modulo.

1. Dal browser componenti, trascina il componente **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >* L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.
   >* reCaptcha è sensibile al tempo e scade tra circa un paio di minuti. Pertanto, si consiglia di inserire il componente Captcha subito prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e seleziona ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specificate un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Selezionare **Nascondi titolo** se non si desidera visualizzare il titolo.
1. Dall&#39;elenco a discesa del servizio **Captcha**, selezionare **reCAPTCHA** per abilitare il servizio reCAPTCHA se è stato configurato come descritto nel servizio [reCAPTCHA da Google](#google-reCAPTCHA).
1. Seleziona una configurazione dal menu a discesa Impostazioni per **reCAPTCHA Enterprise** o **reCAPTCHA v2**
   1. Se si seleziona la versione **reCAPTCHA Enterprise**, il tipo di chiave può essere di **casella di controllo** o **punteggio basato**, si basa sulla selezione quando si configura [chiave sito per siti Web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* Nella configurazione cloud con **tipo chiave** come **casella di controllo**, il messaggio di errore personalizzato viene visualizzato come messaggio in linea se la convalida captcha non riesce.
   >* Nella configurazione cloud con **tipo chiave** come **punteggio basato**, il messaggio di errore personalizzato viene visualizzato come messaggio popup se la convalida captcha non riesce.

   1. È possibile selezionare le dimensioni come **[!UICONTROL Normale]** e **[!UICONTROL Compatta]**.
   1. È possibile selezionare un **[!UICONTROL Riferimento associazione]**. In **[!UICONTROL Riferimento associazione]** i dati inviati sono dati associati, altrimenti si tratta di dati non associati. Di seguito sono riportati alcuni esempi XML di dati non associati e dati associati (con riferimento di associazione come SSN) rispettivamente, quando un modulo viene inviato.

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data>
                   <captcha16820607953761>
                       <captchaType>reCaptchaEnterprise</captchaType>
                       <captchaScore>0.9</captchaScore>
                   </captcha16820607953761>
               </data>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>371237912</SSN>
                       <FirstName>Sarah </FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608034928</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data/>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>
                           <captchaType>reCaptchaEnterprise</captchaType>
                           <captchaScore>0.9</captchaScore>
                       </SSN>
                       <FirstName>Sarah</FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608035111</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   Se si seleziona **reCAPTCHA v2** versione:
   1. È possibile selezionare la dimensione come **[!UICONTROL Normal]** o **[!UICONTROL Compact]** per il widget reCAPTCHA.
   1. È possibile selezionare l&#39;opzione **[!UICONTROL Invisibile]** per visualizzare la richiesta CAPTCHA solo nel caso di attività sospetta.

   Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere il CAPTCHA che funziona. Il badge **protetto da reCAPTCHA**, visualizzato di seguito, viene visualizzato nei moduli protetti.
   ![Google protetto da badge reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

1. Salva le proprietà.

>[!NOTE]
> 
> Non selezionare **[!UICONTROL Default]** dal menu a discesa del servizio Captcha poiché il servizio AEM CAPTCHA predefinito è obsoleto.

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### Mostrare o nascondere il componente CAPTCHA in base alle regole {#show-hide-captcha}

Puoi scegliere di mostrare o nascondere il componente CAPTCHA in base alle regole applicate a un componente in un modulo adattivo. Selezionare il componente, selezionare ![modifica regole](assets/edit-rules-icon.svg) e selezionare **[!UICONTROL Crea]** per creare una regola. Per ulteriori informazioni sulla creazione di regole, vedere [Editor regole](rule-editor.md).

Ad esempio, il componente CAPTCHA deve essere visualizzato in un modulo adattivo solo se il campo Valore valuta nel modulo ha un valore superiore a 25000.

Selezionare il campo **[!UICONTROL Valore valuta]** nel modulo e creare le regole seguenti:

![Mostra o nascondi regole](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Quando selezioni una configurazione reCAPTCHA v2 e la dimensione è impostata su [!UICONTROL Invisibile], l&#39;opzione mostra/nascondi rimane disabilitata.

### Convalida CAPTCHA {#validate-captcha}

È possibile convalidare il CAPTCHA in un modulo adattivo quando si invia il modulo oppure basare la convalida CAPTCHA sulle azioni e condizioni dell’utente.

#### Convalida CAPTCHA all’invio del modulo {#validation-form-submission}

Per convalidare automaticamente un CAPTCHA quando si invia un modulo adattivo:

1. Selezionare il componente CAPTCHA e selezionare ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. Nella sezione **[!UICONTROL Convalida CAPTCHA]**, seleziona **[!UICONTROL Convalida CAPTCHA all&#39;invio del modulo]**.
1. Seleziona ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

#### Convalida CAPTCHA per azioni e condizioni dell’utente {#validate-captcha-user-action}

Per convalidare un CAPTCHA in base a condizioni e azioni dell’utente:

1. Selezionare il componente CAPTCHA e selezionare ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. Nella sezione **[!UICONTROL Convalida CAPTCHA]**, selezionare **[!UICONTROL Convalida CAPTCHA per un&#39;azione utente]**.
1. Seleziona ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

[!DNL Experience Manager Forms] fornisce l&#39;API `ValidateCAPTCHA` per convalidare CAPTCHA utilizzando condizioni predefinite. Puoi richiamare l’API utilizzando un’azione di invio personalizzata o definendo regole sui componenti in un modulo adattivo.

Di seguito è riportato un esempio di API `ValidateCAPTCHA` per convalidare CAPTCHA utilizzando condizioni predefinite:

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

L&#39;esempio indica che l&#39;API `ValidateCAPTCHA` convalida il CAPTCHA nel modulo solo se il numero di cifre nella casella numerica specificata dall&#39;utente durante la compilazione del modulo è maggiore di 5.

**Opzione 1: utilizzare l&#39;API ValidateCAPTCHA [!DNL Experience Manager Forms] per convalidare CAPTCHA tramite un&#39;azione di invio personalizzata**

Per utilizzare l&#39;API `ValidateCAPTCHA` per convalidare il CAPTCHA tramite un&#39;azione di invio personalizzata, eseguire la procedura seguente:

1. Aggiungere lo script che include l&#39;API `ValidateCAPTCHA` all&#39;azione di invio personalizzata. Per ulteriori informazioni sulle azioni di invio personalizzate, vedere [Creare un&#39;azione di invio personalizzata per Forms adattivo](custom-submit-action-form.md).
1. Seleziona il nome dell&#39;azione di invio personalizzata dall&#39;elenco a discesa **[!UICONTROL Azione di invio]** nelle proprietà **[!UICONTROL Invio]** di un modulo adattivo.
1. Seleziona **[!UICONTROL Invia]**. Il CAPTCHA viene convalidato in base alle condizioni definite nell&#39;API `ValidateCAPTCHA` dell&#39;azione di invio personalizzata.

**Opzione 2: utilizzare l&#39;API ValidateCAPTCHA [!DNL Experience Manager Forms] per convalidare CAPTCHA in un&#39;azione utente prima di inviare il modulo**

È inoltre possibile richiamare l&#39;API `ValidateCAPTCHA` applicando regole a un componente in un modulo adattivo.

Ad esempio, puoi aggiungere un pulsante **[!UICONTROL Convalida CAPTCHA]** in un modulo adattivo e creare una regola per richiamare un servizio facendo clic su un pulsante.

Nella figura seguente viene illustrato come richiamare un servizio facendo clic su un pulsante **[!UICONTROL Convalida CAPTCHA]**:

![Convalida CAPTCHA](assets/captcha-validation1.gif)

È possibile richiamare il servlet personalizzato che include l&#39;API `ValidateCAPTCHA` utilizzando l&#39;editor di regole e abilitare o disabilitare il pulsante di invio del modulo adattivo in base al risultato della convalida.

Allo stesso modo, puoi utilizzare l’editor di regole per includere un metodo personalizzato per convalidare il CAPTCHA in un modulo adattivo.

<!--

### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

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

`captchaPropertyNodePath` refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` refers to the `g_recaptcha_response` that gets generated after solving a CAPTCHA in a form. -->

### Modifica dominio del servizio reCAPTCHA {#reCAPTCHA-service-domain}

Il servizio reCAPTCHA utilizza `https://www.recaptcha.net/` come dominio predefinito. È possibile modificare le impostazioni per impostare `https://www.google.com/` o qualsiasi nome di dominio personalizzato per il caricamento, il rendering e la convalida del servizio reCAPTCHA.

Impostare la proprietà **[!UICONTROL af.cloudservices.recaptcha.domain]** della configurazione **[!UICONTROL Modulo adattivo e canale web di comunicazione interattiva]** per specificare `https://www.google.com/` o qualsiasi altro nome di dominio personalizzato. Il seguente file JSON mostra un esempio:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

Per impostare i valori di una configurazione, [Genera configurazioni OSGi utilizzando il SDK dell&#39;AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=it#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [distribuisci la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it#deployment-process) nell&#39;istanza del Cloud Service.

## Consulta anche {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Reference Themes, Templates, and Form Data models for Adaptive Forms](/help/forms/reference-themes-templates-data-models.md)

-->
