---
title: Come si utilizza Google reCAPTCHA in un modulo adattivo AEM?
description: Migliora la sicurezza dei moduli con il servizio Google reCAPTCHA. Guida dettagliata all’interno!
topic-tags: Adaptive Forms, author
keywords: Servizio Google reCAPTCHA, Forms adattivo, sfida CAPTCHA, prevenzione dei bot, componenti core, sicurezza dell’invio dei moduli, prevenzione della posta indesiderata dei moduli
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 7%

---

# Utilizzare Google reCAPTCHA in un modulo adattivo AEM basato su componenti core {#using-reCAPTCHA-in-adaptive-forms}

| Applicabile a | Collegamento articolo |
| -------- | ---------------------------- |
| Modulo adattivo basato su componenti core | Questo articolo |
| Modulo adattivo basato su componenti di base | [Fai clic qui](/help/forms/captcha-adaptive-forms.md) |

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## Collegare i componenti core di AEM Forms con il servizio reCAPTCHA di Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Gli autori di moduli possono utilizzare il servizio reCAPTCHA di Google per implementare reCAPTCHA in Adaptive Forms. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, vedere [Google reCAPTCHA](https://developers.google.com/recaptcha/). La utilizzi per presentare una sfida CAPTCHA all’invio del modulo.[!DNL AEM Forms] as a [!DNL Cloud Service] supporta Google reCAPTCHA v2 e reCAPTCHA Enterprise. Qualsiasi altra versione non è supportata. Inoltre, reCAPTCHA in Adaptive Forms non è supportato in modalità offline nell’app AEM Forms.

In base alle tue esigenze puoi configurare il servizio reCAPTCHA per abilitare:

