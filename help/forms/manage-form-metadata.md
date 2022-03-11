---
title: Gestire i metadati
seo-title: Manage [!DNL AEM Forms] metadata
description: I metadati facilitano la classificazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 2%

---

# Aggiungere, rimuovere o modificare i metadati di un modulo adattivo {#manage-form-metadata}

I metadati facilitano la classificazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.

[!DNL AEM Forms], per impostazione predefinita fornisce un set definito di metadati per ciascun tipo di risorsa. Oltre ai metadati predefiniti, puoi aggiungere metadati personalizzati a ciascuno dei tipi di risorse. [!DNL AEM Forms] fornisce inoltre i mezzi giusti per creare, gestire e scambiare in modo efficiente tutti i metadati per i moduli.

<!-- If you're a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you're using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## Metadati in [!DNL AEM Forms] {#metadata-in-aem-forms}

In [!DNL AEM Forms], l’elenco delle proprietà di metadati associate a una risorsa dipende dal suo tipo. Inoltre, se aggiungi una proprietà di metadati personalizzata, questa viene aggiunta a tutte le risorse del tipo in cui sono stati aggiunti i metadati personalizzati.

### Tipi di risorse {#asset-types}

I seguenti tipi di risorse sono supportati in [!DNL AEM Forms]:

* Modelli di modulo (moduli XFA)
* PDF forms
* Documento (PDF piatti)
* Moduli adattivi
* Modello dati Forms
* XFS

#### Elenco completo dei metadati {#extensive-list-of-metadata}

