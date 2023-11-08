---
title: Come si creano e utilizzano i frammenti di moduli adattivi?
description: Il frammento di modulo è un componente modulare e riutilizzabile di un modulo. Scopri come creare frammenti di modulo e riutilizzarli in più moduli per assemblarli in modo efficiente.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
source-git-commit: cf7c9fc3f254628f2efee2e00ed295e038d17c99
workflow-type: tm+mt
source-wordcount: '2147'
ht-degree: 1%

---


# Creare e utilizzare frammenti di Forms adattivi in un modulo adattivo  {#adaptive-form-fragments}


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Anche se ogni modulo è progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni, ad esempio per fornire dati personali come nome e indirizzo, dettagli sulla famiglia, dettagli sul reddito e così via. Gli sviluppatori di moduli devono creare questi segmenti comuni ogni volta che viene creato un nuovo modulo. L’Adaptive Forms fornisce un comodo meccanismo per creare segmenti di modulo una sola volta, ad esempio un pannello o un gruppo di campi, e riutilizzarli in Adaptive Forms. Questi segmenti riutilizzabili e autonomi sono denominati Frammenti di modulo adattivi.


## Creare un frammento {#create-a-fragment}

Puoi creare un frammento di modulo adattivo da zero o salvare un pannello in un modulo adattivo esistente come frammento.

### Crea frammento da zero {#create-fragment-from-scratch}

1. Accedi a [!DNL AEM Forms] istanza di authoring in https://[*nome host*]:[*porta*]/aem/forms.html.
1. Clic **Crea > Frammento modulo adattivo**.
1. Specifica titolo, nome, descrizione e tag per il frammento.

   >[!NOTE]
   >
   >Assicurati di specificare un nome univoco per il frammento. Se esiste già un altro frammento con lo stesso nome, la creazione del frammento non riesce.

1. Fai clic per aprire **Modello modulo** e dalla scheda **Seleziona da** dal menu a discesa, seleziona uno dei seguenti modelli per il frammento:

   * **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

     >[!NOTE]
     >
     > In Adaptive Forms puoi utilizzare più volte un singolo frammento di modulo (basato su Componenti core) all’interno di un modulo. Supporta sia frammenti di modulo basati su nessuno che basati su schema.

   * **Modello** modulo: specifica di creare il frammento utilizzando un modello XDP caricato in [!DNL AEM Forms]. Selezionare il modello XDP appropriato come modello modulo per il frammento.

   ![Creazione di un modulo adattivo utilizzando il modello di modulo come modello](assets/form-template-model.png)

   Vengono visualizzati anche i sottomoduli contrassegnati come frammenti nel modello di modulo selezionato. Puoi selezionare un modulo secondario per Frammento di modulo adattivo dall’elenco a discesa.

   ![Seleziona sottomoduli dal modello di modulo specificato](assets/fragment-subform.png)

   È inoltre possibile creare un frammento di modulo adattivo utilizzando sottomoduli non contrassegnati come frammenti nel modello di modulo specificando l’espressione SOM per il sottomodulo nella casella a discesa.

   * **Schema XML**: specifica di creare il frammento utilizzando uno schema XML caricato in [!DNL AEM Forms]. Puoi caricare o selezionare dagli schemi XML disponibili come modello di modulo per il frammento.

   ![Creare un frammento di modulo adattivo basato su uno schema XML come modello](assets/xml-schema-model.png)

   Puoi anche creare un frammento di modulo adattivo selezionando dalla casella a discesa un complexType presente nello schema selezionato.

   ![Seleziona un tipo complesso dal modello di schema XML specificato](assets/complex-type.png)

1. Clic **Crea** e quindi fare clic su **Apri** per aprire il frammento, con un modello predefinito, in modalità di modifica.

In modalità di modifica puoi trascinare e rilasciare qualsiasi componente Modulo adattivo dalla barra laterale AEM sul frammento. <!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

Inoltre, se hai selezionato uno schema XML o un modello di modulo XDP come modello di modulo per il frammento, nel Finder contenuto viene visualizzata una nuova scheda che mostra la gerarchia del modello di modulo. Consente di trascinare gli elementi del modello di modulo sul frammento. Gli elementi aggiunti del modello del modulo vengono convertiti in componenti del modulo mantenendo le proprietà originali dell&#39;XDP o XSD associato.

