---
title: Frammenti di moduli adattivi
seo-title: Adaptive Form Fragments
description: Adaptive Forms fornisce un meccanismo per creare un segmento di modulo, ad esempio un pannello o un gruppo di campi, come utilizzato in qualsiasi Modulo adattivo. Puoi anche salvare come frammento un pannello esistente.
seo-description: Adaptive Forms provides a mechanism to create a form segment, such as a panel or a group of fields, as use it in any Adaptive Form. You can also save an existing panel as fragment.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2003'
ht-degree: 1%

---


# Frammenti di moduli adattivi{#adaptive-form-fragments}

Sebbene ogni modulo sia progettato per uno scopo specifico, la maggior parte dei moduli contiene alcuni segmenti comuni, ad esempio per fornire dati personali come nome e indirizzo, dettagli sulla famiglia, dettagli sul reddito e così via. Gli sviluppatori di moduli devono creare questi segmenti comuni ogni volta che viene creato un nuovo modulo.

Adaptive Forms offre un meccanismo conveniente per creare segmenti di modulo una sola volta, come un pannello o un gruppo di campi, e riutilizzarli in Adaptive Forms. Questi segmenti riutilizzabili e autonomi sono denominati Frammenti modulo adattivi.

## Creazione di un frammento {#create-a-fragment}

È possibile creare un frammento di modulo adattivo da zero o salvare un pannello in un modulo adattivo esistente come frammento.

### Crea frammento da zero {#create-fragment-from-scratch}

1. Accedi a [!DNL AEM Forms] istanza dell&#39;autore all&#39;indirizzo https://[*hostname*]:[*porta*]/aem/forms.html.
1. Fai clic su **Crea > Frammento di modulo adattivo**.
1. Specifica titolo, nome, descrizione e tag per il frammento.

   >[!NOTE]
   >
   >Assicurarsi di specificare un nome univoco per il frammento. Se esiste già un altro frammento con lo stesso nome, la creazione del frammento non riesce.

1. Fai clic per aprire **Modello Modulo** e dalla scheda **Seleziona da** menu a discesa, selezionare uno dei seguenti modelli per il frammento:

   * **Nessuno**: Specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.
   * **Modello di modulo**: Specifica la creazione del frammento utilizzando un modello XDP caricato in [!DNL AEM Forms]. Selezionare il modello XDP appropriato come modello di modulo per il frammento.

   ![Creazione di un modulo adattivo utilizzando il modello di modulo come modello](assets/form-template-model.png)

   Vengono visualizzati anche i sottomoduli contrassegnati come frammenti nel modello di modulo selezionato. È possibile selezionare un sottomodulo per Frammento di modulo adattivo dall’elenco a discesa.

   ![Selezionare sottomoduli dal modello di modulo specificato](assets/fragment-subform.png)

   Inoltre, è possibile creare un frammento di modulo adattivo utilizzando sottomoduli non contrassegnati come frammenti nel modello di modulo specificando l’espressione SOM per il sottomodulo nella casella a discesa.

   * **Schema XML**: Specifica la creazione del frammento utilizzando uno schema XML caricato in [!DNL AEM Forms]. È possibile caricare o selezionare dagli schemi XML disponibili come modello di modulo per il frammento.

   ![Creare un frammento di modulo adattivo basato su uno schema XML come modello](assets/xml-schema-model.png)

   Puoi anche creare un frammento di modulo adattivo selezionando un tipo complesso presente nello schema selezionato dalla casella a discesa.

   ![Selezionare un tipo complesso dal modello di schema XML specificato](assets/complex-type.png)

1. Fai clic su **Crea** quindi fai clic su **Apri** per aprire il frammento, con un modello predefinito, in modalità di modifica.

In modalità di modifica, puoi trascinare nel frammento qualsiasi componente Modulo adattivo dalla barra laterale AEM. <!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

Inoltre, se come modello di modulo per il frammento è stato selezionato uno schema XML o un modello di modulo XDP, in Content Finder verrà visualizzata una nuova scheda con la gerarchia del modello di modulo. Consente di trascinare elementi del modello di modulo sul frammento. Gli elementi aggiunti al modello di modulo vengono convertiti in componenti modulo mantenendo le proprietà originali dell&#39;XDP o XSD associato.

