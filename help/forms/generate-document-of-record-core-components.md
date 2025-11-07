---
title: Come si genera un documento di record per Adaptive Forms?
description: Scopri come generare un modello per un documento di record (DoR) per i componenti core di Forms adattivi.
feature: Adaptive Forms, Core Components
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
role: User, Developer
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '3244'
ht-degree: 1%

---

# Generare documenti di record per Forms adattivo (componenti core)

## Panoramica {#overview}

Quando un modulo viene compilato o inviato, è possibile conservarne una registrazione, in formato cartaceo o in formato documento. Questo record è denominato documento record (DoR). Si tratta di una copia stampabile del modulo inviato. È inoltre possibile fare riferimento al documento record per le informazioni che i clienti hanno compilato in una data successiva oppure utilizzare il documento record per archiviare moduli e contenuti in formato PDF.

![Documento record](assets/document-of-record.png)

Per creare un documento record, un modello basato su XFA o Acroform viene unito ai dati raccolti tramite un modulo adattivo. È possibile generare un documento di record automaticamente o su richiesta. L’opzione on-demand consente di specificare un modello personalizzato basato su XFA o Acroform per fornire un aspetto personalizzato al documento record.

Operazioni disponibili:

* [Generare un documento di record basato su XFA](#generate-an-XFA-based-document-of-record)
* [Generare un documento di record basato su Acroform (Acrobat Form PDF)](#generate-an-Acroform-based-document-of-record)
* [Generazione automatica di un documento di record](#auto-generate-a-document-of-record)

## Prima di iniziare {#components-to-automatically-generate-a-document-of-record}

Prima di iniziare ad apprendere e preparare le risorse necessarie per un documento di record:

**Modello di base:** un modello XFA (file XDP) creato in Forms Designer o in un modulo Acrobat (AcroForm). [Il modello di base](#base-template-of-a-document-of-record) viene utilizzato per specificare le informazioni di stile e branding per un documento di record. Carica il modello XFA (file XDP) nell’istanza di AEM Forms in precedenza.

**Modulo adattivo:** Modulo adattivo per il quale deve essere generato il documento record.

## Generare un documento di record basato su XFA {#generate-an-XFA-based-document-of-record}

Carica il modello XFA (file XDP) nella tua istanza di AEM Forms. Per configurare un modulo adattivo in modo che utilizzi il modello XFA (file XDP) come modello per il documento record, effettua le seguenti operazioni:

1. Nell&#39;istanza di Experience Manager Author, fare clic su **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti].**
1. Selezionare un modulo o creare un modulo adattivo e fare clic su **[!UICONTROL Proprietà]**.
1. Nella finestra Proprietà, selezionare **[!UICONTROL Modello modulo]**.
1. Nella scheda **[!UICONTROL Modello modulo]**, nel menu a discesa **[!UICONTROL Seleziona da]**, selezionare **[!UICONTROL Modello dati modulo]**, **[!UICONTROL Schema]** o **[!UICONTROL Nessuno]**. È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.
1. Nella sezione Configurazione modello del documento record della scheda Modello modulo, selezionare **Associa modello modulo come modello del documento record**. Quando si seleziona questa opzione, vengono visualizzati tutti i modelli XFA (file XDP) disponibili sul computer. Selezionare il file appropriato. Inoltre, assicurati che venga utilizzato lo stesso schema (schema dati) per il modulo adattivo e il modello XFA selezionato (file XDP).
1. Fai clic su **[!UICONTROL Fine]**

Il modulo adattivo è ora configurato per utilizzare un file XDP come modello per il documento di record. Il passaggio successivo consiste nel [associare i componenti del modulo adattivo ai campi modello corrispondenti](#bind-adaptive-form-components-with-template-fields).

## Generare un documento di record basato su Acroform {#generate-an-Acroform-based-document-of-record}

Carica Adobe Acrobat PDF (Acroform) nella tua istanza di AEM Forms. Per configurare un modulo adattivo per l’utilizzo di Adobe Acrobat PDF (Acroform) come modello per documento record, effettua le seguenti operazioni:

1. Nell&#39;istanza di Experience Manager Author, fare clic su **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti].**
1. Seleziona un modulo o **[!UICONTROL Crea un modulo adattivo]** e fai clic su **[!UICONTROL Proprietà]**.
1. Nella finestra Proprietà, selezionare **[!UICONTROL Modello modulo]**.
1. Nella scheda **[!UICONTROL Modello modulo]**, nel menu a discesa **[!UICONTROL Seleziona da]**, selezionare **[!UICONTROL Modello dati modulo]**, **[!UICONTROL Schema]** o **[!UICONTROL Nessuno]**. È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.
1. Nella sezione Configurazione modello del documento record della scheda Modello modulo, selezionare **Associa modello modulo come modello del documento record**. Selezionando questa opzione, vengono visualizzati tutti i PDF di Acrobat (Acroform) disponibili sul computer. Selezionare l&#39;Acroform che si desidera utilizzare.
1. Fai clic su **[!UICONTROL Fine]**

Il modulo adattivo è ora configurato per utilizzare un Acroform come modello per documento di record. Il passaggio successivo consiste nel [associare i componenti del modulo adattivo ai campi modello corrispondenti](#bind-adaptive-form-components-with-template-fields).

## Genera automaticamente un documento di record {#auto-generate-a-document-of-record}

Quando un modulo adattivo è configurato per generare automaticamente un documento di record, ogni volta che un modulo viene modificato, il relativo documento di record viene aggiornato immediatamente. Ad esempio, se un campo viene rimosso da un modulo adattivo esistente, anche il campo corrispondente viene rimosso e non è visibile nel documento di record. Esistono molti altri vantaggi della generazione automatica di documenti di record:

* Gli sviluppatori di moduli non devono mantenere manualmente le associazioni dati. Il documento di record generato automaticamente si occupa degli aggiornamenti relativi all’associazione dei dati.
* Gli sviluppatori di moduli non devono nascondere manualmente i campi contrassegnati come esclusi dal documento di record. Il documento di record generato automaticamente è preconfigurato per escludere tali campi.
* L’opzione Documento di record generato automaticamente consente di risparmiare il tempo necessario per creare un modello di modulo per il documento di record.
* L’opzione Documento di record generato automaticamente consente di utilizzare stili e aspetti diversi utilizzando modelli di base diversi. Consente di selezionare lo stile e l’aspetto migliori per il documento di record per la tua organizzazione. Se non specificate lo stile, gli stili di sistema vengono impostati come predefiniti.
* Il documento di record generato automaticamente garantisce che qualsiasi modifica apportata al modulo venga immediatamente riportata nel documento di record.

Per configurare un modulo adattivo in modo da generare automaticamente un documento di record, effettua le seguenti operazioni:

1. Nell&#39;istanza di Experience Manager Author, fare clic su **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti].**
1. Selezionare un modulo o creare un modulo adattivo e fare clic su **[!UICONTROL Proprietà]**.
1. Nella finestra Proprietà, selezionare **[!UICONTROL Modello modulo]**.
1. Nella scheda **[!UICONTROL Modello modulo]**, nel menu a discesa **[!UICONTROL Seleziona da]**, selezionare **[!UICONTROL Modello dati modulo]**, **[!UICONTROL Schema]** o **[!UICONTROL Nessuno]**. È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.
1. Nella sezione Configurazione modello del documento record della scheda Modello modulo, selezionare **Genera documento record**.
1. Fai clic su **[!UICONTROL Fine]**

## Associare i componenti del modulo adattivo ai campi modello {#bind-adaptive-form-components-with-template-fields}

Associa campi modulo adattivo a campi modello per visualizzare i dati del modulo acquisiti nel campo del documento di record corrispondente. Per associare i componenti Modulo adattivo ai campi modello del documento record corrispondenti:

1. Apri il modulo adattivo configurato per l’utilizzo di un modello di modulo personalizzato per la modifica.

1. Seleziona un componente modulo adattivo e fai clic sull&#39;icona Configura ![Configura](assets/Smock_Wrench_18_N.svg). Apre il browser delle proprietà.

1. Nel browser delle proprietà, sfoglia e seleziona un campo.

   * (Per il modello AcroForm) la proprietà **[!UICONTROL Document of Record Bind Reference field]**.
   * (Per il modello XFA) la proprietà **[!UICONTROL Riferimento associazione modello dati]**.

1. Fai clic su **[!UICONTROL Salva]**.

<!-- 
In the following video, Adaptive Form components are bound with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

Puoi utilizzare le azioni di invio, ad esempio &quot;Invia e-mail&quot;, &quot;Richiama un flusso di lavoro AEM&quot;, &quot;Richiama un flusso Power Automate&quot; e altre [azioni di invio](configuring-submit-actions.md) per ricevere un documento di record.
![Azioni invio immagine](/help/forms/assets/submit-actions-img.png)


>[!NOTE]
>
> È possibile salvare il documento record per qualsiasi modello dati modulo utilizzando la proprietà **[!UICONTROL Riferimento associazione documento di record]**.

## Aggiornamenti incrementali al modello del documento record {#document-of-record-template-incremental-updates}

I moduli adattivi e i corrispondenti modelli di documento record possono evolvere nel corso del tempo. Puoi scegliere di aggiungere, rimuovere o modificare campi in un modulo adattivo o in un modello per documento di record.

Quando modifichi un modello di documento record e carichi il modello di documento record modificato in AEM Forms, l’editor di Forms adattivo rileva automaticamente le associazioni modificate e ti informa sui componenti del modulo adattivo che richiedono nuove associazioni. Consente di apportare aggiornamenti incrementali a un modello di documento record.

Ad esempio, un&#39;organizzazione, *We.Retail*, dispone di un modello di documento di record basato su AcroForm, *we-retail-invoc.pdf*. Il modello si presenta come segue:

![Modello originale](assets/we-retail-invoice.png)

Dopo aver utilizzato il modello per un certo periodo di tempo, l&#39;organizzazione decide di rinominare il campo `invoice-number` nel campo `bill-number` e di acquisire l&#39;indirizzo e-mail degli acquirenti. Uno sviluppatore aggiorna il nome del campo `invoice-number` e aggiunge un campo e-mail al modello. Crea anche una nuova versione del modello denominata *we-retail-invov2.pdf*.

![Modello aggiornato](assets/we-retail-new-invoice.png)

<!--

The developer uploads and applies to the updated template to the adaptive form. The adaptive form automatically detects and displays list of fields where binding has changed.

![Binding Error](assets/we-retail-binding-error.png)

The form developer binds Adaptive Forms fields with corresponding Document of Record template.

-->

>[!VIDEO](assets/we-retail-binding.mp4)

Ora, quando il modulo adattivo viene inviato, viene generato un documento di record aggiornato.

![Aggiornato-](assets/we-retail-new-invoice-sent-to-customer.png)

## Considerazioni chiave durante l’utilizzo del documento record {#key-considerations-when-working-with-document-of-record}

Tieni presenti le seguenti considerazioni e limitazioni durante l’utilizzo del documento di record per Forms adattivo.

* I modelli di documento Record non supportano il formato RTF. Pertanto, qualsiasi testo RTF nel modulo adattivo statico o nelle informazioni compilate dall’utente viene visualizzato come testo normale nel documento di record.
* I frammenti di documento in un modulo adattivo non vengono visualizzati nel documento di record. Tuttavia, sono supportati i frammenti di moduli adattivi.
* L’associazione del contenuto nel documento di record generato per un modulo adattivo basato su schema XML non è supportata.
* La versione localizzata del documento record viene creata su richiesta per una lingua quando l’utente richiede il rendering del documento record. La localizzazione del documento record si verifica insieme alla localizzazione del modulo adattivo. <!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!-- ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration). -->

## Mappatura degli elementi del modulo adattivo {#mapping-of-adaptive-form-elements}

La tabella seguente descrive i componenti Modulo adattivo e i corrispondenti componenti XFA e se compaiono in un documento Record.

### Campi {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente modulo adattivo</th>
   <th>Componente XFA corrispondente</th>
   <th>Incluso per impostazione predefinita nel modello del documento record?</th>
   <th>Note</th>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td>Pulsante</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella di selezione</td>
   <td>Casella di controllo</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td>Campo data/ora</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Elenco a discesa</td>
   <td>Elenco a discesa</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella numerica</td>
   <td>Campo numerico</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td>Pulsante di scelta</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella di testo</td>
   <td>Campo testo</td>
   <td>vero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Pulsante Ripristina</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante Invia</td>
   <td><p>Pulsante Invia e-mail</p> <p>Pulsante invio HTTP</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td> </td>
   <td>false</td>
   <td>Non disponibile nel modello del documento record. Disponibile solo nel documento record tramite allegati.</td>
  </tr>
 </tbody>
</table>

### Contenitori {#containers}

<table>
 <tbody>
  <tr>
   <th>Componente modulo adattivo</th>
   <th>Componente XFA corrispondente</th>
   <th>Note</th>
  </tr>
  <tr>
   <td>Pannello<br /> </td>
   <td>Sottomodulo<br /> </td>
   <td>Il pannello ripetibile viene mappato su una sottomaschera ripetibile.</td>
  </tr>
 </tbody>
</table>

### Componenti statici {#static-components}

| Componente modulo adattivo | Componente XFA corrispondente | Note |
|---|---|---|
| Immagine | Immagine | I componenti TextDraw e Image, sia associati che non associati, vengono sempre visualizzati nel documento di record per un modulo adattivo basato su XSD, a meno che non vengano esclusi utilizzando le impostazioni del documento di record. |
| Testo | Testo |  |

### Tabelle {#tables}

I componenti della tabella Adaptive Forms, come intestazione, piè di pagina e riga, vengono mappati ai componenti XFA corrispondenti. Puoi mappare i pannelli ripetibili alle tabelle nel documento di record.

## Modello base di un documento record {#base-template-of-a-document-of-record}

Il modello base fornisce informazioni sullo stile e sull&#39;aspetto del documento di record. Consente di personalizzare l’aspetto predefinito del documento di record generato automaticamente. Ad esempio, è possibile utilizzare un modello base per aggiungere il logo della società nell&#39;intestazione e le informazioni sul copyright nel piè di pagina del documento record.

La pagina master di un modello di base viene utilizzata come pagina master per il modello del documento record. La pagina mastro può contenere informazioni quali intestazione di pagina, piè di pagina e numero di pagina che è possibile applicare al documento di record. È possibile applicare tali informazioni al documento record utilizzando il modello base per la generazione automatica del documento record. L&#39;utilizzo di un modello di base consente di modificare le proprietà predefinite dei campi.

Segui sempre le [convenzioni del modello base](#base-template-conventions) durante la progettazione del modello base.

## Convenzioni modello base {#base-template-conventions}

Un modello di base viene utilizzato per definire l&#39;intestazione, il piè di pagina, lo stile e l&#39;aspetto di un documento di record. L&#39;intestazione e il piè di pagina possono includere informazioni quali il logo aziendale e il testo del copyright. La prima pagina master del modello di base viene copiata e utilizzata come pagina master per il documento di record, che contiene un&#39;intestazione, un piè di pagina, un numero di pagina o qualsiasi altra informazione da visualizzare in tutte le pagine del documento di record. Se si utilizza un modello di base non conforme alle convenzioni del modello di base, nel modello del documento record viene ancora utilizzata la prima pagina master del modello di base. È consigliabile progettare il modello di base in base alle relative convenzioni e utilizzarlo per la generazione automatica di documenti di record.

**Convenzioni pagina master**

* Nel modello di base, assegnare al sottomodulo principale il nome `AF_METATEMPLATE` e alla pagina master il nome `AF_MASTERPAGE`.

* La pagina master con il nome `AF_MASTERPAGE` che si trova sotto la sottomaschera principale `AF_METATEMPLATE` è preferita per l&#39;estrazione di informazioni su intestazione, piè di pagina e stile.

* Se `AF_MASTERPAGE` è assente, viene utilizzata la prima pagina master presente nel modello di base.

**Convenzioni di stile per i campi**

* Per applicare lo stile ai campi del documento record, il modello base fornisce i campi che si trovano nella sottomaschera `AF_FIELDSSUBFORM` sotto la sottomaschera principale `AF_METATEMPLATE`.

* Le proprietà di questi campi vengono applicate ai campi del documento record. Questi campi devono seguire la convenzione di denominazione `AF_<name of field in all caps>_XFO`. Ad esempio, il nome del campo per la casella di controllo deve essere `AF_CHECKBOX_XFO`.

Per creare un modello di base, eseguire le operazioni seguenti in Forms Designer.

1. Fare clic su **[!UICONTROL File]** > **[!UICONTROL Nuovo]**.
1. Seleziona l&#39;opzione **[!UICONTROL Basato su un modello]**.

1. Selezionare la categoria **[!UICONTROL Forms - Documento di record]**.
1. Selezionare **[!UICONTROL Modello base DoR]**.
1. Fai clic su **[!UICONTROL Avanti]** e fornisci le informazioni richieste.

1. (Facoltativo) Modificare lo stile e l&#39;aspetto dei campi che si desidera applicare ai campi del documento record.
1. Salvare il modulo.
   ![Proprietà di base](/help/forms/assets/form-designer-dor-img.png)

È ora possibile utilizzare il modulo salvato come modello di base per un documento di record. Non modificare o rimuovere gli script presenti nel modello di base.

**Modifica del modello di base**

* Non applicare alcuno stile ai campi nel modello di base. È consigliabile rimuovere tali campi dal modello di base in modo che tutti gli aggiornamenti al modello di base vengano selezionati automaticamente.
* Durante la modifica del modello di base, non rimuovere, aggiungere o modificare gli script.

Segui rigorosamente le convenzioni e le istruzioni di cui sopra per progettare un modello di base.

## Personalizzare le informazioni di branding nel documento record {#customize-the-branding-information-in-document-of-record}

Durante la generazione di un documento record, è possibile modificare le informazioni di branding per il documento record nella scheda Documento record. La scheda Documento record include opzioni quali logo, aspetto, layout, intestazione e piè di pagina, liberatoria e se si desidera includere o meno le opzioni di caselle di controllo e pulsanti di scelta non selezionate.

Per localizzare le informazioni di branding immesse nella scheda Documento record, verificare che le impostazioni internazionali del browser siano impostate in modo appropriato. Per personalizzare le informazioni di branding del documento record, effettuare le seguenti operazioni:

1. Selezionare un pannello (pannello principale) nel documento di record, quindi selezionare ![configura](assets/configure.png).
1. Seleziona ![dortab](assets/dortab.png). Viene visualizzata la scheda Documento record.
1. Seleziona il modello predefinito o un modello personalizzato per il rendering del documento di record. Se selezioni il modello predefinito, sotto il menu a discesa Modello viene visualizzata un’anteprima in miniatura del documento di record.
1. Se si seleziona un modello predefinito o personalizzato, nella scheda Documento record verranno visualizzate alcune delle seguenti proprietà o tutte le proprietà. Specificate le seguenti proprietà per definire l&#39;aspetto del documento record:

   1. **Proprietà di base**:
      * **Modello**: per selezionare un modello personalizzato, sfogliare e selezionare un XDP nel server [!DNL AEM Forms]. Se desideri utilizzare un modello non disponibile sul server [!DNL AEM Forms], devi prima caricare XDP nel server [!DNL AEM Forms].
      * **Colore accento**: il colore con cui vengono riprodotti il testo di intestazione e le linee di separazione nel PDF del documento record.
      * **Famiglia di caratteri**: famiglia di caratteri del testo nel PDF del documento record.

        >[!NOTE]
        >
        > AEM Forms offre una varietà di font incorporati che si integrano facilmente con i file PDF. Per visualizzare l&#39;elenco dei caratteri supportati, [fare clic qui](/help/forms/supported-out-of-the-box-fonts.md).

      * **Includi oggetti modulo non associati al modello dati**: l&#39;impostazione della proprietà include campi non associati del modulo adattivo basato su schema nel documento di record.

        <!-- **Exclude hidden fields from the Document of Record**: Setting the property identifies the hidden fields for exclusion from Document of Record.-->

      * **Nascondi descrizione pannelli**: l&#39;impostazione della proprietà esclude la descrizione del pannello o della tabella dal documento record. Applicabile per il pannello e la tabella.



   1. **Proprietà campo modulo**:

      * **Per i componenti Casella di controllo e Pulsante di opzione, mostrare solo i valori selezionati**: impostando la proprietà verranno visualizzati solo i valori selezionati della casella di controllo e del pulsante di opzione in [!UICONTROL Documento record].
      * **Separatore per più valori**: è possibile scegliere qualsiasi separatore, ad esempio virgola o interruzione di riga, per visualizzare più valori.
      * **Allineamento opzioni**: è possibile selezionare l&#39;allineamento desiderato (Orizzontale, Verticale, Come modulo adattivo) per impostare l&#39;allineamento per i campi, ad esempio la casella di controllo o il pulsante di scelta da visualizzare nel [!UICONTROL Documento record]. Per impostazione predefinita, l&#39;allineamento verticale è impostato per i campi in [!UICONTROL Documento di record]. L&#39;impostazione delle proprietà dalle [!UICONTROL proprietà campo modulo] del DoR sovrascrive le proprietà impostate in [!UICONTROL Allineamento elemento] per i campi di un modulo adattivo. Se si seleziona l&#39;opzione [!UICONTROL Come modulo adattivo], per i campi [!UICONTROL Documento record] viene utilizzato l&#39;allineamento configurato in un&#39;istanza di authoring del modulo adattivo.
      * **Numero di opzioni per l&#39;allineamento orizzontale**:You può impostare il numero di opzioni da visualizzare nel documento di record per l&#39;allineamento orizzontale.



   1. **Proprietà pagina master**:

      * **Immagine logo**: puoi scegliere di utilizzare l&#39;immagine del logo dal modulo adattivo, sceglierne una da DAM o caricarne una dal computer.
      * **Titolo modulo**: titolo del documento record.
      * **Testo intestazione**: testo visualizzato nella sezione dell&#39;intestazione del documento di record.
      * **Etichetta liberatoria**: etichetta della liberatoria.
      * **Dichiarazione di non responsabilità**: testo che specifica l&#39;ambito dei diritti e degli obblighi del documento record.
      * **Testo liberatoria**: testo liberatoria.

      ![Proprietà pagina master](/help/forms/assets/dorpropertiesimg.png)

      >[!NOTE]
      >
      >Se utilizzi un modello di modulo adattivo creato con una versione di Designer precedente alla 6.3, affinché le proprietà Colore accento e Famiglia font funzionino, accertati che nel modello di modulo adattivo nel sottomodulo principale sia presente quanto segue:

      ```xml
      <proto>
      <font typeface="Arial"/>
      <fill>
      <color value="4,166,203"/>
      </fill>
      <edge>
      <color value="4,166,203"/>
      </edge>
      </proto>
      ```

1. Per salvare le modifiche di branding, selezionare **[!UICONTROL Fine]**.

>[!NOTE]
> 
> Per visualizzare il titolo di un modulo personalizzato nel documento record, modifica il **Titolo modulo personalizzato** in **Proprietà documento record** > **Proprietà pagina master**. Questo titolo personalizzato:
> 
> * Viene visualizzato nell’intestazione del PDF generato
> * Viene visualizzato come Titolo nelle proprietà del documento di PDF
> * Appare come titolo della vista iniziale all&#39;apertura del PDF

## Layout di tabella e colonna per i pannelli nel documento record {#table-and-column-layouts-for-panels-in-document-of-record}

Il modulo adattivo potrebbe essere lungo e contenere diversi campi modulo. Potrebbe non essere necessario salvare un documento record come copia esatta del modulo adattivo. Ora puoi scegliere un layout di tabella o colonna per salvare uno o più pannelli Modulo adattivo nel PDF del documento record.

Prima di generare un documento di record, nelle impostazioni di un pannello, seleziona Layout per il documento di record del pannello come Tabella o Colonna. I campi nel pannello vengono organizzati di conseguenza nel documento di record.

![Campi in un pannello sottoposti a rendering in un layout di tabella nel documento di record](assets/dortablelayout.png)

Campi in un pannello di cui è stato eseguito il rendering in un layout di tabella nel documento record

![Campi in un pannello sottoposti a rendering in un layout di colonna nel documento di record](assets/dorcolumnlayout.png)

Campi in un pannello di cui è stato eseguito il rendering in un layout di colonna nel documento record

## Impostazioni del documento record {#document-of-record-settings}

Le impostazioni del documento record consentono di scegliere le opzioni da includere nel documento record. Ad esempio, una banca accetta in un modulo nome, età, numero di previdenza sociale e numero di telefono. Il modulo genera un numero di conto bancario e i dettagli della filiale. È possibile scegliere di visualizzare solo il nome, il numero di previdenza sociale, il conto bancario e i dettagli della filiale nel documento record.

L’impostazione del componente Documento di record è disponibile nelle relative proprietà. Per accedere alle proprietà di un componente, selezionarlo e fare clic su ![cmppr](assets/cmppr.png) nella sovrapposizione. Le proprietà sono elencate nella barra laterale e le impostazioni seguenti sono disponibili.

**Impostazioni a livello di campo**

* **Escludi da documento record**: impostando la proprietà su true il campo viene escluso dal documento record. Si tratta di una proprietà che supporta lo script denominata `excludeFromDoR`. Il suo comportamento dipende da **Escludi campi dal DoR se nascosto** proprietà a livello di modulo.

* **Visualizza il pannello come tabella:** Se la proprietà viene impostata, il pannello viene visualizzato come tabella nel documento di record se il pannello contiene meno di 6 campi. Applicabile solo al pannello.
* **Escludi titolo da documento record:** L&#39;impostazione della proprietà esclude il titolo del pannello o della tabella dal documento record. Applicabile solo al pannello e alla tabella.
* **Escludi descrizione da documento record:** L&#39;impostazione della proprietà esclude la descrizione del pannello o della tabella dal documento record. Applicabile solo al pannello e alla tabella.
* **Escludi campi nascosti dal documento record**: se si seleziona questa proprietà, i campi nascosti verranno esclusi dal documento record. Si applica a tutti i campi modulo. Per impostazione predefinita, l&#39;opzione **Escludi campi nascosti dal documento di record** non è selezionata.

**Impostazioni livello modulo**

* **Includi campi non associati nel DoR:** L&#39;impostazione della proprietà include campi non associati del modulo adattivo basato su schema nel documento di record. Per impostazione predefinita è true.

## Consulta anche {#see-also}

{{see-also}}


<!-- 

**Exclude fields from DoR if hidden:** Set the property to exclude the hidden fields from Document of Record at form submission. When you enable [Revalidate on server](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), the server recomputes the hidden fields before excluding those fields from the Document of Record.

!->>
