---
title: 'Generatore di moduli: creare moduli con i componenti di base'
description: Scopri come utilizzare AEM Forms Form Builder per creare moduli adattivi con i componenti di base. Ideale per i creatori di moduli che mantengono moduli esistenti o che lavorano con integrazioni legacy.
keywords: generatore di moduli, componenti di base, creazione di moduli, creatore di moduli, moduli adattivi, creazione di moduli, AEM forms, creatore di moduli
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 61%

---

# Generatore di moduli: creare moduli con i componenti di base {#creating-an-adaptive-form}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |


>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

Il generatore di moduli di AEM Forms consente di creare moduli coinvolgenti, reattivi, dinamici e adattivi. Sia che tu sia un creatore di moduli che gestisce moduli basati su Foundation esistenti o che tu debba creare rapidamente moduli con componenti consolidati, AEM Forms fornisce una procedura guidata intuitiva. La procedura guidata offre una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati.

Prima di iniziare, scopri i tipi di componenti dei moduli disponibili:

* [I componenti core adattivi di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) sono componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione, riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può facilmente personalizzare e assegnare uno stile a questi componenti. Adobe consiglia di utilizzare questi componenti moderni ed estensibili per sviluppare Forms adattivo.

* [I componenti adattivi di Forms Foundation](creating-adaptive-form.md) sono componenti di acquisizione dati classici (precedenti). Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando nuovi moduli, Adobe consiglia di utilizzare [Componenti core Forms adattivi](creating-adaptive-form-core-components.md) per creare un Forms adattivo.



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

