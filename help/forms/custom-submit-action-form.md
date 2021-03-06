---
title: Come creare un’azione di invio personalizzata per un modulo adattivo?
description: Scopri come creare un’azione di invio personalizzata per un Forms adattivo per ritardare l’invio e l’elaborazione dei dati prima di inviarli a un endpoint rest, salvarli in un archivio dati ed eseguire altre funzioni personalizzate.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 77131cc2-9cb1-4a00-bbc4-65b1a66e76f5
source-git-commit: 391a9482cc6ed97984693c21b41910fdd32ff25d
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 0%

---

# Creare un’azione di invio personalizzata per Adaptive Forms {#writing-custom-submit-action-for-adaptive-forms}

Un modulo adattivo fornisce più azioni di invio pronte all’uso (OOTB). Un’azione di invio specifica i dettagli delle azioni da eseguire sui dati raccolti tramite il modulo adattivo. Ad esempio, l’invio di dati tramite e-mail.

Puoi creare un’azione di invio personalizzata per aggiungere funzionalità non incluse in [Azioni di invio predefinite](configuring-submit-actions.md) o non supportato da una singola azione di invio OOTB. Ad esempio, l’invio di dati a un flusso di lavoro, il salvataggio dei dati in un archivio dati, l’invio di notifiche e-mail alla persona che invia il modulo e-mail alla persona responsabile dell’elaborazione del modulo inviato per le approvazioni e i rifiuti tramite una singola azione di invio.

## Formato dati XML {#xml-data-format}

