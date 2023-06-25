---
title: Gestire i metadati
seo-title: Manage [!DNL AEM Forms] metadata
description: I metadati semplificano la classificazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 2%

---

# Aggiungere, rimuovere o modificare i metadati di un modulo adattivo {#manage-form-metadata}

I metadati semplificano la classificazione e l’organizzazione delle risorse e aiutano gli utenti che cercano una risorsa specifica.

[!DNL AEM Forms]Per impostazione predefinita, fornisce un set definito di metadati per ogni tipo di risorsa. Oltre ai metadati predefiniti, puoi aggiungere metadati personalizzati a ciascun tipo di risorsa. [!DNL AEM Forms] consente inoltre di creare, gestire e scambiare tutti i metadati in modo efficiente per i moduli.

<!-- If you are a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you are using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## Metadati in [!DNL AEM Forms] {#metadata-in-aem-forms}

In entrata [!DNL AEM Forms], l’elenco delle proprietà dei metadati associate a una risorsa dipende dal suo tipo. Inoltre, se aggiungi una proprietà di metadati personalizzata, questa viene aggiunta in tutte le risorse del tipo a cui sono stati aggiunti i metadati personalizzati.

### Tipi di risorse {#asset-types}

I seguenti tipi di risorse sono supportati in [!DNL AEM Forms]:

* Modelli di modulo (moduli XFA)
* PDF forms
* Documento (PDF flat)
* Moduli adattivi
* Modello dati Forms
* XFS

#### Ampio elenco di metadati {#extensive-list-of-metadata}

