---
title: Come si genera un documento di record per Adaptive Forms?
description: Scopri come generare un modello per un documento di record (DoR) per i componenti core di Forms adattivi.
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3108'
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

**Modello di base:** Un modello XFA (file XDP) creato in Forms Designer o in un Acrobat Form (AcroForm). [Modello base](#base-template-of-a-document-of-record) viene utilizzato per specificare lo stile e le informazioni di branding per un documento di record. Carica il modello XFA (file XDP) nell’istanza di AEM Forms in precedenza.

**Modulo adattivo:** Modulo adattivo per il quale deve essere generato il documento di record.

## Generare un documento di record basato su XFA {#generate-an-XFA-based-document-of-record}

Carica il modello XFA (file XDP) nella tua istanza di AEM Forms. Per configurare un modulo adattivo in modo che utilizzi il modello XFA (file XDP) come modello per il documento record, effettua le seguenti operazioni:

1. Nell’istanza Autore Experience Manager, fai clic su **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti].**
1. Seleziona un modulo o crea un modulo adattivo e fai clic su **[!UICONTROL Proprietà]**.
1. Nella finestra Proprietà, seleziona **[!UICONTROL Modello modulo]**.
1. Il giorno  **[!UICONTROL Modello modulo]** , nella scheda **[!UICONTROL Seleziona da]** a discesa, seleziona **[!UICONTROL Modello dati modulo]**, **[!UICONTROL Schema]** o **[!UICONTROL Nessuno]**. È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.
1. Nella sezione Configurazione modello del documento record della scheda Modello modulo, seleziona **Associa modello modulo come modello del documento record**. Quando si seleziona questa opzione, vengono visualizzati tutti i modelli XFA (file XDP) disponibili sul computer. Selezionare il file appropriato. Inoltre, assicurati che venga utilizzato lo stesso schema (schema dati) per il modulo adattivo e il modello XFA selezionato (file XDP).
1. Clic **[!UICONTROL Fine.]**

Il modulo adattivo è ora configurato per utilizzare un file XDP come modello per il documento di record. Il passaggio successivo consiste nel [associare componenti Modulo adattivo ai campi modello corrispondenti](#bind-adaptive-form-components-with-template-fields).

## Generare un documento di record basato su Acroform {#generate-an-Acroform-based-document-of-record}

Carica Adobe Acrobat PDF (Acroform) nella tua istanza di AEM Forms. Per configurare un modulo adattivo per l’utilizzo di Adobe Acrobat PDF (Acroform) come modello per documento record, effettua le seguenti operazioni:

1. Nell’istanza Autore Experience Manager, fai clic su **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti].**
1. Seleziona un modulo o **[!UICONTROL Creare un modulo adattivo]** e fai clic su **[!UICONTROL Proprietà]**.
1. Nella finestra Proprietà, seleziona **[!UICONTROL Modello modulo]**.
1. Il giorno  **[!UICONTROL Modello modulo]** , nella scheda **[!UICONTROL Seleziona da]** a discesa, seleziona **[!UICONTROL Modello dati modulo]**, **[!UICONTROL Schema]** o **[!UICONTROL Nessuno]**. È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.
1. Nella sezione Configurazione modello del documento record della scheda Modello modulo, seleziona **Associa modello modulo come modello del documento record**. Selezionando questa opzione, vengono visualizzati tutti gli Acrobat PDF (Acroform) disponibili sul computer. Selezionare l&#39;Acroform che si desidera utilizzare.
1. Clic **[!UICONTROL Fine.]**