### Salva pannello come frammento {#save-panel-as-a-fragment}

1. Aprire un modulo adattivo contenente il pannello che si desidera salvare come frammento di modulo adattivo.
1. Nella barra degli strumenti del pannello, fai clic su **[!UICONTROL Salva come frammento]**. Viene visualizzata la finestra di dialogo Salva con nome frammento.

   >[!NOTE]
   >
   >Se il pannello che si sta salvando come frammento contiene un pannello secondario, il frammento risultante li includerà.

1. Nella finestra di dialogo Creazione frammento specificare le informazioni seguenti:

   * **Nome**: Nome del frammento. Il valore predefinito è il nome dell’elemento del pannello. È un campo obbligatorio.
      >[!NOTE]
      >
      >Assicurarsi di specificare un nome univoco per il frammento. Se esiste già un altro frammento con lo stesso nome, la creazione del frammento non riesce.

   * **Titolo**: Titolo del frammento. Il valore predefinito è il titolo del pannello.

   * **Descrizione**: Descrizione del frammento.

   * **Tag**: Assegna tag ai metadati del frammento.

   * **Percorso di Target**: Percorso archivio in cui verrà salvato il frammento. Se non si specifica un percorso, accanto al nodo contenente il modulo adattivo viene creato un nodo con lo stesso nome del frammento. Il frammento viene salvato in questo nodo.

   * **Modello Modulo**: A seconda del modello di modulo per il modulo adattivo, in questo campo viene visualizzato il campo **Schema XML**, **Modello di modulo** oppure **Nessuno**. Si tratta di un campo non modificabile.

   * **Radice modello frammento**: Viene visualizzato solo in Forms adattivo basato su XSD. Specifica la radice del modello di frammento. Puoi scegliere **/** o il tipo complesso XSD dal menu a discesa. È possibile riutilizzare il frammento in un altro modulo adattivo solo se si seleziona il tipo complesso come radice del modello di frammento.
Se scegli **/** come radice del modello di frammento, la struttura XSD completa dalla radice è visibile nella scheda Modello dati modulo adattivo . Per una directory principale di un modello di frammento di tipo complesso, nella scheda Modello dati modulo adattivo sono visibili solo i discendenti del tipo complesso selezionato.

   * **Rif. XSD**: Viene visualizzato solo in Forms adattivo basato su XSD. Visualizza la posizione dello schema XML.

   * **Rif. XDP**: Viene visualizzato solo in Forms adattivo basato su XDP. Visualizza la posizione del modello di modulo XDP.

   ![save-fragment](assets/save-fragment.png)

   Finestra di dialogo Salva come frammento

1. Fai clic su **OK**.

   Il pannello viene salvato nel percorso specificato o predefinito nella directory archivio. Nel modulo adattivo, il pannello viene sostituito da un’istantanea del frammento. Come illustrato di seguito, il pannello Informazioni generali e i relativi pannelli secondari, Informazioni personali e Indirizzo, vengono salvati come frammento.

   Per modificare il frammento, fai clic su **[!UICONTROL Modifica risorsa]** nella barra degli strumenti del pannello. Il frammento viene aperto in una nuova scheda o finestra in modalità di modifica.

   ![Modifica di un frammento](assets/edit-fragment.png)

## Uso dei frammenti {#working-with-fragments}

### Configurare l’aspetto del frammento {#configure-fragment-appearance}

Qualsiasi frammento inserito in Forms adattivo viene visualizzato come immagine segnaposto. Nel frammento viene visualizzato un massimo di dieci pannelli secondari. Puoi configurare [!DNL AEM Forms] per visualizzare il frammento completo anziché l’immagine segnaposto.

Per visualizzare frammenti completi nei moduli, effettua le seguenti operazioni:

1. Vai AEM pagina di configurazione della console Web all&#39;indirizzo https:[*host*]:[*porta*]/system/console/configMgr.

1. Cerca e fai clic su **[!UICONTROL Servizio di configurazione dei moduli adattivi]** per aprirlo in modalità di modifica.
1. Disattiva **[!UICONTROL Abilita segnaposto al posto del frammento]** per mostrare frammenti completi anziché l’immagine segnaposto.

### Inserire un frammento in un modulo adattivo {#insert-a-fragment-in-an-adaptive-form}

