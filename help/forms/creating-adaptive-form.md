---
title: Come creare un Forms adattivo
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. I Forms adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondisci le modalità di creazione di un modulo adattivo basato su un modello di dati modulo e uno schema XML o JSON.
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 59e27998820e3c877c5594b9284b43ce108394fa
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 4%

---

# Creare un modulo adattivo (componenti di base) {#creating-an-adaptive-form}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html) |
| AEM as a Cloud Service | Questo articolo |


<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Forms adattivo consente di creare moduli coinvolgenti, reattivi, dinamici e adattivi. AEM Forms fornisce una procedura intuitiva e rapida per la creazione di Adaptive Forms pensata per gli utenti aziendali. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per la creazione di un modulo adattivo.

Prima di iniziare, scopri i tipi di componenti Forms disponibili:

* [Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) sono componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può personalizzare e assegnare uno stile a questi componenti. L’Adobe consiglia di sfruttare questi componenti moderni ed estensibili per sviluppare Forms adattivo.

* [Componenti adattivi di Forms Foundation](creating-adaptive-form.md) sono componenti di acquisizione dati classici (vecchi). Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando nuovi moduli, l’Adobe consiglia di utilizzare  [Componenti core Forms adattivi](creating-adaptive-form-core-components.md) per creare un Forms adattivo.



<!-- 

You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form: 

-->

![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)

<!-- 

Adaptive Forms allow you to create forms that are engaging, responsive, dynamic, and adaptive. [!DNL AEM Forms] provides an intuitive wizard and out-of-the-box components to create Adaptive Forms. You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form:

* **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source.

  <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. 

