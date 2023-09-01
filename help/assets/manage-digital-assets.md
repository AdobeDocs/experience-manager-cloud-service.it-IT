---
title: Consente di gestire i contenuti digitali
description: Scopri i vari metodi di gestione e modifica delle risorse
contentOwner: AG
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: c63f621f2526f05c8555acdac77a4c05a473c95d
workflow-type: tm+mt
source-wordcount: '4481'
ht-degree: 11%

---

# Gestire le risorse {#manage-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Questo articolo descrive come gestire e modificare le risorse in [!DNL Adobe Experience Manager Assets]. Per gestire [!DNL Content Fragments], vedi [[!DNL Content Fragments]](content-fragments/content-fragments.md) risorse.

## Creare cartelle {#creating-folders}

Quando si organizza una raccolta di risorse, ad esempio, tutti `Nature` immagini, puoi creare cartelle per mantenerle unite. Puoi utilizzare le cartelle per categorizzare e organizzare le risorse. [!DNL Experience Manager Assets] non richiede di organizzare le risorse in cartelle per funzionare meglio.

>[!NOTE]
>
>* Condivisione di una cartella di risorse di tipo `sling:OrderedFolder`, non è supportato quando si condivide con Experience Cloud. Se desideri condividere una cartella, non selezionare [!UICONTROL Ordinato] durante la creazione di una cartella.
>* L’Experience Manager non consente l’utilizzo di `subassets` word come nome di una cartella. È una parola chiave riservata ai nodi che contengono risorse secondarie per le risorse composte

1. Passa alla posizione nella cartella delle risorse digitali in cui desideri creare una nuova cartella. Nel menu, fai clic su **[!UICONTROL Crea]**. Seleziona **[!UICONTROL Nuova cartella]**.
1. In **[!UICONTROL Titolo]** , inserisci un nome per la cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, puoi sovrascrivere l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

I seguenti caratteri (separati da spazi) non sono supportati:

