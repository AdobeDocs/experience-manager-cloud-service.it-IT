---
title: Gestione delle risorse digitali in Experience Manager
description: Scopri i diversi metodi di gestione e modifica delle risorse.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 913339d0892b37814df1bd04bc352cfadf32b3e6

---


# Manage assets {#manage-assets}

Questo articolo descrive come gestire e modificare le risorse in Risorse Adobe Experience Manager (AEM). Per gestire i frammenti di contenuto, consulta Risorse relative ai frammenti di [contenuto](content-fragments/content-fragments.md) .

## Creare le cartelle {#creating-folders}

Quando organizzate una raccolta di risorse, ad esempio tutte `Nature` le immagini, potete creare delle cartelle per mantenerle unite. Potete usare le cartelle per classificare e organizzare le risorse. Risorse AEM non richiede l’organizzazione di risorse in cartelle per migliorare il funzionamento.

>[!NOTE]
>
>* La condivisione di una cartella di risorse di tipo `sling:OrderedFolder`non è supportata quando si condivide con Marketing Cloud. Se desiderate condividere una cartella, non selezionate [!UICONTROL Ordinato] al momento della creazione di una cartella.
>* Experience Manager non consente l&#39;uso di `subassets` parole come nome di una cartella. È una parola chiave riservata al nodo che contiene risorse secondarie per le risorse composte


1. Andate alla posizione nella cartella delle risorse digitali in cui desiderate creare una nuova cartella. Nel menu, fate clic su **[!UICONTROL Crea]**. Selezionate **[!UICONTROL Nuova cartella]**.
1. Nel campo **[!UICONTROL Titolo]** , inserite un nome di cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, potete ignorare l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

I seguenti caratteri (elenco separato da spazi) non sono supportati:

* Il nome di un file di risorsa non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? &`
* Il nome di una cartella di risorse non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Upload assets {#uploading-assets}

Per informazioni dettagliate, consultate [Aggiunta di risorse digitali a Experience Manager](add-assets.md).

## Visualizzare le risorse {#previewing-assets}

Per visualizzare l’anteprima di una risorsa, effettuate le seguenti operazioni.

1. Dall’interfaccia utente Risorse, andate alla posizione della risorsa da visualizzare in anteprima.
1. Toccate la risorsa desiderata per aprirla.

1. Nella modalità di anteprima, le opzioni di zoom sono disponibili per i tipi [di immagini](/help/assets/file-format-support.md) supportati (con modifica interattiva).

   Per ingrandire una risorsa, toccate o fate clic `+` (oppure toccate o fate clic sulla lente di ingrandimento della risorsa). Per ridurre la visualizzazione, toccate o fate clic `-`. Quando ingrandite, potete osservare da vicino qualsiasi area dell’immagine eseguendo il panning. La freccia di reimpostazione dello zoom consente di tornare alla visualizzazione originale.

   Toccate **[!UICONTROL Ripristina]** per ripristinare le dimensioni originali della visualizzazione.

## Modifica proprietà {#editing-properties}

1. Andate alla posizione della risorsa di cui desiderate modificare i metadati.

1. Selezionate la risorsa, quindi toccate o fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti per visualizzare le proprietà della risorsa. In alternativa, scegliete l’azione rapida **[!UICONTROL Proprietà]** sulla scheda delle risorse.

   ![properties_quickaction](assets/properties_quickaction.png)

1. Nella pagina [!UICONTROL Proprietà] , modificate le proprietà dei metadati in varie schede. Ad esempio, nella scheda **[!UICONTROL Base]** , modificare il titolo, la descrizione e così via.

   >[!NOTE]
   >
   >Il layout della pagina [!UICONTROL Proprietà] e le proprietà dei metadati disponibili dipendono dallo schema di metadati sottostante. Per informazioni su come modificare il layout della pagina [!UICONTROL Proprietà] , consultate Schemi [di](/help/assets/metadata-schemas.md)metadati.

1. Per pianificare una data/ora specifica per l’attivazione della risorsa, utilizza il selettore data posto accanto al campo **[!UICONTROL On Time (All’ora)]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Per disattivare la risorsa dopo una determinata durata, scegliete la data/ora di disattivazione dal selettore data accanto al campo **[!UICONTROL Ora]** disattivazione. La data di disattivazione deve essere successiva alla data di attivazione di una risorsa. Dopo la [!UICONTROL disattivazione], una risorsa e le relative rappresentazioni non sono disponibili né tramite l’interfaccia Web di Assets né tramite l’API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Nel campo **[!UICONTROL Tag]** , selezionare uno o più tag. Per aggiungere un tag personalizzato, digitate il nome del tag nella casella e premete il tasto Invio. Il nuovo tag viene salvato in AEM.

   YouTube richiede la pubblicazione di tag e un collegamento a YouTube (se è possibile trovare un collegamento appropriato).

   >[!NOTE]
   >
   >Per creare i tag, è necessario disporre dell&#39;autorizzazione di scrittura nel `/content/cq:tags/default` percorso dell&#39;archivio CRX.

1. Per visualizzare le statistiche di utilizzo della risorsa, tocca o fai clic sulla scheda **[!UICONTROL Approfondimenti]** .

   Le statistiche di utilizzo includono quanto segue:

   * Numero di volte in cui la risorsa è stata visualizzata o scaricata
   * Canali/dispositivi attraverso i quali è stata utilizzata la risorsa
   * Soluzioni creative in cui la risorsa è stata utilizzata di recente
   Per ulteriori dettagli, consulta [Informazioni approfondite](assets-insights.md)sulle risorse.

1. Toccate o fate clic su **[!UICONTROL Salva e chiudi]**.

1. Passa all’interfaccia utente Risorse. Le proprietà dei metadati modificate, inclusi titolo, descrizione e tag, vengono visualizzate sulla scheda delle risorse nella vista a schede e nelle relative colonne nella vista Elenco.

## Copiare le risorse {#copying-assets}

Quando copiate una risorsa o una cartella, viene copiata l’intera risorsa o la cartella, insieme alla relativa struttura del contenuto. Una risorsa o una cartella copiata viene duplicata nel percorso di destinazione. La risorsa nella posizione di origine non viene modificata.

Alcuni attributi univoci per una particolare copia di una risorsa non vengono riportati avanti. Alcuni esempi sono:

* ID risorsa, data e ora di creazione, versioni e cronologia delle versioni. Alcune di queste proprietà sono indicate dalle proprietà `jcr:uuid`, `jcr:created`e `cq:name`.

* L’ora di creazione e i percorsi di riferimento sono univoci per ciascuna risorsa e per ciascuna delle relative rappresentazioni.

Le altre proprietà e informazioni sui metadati vengono mantenute. Durante la copia di una risorsa non viene creata una copia parziale.

1. Nell’interfaccia utente Risorse, seleziona una o più risorse, quindi tocca o fai clic sull’icona **[!UICONTROL Copia]** dalla barra degli strumenti. In alternativa, selezionate l’azione rapida **[!UICONTROL Copia]** icona ![](assets/copy_icon.png) copia dalla scheda delle risorse.

   >[!NOTE]
   >
   >Se utilizzate l’azione rapida [!UICONTROL Copia] , potete copiare una sola risorsa alla volta.

1. Andate alla posizione in cui desiderate copiare le risorse.

   >[!NOTE]
   >
   >Se copiate una risorsa nella stessa posizione, AEM genera automaticamente una variante del nome. Ad esempio, se copiate una risorsa con titolo `Square`, AEM genera automaticamente il titolo della relativa copia come `Square1`.

1. Fate clic sull&#39;icona della risorsa **[!UICONTROL Incolla]** dalla barra degli strumenti. Le risorse vengono copiate in questa posizione.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >L’icona **[!UICONTROL Incolla]** è disponibile nella barra degli strumenti fino al completamento dell’operazione Incolla.

### Spostare o rinominare le risorse {#moving-or-renaming-assets}

1. Andate alla posizione della risorsa da spostare.

1. Selezionate la risorsa, quindi toccate o fate clic sull’icona **[!UICONTROL Sposta]** , ![icona](assets/move_icon.png) Sposta_barra degli strumenti.

1. Nella procedura guidata Sposta risorse, effettuate una delle seguenti operazioni:

   * Dopo averlo spostato, specificate il nome della risorsa. Quindi toccate o fate clic su **[!UICONTROL Avanti]** per continuare.

   * Toccate/fate clic su **[!UICONTROL Annulla]** per interrompere il processo.
   >[!NOTE]
   >
   >* Potete specificare lo stesso nome per la risorsa se nella nuova posizione non è presente alcuna risorsa con lo stesso nome. Tuttavia, se spostate la risorsa in una posizione in cui esiste una risorsa con lo stesso nome, usate un nome diverso. Se usate lo stesso nome, il sistema genera automaticamente una variante del nome. Ad esempio, se la risorsa ha il nome Square, il sistema genera il nome Square1 per la relativa copia.
   >* Durante la ridenominazione, gli spazi bianchi non sono consentiti nel nome del file.


1. Nella finestra di dialogo **[!UICONTROL Seleziona destinazione]** , effettuate una delle seguenti operazioni:

   * Andate alla nuova posizione delle risorse, quindi toccate o fate clic su **[!UICONTROL Avanti]** per proseguire.

   * Toccate/fate clic su **[!UICONTROL Indietro]** per tornare alla schermata **[!UICONTROL Rinomina]** .

1. Se le risorse che state spostando dispongono di pagine, risorse o raccolte di riferimento, accanto alla scheda **[!UICONTROL Seleziona destinazione]** viene visualizzata la scheda **[!UICONTROL Regola riferimenti]** .

   Effettuate una delle seguenti operazioni nella schermata **[!UICONTROL Regola riferimenti]** :

   * Specificate i riferimenti da modificare in base ai nuovi dettagli, quindi toccate o fate clic su **[!UICONTROL Sposta]** per proseguire.

   * Nella colonna **[!UICONTROL Regola]** , selezionate o deselezionate i riferimenti alle risorse.
   * Toccate/fate clic su **[!UICONTROL Indietro]** per tornare alla schermata **[!UICONTROL Seleziona destinazione]** .

   * Toccate/fate clic su **[!UICONTROL Annulla]** per interrompere l&#39;operazione di spostamento.
   Se non aggiornate i riferimenti, continueranno a indicare il percorso precedente della risorsa. Se regolate i riferimenti, questi vengono aggiornati al nuovo percorso della risorsa.

### Gestire le rappresentazioni {#managing-renditions}

1. Potete aggiungere o rimuovere rappresentazioni per una risorsa, tranne l’originale. Andate alla posizione della risorsa per la quale desiderate aggiungere o rimuovere le rappresentazioni.

1. Toccate o fate clic sulla risorsa per aprirne la pagina.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Toccate o fate clic sull&#39;icona GlobalNav, quindi selezionate **[!UICONTROL Rendering]** dall&#39;elenco.

   ![renditions_menu](assets/renditions_menu.png)

1. Nel pannello **[!UICONTROL Rappresentazioni]** , visualizzate l’elenco delle rappresentazioni generate per la risorsa.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, Risorse AEM non visualizza la rappresentazione originale della risorsa in modalità di anteprima. Gli amministratori possono utilizzare le sovrapposizioni per configurare Risorse AEM in modo da visualizzare le rappresentazioni originali in modalità di anteprima.

1. Selezionate una rappresentazione per visualizzare o eliminare la rappresentazione.

   **Eliminazione di una rappresentazione**

   Selezionate una rappresentazione dal pannello **[!UICONTROL Rappresentazioni]** , quindi toccate o fate clic sull&#39;icona **[!UICONTROL Elimina rappresentazione]** dalla barra degli strumenti.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Caricamento di una nuova rappresentazione**

   Vai alla pagina dei dettagli della risorsa, quindi tocca o fai clic sull’icona **[!UICONTROL Aggiungi rappresentazione]** della barra degli strumenti per caricare una nuova rappresentazione della risorsa.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Se selezioni un rendering dal pannello **[!UICONTROL Rendering]**, la barra degli strumenti cambia contesto, visualizzando solo le azioni del rendering specifico. Le opzioni non sono visualizzate, ad esempio l’icona Carica rappresentazione. Per visualizzare queste opzioni nella barra degli strumenti, vai alla pagina dei dettagli della risorsa.

   Potete configurare le dimensioni per la rappresentazione da visualizzare nella pagina dei dettagli di un’immagine o di una risorsa video. In base alle dimensioni specificate, Risorse AEM visualizza la rappresentazione con le dimensioni esatte o più vicine.

   Per configurare le dimensioni di rendering di un’immagine a livello di dettaglio della risorsa, sovrapponi il nodo `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configura il valore della proprietà larghezza.  Per personalizzare il rendering sulla pagina dei dettagli della risorsa in base alle dimensioni dell’immagine, configura la proprietà **[!UICONTROL size (Long) in KB (dimensione (lunga) in KB)]** al posto della larghezza. Per la personalizzazione basata sulle dimensioni, la proprietà `preferOriginal` assegna le preferenze all’originale se la dimensione del rendering corrispondente è maggiore.

   Allo stesso modo, potete personalizzare l&#39;immagine della pagina Annotazione sovrapponendo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Per configurare le dimensioni di rappresentazione per una risorsa video, andate al `videopicker` nodo nell’archivio CRX nella posizione `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sovrapponete il nodo, quindi modificate la proprietà appropriata.

   >[!NOTE]
   >
   >Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. Inoltre, a seconda del browser, sono supportati diversi formati video.