Di seguito è riportato un elenco completo delle proprietà dei metadati supportate in [!DNL AEM Forms]:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome proprietà</strong></td> 
   <td><strong>Tipo risorsa</strong></td> 
   <td><strong>Descrizione</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Titolo</td> 
   <td>Tutto tranne le risorse</td> 
   <td>Visualizza il nome della risorsa.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrizione</td> 
   <td>Tutto tranne le risorse</td> 
   <td>Descrizione della risorsa. L’utente può specificare questo valore.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Tutti i bundle </td> 
   <td><p>Un valore di sola lettura che specifica il tipo di risorsa. Può avere uno dei seguenti valori:</p> 
    <ul> 
     <li>Modello di modulo</li> 
     <li>Modulo PDF, modulo PDF (Acroform) o modulo PDF (Signed)</li> 
     <li>Documento, documento (firmato)</li> 
     <li>Modulo adattivo</li> 
     <li>Modello dati modulo</li>
     <li>Risorsa</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Creato</td> 
   <td>Tutti i bundle </td> 
   <td>Un valore di sola lettura che specifica l’ora di creazione delle risorse.</td> 
  </tr> 
  <tr> 
   <td>Data ultima modifica</td> 
   <td>Tutti i bundle </td> 
   <td>Un valore di sola lettura che specifica l’ora dell’ultima modifica della risorsa.</td> 
  </tr> 
  <tr> 
   <td>Autore</td> 
   <td>Tutto tranne le risorse</td> 
   <td><p>Valore di sola lettura calcolato automaticamente in base al tipo di modulo.</p> 
    <ul> 
     <li>PDF/Form template/Document - recuperato dal file binario caricato.</li> 
     <li>Modulo adattivo : accesso utente al momento della creazione del modulo.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Stato</td> 
   <td>Tutto tranne le risorse</td> 
   <td><p> Valore di sola lettura che definisce uno dei seguenti stati di un modulo:</p> 
    <ul> 
     <li>Nessun valore: Se un modulo non è mai stato pubblicato.</li> 
     <li>Pubblicato: Quando viene pubblicato un modulo.</li> 
     <li>Modificato: Quando un modulo è stato modificato dopo essere stato pubblicato una volta.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data ultima pubblicazione</td> 
   <td>Tutto tranne le risorse</td> 
   <td>Valore di sola lettura che specifica l’ora dell’ultima pubblicazione del modulo.</td> 
  </tr> 
  <tr> 
   <td>Ora di attivazione/disattivazione pubblicazione</td> 
   <td>Tutto tranne le risorse</td> 
   <td><p>Data e ora in cui è pianificata la pubblicazione automatica o l’annullamento della pubblicazione del modulo. L'utente imposta questo valore sulla modifica dei metadati.</p> 
    <ul> 
     <li>L’ora di attivazione e disattivazione della pubblicazione deve essere successiva alla data corrente. </li> 
     <li>Il tempo di pubblicazione deve essere successivo al tempo di pubblicazione. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Invia URL</td> 
   <td><p>Modello di modulo</p> <p>modulo PDF</p> </td> 
   <td><p>Per configurare un URL specificato dall’utente per l’invio dei dati del modulo a un servlet.</p> <p>L’URL di invio può essere configurato utilizzando uno dei seguenti metodi, elencati in ordine di precedenza:</p> 
    <ul> 
     <li>Durante la creazione di un modulo XFA in AEM Forms Designer, specificare l’URL di invio direttamente in un modello di modulo utilizzando il pulsante Invia per HTTP.</li> 
     <li>Nell’interfaccia utente di AEM Forms, seleziona un modulo e specifica un URL di invio per la modifica delle proprietà dei metadati.</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Profilo di rendering HTML</td> 
   <td>Modello di modulo</td> 
   <td>Profilo di rendering di HTML utilizzato per il rendering di un modello di modulo in formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato di rendering</td> 
   <td><p>Modello di modulo</p> <p>Modulo adattivo</p> </td> 
   <td><p>Questa opzione consente all’utente di specificare il formato di rendering del modulo quando i moduli vengono pubblicati:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Entrambe</li> 
    </ul> <p>Questa opzione viene utilizzata per limitare il formato di rendering dei moduli solo sul portale dei moduli in cui sono visibili all’utente finale.</p> </td> 
  </tr> 
  <tr> 
   <td>Tag</td> 
   <td>Tutto tranne le risorse</td> 
   <td>Etichette associate al modulo per facilitare la ricerca rapida e semplice.</td> 
  </tr> 
  <tr> 
   <td>Riferimenti</td> 
   <td><p>Modulo adattivo</p> <p>Modello di modulo</p> <p>Risorsa</p> </td> 
   <td><p>Elenco delle risorse (altri moduli o risorse) a cui è correlato il modulo. Tali attività possono rientrare in due categorie:</p> 
    <ul> 
     <li>Riferimenti: Risorse a cui fa riferimento il modulo corrente.</li> 
     <li>di cui: Risorse che fanno riferimento alla risorsa corrente.</li> 
    </ul> <p>Queste risorse vengono visualizzate come collegamenti e i relativi metadati sono accessibili direttamente facendo clic su di esse.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Selezione del modello di modulo (XDP/XSD)</td> 
   <td>Modulo adattivo</td> 
   <td><p>Specifica il modello di modulo utilizzato per la creazione del modulo adattivo. Questa proprietà può avere i seguenti valori:</p> 
    <ul> 
      <li>Modello dati modulo </li>
      <li>Schema: Un XML di uno schema JSON</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>Nessuno</li> 
    </ul> 
    <div>
      Una volta selezionato, è possibile aggiornare un modello di modulo ma non rimuoverlo. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizzare i metadati del modulo {#view-form-metadata}

Le risorse dispongono di valori di proprietà esistenti che possono essere visualizzati in modalità di sola lettura. Questi metadati vengono creati al momento del caricamento del modulo o della creazione del modulo.

1. Andate alla posizione della risorsa per la quale desiderate visualizzare i metadati.

1. Apri la pagina delle proprietà utilizzando uno dei seguenti modi:

   * Fai clic sul pulsante **[!UICONTROL Proprietà]** ![Proprietà](assets/Smock_Info_18_N.svg) da Azioni rapide.

      >[!NOTE]
      >
      >Azioni rapide sono gli elementi azione visualizzati sopra una miniatura al passaggio del mouse.

   * Seleziona il modulo e fai clic sul pulsante **[!UICONTROL Proprietà]** ![Proprietà](assets/Smock_Info_18_N.svg) nella barra degli strumenti.
   * Passa alla pagina dei dettagli del modulo facendo clic sulla miniatura del modulo quando non è attiva la modalità di selezione. Ora fai clic sul pulsante ![Proprietà](assets/Smock_Info_18_N.svg) icona occhio in alto a destra, quindi fare clic su Proprietà nell&#39;elenco sottostante.

1. Nella pagina delle proprietà visualizzata viene visualizzato uno schema contenente solo le proprietà dei metadati che contengono un certo valore.

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   La porzione di contenuto è divisa in due parti:

   * Il pannello a sinistra contiene una miniatura del modulo
   * Il pannello a destra contiene le proprietà dei metadati in modalità di sola lettura, distribuite su varie schede.

## Aggiungere/aggiornare i valori dei metadati del modulo {#add-update-form-metadata-values}

È possibile modificare il valore delle proprietà dei metadati esistenti o aggiungere nuovi valori a un campo di proprietà dei metadati esistente (ad esempio, quando un campo di metadati è vuoto).

<!-- ### Update metadata property values {#update-metadata-property-values}

1. Follow the steps mentioned in the previous section to open the properties page where existing metadata of the selected form can be viewed.  

1. From the toolbar, click the Edit icon ![Edit](assets/Smock_Edit_18_N.svg) to change the mode of the page from read-only to read/write.  

1. The properties page that opens holds a schema that contains a mix of editable input fields and static text.  

1. The properties displayed in static text are the ones that you cannot edit.  

1. You can navigate to other tabs to find input fields for metadata properties placed under them.

   This page has a toolbar containing two action icons different from those in view mode:

    * Cancel: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancel any changes made to metadata property values so far
    * Done: ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values so far

   Both these actions direct the user back to read-only mode of the properties page containing the updated values.-->

### Aggiornare la miniatura del modulo {#update-the-form-thumbnail}

Il pannello a sinistra nella pagina delle proprietà visualizza la miniatura del modulo. Per impostazione predefinita, la miniatura visualizzata è quella generata al momento della creazione del modulo (Modulo adattivo) o al momento del caricamento del modulo.

Per tutti i tipi di modulo, puoi caricare un’immagine facendo clic su **[!UICONTROL Carica immagine]** e la ricerca di un file immagine dalla directory locale. L’immagine selezionata viene utilizzata come miniatura invece di quella predefinita.

Per Adaptive Forms, sono disponibili funzionalità aggiuntive che consentono all&#39;utente di generare una miniatura come istantanea dell&#39;anteprima del modulo adattivo corrente. Da [!DNL AEM Forms] supporta anche l’authoring di Adaptive Forms; l’anteprima del Modulo adattivo può cambiare ogni volta che si modifica il Modulo adattivo. Questa funzionalità per generare una miniatura consente di ottenere una nuova miniatura per il modulo adattivo in base allo stato di anteprima corrente. Fai clic su **[!UICONTROL Genera anteprima]** per eseguire questa azione.

>[!NOTE]
>
>* Usa un&#39;immagine quadrata per la miniatura. Quando si utilizza un’immagine non quadrata e si visualizza la miniatura nella vista a elenco, la miniatura appare troncata.
>* Una volta caricata o generata una nuova immagine, la miniatura viene sostituita da questa immagine e non può essere reimpostata sull’immagine precedente.
>


## Aggiungere metadati personalizzati {#add-custom-metadata}

Oltre ai metadati forniti, [!DNL AEM Forms] supporta nuovi metadati personalizzati.

È disponibile uno strumento (Editor schema metadati) per definire lo schema per il layout dei metadati; cioè, il layout di ciò che appare nel **[!UICONTROL Proprietà]** pagina di un modulo. L’Editor schema metadati consente di aggiungere o modificare uno schema personalizzato per le risorse.

[!DNL AEM Forms] espone gli schemi di metadati dei tipi di moduli supportati in questo strumento. In questo modo, puoi accedere a questi schemi e utilizzare la funzionalità fornita nell’editor dello schema dei metadati per aggiungere proprietà personalizzate.

### Navigare nell’editor dello schema metadati {#navigate-the-metadata-schema-editor}

1. Passa a **[!UICONTROL Strumenti > Risorse > Schemi di metadati]**.

1. Fai clic su **[!UICONTROL forms]** dai moduli dello schema elencati.

1. Dall’elenco visualizzato, fai clic sul tipo di risorsa per il quale desideri aggiungere metadati personalizzati.

   >[!NOTE]
   >
   >Questi schemi contengono proprietà di metadati predefinite che non possono essere modificate o modificate (selezionando la casella di controllo e facendo clic su Modifica dalla barra degli strumenti) per evitare problemi di funzionalità.

1. Qualsiasi tipo di risorsa su cui hai fatto clic apre un elenco contenente `extendedmetadata` opzione . Modifica lo schema.

1. Seleziona la casella di controllo accanto a `extendedmetadata` quindi fai clic su Modifica ![Modifica](assets/Smock_Edit_18_N.svg) nella barra degli strumenti.

1. [!DNL AEM Forms] apre l’editor schema metadati/generatore di moduli del tipo di risorsa selezionato (in questo caso Modulo adattivo).

   Editor metadati

   1. Il pannello a sinistra contiene sezioni a schede in cui i campi vengono posizionati e il pannello a destra visualizza tutti i componenti dell’interfaccia utente disponibili e le proprietà del campo selezionato dal pannello a sinistra.

   1. La sezione bloccata non è modificabile e contiene campi per tutte le proprietà dei metadati fornite in modalità predefinita.

   1. Per aggiungere altre schede, fai clic sul simbolo + .

   1. Per aggiungere un campo personalizzato del tipo desiderato, trascina il componente Campo dal **[!UICONTROL Crea modulo]** nella pagina schema.
   1. Le specifiche di questo campo possono essere fornite nel **[!UICONTROL Impostazioni]** dopo aver fatto clic sul campo.

### Aggiungi proprietà metadati personalizzate nell’editor dello schema {#add-custom-metadata-property-in-schema-editor}

1. Passa alla scheda (esistente o nuova) in cui desideri aggiungere la proprietà personalizzata.

1. Trascina un componente del tipo desiderato dal **[!UICONTROL Crea modulo]** sul pannello a sinistra e posizionarsi in una posizione comoda.

   >[!NOTE]
   >
   >Non è possibile spostare le sezioni bloccate, ma è possibile posizionare il componente in uno qualsiasi degli spazi vuoti.

1. Fai clic su un componente appena trascinato. Nella scheda Impostazioni visualizzata nel pannello a destra, compila le informazioni per i campi seguenti:

   1. Specifica un&#39;etichetta campo da utilizzare come nome visualizzato sopra il campo inserito nello schema (ad esempio: Dipartimento)
   1. Nel campo Mappa su proprietà puoi visualizzare un valore precompilato **&quot;./jcr:content/metadata/default&#39;**. Cambia l’**default**&quot; al nome della proprietà desiderato, utilizzato per memorizzare la proprietà nell&#39;archivio crx (ad esempio: &quot;./jcr:content/metadata/dipartimento&#39;)

      >[!NOTE]
      >
      >Non modificare il prefisso ‘./jcr:content/metadata/’ definisce il percorso in cui viene memorizzata la proprietà.
      >
      >Inoltre, il nome della proprietà deve essere univoco per evitare di scrivere valori per due o più proprietà nella stessa posizione nell’archivio. Pertanto, si consiglia di modificare il valore &quot;default&quot;.

   1. Riempire altre impostazioni in base ai requisiti. Ad esempio: seleziona l’opzione Obbligatorio se desideri rendere il campo obbligatorio.
   1. Per eliminare un campo aggiunto, selezionalo e fai clic sul pulsante Elimina ![Elimina](assets/Smock_Delete_18_N.svg) icona.

1. Se necessario, segui i passaggi 1-3 per aggiungere un’altra proprietà.
1. Fai clic su **[!UICONTROL Salva]** dopo aver apportato tutte le modifiche.

   È stata aggiunta correttamente una proprietà di metadati personalizzata.

Tutti i Forms adattivi in [!DNL AEM Forms] ora contiene questa proprietà di metadati aggiuntivi. Puoi modificarlo dalla pagina delle proprietà.
