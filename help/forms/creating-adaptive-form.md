---
title: Come si crea un modulo adattivo?
description: 'Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. Adaptive Forms sono moduli HTML5 reattivi che semplificano la raccolta e l''elaborazione delle informazioni. Scopri come creare un modulo adattivo basato su un modello di dati modulo e su uno schema XML o JSON. '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# Creare un modulo adattivo {#creating-an-adaptive-form}

La funzione Forms adattiva consente di creare moduli coinvolgenti, reattivi, dinamici e adattivi. [!DNL AEM Forms] fornisce un’interfaccia utente intuitiva e componenti pronti all’uso per la creazione e l’utilizzo di Adaptive Forms. È possibile scegliere di creare un modulo adattivo basato su un modello di modulo o schema o senza un modello di modulo. È importante scegliere con attenzione il modello di modulo che non solo si adatta alle proprie esigenze ma estende gli investimenti e le risorse infrastrutturali esistenti. Per creare un modulo adattivo è possibile scegliere tra le seguenti opzioni:

* **Uso di un modello dati modulo**
   [Integrazione dei dati](data-integration.md) consente di integrare entità e servizi da diverse origini dati in a un modello dati modulo da utilizzare per creare Forms adattivo. Scegliere Modello dati modulo se il modulo adattivo che si sta creando prevede il recupero e la scrittura di dati da e verso più origini dati.

   <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. -->

* **Utilizzo di una definizione di schema XML (XSD) o di uno schema JSON**
Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare lo schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema saranno disponibili per l’uso nella scheda Oggetti modello dati del browser Contenuto durante la creazione di Forms adattivo.

* **Uso di un modello di modulo senza o senza**
La funzione per Forms adattivo creata con questa opzione non utilizza alcun modello di modulo. I dati XML generati da tali moduli hanno una struttura piatta con campi e valori corrispondenti.

## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* Un modello di modulo adattivo. Un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Dispone di componenti preformattati contenenti determinate proprietà e struttura del contenuto È possibile [creare un nuovo modello](template-editor.md), importa un modello esistente oppure scarica e importa alcuni modelli [modelli di esempio](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:3f89abe1-0ece-492a-b5af-57c73badad52).
* Un tema Modulo adattivo. Un tema contiene dettagli di stile per i componenti e i pannelli. Gli stili includono proprietà quali colori di sfondo, colori dello stato, trasparenza, allineamento e dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti. È possibile [creare un nuovo tema](themes.md), [importare un tema esistente](import-export-forms-templates.md#uploading-a-theme), oppure scarica e importa alcuni [temi di esempio](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25).
* Aggiungi gli utenti a [!DNL forms-users] per fornire loro le autorizzazioni necessarie per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici dei moduli, vedere [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

## Creare un modulo adattivo {#strong-create-an-adaptive-form-strong}

Per creare un modulo adattivo, effettua le seguenti operazioni.

1. Accesso [!DNL Experience Manager Forms] Istanza di authoring. Può essere un’istanza Cloud o un’istanza di sviluppo locale.

1. Immetti le credenziali nella pagina di accesso di Experience Manager.

   Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Seleziona un modello e tocca **[!UICONTROL Successivo]**.
1. Opzione per **[!UICONTROL Aggiungi proprietà]** appare. Specifica i valori per i seguenti campi di proprietà. I campi Titolo e Nome sono obbligatori:

   * **[!UICONTROL Titolo:]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel [!DNL Experience Manager Forms] interfaccia utente.
   * **[!UICONTROL Nome:]** Specifica il nome del modulo. Nel repository viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. È possibile modificare il valore suggerito. Il campo name può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.
   * **[!UICONTROL Descrizione:]** Specifica le informazioni dettagliate sul modulo.
   * **[!UICONTROL Tag:]** Specifica i tag per identificare in modo univoco il modulo adattivo. I tag consentono di cercare il modulo. Per creare i tag, digitate nuovi nomi di tag nella sezione **[!UICONTROL Tag]** scatola.

1. È possibile creare un modulo adattivo basato su uno dei seguenti modelli di modulo:

   * [Modello dati modulo](#fdm)

   <!--* [XFA form template](#create-an-adaptive-form-based-on-an-xfa-form-template)-->
   * [Schema XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nessuno o senza un modello di modulo

   Puoi configurarli dalla **[!UICONTROL Modello Modulo]** nella scheda **[!UICONTROL Aggiungi proprietà]** pagina. Per impostazione predefinita, il modello di modulo selezionato è **[!UICONTROL Nessuno]**.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

1. Tocca **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo viene aperto per la modifica e visualizza il contenuto disponibile nel modello. Visualizza inoltre la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   In base al tipo di Modulo adattivo, gli elementi modulo presenti nel <!--XFA form template, -->Lo schema XML o lo schema JSON vengono visualizzati nella **[!UICONTROL Oggetti del modello dati]** della scheda **[!UICONTROL Browser dei contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

## Creare un modulo adattivo basato su un modello dati del modulo {#fdm}

[Integrazione dei dati](data-integration.md) consente di integrare più origini dati e di riunire le relative entità e servizi per creare un modello dati modulo. È un&#39;estensione dello schema JSON. È possibile utilizzare un modello dati modulo per creare un modulo adattivo. Le entità o gli oggetti modello dati configurati in un modello dati modulo sono disponibili come oggetti modello dati per la creazione di moduli. Sono associati alle rispettive origini dati e vengono utilizzati per precompilare un modulo e riscrivere i dati inviati alle rispettive origini dati. È inoltre possibile chiamare i servizi configurati in un modello dati modulo utilizzando le regole del modulo adattivo.

Per utilizzare un modello dati modulo per la creazione di un modulo adattivo:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, selezionare **[!UICONTROL Modello dati modulo]** in **[!UICONTROL Seleziona da]** elenco a discesa.

   ![Creare un modulo adattivo](assets/create-af-1-1.png)

1. Tocca per espandere **[!UICONTROL Seleziona modello dati modulo]**. Sono elencati tutti i modelli di dati modulo disponibili.Selezionare un modello dati da.

>[!NOTE]
>
>È inoltre possibile modificare il modello dati del modulo per un modulo adattivo. Per i passaggi dettagliati vedi [Modificare le proprietà del modello di modulo di un modulo adattivo](#edit-form-model).

## Creare un modulo adattivo basato su uno schema XML o JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser del contenuto per la creazione di Forms adattivo. È possibile trascinare gli elementi dello schema per creare il modulo.

Per informazioni su come progettare uno schema XML o JSON per la creazione di Forms adattivo, consulta i documenti seguenti.

* [Creazione di Forms adattivo utilizzando lo schema XML](adaptive-form-xml-schema-form-model.md)
* [Creazione di Forms adattivo utilizzando lo schema JSON](adaptive-form-json-schema-form-model.md)

Effettua le seguenti operazioni per utilizzare lo schema XML o JSON come modello di modulo per un modulo adattivo:

1. Sulla **[!UICONTROL Aggiungi proprietà]** passaggio della pagina di creazione di un modulo adattivo, tocca **[!UICONTROL Modello Modulo]** scheda .
1. Nella scheda Modello di modulo, selezionare **[!UICONTROL Schema]** dal **[!UICONTROL Seleziona da]** campo a discesa.

1. Tocca **[!UICONTROL Seleziona schema]** ed effettuare una delle seguenti operazioni:

   * **[!UICONTROL Carica dal disco]** - Seleziona questa opzione e tocca Carica definizione schema per sfogliare e caricare uno schema XML o uno schema JSON dal file system. Il file di schema caricato si trova con il modulo e non è accessibile ad altri Forms adattivi.
   * **[!UICONTROL Cerca nell’archivio]** - Selezionare questa opzione per selezionare dall&#39;elenco dei file di definizione dello schema disponibili nel repository. Selezionare il file di schema XML o JSON come modello di modulo. Lo schema selezionato è associato al modulo tramite riferimento ed è accessibile per l’uso in altri Forms adattivi.

      Assicurati che il nome del file dello schema JSON termini con **.schema.json**. Ad esempio: mySchema.schema.json
   ![Selezione dello schema XML o JSON](assets/upload-schema.png)
   **Figura:** *Selezione dello schema XML o JSON*

1. (Solo per schema XML) Dopo aver selezionato o caricato uno schema XML, specificare un elemento principale del file XSD selezionato da mappare con il modulo adattivo.

   ![Selezione dell&#39;elemento principale XSD](assets/xsd-root-element.png)
   **Figura:** *Selezione dell&#39;elemento principale XSD*

>[!NOTE]
>
>È inoltre possibile modificare lo schema di un modulo adattivo. Per i passaggi dettagliati vedi [Modificare le proprietà del modello di modulo di un modulo adattivo](#edit-form-model).

## Modificare le proprietà del modello di modulo di un modulo adattivo {#edit-form-model}

Gli Forms adattivi vengono creati senza un modello di modulo (utilizzando l’opzione Nessuno per il modello di modulo) o senza un modello di modulo, ad esempio <!-- form template, --> Schema XML, schema JSON o modello dati del modulo. È possibile cambiare il modello di modulo per un modulo adattivo da Nessuno a un altro modello di modulo. Per i moduli adattivi basati su un modello di modulo, è possibile scegliere un altro <!-- form template,--> Schema XML, schema JSON o modello dati modulo per lo stesso modello di modulo. Tuttavia, non è possibile passare da un modello di modulo all’altro.

1. Seleziona il modulo adattivo e tocca il **Proprietà** icona.
1. Apri **[!UICONTROL Modello Modulo]** e effettuare una delle seguenti operazioni.

   * Se il modulo adattivo non dispone di un modello di modulo, è possibile scegliere un altro modello di modulo e quindi selezionare <!-- a form template, --> Schema XML o JSON o modello dati del modulo.
   * Se il modulo adattivo è basato su un modello di modulo, è possibile scegliere un altro modello <!-- form template, --> Schema XML o JSON o Modello dati modulo per lo stesso modello di modulo.

1. Tocca **[!UICONTROL Salva]** per salvare le proprietà.