## Delete assets {#delete-assets}

Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiornate i riferimenti pertinenti prima di eliminare una risorsa.

Inoltre, disattivate il pulsante Forza eliminazione con una sovrapposizione, per impedire agli utenti di eliminare le risorse di riferimento e di lasciare i collegamenti interrotti.

1. Andate alla posizione delle risorse che desiderate eliminare.

1. Selezionate la risorsa, quindi toccate o fate clic sull’icona **[!UICONTROL Elimina]** dalla barra degli strumenti.

   ![delete_icon](assets/delete_icon.png)

1. Nella finestra di dialogo di conferma, fate clic su:

   * **[!UICONTROL Annulla]** per interrompere l’azione
   * **[!UICONTROL Elimina]** per confermare l’azione:

      * Se la risorsa non dispone di riferimenti, viene eliminata.
      * Se la risorsa dispone di riferimenti, un messaggio di errore vi informa che **Una o più risorse dispongono di riferimenti.** Potete selezionare **[!UICONTROL Forza eliminazione]** o **[!UICONTROL Annulla]**.
   >[!NOTE]
   >
   >Per poter eliminare una risorsa è necessario disporre delle autorizzazioni di eliminazione per la risorsa DAM o la risorsa. Se disponete solo di autorizzazioni di modifica, potete modificare solo i metadati della risorsa e aggiungere delle annotazioni alla risorsa. Tuttavia, non potete eliminare la risorsa o i relativi metadati.

   >[!NOTE]
   >
   >Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiornate i riferimenti pertinenti prima di eliminare una risorsa.
   >
   >
   >Inoltre, disattivate il pulsante Forza eliminazione con una sovrapposizione, per impedire agli utenti di eliminare le risorse di riferimento e di lasciare i collegamenti interrotti.