* Il nome di un file di risorse non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? &`
* Il nome di una cartella di risorse non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricare le risorse {#uploading-assets}

Consulta [aggiungere risorse digitali all’Experience Manager](add-assets.md).

## Rilevare risorse duplicate {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Se un utente DAM carica una o più risorse già esistenti nell’archivio, [!DNL Experience Manager] rileva la duplicazione e avvisa l’utente. Il rilevamento duplicati è disabilitato per impostazione predefinita in quanto può avere un impatto sulle prestazioni a seconda delle dimensioni dell’archivio e del numero di risorse caricate.

Per attivare la funzione:

1. Accedi a **[!UICONTROL Strumenti > Risorse > Configurazioni risorse]**.

1. Clic **[!UICONTROL Rilevamento duplicazione risorse]**.

1. Il giorno [!UICONTROL Pagina Rilevamento duplicazione risorse], fai clic su **[!UICONTROL Abilitato]**.

   `dam:sha1` Il valore del campo Rileva metadati garantisce che vengano rilevate risorse duplicate anche se i nomi dei file sono diversi.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Se hai configurato il rilevatore di duplicazione utilizzando `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` file di configurazione di (configurazione OSGi), puoi continuare a utilizzarlo, tuttavia, l’Adobe consiglia di utilizzare il nuovo metodo.


Una volta abilitata, Experience Manager invia le notifiche delle risorse duplicate alla casella in entrata di Experience Manager. È un risultato aggregato per più duplicati. Gli utenti possono scegliere di rimuovere le risorse in base ai risultati.

![Notifica nella casella in entrata per le risorse duplicate](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Quando carichi le risorse nell’archivio, Experience Manager rileva la duplicazione e notifica le prime 100 risorse duplicate.

## Estrai archivi ZIP {#extract-zip-archives}

Seleziona gli archivi ZIP gestiti in Experience Manager ed estrai i file direttamente in Experience Manager senza scaricarli.

Per estrarre i file ZIP, effettuare le seguenti operazioni:

1. Seleziona il tipo di file ZIP.
1. Fai clic su **[!UICONTROL Estrai archivio]** disponibile sulla barra delle azioni.
1. Seleziona la cartella in cui salvare le risorse estratte disponibili nella cartella compressa.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona il comportamento appropriato per gestire i conflitti di nome file durante l’estrazione. Puoi scegliere di creare una nuova versione di una risorsa esistente, sostituirla, mantenere entrambe le risorse nella cartella di destinazione o saltare l’estrazione della nuova risorsa.
1. Clic **[!UICONTROL Extract]**. Il processo di estrazione ZIP viene avviato. Una volta completato il processo, puoi visualizzare le risorse estratte nella cartella di destinazione.

   ![estrazione zip](assets/zip-extraction.png)

## Visualizzare l’anteprima delle risorse {#previewing-assets}

Per visualizzare in anteprima una risorsa, segui la procedura riportata di seguito.

1. Dall’interfaccia utente Assets, individua il percorso della risorsa di cui vuoi visualizzare l’anteprima.
1. Tocca la risorsa desiderata per aprirla.

1. Nella modalità anteprima, sono disponibili le opzioni di zoom per [Tipi di immagini supportati](/help/assets/file-format-support.md) (con modifica interattiva).

   Per ingrandire una risorsa, tocca o fai clic su `+` (oppure tocca o fai clic sulla lente di ingrandimento della risorsa). Per ridurre, tocca o fai clic su `-`. Quando si esegue lo zoom avanti, è possibile esaminare attentamente qualsiasi area dell&#39;immagine eseguendo una panoramica. La freccia di ripristino consente di tornare alla visualizzazione originale.

   Tocca **[!UICONTROL Reimposta]** per ripristinare le dimensioni originali della vista.

## Modifica delle proprietà {#editing-properties}

1. Passa alla posizione della risorsa di cui desideri modificare i metadati.

1. Seleziona la risorsa e tocca o fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti per visualizzare le proprietà della risorsa. In alternativa, scegliete **[!UICONTROL Proprietà]** azione rapida sulla scheda delle risorse.

   ![properties_quickaction](assets/properties_quickaction.png)

1. In [!UICONTROL Proprietà] , modificare le proprietà dei metadati in varie schede. Ad esempio, sotto **[!UICONTROL Base]** , modificare il titolo, la descrizione e così via.

   >[!NOTE]
   >
   >Il layout del [!UICONTROL Proprietà] pagina e le proprietà dei metadati disponibili dipendono dallo schema di metadati sottostante. Per informazioni su come modificare il layout del [!UICONTROL Proprietà] pagina, vedi [Schemi metadati](/help/assets/metadata-schemas.md).

1. Per pianificare una data/ora specifica per l’attivazione della risorsa, utilizza il selettore data posto accanto al campo **[!UICONTROL On Time (All’ora)]**.

   ![Selettore data](assets/date-picker.png)

1. Per disattivare la risorsa dopo una determinata durata, scegli la data/ora di disattivazione dal selettore data posto accanto a **[!UICONTROL Ora di disattivazione]** campo. La data di disattivazione deve essere successiva alla data di attivazione di una risorsa. Dopo il [!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili né tramite l’interfaccia web di Assets né tramite l’API HTTP.

   <!--![chlimage_1-218](assets/chlimage_1-218.png)
1. In **[!UICONTROL Tag]** , selezionare uno o più tag. Per aggiungere un tag personalizzato, digita il nome del tag nella casella e seleziona il `Enter` chiave. Il nuovo tag viene salvato in [!DNL Experience Manager].

   YouTube richiede che i tag siano pubblicati e che sia presente un collegamento ad YouTube (se disponibile).

   >[!NOTE]
   >
   > Per creare i tag, devi disporre dell’autorizzazione di scrittura su `/content/cq:tags/default` percorso nell’archivio CRX.

1. Tocca o fai clic **[!UICONTROL Salva e chiudi]**.

1. Passa all’interfaccia utente di Assets. Le proprietà dei metadati modificate, tra cui titolo, descrizione e tag, vengono visualizzate nella scheda delle risorse nella vista a schede e nelle colonne pertinenti nella vista a elenco.

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

Quando copi una risorsa o una cartella, viene copiata l’intera risorsa o cartella, insieme alla relativa struttura del contenuto. Una risorsa o una cartella copiata viene duplicata nel percorso di destinazione. La risorsa nel percorso di origine non viene modificata.

Alcuni attributi univoci di una particolare copia di una risorsa non vengono riportati. Alcuni esempi sono:

* ID risorsa, data e ora di creazione, versioni e cronologia delle versioni. Alcune di queste proprietà sono indicate dalle proprietà `jcr:uuid`, `jcr:created`, e `cq:name`.

* Il tempo di creazione e i percorsi di riferimento sono univoci per ogni risorsa e per ogni relativa rappresentazione.

Le altre proprietà e le informazioni sui metadati vengono conservate. Una copia parziale non viene creata durante la copia di una risorsa.

1. Dall’interfaccia utente Assets, seleziona una o più risorse, quindi tocca o fai clic sul pulsante **[!UICONTROL Copia]** dalla barra degli strumenti. In alternativa, seleziona la **[!UICONTROL Copia]** ![copy_icon](assets/copy_icon.png) azione rapida dalla scheda delle risorse.

   >[!NOTE]
   >
   >Se si utilizza [!UICONTROL Copia] azione rapida, puoi copiare una sola risorsa alla volta.

1. Passa alla posizione in cui desideri copiare le risorse.

   >[!NOTE]
   >
   >Se copi una risorsa nella stessa posizione, [!DNL Experience Manager] genera automaticamente una variante del nome. Ad esempio, se copi una risorsa con titolo `Square`, [!DNL Experience Manager] genera automaticamente il titolo per la relativa copia come `Square1`.

1. Fai clic su **[!UICONTROL Incolla]** nella barra degli strumenti. Le risorse vengono copiate in questa posizione.

   <!--![chlimage_1-219](assets/chlimage_1-219.png)-->

   >[!NOTE]
   >
   >Il **[!UICONTROL Incolla]** L’icona è disponibile nella barra degli strumenti fino a quando l’operazione Incolla non è completata.

### Spostare o rinominare le risorse {#moving-or-renaming-assets}

1. Passa alla posizione della risorsa da spostare.

1. Seleziona la risorsa e tocca o fai clic sul pulsante **[!UICONTROL Sposta]** icona ![move_icon](assets/move_icon.png) dalla barra degli strumenti.

1. Nella procedura guidata Sposta risorse, effettua una delle seguenti operazioni:

   * Specifica il nome della risorsa dopo lo spostamento. Quindi tocca o fai clic su **[!UICONTROL Successivo]** per procedere.

   * Tocca o fai clic **[!UICONTROL Annulla]** per interrompere il processo.

   >[!NOTE]
   >
   >* Se nella nuova posizione non è presente alcuna risorsa con lo stesso nome, è possibile specificare lo stesso nome per la risorsa. Tuttavia, se sposti la risorsa in una posizione in cui esiste già una risorsa con lo stesso nome, utilizza un nome diverso. Se utilizzate lo stesso nome, il sistema genera automaticamente una variante del nome. Ad esempio, se la risorsa è denominata Square, il sistema genera il nome Square1 per la relativa copia.
   >* Durante la ridenominazione, il nome del file non può contenere spazi.

1. Il giorno **[!UICONTROL Seleziona destinazione]** eseguire una delle operazioni seguenti:

   * Passa alla nuova posizione per le risorse, quindi tocca o fai clic su **[!UICONTROL Successivo]** per procedere.

   * Tocca o fai clic **[!UICONTROL Indietro]** per tornare al **[!UICONTROL Rinomina]** schermo.

1. Se le risorse da spostare hanno pagine, risorse o raccolte di riferimento, il **[!UICONTROL Regola riferimenti]** accanto alla scheda **[!UICONTROL Seleziona destinazione]** scheda.

   Effettua una delle seguenti operazioni in **[!UICONTROL Regola riferimenti]** schermata:

   * Specifica i riferimenti da regolare in base ai nuovi dettagli, quindi tocca o fai clic su **[!UICONTROL Sposta]** per procedere.

   * Dalla sezione **[!UICONTROL Regola]** , seleziona/deseleziona i riferimenti alle risorse.
   * Tocca o fai clic **[!UICONTROL Indietro]** per tornare al **[!UICONTROL Seleziona destinazione]** schermo.

   * Tocca o fai clic **[!UICONTROL Annulla]** per interrompere l&#39;operazione di spostamento.

   Se non aggiorni i riferimenti, questi continuano a puntare al percorso precedente della risorsa. Se regoli i riferimenti, questi vengono aggiornati al nuovo percorso della risorsa.

### Gestire le rappresentazioni {#managing-renditions}

1. Puoi aggiungere o rimuovere rappresentazioni per una risorsa, ad eccezione dell’originale. Passa alla posizione della risorsa per la quale desideri aggiungere o rimuovere rappresentazioni.

1. Tocca o fai clic sulla risorsa per aprirne la pagina.

   <!--![chlimage_1-220](assets/chlimage_1-220.png)-->

1. Tocca o fai clic sull’icona GlobalNav e seleziona **[!UICONTROL Rappresentazioni]** dall&#39;elenco.

   ![renditions_menu](assets/renditions_menu.png)

1. In **[!UICONTROL Rappresentazioni]** visualizzare l’elenco delle rappresentazioni generate per la risorsa.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, [!DNL Experience Manager Assets] non visualizza la rappresentazione originale della risorsa nella modalità di anteprima. Gli amministratori possono utilizzare le sovrapposizioni per configurare [!DNL Assets] per visualizzare le rappresentazioni originali in modalità anteprima.

1. Selezionare una copia trasformata per visualizzarla o eliminarla.

   **Eliminazione di una rappresentazione**

   Selezionare una rappresentazione dal **[!UICONTROL Rappresentazioni]** , quindi tocca o fai clic sul pulsante **[!UICONTROL Elimina rappresentazione]** dalla barra degli strumenti. Non è possibile eliminare le rappresentazioni in blocco al termine dell’elaborazione delle risorse. Per le singole risorse, puoi rimuovere manualmente le rappresentazioni dall’interfaccia utente. Per più risorse, puoi personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche o per eliminare le risorse e ricaricare quelle eliminate.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Caricamento di una nuova rappresentazione**

   Vai alla pagina dei dettagli della risorsa, quindi tocca o fai clic sull’icona **[!UICONTROL Aggiungi rappresentazione]** della barra degli strumenti per caricare una nuova rappresentazione della risorsa.

   <!--![chlimage_1-221](assets/chlimage_1-221.png)-->

   >[!NOTE]
   >
   >Se selezioni un rendering dal pannello **[!UICONTROL Rendering]**, la barra degli strumenti cambia contesto, visualizzando solo le azioni del rendering specifico. Le opzioni non sono visualizzate, ad esempio l’icona Carica rappresentazione. Per visualizzare queste opzioni nella barra degli strumenti, vai alla pagina dei dettagli della risorsa.

   Puoi configurare le dimensioni per la rappresentazione da visualizzare nella pagina dei dettagli di un’immagine o di una risorsa video. In base alle dimensioni specificate, Assets visualizza la rappresentazione con le dimensioni esatte o più vicine.

   Per configurare le dimensioni di rendering di un’immagine a livello di dettaglio della risorsa, sovrapponi il nodo `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configura il valore della proprietà larghezza.  Per personalizzare il rendering sulla pagina dei dettagli della risorsa in base alle dimensioni dell’immagine, configura la proprietà **[!UICONTROL size (Long) in KB (dimensione (lunga) in KB)]** al posto della larghezza. Per la personalizzazione basata sulle dimensioni, la proprietà `preferOriginal` assegna le preferenze all’originale se la dimensione del rendering corrispondente è maggiore.

   Allo stesso modo, potete personalizzare l&#39;immagine della pagina Annotazione sovrapponendola `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   <!--![chlimage_1-222](assets/chlimage_1-222.png)-->

   Per configurare le dimensioni di rendering per una risorsa video, passa alla `videopicker` nodo nell’archivio CRX nel percorso `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sovrapporre il nodo e quindi modificare la proprietà appropriata.

   >[!NOTE]
   >
   >Le annotazioni video sono supportate solo nei browser con formati video compatibili con HTML5. Inoltre, a seconda del browser, sono supportati diversi formati video. Tuttavia, il formato video MXF non è ancora supportato con le annotazioni video.

## Eliminare risorse {#delete-assets}

Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiorna i riferimenti rilevanti prima di eliminare una risorsa.

Inoltre, disattiva il pulsante Forza eliminazione utilizzando una sovrapposizione, per impedire agli utenti di eliminare le risorse di riferimento e lasciare i collegamenti interrotti.

1. Passa alla posizione delle risorse da eliminare.

1. Seleziona la risorsa e fai clic su **[!UICONTROL Elimina]** ![delete_icon](assets/do-not-localize/delete-icon.png) dalla barra degli strumenti.

1. Nella finestra di dialogo di conferma, fai clic su:

   * **[!UICONTROL Annulla]** per interrompere l&#39;azione
   * **[!UICONTROL Elimina]** per confermare l’azione:

      * Se la risorsa non ha riferimenti, viene eliminata.
      * Se la risorsa contiene riferimenti, un messaggio di errore informa che **[!UICONTROL Si fa riferimento a una o più risorse]**. Puoi selezionare **[!UICONTROL Forza eliminazione]** o **[!UICONTROL Annulla]**.

   >[!NOTE]
   >
   >Per eliminare una risorsa è necessario disporre delle autorizzazioni di eliminazione per DAM/risorsa. Se disponi solo delle autorizzazioni di modifica, puoi modificare solo i metadati della risorsa e aggiungere annotazioni alla risorsa. Tuttavia, non puoi eliminare la risorsa o i relativi metadati.

   >[!NOTE]
   >
   >Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiorna i riferimenti rilevanti prima di eliminare una risorsa. Puoi impedire l’eliminazione delle risorse di riferimento in quanto causa collegamenti interrotti. Disattiva il pulsante Forza eliminazione utilizzando una sovrapposizione.

## Scaricare le risorse {#download-assets}

Consulta [scarica risorse da [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Pubblicare o annullare la pubblicazione delle risorse {#publish-assets}

1. Passa alla posizione della risorsa o della cartella di risorse da pubblicare o da rimuovere dall’ambiente di pubblicazione (annulla pubblicazione).

1. Seleziona la risorsa o la cartella da pubblicare o di cui annullare la pubblicazione e seleziona **[!UICONTROL Gestisci pubblicazione]** ![opzione gestisci pubblicazione](assets/do-not-localize/globe-publication.png) dalla barra degli strumenti. In alternativa, per pubblicare rapidamente, seleziona la **[!UICONTROL Pubblicazione rapida]** dalla barra degli strumenti. Se la cartella da pubblicare include una cartella vuota, questa non viene pubblicata.

1. Seleziona la **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** in base alle esigenze.

   ![Annulla pubblicazione](assets/unpublish_action.png)
   *Figura: Opzioni di pubblicazione e annullamento della pubblicazione e opzione di pianificazione.*

1. Seleziona **[!UICONTROL Ora]** per agire subito sulla risorsa o selezionare **[!UICONTROL Più tardi]** per pianificare l&#39;azione. Seleziona una data e un’ora se scegli **[!UICONTROL Più tardi]** opzione. Fai clic su **[!UICONTROL Avanti]**.

1. Durante la pubblicazione, se una risorsa fa riferimento ad altre risorse, i relativi riferimenti sono elencati nella procedura guidata. Vengono visualizzati solo i riferimenti non pubblicati o modificati dall&#39;ultima pubblicazione. Scegliete i riferimenti da pubblicare.

1. Quando annulli la pubblicazione, se una risorsa fa riferimento ad altre risorse, scegli i riferimenti da annullare la pubblicazione. Fai clic su **[!UICONTROL Annulla pubblicazione]**. Nella finestra di dialogo di conferma, fai clic su **[!UICONTROL Annulla]** per interrompere l’azione o fai clic su **[!UICONTROL Annulla pubblicazione]** per confermare che la pubblicazione delle risorse verrà annullata alla data specificata.

Scopri le limitazioni e i suggerimenti seguenti relativi alla pubblicazione o all’annullamento della pubblicazione di risorse o cartelle:

* Opzione per [!UICONTROL Gestisci pubblicazione] è disponibile solo per gli account utente con autorizzazioni di replica.
* Durante l’annullamento della pubblicazione di una risorsa complessa, annulla solo la pubblicazione della risorsa. Evita di annullare la pubblicazione dei riferimenti, poiché altre risorse pubblicate potrebbero farvi riferimento.
* Le cartelle vuote non vengono pubblicate.
* Se pubblichi una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano le rappresentazioni. Attendi il completamento dell’elaborazione, quindi pubblica o ripubblica la risorsa al termine dell’elaborazione.

## Gruppo utenti chiuso {#closed-user-group}

Un gruppo utenti chiuso viene utilizzato per limitare l’accesso a cartelle di risorse specifiche pubblicate da [!DNL Experience Manager]. Se si crea un gruppo utenti chiusi (CUG) per una cartella, l&#39;accesso alla cartella (incluse le risorse e le sottocartelle della cartella) è limitato solo ai membri o ai gruppi assegnati. Per accedere alla cartella, devono accedere utilizzando le credenziali di sicurezza.

I CUG sono un modo aggiuntivo per limitare l’accesso alle risorse. Puoi anche configurare una pagina di accesso per la cartella.

1. Seleziona una cartella dall’interfaccia utente Assets, quindi tocca o fai clic sull’icona Proprietà nella barra degli strumenti per visualizzare la pagina delle proprietà.
1. Dalla sezione **[!UICONTROL Autorizzazioni]** , aggiungere membri o gruppi in **[!UICONTROL Gruppo utenti chiuso]**.

   ![add_user](assets/add_user.png)

1. Per visualizzare una schermata di accesso quando gli utenti accedono alla cartella, selezionare **[!UICONTROL Abilita]** opzione. Quindi, seleziona il percorso di una pagina di accesso in [!DNL Experience Manager]e salva le modifiche.

   ![pagina_di_accesso](assets/login_page.png)

   >[!NOTE]
   >
   >Se non si specifica il percorso di una pagina di accesso, [!DNL Experience Manager] visualizza la pagina di accesso predefinita nell’istanza di pubblicazione.

1. Pubblica la cartella, quindi prova ad accedervi dall’istanza di pubblicazione. Viene visualizzata una schermata di accesso.
1. Se si è un membro del gruppo utenti chiusi, immettere le credenziali di sicurezza. La cartella viene visualizzata dopo [!DNL Experience Manager] ti autentica.

## Cerca risorse {#search-assets}

La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, che sia destinato a un ulteriore utilizzo da parte dei creativi, per la gestione affidabile delle risorse da parte degli utenti aziendali e dei professionisti del marketing o per l’amministrazione da parte degli amministratori DAM.

Per ricerche semplici, avanzate e personalizzate per individuare e utilizzare le risorse più appropriate, consulta [cercare risorse in [!DNL Experience Manager]](/help/assets/search-assets.md).

## Azioni rapide {#quick-actions}

Le icone di azione rapida sono disponibili per una singola risorsa alla volta. A seconda del dispositivo in uso, eseguire le azioni seguenti per visualizzare le icone delle azioni rapide:

* Dispositivi touch: toccare e tenere premuto. Ad esempio, su un’iPad, puoi toccare e tenere premuto un tasto di una risorsa in modo che vengano visualizzate le azioni rapide.
* Dispositivi non touch: puntatore del mouse. Ad esempio, su un dispositivo desktop, se passi il puntatore del mouse sulla miniatura della risorsa, viene visualizzata la barra di azione rapida.

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

## Timeline {#timeline}

La timeline consente di visualizzare vari eventi per un elemento selezionato, ad esempio flussi di lavoro attivi per una risorsa, commenti/annotazioni, registri attività e versioni.

![Ordinare le voci della sequenza temporale per una risorsa](assets/sort_timeline.gif)
*Figura: Ordinare le voci della timeline per una risorsa*

>[!NOTE]
>
>In [Console Raccolte](/help/assets/manage-collections.md#navigate-the-collections-console), il **[!UICONTROL Mostra tutto]** fornisce opzioni per visualizzare solo i commenti e i flussi di lavoro. Inoltre, la timeline viene visualizzata solo per le raccolte di livello superiore elencate nella console. Non viene visualizzato se ti sposti all’interno di una delle raccolte.

>[!NOTE]
>
>La timeline contiene diversi [opzioni specifiche per i frammenti di contenuto](content-fragments/content-fragments.md).

## Annotare risorse {#annotating}

Le annotazioni sono commenti o note esplicative aggiunti a immagini o video. Le annotazioni consentono agli addetti al marketing di collaborare e lasciare un feedback sulle risorse.

Le annotazioni video sono supportate solo nei browser con formati video compatibili con HTML5. I formati video supportati da Assets dipendono dal browser. Tuttavia, il formato video MXF non è ancora supportato con le annotazioni video.

>[!NOTE]
>
>Per Frammenti Di Contenuto, [le annotazioni vengono create nell’editor frammenti](content-fragments/content-fragments.md).

1. Passa alla posizione della risorsa a cui desideri aggiungere annotazioni.
1. Tocca o fai clic sul pulsante **[!UICONTROL Annota]** da una delle seguenti:

   * [Azioni rapide](#quick-actions)
   * Dalla barra degli strumenti, dopo aver selezionato la risorsa o essere passato alla pagina della risorsa

   <!--![chlimage_1-233](assets/chlimage_1-233.png)-->

1. Aggiungi un commento nella casella **[!UICONTROL Commento]** posta nella parte inferiore della timeline. In alternativa, contrassegna un’area sull’immagine e aggiungi un’annotazione nella finestra di dialogo **[!UICONTROL Aggiungi annotazione]**.

<!-- ![chlimage_1-234](assets/chlimage_1-234.png)-->

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Per un utente non amministratore, i suggerimenti vengono visualizzati solo se l’utente dispone delle autorizzazioni di lettura in `/home` in CRXDE.

<!--![chlimage_1-235](assets/chlimage_1-235.png)-->

1. Dopo aver aggiunto l’annotazione, fai clic su **[!UICONTROL Aggiungi]** per salvarlo. Viene inviata una notifica per l’annotazione ad Aaron.

   <!--![chlimage_1-236](assets/chlimage_1-236.png)-->

   >[!NOTE]
   >
   >È possibile aggiungere più annotazioni prima di salvarle.

1. Tocca o fai clic **[!UICONTROL Chiudi]** per uscire dalla modalità Annotation.
1. Per visualizzare la notifica, accedi ad Assets con le credenziali di Aaron MacDonald e fai clic su **[!UICONTROL Notifiche]** per visualizzare la notifica.

   >[!NOTE]
   >
   >È inoltre possibile aggiungere annotazioni alle risorse video. Durante l’annotazione dei video, il lettore si interrompe per consentire l’annotazione su un fotogramma. Per ulteriori informazioni, consulta [gestione delle risorse video](manage-video-assets.md). Tuttavia, il formato video MXF non è ancora supportato con le annotazioni video.

1. Per scegliere un colore diverso in modo da poter distinguere tra gli utenti, tocca o fai clic sull’icona Profilo e tocca o fai clic su **[!UICONTROL Le mie preferenze]**.

   <!--![chlimage_1-237](assets/chlimage_1-237.png)-->

   Nella casella **[!UICONTROL Colore annotazione]**, specifica il colore desiderato, infine tocca o fai clic su **[!UICONTROL Accetta]**.

<!-- ![chlimage_1-238](assets/chlimage_1-238.png)-->

>[!NOTE]
>
>Puoi anche aggiungere annotazioni a una raccolta. Tuttavia, se una raccolta contiene raccolte secondarie, è possibile aggiungere annotazioni o commenti solo alla raccolta principale. L’opzione Annota non è disponibile per le raccolte secondarie.

### Visualizzare le annotazioni salvate {#viewing-saved-annotations}

È possibile visualizzare una sola annotazione alla volta.

>[!NOTE]
>
>Se selezioni più annotazioni, l’ultima annotazione è visibile nell’interfaccia utente.
>
>La selezione multipla è supportata solo per la stampa della risorsa annotata come PDF.

1. Per visualizzare le annotazioni salvate per una risorsa, passa alla posizione della risorsa e apri la relativa pagina.

1. Tocca o fai clic sull’icona GlobalNav e scegli **[!UICONTROL Timeline]** dall&#39;elenco.

   <!--![chlimage_1-239](assets/chlimage_1-239.png)-->

1. Dall’elenco **[!UICONTROL Mostra tutti]** nella timeline, seleziona **[!UICONTROL Commenti]** per filtrare i risultati in base alle annotazioni.

   <!--![chlimage_1-240](assets/chlimage_1-240.png)-->

   Tocca o fai clic su un commento nella **[!UICONTROL Timeline]** per visualizzare l’annotazione corrispondente sull’immagine.

   <!--![chlimage_1-241](assets/chlimage_1-241.png)-->

   Tocca o fai clic **[!UICONTROL Elimina]**, per eliminare un particolare commento.

### Stampa annotazioni {#printing-annotations}

Se una risorsa contiene annotazioni o è stata soggetta a un flusso di lavoro di revisione, puoi stampare la risorsa insieme alle annotazioni e rivederne lo stato come file PDF per la revisione offline.

È inoltre possibile scegliere di stampare solo le annotazioni o lo stato di revisione.

>[!NOTE]
>
>È possibile selezionare più annotazioni durante la stampa della risorsa annotata come PDF.

Per stampare le annotazioni e controllare lo stato, tocca o fai clic sul pulsante **[!UICONTROL Stampa]** e seguire le istruzioni della procedura guidata. Il **[!UICONTROL Stampa]** viene visualizzata nella barra degli strumenti solo quando alla risorsa è assegnato almeno uno stato di annotazione o revisione.

1. Dall’interfaccia utente Assets, apri la pagina di anteprima di una risorsa.
1. Effettua una delle operazioni seguenti:

   * Per stampare tutte le annotazioni e lo stato di revisione, saltare il passaggio 3 e passare direttamente al passaggio 4.
   * Per stampare annotazioni specifiche e rivedere lo stato, aprire [timeline](/help/assets/manage-digital-assets.md#timeline) quindi andare al punto 3.

1. Per stampare annotazioni specifiche, selezionarle dalla timeline.

   <!--![chlimage_1-242](assets/chlimage_1-242.png)-->

   Per stampare solo lo stato di revisione, selezionarlo dalla timeline.

   <!--![chlimage_1-243](assets/chlimage_1-243.png)-->

1. Tocca o fai clic sul pulsante **[!UICONTROL Stampa]** dalla barra degli strumenti.

   <!--![chlimage_1-244](assets/chlimage_1-244.png)-->

1. Nella finestra di dialogo Stampa, scegliere la posizione in cui si desidera visualizzare lo stato di annotazioni/revisioni sul PDF. Ad esempio, se desideri stampare le annotazioni/stato in alto a destra della pagina che contiene l’immagine stampata, utilizza **In alto a sinistra** impostazione. È selezionata per impostazione predefinita.

   <!--![chlimage_1-245](assets/chlimage_1-245.png)-->

   È possibile scegliere altre impostazioni, a seconda della posizione in cui si desidera visualizzare le annotazioni o lo stato nel PDF stampato. Se vuoi che le annotazioni o lo stato vengano visualizzati in una pagina separata dalla risorsa stampata, scegli **[!UICONTROL Pagina successiva]**.

1. Clic **[!UICONTROL Stampa]**. A seconda dell’opzione scelta al passaggio 2, il PDF generato visualizza annotazioni/stato nella posizione specificata. Ad esempio, se scegli di stampare sia le annotazioni che lo stato di revisione utilizzando l’impostazione **In alto a sinistra**, l’output generato sarà simile al file PDF qui riportato.

   <!--![chlimage_1-246](assets/chlimage_1-246.png)-->

1. Scarica o stampa il PDF utilizzando le opzioni in alto a destra.

   <!--![chlimage_1-247](assets/chlimage_1-247.png)-->

   Per modificare l&#39;aspetto del file PDF sottoposto a rendering, ad esempio il colore, la dimensione e lo stile del carattere e il colore di sfondo dei commenti e degli stati, aprire **[!UICONTROL Configurazione di Annotation PDF]** da Configuration Manager e modificare le opzioni desiderate. Ad esempio, per modificare il colore di visualizzazione dello stato approvato, modifica il codice del colore nel campo corrispondente. Per informazioni sulla modifica del colore del carattere delle annotazioni, vedere [Annotazione](/help/assets/manage-digital-assets.md#annotating).

   Tornate al file PDF sottoposto a rendering e aggiornatelo. Il PDF aggiornato riflette le modifiche apportate.

## Controllo delle versioni di una risorsa {#asset-versioning}

Il controllo delle versioni crea un’istantanea delle risorse digitali in un determinato momento. Il controllo delle versioni consente di ripristinare le risorse a uno stato precedente in un secondo momento. Ad esempio, per annullare una modifica apportata a una risorsa, ripristina la versione non modificata della risorsa.

Di seguito sono riportati gli scenari in cui si creano le versioni:

* Puoi modificare un’immagine in un’altra applicazione e caricarla in Assets. Viene creata una versione dell&#39;immagine in modo che l&#39;immagine originale non venga sovrascritta.
* Puoi modificare i metadati di una risorsa.
* Utilizzi [!DNL Experience Manager] app desktop per estrarre una risorsa esistente e salvare le modifiche. A ogni salvataggio della risorsa viene creata una nuova versione.

È inoltre possibile abilitare il controllo automatico delle versioni tramite un flusso di lavoro. Quando crei una versione per una risorsa, i metadati e le rappresentazioni vengono salvati insieme alla versione. Le rappresentazioni sono rappresentazioni alternative delle stesse immagini, ad esempio una rappresentazione PNG di un file JPEG caricato.

La funzionalità di controllo delle versioni consente di effettuare le seguenti operazioni:

* Crea una versione di una risorsa.
* Visualizzare la revisione corrente di una risorsa.
* Ripristina una versione precedente della risorsa.

1. Passa alla posizione della risorsa per la quale desideri creare una versione e tocca o fai clic su di essa per aprire la relativa pagina della risorsa.

1. Tocca o fai clic sull’icona GlobalNav e scegli **[!UICONTROL Timeline]** dal menu.

   ![timeline](assets/timeline.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Azioni]** (freccia) in basso per visualizzare le azioni disponibili che puoi eseguire sulla risorsa.

   <!--![chlimage_1-249](assets/chlimage_1-249.png)-->

1. Tocca o fai clic **[!UICONTROL Salva come versione]** per creare una versione della risorsa.

<!--![chlimage_1-250](assets/chlimage_1-250.png)-->

1. Aggiungere un&#39;etichetta e un commento, quindi fare clic su **[!UICONTROL Crea]** per creare una versione. In alternativa, tocca o fai clic su **Annulla** per uscire dall&#39;operazione.

   <!--![chlimage_1-251](assets/chlimage_1-251.png)-->

1. Per visualizzare la nuova versione, apri l’elenco **[!UICONTROL Mostra tutti]** nella timeline dalla pagina dei dettagli della risorsa o dall’interfaccia utente Assets, quindi scegli **[!UICONTROL Versioni]**. Tutte le versioni create per una risorsa sono elencate nella scheda della timeline. Puoi filtrare l’elenco Versioni, facendo clic sulla freccia rivolta verso il basso e selezionando **[!UICONTROL Versioni]** dall’elenco.

   ![versions_option](assets/versions_option.png)

1. Seleziona una versione specifica per la risorsa per visualizzarla in anteprima o per consentirne la visualizzazione nell&#39;interfaccia utente Assets.

   ![select_version](assets/select_version.png)

1. Aggiungi un’etichetta e un commento per la versione per ripristinare una versione specifica nell’interfaccia utente Assets.

   ![save_version](assets/save_version.png)

1. Per generare un’anteprima per la versione, tocca o fai clic su **[!UICONTROL Anteprima versione]**.
1. Per visualizzare questa versione nell’interfaccia utente Assets, seleziona **[!UICONTROL Ripristina questa versione]**.
1. Per confrontare due versioni, vai alla pagina della risorsa e tocca o fai clic sulla versione da confrontare con la versione corrente.

   ![select_version_to_compare](assets/select_version_tocompare.png)

1. Dalla timeline, seleziona la versione da confrontare e trascina il cursore verso sinistra per sovrapporre questa versione alla versione corrente e confrontare.

   ![compare_versions](assets/compare_versions.png)

### Avviare un flusso di lavoro su una risorsa {#starting-a-workflow-on-an-asset}

1. Passa alla posizione della risorsa per la quale desideri avviare un flusso di lavoro, quindi tocca o fai clic sulla risorsa per aprire la pagina della risorsa.
1. Tocca o fai clic sull’icona GlobalNav e scegli **[!UICONTROL Timeline]** per visualizzare la timeline.

   ![timeline-1](assets/timeline-1.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Azioni]** (freccia) in basso per aprire l’elenco delle azioni disponibili per la risorsa.

   <!--![chlimage_1-252](assets/chlimage_1-252.png)-->

1. Tocca o fai clic **[!UICONTROL Avvia flusso di lavoro]** dall&#39;elenco.

   <!--![chlimage_1-253](assets/chlimage_1-253.png)-->

1. In **[!UICONTROL Avvia flusso di lavoro]** , seleziona un modello di flusso di lavoro dall’elenco.

   <!--![chlimage_1-254](assets/chlimage_1-254.png)-->

1. (Facoltativo) Specifica un titolo per il flusso di lavoro, che può essere utilizzato per fare riferimento all’istanza del flusso di lavoro.

   <!--![chlimage_1-255](assets/chlimage_1-255.png)-->

1. Tocca o fai clic su **[!UICONTROL Avvia]**, quindi, per confermare, tocca o fai clic su **[!UICONTROL Procedi]** nella finestra di dialogo. Ciascun passaggio del flusso di lavoro viene visualizzato nella timeline come un evento.

   <!--![chlimage_1-256](assets/chlimage_1-256.png)-->

## Raccolte {#collections}

Una raccolta è un set ordinato di risorse. Puoi utilizzare le raccolte per condividere le risorse tra i vari utenti.

* Una raccolta può includere risorse da posizioni diverse, perché contengono solo riferimenti a tali risorse. Ogni raccolta mantiene l’integrità referenziale delle risorse.
* Puoi condividere raccolte con più utenti con diversi livelli di privilegi, ad esempio per modificare, visualizzare e così via.

Per informazioni dettagliate sulla gestione della raccolta, consulta [gestisci raccolte](/help/assets/manage-collections.md).

## Nascondere le risorse scadute durante la visualizzazione delle risorse nell’app desktop o nel collegamento di risorse Adobe {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] L’app desktop consente di accedere all’archivio DAM da Windows o dal desktop Mac. Adobe Asset Link consente di accedere alle risorse dall’interno del [!DNL Creative Cloud] applicazioni desktop.

Quando esplori le risorse da [!DNL Experience Manager] nell’interfaccia utente, le risorse scadute non vengono visualizzate. Per evitare di visualizzare, cercare e recuperare le risorse scadute durante la navigazione dall’app desktop e da Asset Link, gli amministratori possono effettuare la seguente configurazione. La configurazione funziona per tutti gli utenti, indipendentemente dal privilegio di amministratore.

Eseguite il seguente comando CURL. Assicurare l&#39;accesso in lettura su `/conf/global/settings/dam/acpapi/` per gli utenti che accedono alle risorse. Utenti che fanno parte di `dam-user` dispongono dell&#39;autorizzazione per impostazione predefinita.

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

Per ulteriori informazioni, vedere come [Sfogliare le risorse DAM tramite l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) e [come utilizzare Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).

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