Il modulo adattivo è ora configurato per utilizzare un Acroform come modello per documento di record. Il passaggio successivo consiste nel [associare componenti Modulo adattivo ai campi modello corrispondenti](#bind-adaptive-form-components-with-template-fields).

## Genera automaticamente un documento di record {#auto-generate-a-document-of-record}

Quando un modulo adattivo è configurato per generare automaticamente un documento di record, ogni volta che un modulo viene modificato, il relativo documento di record viene aggiornato immediatamente. Ad esempio, se un campo viene rimosso da un modulo adattivo esistente, anche il campo corrispondente viene rimosso e non è visibile nel documento di record. Esistono molti altri vantaggi della generazione automatica di documenti di record:

* Gli sviluppatori di moduli non devono mantenere manualmente le associazioni dati. Il documento di record generato automaticamente si occupa degli aggiornamenti relativi all’associazione dei dati.
* Gli sviluppatori di moduli non devono nascondere manualmente i campi contrassegnati come esclusi dal documento di record. Il documento di record generato automaticamente è preconfigurato per escludere tali campi.
* L’opzione Documento di record generato automaticamente consente di risparmiare il tempo necessario per creare un modello di modulo per il documento di record.
* L’opzione Documento di record generato automaticamente consente di utilizzare stili e aspetti diversi utilizzando modelli di base diversi. Consente di selezionare lo stile e l’aspetto migliori per il documento di record per la tua organizzazione. Se non specificate lo stile, gli stili di sistema vengono impostati come predefiniti.
* Il documento di record generato automaticamente garantisce che qualsiasi modifica apportata al modulo venga immediatamente riportata nel documento di record.

Per configurare un modulo adattivo in modo da generare automaticamente un documento di record, effettua le seguenti operazioni:

1. Nell’istanza Autore Experience Manager, fai clic su **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti].**
1. Seleziona un modulo o crea un modulo adattivo e fai clic su **[!UICONTROL Proprietà]**.
1. Nella finestra Proprietà, seleziona **[!UICONTROL Modello modulo]**.
1. Il giorno  **[!UICONTROL Modello modulo]** , nella scheda **[!UICONTROL Seleziona da]** a discesa, seleziona **[!UICONTROL Modello dati modulo]**, **[!UICONTROL Schema]** o **[!UICONTROL Nessuno]**. È inoltre possibile selezionare un modello di modulo durante la creazione di un modulo.
1. Nella sezione Configurazione modello del documento record della scheda Modello modulo, seleziona **Genera documento di record**.
1. Clic **[!UICONTROL Fine.]**

## Associare i componenti del modulo adattivo ai campi modello {#bind-adaptive-form-components-with-template-fields}

Associa campi modulo adattivo a campi modello per visualizzare i dati del modulo acquisiti nel campo del documento di record corrispondente. Per associare i componenti Modulo adattivo ai campi modello del documento record corrispondenti:

1. Apri il modulo adattivo configurato per l’utilizzo di un modello di modulo personalizzato per la modifica.

1. Seleziona un componente Modulo adattivo e fai clic su Apri Configura ![Configura](assets/Smock_Wrench_18_N.svg) icona. Apre il browser delle proprietà.

1. Nel browser delle proprietà, sfoglia e seleziona un campo.

   * (per il modello AcroForm) **[!UICONTROL Campo di riferimento associazione documento di record]** proprietà.
   * (Per il modello XFA) il **[!UICONTROL Riferimento associazione modello dati]** proprietà.

1. Fai clic su **[!UICONTROL Salva]**.

<!-- 
In the following video, Adaptive Form components are bound with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

Puoi utilizzare le azioni di invio, ad esempio &quot;Invia e-mail&quot;, &quot;Richiama un flusso di lavoro AEM&quot;, &quot;Richiama un flusso Power Automate&quot; e altro [Invia azioni](configuring-submit-actions.md) per ricevere un documento di record.
![Azioni invio immagine](/help/forms/assets/submit-actions-img.png)



## Aggiornamenti incrementali al modello del documento record {#document-of-record-template-incremental-updates}

I moduli adattivi e i corrispondenti modelli di documento record possono evolvere nel corso del tempo. Puoi scegliere di aggiungere, rimuovere o modificare campi in un modulo adattivo o in un modello per documento di record.