### Salva pannello come frammento {#save-panel-as-a-fragment}

1. Apri un modulo adattivo contenente il pannello da salvare come frammento di modulo adattivo.
1. Nella barra degli strumenti del pannello, fai clic su **[!UICONTROL Salva come frammento]**. Viene visualizzata la finestra di dialogo Salva come frammento (Save As Fragment).

   >[!NOTE]
   >
   >Se il pannello che stai salvando come frammento contiene un pannello figlio, il frammento risultante li includerà.

1. Nella finestra di dialogo Creazione frammento, specifica le seguenti informazioni:

   * **Nome**: nome del frammento. Il valore predefinito è il nome dell’elemento del pannello. È un campo obbligatorio.

     >[!NOTE]
     >
     >Assicurati di specificare un nome univoco per il frammento. Se esiste già un altro frammento con lo stesso nome, la creazione del frammento non riesce.

   * **Titolo**: titolo del frammento. Il valore predefinito è il titolo del pannello.

   * **Descrizione**: descrizione del frammento.

   * **Tag**: assegna i tag ai metadati del frammento.

   * **Percorso di destinazione**: percorso dell’archivio in cui viene salvato il frammento. Se non specifichi un percorso, viene creato un nodo con lo stesso nome del frammento accanto al nodo contenente il modulo adattivo. Il frammento viene salvato in questo nodo.

   * **Modello modulo**: a seconda del modello del modulo adattivo, questo campo mostra il **Schema XML**, **Modello modulo**, o **Nessuno**. È un campo non modificabile.

   * **Elemento principale** modello frammento: appare solo nei Forms adattivi basati su XSD. Specifica la directory principale per il modello di frammento. È possibile scegliere **/** o il tipo complesso XSD dal menu a discesa. Puoi riutilizzare il frammento in un altro modulo adattivo solo se come radice del modello di frammento selezioni il tipo complesso.
Se si sceglie **/** come directory principale del modello di frammento, la struttura XSD completa dalla directory principale è visibile nella scheda Modello dati modulo adattivo. Per un elemento principale del modello di frammento di tipo complesso, nella scheda Modello dati modulo adattivo sono visibili solo i discendenti del tipo complesso selezionato.

   * **Rif XSD**: viene visualizzato solo in Adaptive Forms basato su XSD. Viene visualizzata la posizione dello schema XML.

   * **Rif. XDP**: viene visualizzato solo in Adaptive Forms basato su XDP. Viene visualizzata la posizione del modello di modulo XDP.

   ![save-fragment](assets/save-fragment.png)

   Finestra di dialogo Salva come frammento

1. Fai clic su **OK**.

   Il pannello viene salvato nella posizione specificata o predefinita nell’archivio. Nel modulo adattivo, il pannello viene sostituito da un’istantanea del frammento. Come mostrato di seguito, il pannello Informazioni generali e i relativi pannelli secondari, Informazioni personali e Indirizzo, vengono salvati come frammento.

   Per modificare il frammento, fai clic su **[!UICONTROL Modifica risorsa]** nella barra degli strumenti del pannello. Il frammento viene aperto in una nuova scheda o finestra in modalità di modifica.

   ![Modifica di un frammento](assets/edit-fragment.png)

## Utilizzo dei frammenti {#working-with-fragments}

### Configurare l’aspetto del frammento {#configure-fragment-appearance}

Qualsiasi frammento inserito in Adaptive Forms viene visualizzato come immagine segnaposto. Il segnaposto visualizza titoli contenenti fino a un massimo di dieci pannelli secondari nel frammento. Puoi configurare [!DNL AEM Forms] per mostrare il frammento completo invece dell’immagine segnaposto.

Per visualizzare i frammenti completi nei moduli, effettua le seguenti operazioni:

1. Vai alla pagina di configurazione della console web AEM all’indirizzo https:[*host*]:[*porta*]/system/console/configMgr.

1. Cerca e fai clic su **[!UICONTROL Servizio configurazione modulo adattivo]** per aprirlo in modalità di modifica.
1. Disattiva **[!UICONTROL Abilita segnaposto al posto del frammento]** per mostrare i frammenti completi anziché l’immagine segnaposto.

### Inserire un frammento in un modulo adattivo {#insert-a-fragment-in-an-adaptive-form}

