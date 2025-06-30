---
title: Come gestire i tag nella Vista risorse?
description: Scopri come gestire i tag nella Vista risorse. I tag consentono di categorizzare le risorse così da poter essere sfogliate e cercate in modo più efficiente.
exl-id: 7c5e1212-054f-46ca-9982-30e40b0482e1
feature: Smart Tags
role: User, Admin, Developer
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 98%

---

# Gestire i tag nella Vista risorse {#view-assets-and-details}

>[!CONTEXTUALHELP]
>id="assets_taxonomy_management"
>title="Gestisci tag"
>abstract="I tag consentono di categorizzare le risorse così da poter essere sfogliate e cercate in modo più efficiente. Gli amministratori possono utilizzare la struttura gerarchica dell’assegnazione di tag, che facilita l’applicazione di metadati rilevanti, la classificazione delle risorse, il supporto della ricerca, il riutilizzo dei tag, il miglioramento della reperibilità e così via."

I tag consentono di categorizzare le risorse così da poter essere sfogliate e cercate in modo più efficiente. L’assegnazione tag consente di estendere la tassonomia appropriata ad altri utenti e flussi di lavoro.

Gli elenchi semplici di vocabolari controllati possono diventare ingestibili nel tempo. Gli amministratori possono utilizzare la struttura gerarchica dell’assegnazione di tag, che facilita l’applicazione di metadati rilevanti, la classificazione delle risorse, il supporto della ricerca, il riutilizzo dei tag, il miglioramento della reperibilità e così via.

Puoi creare uno spazio dei nomi a livello di radice e creare al suo interno una struttura gerarchica di sottotag. Ad esempio, puoi creare uno spazio dei nomi `Activities` a livello di radice e assegnare i tag `Cycling`, `Hiking` e `Running` al suo interno. Puoi assegnare ulteriori sottotag `Clothing` e `Shoes` all’interno di `Running`.

![Gestione dell’assegnazione tag](assets/tags-hierarchy.png)

L’assegnazione tag offre molti vantaggi, ad esempio:

* l’assegnazione tag consente agli autori di organizzare facilmente risorse differenti tramite una tassonomia comune. Gli autori possono cercare e organizzare rapidamente le risorse in base a tag comuni.

* I tag gerarchici sono estremamente flessibili e costituiscono un modo eccellente di organizzare i termini in modo logico. È possibile rappresentare interi sistemi tassonomici tramite spazi dei nomi, tag e sottotag.

* I tag possono evolvere nel tempo in funzione dei cambiamenti del vocabolario organizzativo.

* I tag gestiti nella Vista amministrazione rimangono sincronizzati con i tag gestiti nella Vista risorse garantendo la governance e l’integrità dei metadati.

Per poter applicare tag alle risorse, è necessario prima creare uno spazio dei nomi, quindi creare e aggiungervi i tag. È possibile anche creare dei tag e aggiungerli a uno spazio dei nomi esistente. Tutti i tag creati a livello di radice vengono aggiunti automaticamente allo spazio dei nomi Tag standard. È possibilie quindi aggiungere il campo Tag al modulo dei metadati in modo che venga visualizzato nella pagina dei dettagli della risorsa. Dopo aver configurato queste impostazioni, puoi iniziare ad applicare i tag alle risorse.

>[!NOTE]
>
>È necessario aggiungere il campo Tag al modulo dei metadati solo se non si utilizza il modulo dei metadati predefinito.

![Gestione dell’assegnazione tag](assets/tagging-taxonomy-management.png)

Nella Vista amministrazione, sono disponibili ulteriori funzionalità oltre a quelle indicate in questo articolo, tra cui unione, ridenominazione, localizzazione e pubblicazione di tag.

## Creare uno spazio dei nomi {#create-a-namespace}

Uno spazio dei nomi è un contenitore per i tag che può esistere solo a livello di radice. È possibile iniziare a impostare la struttura gerarchica dei tag definendo per prima cosa un nome logico per lo spazio dei nomi. Se non aggiungi un tag a nessuno degli spazi dei nomi esistenti, il tag si sposta automaticamente nei Tag standard.

