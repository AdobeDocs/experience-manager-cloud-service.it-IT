---
title: Consente di gestire i contenuti digitali
description: Scopri vari metodi di gestione e modifica delle risorse
contentOwner: AG
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: 42298e0ff7d977a32c87e61e9e1f4b02a846f2c0
workflow-type: tm+mt
source-wordcount: '4326'
ht-degree: 12%

---

# Gestire le risorse {#manage-assets}

Questo articolo descrive come gestire e modificare le risorse in [!DNL Adobe Experience Manager Assets]. Per gestire [!DNL Content Fragments], vedi [[!DNL Content Fragments]](content-fragments/content-fragments.md) risorse.

## Creare cartelle {#creating-folders}

Quando si organizza una raccolta di risorse, ad esempio, tutte le `Nature` immagini, puoi creare cartelle per mantenerle unite. Puoi utilizzare le cartelle per suddividere in categorie e organizzare le risorse. [!DNL Experience Manager Assets] non richiede di organizzare meglio le risorse nelle cartelle.

>[!NOTE]
>
>* Condivisione di una cartella di risorse del tipo `sling:OrderedFolder`, non è supportato quando si condivide con Experience Cloud. Se desideri condividere una cartella, non selezionare [!UICONTROL Ordinato] durante la creazione di una cartella.
>* L&#39;Experience Manager non consente di utilizzare `subassets` parola come nome di una cartella. È una parola chiave riservata al nodo che contiene risorse secondarie per le risorse composte


1. Passa alla posizione nella cartella delle risorse digitali in cui desideri creare una nuova cartella. Nel menu , fai clic su **[!UICONTROL Crea]**. Seleziona **[!UICONTROL Nuova cartella]**.
1. In **[!UICONTROL Titolo]** specificare un nome di cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, è possibile sostituire l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

I seguenti caratteri (elenco separato da spazi) non sono supportati:

* Il nome di un file di risorsa non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? &`
* Il nome di una cartella di risorse non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricare le risorse {#uploading-assets}

Vedi [aggiungere risorse digitali ad Experience Manager](add-assets.md).

## Rileva risorse duplicate {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Se un utente DAM carica una o più risorse già esistenti nell’archivio, [!DNL Experience Manager] rileva la duplicazione e notifica l’utente. Il rilevamento dei duplicati è disattivato per impostazione predefinita in quanto può avere un impatto sulle prestazioni a seconda delle dimensioni dell’archivio e del numero di risorse caricate.

Per abilitare la funzione:

1. Passa a **[!UICONTROL Strumenti > Risorse > Configurazioni risorse]**.

1. Fai clic su **[!UICONTROL Rilevatore di duplicazione delle risorse]**.

1. Sulla [!UICONTROL Pagina del rilevatore della duplicazione delle risorse], fai clic su **[!UICONTROL Abilitato]**.

   `dam:sha1` Il valore per il campo Rileva metadati garantisce che le risorse duplicate vengano rilevate anche se i nomi dei file sono diversi.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Se hai configurato il rilevatore di duplicazione utilizzando `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` file di configurazione (configurazione OSGi), è possibile continuare a utilizzarlo, tuttavia, Adobe consiglia di utilizzare il nuovo metodo.


Una volta attivato, Experience Manager invia le notifiche delle risorse duplicate alla casella in entrata dell’Experience Manager. È un risultato aggregato per più duplicati. Gli utenti possono scegliere di rimuovere le risorse in base ai risultati.

![Notifica della casella in entrata per le risorse duplicate](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Quando carichi le risorse nell’archivio, Experience Manager rileva le duplicazioni e notifica le prime 100 risorse duplicate.

## Visualizzare l’anteprima delle risorse {#previewing-assets}

Per visualizzare l’anteprima di una risorsa, effettua le seguenti operazioni.

1. Dall’interfaccia utente Assets, individua il percorso della risorsa da visualizzare in anteprima.
1. Tocca la risorsa desiderata per aprirla.

1. Nella modalità di anteprima sono disponibili le opzioni di zoom per [Tipi di immagini supportati](/help/assets/file-format-support.md) (con modifica interattiva).

   Per ingrandire una risorsa, tocca o fai clic su `+` oppure tocca o fai clic sulla lente di ingrandimento sulla risorsa. Per ridurre lo zoom, tocca o fai clic su `-`. Quando ingrandisci, puoi osservare da vicino qualsiasi area dell&#39;immagine tramite panoramica. La freccia di reimpostazione dello zoom consente di tornare alla visualizzazione originale.

   Tocca **[!UICONTROL Reimposta]** per ripristinare le dimensioni originali della visualizzazione.

## Modifica delle proprietà {#editing-properties}

1. Andate alla posizione della risorsa di cui desiderate modificare i metadati.

1. Seleziona la risorsa e tocca o fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti per visualizzare le proprietà della risorsa. In alternativa, scegli la **[!UICONTROL Proprietà]** azione rapida sulla scheda delle risorse.

   ![properties_quickaction](assets/properties_quickaction.png)

1. In [!UICONTROL Proprietà] , modifica le proprietà dei metadati in varie schede. Ad esempio, sotto il **[!UICONTROL Base]** , modifica il titolo, la descrizione e così via.

   >[!NOTE]
   >
   >Il layout del [!UICONTROL Proprietà] le proprietà di pagina e metadati disponibili dipendono dallo schema di metadati sottostante. Per scoprire come modificare il layout del [!UICONTROL Proprietà] pagina, vedi [Schemi metadati](/help/assets/metadata-schemas.md).

1. Per pianificare una data/ora specifica per l’attivazione della risorsa, utilizza il selettore data posto accanto al campo **[!UICONTROL On Time (All’ora)]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Per disattivare la risorsa dopo una determinata durata, scegli la data/ora di disattivazione dal selettore data accanto al **[!UICONTROL Ora di disattivazione]** campo . La data di disattivazione deve essere successiva alla data di attivazione di una risorsa. Dopo la [!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili né tramite l’interfaccia web Assets né tramite l’API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. In **[!UICONTROL Tag]** selezionare uno o più tag. Per aggiungere un tag personalizzato, digita il nome del tag nella casella e seleziona la `Enter` chiave. Il nuovo tag viene salvato in [!DNL Experience Manager].

   YouTube richiede la pubblicazione dei tag e dispone di un collegamento ad YouTube (se è possibile trovare un collegamento adatto).

   >[!NOTE]
   >
   >Per creare i tag, è necessario disporre dell’autorizzazione di scrittura in `/content/cq:tags/default` nel repository CRX.

1. Tocca o fai clic su **[!UICONTROL Salva e chiudi]**.

1. Passa all’interfaccia utente Assets. Le proprietà dei metadati modificate, inclusi titolo, descrizione e tag, vengono visualizzate sulla scheda delle risorse nella vista Scheda e nelle relative colonne nella vista Elenco.

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Assets Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## Copiare le risorse {#copying-assets}

Quando copi una risorsa o una cartella, viene copiata l’intera risorsa o la cartella insieme alla relativa struttura del contenuto. Una risorsa o una cartella copiata viene duplicata nel percorso di destinazione. La risorsa nella posizione di origine non viene modificata.

Alcuni attributi univoci per una particolare copia di una risorsa non vengono riportati in avanti. Alcuni esempi sono:

* ID risorsa, data e ora di creazione, versioni e cronologia delle versioni. Alcune di queste proprietà sono indicate dalle proprietà `jcr:uuid`, `jcr:created`e `cq:name`.

* L’ora di creazione e i percorsi di riferimento sono univoci per ogni risorsa e per ogni suo rendering.

Le altre proprietà e informazioni sui metadati vengono mantenute. Non viene creata una copia parziale durante la copia di una risorsa.

1. Dall’interfaccia utente Assets, seleziona una o più risorse, quindi tocca o fai clic sul pulsante **[!UICONTROL Copia]** dalla barra degli strumenti. In alternativa, seleziona la **[!UICONTROL Copia]** ![copy_icon](assets/copy_icon.png) azione rapida dalla scheda delle risorse.

   >[!NOTE]
   >
   >Se utilizzi [!UICONTROL Copia] azione rapida, puoi copiare una sola risorsa alla volta.

1. Andate alla posizione in cui desiderate copiare le risorse.

   >[!NOTE]
   >
   >Se copi una risorsa nella stessa posizione, [!DNL Experience Manager] genera automaticamente una variante del nome. Ad esempio, se copi una risorsa con titolo `Square`, [!DNL Experience Manager] genera automaticamente il titolo per la relativa copia come `Square1`.

1. Fai clic sul pulsante **[!UICONTROL Incolla]** icona della risorsa dalla barra degli strumenti. Le risorse vengono copiate in questa posizione.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >La **[!UICONTROL Incolla]** l’icona è disponibile nella barra degli strumenti fino al completamento dell’operazione Incolla .

### Spostare o rinominare le risorse {#moving-or-renaming-assets}

1. Andate alla posizione della risorsa da spostare.

1. Seleziona la risorsa e tocca o fai clic sul pulsante **[!UICONTROL Sposta]** icona ![move_icon](assets/move_icon.png) dalla barra degli strumenti.

1. Nella procedura guidata Sposta risorse , effettua una delle seguenti operazioni:

   * Specifica il nome della risorsa dopo averlo spostata. Quindi tocca o fai clic su **[!UICONTROL Successivo]** per procedere.

   * Tocca o fai clic su **[!UICONTROL Annulla]** per interrompere il processo.
   >[!NOTE]
   >
   >* Potete specificare lo stesso nome per la risorsa se nella nuova posizione non è presente alcuna risorsa con tale nome. Tuttavia, se sposti la risorsa in una posizione in cui esiste una risorsa con lo stesso nome, utilizza un nome diverso. Se utilizzi lo stesso nome, il sistema genera automaticamente una variante del nome. Ad esempio, se la risorsa ha il nome Square, il sistema genera il nome Square1 per la relativa copia.
   >* Durante la ridenominazione, lo spazio vuoto non è consentito nel nome del file.


1. Sulla **[!UICONTROL Seleziona destinazione]** eseguire una delle operazioni seguenti:

   * Passa alla nuova posizione delle risorse, quindi tocca o fai clic su **[!UICONTROL Successivo]** per procedere.

   * Tocca o fai clic su **[!UICONTROL Indietro]** per tornare al **[!UICONTROL Rinomina]** schermo.

1. Se le risorse che stai spostando dispongono di pagine, risorse o raccolte di riferimento, la **[!UICONTROL Regolare i riferimenti]** accanto alla scheda **[!UICONTROL Seleziona destinazione]** scheda .

   Effettua una delle seguenti operazioni nel **[!UICONTROL Regolare i riferimenti]** schermo:

   * Specifica i riferimenti da regolare in base ai nuovi dettagli, quindi tocca o fai clic su **[!UICONTROL Sposta]** per procedere.

   * Da **[!UICONTROL Regola]** , seleziona o deseleziona i riferimenti alle risorse.
   * Tocca o fai clic su **[!UICONTROL Indietro]** per tornare al **[!UICONTROL Seleziona destinazione]** schermo.

   * Tocca o fai clic su **[!UICONTROL Annulla]** per interrompere l&#39;operazione di spostamento.

   Se non aggiorni i riferimenti, continuano a indicare il percorso precedente della risorsa. Se regoli i riferimenti, vengono aggiornati al nuovo percorso della risorsa.

### Gestire le rappresentazioni {#managing-renditions}

1. Puoi aggiungere o rimuovere rappresentazioni per una risorsa, tranne l’originale. Passa alla posizione della risorsa per la quale desideri aggiungere o rimuovere rappresentazioni.

1. Tocca o fai clic sulla risorsa per aprire la relativa pagina di risorse.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Tocca o fai clic sull’icona di Navigazione globale e seleziona **[!UICONTROL Rendering]** dall&#39;elenco.

   ![renditions_menu](assets/renditions_menu.png)

1. In **[!UICONTROL Rendering]** Visualizza l’elenco delle rappresentazioni generate per la risorsa.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, [!DNL Experience Manager Assets] non visualizza il rendering originale della risorsa in modalità anteprima. Gli amministratori possono utilizzare le sovrapposizioni per configurare [!DNL Assets] per visualizzare le rappresentazioni originali in modalità anteprima.

1. Selezionare un rendering per visualizzare o eliminare il rendering.

   **Eliminazione di un rendering**

   Selezionare un rendering dal **[!UICONTROL Rendering]** , quindi tocca o fai clic sul **[!UICONTROL Elimina rappresentazione]** dalla barra degli strumenti. Le rappresentazioni non possono essere eliminate in blocco al termine dell’elaborazione delle risorse. Per le singole risorse, puoi rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, puoi personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche o eliminare le risorse e ricaricare le risorse eliminate.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Caricamento di un nuovo rendering**

   Vai alla pagina dei dettagli della risorsa, quindi tocca o fai clic sull’icona **[!UICONTROL Aggiungi rappresentazione]** della barra degli strumenti per caricare una nuova rappresentazione della risorsa.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Se selezioni un rendering dal pannello **[!UICONTROL Rendering]**, la barra degli strumenti cambia contesto, visualizzando solo le azioni del rendering specifico. Le opzioni non sono visualizzate, ad esempio l’icona Carica rappresentazione. Per visualizzare queste opzioni nella barra degli strumenti, vai alla pagina dei dettagli della risorsa.

   Puoi configurare le dimensioni per il rendering da visualizzare nella pagina dei dettagli di un’immagine o di una risorsa video. In base alle dimensioni specificate, Assets visualizza il rendering con le dimensioni esatte o più vicine.

   Per configurare le dimensioni di rendering di un’immagine a livello di dettaglio della risorsa, sovrapponi il nodo `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configura il valore della proprietà larghezza.  Per personalizzare il rendering sulla pagina dei dettagli della risorsa in base alle dimensioni dell’immagine, configura la proprietà **[!UICONTROL size (Long) in KB (dimensione (lunga) in KB)]** al posto della larghezza. Per la personalizzazione basata sulle dimensioni, la proprietà `preferOriginal` assegna le preferenze all’originale se la dimensione del rendering corrispondente è maggiore.

   Allo stesso modo, è possibile personalizzare l&#39;immagine della pagina Annotazione sovrapponendo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Per configurare le dimensioni di rendering per una risorsa video, passa alla `videopicker` nodo nell&#39;archivio CRX nella posizione `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sovrapponi il nodo e quindi modifica la proprietà appropriata.

   >[!NOTE]
   >
   >Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. Inoltre, a seconda del browser, sono supportati diversi formati video. Tuttavia, il formato video MXF non è ancora supportato con le annotazioni video.

