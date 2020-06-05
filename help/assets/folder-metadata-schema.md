---
title: Schema metadati cartelle
description: Scopri come creare uno schema di metadati per le cartelle di risorse in Risorse AEM
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2394ce2b5ebbd3e0e7229a98b5f500312b82dbd7
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 10%

---


# Schema metadati cartelle {#folder-metadata-schema}

Risorse Adobe Experience Manager (AEM) consente di creare schemi di metadati per le cartelle di risorse, che definiscono il layout e i metadati visualizzati nelle pagine delle proprietà della cartella.

## Aggiunta di uno schema di metadati di una cartella {#add-a-folder-metadata-schema-form}

Utilizzare l&#39;editor Moduli schema metadati cartella per creare e modificare gli schemi di metadati per le cartelle.

1. Tocca/fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cartella Schemi di metadati]**.
1. Nella pagina Moduli schema metadati cartella, toccate o fate clic su **[!UICONTROL Crea]**.
1. Specificare un nome per il modulo, quindi toccare o fare clic su **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato nella pagina Moduli schema.

## Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

È possibile modificare un modulo di schema di metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi del modulo all&#39;interno delle schede.

È possibile mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o elementi del modulo al modulo schema di metadati.

1. Nella pagina Moduli schema, selezionare il modulo creato, quindi toccare o fare clic sull&#39;icona **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartella, toccate o fate clic sull&#39;icona **[!UICONTROL +]** per aggiungere una scheda al modulo. Per rinominare la scheda, toccate o fate clic sul nome predefinito e specificate il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![custom_tab](assets/custom_tab.png)

   Per aggiungere altre schede, toccate o fate clic sull&#39;icona **[!UICONTROL +]** . Toccate/fate clic su **[!UICONTROL X]** per eliminare una scheda.

1. Nella scheda attiva, aggiungere uno o più componenti dalla scheda **[!UICONTROL Genera modulo]** .

   ![adding_components](assets/adding_components.png)

   Se create più schede, toccate o fate clic su una scheda specifica per aggiungere i componenti.

1. Per configurare un componente, selezionatelo e modificatene le proprietà nella scheda **[!UICONTROL Impostazioni]** .

   Se necessario, eliminate un componente dalla scheda **[!UICONTROL Impostazioni]** .

   ![configure_properties](assets/configure_properties.png)

1. Toccate/fate clic su **[!UICONTROL Salva]** dalla barra degli strumenti per salvare le modifiche.

### Componenti per la creazione di moduli {#components-to-build-forms}

Nella scheda **[!UICONTROL Genera modulo]** sono elencati gli elementi del modulo utilizzati nel modulo schema di metadati della cartella. Nella scheda **[!UICONTROL Impostazioni]** sono visualizzati gli attributi per ogni elemento selezionato nella scheda **[!UICONTROL Modulo]** di creazione. Elenco degli elementi del modulo disponibili nella scheda **[!UICONTROL Genera modulo]** :

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome componente</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Intestazione sezione</p> </td>
   <td><p> Aggiungere un'intestazione di sezione per un elenco di componenti comuni.</p> </td>
  </tr>
  <tr>
   <td><p>Testo su riga singola</p> </td>
   <td><p> Aggiungere una proprietà di testo su una sola riga. È memorizzato come stringa.</p> </td>
  </tr>
  <tr>
   <td><p>Testo con più valori</p> </td>
   <td><p> Aggiungete una proprietà di testo con più valori. È memorizzato come array di stringhe.</p> </td>
  </tr>
  <tr>
   <td><p>Numero</p> </td>
   <td><p> Aggiungere un componente numero.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p> Aggiungere un componente data.</p> </td>
  </tr>
  <tr>
   <td><p>A discesa</p> </td>
   <td><p> Aggiungere un elenco a discesa.</p> </td>
  </tr>
  <tr>
   <td><p>Tag standard</p> </td>
   <td><p> Aggiungi un tag. </p> </td>
  </tr>
  <tr>
   <td><p>Campo nascosto</p> </td>
   <td><p> Aggiungere un campo nascosto. Viene inviato come parametro POST al momento del salvataggio della risorsa.</p> </td>
  </tr>
 </tbody>
