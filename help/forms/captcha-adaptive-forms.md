---
title: Utilizzo di reCAPTCHA in Adaptive Forms
description: Scopri come configurare il servizio Google reCAPTCHA in Adaptive Forms.
topic-tags: adaptive_forms, author
source-git-commit: a1689c61715f01cb4eb62882dbcd6e202b74ffc9
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 1%

---

# Utilizzare reCAPTCHA in Adaptive Forms{#using-reCAPTCHA-in-adaptive-forms}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service | Questo articolo |

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o scopi dannosi.

[!DNL AEM Forms] supporta reCAPTCHA in Adaptive Forms. Puoi utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA.

>[!NOTE]
>
>* [!DNL AEM Forms] supporta reCaptcha v2 e reCaptcha Enterprise. Qualsiasi altra versione non è supportata.
>* reCAPTCHA in Adaptive Forms non è supportato in modalità offline su [!DNL AEM Forms] app.
>

## Configurare il servizio reCAPTCHA con Google {#google-reCAPTCHA}

Gli autori di moduli possono utilizzare il servizio reCAPTCHA di Google per implementare reCAPTCHA in Adaptive Forms. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, consulta [Google reCAPTCHA](https://developers.google.com/recaptcha/). Il servizio reCAPTCHA include [!DNL reCAPTCHA v2] e [!DNL reCAPTCHA Enterprise] che puoi integrare in [!DNL AEM Forms]. In base alle tue esigenze puoi configurare il servizio reCAPTCHA per abilitare:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [reCAPTCHA Enterprise in AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 in AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Configurare reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Crea o seleziona un elemento [Progetto Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) e abilita [API di reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Ottenere il [ID Progetto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) e creare un [Chiave API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e un [chiave del sito per i siti web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona una cartella o creane una e abilitala per le configurazioni cloud, come descritto di seguito:
      1. Nel Browser configurazioni, seleziona la cartella e tocca **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il servizio cloud per [!DNL reCAPTCHA Enterprise].

   1. Nell’istanza Autore dell’Experience Manager, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato e tocca **[!UICONTROL Crea]**.
   1. Seleziona versione come [!DNL reCAPTCHA Enterprise] e specifica Nome, ID progetto, Chiave sito e Chiave API (ottenuta nel passaggio 2) per il servizio reCAPTCHA Enterprise.
   1. Seleziona il tipo di chiave; il tipo di chiave deve essere uguale alla chiave del sito configurata in [Progetto Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)ad esempio: **Casella di selezione chiave sito** o **Chiave del sito basata su punteggio**.
   1. Specifica un [punteggio di soglia nell’intervallo da 0 a 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). I punteggi superiori o uguali ai punteggi di soglia identificano l’interazione umana, altrimenti considerata interazione da bot.
   1. Tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Tap **[!UICONTROL Save Settings]** and then tap **[!UICONTROL OK]** to complete the configuration.
-->

Una volta abilitato, il servizio reCAPTCHA Enterprise è disponibile per l’utilizzo in moduli adattivi. Consulta [utilizzo del CAPTCHA nei moduli adattivi](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### Configurare Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Ottenere [coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include un **chiave del sito** e un **chiave segreta**.
1. Crea un contenitore di configurazione per i servizi cloud.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona una cartella o creane una e abilitala per le configurazioni cloud, come descritto di seguito:
      1. Nel Browser configurazioni, seleziona la cartella e tocca **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Tocca **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configura il servizio cloud per reCAPTCHA v2.

   1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Tocca **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato e tocca **[!UICONTROL Crea]**.
   1. Seleziona versione come [!DNL reCAPTCHA v2] , specifica Nome, Chiave sito e Chiave segreta per il servizio reCAPTCHA (ottenuti nel passaggio 1) e tocca **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente, specifica il sito e le chiavi segrete ottenuti nel passaggio 1. Tocca **[!UICONTROL Salva impostazioni]** e quindi tocca **OK** per completare la configurazione.

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo nei moduli adattivi. Per ulteriori informazioni, consulta [utilizzo del CAPTCHA nei moduli adattivi](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Utilizzare reCAPTCHA nei moduli adattivi {#using-reCAPTCHA}

Per utilizzare reCAPTCHA nei moduli adattivi:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. Puoi anche modificare le proprietà dei moduli adattivi per cambiare il contenitore di configurazione associato al modulo.

1. Dal browser Componenti, trascina **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >* L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.
   >* reCaptcha è sensibile al tempo e scade tra circa un paio di minuti. Pertanto, si consiglia di inserire il componente Captcha subito prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e tocca ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specificate un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Seleziona **Nascondi titolo** se non desideri che il titolo venga visualizzato.
1. Dalla sezione **Servizio Captcha** a discesa, seleziona **reCAPTCHA** per abilitare il servizio reCAPTCHA se è stato configurato come descritto in [Servizio reCAPTCHA di Google](#google-reCAPTCHA).
1. Seleziona una configurazione dal menu a discesa Impostazioni per **reCAPTCHA Enterprise** o **reCAPTCHA v2**
   1. Se si seleziona **reCAPTCHA Enterprise** versione, il tipo di chiave può essere di **casella di controllo** o **basato su punteggio**, si basa sulla selezione effettuata al momento della configurazione [chiave del sito per i siti web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* Nella configurazione cloud con **tipo di chiave** as **casella di controllo**, se la convalida captcha non riesce, il messaggio di errore personalizzato viene visualizzato come messaggio in linea.
   >* Nella configurazione cloud con **tipo di chiave** as **basato su punteggio**, il messaggio di errore personalizzato viene visualizzato come messaggio a comparsa se la convalida captcha non riesce.

   1. È possibile selezionare le dimensioni come **[!UICONTROL Normale]** e **[!UICONTROL Compatto]**.
   1. È possibile selezionare una **[!UICONTROL Riferimento binding]**, In **[!UICONTROL Riferimento binding]** i dati inviati sono dati associati, altrimenti si tratta di dati non associati. Di seguito sono riportati alcuni esempi XML di dati non associati e dati associati (con riferimento di associazione come SSN) rispettivamente, quando un modulo viene inviato.

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
   1. Puoi selezionare la dimensione come **[!UICONTROL Normale]** o **[!UICONTROL Compatto]** per il widget reCAPTCHA.
   1. È possibile selezionare **[!UICONTROL Invisibile]** per mostrare la richiesta CAPTCHA solo nel caso di attività sospetta.

   Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere il CAPTCHA che funziona. Il **protetto da reCAPTCHA** nei moduli protetti viene visualizzato il contrassegno riportato di seguito.
   ![Google protetto da badge reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

1. Salva le proprietà.

>[!NOTE]
> 
> Non selezionare **[!UICONTROL Predefinito]** dall’elenco a discesa del servizio Captcha poiché il servizio AEM CAPTCHA predefinito è obsoleto.

>[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

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

**Opzione 2: utilizzo [!DNL Experience Manager Forms] API ValidateCAPTCHA per convalidare CAPTCHA su un’azione dell’utente prima di inviare il modulo**

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