## Eliminare le risorse {#delete-assets}

Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiorna i riferimenti rilevanti prima di eliminare una risorsa.

Inoltre, disattiva il pulsante force delete utilizzando una sovrapposizione, per impedire agli utenti di eliminare le risorse di riferimento e di lasciare i collegamenti interrotti.

1. Andate alla posizione delle risorse che desiderate eliminare.

1. Seleziona la risorsa e fai clic su **[!UICONTROL Elimina]** ![delete_icon](assets/do-not-localize/delete-icon.png) dalla barra degli strumenti.

1. Nella finestra di dialogo di conferma, fai clic su:

   * **[!UICONTROL Annulla]** per interrompere l&#39;azione
   * **[!UICONTROL Elimina]** per confermare l’azione:

      * Se la risorsa non ha riferimenti, viene eliminata.
      * Se la risorsa dispone di riferimenti, un messaggio di errore segnala che **[!UICONTROL Riferimento a una o più risorse]**. Potete selezionare **[!UICONTROL Forza eliminazione]** o **[!UICONTROL Annulla]**.

   >[!NOTE]
   >
   >Per poter eliminare una risorsa è necessario disporre delle autorizzazioni di eliminazione per dam/asset. Se disponi solo di autorizzazioni di modifica, puoi modificare solo i metadati della risorsa e aggiungere annotazioni alla risorsa. Tuttavia, non puoi eliminare la risorsa o i relativi metadati.

   >[!NOTE]
   >
   >Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiorna i riferimenti rilevanti prima di eliminare una risorsa. È possibile impedire l’eliminazione delle risorse di riferimento in quanto causa collegamenti interrotti. Disattiva il pulsante di eliminazione forzata utilizzando una sovrapposizione.

