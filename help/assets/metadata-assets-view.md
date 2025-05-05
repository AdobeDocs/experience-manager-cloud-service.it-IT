---
title: Come si gestiscono i metadati nella vista Assets?
description: Scopri come gestire i metadati nella vista Assets. Una migliore gestione dei metadati rende una risorsa più accessibile, facile da gestire e completa.
role: User, Leader, Admin, Architect, Developer
contentOwner: AG
exl-id: 7264e8d1-fc8f-4eb3-93a9-a6066ca3f851
feature: Metadata
source-git-commit: 6d729c8e7f84dccce9c11f1ca13553763d0547f8
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 79%

---

# Metadati in Visualizza Risorse {#metadata}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilitare Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Con metadati si intendono i dati o la descrizione dei dati. Ad esempio, le immagini come risorsa possono contenere informazioni sulla fotocamera con cui sono state scattate o su eventuale copyright. Queste informazioni sono metadati dell’immagine. I metadati sono fondamentali per una gestione efficiente delle risorse. I metadati raccolgono tutti i dati disponibili per una risorsa, ma non sono necessariamente contenuti in essa.

I metadati consentono di categorizzare ulteriormente le risorse, cosa molto utile con il crescere della quantità di informazioni digitali. Ricorrendo solo ai nomi dei file, alle miniature e alla memoria dell’utente, è possibile gestire alcune centinaia di file. Tuttavia, questo approccio non è scalabile. E diventa praticamente inutile quando aumentano sia il numero di persone coinvolte che il numero di attività gestite.

Con l’aggiunta dei metadati, il valore di una risorsa digitale aumenta, perché la risorsa diventa:

* Più accessibile: i sistemi e gli utenti possono trovarla facilmente.
* Più semplice da gestire: puoi trovare e modificare più facilmente le risorse che hanno uno stesso set di proprietà.
* Completa: la risorsa contiene più informazioni e contesto grazie a un maggior numero di metadati.

Per questi motivi, Assets offre i mezzi giusti per creare, gestire e scambiare metadati per le risorse digitali.

## Visualizzare i metadati {#view-metadata}

Per visualizzare i metadati di una risorsa, cerca la risorsa, selezionala e fai clic su **[!UICONTROL Dettagli]** nella barra degli strumenti.

![Visualizzare i metadati di una risorsa](assets/metadata-view.png)

*Figura: per visualizzare una risorsa e i relativi metadati, fai clic su **[!UICONTROL Dettagli]** nella barra degli strumenti o fai doppio clic sulla risorsa.*

I metadati di base quali titolo, descrizione e data di caricamento sono disponibili nella scheda [!UICONTROL Base]. La scheda [!UICONTROL Avanzate] contiene metadati più avanzati, ad esempio il modello della fotocamera, i dettagli dell’obiettivo e i geotag. La scheda [!UICONTROL Tag] contiene tag applicati automaticamente in base al contenuto dell’immagine.

## Aggiornare i metadati {#update-metadata}

Una volta che l’amministratore ha configurato il modulo metadati, è possibile aggiornare manualmente gli altri campi. Potrebbe essere utile modificare tale impostazione, in quanto viene letta solo in base al modulo di metadati predefinito.

## Tag avanzati {#smart-tags}