I frammenti di modulo adattivo creati vengono visualizzati nella scheda Frammenti di modulo adattivo del Content Finder di AEM. Per inserire un frammento di modulo adattivo in un modulo adattivo:

1. Apri il modulo adattivo in modalità di modifica in cui desideri inserire un frammento di modulo adattivo.
1. Fai clic su **Risorse** ![browser risorse](assets/assets-browser.png) nella barra laterale. Nel browser Risorse, seleziona **Frammenti modulo adattivi** dal menu a discesa.

   È inoltre possibile scegliere di visualizzare tutti i frammenti di modulo adattivi o di filtrare in base al relativo modello di modulo: Modello di modulo, Schema XML o Base.

1. Trascina un frammento di modulo adattivo nel modulo adattivo.

   >[!NOTE]
   >
   >Il frammento di modulo adattivo non è abilitato per la creazione dall’interno del modulo adattivo. Inoltre, non è possibile utilizzare un frammento basato su XSD in un modulo adattivo basato su JSON e in modo opposto.

Il frammento di modulo adattivo viene inserito tramite riferimento nel modulo adattivo e sincronizzato con il frammento di modulo adattivo autonomo. Ciò significa che quando si aggiorna il frammento di modulo adattivo, le modifiche si riflettono in tutti i Forms adattivi in cui viene utilizzato il frammento.

### Incorporare un frammento nel modulo adattivo {#embed-a-fragment-in-adaptive-form}

Per incorporare un frammento di modulo adattivo in un modulo adattivo, fai clic su **Incorpora risorsa: &lt;*fragmentName*>** nella barra degli strumenti del pannello del frammento aggiunto, come illustrato nell’immagine di esempio seguente.

![Incorporare un frammento di modulo in Modulo adattivo](assets/embed-fragment.png)

>[!NOTE]
>
>Il frammento incorporato non è più collegato al frammento autonomo. Puoi modificare i componenti del frammento incorporato direttamente dal modulo adattivo.

### Uso dei frammenti all’interno dei frammenti {#using-fragments-within-fragments}

È possibile creare frammenti di modulo adattivi nidificati, il che significa che è possibile trascinare un frammento in un altro frammento e disporre di una struttura di frammento nidificata.

### Modificare i frammenti {#change-fragments}

È possibile sostituire o modificare un frammento di modulo adattivo con un altro frammento utilizzando il comando **Seleziona risorsa frammento** nella finestra di dialogo Modifica componente per un pannello Frammento modulo adattivo.

## Mappatura automatica dei frammenti per il binding dei dati {#auto-mapping-of-fragments-for-data-binding}

Quando si crea un frammento di modulo adattivo utilizzando un modello di modulo XFA o un tipo complesso XSD e si trascina il frammento in un modulo adattivo, il frammento XFA o il tipo complesso XSD viene sostituito automaticamente dal corrispondente frammento di modulo adattivo la cui radice del modello di frammento è mappata al frammento XFA o al tipo complesso XSD.

Puoi modificare la risorsa frammento e i relativi binding dalla finestra di dialogo Modifica componente.

>[!NOTE]
>
>È inoltre possibile trascinare un frammento di modulo adattivo associato dalla libreria Frammento di modulo adattivo in AEM Content Finder e fornire il riferimento di binding corretto dalla finestra di dialogo Modifica componente del pannello Frammento di modulo adattivo.

## Gestire i frammenti {#manage-fragments}

È possibile eseguire diverse operazioni sui frammenti di modulo adattivo utilizzando [!DNL AEM Forms] Interfaccia utente.

1. Passa a `https://[hostname]:'port'/aem/forms.html`.