Per creare uno spazio dei nomi, esegui le seguenti operazioni:

1. Passa a `Taxonomy Management` in `Settings` per visualizzare l’elenco degli spazi dei nomi esistenti. È anche possibile visualizzare la data dell’ultima modifica, l’utente che ha modificato lo spazio dei nomi o i tag al suo interno e il numero di volte in cui il tag viene utilizzato in una risorsa.
1. Fai clic su `Create Namespace`.
1. Aggiungi `Title`, `Name` e `Description` per lo spazio dei nomi. L’input specificato nel campo `Title` viene visualizzato nella parte superiore della gerarchia. Ad esempio, nell’immagine seguente, **Attività** fa riferimento al titolo dello spazio dei nomi.

   ![Gestione dell’assegnazione tag](assets/tags-hierarchy.png)

1. Fai clic su `Save`.

## Aggiungere di tag a uno spazio dei nomi {#add-tags-to-namespace}

Per aggiungere tag a uno spazio dei nomi, esegui le seguenti operazioni:

1. Passa a **[!UICONTROL Gestione della tassonomia]**.
1. Seleziona lo spazio dei nomi e fai clic su `Create` per creare il tag al livello superiore nello spazio dei nomi. Se devi creare un sottotag in un tag esistente in uno spazio dei nomi, seleziona il tag e fai clic su `Create`.
   ![Gerarchia dei tag](assets/hierarchy-of-tags.png)

   In questo esempio, l’immagine a sinistra rappresenta il tag direttamente nello spazio dei nomi `automobile-four-wheeler` visualizzato nel campo `Path`. L’immagine a destra è un esempio di sottotag aggiunti all’interno di un tag in quanto, oltre allo spazio dei nomi, sono presenti più nomi di tag `jeep` e `jeep-meridian` visualizzati nel campo `Path`.
1. Specifica il titolo, il nome e la descrizione del tag, quindi fai clic su `Save`.


   >[!NOTE]
   >
   >* I campi `Title` e `Name` sono obbligatori, mentre il campo `Description` è facoltativo.
   >* Per impostazione predefinita, lo strumento copia il testo digitato nel campo Titolo rimuove gli spazi vuoti o i caratteri speciali (. &amp; / \ : * ? [ ] | &quot; %) e lo memorizza come Nome.
   >* È possibile aggiornare il campo `Title` in un secondo momento ma il campo `Name` è di sola lettura.

## Aggiungere tag ai tag standard {#add-tags-to-standard-tags}

I tag non strutturati o i tag privi di gerarchia sono memorizzati sotto spazio dei nomi `Standard Tags`. Inoltre, se desideri aggiungere altri termini descrittivi senza influire sulla tassonomia gestita, puoi memorizzare tale valore in `Standard Tags`. È possibile spostare questi valori in spazi dei nomi strutturati nel tempo. Inoltre, è possibile utilizzare lo spazio dei nomi `Standard Tags` come voce in formato libero per le parole chiave.

Per creare un tag standard, fai clic su `Create Tag` a livello di radice. Specifica titolo, nome e descrizione, quindi fai clic su `Save`.

![Aggiunta di tag ai tag standard](assets/adding-tags-to-standard-tags.png)

>[!NOTE]
>
>Se elimini lo spazio dei nomi `Standard Tags` utilizzando Assets as a Cloud Service, i tag creati a livello di radice non vengono visualizzati nell’elenco dei tag disponibili.

## Spostare i tag {#move-tags}

Se i tag vengono memorizzati in una gerarchia errata o se la tassonomia cambia nel tempo, è possibile spostare i tag selezionati per mantenere l’integrità dei dati. Durante lo spostamento dei tag è necessario tenere presenti le seguenti condizioni:

* I tag possono essere spostati solo al di sotto degli spazi dei nomi esistenti o all’interno di una gerarchia di tag esistente.
* Non è possibile spostare i tag nella directory principale per diventare uno spazio dei nomi.
* Lo spostamento di un tag principale comporta anche lo spostamento di tutti i tag secondari memorizzati nella gerarchia.