## Scaricare le risorse {#download-assets}

Vedi [scaricare risorse da [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Pubblicare o annullare la pubblicazione delle risorse {#publish-assets}

1. Passa alla posizione della risorsa o della cartella di risorse che desideri pubblicare o che desideri rimuovere dall’ambiente di pubblicazione (Annulla pubblicazione).

1. Seleziona la risorsa o la cartella da pubblicare o di cui annullare la pubblicazione e seleziona **[!UICONTROL Gestisci pubblicazione]** ![opzione gestione pubblicazione](assets/do-not-localize/globe-publication.png) dalla barra degli strumenti. In alternativa, per pubblicare rapidamente, seleziona la **[!UICONTROL Pubblicazione rapida]** dalla barra degli strumenti. Se la cartella da pubblicare include una cartella vuota, questa non verrà pubblicata.

1. Seleziona la **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** se necessario.

   ![Annulla pubblicazione azione](assets/unpublish_action.png)
   *Figura: Opzioni di pubblicazione e annullamento della pubblicazione e opzione di pianificazione.*

1. Seleziona **[!UICONTROL Ora]** per agire immediatamente sulla risorsa o seleziona **[!UICONTROL Più tardi]** per pianificare l’azione. Seleziona una data e un’ora se scegli la **[!UICONTROL Più tardi]** opzione . Fai clic su **[!UICONTROL Avanti]**.

1. Durante la pubblicazione, se una risorsa fa riferimento ad altre risorse, i relativi riferimenti sono elencati nella procedura guidata. Vengono visualizzati solo i riferimenti, che vengono annullati o modificati dall’ultima pubblicazione. Scegli i riferimenti da pubblicare.

1. Quando si annulla la pubblicazione, se una risorsa fa riferimento ad altre risorse, scegliete i riferimenti di cui desiderate annullare la pubblicazione. Fai clic su **[!UICONTROL Annulla pubblicazione]**. Nella finestra di dialogo di conferma, fai clic su **[!UICONTROL Annulla]** per interrompere l’azione o fare clic su **[!UICONTROL Annulla pubblicazione]** per confermare l’annullamento della pubblicazione delle risorse alla data specificata.

Scopri i seguenti limiti e suggerimenti relativi alla pubblicazione o all’annullamento della pubblicazione di risorse o cartelle:

* L’opzione [!UICONTROL Gestisci pubblicazione] è disponibile solo per gli account utente che dispongono di autorizzazioni di replica.
* Quando si annulla la pubblicazione di una risorsa complessa, è necessario annullare la pubblicazione solo della risorsa. Evita di annullare la pubblicazione dei riferimenti, poiché altri contenuti pubblicati potrebbero farvi riferimento.
* Le cartelle vuote non vengono pubblicate.
* Se pubblichi una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano i rendering. Attendi il completamento dell’elaborazione, quindi pubblica o ripubblica la risorsa al termine dell’elaborazione.

## Gruppo utenti chiuso {#closed-user-group}

Un gruppo utenti chiuso (CUG) viene utilizzato per limitare l’accesso a specifiche cartelle di risorse pubblicate da [!DNL Experience Manager]. Se si crea un CUG per una cartella, l’accesso alla cartella (incluse le risorse della cartella e le sottocartelle) è limitato solo ai membri o ai gruppi assegnati. Per accedere alla cartella, è necessario che accedano utilizzando le proprie credenziali di sicurezza.

I gruppi di utenti chiusi rappresentano un modo aggiuntivo per limitare l’accesso alle risorse. Puoi anche configurare una pagina di accesso per la cartella.

1. Seleziona una cartella dall’interfaccia utente Assets, quindi tocca o fai clic sull’icona Proprietà nella barra degli strumenti per visualizzare la pagina delle proprietà.
1. Da **[!UICONTROL Autorizzazioni]** scheda aggiungi membri o gruppi in **[!UICONTROL Gruppo utenti chiuso]**.

   ![add_user](assets/add_user.png)

1. Per visualizzare una schermata di accesso quando gli utenti accedono alla cartella, seleziona la **[!UICONTROL Abilita]** opzione . Quindi, seleziona il percorso di una pagina di accesso in [!DNL Experience Manager]e salva le modifiche.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Se non si specifica il percorso di una pagina di accesso, [!DNL Experience Manager] visualizza la pagina di accesso predefinita nell’istanza di pubblicazione.

1. Pubblica la cartella e prova ad accedervi dall&#39;istanza di pubblicazione. Viene visualizzata una schermata di accesso.
1. Se sei un membro CUG, immetti le tue credenziali di sicurezza. La cartella viene visualizzata dopo [!DNL Experience Manager] ti autentica.

## Cercare risorse {#search-assets}

La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e dei professionisti del marketing, sia per l’amministrazione da parte degli amministratori DAM.

Per ricerche semplici, avanzate e personalizzate per scoprire e utilizzare le risorse più appropriate, consulta [cercare risorse in [!DNL Experience Manager]](/help/assets/search-assets.md).

## Azioni rapide {#quick-actions}

Le icone delle azioni rapide sono disponibili per una singola risorsa alla volta. A seconda del dispositivo, esegui le seguenti azioni per visualizzare le icone delle azioni rapide:

* Dispositivi touch: Toccare e tenere premuto. Ad esempio, in un iPad, puoi toccare e tenere premuto una risorsa per visualizzare le azioni rapide.
* Dispositivi non touch: Puntatore al passaggio del mouse. Ad esempio, su un dispositivo desktop, se passi il puntatore sulla miniatura della risorsa viene visualizzata la barra delle azioni rapide.

<!-- Hiding this topic via cqdoc-18707

## Edit images {#editing-images}

The editing tools in the [!DNL Experience Manager Assets] interface let you perform small editing jobs on image assets. You can crop, rotate, flip, and perform other editing jobs on images. You can also add image maps to assets.

>[!NOTE]
>
>For some components, the Full Screen mode has additional options available.

1. Do one of the following to open an asset in edit mode:

    * Select the asset and then click/tap the **[!UICONTROL Edit]** icon in the toolbar.
    * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
    * In the asset page, tap/click the **[!UICONTROL Edit]** icon in the toolbar.

   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Select the desired option from the list. The crop area appears on the image based on the option you choose. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Select the area to be cropped, and resize or reposition it on the image.
1. Use the **Finish** icon (top right corner) to crop the image. Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use the **Undo** and **Redo** icons on the top right to revert to the uncropped image or retain the cropped image, respectively.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Tap/click the appropriate Rotate icon to rotate the image clockwise or anti-clockwise.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Tap/click the appropriate Flip icon to flip the image horizontally or vertically.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>Image editing is supported for BMP, GIF, PNG, and JPEG files formats.

>[!NOTE]
>
>To edit a TXT file, set **Day CQ Link Externalizer** from Configuration Manager.
-->

## Timeline  {#timeline}

La timeline consente di visualizzare vari eventi per un elemento selezionato, ad esempio flussi di lavoro attivi per una risorsa, commenti/annotazioni, registri attività e versioni.

![Ordinare le voci della timeline per una risorsa](assets/sort_timeline.gif)
*Figura: Ordinare le voci della timeline per una risorsa*

>[!NOTE]
>
>In [Console Raccolte](/help/assets/manage-collections.md#navigate-the-collections-console), **[!UICONTROL Mostra tutto]** fornisce opzioni per visualizzare solo i commenti e i flussi di lavoro. Inoltre, la timeline viene visualizzata solo per le raccolte di primo livello elencate nella console. Non viene visualizzato se vi spostate all’interno di una qualsiasi delle raccolte.

>[!NOTE]
>
>La timeline contiene diversi [opzioni specifiche per i frammenti di contenuto](content-fragments/content-fragments.md).

## Annotare risorse {#annotating}

Le annotazioni sono commenti o note esplicative aggiunte a immagini o video. Le annotazioni consentono agli addetti al marketing di collaborare e lasciare un feedback sulle risorse.

Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. I formati video supportati da Assets dipendono dal browser. Tuttavia, il formato video MXF non è ancora supportato con le annotazioni video.

>[!NOTE]
>
>Per i frammenti di contenuto, [le annotazioni vengono create nell’editor frammenti](content-fragments/content-fragments.md).

1. Andate alla posizione della risorsa alla quale desiderate aggiungere annotazioni.
1. Tocca o fai clic sul pulsante **[!UICONTROL Annota]** da una delle seguenti icone:

   * [Azioni rapide](#quick-actions)
   * Dalla barra degli strumenti dopo aver selezionato la risorsa o essere passato alla pagina della risorsa

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Aggiungi un commento nella casella **[!UICONTROL Commento]** posta nella parte inferiore della timeline. In alternativa, contrassegna un’area sull’immagine e aggiungi un’annotazione nella finestra di dialogo **[!UICONTROL Aggiungi annotazione]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Per un utente non amministratore, i suggerimenti vengono visualizzati solo se l’utente dispone delle autorizzazioni di lettura in `/home` in CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. Dopo aver aggiunto l’annotazione, fai clic su **[!UICONTROL Aggiungi]** per salvarlo. Ad Aaron viene inviata una notifica relativa all’annotazione.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >È possibile aggiungere più annotazioni prima di salvarle.

1. Tocca o fai clic su **[!UICONTROL Chiudi]** per uscire dalla modalità Annotazione.
1. Per visualizzare la notifica, accedi a Assets con le credenziali di Aaron MacDonald e fai clic sul **[!UICONTROL Notifiche]** per visualizzare la notifica.

   >[!NOTE]
   >
   >Le annotazioni possono essere aggiunte anche alle risorse video. Durante l&#39;annotazione dei video, il lettore si mette in pausa per consentirvi di annotare un fotogramma. Per maggiori dettagli, vedi [gestione delle risorse video](manage-video-assets.md). Tuttavia, il formato video MXF non è ancora supportato con le annotazioni video.

1. Per scegliere un colore diverso per differenziare gli utenti, tocca o fai clic sull’icona Profilo e tocca o fai clic su **[!UICONTROL Preferenze]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Nella casella **[!UICONTROL Colore annotazione]**, specifica il colore desiderato, infine tocca o fai clic su **[!UICONTROL Accetta]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>È inoltre possibile aggiungere annotazioni a una raccolta. Tuttavia, se una raccolta contiene raccolte figlie, è possibile aggiungere annotazioni/commenti solo alla raccolta principale. L’opzione Annota non è disponibile per le raccolte figlio.

### Visualizzare le annotazioni salvate {#viewing-saved-annotations}

È possibile visualizzare una sola annotazione alla volta.

>[!NOTE]
>
>Se selezioni più annotazioni, l’ultima sarà visibile nell’interfaccia utente.
>
>La selezione multipla è supportata solo per la stampa della risorsa annotata come PDF.

1. Per visualizzare le annotazioni salvate per una risorsa, accedi alla posizione della risorsa e apri la pagina della risorsa.

1. Tocca o fai clic sull’icona di Navigazione globale e scegli **[!UICONTROL Timeline]** dall&#39;elenco.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. Dall’elenco **[!UICONTROL Mostra tutti]** nella timeline, seleziona **[!UICONTROL Commenti]** per filtrare i risultati in base alle annotazioni.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Tocca o fai clic su un commento nel **[!UICONTROL Timeline]** per visualizzare l’annotazione corrispondente sull’immagine.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Tocca o fai clic su **[!UICONTROL Elimina]**, per eliminare un particolare commento.

### Stampa annotazioni {#printing-annotations}

Se una risorsa dispone di annotazioni o è stata sottoposta a un flusso di lavoro di revisione, puoi stampare la risorsa insieme a annotazioni e rivederne lo stato come file PDF per la revisione offline.

È inoltre possibile scegliere di stampare solo le annotazioni o lo stato di revisione.

>[!NOTE]
>
>È possibile selezionare più annotazioni durante la stampa della risorsa annotata come PDF.

Per stampare le annotazioni e controllare lo stato, tocca o fai clic sul pulsante **[!UICONTROL Stampa]** e segui le istruzioni della procedura guidata. La **[!UICONTROL Stampa]** l’icona viene visualizzata nella barra degli strumenti solo quando alla risorsa è assegnata almeno un’annotazione o uno stato di revisione.

1. Dall’interfaccia utente Assets, apri la pagina di anteprima per una risorsa.
1. Effettua una delle operazioni seguenti:

   * Per stampare tutte le annotazioni e lo stato di revisione, saltare il passaggio 3 e passare direttamente al passaggio 4.
   * Per stampare annotazioni specifiche e controllare lo stato, aprire [timeline](/help/assets/manage-digital-assets.md#timeline) e poi andare al punto 3.

1. Per stampare annotazioni specifiche, selezionate le annotazioni nella timeline.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Per stampare solo lo stato di revisione, selezionarlo dalla timeline.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Stampa]** dalla barra degli strumenti.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Nella finestra di dialogo Stampa, scegliere la posizione in cui visualizzare le annotazioni o lo stato di revisione in PDF. Ad esempio, se desideri che le annotazioni o lo stato vengano stampati in alto a destra della pagina contenente l’immagine stampata, utilizza l’ **In alto a sinistra** impostazione. È selezionata per impostazione predefinita.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   È possibile scegliere altre impostazioni, a seconda della posizione in cui si desidera visualizzare le annotazioni o lo stato nel PDF stampato. Se vuoi che le annotazioni o lo stato vengano visualizzati in una pagina separata dalla risorsa stampata, scegli **[!UICONTROL Pagina successiva]**.

1. Fai clic su **[!UICONTROL Stampa]**. A seconda dell’opzione scelta al passaggio 2, il PDF generato visualizza annotazioni/stato nella posizione specificata. Ad esempio, se scegli di stampare sia le annotazioni che lo stato di revisione utilizzando l’impostazione **In alto a sinistra**, l’output generato sarà simile al file PDF qui riportato.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Scarica o stampa il PDF utilizzando le opzioni in alto a destra.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   Per modificare l’aspetto del file PDF renderizzato, ad esempio il colore, la dimensione e lo stile del font, il colore di sfondo dei commenti e degli stati, aprire il **[!UICONTROL Configurazione di Annotation PDF]** da Configuration Manager e modifica le opzioni desiderate. Ad esempio, per modificare il colore di visualizzazione dello stato approvato, modificare il codice del colore nel campo corrispondente. Per informazioni sulla modifica del colore del font delle annotazioni, consultare [Annotazione](/help/assets/manage-digital-assets.md#annotating).

   Torna al file PDF renderizzato e aggiornalo. Il PDF aggiornato riflette le modifiche apportate.

## Controllo delle versioni di una risorsa {#asset-versioning}

Il controllo delle versioni crea un’istantanea delle risorse digitali in un momento preciso. Il controllo delle versioni consente di ripristinare le risorse a uno stato precedente in un secondo momento. Ad esempio, per annullare una modifica apportata a una risorsa, ripristina la versione non modificata della risorsa.

Di seguito sono riportati gli scenari in cui si creano versioni:

* Puoi modificare un’immagine in un’altra applicazione e caricarla in Assets. Viene creata una versione dell’immagine in modo che l’immagine originale non venga sovrascritta.
* Puoi modificare i metadati di una risorsa.
* Utilizzate [!DNL Experience Manager] app desktop per estrarre una risorsa esistente e salvare le modifiche. A ogni salvataggio della risorsa viene creata una nuova versione.

È inoltre possibile abilitare il controllo delle versioni automatico tramite un flusso di lavoro. Quando crei una versione per una risorsa, i metadati e le rappresentazioni vengono salvati insieme alla versione. Le rappresentazioni sono alternative di rendering delle stesse immagini, ad esempio, una rappresentazione PNG di un file JPEG caricato.

La funzionalità di controllo delle versioni consente di effettuare le seguenti operazioni:

* Crea una versione di una risorsa.
* Visualizza la revisione corrente per una risorsa.
* Ripristina una versione precedente della risorsa.

1. Andate alla posizione della risorsa per la quale desiderate creare una versione e toccatela o fate clic per aprire la relativa pagina delle risorse.

1. Tocca o fai clic sull’icona di Navigazione globale e scegli **[!UICONTROL Timeline]** dal menu.

   ![timeline](assets/timeline.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Azioni]** Icona (freccia) nella parte inferiore per visualizzare le azioni disponibili sulla risorsa.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Tocca o fai clic su **[!UICONTROL Salva come versione]** per creare una versione della risorsa.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Aggiungi un&#39;etichetta e un commento, quindi fai clic su **[!UICONTROL Crea]** per creare una versione. In alternativa, tocca o fai clic su **Annulla** per uscire dall&#39;operazione.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Per visualizzare la nuova versione, apri l’elenco **[!UICONTROL Mostra tutti]** nella timeline dalla pagina dei dettagli della risorsa o dall’interfaccia utente Assets, quindi scegli **[!UICONTROL Versioni]**. Tutte le versioni create per una risorsa sono elencate nella scheda della timeline. Puoi filtrare l’elenco Versioni, facendo clic sulla freccia rivolta verso il basso e selezionando **[!UICONTROL Versioni]** dall’elenco.

   ![version_option](assets/versions_option.png)

1. Seleziona una versione specifica per la risorsa da visualizzare in anteprima o abilitare per visualizzarla nell’interfaccia utente di Assets.

   ![select_version](assets/select_version.png)

1. Aggiungi un’etichetta e un commento per la versione da ripristinare alla versione specifica nell’interfaccia utente di Assets.

   ![save_version](assets/save_version.png)

1. Per generare un’anteprima per la versione, tocca o fai clic su **[!UICONTROL Anteprima versione]**.
1. Per visualizzare questa versione nell’interfaccia utente di Assets, seleziona **[!UICONTROL Ripristina questa versione]**.
1. Per confrontare tra due versioni, vai alla pagina della risorsa e tocca o fai clic sulla versione da confrontare con la versione corrente.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. Dalla timeline, seleziona la versione da confrontare e trascina il cursore a sinistra per sovrapporre questa versione alla versione corrente e confrontare.

   ![confrontare_versioni](assets/compare_versions.png)

### Avviare un flusso di lavoro su una risorsa {#starting-a-workflow-on-an-asset}

1. Andate alla posizione della risorsa per la quale desiderate avviare un flusso di lavoro, quindi toccate o fate clic sulla risorsa per aprire la pagina della risorsa.
1. Tocca o fai clic sull’icona di Navigazione globale e scegli **[!UICONTROL Timeline]** dal menu per visualizzare la timeline.

   ![timeline-1](assets/timeline-1.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Azioni]** Icona (freccia) in basso per aprire l’elenco delle azioni disponibili per la risorsa.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Tocca o fai clic su **[!UICONTROL Avvia flusso di lavoro]** dall&#39;elenco.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. In **[!UICONTROL Avvia flusso di lavoro]** , seleziona un modello di flusso di lavoro dall’elenco.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Facoltativo) Specifica un titolo per il flusso di lavoro, che può essere utilizzato per fare riferimento all’istanza del flusso di lavoro.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tocca o fai clic su **[!UICONTROL Avvia]**, quindi, per confermare, tocca o fai clic su **[!UICONTROL Procedi]** nella finestra di dialogo. Ciascun passaggio del flusso di lavoro viene visualizzato nella timeline come un evento.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Raccolte {#collections}

Una raccolta è un set ordinato di risorse. Puoi utilizzare le raccolte per condividere le risorse tra i vari utenti.

* Una raccolta può includere risorse provenienti da posizioni diverse, poiché contiene solo riferimenti a tali risorse. Ogni raccolta mantiene l’integrità referenziale delle risorse.
* Puoi condividere raccolte con più utenti con diversi livelli di privilegi, ad esempio per la modifica, la visualizzazione e così via.

Per informazioni dettagliate sulla gestione delle raccolte, consulta [gestire le raccolte](/help/assets/manage-collections.md).

## Nascondere le risorse scadute durante la visualizzazione delle risorse nell’app desktop o in Adobe Asset Link {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] l’app desktop consente l’accesso all’archivio DAM da desktop Windows o Mac. Adobe Asset Link consente di accedere alle risorse dall’interno del supporto [!DNL Creative Cloud] applicazioni desktop.

Quando esplori risorse da [!DNL Experience Manager] interfaccia utente, le risorse scadute non vengono visualizzate. Per impedire la visualizzazione, la ricerca e il recupero delle risorse scadute durante la navigazione dalle app desktop e da Asset Link, gli amministratori possono effettuare le seguenti operazioni di configurazione. La configurazione funziona per tutti gli utenti, indipendentemente dal privilegio di amministratore.

Esegui il seguente comando CURL. Accesso in lettura attivato `/conf/global/settings/dam/acpapi/` per gli utenti che accedono alle risorse. Utenti che fanno parte di `dam-user` per impostazione predefinita, il gruppo dispone dell&#39;autorizzazione .

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

Per saperne di più, vedi come [sfogliare le risorse DAM utilizzando l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) e [come utilizzare Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).
