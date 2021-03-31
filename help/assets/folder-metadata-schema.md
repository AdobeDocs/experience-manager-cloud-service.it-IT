---
title: Schema metadati cartelle
description: Scopri come creare uno schema di metadati per le cartelle di risorse in [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadati
role: Business Practices, Amministratore
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 10%

---


# Schema metadati cartelle {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] consente di creare schemi di metadati per le cartelle delle risorse, che definiscono il layout e i metadati visualizzati nelle pagine di proprietà delle cartelle.

## Aggiungi un modulo schema metadati cartella {#add-a-folder-metadata-schema-form}

Utilizza l’editor Forms per Schema metadati cartelle per creare e modificare schemi di metadati per le cartelle.

1. Tocca/fai clic sul logo [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cartella Schemi di metadati]**.
1. Nella pagina Forms Schema metadati cartelle, tocca o fai clic su **[!UICONTROL Crea]**.
1. Specifica un nome per il modulo e tocca o fai clic su **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato nella pagina Forms schema.

## Modifica moduli schema metadati cartelle {#edit-folder-metadata-schema-forms}

È possibile modificare un modulo schema metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi modulo all’interno di schede.

Puoi mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o nuovi elementi modulo al modulo schema metadati.

1. Nella pagina Forms schema, seleziona il modulo creato, quindi tocca o fai clic sull’icona **[!UICONTROL Modifica]** nella barra degli strumenti.
1. Nella pagina Editor schema metadati cartelle, tocca o fai clic sull’icona **[!UICONTROL +]** per aggiungere una scheda al modulo. Per rinominare la scheda, tocca o fai clic sul nome predefinito e specifica il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![custom_tab](assets/custom_tab.png)

   Per aggiungere altre schede, tocca o fai clic sull&#39;icona **[!UICONTROL +]** . Tocca o fai clic su **[!UICONTROL X]** per eliminare una scheda.

1. Nella scheda attiva, aggiungi uno o più componenti dalla scheda **[!UICONTROL Genera modulo]** .

   ![add_components](assets/adding_components.png)

   Se crei più schede, tocca o fai clic su una scheda specifica per aggiungere componenti.

1. Per configurare un componente, selezionalo e modificane le proprietà nella scheda **[!UICONTROL Impostazioni]** .

   Se necessario, elimina un componente dalla scheda **[!UICONTROL Impostazioni]** .

   ![configure_properties](assets/configure_properties.png)

1. Tocca o fai clic su **[!UICONTROL Salva]** nella barra degli strumenti per salvare le modifiche.

### Componenti per creare moduli {#components-to-build-forms}

La scheda **[!UICONTROL Genera modulo]** elenca gli elementi del modulo utilizzati nel modulo schema metadati della cartella. La scheda **[!UICONTROL Impostazioni]** visualizza gli attributi per ogni elemento selezionato nella scheda **[!UICONTROL Genera modulo]** . Elenco degli elementi del modulo disponibili nella scheda **[!UICONTROL Genera modulo]** :

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
   <td><p> Aggiungi un componente numerico.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p> Aggiungi un componente data .</p> </td>
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
   <td><p> Aggiungi un campo nascosto. Viene inviato come parametro POST al momento del salvataggio della risorsa.</p> </td>
  </tr>
 </tbody>
</table>

### Modifica degli elementi del modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, tocca o fai clic sul componente e modifica tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]** .

**[!UICONTROL Etichetta]** campo: Nome della proprietà di metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: Questa proprietà specifica il percorso relativo del nodo della cartella nell&#39;archivio CRX in cui viene salvato. Inizia con &quot;**./**&quot;, che indica che il percorso si trova sotto il nodo della cartella.

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: Memorizza il valore nel nodo di metadati della cartella come proprietà  `dc:title`.

* `./jcr:created`: Memorizza la data e l’ora di creazione di una risorsa. È una proprietà protetta. Se configuri queste proprietà, l&#39;Adobe consiglia di contrassegnarle come [!UICONTROL Disabilita Modifica].

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, non includere uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso]** JSON: Usarlo per specificare il percorso del file JSON in cui specificare coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: Utilizzare questa proprietà per specificare il testo segnaposto pertinente relativo alla proprietà metadati.

**[!UICONTROL Scelte]**: Utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: Utilizza questa proprietà per aggiungere una breve descrizione per il componente metadati.

**[!UICONTROL Classe]**: Classe oggetto a cui è associata la proprietà.

## Elimina moduli schema metadati cartelle {#delete-folder-metadata-schema-forms}

È possibile eliminare i moduli schema metadati cartelle dalla pagina Forms Schema metadati cartelle. Per eliminare un modulo, selezionalo e tocca o fai clic sull’icona Elimina sulla barra degli strumenti.

![delete_form](assets/delete_form.png)

## Assegnare uno schema di metadati della cartella {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati a una cartella dalla pagina Forms Schema metadati cartelle o durante la creazione di una cartella.

Se si configura uno schema di metadati per una cartella, il percorso del modulo schema viene memorizzato nella proprietà `folderMetadataSchema` del nodo della cartella in .*/jcr:content*.

### Assegna a uno schema dalla pagina Schema metadati cartelle {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Tocca/fai clic sul logo [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**> **[!UICONTROL Cartella Schemi di metadati]**.
1. Nella pagina Forms Schema metadati cartelle selezionare il modulo schema da applicare a una cartella.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Applica a cartelle]**.

1. Seleziona la cartella in cui applicare lo schema, quindi tocca o fai clic su **[!UICONTROL Applica]**. Se nella cartella è già applicato uno schema di metadati, un messaggio di avviso segnala che lo schema di metadati esistente sta per essere sovrascritto. Tocca o fai clic su **[!UICONTROL Sovrascrivi]**.
1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.

   ![folder_properties](assets/folder_properties.png)

   Per visualizzare i campi di metadati della cartella, tocca o fai clic sulla scheda **[!UICONTROL Folder Metadata (Metadati cartella)]**.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Assegnare uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

È possibile assegnare uno schema di metadati della cartella durante la creazione di una cartella. Se nel sistema esiste almeno uno schema di metadati della cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** viene visualizzato un elenco aggiuntivo. È possibile selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcun schema.

1. Dall’interfaccia utente [!DNL Experience Manager Assets], tocca o fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Specifica un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartelle, selezionare lo schema desiderato. Quindi, tocca o fai clic su **[!UICONTROL Crea]**.

   ![select_schema](assets/select_schema.png)

1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.
1. Per visualizzare i campi di metadati della cartella, tocca o fai clic sulla scheda **[!UICONTROL Folder Metadata (Metadati cartella)]**.

## Utilizza lo schema metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. Nella pagina delle proprietà della cartella viene visualizzata la scheda **[!UICONTROL Metadati cartella]**. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immetti i valori dei metadati nei vari campi e tocca o fai clic su **[!UICONTROL Salva]** per memorizzare i valori. I valori specificati vengono memorizzati nel nodo della cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
