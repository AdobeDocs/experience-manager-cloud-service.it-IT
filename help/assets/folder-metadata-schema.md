---
title: Schema metadati cartelle
description: Scopri come creare uno schema di metadati per le cartelle di risorse in [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 10%

---

# Schema metadati cartelle {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] consente di creare schemi di metadati per le cartelle di risorse, che definiscono il layout e i metadati visualizzati nelle pagine delle proprietà delle cartelle.

## Aggiungere un modulo schema metadati cartelle {#add-a-folder-metadata-schema-form}

Utilizza l’editor di Forms per lo schema metadati delle cartelle per creare e modificare gli schemi di metadati per le cartelle.

1. Seleziona il logo [!DNL Experience Manager] e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Nella pagina Forms dello schema metadati cartelle, selezionare **[!UICONTROL Crea]**.
1. Specificare un nome per il modulo e selezionare **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato nella pagina Schema Forms.

## Modifica moduli schema metadati cartelle {#edit-folder-metadata-schema-forms}

Puoi modificare un modulo schema metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi modulo all’interno di schede.

Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o elementi del modulo al modulo schema metadati.

1. Nella pagina Forms schema, seleziona il modulo creato, quindi seleziona l&#39;icona **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartelle selezionare l&#39;icona **[!UICONTROL +]** per aggiungere una scheda al modulo. Per rinominare la scheda, selezionare il nome predefinito e specificare il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![scheda_personalizzata](assets/custom_tab.png)

   Per aggiungere altre schede, selezionare l&#39;icona **[!UICONTROL +]**. Selezionare **[!UICONTROL X]** per eliminare una scheda.

1. Nella scheda attiva, aggiungi uno o più componenti dalla scheda **[!UICONTROL Genera modulo]**.

   ![aggiunta_componenti](assets/adding_components.png)

   Se crei più schede, seleziona una scheda particolare per aggiungere componenti.

1. Per configurare un componente, selezionarlo e modificarne le proprietà nella scheda **[!UICONTROL Impostazioni]**.

   Se necessario, eliminare un componente dalla scheda **[!UICONTROL Impostazioni]**.

   ![configure_properties](assets/configure_properties.png)

1. Seleziona **[!UICONTROL Salva]** nella barra degli strumenti per salvare le modifiche.

### Componenti per la creazione di moduli {#components-to-build-forms}

Nella scheda **[!UICONTROL Genera modulo]** sono elencati gli elementi del modulo utilizzati nel modulo schema metadati cartelle. Nella scheda **[!UICONTROL Impostazioni]** vengono visualizzati gli attributi di ogni elemento selezionato nella scheda **[!UICONTROL Genera modulo]**. Elenco degli elementi modulo disponibili nella scheda **[!UICONTROL Genera modulo]**:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome componente</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Intestazione sezione</p> </td>
   <td><p> Aggiungi un’intestazione di sezione per un elenco di componenti comuni.</p> </td>
  </tr>
  <tr>
   <td><p>Testo su riga singola</p> </td>
   <td><p> Aggiungi una proprietà di testo a riga singola. Viene memorizzato come stringa.</p> </td>
  </tr>
  <tr>
   <td><p>Testo con più valori</p> </td>
   <td><p> Aggiungi una proprietà di testo con più valori. Viene memorizzato come array di stringhe.</p> </td>
  </tr>
  <tr>
   <td><p>Numero</p> </td>
   <td><p> Aggiungi un componente numero.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p> Aggiungi un componente data.</p> </td>
  </tr>
  <tr>
   <td><p>A discesa</p> </td>
   <td><p> Aggiungi un elenco a discesa.</p> </td>
  </tr>
  <tr>
   <td><p>Tag standard</p> </td>
   <td><p> Aggiungi un tag. </p> </td>
  </tr>
  <tr>
   <td><p>Campo nascosto</p> </td>
   <td><p> Aggiungi un campo nascosto. Viene inviato come parametro POST al salvataggio della risorsa.</p> </td>
  </tr>
 </tbody>
</table>

### Modifica di elementi modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, selezionare il componente e modificare tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]**. Si consiglia di mappare un solo campo a una determinata proprietà nello schema metadati. In caso contrario, il sistema seleziona l’ultimo campo aggiunto mappato alla proprietà.

**[!UICONTROL Etichetta campo]**: nome della proprietà dei metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: questa proprietà specifica il percorso relativo del nodo della cartella nell&#39;archivio di CRX in cui viene salvato. Inizia con &quot;**./**&quot;, che indica che il percorso si trova nel nodo della cartella.

Di seguito sono riportati alcuni esempi di valori validi per una proprietà:

* `./jcr:content/metadata/dc:title`: memorizza il valore nel nodo di metadati della cartella come proprietà `dc:title`.

* `./jcr:created`: memorizza la data e l&#39;ora di creazione di una risorsa. È una proprietà protetta. Se configuri queste proprietà, l&#39;Adobe consiglia di contrassegnarle come [!UICONTROL Disabilita modifica].

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, non includere uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso JSON]**: utilizzalo per specificare il percorso del file JSON in cui specificare le coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: utilizzare questa proprietà per specificare il testo segnaposto relativo alla proprietà dei metadati.

