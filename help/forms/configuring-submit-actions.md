---
title: Come configurare un’azione di invio per un modulo adattivo
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. È possibile utilizzare le azioni di invio integrate o crearne una personalizzata.
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 0%

---

# Azione di invio di moduli adattivi {#configuring-the-submit-action}

Un’azione di invio viene attivata quando un utente fa clic sul pulsante **[!UICONTROL Invia]** su un modulo adattivo. Adaptive Forms fornisce alcune azioni di invio pronte all&#39;uso. Le azioni di invio disponibili sono:

* [Invia all’endpoint REST](#submit-to-rest-endpoint)
* [Invia e-mail](#send-email)
* [Invia usando il modello dati modulo](#submit-using-form-data-model)
* [Richiamare un flusso di lavoro AEM](#invoke-an-aem-workflow)

È inoltre possibile [estendere le azioni di invio predefinite](custom-submit-action-form.md) per creare un’azione di invio personalizzata.

Puoi configurare un’azione di invio nella **[!UICONTROL Invio]** della sezione delle proprietà del contenitore di moduli adattivi, nella barra laterale.

![Configurare l’azione Invia](assets/submission.png)


<!-- [!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it. -->

<!--

>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.


-->




## Invia all’endpoint REST {#submit-to-rest-endpoint}

Utilizza la **[!UICONTROL Invia a endpoint REST]** per inviare i dati inviati a un URL rimanente. L’URL può essere di un server interno (il server su cui viene eseguito il rendering del modulo) o di un server esterno.

Per inviare dati a un server interno, fornisci il percorso della risorsa. I dati vengono inviati nel percorso della risorsa. Ad esempio, /content/restEndPoint. Per tali richieste post, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

Per inviare dati a un server esterno, specifica un URL. Il formato dell’URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

![Mappatura dei valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

Nell’esempio precedente, l’utente ha immesso informazioni in `textbox` viene acquisito utilizzando il parametro `param1`. Sintassi per la registrazione dei dati acquisiti tramite `param1` è:

`String data=request.getParameter("param1");`

Analogamente, i parametri utilizzati per la registrazione di dati XML e allegati sono `dataXml` e `attachments`.

Ad esempio, è possibile utilizzare questi due parametri nello script per analizzare i dati in un punto finale residuo. Utilizza la sintassi seguente per memorizzare e analizzare i dati:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

In questo esempio, `data` memorizza i dati XML e `att` memorizza i dati degli allegati.

La **[!UICONTROL Invia all’endpoint REST]** Invia azione invia i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome dei campi da richiedere. Il formato della richiesta è:

`{fieldName}={request parameter name}`

Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con i valori copiati dal **casella di testo** e **casella numerica** campi per l’azione successiva.

![Configurazione dell&#39;azione di invio dell&#39;endpoint rimanente](assets/action-config.png)

È inoltre possibile **[!UICONTROL Abilita richiesta POST]** e fornire un URL per inviare la richiesta. Per inviare dati al server AEM che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso principale del server AEM. Esempio, `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizzare un percorso assoluto.

>[!NOTE]
>
>Per trasmettere i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

## Invia e-mail {#send-email}

È possibile utilizzare **[!UICONTROL Invia e-mail]** Invia azione per inviare un’e-mail a uno o più destinatari dopo l’invio corretto del modulo. L’e-mail generata può contenere dati del modulo in un formato predefinito. Ad esempio, nel modello seguente, il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviati.

    &quot;
    
    Hi ${customer_Name},
    
    Il seguente è impostato come indirizzo di spedizione predefinito:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Cordiali saluti,
    WKND
    
    &quot;

>[!NOTE]
>
> * Tutti i campi del modulo devono avere nomi di elementi diversi, anche se si trovano su pannelli diversi di un modulo adattivo.
> * AEM as a Cloud Service richiede che la posta in uscita sia crittografata. Per impostazione predefinita, le e-mail in uscita sono disabilitate. Per attivarlo, invia un ticket di supporto a [Richiesta di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


È inoltre possibile includere allegati e un documento di record (DoR) nell’e-mail. Per abilitare **[!UICONTROL Allega documento di registrazione]** configurare il modulo adattivo per generare un documento di record (DoR). È possibile abilitare l’opzione per generare un documento di record dalle proprietà Modulo adattivo.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Invia usando il modello dati modulo {#submit-using-form-data-model}

La **[!UICONTROL Invia utilizzando il modello dati del modulo]** L’azione di invio scrive i dati del modulo adattivo inviati per l’oggetto modello dati specificato in un modello dati modulo nella relativa origine dati. Durante la configurazione dell’azione di invio, è possibile scegliere un oggetto modello dati di cui si desidera riscrivere i dati inviati nella relativa origine dati.

Inoltre, è possibile inviare all’origine dati un allegato del modulo utilizzando un modello dati modulo e un documento di record. Per informazioni sul modello dati del modulo, consultare [[!DNL AEM Forms] Integrazione dei dati](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Richiamare un flusso di lavoro AEM {#invoke-an-aem-workflow}

La **[!UICONTROL Richiamare un flusso di lavoro AEM]** Invia azione associa un modulo adattivo a un [Flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente nell’istanza di authoring. L’azione Invia inserisce quanto segue nel percorso di payload del flusso di lavoro:

* **File di dati**: Contiene i dati inviati al modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso file dati]** per specificare il nome del file e il percorso del file relativo al payload. Ad esempio, il `/addresschange/data.xml` crea una cartella denominata `addresschange` e lo posiziona rispetto al carico utile. Puoi anche specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle.

* **Allegati**: È possibile utilizzare **[!UICONTROL Percorso allegato]** opzione per specificare il nome della cartella in cui memorizzare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload.

* **Documento di registrazione**: Contiene il documento di record generato per il modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso del documento di registrazione]** per specificare il nome del file del documento di record e il percorso del file relativo al payload. Ad esempio, il `/addresschange/DoR.pdf` crea una cartella denominata `addresschange` relativo al payload e inserisce il `DoR.pdf` relativo al payload. Puoi anche specificare solo `DoR.pdf` per salvare solo il documento di record senza creare una gerarchia di cartelle.

Prima di utilizzare **[!UICONTROL Richiamare un flusso di lavoro AEM]** Invia azione configura quanto segue per **[!UICONTROL Servizio impostazioni di DS AEM]** configurazione:

* **[!UICONTROL URL server di elaborazione]**: Il server di elaborazione è il server in cui viene attivato il flusso di lavoro Forms o AEM. Può essere lo stesso dell’URL dell’istanza di authoring AEM o di un altro server.

* **[!UICONTROL Nome utente del server di elaborazione]**: Nome utente dell’utente del flusso di lavoro

* **[!UICONTROL Password server di elaborazione]**: Password dell’utente del flusso di lavoro

Per impostare i valori di una configurazione, [Generare configurazioni OSGi utilizzando l’SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all&#39;istanza di Cloud Service.

## Utilizzare l’invio sincrono o asincrono {#use-synchronous-or-asynchronous-submission}

Un’azione di invio può utilizzare l’invio sincrono o asincrono.

**Invio sincrono**: In genere, i moduli web sono configurati per l’invio in modo sincrono. In un invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento o in caso di errore di invio, a una pagina di errore. È possibile selezionare la **[!UICONTROL Utilizzare l’invio asincrono]** per reindirizzare gli utenti a una pagina web o mostrare un messaggio all’invio.

![Configurare l’azione Invia](assets/thank-you-setting.png)

**Invio asincrono**: Le esperienze web moderne, come le applicazioni a pagina singola, stanno guadagnando popolarità laddove la pagina web rimane statica mentre l&#39;interazione client-server avviene in background. È ora possibile fornire questa esperienza con Adaptive Forms tramite [configurazione dell’invio asincrono](asynchronous-submissions-adaptive-forms.md).

## Rivalutazione lato server in forma adattiva {#server-side-revalidation-in-adaptive-form}

In genere, in qualsiasi sistema di acquisizione dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole business. Ma nei browser moderni, gli utenti finali hanno modo di bypassare tali convalide e fare manualmente gli invii utilizzando varie tecniche, come ad esempio Web Browser DevTools Console. Tali tecniche sono valide anche per Adaptive Forms. Uno sviluppatore di moduli può creare diversi logici di convalida, ma tecnicamente, gli utenti finali possono ignorare tali logici di convalida e inviare dati non validi al server. Dati non validi potrebbero interrompere le regole business applicate da un autore di moduli.

La funzione di riconvalida lato server consente di eseguire anche le convalide fornite da un autore di Forms adattivo durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi possibile compromesso tra l’invio dei dati e le violazioni delle regole aziendali rappresentate in termini di convalida dei moduli.

### Cosa convalidare sul server? {#what-to-validate-on-server-br}

Tutte le convalide predefinite (OOTB) di un modulo adattivo che vengono ripetute sul server sono:

* Obbligatorio
* Clausola di convalida dell&#39;immagine
* Espressione di convalida

### Abilitazione della convalida lato server {#enabling-server-side-validation-br}

Utilizza la **[!UICONTROL Rivelare sul server]** in Contenitore di moduli adattivi nella barra laterale per abilitare o disabilitare la convalida lato server per il modulo corrente.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

Abilitazione della convalida lato server

Se l’utente finale bypassa tali convalide e invia i moduli, il server esegue nuovamente la convalida. Se la convalida ha esito negativo al server, la transazione di invio viene arrestata. All’utente finale viene presentato nuovamente il modulo originale. I dati acquisiti e inviati vengono presentati all’utente come un errore.

>[!NOTE]
>
>La convalida lato server convalida il modello di modulo. È consigliabile creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile di HTML e la manipolazione DOM nella stessa libreria client.

### Supporto di funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

A volte, se **regole di convalida complesse**, lo script di convalida esatto risiede in funzioni personalizzate e l’autore chiama queste funzioni personalizzate dall’espressione di convalida del campo. Per rendere questa libreria di funzioni personalizzate nota e disponibile durante l’esecuzione di convalide lato server, l’autore del modulo può configurare il nome di AEM libreria client nella sezione **[!UICONTROL Base]** scheda delle proprietà del contenitore di moduli adattivi come mostrato di seguito.

![Supporto di funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto di funzioni personalizzate nelle espressioni di convalida

L’autore può configurare una libreria JavaScript personalizzata per modulo adattivo. Nella libreria , mantieni solo le funzioni riutilizzabili, che dipendono dalle librerie di terze parti jquery e underscore.js.

## Gestione degli errori nell’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida per la protezione e l’indurimento AEM, configura pagine di errore personalizzate come 400.jsp, 404.jsp e 500.jsp. Quando si invia un modulo 400, 404 o 500 vengono visualizzati errori di questi gestori. I gestori vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish . Puoi anche creare pagine JSP per altri codici di errore HTTP.

Quando si precompila un modello dati del modulo o un modulo adattivo basato su schema con dati XML o JSON in uno schema che non contiene dati `<afData>`, `<afBoundData>`e `</afUnboundData>` quindi i dati dei campi non associati del modulo adattivo vengono persi. Lo schema può essere uno schema XML, uno schema JSON o un modello dati modulo. I campi non collegati sono campi Modulo adattivo senza `bindref` proprietà.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