* **Using an XML Schema Definition (XSD) or a JSON Schema**
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option do not use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* **Autorizzazioni**: aggiungi gli utenti a [!DNL forms-users] per fornire loro le autorizzazioni per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici per i moduli, consulta [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

* **Un tema per moduli adattivi**: un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l&#39;allineamento e le dimensioni. Quando applicate un tema, lo stile specificato viene riflesso sui componenti corrispondenti. È possibile [crea un nuovo tema](themes.md) o [importa un tema esistente](import-export-forms-templates.md#uploading-a-theme). Puoi anche distribuire [archetipo più recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) per alcuni temi di esempio.

* **Un modello di modulo adattivo**: un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. Fornisce inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’azione &quot;look and feel&quot; e &quot;submit&quot; definisce l’azione da intraprendere al momento dell’invio di un modulo adattivo. Ad esempio, l’invio dei dati raccolti a un’origine dati. Il servizio cloud supporta due tipi di modelli:

   * **Modello modificabile**: puoi [crea un nuovo](template-editor.md) o [importa un modello modificabile esistente](migrate-to-forms-as-a-cloud-service.md). Puoi anche distribuire [archetipo più recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20sono%20basati su Java%20integration%20tests.) per ottenere alcuni modelli modificabili di esempio.

   * **Modello statico**: si tratta di modelli legacy e sono consigliati solo per i clienti che eseguono la migrazione dalle installazioni di Adobe Managed Services (AMS) e AEM Forms on-premise (AEM 6.5 Forms o versioni precedenti). Questi consentono di continuare a utilizzare l’investimento esistente nei modelli statici. Quando crei un nuovo modulo adattivo, si consiglia di utilizzare un modello modificabile.



## Creare un modulo adattivo (componenti di base) {#create-an-adaptive-form-foundation-components}

1. Accesso [!DNL Experience Manager Forms] Istanza Autore. Può essere un’istanza Cloud o un’istanza di sviluppo locale.

1. Immetti le credenziali nella pagina di accesso di Experience Manager.

   Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Tocca **[!UICONTROL Crea]**  > **[!UICONTROL Forms adattivo]**. Viene visualizzata la procedura guidata.
1. Nella scheda Origine, seleziona un modello:

   * Quando selezioni un modello modificabile, viene selezionato automaticamente un tema e un’azione di invio specificati nel modello, e il **[!UICONTROL Crea]** è attivato. È possibile passare al **[!UICONTROL Stile]** o **[!UICONTROL Invio]** per selezionare un tema diverso o un’azione di invio diversa. Se il modello modificabile selezionato non specifica un tema, il pulsante Crea rimane disattivato. È possibile passare al **[!UICONTROL Stili]** per selezionare manualmente un tema.

     >[!NOTE]
     >
     > Puoi anche creare [!UICONTROL Documento record] mediante un editor di Forms adattivo. Per ulteriori informazioni, consulta [Supporto per documenti di record nell’editor di moduli adattivi](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * Quando selezioni un modello statico, le opzioni di dati, stile, invio, consegna e anteprima non sono disponibili. Quando crei un nuovo modulo adattivo, si consiglia di utilizzare un modello modificabile.

1. In **[!UICONTROL Stile]** , selezionare un tema:

   * Quando il modello selezionato specifica un tema, il tema viene selezionato automaticamente nella procedura guidata. È inoltre possibile scegliere un tema diverso dalla scheda Stile.
   * Se nel modello selezionato non è specificato un tema, è possibile utilizzare la scheda Stile per scegliere un tema. Il **[!UICONTROL Crea]** viene attivato solo dopo la selezione di un tema.

1. (Facoltativo) In **[!UICONTROL Dati]** , seleziona un modello dati:

   * **Modello dati modulo**: A [Modello dati modulo](data-integration.md) consente di integrare entità e servizi da diverse origini dati a un modulo adattivo. Scegli modello dati modulo se il modulo adattivo che stai creando richiede il recupero e la scrittura di dati da e verso più origini dati.

   * **Schema JSON**: [Schema JSON](adaptive-form-json-schema-form-model.md) rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell’organizzazione. È possibile associare lo schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili per l’utilizzo nella scheda Oggetti modello dati del browser Contenuto durante l’authoring di Forms adattivo. Tutti i campi vengono aggiunti anche al nuovo modulo adattivo creato.

   Per impostazione predefinita, vengono selezionati tutti i campi del modello dati. Quando crei il modulo adattivo, tutti i campi del modello dati selezionati vengono convertiti nei corrispondenti componenti del modulo adattivo. La procedura guidata fornisce caselle di controllo per selezionare solo i campi da includere nel modulo adattivo.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. In **[!UICONTROL Invio]** , seleziona un’azione di invio:

   * Quando selezioni un modello, l’azione di invio specificata nel modello viene selezionata automaticamente. Puoi selezionare un’azione di invio diversa dalla scheda Invio. Il **[!UICONTROL Invio]** visualizza tutte le azioni di invio disponibili.

   * Se nel modello selezionato non è specificata un&#39;azione di invio, è possibile utilizzare **[!UICONTROL Invio]** per selezionare un’azione di invio

1. (Facoltativo) Nella scheda Consegna, puoi specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo adattivo.

1. Tocca **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo che specifica il titolo, il nome e la posizione in cui salvare il modulo adattivo:

   * **[!UICONTROL Titolo]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel [!DNL Experience Manager Forms] dell&#39;utente.
   * **[!UICONTROL Nome:]** Specifica il nome del modulo. Nell&#39;archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo del nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo del nome può contenere solo caratteri alfanumerici, trattini e trattini bassi. Tutti gli input non validi vengono sostituiti da un trattino.
   * **[!UICONTROL Percorso:]** Specifica la posizione in cui deve essere salvato il modulo adattivo. Puoi salvare il modulo adattivo direttamente all’indirizzo `/content/dam/formsanddocuments` o crea una cartella come `/content/dam/formsanddocuments/adaptiveforms` per salvare un modulo adattivo. Assicurati di creare la cartella prima di utilizzarla nel percorso. Il **[!UICONTROL Percorso:]** non crea automaticamente una cartella.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo che viene aperto nell’editor di Forms adattivo. L’editor visualizza i contenuti disponibili nel modello. Viene inoltre visualizzata la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   In base al tipo di modulo adattivo, gli elementi del modulo presenti nel <!--XFA form template, XML schema or --> Lo schema JSON o il modello dati del modulo vengono visualizzati nel **[!UICONTROL Oggetti modello dati]** scheda di **[!UICONTROL Browser contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Tap to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and tap Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model). -->

## Modificare le proprietà di un modello di modulo adattivo {#edit-form-model}

Puoi modificare il modello di modulo per un modulo adattivo (basato su JSON o modello dati modulo). Non è possibile passare da un modello di modulo a un altro.

1. Seleziona il modulo adattivo e tocca il **Proprietà** icona.
1. Apri **[!UICONTROL Modello modulo]** ed effettuare una delle seguenti operazioni.

   * Se il modulo adattivo non dispone di un modello di modulo, puoi scegliere un altro modello di modulo e quindi selezionare <!-- a form template, --> Schema XML o JSON o modello dati modulo.
   * Se il modulo adattivo è basato su un modello di modulo, puoi sceglierne un altro <!-- form template, --> Schema XML o JSON o modello dati modulo per lo stesso modello di modulo.

1. Tocca **[!UICONTROL Salva]** per salvare le proprietà.

È inoltre possibile modificare le proprietà del modello di modulo dall’editor di moduli adattivi o dall’editor di modelli di moduli adattivi.

1. Seleziona la **[!UICONTROL Contenitore modulo adattivo (radice)]** componente.
1. Clic ![Icona Configura](/help/forms/assets/configure-icon.svg) per aprire **[!UICONTROL Proprietà]** del contenitore Modulo adattivo.
1. Seleziona la **[!UICONTROL Modello dati]** ed effettuare una delle seguenti operazioni:

   * Se il modulo adattivo non dispone di un modello di modulo, puoi scegliere un modello di modulo e quindi selezionare <!-- a form template, --> Schema XML o JSON o modello dati modulo.
   * Se il modulo adattivo è basato su un modello di modulo, non è possibile modificarlo. Puoi sceglierne un altro <!-- form template, --> Schema XML o JSON o modello dati modulo per lo stesso modello di modulo applicabile.
1. Tocca ![Salva](/help/forms/assets/check-button.png) per salvare le proprietà.

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png)

>[!NOTE]
>
> È inoltre possibile salvare un modulo adattivo come modello. Per ulteriori informazioni, consulta [Creare un modello utilizzando un modulo adattivo](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).