**[!UICONTROL Opzioni]**: utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: utilizzare questa proprietà per aggiungere una breve descrizione del componente metadati.

**[!UICONTROL Classe]**: classe oggetto a cui è associata la proprietà.

## Elimina moduli schema metadati cartelle {#delete-folder-metadata-schema-forms}

Puoi eliminare i moduli schema metadati cartelle dalla pagina Forms dello schema metadati cartelle. Per eliminare un modulo, selezionalo e seleziona l’icona Elimina dalla barra degli strumenti.

![elimina_modulo](assets/delete_form.png)

## Assegnare uno schema di metadati per le cartelle {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati di cartella a una cartella dalla pagina Forms dello schema metadati cartelle o durante la creazione di una cartella.

Se configuri uno schema di metadati per una cartella, il percorso del modulo schema viene memorizzato nella proprietà `folderMetadataSchema` del nodo della cartella in .*/jcr:content*.

### Assegnare a uno schema dalla pagina Schema metadati cartelle {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Seleziona il logo [!DNL Experience Manager] e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]**> **[!UICONTROL Schemi metadati cartelle]**.
1. Dalla pagina Forms schema metadati cartelle, seleziona il modulo schema da applicare a una cartella.
1. Dalla barra degli strumenti, selezionare **[!UICONTROL Applica a cartelle]**.

1. Selezionare la cartella in cui applicare lo schema, quindi selezionare **[!UICONTROL Applica]**. Se nella cartella è già applicato uno schema metadati, un messaggio di avviso informa che stai per sovrascrivere lo schema metadati esistente. Seleziona **[!UICONTROL Sovrascrivi]**.
1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.

   ![proprietà_cartella](assets/folder_properties.png)

   Per visualizzare i campi dei metadati della cartella, selezionare la scheda **[!UICONTROL Metadati cartella]**.

   ![proprietà_metadati_cartelle](assets/folder_metadata_properties.png)

### Assegnare uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Puoi assegnare uno schema di metadati della cartella durante la creazione di una cartella. Se nel sistema è presente almeno uno schema di metadati di cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** verrà visualizzato un elenco aggiuntivo. Puoi selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcuno schema.

1. Dall&#39;interfaccia utente di [!DNL Experience Manager Assets], selezionare **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Specifica un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartelle, seleziona lo schema desiderato. Quindi, seleziona **[!UICONTROL Crea]**.

   ![seleziona_schema](assets/select_schema.png)

1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.
1. Per visualizzare i campi dei metadati della cartella, selezionare la scheda **[!UICONTROL Metadati cartella]**.

## Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. Nella pagina delle proprietà della cartella viene visualizzata la scheda **[!UICONTROL Metadati cartella]**. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immetti i valori dei metadati nei vari campi e seleziona **[!UICONTROL Salva]** per memorizzare i valori. I valori specificati vengono memorizzati nel nodo della cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