* [reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components)
* [reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

### Configurare reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components}

1. Crea o seleziona un [progetto Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) e abilita [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Ottieni l&#39;[ID progetto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) e crea una [chiave API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e una [chiave sito per siti Web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Seleziona una cartella o creane una e abilitala per le configurazioni cloud, come descritto di seguito:
      1. Nel Browser configurazioni, selezionare la cartella e selezionare **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il servizio cloud per [!DNL reCAPTCHA Enterprise].

   1. Nell&#39;istanza Autore Experience Manager, vai a ![strumenti-1](assets/tools-1.png) > **[!UICONTROL Servizi cloud]**.
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

   ![Crea la configurazione reCAPTCHA di Google del sito Web di Google per ottenere le chiavi reCAPTCHA](/help/forms/assets/google-captcha.gif)
1. Crea un contenitore di configurazione nell’ambiente AEM Forms as a Cloud Service. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per connettere AEM a servizi esterni. Per creare e configurare un Contenitore di configurazione per collegare il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google:
   1. Apri l’istanza di AEM Forms as a Cloud Service.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Nel Browser configurazioni, puoi effettuare le seguenti operazioni:
   1. Seleziona una cartella esistente o creane una. Puoi creare una cartella e abilitare per essa l’opzione Configurazioni cloud o Abilitare l’opzione Configurazioni cloud per una cartella esistente:

      * Per creare una cartella e abilitare l’opzione Configurazioni cloud:
         1. Nel browser configurazioni fare clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica nome, titolo e seleziona l&#39;opzione **[!UICONTROL Configurazioni cloud]**.
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare l’opzione Configurazioni cloud per una cartella esistente:
         1. Nel Browser configurazioni, selezionare la cartella e selezionare **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configura Cloud Service:
   1. Nell&#39;istanza Autore AEM, vai a ![strumenti-1](assets/tools-1.png) > **[!UICONTROL Servizi cloud]** e seleziona **[!UICONTROL reCAPTCHA]**.
   1. Seleziona un Contenitore di configurazione, creato o aggiornato nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
   1. Specifica **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]** e **[!UICONTROL Chiave segreta]** per il servizio reCAPTCHA (ottenuto nel passaggio 1). Seleziona **[!UICONTROL Crea]**.

   ![Configura Cloud Service per connettere il tuo ambiente AEM Forms con il servizio reCAPTCHA di Google](/help/forms/assets/captcha-configuration.gif)

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo in un modulo adattivo. Per ulteriori informazioni, vedere [utilizzo di Google reCAPTCHA in un modulo adattivo](#using-reCAPTCHA).


Utilizzare Google reCAPTCHA nei moduli adattivi

## Utilizzare reCAPTCHA di Google in un modulo adattivo {#using-reCAPTCHA}

Per utilizzare reCAPTCHA in Adaptive Forms:

1. Apri l’istanza di AEM Forms as a Cloud Service.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Selezionare un Forms adattivo e selezionare **[!UICONTROL Proprietà]**. Per l&#39;opzione **[!UICONTROL Contenitore configurazione]**, selezionare il Contenitore configurazione che contiene la configurazione cloud che connette AEM Forms con il servizio reCAPTCHA di Google, quindi selezionare **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un contenitore di configurazione di questo tipo, consulta la sezione [Connettere l&#39;ambiente AEM Forms al servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google) per scoprire come creare un contenitore di configurazione di questo tipo.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un Forms adattivo e seleziona **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser componenti, trascina il componente **[!UICONTROL Modulo adattivo reCAPTCHA]** nel Modulo adattivo.

   >[!NOTE]
   > * La convalida di Google reCAPTCHA è sensibile al tempo e scade tra circa un paio di minuti. Adobe consiglia pertanto di inserire il componente **[!UICONTROL reCAPTCHA]** del modulo adattivo immediatamente prima del pulsante **[!UICONTROL Invia]**.

1. Seleziona il componente **[!UICONTROL reCAPTCHA]** del modulo adattivo e l&#39;icona ![Proprietà](assets/configure-icon.svg). Apre la finestra di dialogo delle proprietà. Specifica le seguenti proprietà obbligatorie:
   * **[!UICONTROL Nome]:** È possibile identificare facilmente un componente modulo con il relativo nome univoco sia nel modulo che nell&#39;editor di regole, ma il nome non deve contenere spazi o caratteri speciali.
   * **[!UICONTROL Titolo]:** Specificare un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Selezionare **Nascondi titolo** se non si desidera visualizzare il titolo. Seleziona **Consenti formato RTF per il titolo** per modificare il titolo in formato RTF. Puoi anche contrassegnare il titolo come **Elemento modulo non associato**.
   * **[!UICONTROL Configurazione CAPTCHA]:** Seleziona una configurazione dal menu a discesa Impostazioni per **reCAPTCHA Enterprise** o **reCAPTCHA v2** per visualizzare la finestra di dialogo Google reCAPTCHA per il modulo:
      1. Se si seleziona la versione **reCAPTCHA Enterprise**, il tipo di chiave può essere di **casella di controllo** o **punteggio basato**, si basa sulla selezione quando si configura [chiave sito per siti Web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

         >[!NOTE]
         >
         >* Nella configurazione cloud con **tipo chiave** come **casella di controllo**, il messaggio di errore personalizzato viene visualizzato come messaggio in linea se la convalida captcha non riesce.
         >* Nella configurazione cloud con **tipo chiave** come **punteggio basato**, il messaggio di errore personalizzato viene visualizzato come messaggio popup se la convalida captcha non riesce.

      1. È possibile selezionare le dimensioni come **[!UICONTROL Normale]** e **[!UICONTROL Compatta]**.

     >[!NOTE]
     >* Puoi avere più configurazioni cloud nell’ambiente per scopi simili. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Connettere l&#39;ambiente AEM Forms con il servizio reCAPTCHA di Google](#connect-your-forms-environment-with-recaptcha-service-by-google) per scoprire come creare un Cloud Service che colleghi l&#39;ambiente AEM Forms con il servizio reCAPTCHA di Google.

   * **Dimensione Captcha:** È possibile selezionare la dimensione di visualizzazione della finestra di dialogo di verifica reCAPTCHA di Google. Utilizza l&#39;opzione **[!UICONTROL Compact]** per visualizzare una finestra di dialogo di verifica Google reCAPTCHA di piccole dimensioni e l&#39;opzione **[!UICONTROL Normal]** per visualizzare una finestra di dialogo di verifica reCAPTCHA di dimensioni relativamente grandi.
Se si seleziona **reCAPTCHA v2** versione:
      1. È possibile selezionare la dimensione come **[!UICONTROL Normal]** o **[!UICONTROL Compact]** per il widget reCAPTCHA.
      1. È possibile selezionare l&#39;opzione **[!UICONTROL Invisibile]** per visualizzare la richiesta CAPTCHA solo nel caso di attività sospetta.

   Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere il CAPTCHA che funziona. Il badge **protetto da reCAPTCHA**, visualizzato di seguito, viene visualizzato nei moduli protetti.

   ![Google protetto da badge reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

1. Seleziona **[!UICONTROL Fine]**.

   Ora **protetto da reCAPTCHA** è visualizzato nel modulo adattivo. Viene visualizzato su tutti i Forms adattivi configurati per utilizzare il servizio Google reCAPTCHA.

   Ora, solo i moduli legittimi, in cui la compilazione del modulo risolve con successo la sfida posta dal servizio Google reCAPTCHA, sono consentiti per l’invio.

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

**D: posso utilizzare più di un componente Captcha in un modulo adattivo?**
**Ans:** L&#39;utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}