Per spostare i tag da una posizione a un’altra, effettua le seguenti operazioni:

1. Seleziona il tag o l’intera gerarchia di tag nello spazio dei nomi appropriato e fai clic su `Move`.
1. Nella finestra di dialogo Sposta, seleziona il nuovo tag di destinazione o spazio dei nomi utilizzando la sezione `Select Tag`.
1. Fai clic su `Save`. Il tag viene visualizzato nella nuova posizione.

## Modificare i tag {#edit-tags}

Per modificare il titolo del tag, selezionalo e fai clic su `Edit`. Specifica il nuovo titolo e fai clic su `Save`.

>[!NOTE]
>
>* Il `Name` di un tag non può essere aggiornato. Anche il percorso principale di un tag è basato sul nome del tag. Il percorso rimane invariato anche se si aggiorna il campo `Title`.
>* Ulteriori operazioni, quali unione, localizzazione e pubblicazione, sono disponibili in Assets as a Cloud Service.

## Eliminare i tag {#delete-tags}

È possibile eliminare più spazi dei nomi o tag contemporaneamente. L’operazione di eliminazione non può essere annullata.

Per eliminare i tag, effettua le seguenti operazioni:

1. Seleziona lo spazio dei nomi o il tag e fai clic su `Delete`.
1. Fai clic su `Confirm`.

