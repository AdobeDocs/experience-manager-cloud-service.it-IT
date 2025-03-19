---
title: Creare frammenti di modulo per l’authoring basato su WYSIWYG
description: Scopri come creare frammenti di modulo nell’Editor universale e aggiungerli ai moduli.
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 62c58ceb2d2d659bad591b3eba1bfd924f2a848b
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 7%

---


# Creazione e utilizzo di frammenti di Edge Delivery Services Form nell’editor universale

Forms spesso include sezioni comuni come informazioni di contatto, dettagli di identificazione o accordi di consenso. Gli sviluppatori di moduli creano queste sezioni ogni volta che creano un nuovo modulo, operazione ripetitiva e dispendiosa in termini di tempo.
Per eliminare questa duplicazione, Universal Editor consente di creare segmenti di modulo riutilizzabili, ad esempio pannelli o gruppi di campi, una sola volta e di riutilizzarli in vari moduli. Questi segmenti riutilizzabili, modulari e autonomi sono denominati frammenti di modulo. Ad esempio, lo stesso frammento di contatto di emergenza può essere utilizzato in diverse sezioni di un modulo, ad esempio per i dettagli di contatto del dipendente e del supervisore.

Alla fine dell&#39;articolo verrà illustrato come creare e utilizzare frammenti nei moduli mediante l&#39;Editor universale.

## Caratteristiche dei frammenti di Edge Delivery Services Form

* **Mantenimento della coerenza con i frammenti di modulo**
È possibile integrare i frammenti in moduli diversi, per mantenere layout coerenti e contenuti standardizzati. Con l’approccio &quot;cambia una volta, riflette ovunque&quot;, qualsiasi aggiornamento effettuato su un frammento si applica automaticamente a tutti i moduli.

* **Aggiunta di frammenti di modulo più volte nel modulo**
È possibile aggiungere più volte un frammento di modulo all’interno di un modulo e configurarne le proprietà di associazione dati a origini dati o schemi.

* **Utilizzo di frammenti all&#39;interno di frammenti**
Puoi creare frammenti di modulo nidificati, il che significa che puoi aggiungere un frammento in un altro frammento e disporre di una struttura di frammenti nidificata.

  >[!NOTE]
  >
  > Non è possibile nidificare un frammento all’interno di se stesso, in quanto ciò può causare riferimenti ricorsivi e comportamenti non desiderati, con conseguenti errori o problemi di rendering.

## Considerazioni durante l’utilizzo dei frammenti di Edge Delivery Services Form

* Devi aggiungere lo stesso URL GitHub sia nel frammento che nel modulo in cui intendi utilizzare il frammento.
* Non è possibile modificare un frammento di modulo, inserito per riferimento, dall’interno di un modulo. Per modificare, modifica il frammento di modulo autonomo.

## Prerequisiti per la creazione di frammenti di Edge Delivery Services Form