* **Autorizzazioni**: aggiungi gli utenti a [!DNL forms-users] per fornire loro le autorizzazioni per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici per i moduli, vedere [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

* **Un tema per moduli adattivi**: un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti. Puoi [creare un tema](themes.md) o [importare un tema esistente](import-export-forms-templates.md#uploading-a-theme). Puoi anche distribuire l’[archetipo più recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=it#create-project) per alcuni temi campioni.

* **Modello per moduli adattivi**: un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. Fornisce inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’aspetto, mentre l’azione di invio definisce l’azione da intraprendere al momento dell’invio di un modulo adattivo. Ad esempio, l’invio dei dati raccolti a un’origine dati. Cloud Service supporta due tipi di modelli:

   * **Modello modificabile**: è possibile [creare un](template-editor.md) o [importare un modello modificabile esistente](migrate-to-forms-as-a-cloud-service.md). Puoi anche distribuire l’[archetipo più recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=it#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests.) per ottenere alcuni modelli modificabili campioni.

   * **Modello statico**: si tratta di modelli legacy e sono consigliati solo se si esegue la migrazione da installazioni di AEM Forms On-Premise o Adobe Managed Services (AMS) (AEM Forms 6.5 o versioni precedenti). Consentono di continuare a sfruttare quanto hai già investito in modelli statici. Quando crei un modulo adattivo, utilizza un modello modificabile.



## Creare un modulo adattivo (componenti di base) {#create-an-adaptive-form-foundation-components}

1. Accedi all’istanza di authoring di [!DNL Experience Manager Forms]. Può essere un’istanza Cloud o un’istanza di sviluppo locale.

1. Inserisci le credenziali nella pagina di accesso di Experience Manager.

   Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene aperta la procedura guidata.
1. Nella scheda Sorgente, seleziona un modello:

   * Quando selezioni un modello modificabile, vengono selezionati automaticamente il tema e l’azione di invio specificati nel modello e viene abilitato il pulsante **[!UICONTROL Crea]**. Puoi per selezionare un altro tema o un’altra azione di invio dalla scheda **[!UICONTROL Stile]** o **[!UICONTROL Invio]**. Se nel modello modificabile selezionato non è stato specificato un tema, il pulsante Crea rimane disattivato. Puoi selezionare manualmente un tema dalla scheda **[!UICONTROL Stili]**.

     >[!NOTE]
     >
     > Puoi anche creare un modello di [!UICONTROL Documento record] tramite un editor di moduli adattivi. Per ulteriori informazioni, consulta [Supporto per documenti di record nell’editor di moduli adattivi](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * Quando selezioni un modello statico, le opzioni di dati, stile, invio, consegna e anteprima non sono disponibili. Quando crei un modulo adattivo, utilizza un modello modificabile.

1. Nella scheda **[!UICONTROL Stile]**, seleziona un tema:

   * Quando il modello selezionato specifica un tema, lo stesso viene selezionato automaticamente nella procedura guidata. È possibile inoltre scegliere un tema diverso dalla scheda Stile.
   * Se il modello selezionato non specifica un tema, è possibile utilizzare la scheda Stile per sceglierne uno. Il pulsante **[!UICONTROL Crea]** viene abilitato solo dopo la selezione di un tema.

1. (Facoltativo) Nella scheda **[!UICONTROL Dati]**, seleziona un modello dati:

   * **Modello dati modulo**: un [Modello di dati modulo](data-integration.md) consente di integrare entità e servizi da diverse origini dati a un modulo adattivo. Scegli Modello dati modulo (FDM) se il modulo adattivo che stai creando richiede il recupero e la scrittura di dati da e verso più origini dati.

   * **Schema JSON**: lo [schema JSON](adaptive-form-json-schema-form-model.md) rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema di back-end dell’organizzazione. È possibile associare lo schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili per l’utilizzo nella scheda Oggetti modello dati del browser Contenuto durante l’authoring di Forms adattivo. Tutti i campi vengono aggiunti anche al modulo adattivo creato.

   Per impostazione predefinita, sono selezionati tutti i campi del modello di dati. Quando crei il modulo adattivo, tutti i campi del modello di dati selezionati vengono convertiti nei corrispondenti componenti del modulo adattivo. La procedura guidata fornisce caselle di controllo perché possano essere selezionati solo i campi da includere nel modulo adattivo.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. Nella scheda **[!UICONTROL Invio]**, seleziona un’azione di invio:

   * Quando selezioni un modello, l’azione di invio specificata in quel modello viene selezionata automaticamente. Dalla scheda Invio puoi selezionare un’azione di invio diversa. La scheda **[!UICONTROL Invio]** mostra tutte le azioni di invio disponibili.

   * Se nel modello selezionato non è specificata un&#39;azione di invio, è possibile utilizzare la scheda **[!UICONTROL Invio]** per selezionarne una.

1. (Facoltativo) Nella scheda Consegna, puoi specificare una data di pubblicazione o di annullamento della pubblicazione per un modulo adattivo.

1. Seleziona **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo che specifica il titolo, il nome e la posizione in cui salvare il modulo adattivo:

   * **[!UICONTROL Titolo]**: specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell’interfaccia utente di [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** specifica il nome del modulo. Nell’archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo nome può contenere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti da un trattino.
   * **[!UICONTROL Percorso:]** specifica la posizione in cui salvare il modulo adattivo. Puoi salvare il modulo adattivo direttamente all’indirizzo `/content/dam/formsanddocuments` o creare una cartella di salvataggio come `/content/dam/formsanddocuments/adaptiveforms`. Assicurati di creare la cartella prima di utilizzarla nel percorso. Il campo **[!UICONTROL Percorso:]** non crea automaticamente una cartella.

1. Seleziona **[!UICONTROL Crea]**. Viene creato un modulo adattivo che viene aperto nell’editor di moduli adattivi. L’editor mostra i contenuti disponibili nel modello. Viene inoltre visualizzata la barra laterale per personalizzare il modulo creato in base alle esigenze.

   In base al tipo di modulo adattivo, gli elementi del modulo presenti nello schema JSON o nel modello dati del modulo (FDM) <!--XFA form template, XML schema or --> associato vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** del **[!UICONTROL Browser contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Select to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Build an adaptive form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, select on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Select **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and select Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
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

Puoi cambiare il modello di modulo per un modulo adattivo (basato su schema JSON o modello dati modulo). Non è possibile passare da un modello di modulo a un altro.

1. Seleziona il modulo adattivo e l&#39;icona **Proprietà**.
1. Apri la scheda **[!UICONTROL Modello modulo]** ed effettua una delle seguenti operazioni.

   * Se il modulo adattivo non dispone di un modello di modulo, è possibile scegliere un altro modello di modulo e di conseguenza selezionare lo schema XML o JSON <!-- a form template, --> o il modello di dati del modulo (FDM).
   * Se il modulo adattivo è basato su un modello di modulo, è possibile scegliere un altro schema XML o JSON <!-- form template, --> o modello dati modulo (FDM) per lo stesso modello di modulo.

1. Seleziona **[!UICONTROL Salva]** per salvare le proprietà.

È inoltre possibile modificare le proprietà del modello di modulo dal generatore di moduli adattivi o dal generatore di modelli di moduli adattivi.

1. Seleziona il componente **[!UICONTROL Contenitore per modulo adattivo (principale)]**.
1. Fai clic sull’icona ![Configura icona](/help/forms/assets/configure-icon.svg) per aprire le **[!UICONTROL proprietà]** del contenitore per modulo adattivo.
1. Seleziona la scheda **[!UICONTROL Modello di dati]** ed effettua una delle seguenti operazioni:

   * Se il modulo adattivo non dispone di un modello di modulo, è possibile scegliere un modello di modulo e di conseguenza selezionare lo schema XML o JSON <!-- a form template, --> o il modello di dati del modulo (FDM).
   * Se il modulo adattivo si basa su un modello di modulo, non è possibile modificarlo. È possibile scegliere un altro schema XML o JSON <!-- form template, --> o modello dati modulo (FDM) per lo stesso modello di modulo applicabile.
1. Seleziona ![Salva](/help/forms/assets/check-button.png) per salvare le proprietà.

![Supporto schema FDM](/help/forms/assets/fdmsupport.png)

>[!NOTE]
>
> È inoltre possibile salvare un modulo adattivo come modello. Per ulteriori informazioni, consulta [Creare un modello utilizzando un modulo adattivo](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).

## Come rinominare un modulo adattivo AEM? {#rename-an-AEM-Adaptive-Form}

Per rinominare un modulo adattivo, effettua le seguenti operazioni:

1. Seleziona un modulo adattivo nell’interfaccia utente di AEM Forms.
1. Fai clic su **Proprietà** nella barra superiore.
1. Modifica il nome del modulo nella scheda **Titolo**, come illustrato nell&#39;immagine seguente.
1. Fai clic su **Salva e chiudi**.

![Rinominare un modulo adattivo AEM](/help/forms/assets/change-af-name.png)

## Consulta anche {#see-also}

{{see-also}}