## Scaricare le risorse {#download-assets}

See [Download assets from AEM](/help/assets/download-assets-from-aem.md).

## Publish assets {#publish-assets}

<!--
>[!NOTE]
>
>For more information specific to Dynamic Media, see [Publishing Dynamic Media Assets.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
-->

1. Andate alla posizione delle risorse o della cartella che desiderate pubblicare.

1. Seleziona l’azione rapida **[!UICONTROL Pubblica]** dalla scheda delle risorse oppure fai clic sulla risorsa e tocca o fai clic sull’icona **[!UICONTROL Pubblicazione rapida]** dalla barra degli strumenti.
1. Se la risorsa fa riferimento ad altre risorse, i relativi riferimenti sono elencati nella procedura guidata. Vengono visualizzati solo i riferimenti non pubblicati o modificati dopo l’ultima pubblicazione o l’annullamento della pubblicazione. Scegliete i riferimenti da pubblicare.

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >Se la cartella da pubblicare include una cartella vuota, la cartella vuota non verrà pubblicata.

1. Toccate o fate clic su **[!UICONTROL Pubblica]** per confermare l’attivazione delle risorse.

>[!CAUTION]
>
>Se pubblicate una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano le rappresentazioni. Attendere il completamento dell’elaborazione, quindi pubblicare o pubblicare nuovamente la risorsa al termine dell’elaborazione.

## Annullare la pubblicazione delle risorse {#unpublishing-assets}

1. Andate alla posizione della cartella di risorse o risorse che desiderate rimuovere dall’ambiente di pubblicazione (Annulla pubblicazione).

1. Selezionate la risorsa o la cartella da annullare la pubblicazione, quindi toccate o fate clic sull’icona **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti.

   ![manage_publication](assets/manage_publication.png)

1. Selezionate l’azione **[!UICONTROL Annulla pubblicazione]** dall’elenco.

   ![unpublish_action](assets/unpublish_action.png)

1. Per annullare la pubblicazione della risorsa in un secondo momento, selezionate **[!UICONTROL Annulla pubblicazione più tardi]**, quindi selezionate una data per annullare la pubblicazione della risorsa.
1. Pianificate una data in cui la risorsa non sarà disponibile dall’ambiente di pubblicazione.
1. Se la risorsa fa riferimento ad altre risorse, scegliete i riferimenti da annullare la pubblicazione. Toccate o fate clic su **[!UICONTROL Annulla pubblicazione]**.
1. Nella finestra di dialogo di conferma, toccate o fate clic su:

   * **[!UICONTROL Annulla]** per interrompere l’azione
   * **[!UICONTROL Annulla pubblicazione]** per confermare che le risorse non sono più pubblicate (non sono più disponibili nell’ambiente di pubblicazione) alla data specificata.
   >[!NOTE]
   >
   >Quando si annulla la pubblicazione di una risorsa complessa, è necessario annullare la pubblicazione solo della risorsa. Evitate di annullare la pubblicazione dei riferimenti, in quanto ad essi potrebbero fare riferimento altre risorse pubblicate.

## Closed user group {#closed-user-group}

Un gruppo di utenti chiuso (CUG) viene usato per limitare l’accesso a specifiche cartelle di risorse pubblicate da AEM. Se create un gruppo di utenti chiuso per una cartella, l’accesso alla cartella (comprese le risorse e le sottocartelle) è limitato solo ai membri o ai gruppi assegnati. Per accedere alla cartella, devono accedere utilizzando le credenziali di protezione.

I COG consentono di limitare l’accesso alle risorse. Potete anche configurare una pagina di login per la cartella.

1. Selezionate una cartella dall’interfaccia utente Risorse, quindi toccate o fate clic sull’icona Proprietà dalla barra degli strumenti per visualizzare la pagina delle proprietà.
1. Dalla scheda **[!UICONTROL Autorizzazioni]** , aggiungete membri o gruppi in Gruppo **[!UICONTROL utenti]** chiuso.

   ![add_user](assets/add_user.png)

1. Per visualizzare una schermata di login quando gli utenti accedono alla cartella, selezionate l’opzione **[!UICONTROL Abilita]** . Quindi, selezionate il percorso di una pagina di accesso in AEM e salvate le modifiche.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Se non specificate il percorso di una pagina di accesso, AEM visualizza la pagina di accesso predefinita nell’istanza di pubblicazione.

1. Pubblicate la cartella, quindi provate ad accedervi dall’istanza di pubblicazione. Viene visualizzata una schermata di login.
1. Se siete un membro CUG, immettete le vostre credenziali di protezione. La cartella viene visualizzata dopo l’autenticazione da parte di AEM.

## Cercare risorse {#search-assets}

La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e degli esperti di marketing, sia per l’amministrazione da parte degli amministratori DAM.

Per ricerche semplici, avanzate e personalizzate per scoprire e utilizzare le risorse più appropriate, consultate [Cercare risorse in AEM](/help/assets/search-assets.md).

## Azioni rapide {#quick-actions}

Le icone delle azioni rapide sono disponibili per una singola risorsa alla volta. A seconda del dispositivo, effettuate le seguenti operazioni per visualizzare le icone delle azioni rapide:

* Dispositivi touch: Toccate e tenete premuto. Ad esempio, su un iPad potete toccare e tenere premuto un contenuto per visualizzare le azioni rapide.
* Dispositivi non touch: Puntatore al passaggio del mouse. Ad esempio, su un dispositivo desktop, se passate il puntatore sulla miniatura della risorsa viene visualizzata la barra delle azioni rapide.

## Modificare le immagini {#editing-images}

Gli strumenti di modifica nell’interfaccia di Risorse AEM consentono di effettuare piccoli processi di modifica sulle risorse di immagine. Potete ritagliare, ruotare, capovolgere ed eseguire altri processi di modifica sulle immagini. Potete anche aggiungere mappe immagine alle risorse.

>[!NOTE]
>
>Per alcuni componenti, la modalità Schermo intero dispone di opzioni aggiuntive.

1. Per aprire una risorsa in modalità di modifica, effettuate una delle seguenti operazioni:

   * Selezionate la risorsa, quindi toccate o fate clic sull’icona **[!UICONTROL Modifica]** nella barra degli strumenti.
   * Toccate/fate clic sull&#39;icona **[!UICONTROL Modifica]** visualizzata su una risorsa nella vista a schede.
   * Nella pagina della risorsa, toccate o fate clic sull’icona **[!UICONTROL Modifica]** nella barra degli strumenti.
   ![edit_icon](assets/edit_icon.png)

1. Per ritagliare l’immagine, toccate o fate clic sull’icona **Ritaglia** .

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Seleziona l’opzione desiderata dall’elenco. L’area di ritaglio viene visualizzata sull’immagine in base all’opzione scelta. L’opzione **Mano libera** consente di ritagliare l’immagine senza limitazioni di proporzioni.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Selezionate l’area da ritagliare e ridimensionatela o riposizionatela sull’immagine.
1. Utilizzate l’icona **Fine** (angolo in alto a destra) per ritagliare l’immagine. Facendo clic sull&#39;icona **Fine** si attiva anche la rigenerazione delle rappresentazioni.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Utilizza le icone **Annulla** e **Ripeti** in alto a destra rispettivamente per ripristinare l’immagine non ritagliata o mantenere l’immagine ritagliata.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Toccate/fate clic sull’icona Ruota appropriata per ruotare l’immagine in senso orario o antiorario.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Toccate/fate clic sull’icona Rifletti per riflettere l’immagine in orizzontale o verticale.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Toccate/fate clic sull’icona **Fine** per salvare le modifiche.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>La modifica delle immagini è supportata per i formati di file BMP, GIF, PNG e JPEG.

<!-- You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md). -->