1. Fai clic su **Seleziona** in [!DNL AEM Forms] Barra degli strumenti dell’interfaccia utente e seleziona un frammento di modulo adattivo. Nella barra degli strumenti sono visualizzate le operazioni seguenti che è possibile eseguire sul frammento di modulo adattivo selezionato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Apri</p> </td>
   <td><p>Apre il frammento di modulo adattivo selezionato in modalità di modifica.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Visualizza proprietà</p> </td>
   <td><p>Apre il pannello Proprietà. Dal pannello Proprietà è possibile visualizzare e modificare le proprietà, generare un’anteprima e caricare un’immagine in miniatura per il frammento selezionato. Per ulteriori informazioni, consulta <a href="manage-form-metadata.md" target="_blank">Gestione dei metadati</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copia</p> </td>
   <td><p>Copia il frammento selezionato. Il pulsante Incolla viene visualizzato nella barra degli strumenti.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare un’anteprima del frammento come HTML o come anteprima personalizzata unendo i dati di un file XML con il frammento. <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
  </tr>
  <tr>
   <td><p>Avvia revisione/Gestisci revisione</p> </td>
   <td><p>Consente di avviare e gestire una revisione del frammento selezionato. <!-- For more information, see <a href="create-reviews-forms.md" target="_blank">Creating and managing reviews</a>.<br /> <br /> </p> --> </td>
  </tr>
  <tr>
   <td><p>Crea dizionario</p> </td>
   <td><p>Genera un dizionario per la localizzazione del frammento selezionato. <!-- For more information, see <a href="lazy-loading-adaptive-forms.md" target="_blank">Localizing Adaptive Forms</a>.<br /> <br /> --> </p> </td>
  </tr>
  <tr>
   <td><p>Pubblicare/Annullare la pubblicazione</p> </td>
   <td><p>Pubblica o annulla la pubblicazione del frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Elimina</p> </td>
   <td><p>Elimina il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Localizzazione di moduli adattivi contenenti frammenti {#localizing-adaptive-form-containing-fragments}

Per localizzare un modulo adattivo contenente frammenti di modulo adattivo, è necessario localizzare separatamente il frammento e il modulo. L’idea è quella di localizzare un frammento una volta e riutilizzarlo in più Forms adattivi.

>[!NOTE]
>
>Le chiavi di localizzazione nel frammento non vengono visualizzate nel file XLIFF di un modulo adattivo.

## Punti chiave da ricordare durante l’utilizzo dei frammenti {#key-points-to-remember-when-working-with-fragments}

* Assicurati che il nome del frammento sia univoco. Se esiste un frammento esistente con lo stesso nome, la creazione del frammento non riesce.
* In un modulo adattivo basato su XDP, se salvi un pannello come frammento che include un altro frammento XDP, il frammento risultante verrà automaticamente associato al frammento XDP secondario. Nel caso di un modulo adattivo basato su XSD, il frammento risultante sarà associato alla radice dello schema.
* Quando si crea un frammento di modulo adattivo, viene creato un nodo di frammento, simile al nodo guideContainer per un modulo adattivo, in CRXDe Lite.
* Un frammento in un modulo adattivo che utilizza un modello dati modulo diverso non è supportato. Ad esempio, un frammento basato su XDP non è supportato in un modulo adattivo basato su XSD e viceversa.
* I frammenti di modulo adattivo sono disponibili per l’uso tramite la scheda Frammenti modulo adattivi in Content Finder AEM.
* Qualsiasi espressione, script o stile in un frammento di modulo adattivo autonomo viene mantenuto quando viene inserito tramite riferimento o incorporato in un modulo adattivo.
* Non è possibile modificare un frammento di modulo adattivo, inserito mediante riferimento, dall’interno di un modulo adattivo. Per modificare, è possibile modificare il frammento di modulo adattivo autonomo o incorporarlo nel modulo adattivo.
* Quando si pubblica un modulo adattivo, è necessario pubblicare i frammenti di modulo adattivo autonomi inseriti mediante riferimento nel modulo adattivo.
* Quando si ripubblica un frammento di modulo adattivo aggiornato, le modifiche si riflettono nelle istanze pubblicate del modulo adattivo in cui viene utilizzato il frammento.
* Il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, non è consigliabile utilizzare il componente Verifica in un frammento di modulo adattivo.
* (**Solo Mac**) Per garantire che la funzionalità dei frammenti di modulo funzioni perfettamente in tutti gli scenari, aggiungere la seguente voce al file /private/etc/hosts:
   `127.0.0.1 <Host machine>` **Macchina host**: Il computer Mac Apple su cui [!DNL AEM Forms] viene distribuito.

## Frammenti di riferimento {#reference-fragments}

Sono disponibili i frammenti di modulo adattivi di riferimento utilizzabili per creare il modulo. Per ulteriori informazioni, consulta [Frammenti di riferimento](reference-adaptive-form-fragments.md).