Quando modifichi un modello di documento record e carichi il modello di documento record modificato in AEM Forms, l’editor di Forms adattivo rileva automaticamente le associazioni modificate e ti informa sui componenti del modulo adattivo che richiedono nuove associazioni. Consente di apportare aggiornamenti incrementali a un modello di documento record.

Ad esempio, un’organizzazione, *We.Retail*, dispone di un modello di documento di record basato su AcroForm, *we-retail-invoc.pdf*. Il modello si presenta come segue:

![Modello originale](assets/we-retail-invoice.png)

Dopo aver utilizzato il modello per un certo periodo di tempo, l’organizzazione decide di rinominarlo `invoice-number` campo a `bill-number` e acquisire l’indirizzo e-mail degli acquirenti. Uno sviluppatore aggiorna il nome del `invoice-number` e aggiunge un campo e-mail al modello. Crea anche una nuova versione del modello denominata  *we-retail-invov2.pdf*.

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
| Testo | Testo |

### Tabelle {#tables}

I componenti della tabella Adaptive Forms, come intestazione, piè di pagina e riga, vengono mappati ai componenti XFA corrispondenti. Puoi mappare i pannelli ripetibili alle tabelle nel documento di record.

## Modello base di un documento record {#base-template-of-a-document-of-record}

Il modello base fornisce informazioni sullo stile e sull&#39;aspetto del documento di record. Consente di personalizzare l’aspetto predefinito del documento di record generato automaticamente. Ad esempio, è possibile utilizzare un modello base per aggiungere il logo della società nell&#39;intestazione e le informazioni sul copyright nel piè di pagina del documento record.

La pagina master di un modello di base viene utilizzata come pagina master per il modello del documento record. La pagina mastro può contenere informazioni quali intestazione di pagina, piè di pagina e numero di pagina che è possibile applicare al documento di record. È possibile applicare tali informazioni al documento record utilizzando il modello base per la generazione automatica del documento record. L&#39;utilizzo di un modello di base consente di modificare le proprietà predefinite dei campi.