I dati XML vengono inviati al servlet utilizzando **`jcr:data`** parametro di richiesta. Azioni di invio consente di accedere al parametro per elaborare i dati. Il codice seguente descrive il formato dei dati XML. I campi associati al modello Modulo vengono visualizzati nella **`afBoundData`** sezione . I campi non associati vengono visualizzati nella `afUnoundData`sezione . <!--For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).-->

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Campi azione {#action-fields}

Un’azione di invio può aggiungere campi di input nascosti (utilizzando HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) al modulo di cui è stato effettuato il rendering in HTML. Questi campi nascosti possono contenere i valori necessari durante l’elaborazione dell’invio del modulo. Quando si invia il modulo, questi valori dei campi vengono riportati come parametri di richiesta che l’azione di invio può utilizzare durante la gestione dell’invio. I campi di input sono chiamati campi di azione.

Ad esempio, un’azione di invio che acquisisce anche il tempo necessario per compilare un modulo può aggiungere campi di input nascosti `startTime` e `endTime`.

Uno script può fornire i valori `startTime` e `endTime` i campi in cui viene eseguito il rendering del modulo e prima dell’invio del modulo, rispettivamente. Lo script dell’azione Invia `post.jsp` può quindi accedere a questi campi utilizzando i parametri di richiesta e calcolare il tempo totale necessario per compilare il modulo.

### Allegati file {#file-attachments}

Le azioni di invio possono inoltre utilizzare gli allegati file caricati utilizzando il componente File allegato. Gli script di azione Invia possono accedere a questi file utilizzando lo sling [API RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). La [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) Il metodo dell&#39;API aiuta a identificare se il parametro della richiesta è un file o un campo del modulo. È possibile eseguire iterazioni sui parametri di richiesta in un’azione di invio per identificare i parametri di File allegato.

Il codice di esempio seguente identifica gli allegati di file nella richiesta. Successivamente, legge i dati nel file utilizzando [Ottieni API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Infine, crea un oggetto Document utilizzando i dati e lo aggiunge a un elenco.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

Quando alleghi dei file al modulo adattivo, il server convalida gli allegati dopo l’invio del modulo adattivo e restituisce un messaggio di errore se:

* Gli allegati dei file includono un nome di file che inizia con (.) carattere, contiene \ / : * ? &quot; &lt; > | % $ caratteri o contiene nomi di file speciali riservati al sistema operativo Windows, ad esempio `nul`, `prn`, `con`, `lpt`oppure `com`.

* La dimensione dell&#39;allegato del file è di 0 byte.

* Il formato dell&#39;allegato del file non è definito nella [Tipi di file supportati](https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text) durante la configurazione del componente File allegato in un modulo adattivo.

### URL di percorso e reindirizzamento {#forward-path-and-redirect-url}

Dopo aver eseguito l’azione richiesta, il servlet di invio inoltra la richiesta al percorso successivo. Un’azione utilizza l’API setForwardPath per impostare il percorso in avanti nel servlet di invio della guida.

Se l’azione non fornisce un percorso in avanti, il servlet di invio reindirizzerà il browser utilizzando l’URL di reindirizzamento. L’autore configura l’URL di reindirizzamento utilizzando la configurazione Pagina di ringraziamento nella finestra di dialogo Modifica modulo adattivo. Puoi anche configurare l’URL di reindirizzamento tramite l’azione di invio o l’API setRedirectUrl nel servlet di invio della guida. Puoi anche configurare i parametri Request inviati all’URL di reindirizzamento utilizzando l’API setRedirectParameters nel servlet di invio della guida.

>[!NOTE]
>
>Un autore fornisce l’URL di reindirizzamento (utilizzando la configurazione della pagina di ringraziamento). [Azioni di invio OOTB](configuring-submit-actions.md) utilizza l&#39;URL di reindirizzamento per reindirizzare il browser dalla risorsa a cui fa riferimento il percorso in avanti.
>
>È possibile scrivere un’azione di invio personalizzata che inoltra una richiesta a una risorsa o a un servlet. L’Adobe consiglia che lo script che esegue la gestione delle risorse per il percorso di avanzamento reindirizzi la richiesta all’URL di reindirizzamento al termine dell’elaborazione.

## Azione invio {#submit-action}

Un’azione di invio è una sling:Folder che include quanto segue:

* **addfields.jsp**: Questo script fornisce i campi azione che vengono aggiunti al file HTML durante il rendering. Utilizza questo script per aggiungere i parametri di input nascosti richiesti durante l’invio nello script post.POST.jsp.
* **dialog.xml**: Questo script è simile alla finestra di dialogo del componente CQ. Fornisce informazioni di configurazione personalizzate dall’autore. I campi vengono visualizzati nella scheda Azioni di invio della finestra di dialogo Modifica modulo adattivo quando si seleziona l’azione di invio.
* **post.POST.jsp**: Il servlet di invio chiama questo script con i dati inviati e i dati aggiuntivi nelle sezioni precedenti. Qualsiasi menzione dell&#39;esecuzione di un&#39;azione in questa pagina implica l&#39;esecuzione dello script post.POST.jsp. Per registrare l’azione di invio con la Forms adattiva da visualizzare nella finestra di dialogo Modifica modulo adattivo, aggiungi queste proprietà allo sling:Folder:

   * **guideComponentType** di tipo String e di valore **fd/af/components/guidesubmittype**
   * **guideDataModel** di tipo String che specifica il tipo di Modulo adattivo per il quale è applicabile l’azione Invia. <!--**xfa** is supported for XFA-based Adaptive Forms while -->**xsd** è supportato per Forms adattivo basato su XSD. **base** è supportato per i Forms adattivi che non utilizzano XDP o XSD. Per visualizzare l&#39;azione su più tipi di Adaptive Forms, aggiungi le stringhe corrispondenti. Separa ogni stringa con una virgola. Ad esempio, per rendere visibile un’azione in <!--XFA- and -->Forms adattivo basato su XSD, specifica il valore come <!--**xfa** and--> **xsd**.

   * **jcr:description** di tipo String. Il valore di questa proprietà viene visualizzato nell’elenco Invia azioni della scheda Invia azioni della finestra di dialogo Modifica modulo adattivo. Le azioni OOTB sono presenti nell’archivio CRX nella posizione **/libs/fd/af/components/guidesubmittype**.

   * **submitService** di tipo String. Per ulteriori informazioni, consulta [Pianificazione dell’invio di moduli adattivi per azioni personalizzate](#schedule-adaptive-form-submission).

## Creazione di un’azione di invio personalizzata {#creating-a-custom-submit-action}

Esegui i seguenti passaggi per creare un’azione di invio personalizzata che salva i dati nell’archivio CRX e quindi invia un’e-mail. Il modulo adattivo contiene il contenuto dell’archivio azioni di invio OOTB (obsoleto) che salva i dati nell’archivio CRX. Inoltre, AEM fornisce un [Posta](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) API che può essere utilizzata per inviare e-mail. Prima di utilizzare l&#39;API Mail, configurare il servizio Day CQ Mail tramite la console di sistema. Puoi riutilizzare l’azione Archivia contenuto (obsoleto) per memorizzare i dati nell’archivio. L’azione Archivia contenuto (obsoleto) è disponibile nel percorso /libs/fd/af/components/guidesubmittype/store nell’archivio CRX.

1. Accedi a CRXDE Lite all’URL https://&lt;server>:&lt;port>/crx/de/index.jsp. Crea un nodo con la proprietà sling:Folder e il nome store_and_mail nella cartella /apps/custom_submit_action . Crea la cartella custom_submit_action se non esiste già.

   ![Schermata che descrive la creazione di un nodo con la proprietà sling:Folder](assets/step1.png)

1. **Fornisci i campi di configurazione obbligatori.**

   Aggiungi la configurazione necessaria per l&#39;azione Store. Copia il **cq:dialog** nodo dell&#39;azione Store da /libs/fd/af/components/guidesubmittype/store alla cartella delle azioni in /apps/custom_submit_action/store_and_email.

   ![Schermata che mostra la copia del nodo di dialogo nella cartella delle azioni](assets/step2.png)

1. **Fornisci campi di configurazione per richiedere all’autore la configurazione dell’e-mail.**

   Il Modulo adattivo fornisce anche un’azione e-mail che invia e-mail agli utenti. Personalizza questa azione in base alle tue esigenze. Passa a /libs/fd/af/components/guidesubmittype/email/dialog. Copia i nodi all’interno del nodo cq:dialog nel nodo cq:dialog dell’azione di invio (/apps/custom_submit_action/store_and_email/dialog).

   ![Personalizzazione dell’azione e-mail](assets/step3.png)

1. **Rendi disponibile l’azione nella finestra di dialogo Modifica modulo adattivo .**

   Aggiungi le seguenti proprietà nel nodo store_and_email:

   * **guideComponentType** di tipo **Stringa** e valore **fd/af/components/guidesubmittype**

   * **guideDataModel** di tipo **Stringa** e valore **<!--xfa, -->xsd, base**

   * **jcr:description** di tipo **Stringa** e valore **Azione store ed e-mail**

   * **submitService** di tipo **Stringa** e valore **Archivio ed e-mail**. Per ulteriori informazioni, consulta [Pianificazione dell’invio di moduli adattivi per azioni personalizzate](#schedule-adaptive-form-submission).

1. Aprire un modulo adattivo. Fai clic sul pulsante **Modifica** pulsante accanto a **Inizio** per aprire **Modifica** del contenitore Modulo adattivo. La nuova azione viene visualizzata nella **Inviare azioni** Tab. Selezione della **Azione store ed e-mail** visualizza la configurazione aggiunta nel nodo della finestra di dialogo.

   ![Finestra di dialogo per la configurazione dell’azione Invia](assets/store_and_email_submit_action_dialog.jpg)

1. **Utilizzare l&#39;azione per completare un&#39;attività.**

   Aggiungi lo script post.POST.jsp all&#39;azione. (/apps/custom_submit_action/store_and_mail/).

   Esegui l&#39;azione OOTB Store (script post.POST.jsp). Utilizza la [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-)(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) API che CQ fornisce nel codice per eseguire l&#39;azione Store. Aggiungi il seguente codice nel file JSP:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Per inviare l’e-mail, il codice legge l’indirizzo e-mail del destinatario dalla configurazione. Per recuperare il valore di configurazione nello script dell’azione, leggi le proprietà della risorsa corrente utilizzando il codice seguente. Allo stesso modo puoi leggere gli altri file di configurazione.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Infine, utilizza l’API CQ Mail per inviare l’e-mail. Utilizza la [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) Classe per creare l’oggetto e-mail come illustrato di seguito:

   >[!NOTE]
   >
   >Assicurati che il file JSP abbia il nome post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Seleziona l’azione nel modulo adattivo. L’azione invia un’e-mail e memorizza i dati.

## Utilizzare la proprietà submitService per le azioni di invio personalizzate {#submitservice-property}

Quando imposti l’azione di invio personalizzata, che include `submitService` , il modulo attiva la proprietà [FormSubmitActionService](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/service/FormSubmitActionService.html) su presentazione. La `FormSubmitActionService` utilizza `getServiceName` per recuperare il valore per `submitService` proprietà. In base al valore del `submitService` , il servizio richiama il metodo submit appropriato. Includi il `FormSubmitActionService` nel bundle personalizzato caricato nel [!DNL AEM Forms] server.

Aggiungi il `submitService` proprietà di tipo string al `sling:Folder` dell’azione di invio personalizzata per abilitare [!DNL Adobe Sign] per il modulo adattivo. È possibile selezionare la **[!UICONTROL Abilita Adobe Sign]** in **[!UICONTROL Firma elettronica]** delle proprietà del contenitore Modulo adattivo solo dopo aver impostato il valore per `submitService` proprietà dell&#39;azione di invio personalizzata.

<!--As a result of setting an appropriate value for the `submitService` property and enabling [!DNL Adobe Sign], you can schedule the submission of an Adaptive Form to ensure that all configured signers have taken an action on the form. [!DNL Adobe Sign] Configuration Service keeps polling [!DNL Adobe Sign] server at regular intervals to verify the status of signatures. If all the signers complete signing the form, the Submit Action service is started and the form is submitted.-->


![Invia proprietà servizio](assets/submit-service-property.png)

<!-- You can't do comments within comments, so I changed comment tags to <start-comment> <end-comment> -->

<!--
## Workflow for a Submit Action {#workflow-for-a-submit-action}

The flowchart depicts the workflow for a Submit Action that is triggered when you click the **[!UICONTROL Submit]** button in an Adaptive Form. The files in the File Attachment component are uploaded to the server, and the form data is updated with the URLs of the uploaded files. Within the client, the data is stored in the JSON format. The client sends an Ajax request to an internal servlet that massages the data you specified and returns it in the XML format. The client collates this data with action fields. It submits the data to the final servlet (Guide Submit servlet) through a Form Submit Action. Then, the servlet forwards the control to the Submit Action. The Submit Action can forward the request to a different sling resource or redirect the browser to another URL.

![Flowchart depicting the workflow for Submit Action](assets/diagram1.png)

### XML data format {#xml-data-format}

The XML data is sent to the servlet using the **`jcr:data`** request parameter. Submit Actions can access the parameter to process the data. The following code describes the format of the XML data. The fields that are bound to the Form model appear in the **`afBoundData`** section. Unbound fields appear in the `afUnoundData`section. For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<start comment> xml corresponding to the Form Model /XML Schema <end comment>
<start comment> </afBoundData> <end comment>
</afData>
```

### Action fields {#action-fields}

A Submit Action can add hidden input fields (using the HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) tag) to the rendered form HTML. These hidden fields can contain values that it needs while processing form submission. When submitting the form, these field values are posted back as request parameters that the Submit Action can use during submission handling. The input fields are called action fields.

For example, a Submit Action that also captures the time taken to fill a form can add the hidden input fields `startTime` and `endTime`.

A script can supply the values of the `startTime` and `endTime` fields when the form renders and before form submission, respectively. The Submit Action script `post.jsp` can then access these fields using request parameters and compute the total time required to fill the form.

### File attachments {#file-attachments}

Submit Actions can also use the file attachments you upload using the File Attachment component. Submit Action scripts can access these files using the sling [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). The [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) method of the API helps identify whether the request parameter is a file or a form field. You can iterate over the Request parameters in a Submit Action to identify File Attachment parameters.

The following sample code identifies the file attachments in the request. Next, it reads the data into the file using the [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Finally, it creates a Document object using the data and appends it to a list.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Forward path and Redirect URL {#forward-path-and-redirect-url}

After performing the required action, the Submit servlet forwards the request to the forward path. An action uses the setForwardPath API to set the forward path in the Guide Submit servlet.

If the action doesn't provide a forward path, the Submit servlet redirects the browser using the Redirect URL. The author configures the Redirect URL using the Thank You Page configuration in the Adaptive Form Edit dialog. You can also configure the Redirect URL through the Submit Action or the setRedirectUrl API in the Guide Submit servlet. You can also configure the Request parameters sent to the Redirect URL using the setRedirectParameters API in the Guide Submit servlet.

>[!NOTE]
>
>An author provides the Redirect URL (using the Thank You Page Configuration). [OOTB Submit Actions](configuring-submit-actions.md) use the Redirect URL to redirect the browser from the resource that the forward path references.
>
>You can write a custom Submit Action that forwards a request to a resource or servlet. Adobe recommends that the script that performs resource handling for the forward path redirect the request to the Redirect URL when the processing completes.

## Submit Action {#submit-action}

A Submit Action is a sling:Folder that includes the following:

* **addfields.jsp**: This script provides the action fields that are added to the HTML file during rendition. Use this script to add hidden input parameters required during submission in the post.POST.jsp script.
* **dialog.xml**: This script is similar to the CQ Component dialog. It provides configuration information that the author customizes. The fields are displayed in the Submit Actions Tab in the Adaptive Form Edit dialog when you select the Submit Action.
* **post.POST.jsp**: The Submit servlet calls this script with the data that you submit and the additional data in the previous sections. Any mention of running an action in this page implies running the post.POST.jsp script. To register the Submit Action with the Adaptive Forms to display in the Adaptive Form Edit dialog, add these properties to the sling:Folder:

    * **guideComponentType** of type String and value **fd/af/components/guidesubmittype**
    * **guideDataModel** of type String that specifies the type of Adaptive Form for which the Submit Action is applicable. **xfa** is supported for XFA-based Adaptive Forms while **xsd** is supported for XSD-based Adaptive Forms. **basic** is supported for Adaptive Forms that do not use XDP or XSD. To display the action on multiple types of Adaptive Forms, add the corresponding strings. Separate each string by a comma. For example, to make an action visible on XFA- and XSD-based Adaptive Forms, specify the values **xfa** and **xsd** respectively.

    * **jcr:description** of type String. The value of this property is displayed in the Submit Action list in the Submit Actions Tab of the Adaptive Form Edit dialog. The OOTB actions are present in the CRX repository at the location **/libs/fd/af/components/guidesubmittype**.

## Creating a custom Submit Action {#creating-a-custom-submit-action}

Perform the following steps to create a custom Submit Action that saves the data in the CRX repository and then sends you an email. The Adaptive Form contains the OOTB Submit Action Store Content (deprecated) that saves the data in the CRX repository. In addition, CQ provides a [Mail](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) API that can be used to send emails. Before using the Mail API, configure the Day CQ Mail service through the system console. You can reuse the Store Content (deprecated) action to store the data in the repository. The Store Content (deprecated) action is available at the location /libs/fd/af/components/guidesubmittype/store in the CRX repository.

1. Log in to CRXDE Lite at the URL https://&lt;server&gt;:&lt;port&gt;/crx/de/index.jsp. Create a node with the property sling:Folder and name store_and_mail in the /apps/custom_submit_action folder. Create the custom_submit_action folder if it doesn't exist already.

   ![Screenshot depicting the creation of a node with the property sling:Folder](assets/step1.png)

1. **Provide the mandatory configuration fields.**

   Add the configuration the Store action requires. Copy the **cq:dialog** node of the Store action from /libs/fd/af/components/guidesubmittype/store to the action folder at /apps/custom_submit_action/store_and_email.

   ![Screenshot showing the copying of the dialog node to the action folder](assets/step2.png)

1. **Provide configuration fields to prompt the author for email configuration.**

   The Adaptive Form also provides an Email action that sends emails to users. Customize this action based on your requirements. Navigate to /libs/fd/af/components/guidesubmittype/email/dialog. Copy the nodes within the cq:dialog node to cq:dialog node of your Submit Action (/apps/custom_submit_action/store_and_email/dialog).

   ![Customizing the email action](assets/step3.png)

1. **Make the action available in the Adaptive Form Edit dialog.**

   Add the following properties in the store_and_email node:

    * **guideComponentType** of type **String** and value **fd/af/components/guidesubmittype**

    * **guideDataModel** of type **String** and value **xfa, xsd, basic**

    * **jcr:description** of type **String** and value **Store and Email Action**

1. Open any Adaptive Form. Click the **Edit** button next to **Start** to open the **Edit** dialog of the Adaptive Form container. The new action is displayed in the **Submit Actions** Tab. Selecting the **Store and Email Action** displays the configuration added in the dialog node.

   ![Submit Action configuration dialog](assets/store_and_email_submit_action_dialog.jpg)

1. **Use the action to complete a task.**

   Add the post.POST.jsp script to your action. (/apps/custom_submit_action/store_and_mail/).

   Run the OOTB Store action (post.POST.jsp script). Use the [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)) API that CQ provides in your code to run the Store action. Add the following code in your JSP file:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   To send the email, the code reads the recipient's email address from the configuration. To fetch the configuration value in the action's script, read the properties of the current resource using the following code. Similarly you can read the other configuration files.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Finally, use the CQ Mail API to send the email. Use the [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) class to create the Email Object as depicted below:

   >[!NOTE]
   >
   >Ensure that the JSP file has the name post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Select the action in the Adaptive Form. The action sends an email and stores the data. 

-->