>[!NOTE]
>
>* Se si elimina il tag principale o lo spazio dei nomi, vengono eliminati anche i tag secondari memorizzati nella gerarchia. Per eliminare o aggiornare lo spazio dei nomi principale, si consiglia di [spostare i tag](#moving-tags) nella nuova destinazione prima di eliminare la gerarchia principale.
>* L’eliminazione di un tag comporta anche l’eliminazione di tutti i relativi riferimenti dalle risorse.
>* Non puoi eliminare i tag standard esistenti a livello principale.

## Aggiungere il componente Tag al modulo Metadati {#add-tags-to-metadata-form}

Il componente Tag viene aggiunto al modulo metadati `default` automaticamente. Puoi progettare un [modulo metadati](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/metadata.html?lang=it#metadata-forms) utilizzando un modello o da zero. Se non utilizzi un modello di modulo Metadati esistente, puoi modificare il modulo Metadati e aggiungere il componente Tag. La mappatura della proprietà dei metadati viene compilata automaticamente e non può essere modificata in questo momento. Gli utenti di [!DNL Assets as a Cloud Service] possono aggiornare la mappatura per memorizzare i valori dei tag utilizzando spazi dei nomi personalizzati ed esporre solo sottoinsiemi di gerarchie utilizzando percorsi principali.

Guarda questo video rapido per vedere come aggiungere il componente Tag al modulo di metadati:

>[!VIDEO](https://video.tv.adobe.com/v/3420452)


### Aggiungere tag alle risorse {#add-tags-to-assets}

1. Vai alla pagina dei dettagli della risorsa e passa alla sezione `Tags` del modulo Metadati.
1. Seleziona l’icona del selettore tag posta accanto al campo Tag oppure inizia a digitare il nome di un tag per visualizzare i risultati suggeriti.

   ![Assegnazione di tag alle risorse](assets/adding-tags-to-assets.png)

1. Seleziona uno o più tag. Il tag secondario viene selezionato automaticamente insieme al tag principale o allo spazio dei nomi.
I tag modificati in Assets Essentials vengono applicati anche in Assets as a Cloud Service.

## Aggiungere tag nell’elenco Bloccati {#blocklist-essentials}

[!DNL Assets view] consente di definire l’elenco Bloccati per le parole che non devono essere aggiunte come tag avanzati alle risorse quando vengono caricate nell’archivio. Questa funzionalità consente di mantenere la conformità al marchio e di ridurre gli sforzi nella moderazione dei tag avanzati.
<!--
### Block smart tags for single asset {#block-smart-tags-for-single-asset}
![block smart tags](assets/block-smart-tags.png)
-->

### Bloccare i tag avanzati per tutte le risorse {#block-smart-tags-for-all-assets}

[!DNL Assets view] consente a un amministratore di bloccare i tag avanzati per le risorse esistenti e appena aggiunte. Per bloccare i tag, esegui le seguenti operazioni:

1. Passa a **[!UICONTROL Tag bloccati]** in **[!UICONTROL Impostazioni]**.
1. Fai clic su **[!UICONTROL Aggiungi tag bloccato]**.
1. Digita i tag nella casella di testo da bloccare e fai clic su **[!UICONTROL Invio]**.
1. Una volta aggiunti i tag, fai clic su **[!UICONTROL Aggiungi]**. I tag inseriti vengono inseriti nell’elenco dei tag bloccati.

   >[!NOTE]
   >
   >Puoi aggiungere un massimo di 25 tag all’elenco contemporaneamente. Ripeti i passaggi per aggiungere altri tag nell’elenco Bloccati.

Puoi anche bloccare i tag avanzati per una singola risorsa. Passa ai dettagli di una risorsa. Nella scheda **[!UICONTROL Tag]**, rimuovi i tag avanzati indesiderati e fai clic su **[!UICONTROL Salva]**. I tag sono inseriti nell’elenco Bloccati della risorsa selezionata.

### Azioni eseguite nell’elenco Bloccati {#blocklist-actions}

* **Rimuovi tag:** puoi anche rimuovere i tag dall’elenco Bloccati. Per farlo, seleziona uno o più tag da rimuovere. Fai clic su **[!UICONTROL Rimuovi]**. Puoi rimuovere un massimo di 25 tag dall’elenco contemporaneamente.
* **Seleziona tutto:** seleziona la casella di controllo adiacente a **Nome tag** per selezionare tutti i tag nell’elenco Bloccati.
* **Ordinamento:** puoi ordinare l’elenco Bloccati in ordine crescente o decrescente. Per farlo, fai clic sulla freccia accanto a **Nome tag**.

  ![blocca tag](assets/blocklist.gif)

  >[!NOTE]
  >
  >Quando aggiungi un tag nell’elenco Bloccati, non utilizzare caratteri speciali. Puoi utilizzare caratteri quali a-z, A-Z, 0-9 e -.

### Esportare un elenco Bloccati{#export-blocklist}

La vista Assets consente di esportare i tag bloccati elencati in formato CSV. Per esportare l’elenco Bloccati, effettua le seguenti operazioni:

1. Fai clic su **[!UICONTROL Esporta come CSV]**.
1. Scegli la posizione appropriata per salvare il file CSV. Puoi anche rinominare il file in base alle esigenze.
1. Fai clic su **[!UICONTROL Salva]**. L’elenco esportato in formato CSV viene scaricato nel percorso selezionato.

### Importare un elenco Bloccati{#import-blocklist}

La vista Assets consente di importare tag bloccati da un’origine dati (CSV). Per importare l’elenco Bloccati, effettua le seguenti operazioni:

1. Fai clic su **[!UICONTROL Importa come CSV]**.
1. Scegli il file CSV dal tuo dispositivo. Fai clic su **[!UICONTROL Seleziona un file]** per passare al file dal dispositivo. In alternativa, puoi trascinare e rilasciare il file CSV dal dispositivo.
1. Fai clic su **[!UICONTROL Carica]**. I tag dal file CSV vengono inseriti nell’elenco dei tag bloccati.

   ![Importa elenco dei tag bloccati](assets/import-blocked-tags.png)

Per scaricare un modello di tag bloccati, effettua le seguenti operazioni:

1. Fai clic su **[!UICONTROL Scarica modello]**.
1. Scegli la posizione appropriata per salvare il file CSV. Puoi anche rinominare il file in base alle esigenze.
1. Fai clic su **[!UICONTROL Salva]**. I modelli dei tag bloccati in formato CSV vengono scaricati nella posizione selezionata.