* [Configura l&#39;archivio GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) per stabilire una connessione tra l&#39;ambiente AEM e l&#39;archivio GitHub.
* Se utilizzi già Edge Delivery Services, aggiungi la versione più recente del [Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) all’archivio GitHub.
* L’istanza di authoring di AEM Forms include un modello basato su Edge Delivery Services. Assicurati che nel tuo ambiente sia installata la [versione più recente dei Componenti core](https://github.com/adobe/aem-core-forms-components).
* Tieni a portata di mano l’URL dell’istanza di authoring di AEM Forms as a Cloud Service e dell’archivio GitHub.

## Utilizzo dei frammenti di Edge Delivery Services Form

È possibile creare frammenti di Edge Delivery Services Form nell&#39;Editor universale e aggiungere i frammenti creati a Edge Delivery Services Form. È possibile eseguire le azioni seguenti con i frammenti di Edge Delivery Services Form:

* [Creazione di frammenti di modulo](#creating-form-fragments)
* [Aggiunta di frammenti di modulo a un modulo](#adding-form-fragments-to-a-form)
* [Gestione dei frammenti di modulo](#managing-form-fragments)

### Creazione di frammenti di modulo

Per creare un frammento di modulo nell’Editor universale, effettua le seguenti operazioni:

1. Accedi all’istanza Autore AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Fai clic su **Crea > Frammento modulo adattivo**.

   ![Crea frammento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Viene visualizzata la procedura guidata **Crea frammento di modulo adattivo**.
1. Seleziona il modello basato su Servizi di consegna Edge dalla scheda **Seleziona modello** e fai clic su **[!UICONTROL Avanti]**.
   ![Seleziona modello Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Specifica titolo, nome, descrizione e tag per il frammento. Assicurati di specificare un nome univoco per il frammento. Se esiste un altro frammento con lo stesso nome, la sua creazione non riesce.
1. Specifica l’**URL di GitHub**. Ad esempio, se l&#39;archivio GitHub è denominato `edsforms`, si trova sotto l&#39;account `wkndforms`, l&#39;URL è `https://github.com/wkndforms/edsforms`.

   ![proprietà di base](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Facoltativo) Fai clic per aprire la scheda **Modello modulo** e dal menu a discesa **Seleziona da** seleziona uno dei seguenti modelli per il frammento:

   ![Visualizza il tipo di modello nella scheda Modello modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **Modello dati modulo (FDM)**: integra nel frammento oggetti e servizi del modello dati provenienti da origini dati. Se il modulo richiede la lettura e la scrittura di dati da più origini, scegliere Modello dati modulo.

   * **Schema JSON**: integra il modulo con un sistema back-end associando uno schema JSON che definisce la struttura dati. Consente di aggiungere contenuto dinamico utilizzando gli elementi dello schema.
   * **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

   >[!NOTE]
   >
   > Per informazioni su come integrare moduli o frammenti con un modello dati modulo (FDM) nell&#39;editor universale per utilizzare diverse origini dati di back-end, [fai clic qui](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Facoltativo) Specifica la **Data pubblicazione** o la **Data annullamento pubblicazione** per il frammento nella scheda **Avanzate**.

   ![Scheda Avanzate](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Fai clic su **Crea** per visualizzare una procedura guidata.

   ![Modifica frammento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Fai clic su **Modifica** e il frammento creato con un modello predefinito viene aperto in Universal Editor per l&#39;authoring.

   ![Frammento nell&#39;editor universale per la creazione](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   In modalità di modifica puoi aggiungere al frammento qualsiasi componente del modulo. Per informazioni su come creare un frammento nell&#39;editor universale, fare riferimento all&#39;articolo [Guida introduttiva di Edge Delivery Services per AEM Forms utilizzando l&#39;editor universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

   Nella schermata seguente viene visualizzato `contact fragment` creato in Universal Editor.

   ![Frammento contatto](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   Dopo aver creato il frammento, puoi [aggiungere il frammento creato in Edge Delivery Services Forms](#adding-form-fragments-in-forms).

### Aggiunta di frammenti di modulo a un modulo

Creiamo un semplice modulo `Employee Details` che includa informazioni sia sui dipendenti che sui supervisori. È possibile utilizzare il frammento `Contact Details` sia nei pannelli dipendente che supervisore. Per utilizzare il frammento di modulo nel modulo, effettua le seguenti operazioni:

1. Apri il modulo in modalità di modifica.
1. Aggiungi il componente Frammento modulo al modulo.
1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.
1. Passa alla sezione in cui desideri aggiungere un frammento. Ad esempio, passa al pannello **Dettagli dipendente**.

   ![Passa alla sezione](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Fai clic sull&#39;icona **[!UICONTROL Aggiungi]** e aggiungi il componente **[!UICONTROL Frammento di modulo]** dall&#39;elenco **Componenti modulo adattivo**.
   ![Aggiungi frammento modulo](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Quando selezioni il componente **[!UICONTROL Frammento modulo]**, il frammento viene aggiunto al modulo. Puoi configurare le proprietà del frammento aggiunto aprendo le relative **proprietà**. Ad esempio, nascondi il titolo del frammento dalle relative **Proprietà**.

   ![Configurazione delle proprietà del frammento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Selezionare il **Riferimento frammento** nella scheda **Base**. Vengono visualizzati tutti i frammenti disponibili per il modulo, a seconda del modello del modulo.

   Ad esempio, passa a `/content/forms/af` e seleziona il frammento `Contact Details`.

   ![Seleziona frammento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Fai clic su **[!UICONTROL Seleziona]**.

   Il frammento di modulo viene aggiunto facendo riferimento al modulo e rimane sincronizzato con il frammento di modulo autonomo. Ciò implica che qualsiasi modifica apportata al frammento si rifletta su tutte le istanze in cui il frammento è incorporato all’interno dei moduli.

   ![Frammento nel modulo](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   È possibile visualizzare in anteprima il modulo per visualizzarne l&#39;aspetto nella modalità **Anteprima**.

   ![Anteprima](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Analogamente, è possibile ripetere i passaggi da 3 a 7 per inserire il frammento `Contact Details` per il pannello `Supervisor Details`.

   ![Modulo dettagli dipendente](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### Gestione dei frammenti di modulo

Puoi eseguire diverse operazioni sui frammenti di modulo utilizzando l’interfaccia utente di AEM Forms.

1. Accedi all’istanza Autore AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Seleziona un frammento di modulo e nella barra degli strumenti vengono visualizzate le seguenti operazioni che è possibile eseguire sul frammento selezionato.

   ![Gestisci frammento](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

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
    <td><p>Copiare</p> </td>
   <td><p> Fornisce opzioni per copiare il frammento di modulo e incollarlo nella posizione desiderata. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il frammento come HTML o per eseguire un’anteprima personalizzata unendo i dati di un file XML con il frammento. <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Download</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Avvia revisione/Gestisci revisione</p> </td>
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
   <td><p>Confronto</p> </td>
   <td><p>Confronta due diversi frammenti di modulo a scopo di anteprima.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## Best practice

* Assicurati che il nome del frammento sia univoco. Il frammento non viene creato se è presente un frammento con lo stesso nome.
* Qualsiasi espressione, script o stile in un frammento di modulo autonomo viene mantenuto quando viene inserito tramite riferimento o incorporato in un modulo.
* Quando si pubblica un modulo, i frammenti di modulo inseriti per riferimento all’interno del modulo vengono pubblicati automaticamente.

## Consulta anche

{{universal-editor-see-also}}