I frammenti di modulo adattivo creati vengono visualizzati nella scheda Frammenti di modulo adattivo del Finder di contenuti AEM. Per inserire un frammento di modulo adattivo in un modulo adattivo:

1. Apri il modulo adattivo, in modalità di modifica, in cui desideri inserire un frammento di modulo adattivo.
1. Clic **Risorse** ![assets-browser](assets/assets-browser.png) nella barra laterale. Nel browser Risorse, seleziona **Frammenti di moduli adattivi** dal menu a discesa.

   È inoltre possibile scegliere di visualizzare tutti i frammenti di modulo adattivi o di filtrare in base al modello di modulo, ovvero Modello di modulo, Schema XML o Base.

1. Trascina un frammento di modulo adattivo sul modulo adattivo.

   >[!NOTE]
   >
   >Il frammento di modulo adattivo non è abilitato per la creazione dall&#39;interno del modulo adattivo. Inoltre, non è possibile utilizzare un frammento basato su XSD in un modulo adattivo basato su JSON e viceversa.

Il frammento di modulo adattivo viene inserito per riferimento nel modulo adattivo ed è sincronizzato con il frammento di modulo adattivo autonomo. Ciò significa che quando si aggiorna il frammento di modulo adattivo, le modifiche si riflettono in tutte le Forms adattive in cui viene utilizzato il frammento.

### Incorporare un frammento in un modulo adattivo {#embed-a-fragment-in-adaptive-form}

Puoi scegliere di incorporare un frammento di modulo adattivo in un modulo adattivo facendo clic su **Incorpora risorsa: &lt;*fragmentName*>** sulla barra degli strumenti del pannello del frammento aggiunto, come illustrato nell’immagine di esempio seguente.

![Incorporare un frammento di modulo in un modulo adattivo](assets/embed-fragment.png)

>[!NOTE]
>
>Il frammento incorporato non è più collegato al frammento autonomo. Puoi modificare i componenti nel frammento incorporato direttamente dal modulo adattivo.

### Utilizzo di frammenti all’interno di frammenti {#using-fragments-within-fragments}

È possibile creare frammenti di moduli adattivi nidificati, ovvero trascinare un frammento all’interno di un altro frammento e creare una struttura di frammenti nidificata.

### Modifica frammenti {#change-fragments}

È possibile sostituire o modificare un frammento di modulo adattivo con un altro frammento utilizzando **Seleziona risorsa frammento** nella finestra di dialogo Modifica componente per il pannello Frammento di modulo adattivo.

### Utilizzo di un frammento di modulo più volte in un modulo adattivo {#using-form-fragment-mutiple-times-in-af}

È possibile utilizzare più volte un frammento di modulo basato su schema in un modulo adattivo per salvare i dati in modo univoco per ogni campo del frammento di modulo. Ad esempio, puoi utilizzare un frammento di modulo indirizzo per raccogliere i dettagli dell’indirizzo per indirizzi permanenti, di comunicazione e di presentazione in un modulo di richiesta di prestito.