>[!NOTE]
>
>Per modificare un file TXT, impostare **Day CQ Link Externalizer** da Configuration Manager.

## Timeline   {#timeline}

La timeline consente di visualizzare vari eventi per un elemento selezionato, ad esempio flussi di lavoro attivi per una risorsa, commenti/annotazioni, registri attività e versioni.

![Ordinare le voci della cronologia per una risorsa](assets/sort_timeline.gif)*Figura: Ordinare le voci della cronologia per una risorsa*

>[!NOTE]
>
>Nella console [](/help/assets/manage-collections.md#navigate-the-collections-console)Raccolte, l&#39;elenco **[!UICONTROL Mostra tutto]** contiene opzioni per visualizzare solo commenti e flussi di lavoro. Inoltre, la timeline viene visualizzata solo per le raccolte di livello principale elencate nella console. Non viene visualizzato se vi spostate all&#39;interno di una qualsiasi delle raccolte.

>[!NOTE]
>
>La timeline contiene diverse [opzioni specifiche per i frammenti](content-fragments/content-fragments.md)di contenuto.

## Annotazione {#annotating}

Le annotazioni sono commenti o note esplicative aggiunti alle immagini o ai video. Le annotazioni consentono agli addetti al marketing di collaborare e lasciare commenti sulle risorse.

Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. I formati video supportati da Risorse AEM dipendono dal browser.

>[!NOTE]
>
>Per i frammenti di contenuto, [le annotazioni vengono create nell’editor](content-fragments/content-fragments.md)frammento.

1. Andate alla posizione della risorsa alla quale desiderate aggiungere delle annotazioni.
1. Toccate/fate clic sull’icona **[!UICONTROL Annota]** da una delle seguenti opzioni:

   * [Azioni rapide](#quick-actions)
   * Dalla barra degli strumenti dopo aver selezionato la risorsa o aver aperto la pagina della risorsa
   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Aggiungi un commento nella casella **[!UICONTROL Commento]** posta nella parte inferiore della timeline. In alternativa, contrassegna un’area sull’immagine e aggiungi un’annotazione nella finestra di dialogo **[!UICONTROL Aggiungi annotazione]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.

   >[!NOTE]
   >
   >For a non-administrator user, suggestions appear only if the user has Read permissions at `/home` in CRXDE.

   ![chlimage_1-235](assets/chlimage_1-235.png)

1. After adding the annotation, click **[!UICONTROL Add]** to save it. A notification for the annotation is sent to Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >You can add multiple annotations, before you save them.

1. Tap/click **[!UICONTROL Close]** to exit from the Annotation mode.
1. To view the notification, log in to AEM Assets with Aaron MacDonald's credentials and click the **[!UICONTROL Notifications]** icon to view the notification.

   >[!NOTE]
   >
   >Annotations can also be added to video assets. While annotating videos, the player pauses to let you annotate on a frame. For details, see [managing video assets](manage-video-assets.md).

1. To choose a different color so you can differentiate between users, click/tap the Profile icon and click/tap **[!UICONTROL My Preferences]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Specify the desired color in the **[!UICONTROL Annotation Color]** box and then click/tap **[!UICONTROL Accept]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>You can also add annotations to a collection. However, if a collection contains child collections, you can add annotations/comments to the parent collection only. The Annotate option is not available for child collections.

### View saved annotations {#viewing-saved-annotations}

1. To view saved annotations for an asset, navigate to the location of the asset and open the asset page for the asset.

1. Tap/click the GlobalNav icon, and choose **[!UICONTROL Timeline]** from the list.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. From the **[!UICONTROL Show All]** list in the timeline, select **[!UICONTROL Comments]** to filter the results based on annotations.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Tap/click a comment in the **[!UICONTROL Timeline]** panel to view the corresponding annotation on the image.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Tap/click **[!UICONTROL Delete]**, to delete a particular comment.

### Print annotations {#printing-annotations}

If an asset has annotations or it has been subjected to a review workflow, you can print the asset along with annotations and review status as a PDF file for offline review.

You can also choose to print only the annotations or review status.

To print the annotations and review status, tap/click the **[!UICONTROL Print]** icon and follow the instructions in the wizard. The **[!UICONTROL Print]** icon appears in the toolbar only when the asset has at least one annotation or review status assigned to it.

1. From the Assets UI, open the preview page for an asset.
1. Do one of the following:

    * To print all the annotations and the review status, skip step 3 and directly go to step 4.
    * To print specific annotations and review status, open the [timeline](/help/assets/manage-digital-assets.md#timeline) and then go to step 3.

1. To print specific annotations, select the annotations from the timeline.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   To print the review status only, select it from the timeline.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Tap/click the **[!UICONTROL Print]** icon from the toolbar.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. From the Print dialog, choose the position you want the annotations/review status to be displayed on the PDF. For example, if you want the annotations/status to be printed at the top-right of the page that contains the printed image, use the **Top-Left** setting. It is selected by default.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   You can choose other settings depending on the position where you want the annotations/status to appear in the printed PDF. If you want the annotations/status to appear in a page that is separate from the printed asset, choose **[!UICONTROL Next Page]**.

   >[!NOTE]
   >
   >Lengthy annotations may not render properly in the PDF file. For optimal rendering, Adobe recommends that you limit annotations to 50 words.

1. Tap/click **[!UICONTROL Print]**. Depending upon the option you choose in step 2, the generated PDF displays the annotations/status at the specified position. For example, if you choose to print both annotations and the review status using the **Top-Left** setting, the generated output resembles the PDF file depicted here.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Download or print the PDF using the options at the top-right.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   To modify the appearance of the rendered PDF file, for example the font color, size, and style, background color of the comments and statuses, open the **[!UICONTROL Annotation PDF configuration]** from Configuration Manager, and modify the desired options. For example, to change the display color of the approved status, modify the color code in the corresponding field. For information around changing the font color of annotations, see [Annotating](/help/assets/manage-digital-assets.md#annotating).

   ![chlimage_1-248](assets/chlimage_1-248.png)

   Return to the rendered PDF file and refresh it. The refreshed PDF reflects the changes you made.

## Asset versioning {#asset-versioning}

Versioning creates a snapshot of digital assets at a specific point in time. Versioning helps restore assets to a previous state at a later time. For example, if you want to undo a change that you made to an asset, restore the unedited version of the asset.

The following are scenarios where you create versions:

* You modify an image in a different application and upload to AEM Assets. A version of the image is created so your original image is not overwritten.
* You edit the metadata of an asset.
* You use AEM desktop app to checkout an existing asset and save your changes. A new version is created everytime the asset is saved.

You can also enable automatic versioning through a workflow. When you create a version for an asset, the metadata and renditions are saved along with the version. Renditions are rendered alternatives of the same images, for example, a PNG rendition of an uploaded JPEG file.

The versioning functionality lets you do the following:

* Create a version of an asset.
* View the current revision for an asset.
* Restore the asset to a previous version.

1. Navigate to the location of the asset for which you want to create a version, and tap/click it to open its asset page.

1. Tap/click the GlobalNav icon, and the choose **[!UICONTROL Timeline]** from the menu.

   ![timeline](assets/timeline.png)

1. Tap/click the **[!UICONTROL Actions]** (arrow) icon at the bottom to view the available actions you can perform on the asset.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Tap/click **[!UICONTROL Save as Version]** to create a version for the asset.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Add a label and comment, and then click **[!UICONTROL Create]** to create a version. Alternatively, tap/click **Cancel** to exit the operation.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. To view the new version, open the **[!UICONTROL Show All]** list in the timeline from the asset details page or the Assets UI, and choose **[!UICONTROL Versions]**. All versions created for an asset are listed under the timeline tab. You can filter the list to show Versions, by clicking the drop arrow and selecting **[!UICONTROL Versions]** from the list.

   ![versions_option](assets/versions_option.png)

1. Select a specific version for the asset to preview it or enable it to appear in the Assets UI.

   ![select_version](assets/select_version.png)

1. Add a label and comment for the version to revert to the particular version in the Assets UI.

   ![save_version](assets/save_version.png)

1. To generate a preview for the version, tap/click **[!UICONTROL Preview Version]**.
1. To display this version in the Assets UI, select **[!UICONTROL Revert to this Version]**.
1. To compare between two versions, go to asset page of the asset and tap/click the version to be compared with the current version.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. From the timeline, select the version you want to compare and drag the slider to the left to superimpose this version over the current version and compare.

   ![compare_versions](assets/compare_versions.png)

### Starte a workflow on an asset {#starting-a-workflow-on-an-asset}

1. Navigate to the location of the asset for which you want to start a workflow, and tap/click the asset to open the asset page.
1. Tap/click the GlobalNav icon, and the choose **[!UICONTROL Timeline]** from the menu to display the timeline.

   ![timeline-1](assets/timeline-1.png)

1. Tap/click the **[!UICONTROL Actions]** (arrow) icon at the bottom to open the list of actions available for the asset.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Tap/click **[!UICONTROL Start Workflow]** from the list.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Optional) Specify a title for the workflow, which can be used to reference the workflow instance.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tap/click **[!UICONTROL Start]** and then tap/click **[!UICONTROL Proceed]** in the dialog to confirm. Each step of workflow is displayed in the timeline as an event.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Collections {#collections}

A collection is an ordered set of assets. Use collections to share assets between users.

* A collection can include assets from different locations because they only contain references to these assets. Each collection maintains the referential integrity of assets.
* You can share collections with multiple users with different privilege levels, including editing, viewing, and so on.

See [Managing Collections](/help/assets/manage-collections.md) for details on collection management.