</table>

### Modifica degli elementi del modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, toccate o fate clic sul componente e modificate tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]** .

**[!UICONTROL Etichetta]** campo: Nome della proprietà di metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: Questa proprietà specifica il percorso relativo del nodo della cartella nell&#39;archivio CRX in cui viene salvato. Comincia con &quot;**./**&quot;, che indica che il percorso si trova sotto il nodo della cartella.

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: Memorizza il valore nel nodo di metadati della cartella come proprietà `dc:title`.

* `./jcr:created`: Memorizza la data e l’ora di creazione di una risorsa. È una proprietà protetta. Se configurate queste proprietà, Adobe consiglia di contrassegnarle come [!UICONTROL Disattiva modifica].

Per garantire che il componente venga visualizzato correttamente nel modulo dello schema di metadati, non includete uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso]** JSON: Utilizzatelo per specificare il percorso del file JSON in cui specificate le coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: Utilizzare questa proprietà per specificare il testo segnaposto relativo alla proprietà metadata.

**[!UICONTROL Scelte]**: Utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: Utilizzate questa proprietà per aggiungere una breve descrizione per il componente di metadati.

**[!UICONTROL Classe]**: Classe oggetto a cui è associata la proprietà.

## Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

È possibile eliminare i moduli dello schema di metadati della cartella dalla pagina Moduli schema metadati cartella. Per eliminare un modulo, selezionarlo e toccare o fare clic sull&#39;icona Elimina dalla barra degli strumenti.

![delete_form](assets/delete_form.png)

## Assegnazione di uno schema di metadati di una cartella {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati a una cartella dalla pagina Moduli schema metadati cartella o durante la creazione di una cartella.

Se si configura uno schema di metadati per una cartella, il percorso del modulo dello schema viene memorizzato nella `folderMetadataSchema` proprietà del nodo della cartella in .*/jcr:content*.

### Assegnazione a uno schema dalla pagina Schema metadati cartella {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Tocca/fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cartella Schemi di metadati]**.
1. Dalla pagina Moduli schema metadati cartella, selezionare il modulo schema che si desidera applicare a una cartella.
1. Dalla barra degli strumenti, toccate o fate clic su **[!UICONTROL Applica alle cartelle]**.

1. Selezionare la cartella in cui applicare lo schema, quindi fare clic o toccare **[!UICONTROL Applica]**. Se uno schema di metadati è già applicato alla cartella, un messaggio di avviso informa che lo schema di metadati esistente sta per essere sovrascritto. Toccate o fate clic su **[!UICONTROL Sovrascrivi]**.
1. Aprite le proprietà dei metadati per la cartella a cui avete applicato lo schema di metadati.

   ![folder_properties](assets/folder_properties.png)

   Per visualizzare i campi di metadati della cartella, tocca o fai clic sulla scheda **[!UICONTROL Folder Metadata (Metadati cartella)]**.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Assegnazione di uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Quando create una cartella, potete assegnare uno schema di metadati a una cartella. Se nel sistema è presente almeno uno schema di metadati della cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** viene visualizzato un elenco aggiuntivo. È possibile selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcun schema.

1. Dall’interfaccia utente di Risorse AEM, tocca o fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Specificate un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartella, selezionate lo schema desiderato. Then, tap/click **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. Aprite le proprietà dei metadati per la cartella a cui avete applicato lo schema di metadati.
1. Per visualizzare i campi di metadati della cartella, tocca o fai clic sulla scheda **[!UICONTROL Folder Metadata (Metadati cartella)]**.

## Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. Nella pagina delle proprietà della cartella viene visualizzata la scheda **[!UICONTROL Metadati cartella]**. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immettete i valori dei metadati nei vari campi e toccate o fate clic su **[!UICONTROL Salva]** per memorizzarli. I valori specificati vengono memorizzati nel nodo cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