[!DNL Experience Manager Assets] utilizza l’intelligenza artificiale fornita da [Adobe Sensei](https://www.adobe.com/it/sensei.html) per applicare automaticamente tag rilevanti a tutte le risorse caricate. Questi tag, o “tag avanzati”, consentono di velocizzare le attività relative ai contenuti dei progetti grazie alla possibilità di trovare rapidamente le risorse rilevanti. I tag avanzati sono un esempio di metadati non contenuti nell’immagine.

I tag avanzati vengono applicati quasi in tempo reale e vengono generati in base al contenuto dell’immagine. Quando carichi una risorsa, sulla sua miniatura viene inizialmente visualizzata la dicitura [!UICONTROL In elaborazione]. Una volta completata l’elaborazione, puoi [visualizzare i metadati](#view-metadata) e i tag avanzati.

![Visualizzare i tag avanzati di una risorsa](assets/metadata-view-tags.png)

*Figura: per visualizzare i tag avanzati di una risorsa, fai clic su **[!UICONTROL Dettagli]** nella barra degli strumenti o fai doppio clic sulla risorsa.*

I tag avanzati contengono anche un punteggio di affidabilità in percentuale. Indica l’affidabilità associata al tag applicato. È possibile moderare i tag avanzati applicati automaticamente.

## Aggiungere o aggiornare le parole chiave {#manually-tag}

Puoi aggiungere più tag alle risorse, oltre ai tag avanzati che vengono aggiunti automaticamente utilizzando servizio intelligente [!DNL Adobe Sensei]. Apri una risorsa per l’anteprima, fai clic su [!UICONTROL Tag] e digita le parole chiave desiderate nel campo [!UICONTROL Parole chiave]. Per aggiungere il tag, premi Invio. [!DNL Assets view] indicizza la parola chiave quasi in tempo reale e dopo poco il tuo team può già cercare le risorse aggiornate utilizzando le nuove parole chiave.

Dalla sezione [!UICONTROL Tag avanzati] puoi anche rimuovere i tag aggiunti automaticamente da [!DNL Assets view] a tutte le risorse caricate.

## Gestione della tassonomia {#taxonomy-management}

I tag possono anche essere nidificati in una gerarchia per supportare relazioni come categoria e sottocategoria. Se devi inserire dei tag gerarchici, questi vengono facilmente gestiti dall’amministratore nella sezione [!UICONTROL Gestione tassonomia] delle [!UICONTROL Impostazioni]. Puoi creare un set regolamentato di spazi dei nomi e tag a cui tutti gli utenti possono accedere per l’utilizzo durante la descrizione del contenuto. Solo gli amministratori possono impostare gerarchie di tag nella [!UICONTROL Gestione tassonomia] garantendo che i valori siano controllati e utilizzati in modo coerente.

## Configurare i moduli di metadati {#metadata-forms}

>[!CONTEXTUALHELP]
>id="assets_metadata_forms"
>title="Moduli di metadati"
>abstract="[!DNL Experience Manager Assets] fornisce molti campi di metadati standard per impostazione predefinita. Le organizzazioni hanno l’esigenza di aggiungere altri metadati e ulteriori campi di metadati, specifici per l’azienda. I moduli di metadati consentono alle aziende di aggiungere campi di metadati personalizzati alla pagina Dettagli di una risorsa. I metadati specifici per l’azienda migliorano la governance e l’individuazione delle risorse."

La vista Assets fornisce molti campi di metadati standard per impostazione predefinita. Spesso le organizzazioni hanno l’esigenza di aggiungere altri metadati, specifici per l’azienda. I moduli di metadati consentono alle aziende di aggiungere campi di metadati personalizzati alla pagina [!UICONTROL Dettagli] di una risorsa. I metadati specifici per l’azienda migliorano la governance e l’individuazione delle risorse. Puoi creare nuovi moduli o riutilizzare quelli esistenti.

Puoi configurare i moduli di metadati per diversi tipi di risorse (diversi tipi MIME). Utilizza un modulo con lo stesso nome del tipo MIME del file. La vista Assets fa corrispondere automaticamente il tipo MIME delle risorse caricate al nome del modulo e aggiorna i metadati delle risorse caricate in base ai campi del modulo.
<!--
For example, if a metadata form by the name `PDF` or `pdf` exists, then the uploaded PDF documents contain metadata fields as defined in the form.
-->
La vista Assets utilizza la seguente sequenza per cercare i nomi dei moduli di metadati esistenti per applicare i campi di metadati alle risorse caricate di un particolare tipo:

Sottotipo MIME > Tipo MIME > Modulo `default` > Modulo fornito con il prodotto

Ad esempio, se è presente un modulo di metadati denominato `PDF` o `pdf`, i documenti PDF caricati contengono i campi di metadati definiti in tale modulo. Se non esiste un modulo di metadati denominato `PDF` o `pdf`, la visualizzazione di Assets corrisponde a quella del modulo di metadati denominato `application`. Se è presente un modulo metadati denominato `application`, i documenti PDF caricati contengono campi di metadati definiti nel modulo. Se la visualizzazione Assets non trova un modulo di metadati corrispondente, cerca il modulo di metadati `default` per applicare ai documenti PDF caricati i campi di metadati definiti nel modulo. Se nessuno di questi passaggi funziona, la vista Assets applica a tutti i documenti PDF caricati i campi di metadati definiti nel modulo fornito con il prodotto.
Tuttavia, se desideri assegnare un modulo di metadati a una cartella [vedi](#assign-metadata-form-folder).

>[!IMPORTANT]
>
>Un nuovo modulo di metadati per un tipo di file specifico sostituisce interamente quello predefinito fornito da [!DNL Assets view]. Se elimini o rinomini un modulo di metadati, i campi di metadati predefiniti diventano di nuovo disponibili per le nuove risorse.

Per creare un modulo di metadati, effettua le seguenti operazioni:

1. Nella barra a sinistra, fai clic su **[!UICONTROL Impostazioni]** > **[!UICONTROL Moduli metadati]**.

   ![opzione Moduli di metadati nella barra laterale a sinistra](assets/metadata-forms-sidebar.png)

1. Fai clic su **[!UICONTROL Crea]** in alto a destra nell’interfaccia utente.
1. Assegna un nome al modulo, quindi fai clic su **[!UICONTROL Crea]**.
1. Nella barra a destra, specifica un nome per la scheda in **[!UICONTROL Impostazioni]**.
1. Da **[!UICONTROL Componenti]** nella barra a sinistra, trascina i componenti richiesti su una scheda del modulo. Trascina i componenti nella sequenza desiderata.

   ![opzione oduli di metadati nella barra laterale a sinistra](assets/metadata-form-new.png)

   *Figura: Interfaccia per la creazione di moduli di metadati, con opzioni che consentono di aggiungere componenti e visualizzare l’anteprima del modulo.*

1. Per ogni componente, specifica un nome nelle **[!UICONTROL Impostazioni]** nella barra a destra e una mappatura con le proprietà supportate.
1. Se necessario, per un singolo componente, seleziona **[!UICONTROL Obbligatorio]** per rendere obbligatorio il campo di metadati e seleziona **[!UICONTROL Solo lettura]** per impedire la modifica del campo nella pagina [!UICONTROL Dettagli] della risorsa.
1. Se necessario, fai clic su **[!UICONTROL Anteprima]** per visualizzare in anteprima il modulo che stai creando.
1. Se necessario, aggiungi altre schede e i relativi componenti in ogni scheda.
1. Dopo aver completato il modulo, fai clic su **[!UICONTROL Salva]**.

Guarda questo video per visualizzare la sequenza di passaggi:

>[!VIDEO](https://video.tv.adobe.com/v/341275)

Dopo aver creato il modulo, quest’ultimo viene applicato automaticamente quando gli utenti caricano una risorsa del tipo MIME corrispondente.

Per creare un nuovo modulo riutilizzandone uno esistente, seleziona un modulo di metadati e fai clic su **[!UICONTROL Copia]** nella barra degli strumenti, specifica un nome e fai clic su **[!UICONTROL Conferma]**. A questo punto puoi modificare il modulo di metadati. Quando modifichi un modulo, quest’ultimo viene utilizzato per le risorse caricate in seguito alla modifica. L’operazione non modifica le risorse esistenti.

### Componenti proprietà {#property-components}

Puoi personalizzare il modulo metadati utilizzando uno dei seguenti componenti proprietà. Trascina il tipo di componente sul modulo nella posizione desiderata e modifica le impostazioni del componente.
Di seguito è riportata una panoramica di ciascun tipo di proprietà e della relativa modalità di archiviazione.

| Nome componente | Descrizione |
|---|---|
| Contenitore pannello a soffietto | Aggiungi un’intestazione comprimibile per un elenco di proprietà e componenti comuni. Per impostazione predefinita, può essere espanso o compresso. |
| Testo su riga singola | Aggiungi una proprietà di testo a riga singola. |
| Testo su più righe | Aggiungi più righe di testo o un paragrafo. Si espande quando un utente digita per contenere tutto il contenuto. |
| Testo con più valori | Aggiungi una proprietà di testo con più valori. |
| Numero | Aggiungi un componente numero. |
| Casella di selezione | Aggiungi un valore booleano. Memorizzato come TRUE o FALSE dopo il salvataggio di un valore. |
| Data | Aggiungi un componente data. |
| Elenchi a discesa | Aggiungi un elenco a discesa. |
| Stato | Aggiungi la proprietà dello stato del repository (mappata a repo:state) |
| Stato risorsa | Aggiungi la proprietà predefinita Stato risorsa (mappata a dam:assetStatus) |
| Tag | Aggiungi un tag dai valori memorizzati in Gestione tassonomia (mappato a xcm:tags). |
| Parole chiave | Aggiungi parole chiave in formato libero (mappate a dc:subject). |
| Tag avanzati | Migliora le funzionalità di ricerca aggiungendo automaticamente tag di metadati. |

### Assegnare un modulo di metadati a una cartella {#assign-metadata-form-folder}

Puoi anche assegnare un modulo di metadati a una cartella all’interno della distribuzione della vista Assets. Il modulo di metadati assegnato a una cartella in base al tipo MIME viene sovrascritto quando si applica manualmente un modulo di metadati a una cartella. Per tutte le risorse nella cartella, comprese le risorse nelle sottocartelle, vengono quindi visualizzate le proprietà definite nel modulo di metadati.

Per assegnare un modulo di metadati a una cartella:

1. Passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Moduli di metadati]** e seleziona un modulo di metadati.

2. Fai clic su **[!UICONTROL Assegna a cartella]**.

3. Selezionare la cartella e fare clic su **[!UICONTROL Assegna]**. Puoi selezionare le cartelle facendo clic sui nomi delle cartelle.

   ![assegnare un modulo di metadati a una cartella](assets/assign-to-folder.png)

   Per assegnare un modulo di metadati alla cartella, puoi anche passare alla pagina dei dettagli della cartella e selezionare un modulo di metadati dalle proprietà della cartella, nel riquadro a destra.

   ![Modulo metadati da proprietà cartella](assets/metadata-from-folder-props.png)

### Rimuovere un modulo metadati dalle cartelle {#remove-metadata-form-folder}

Dopo aver assegnato un modulo metadati a una o più cartelle, Experience Manager Assets consente inoltre di rimuovere il modulo metadati dalle cartelle selezionate.

Per rimuovere un modulo di metadati da una cartella:

1. Passa a **[!UICONTROL Impostazioni]** > **[!UICONTROL Moduli di metadati]** e seleziona un modulo di metadati.

1. Fai clic su **[!UICONTROL Rimuovi da cartelle]**. Viene visualizzato l’elenco delle cartelle assegnate al modulo di metadati.

1. Seleziona la cartella e fai clic su **[!UICONTROL Rimuovi]**. È anche possibile selezionare più cartelle dall’elenco.

Puoi passare anche alla pagina dei dettagli della cartella e selezionare **[!UICONTROL Modulo di metadati mappato dal sistema]** dal campo **[!UICONTROL Moduli di metadati]**, per rimuovere il modulo di metadati assegnato da una cartella.

### Utilizzare il componente Collegamento nel modulo di metadati {#link-component-metadata-form}

Il componente Collegamento viene utilizzato per abilitare URL esterni, tra cui link di archiviazione, informazioni sul copyright, moduli di contatto e così via. Per utilizzare il componente Collega nel modulo metadati, devi [configurare il modulo metadati](#metadata-forms).

Per utilizzare il componente Collega nel modulo metadati, segui i passaggi seguenti:

1. Passa alla pagina dei dettagli della risorsa, quindi a **[!UICONTROL URL collegamento]**.
1. Aggiungi un URL da utilizzare per il reindirizzamento della risorsa selezionata.
1. Fai clic su **[!UICONTROL Aggiungi collegamento]**. Effettua una delle seguenti operazioni:
   * Fai clic su ![icona copia](assets/do-not-localize/copy.svg) per copiare l’URL.
   * Fai clic su ![icona modifica](assets/do-not-localize/edit.svg) per modificare l’URL.
1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.


### Utilizzo del componente Tag nel modulo metadati {#tag-component-metadata-form}

L’elemento principale rappresenta la struttura ad albero dei tag che è possibile associare alle risorse, per identificare la risorsa in base al tag assegnato. Inoltre, puoi limitare l’accesso a una tassonomia specifica durante la configurazione del modulo metadati nell’editor metadati.

#### Configurazione del componente Tag {#tags-component-configuration}

Configura il componente Tag eseguendo i passaggi seguenti:

1. Vai all&#39;editor metadati, passa a **[!UICONTROL Tag]** e inseriscilo nell&#39;area di lavoro.
1. Rinomina il componente nell’area di lavoro. A questo scopo, vai a **[!UICONTROL Etichetta]** sotto la [!UICONTROL proprietà metadati] nel pannello delle impostazioni e aggiungi il testo per la sua identificazione.
1. Nella [!UICONTROL proprietà metadati] nel pannello delle impostazioni, cerca la proprietà metadati che desideri assegnare al componente.
1. Fare clic su **[!UICONTROL Limita a tassonomia specifica]** per limitare il percorso della directory principale della tassonomia. A questo scopo, sfoglia i tag e scegli la tassonomia del percorso specifico.
1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

   ![Configurazione tag radice](assets/root-tag-config.png)

1. [Assegna modulo metadati alle cartelle](#assign-metadata-form-folder).

<!--
#### Mapping between assets and taxonomy {#asset-taxonomy-mapping}

See [Assign metadata form to folders](#assign-metadata-form-folder). Follow the steps below to perform mapping between folder and taxonomy:

1. Go back to the Settings and click **[!UICONTROL Metadata forms]** 
1. Select a Metadata form that needs mapping. 
1. Click **[!UICONTROL Assign to folder(s)]**. **[!UICONTROL Select Folder(s)]** screen appears. 
1. Navigate to the folder that you want to assign to the metadata form. You can select multiple folders.
1. Click **[!UICONTROL Assign]**.
-->

Per visualizzare i tag principali configurati, vai alla pagina dei dettagli della risorsa in cui viene eseguito il mapping tra il modulo di metadati e i tag principali.

## Passaggi successivi {#next-steps}

* [Guarda un video per gestire i moduli di metadati nella visualizzazione Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=it)

* Fornisci feedback sui prodotti utilizzando l’opzione [!UICONTROL Feedback] disponibile nell’interfaccia utente della vista Risorse

* Fornisci feedback alla documentazione utilizzando [!UICONTROL Modifica questa pagina] ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema] ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibile sulla barra laterale destra

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/it?support-solution=General&amp;lang=it#support)

<!-- TBD: Cannot create a form using the second option. Documenting only the first option for now.
To reuse an existing form to create a form, do one of these:

* Select a metadata form and click **[!UICONTROL Copy]** from the toolbar, provide a name, and click **[!UICONTROL Confirm]**.

* Click **[!UICONTROL Create]**, select **[!UICONTROL Use existing form structure as template]** option, and select an existing form. 
-->

<!-- TBD: Queries for PM and engg.

Can we edit the existing metadata in any form?

How to moderate smart tags?

Allow or deny list for smart tags?

What about Tags displayed just above Smart Tags in the UI?

Is there a detailed metadata tab. Where do the other details of an asset go?

How can one search based strictly on the metadata. Similar to AEM Assets GQL queries.
-->

<!-- TBD: Link to related articles if any.

>[!MORELIKETHIS]
>
>* [Search assets](search.md).
-->