![utilizzo di più frammenti in un modulo adattivo](/help/forms/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> Se si utilizzano più volte frammenti di modulo basati su nessuno in un modulo adattivo, si verificherà la sincronizzazione dei dati tra i campi dei frammenti. È possibile utilizzare più volte in un modulo un singolo [frammento di modulo (basato su componenti core)](/help/forms/adaptive-form-fragments-core-components.md) che non sia associato ad alcun modello dati modulo senza problemi di sincronizzazione dei dati.

## Automatico mappatura di frammenti per il binding dei dati {#auto-mapping-of-fragments-for-data-binding}

Quando si crea un frammento di modulo adattivo utilizzando un modello di modulo XFA o un tipo complesso XSD e si trascina il frammento in un modulo adattivo, il frammento XFA o il tipo complesso XSD viene sostituito automaticamente dal frammento di modulo adattivo corrispondente la cui radice del modello di frammento è mappata al frammento XFA o al tipo complesso XSD.

È possibile modificare il risorsa del frammento e i relativi binding dalla finestra di dialogo Modifica componente.

>[!NOTE]
>
>Potete inoltre trascinare un frammento di modulo adattivo associato dal libreria Frammento di modulo adattivo in AEM contenuto Finder e fornire il riferimento di binding corretto dalla finestra di dialogo del componente Modifica del pannello Frammento di modulo adattivo.

## Gestire i frammenti {#manage-fragments}

È possibile eseguire diverse operazioni sui frammenti di moduli adattivi utilizzando [!DNL AEM Forms] UI.

1. Passa a `https://[hostname]:'port'/aem/forms.html`.

1. Clic **Seleziona** nel [!DNL AEM Forms] Barra degli strumenti dell’interfaccia utente e seleziona un Frammento di modulo adattivo. La barra degli strumenti mostra le seguenti operazioni che è possibile eseguire sul frammento di modulo adattivo selezionato.

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
   <td><p>Apre il pannello Proprietà. Dal pannello Proprietà puoi visualizzare e modificare le proprietà, generare un’anteprima e caricare un’immagine in miniatura per il frammento selezionato. Per ulteriori informazioni, vedere <a href="manage-form-metadata.md" target="_blank">Gestione dei metadati</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiare</p> </td>
   <td><p>Copia il frammento selezionato. Il pulsante Incolla viene visualizzato nella barra degli strumenti.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il frammento come HTML o come anteprima personalizzata unendo i dati di un file XML con il frammento. <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
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
   <td><p>Eliminare</p> </td>
   <td><p>Elimina il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Localizzazione di frammenti in un modulo adattivo {#localizing-adaptive-form-containing-fragments}

Per localizzare un modulo adattivo che contiene frammenti di modulo adattivo, è necessario localizzare separatamente il frammento e il modulo. L’idea è quella di localizzare un frammento una volta e riutilizzarlo in più Forms adattivi.

>[!NOTE]
>
>Le chiavi di localizzazione nel frammento non verranno visualizzate nel file XLIFF per un modulo adattivo.

## Punti chiave da ricordare quando si lavora con i frammenti {#key-points-to-remember-when-working-with-fragments}

* Assicurati che il nome del frammento sia univoco. Il frammento non viene creato se è presente un frammento con lo stesso nome.
* In un modulo adattivo basato su XDP, se salvi un pannello come frammento che include un altro frammento XDP, il frammento risultante viene associato automaticamente al frammento XDP secondario. Nel caso di un modulo adattivo basato su XSD, il frammento risultante è associato alla directory principale dello schema.
* Quando crei un frammento di modulo adattivo, viene creato un nodo di frammento simile al nodo guideContainer per un modulo adattivo in CRXDe Lite.
* Un frammento in un modulo adattivo che utilizza un modello dati del modulo diverso non è supportato. Ad esempio, un frammento basato su XDP non è supportato in un modulo adattivo basato su XSD e viceversa.
* I Frammenti di moduli adattivi sono disponibili per l’utilizzo tramite la scheda Frammenti di moduli adattivi nel Finder di contenuti AEM.
* Qualsiasi espressione, script o stile in un frammento di modulo adattivo autonomo viene mantenuto quando viene inserito tramite riferimento o incorporato in un modulo adattivo.
* Non è possibile modificare un frammento di modulo adattivo, inserito per riferimento, dall’interno di un modulo adattivo. Per apportare modifiche, puoi modificare il frammento di modulo adattivo autonomo o incorporarlo nel modulo adattivo.
* Quando pubblichi un modulo adattivo, devi pubblicare i frammenti di modulo adattivo autonomi inseriti per riferimento nel modulo adattivo.
* Quando si ripubblica un frammento di modulo adattivo aggiornato, le modifiche si riflettono nelle istanze pubblicate del modulo adattivo in cui viene utilizzato il frammento.
* Il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, non è possibile utilizzare il componente Verifica in un frammento di modulo adattivo.
* (**Solo Mac**) Per garantire che la funzionalità dei frammenti di modulo funzioni perfettamente in tutti gli scenari, aggiungere la seguente voce al file /private/etc/hosts:
  `127.0.0.1 <Host machine>` **Computer host**: il computer Mac di Apple su cui [!DNL AEM Forms] è implementato.

<!--
## Reference Fragments {#reference-fragments}

Reference Adaptive Form Fragments that you can use to create your form are available. For more information, see [Reference Fragments](reference-adaptive-form-fragments.md).
-->

>[!MORELIKETHIS]
>
>* [Frammenti di moduli adattivi nei componenti core](/help/forms/adaptive-form-fragments-core-components.md)