Di seguito è riportato un elenco completo delle proprietà di metadati supportate in [!DNL AEM Forms]:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome proprietà</strong></td> 
   <td><strong>Tipo risorsa</strong></td> 
   <td><strong>Descrizione</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Titolo</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Nome visualizzato della risorsa.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrizione</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Descrizione della risorsa. L’utente può specificare questo valore.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Tutti i bundle </td> 
   <td><p>Valore di sola lettura che specifica il tipo di risorsa. Può avere uno dei seguenti valori:</p> 
    <ul> 
     <li>Modello di modulo</li> 
     <li>Modulo PDF, Modulo PDF (Acroform) o Modulo PDF (Signed)</li> 
     <li>Documento, Documento (Firmato)</li> 
     <li>Modulo adattivo</li> 
     <li>Modello dati modulo</li>
     <li>Risorsa</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Creato</td> 
   <td>Tutti</td> 
   <td>Valore di sola lettura che specifica l’ora di creazione della risorsa.</td> 
  </tr> 
  <tr> 
   <td>Data ultima modifica</td> 
   <td>Tutti</td> 
   <td>Valore di sola lettura che specifica l’ora dell’ultima modifica apportata alla risorsa.</td> 
  </tr> 
  <tr> 
   <td>Autore</td> 
   <td>Tutto tranne la risorsa</td> 
   <td><p>Valore di sola lettura calcolato automaticamente in base al tipo di modulo.</p> 
    <ul> 
     <li>PDF/Modello modulo/Documento: recuperato dal file binario caricato.</li> 
     <li>Modulo adattivo: utente connesso al momento della creazione del modulo.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Stato</td> 
   <td>Tutto tranne la risorsa</td> 
   <td><p> Valore di sola lettura che definisce uno dei seguenti stati di un modulo:</p> 
    <ul> 
     <li>Nessun valore: se un modulo non è mai stato pubblicato.</li> 
     <li>Pubblicato: quando un modulo viene pubblicato.</li> 
     <li>Modificato: quando un modulo è stato modificato dopo essere stato pubblicato una volta.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data ultima pubblicazione</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Valore di sola lettura che specifica l'ora dell'ultima pubblicazione del modulo.</td> 
  </tr> 
  <tr> 
   <td>Ora di attivazione/disattivazione pubblicazione</td> 
   <td>Tutto tranne la risorsa</td> 
   <td><p>Ora in cui è pianificata la pubblicazione automatica o l'annullamento della pubblicazione del modulo. L’utente imposta questo valore durante la modifica dei metadati.</p> 
    <ul> 
     <li>L'ora di attivazione e disattivazione della pubblicazione deve essere successiva alla data corrente. </li> 
     <li>L'ora di disattivazione della pubblicazione deve essere successiva all'ora di attivazione della pubblicazione. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Invia URL</td> 
   <td><p>Modello di modulo</p> <p>Modulo PDF</p> </td> 
   <td><p>Per configurare un URL specificato dall'utente per l'invio dei dati del modulo a un servlet.</p> <p>L’URL di invio può essere configurato utilizzando uno dei seguenti metodi, elencati in ordine di precedenza:</p> 
    <ul> 
     <li>Specifica un URL di invio direttamente in un modello di modulo utilizzando il pulsante HTTP Invia durante la creazione di un modulo XFA in AEM Forms Designer.</li> 
     <li>Nell’interfaccia utente di AEM Forms, seleziona un modulo e specifica un URL di invio in caso di modifica delle proprietà dei metadati.</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Profilo rendering HTML</td> 
   <td>Modello di modulo</td> 
   <td>Il profilo di rendering HTML utilizzato durante il rendering di un modello di modulo in formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato rendering</td> 
   <td><p>Modello di modulo</p> <p>Modulo adattivo</p> </td> 
   <td><p>Questa opzione consente di specificare il formato di rendering del modulo al momento della pubblicazione dei moduli:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Entrambi</li> 
    </ul> <p>Questa opzione viene utilizzata per limitare il formato di rendering dei moduli solo nel portale dei moduli in cui sono visibili all'utente finale.</p> </td> 
  </tr> 
  <tr> 
   <td>Tag</td> 
   <td>Tutto tranne la risorsa</td> 
   <td>Etichette associate al modulo per facilitare la ricerca.</td> 
  </tr> 
  <tr> 
   <td>Riferimenti</td> 
   <td><p>Modulo adattivo</p> <p>Modello di modulo</p> <p>Risorsa</p> </td> 
   <td><p>Elenco delle risorse (altre forme o risorse) a cui è correlato questo modulo. Queste risorse possono rientrare nelle due categorie seguenti:</p> 
    <ul> 
     <li>Riferimenti: risorse a cui fa riferimento il modulo corrente.</li> 
     <li>Con riferimento da: risorse che fanno riferimento alla risorsa corrente.</li> 
    </ul> <p>Queste risorse vengono visualizzate come collegamenti e i relativi metadati sono accessibili direttamente facendo clic su di essi.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Selezione del modello del modulo (XDP/XSD)</td> 
   <td>Modulo adattivo</td> 
   <td><p>Specifica quale modello di modulo viene utilizzato per la creazione del modulo adattivo. Questa proprietà può avere i seguenti valori:</p> 
    <ul> 
      <li>Modello dati modulo </li>
      <li>Schema: un XML di schema JSON</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>Nessuno</li> 
    </ul> 
    <div>
      Un modello di modulo selezionato può essere aggiornato ma non rimosso. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza metadati modulo {#view-form-metadata}

Le risorse presentano valori di proprietà esistenti che possono essere visualizzati in modalità di sola lettura. Questi metadati vengono generati al momento del caricamento del modulo o della creazione del modulo.

1. Passa alla posizione della risorsa di cui desideri visualizzare i metadati.

1. Aprire la pagina delle proprietà utilizzando uno dei modi seguenti:

   * Fai clic su **[!UICONTROL Proprietà]** ![Proprietà](assets/Smock_Info_18_N.svg) da Azioni rapide.

     >[!NOTE]
     >
     >Le Azioni rapide sono le azioni che vengono visualizzate su una miniatura al passaggio del mouse.

   * Seleziona il modulo e fai clic su **[!UICONTROL Proprietà]** ![Proprietà](assets/Smock_Info_18_N.svg) nella barra degli strumenti.
   * Passare alla pagina dei dettagli del modulo facendo clic sulla miniatura del modulo quando non è attiva la modalità di selezione. A questo punto, fai clic su ![Proprietà](assets/Smock_Info_18_N.svg) icona a forma di occhio in alto a destra, quindi fare clic su Proprietà nell&#39;elenco sottostante.

1. Nella pagina delle proprietà visualizzata viene visualizzato uno schema contenente solo le proprietà dei metadati che contengono un certo valore.

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   La porzione di contenuto è divisa in due parti:

   * Il pannello sinistro contiene la miniatura del modulo
   * Il pannello a destra contiene proprietà di metadati in modalità di sola lettura, distribuite tra varie schede.

## Aggiungi/aggiorna valori metadati modulo {#add-update-form-metadata-values}

Puoi modificare il valore delle proprietà dei metadati esistenti o aggiungere nuovi valori a un campo delle proprietà dei metadati esistente (ad esempio, quando un campo dei metadati è vuoto).

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

Nel pannello sinistro della pagina delle proprietà viene visualizzata la miniatura del modulo. Per impostazione predefinita, la miniatura visualizzata è quella generata al momento della creazione del modulo (Modulo adattivo) o al momento del caricamento del modulo.

Per tutti i tipi di modulo, puoi caricare un’immagine facendo clic su **[!UICONTROL Carica immagine]** e la ricerca di un file di immagine dalla directory locale. L&#39;immagine selezionata viene utilizzata come miniatura invece di quella predefinita.

Per l’Adaptive Forms è disponibile una funzionalità aggiuntiva che consente all’utente di generare una miniatura come istantanea dell’anteprima del modulo adattivo corrente. Da [!DNL AEM Forms] supporta anche l’authoring di Forms adattivo; l’anteprima del modulo adattivo potrebbe cambiare ogni volta che lo si modifica. Questa funzionalità per generare una miniatura consente di ottenere una nuova miniatura per il modulo adattivo in base allo stato di anteprima corrente. Clic **[!UICONTROL Genera anteprima]** per eseguire questa azione.

>[!NOTE]
>
>* Utilizza un’immagine quadrata per la miniatura. Quando si utilizza un&#39;immagine non quadrata e si visualizza la miniatura nella vista a elenco, la miniatura appare ritagliata.
>* Una volta caricata o generata una nuova immagine, la miniatura viene sostituita da questa immagine e non può essere ripristinata all&#39;immagine precedente.
>

## Aggiungere metadati personalizzati {#add-custom-metadata}

A parte i metadati forniti come predefiniti, [!DNL AEM Forms] supporta nuovi metadati personalizzati.

Viene fornito uno strumento (Editor schema metadati) per definire lo schema per il layout dei metadati, ovvero il layout di ciò che viene visualizzato nel **[!UICONTROL Proprietà]** pagina di un modulo. L’Editor schema metadati consente di aggiungere o modificare uno schema personalizzato per le risorse.

[!DNL AEM Forms] espone gli schemi di metadati dei tipi di moduli supportati in questo strumento. In questo modo, puoi accedere a questi schemi e utilizzare la funzionalità fornita nell’editor schema metadati per aggiungere proprietà personalizzate.

### Navigare nell’editor schema metadati {#navigate-the-metadata-schema-editor}

1. Accedi a **[!UICONTROL Strumenti > Risorse > Schemi metadati]**.

1. Clic **[!UICONTROL moduli]** dai moduli schema elencati.

1. Nell’elenco visualizzato, fai clic sul tipo di risorsa per il quale desideri aggiungere metadati personalizzati.

   >[!NOTE]
   >
   >Questi schemi contengono proprietà di metadati che vengono fornite come predefinite e non devono essere modificate (selezionando la casella di controllo e facendo clic su modifica nella barra degli strumenti) per evitare problemi funzionali.

1. Qualsiasi tipo di risorsa su cui hai fatto clic apre un elenco contenente `extendedmetadata` opzione. Modifica questo schema.

1. Seleziona la casella di controllo accanto a `extendedmetadata` e quindi fare clic sul pulsante Modifica ![Modifica](assets/Smock_Edit_18_N.svg) nella barra degli strumenti.

1. [!DNL AEM Forms] apre l’editor schema metadati o il generatore di moduli del tipo di risorsa selezionato (in questo caso Modulo adattivo).

   Editor metadati

   1. Il pannello sinistro contiene sezioni a schede in cui vengono inseriti i campi e il pannello destro visualizza tutti i componenti dell’interfaccia utente disponibili e le proprietà del campo selezionato dal pannello sinistro.

   1. La sezione bloccata non è modificabile e contiene campi per tutte le proprietà di metadati fornite come predefiniti.

   1. È possibile aggiungere altre schede facendo clic sul simbolo +.

   1. Puoi aggiungere un campo personalizzato del tipo desiderato trascinando il componente Campo dalla sezione **[!UICONTROL Genera modulo]** nella pagina dello schema.
   1. Le specifiche di questo campo possono essere fornite nel **[!UICONTROL Impostazioni]** dopo aver fatto clic sul campo.

### Aggiungi proprietà metadati personalizzata nell’editor schema {#add-custom-metadata-property-in-schema-editor}

1. Passa alla scheda (esistente o nuova) in cui desideri aggiungere la proprietà personalizzata.

1. Trascina un componente del tipo desiderato dalla sezione **[!UICONTROL Genera modulo]** sul pannello sinistro e posizionarlo in una posizione comoda.

   >[!NOTE]
   >
   >Non è possibile spostare le sezioni bloccate, ma è possibile inserire il componente in uno qualsiasi degli spazi vuoti.

1. Fai clic su un componente appena trascinato. Nella scheda Impostazioni visualizzata nel pannello di destra, inserisci le informazioni per i campi seguenti:

   1. Specifica un&#39;etichetta campo da utilizzare come nome visualizzato sopra il campo inserito nello schema (ad esempio: Reparto)
   1. Nel campo Mappa su proprietà puoi visualizzare un valore precompilato **&quot;./jcr:content/metadata/default&#39;**. Cambia &#39;**predefinito**&#39; a un nome di proprietà desiderato, utilizzato per memorizzare la proprietà nell&#39;archivio crx (ad esempio: &#39;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >Non modificare il prefisso &#39;./jcr:content/metadata/&#39; definisce il percorso in cui è memorizzata la proprietà.
      >
      >Inoltre, il nome della proprietà deve essere univoco per evitare di scrivere valori per due o più proprietà nella stessa posizione nell’archivio. Pertanto, si consiglia di modificare il valore &quot;default&quot;.

   1. Compila altre impostazioni in base alle esigenze. Ad esempio: seleziona l’opzione Obbligatorio se desideri rendere obbligatorio il campo.
   1. Per eliminare un campo aggiunto, selezionarlo e quindi fare clic sul pulsante Elimina ![Elimina](assets/Smock_Delete_18_N.svg) icona.

1. Se necessario, segui i passaggi 1-3 per aggiungere un’altra proprietà.
1. Clic **[!UICONTROL Salva]** dopo aver apportato tutte le modifiche.

   È stata aggiunta una proprietà di metadati personalizzata.

Tutti i Forms adattivi in [!DNL AEM Forms] ora contiene questa proprietà di metadati aggiuntiva. Puoi modificarlo dalla pagina delle proprietà.