Segui sempre [Convenzioni modello base](#base-template-conventions) quando si progetta un modello di base.

## Convenzioni modello base {#base-template-conventions}

Un modello di base viene utilizzato per definire l&#39;intestazione, il piè di pagina, lo stile e l&#39;aspetto di un documento di record. L&#39;intestazione e il piè di pagina possono includere informazioni quali il logo aziendale e il testo del copyright. La prima pagina master del modello di base viene copiata e utilizzata come pagina master per il documento di record, che contiene un&#39;intestazione, un piè di pagina, un numero di pagina o qualsiasi altra informazione da visualizzare in tutte le pagine del documento di record. Se si utilizza un modello di base non conforme alle convenzioni del modello di base, nel modello del documento record viene ancora utilizzata la prima pagina master del modello di base. È consigliabile progettare il modello di base in base alle relative convenzioni e utilizzarlo per la generazione automatica di documenti di record.

**Convenzioni della pagina mastro**

* Nel modello di base, assegna al sottomodulo principale il nome `AF_METATEMPLATE` e la pagina master come `AF_MASTERPAGE`.

* Pagina master con il nome `AF_MASTERPAGE` si trova sotto `AF_METATEMPLATE` la sottomaschera principale è preferibile per l&#39;estrazione di informazioni su intestazione, piè di pagina e stili.

* Se `AF_MASTERPAGE` è assente, viene utilizzata la prima pagina master presente nel modello di base.

**Convenzioni di stile per i campi**

* Per applicare lo stile ai campi del documento record, il modello di base fornisce i campi che si trovano nel `AF_FIELDSSUBFORM` sottometti sotto `AF_METATEMPLATE` sottomodulo principale.

* Le proprietà di questi campi vengono applicate ai campi del documento record. Questi campi devono seguire la `AF_<name of field in all caps>_XFO` convenzione di denominazione. Ad esempio, il nome del campo per la casella di controllo deve essere `AF_CHECKBOX_XFO`.

Per creare un modello di base, eseguire le operazioni seguenti in Forms Designer.

1. Clic **[!UICONTROL File]** > **[!UICONTROL Nuovo]**.
1. Seleziona la **[!UICONTROL In base a un modello]** opzione.

1. Seleziona la **[!UICONTROL Forms - Documento record]** categoria.
1. Seleziona **[!UICONTROL Modello base DoR]**.
1. Clic **[!UICONTROL Successivo]** e fornire le informazioni richieste.

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

1. Seleziona un pannello (pannello principale) nel documento di record, quindi fai clic su ![configura](assets/configure.png).
1. Seleziona ![dortab](assets/dortab.png). Viene visualizzata la scheda Documento record.
1. Seleziona il modello predefinito o un modello personalizzato per il rendering del documento di record. Se selezioni il modello predefinito, sotto il menu a discesa Modello viene visualizzata un’anteprima in miniatura del documento di record.
1. Se si seleziona un modello predefinito o personalizzato, nella scheda Documento record verranno visualizzate alcune delle seguenti proprietà o tutte le proprietà. Specificate le seguenti proprietà per definire l&#39;aspetto del documento record:

   1. **Proprietà di base**:
      * **Modello**: se desideri selezionare un modello personalizzato, sfoglia e seleziona un XDP sul tuo [!DNL AEM Forms] server. Se desideri utilizzare un modello non disponibile nel [!DNL AEM Forms] server, devi prima caricare XDP nel tuo [!DNL AEM Forms] server.
      * **Colore accento**: colore in cui vengono riprodotti il testo dell’intestazione e le righe del separatore nel documento di record PDF.
      * **Famiglia font**: famiglia di caratteri del testo nel Document of Record PDF.

      * **Includi oggetti modulo non associati al modello dati**: l’impostazione della proprietà include i campi non associati dal modulo adattivo basato su schema nel documento di record.

      <!-- **Exclude hidden fields from the Document of Record**: Setting the property identifies the hidden fields for exclusion from Document of Record.-->

      * **Nascondi descrizione pannelli**: quando si imposta la proprietà, la descrizione del pannello o della tabella viene esclusa dal documento di record. Applicabile per il pannello e la tabella.



   1. **Proprietà campo modulo**:
      * **Per i componenti Casella di controllo e Pulsante di opzione, mostra solo i valori selezionati**: impostando la proprietà vengono visualizzati solo i valori selezionati delle caselle di controllo e dei pulsanti di scelta in [!UICONTROL Documento record].
      * **Separatore per più valori**: per visualizzare più valori, puoi scegliere qualsiasi separatore, ad esempio virgola o interruzione di riga.
      * **Allineamento opzioni**: puoi selezionare l’allineamento desiderato (Orizzontale, Verticale, Come modulo adattivo) per impostare l’allineamento dei campi, ad esempio la casella di controllo o il pulsante di opzione da visualizzare [!UICONTROL Documento record]. Per impostazione predefinita, l’allineamento verticale è impostato per i campi in [!UICONTROL Documento record]. Impostazione delle proprietà da [!UICONTROL Proprietà campo modulo] di DoR sovrascrive le proprietà impostate in [!UICONTROL Allineamento elemento] per i campi di un modulo adattivo. Nel caso, seleziona [!UICONTROL Come modulo adattivo] , l’allineamento configurato in un’istanza di authoring di moduli adattivi viene utilizzato per [!UICONTROL Documento record] campi.
      * **Numero di opzioni per l&#39;allineamento orizzontale**: è possibile impostare il numero di opzioni da visualizzare nel documento di record per l’allineamento orizzontale.



   1. **Proprietà pagina mastro**:
      * **Immagine logo**: puoi scegliere di utilizzare l’immagine del logo dal modulo adattivo, sceglierne una da DAM o caricarne una dal computer.
      * **Titolo modulo**: titolo del documento record.
      * **Testo intestazione**: testo che viene visualizzato nella sezione dell’intestazione del documento record.
      * **Etichetta liberatoria**: etichetta della liberatoria.
      * **Esclusione di responsabilità**: testo che specifica la portata dei diritti e degli obblighi sul documento record.
      * **Testo liberatoria**: testo della liberatoria.

      ![Proprietà pagina mastro](/help/forms/assets/dorpropertiesimg.png)

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

1. Per salvare le modifiche di branding, seleziona **[!UICONTROL Fine]**.



## Layout di tabella e colonna per i pannelli nel documento record {#table-and-column-layouts-for-panels-in-document-of-record}

Il modulo adattivo potrebbe essere lungo e contenere diversi campi modulo. Potrebbe non essere necessario salvare un documento record come copia esatta del modulo adattivo. Ora puoi scegliere un layout di tabella o colonna per salvare uno o più pannelli Modulo adattivo in Document of Record PDF.

Prima di generare un documento di record, nelle impostazioni di un pannello, seleziona Layout per il documento di record del pannello come Tabella o Colonna. I campi nel pannello vengono organizzati di conseguenza nel documento di record.

![Campi in un pannello di cui è stato eseguito il rendering in un layout di tabella nel documento record](assets/dortablelayout.png)

Campi in un pannello di cui è stato eseguito il rendering in un layout di tabella nel documento record

![Campi in un pannello di cui è stato eseguito il rendering in un layout di colonna nel documento record](assets/dorcolumnlayout.png)

Campi in un pannello di cui è stato eseguito il rendering in un layout di colonna nel documento record

## Impostazioni del documento record {#document-of-record-settings}

Le impostazioni del documento record consentono di scegliere le opzioni da includere nel documento record. Ad esempio, una banca accetta in un modulo nome, età, numero di previdenza sociale e numero di telefono. Il modulo genera un numero di conto bancario e i dettagli della filiale. È possibile scegliere di visualizzare solo il nome, il numero di previdenza sociale, il conto bancario e i dettagli della filiale nel documento record.

L’impostazione del componente Documento di record è disponibile nelle relative proprietà. Per accedere alle proprietà di un componente, selezionalo e fai clic su ![cmppr](assets/cmppr.png) nella sovrapposizione. Le proprietà sono elencate nella barra laterale e le impostazioni seguenti sono disponibili.

**Impostazioni a livello di campo**

* **Escludi da documento record**: impostando la proprietà su true il campo viene escluso dal documento di record. Questa è una proprietà che supporta lo script denominata `excludeFromDoR`. Il suo comportamento dipende da **Escludi campi dal DoR se nascosto** proprietà a livello di modulo.

* **Visualizza pannello come tabella:** Se si imposta la proprietà, il pannello viene visualizzato come tabella nel documento di record se il pannello contiene meno di 6 campi. Applicabile solo al pannello.
* **Escludi titolo da documento record:** L’impostazione della proprietà esclude il titolo del pannello o della tabella dal documento di record. Applicabile solo al pannello e alla tabella.
* **Escludi descrizione da documento record:** L’impostazione della proprietà esclude la descrizione del pannello o della tabella dal documento di record. Applicabile solo al pannello e alla tabella.

**Impostazioni livello modulo**

* **Includi campi non associati nel DoR:** L’impostazione della proprietà include campi non associati dal modulo adattivo basato su schema nel documento di record. Per impostazione predefinita è true.

## Consulta anche {#see-also}

{{see-also}}


<!-- 

**Exclude fields from DoR if hidden:** Set the property to exclude the hidden fields from Document of Record at form submission. When you enable [Revalidate on server](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), the server recomputes the hidden fields before excluding those fields from the Document of Record.

!->>
