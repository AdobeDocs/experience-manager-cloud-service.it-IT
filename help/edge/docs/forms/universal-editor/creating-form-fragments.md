---
title: Come creare frammenti di modulo per l’authoring basato su WYSIWYG
description: Scopri come creare frammenti di modulo nell’editor universale e aggiungerli ai moduli.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: ht
source-wordcount: '1401'
ht-degree: 100%

---

# Creazione di frammenti di modulo nell’editor universale

<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail con il nome dell’organizzazione e il nome dell’archivio GitHub dall’indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

<span class="preview">Si tratta di una funzione pre-release accessibile tramite il [canale pre-release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features). </span>

I moduli includono spesso sezioni comuni come informazioni di contatto, dettagli di identificazione o accordi di consenso. Gli sviluppatori di moduli creano queste sezioni ogni volta che realizzano un nuovo modulo e si trovano quindi a dover eseguire operazioni lunghe e ripetitive.
Per eliminare operazioni duplicate, l’editor universale consente di creare una sola volta segmenti di modulo riutilizzabili, ad esempio pannelli o gruppi di campi, e di applicarli a vari moduli. Questi segmenti riutilizzabili, modulari e autonomi sono denominati frammenti di modulo. Lo stesso frammento del contatto di emergenza, ad esempio, può essere utilizzato in diverse sezioni di un modulo, ad esempio nei dettagli di contatto del dipendente e del supervisore.

Alla fine dell’articolo avrai appreso come creare e utilizzare frammenti nei moduli mediante l’editor universale.

## Caratteristiche dei frammenti di modulo di Edge Delivery Services

* **Mantenimento della coerenza a livello di frammenti di modulo**
Puoi integrare i frammenti in moduli diversi per mantenere layout coerenti e contenuti standardizzati.

  >[!NOTE]
  >
  > Con l’approccio “cambia una volta, rifletti ovunque”, qualsiasi aggiornamento effettuato su un frammento si applica automaticamente a tutti i moduli in modalità Anteprima. Tuttavia, in modalità Pubblicazione, devi pubblicare il frammento o ripubblicare il modulo affinché le modifiche si riflettano.

* **Possibilità di aggiungere più volte frammenti di modulo all’interno di un modulo**
Puoi aggiungere più volte un frammento di modulo all’interno di un modulo e configurarne le proprietà di associazione dei dati a schemi o origini di dati.

* **Utilizzo di frammenti all’interno di frammenti**
Puoi creare frammenti di modulo nidificati, ovvero puoi aggiungere un frammento in un altro frammento e creare così una struttura di frammenti nidificata.

  >[!NOTE]
  >
  > Non puoi invece nidificare un frammento all’interno di se stesso, poiché questa operazione può determinare riferimenti ricorrenti e comportamenti non desiderati, con conseguenti errori o problemi di rendering.

## Considerazioni durante l’utilizzo dei frammenti di modulo di Edge Delivery Services

* Devi aggiungere lo stesso URL GitHub sia nel frammento sia nel modulo in cui intendi utilizzare il frammento.
* Non puoi modificare un frammento di modulo all’interno di un modulo. Per apportare modifiche, modifica il frammento di modulo indipendente.

## Prerequisiti

* [Configura l’archivio GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) per stabilire una connessione tra l’ambiente AEM e l’archivio GitHub.
* Se utilizzi già Edge Delivery Services, aggiungi la versione più recente del [Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) all’archivio GitHub.
* L’istanza di authoring di AEM Forms include un modello basato su Edge Delivery Services.
* Tieni a portata di mano l’URL dell’istanza di authoring di AEM Forms as a Cloud Service e dell’archivio GitHub.

## Utilizzo dei frammenti di modulo di Edge Delivery Services

Puoi creare frammenti di modulo di Edge Delivery Services nell’editor universale e aggiungere i frammenti creati a moduli di Edge Delivery Services. Con i frammenti di modulo di Edge Delivery Services puoi creare le azioni elencate di seguito:

* [Creazione di frammenti di modulo](#creating-form-fragments)
* [Aggiunta di frammenti di modulo a un modulo](#adding-form-fragments-to-a-form)
* [Gestione dei frammenti di modulo](#managing-form-fragments)

### Creazione di frammenti di modulo

Per creare un frammento di modulo nell’editor universale, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Fai clic su **Crea > Frammento di modulo adattivo**.

   ![Crea frammento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Viene visualizzata la procedura guidata **Crea frammento di modulo adattivo**.
1. Seleziona il modello basato su Egde Delivery Services dalla scheda **Seleziona modello** e fai clic su **[!UICONTROL Avanti]**.
   ![Seleziona modello di Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Inserisci un titolo, un nome, una descrizione e i tag relativi al frammento. Assicurati di specificare un nome univoco per il frammento. Se esiste un altro frammento con lo stesso nome, il frammento non viene creato.
1. Specifica l’**URL di GitHub**. Se, ad esempio, l’archivio GitHub è denominato `edsforms` e nell’account `wkndforms`, l’URL è `https://github.com/wkndforms/edsforms`.

   ![proprietà di base](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Facoltativo) Fai clic per aprire la scheda **Modello modulo** e dal menu a discesa **Seleziona da** seleziona uno dei seguenti modelli per il frammento:

   ![Mostra il tipo di modello nella scheda Modello modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **Modello dati modulo (FDM)**: integra nel frammento oggetti e servizi del modello dati provenienti dalle origini dati. Se il modulo richiede la lettura e la scrittura di dati da più origini, scegli Modello dati modulo (FDM).

   * **Schema JSON**: integra il modulo con un sistema back-end associando uno schema JSON che definisce la struttura dei dati. Consente di aggiungere contenuti dinamici utilizzando gli elementi dello schema.
   * **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

   >[!NOTE]
   >
   > Per informazioni su come integrare moduli o frammenti con un modello dati modulo (FDM) nell’editor universale per utilizzare diverse origini dati di back-end, [fai clic qui](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Facoltativo) Specifica la **Data pubblicazione** o la **Data annullamento pubblicazione** per il frammento nella scheda **Avanzate**.

   ![Scheda Avanzate](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Fai clic su **Crea** per visualizzare una procedura guidata.

   ![Modifica frammento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Facendo clic su **Modifica** viene aperto il frammento creato con un modello predefinito nell’editor universale per l’authoring.

   ![Frammento nell’editor universale per l’authoring](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   In modalità di modifica, puoi aggiungere al frammento qualsiasi componente del modulo. Per informazioni su come creare un frammento nell’editor universale, consulta l’articolo [Guida introduttiva a Edge Delivery Services per AEM Forms utilizzando l’editor universale (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

   Nella schermata seguente viene visualizzato il `contact fragment` creato nell’editor universale.

   ![Schermata di un frammento di modulo dei dettagli di contatto completato nell’editor universale, con campi per nome, telefono, e-mail e indirizzo che possono essere riutilizzati in più moduli](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   Dopo aver creato il frammento, puoi [aggiungere il frammento creato nei moduli di Edge Delivery Services](#adding-form-fragments-in-forms).

### Aggiunta di frammenti di modulo a un modulo

Ora verrà creato un modulo `Employee Details` semplice che include informazioni sia sul dipendente sia sul supervisore. È possibile utilizzare il frammento `Contact Details` sia nel pannello del dipendente che in quello del supervisore. Per utilizzare il frammento di modulo nel modulo, esegui i seguenti passaggi:

1. Apri il passaggio in modalità di modifica.
1. Aggiungi il componente Frammento modulo al modulo.
1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.
1. Passa alla sezione in cui desideri aggiungere un frammento. Ad esempio, passa al pannello **Dettagli dipendente**.

   ![Accedi alla sezione](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi il componente **[!UICONTROL Frammento modulo]** dall’elenco **Componenti modulo adattivo**.
   ![Aggiungi frammento modulo](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Quando selezioni il componente **[!UICONTROL Frammento modulo]**, il frammento viene aggiunto al modulo. Puoi configurare le proprietà del frammento aggiunto aprendo le relative **proprietà**. Ad esempio, nascondere il titolo del frammento dalle relative **Proprietà**.

   ![Configurazione delle proprietà del frammento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Seleziona il **Riferimento frammento** nella scheda **Base**. Vengono visualizzati tutti i frammenti disponibili per il modulo, a seconda del modello del modulo.

   Ad esempio, passa a `/content/forms/af` e seleziona il frammento `Contact Details`.

   ![Seleziona frammento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Fai clic su **[!UICONTROL Seleziona]**.

   Il frammento di modulo viene aggiunto facendo riferimento al modulo e rimane sincronizzato con il frammento di modulo indipendente.

   ![Schermata che mostra il frammento dei dettagli di contatto integrato correttamente in un modulo dipendente all’interno dell’editor universale, in cui viene illustrato come i frammenti mantengono la propria struttura quando vengono riutilizzati](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   È possibile visualizzare in anteprima il modulo per visualizzarne l’aspetto nella modalità **Anteprima**.

   ![Anteprima](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Analogamente, è possibile ripetere i passaggi da 3 a 7 per inserire il frammento `Contact Details` nel pannello `Supervisor Details`.

   ![Modulo dettagli dipendente](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### Gestione dei frammenti di modulo

Puoi eseguire diverse operazioni sui frammenti di modulo utilizzando l’interfaccia utente di AEM Forms.

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

1. Selezionando un frammento di modulo, nella barra degli strumenti vengono visualizzate le seguenti operazioni che è possibile eseguire sul frammento selezionato.

   ![Gestione frammento](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
    </tr>
    <tr>
   <td><p>Modifica</p> </td>
   <td><p>Apre il frammento di modulo in modalità di modifica.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Proprietà</p> </td>
   <td><p>Fornisce opzioni per modificare le proprietà del frammento di modulo.<br /> <br /> </p> </td>
    </tr>
    <td><p>Copia</p> </td>
   <td><p> Fornisce opzioni per copiare il frammento di modulo e incollarlo nella posizione desiderata. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il frammento come HTML o per eseguire un’anteprima personalizzata unendo i dati di un file XML con il frammento. <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Avvia/Gestisci revisione</p> </td>
   <td><p>Consente di avviare e gestire una revisione del frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>Pubblica/Annulla pubblicazione</p> </td>
   <td><p>Pubblica o annulla la pubblicazione del frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Elimina</p> </td>
   <td><p>Elimina il frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Confronta</p> </td>
   <td><p>Confronta due diversi frammenti di modulo a scopo di anteprima.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## Best practice

* Assicurati che il nome del frammento sia univoco. Il frammento non viene creato se è presente un frammento con lo stesso nome.
* Qualsiasi espressione, script o stile in un frammento di modulo autonomo viene mantenuto quando viene inserito tramite riferimento o incorporato in un modulo.
* Quando pubblichi un modulo, i frammenti del modulo inseriti tramite riferimento all’interno del modulo vengono pubblicati automaticamente.

## Consulta anche

{{universal-editor-see-also}}
