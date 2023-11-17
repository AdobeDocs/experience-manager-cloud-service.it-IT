---
title: Schema metadati cartelle
description: Scopri come creare uno schema di metadati per le cartelle di risorse in [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 10%

---

# Schema metadati cartelle {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] consente di creare schemi di metadati per le cartelle di risorse, che definiscono il layout e i metadati visualizzati nelle pagine delle proprietà delle cartelle.

## Aggiungere un modulo schema metadati cartelle {#add-a-folder-metadata-schema-form}

Utilizza l’editor di Forms per lo schema metadati delle cartelle per creare e modificare gli schemi di metadati per le cartelle.

1. Seleziona la [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Nella pagina Forms dello schema metadati cartelle, seleziona **[!UICONTROL Crea]**.
1. Specificare un nome per il modulo e selezionare **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato nella pagina Schema Forms.

## Modifica moduli schema metadati cartelle {#edit-folder-metadata-schema-forms}

Puoi modificare un modulo schema metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi modulo all’interno di schede.

Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o elementi del modulo al modulo schema metadati.

1. Nella pagina Schema Forms selezionare il modulo creato, quindi selezionare **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartelle, seleziona la **[!UICONTROL +]** per aggiungere una scheda al modulo. Per rinominare la scheda, selezionate il nome di default e specificate il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![custom_tab](assets/custom_tab.png)

   Per aggiungere altre schede, seleziona la **[!UICONTROL +]** icona. Seleziona **[!UICONTROL X]** per eliminare una scheda.

1. Nella scheda attiva, aggiungi uno o più componenti della **[!UICONTROL Genera modulo]** scheda.

   ![add_components](assets/adding_components.png)

   Se crei più schede, seleziona una scheda particolare per aggiungere componenti.

1. Per configurare un componente, selezionalo e modificane le proprietà in **[!UICONTROL Impostazioni]** scheda.

   Se necessario, elimina un componente da **[!UICONTROL Impostazioni]** scheda.

   ![configure_properties](assets/configure_properties.png)

1. Seleziona **[!UICONTROL Salva]** dalla barra degli strumenti per salvare le modifiche.

### Componenti per la creazione di moduli {#components-to-build-forms}

Il **[!UICONTROL Genera modulo]** scheda elenca gli elementi del modulo utilizzati nel modulo schema metadati cartelle. Il **[!UICONTROL Impostazioni]** nella scheda vengono visualizzati gli attributi di ogni elemento selezionato nel **[!UICONTROL Genera modulo]** scheda. Di seguito è riportato un elenco degli elementi modulo disponibili nel **[!UICONTROL Genera modulo]** scheda:

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

Per modificare le proprietà degli elementi modulo, seleziona il componente e modifica tutte o un sottoinsieme delle seguenti proprietà in **[!UICONTROL Impostazioni]** scheda. Si consiglia di mappare un solo campo a una determinata proprietà nello schema metadati. In caso contrario, il sistema seleziona l’ultimo campo aggiunto mappato alla proprietà.

**[!UICONTROL Etichetta campo]**: nome della proprietà dei metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: questa proprietà specifica il percorso relativo del nodo della cartella nell’archivio CRX in cui viene salvato. Inizia con &quot;**./**&quot;, che indica che il percorso si trova sotto il nodo della cartella.

Di seguito sono riportati alcuni esempi di valori validi per una proprietà:

* `./jcr:content/metadata/dc:title`: memorizza il valore come proprietà nel nodo di metadati della cartella `dc:title`.

* `./jcr:created`: memorizza la data e l’ora di creazione di una risorsa. È una proprietà protetta. Se configuri queste proprietà, l’Adobe consiglia di contrassegnarle come [!UICONTROL Disattiva modifica].

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, non includere uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso JSON]**: utilizzalo per specificare il percorso del file JSON in cui specificare le coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: utilizza questa proprietà per specificare il testo segnaposto rilevante relativo alla proprietà dei metadati.

**[!UICONTROL Scelte]**: utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: utilizza questa proprietà per aggiungere una breve descrizione del componente metadati.

**[!UICONTROL Classe]**: classe oggetto a cui è associata la proprietà.

## Elimina moduli schema metadati cartelle {#delete-folder-metadata-schema-forms}

Puoi eliminare i moduli schema metadati cartelle dalla pagina Forms dello schema metadati cartelle. Per eliminare un modulo, selezionalo e seleziona l’icona Elimina dalla barra degli strumenti.

![delete_form](assets/delete_form.png)

## Assegnare uno schema di metadati per le cartelle {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati di cartella a una cartella dalla pagina Forms dello schema metadati cartelle o durante la creazione di una cartella.

Se configuri uno schema di metadati per una cartella, il percorso del modulo schema viene memorizzato in `folderMetadataSchema` proprietà del nodo della cartella in .*/jcr:contenuto*.

### Assegnare a uno schema dalla pagina Schema metadati cartelle {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Seleziona la [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**> **[!UICONTROL Schemi metadati cartelle]**.
1. Dalla pagina Forms schema metadati cartelle, seleziona il modulo schema da applicare a una cartella.
1. Dalla barra degli strumenti, seleziona **[!UICONTROL Applica a cartelle]**.

1. Seleziona la cartella in cui applicare lo schema, quindi seleziona **[!UICONTROL Applica]**. Se nella cartella è già applicato uno schema metadati, un messaggio di avviso informa che stai per sovrascrivere lo schema metadati esistente. Seleziona **[!UICONTROL Sovrascrivere]**.
1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.

   ![folder_properties](assets/folder_properties.png)

   Per visualizzare i campi dei metadati della cartella, seleziona la **[!UICONTROL Metadati cartella]** scheda.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Assegnare uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Puoi assegnare uno schema di metadati della cartella durante la creazione di una cartella. Se nel sistema è presente almeno uno schema di metadati di cartella, viene visualizzato un elenco aggiuntivo nel **[!UICONTROL Crea cartella]** . Puoi selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcuno schema.

1. Dalla sezione [!DNL Experience Manager Assets] interfaccia utente, selezionare **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Specifica un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartelle, seleziona lo schema desiderato. Quindi, seleziona **[!UICONTROL Crea]**.

   ![select_schema](assets/select_schema.png)

1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.
1. Per visualizzare i campi dei metadati della cartella, seleziona la **[!UICONTROL Metadati cartella]** scheda.

## Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. Nella pagina delle proprietà della cartella viene visualizzata la scheda **[!UICONTROL Metadati cartella]**. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Inserisci i valori dei metadati nei vari campi e seleziona **[!UICONTROL Salva]** per memorizzare i valori. I valori specificati vengono memorizzati nel nodo della cartella nell’archivio CRX.

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
