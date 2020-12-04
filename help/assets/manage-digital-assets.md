---
title: Consente di gestire i contenuti digitali
description: Scopri i diversi metodi di gestione e modifica delle risorse.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '4408'
ht-degree: 13%

---


# Gestire le risorse {#manage-assets}

Questo articolo descrive come gestire e modificare le risorse in Adobe Experience Manager Assets. Per gestire i frammenti di contenuto, vedere [Risorse frammenti di contenuto](content-fragments/content-fragments.md).

## Creare cartelle {#creating-folders}

Quando organizzate una raccolta di risorse, ad esempio tutte le immagini `Nature`, potete creare delle cartelle per mantenerle unite. Potete usare le cartelle per classificare e organizzare le risorse. [!DNL Experience Manager Assets] non richiede l’organizzazione di risorse in cartelle per migliorare il funzionamento.

>[!NOTE]
>
>* La condivisione di una cartella di risorse di tipo `sling:OrderedFolder` non è supportata quando si condivide un Marketing Cloud. Se desiderate condividere una cartella, non selezionate [!UICONTROL Ordinato] durante la creazione di una cartella.
>*  Experience Manager non consente l&#39;uso della parola `subassets` come nome di una cartella. È una parola chiave riservata al nodo che contiene risorse secondarie per le risorse composte


1. Andate alla posizione nella cartella delle risorse digitali in cui desiderate creare una nuova cartella. Scegliere **[!UICONTROL Crea]** dal menu. Selezionare **[!UICONTROL Nuova cartella]**.
1. Nel campo **[!UICONTROL Titolo]**, specificare un nome di cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, potete ignorare l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

I seguenti caratteri (elenco separato da spazi) non sono supportati:

* Il nome di un file di risorsa non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? &`
* Il nome di una cartella di risorse non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricare le risorse {#uploading-assets}

Consultate [aggiungere risorse digitali al Experience Manager ](add-assets.md).

## Rileva risorse duplicate {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Se un utente DAM carica una o più risorse già presenti nella directory archivio, [!DNL Experience Manager] rileva la duplicazione e invia una notifica all&#39;utente. Per impostazione predefinita, il rilevamento di duplicati è disabilitato in quanto può avere un impatto sulle prestazioni a seconda delle dimensioni dell&#39;archivio e del numero di risorse caricate. Per attivare la funzione, configurate il [!UICONTROL  Adobe AEM Rilevatore duplicazione risorse cloud]. Vedere [come eseguire configurazioni OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html). Il rilevamento della duplicazione si basa sul valore `dam:sha1` univoco memorizzato in `jcr:content/metadata/dam:sha1`. Ciò significa che le risorse duplicate vengono rilevate anche se i nomi dei file sono diversi.

![Rileva configurazione OSGi della risorsa duplicata](assets/duplicate-detection.png)

È possibile aggiungere il file di configurazione `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` nel codice personalizzato e il file può contenere quanto segue:

```json
{
  "enabled":true,
  "detectMetadataField":"dam:sha1"
}
```

Una volta attivato,  Experience Manager invia alla inbox le notifiche relative alle risorse duplicate. Si tratta di un risultato aggregato per più duplicati. Gli utenti possono scegliere di rimuovere le risorse in base ai risultati.

![Notifica Inbox per risorse duplicate](assets/duplicate-detect-inbox-notification.png)

## Visualizzare in anteprima le risorse {#previewing-assets}

Per visualizzare l’anteprima di una risorsa, effettuate le seguenti operazioni.

1. Dall’interfaccia utente Risorse, andate alla posizione della risorsa da visualizzare in anteprima.
1. Toccate la risorsa desiderata per aprirla.

1. Nella modalità di anteprima, le opzioni di zoom sono disponibili per [tipi di immagini supportati](/help/assets/file-format-support.md) (con modifica interattiva).

   Per ingrandire una risorsa, toccate o fate clic su `+` (oppure toccate o fate clic sulla lente di ingrandimento della risorsa). Per ridurre la visualizzazione, toccate o fate clic su `-`. Quando ingrandite, potete osservare da vicino qualsiasi area dell’immagine eseguendo il panning. La freccia di reimpostazione dello zoom consente di tornare alla visualizzazione originale.

   Toccate **[!UICONTROL Reimposta]** per ripristinare la visualizzazione alle dimensioni originali.

## Modifica delle proprietà {#editing-properties}

1. Andate alla posizione della risorsa di cui desiderate modificare i metadati.

1. Selezionate la risorsa, quindi toccate o fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti per visualizzare le proprietà della risorsa. In alternativa, scegliete l&#39;azione rapida **[!UICONTROL Proprietà]** sulla scheda delle risorse.

   ![properties_quickaction](assets/properties_quickaction.png)

1. Nella pagina [!UICONTROL Proprietà], modificate le proprietà dei metadati in varie schede. Ad esempio, nella scheda **[!UICONTROL Base]** modificare il titolo, la descrizione e così via.

   >[!NOTE]
   >
   >Il layout della pagina [!UICONTROL Properties] e le proprietà dei metadati disponibili dipendono dallo schema di metadati sottostante. Per informazioni su come modificare il layout della pagina [!UICONTROL Proprietà], vedere [Schemi di metadati](/help/assets/metadata-schemas.md).

1. Per pianificare una data/ora specifica per l’attivazione della risorsa, utilizza il selettore data posto accanto al campo **[!UICONTROL On Time (All’ora)]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Per disattivare la risorsa dopo una determinata durata, scegliete la data/ora di disattivazione dal selettore data accanto al campo **[!UICONTROL Ora di disattivazione]**. La data di disattivazione deve essere successiva alla data di attivazione di una risorsa. Dopo la [!UICONTROL Ora di disattivazione], una risorsa e le relative rappresentazioni non sono disponibili né tramite l&#39;interfaccia Web di Assets, né tramite l&#39;API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Nel campo **[!UICONTROL Tag]**, selezionare uno o più tag. Per aggiungere un tag personalizzato, digitate il nome del tag nella casella e premete il tasto Invio. Il nuovo tag viene salvato in [!DNL Experience Manager].

   YouTube richiede la pubblicazione di tag e un collegamento a YouTube (se è possibile trovare un collegamento appropriato).

   >[!NOTE]
   >
   >Per creare i tag, è necessario disporre dell&#39;autorizzazione di scrittura nel percorso `/content/cq:tags/default` dell&#39;archivio CRX.

1. Per visualizzare le statistiche di utilizzo della risorsa, tocca o fai clic sulla scheda **[!UICONTROL Insights]**.

   Le statistiche di utilizzo includono quanto segue:

   * Numero di volte in cui la risorsa è stata visualizzata o scaricata
   * Canali/dispositivi attraverso i quali è stata utilizzata la risorsa
   * Soluzioni creative in cui la risorsa è stata utilizzata di recente

   Per ulteriori dettagli, consultate [Informazioni sulle risorse](assets-insights.md).

1. Toccate/fate clic su **[!UICONTROL Salva e chiudi]**.

1. Passa all’interfaccia utente Risorse. Le proprietà dei metadati modificate, inclusi titolo, descrizione e tag, vengono visualizzate sulla scheda delle risorse nella vista a schede e nelle relative colonne nella vista Elenco.

## Copiare le risorse {#copying-assets}

Quando copiate una risorsa o una cartella, viene copiata l’intera risorsa o la cartella, insieme alla relativa struttura del contenuto. Una risorsa o una cartella copiata viene duplicata nel percorso di destinazione. La risorsa nella posizione di origine non viene modificata.

Alcuni attributi univoci per una particolare copia di una risorsa non vengono riportati avanti. Alcuni esempi sono:

* ID risorsa, data e ora di creazione, versioni e cronologia delle versioni. Alcune di queste proprietà sono indicate dalle proprietà `jcr:uuid`, `jcr:created` e `cq:name`.

* L’ora di creazione e i percorsi di riferimento sono univoci per ciascuna risorsa e per ciascuna delle relative rappresentazioni.

Le altre proprietà e informazioni sui metadati vengono mantenute. Durante la copia di una risorsa non viene creata una copia parziale.

1. Nell’interfaccia utente delle risorse, seleziona una o più risorse, quindi tocca o fai clic sull’icona **[!UICONTROL Copia]** nella barra degli strumenti. In alternativa, selezionate l&#39;azione rapida **[!UICONTROL Copy]** ![copy_icon](assets/copy_icon.png) dalla scheda delle risorse.

   >[!NOTE]
   >
   >Se utilizzate l&#39;azione rapida [!UICONTROL Copia], potete copiare una sola risorsa alla volta.

1. Andate alla posizione in cui desiderate copiare le risorse.

   >[!NOTE]
   >
   >Se copiate una risorsa nella stessa posizione, [!DNL Experience Manager] genera automaticamente una variante del nome. Ad esempio, se copiate una risorsa denominata `Square`, [!DNL Experience Manager] genera automaticamente il titolo della relativa copia come `Square1`.

1. Fate clic sull&#39;icona della risorsa **[!UICONTROL Incolla]** dalla barra degli strumenti. Le risorse vengono copiate in questa posizione.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >L&#39;icona **[!UICONTROL Incolla]** è disponibile nella barra degli strumenti fino al completamento dell&#39;operazione Incolla.

### Spostare o rinominare le risorse {#moving-or-renaming-assets}

1. Andate alla posizione della risorsa da spostare.

1. Selezionate la risorsa, quindi toccate o fate clic sull&#39;icona **[!UICONTROL Sposta]** ![move_icon](assets/move_icon.png) dalla barra degli strumenti.

1. Nella procedura guidata Sposta risorse, effettuate una delle seguenti operazioni:

   * Dopo averlo spostato, specificate il nome della risorsa. Quindi toccate/fate clic su **[!UICONTROL Next]** per proseguire.

   * Toccate/fate clic su **[!UICONTROL Annulla]** per interrompere il processo.
   >[!NOTE]
   >
   >* Potete specificare lo stesso nome per la risorsa se nella nuova posizione non è presente alcuna risorsa con lo stesso nome. Tuttavia, se spostate la risorsa in una posizione in cui esiste una risorsa con lo stesso nome, usate un nome diverso. Se usate lo stesso nome, il sistema genera automaticamente una variante del nome. Ad esempio, se la risorsa ha il nome Square, il sistema genera il nome Square1 per la relativa copia.
   >* Durante la ridenominazione, gli spazi bianchi non sono consentiti nel nome del file.


1. Nella finestra di dialogo **[!UICONTROL Seleziona destinazione]**, effettuare una delle seguenti operazioni:

   * Andate alla nuova posizione delle risorse, quindi toccate o fate clic su **[!UICONTROL Next]** per proseguire.

   * Toccate/fate clic su **[!UICONTROL Indietro]** per tornare alla schermata **[!UICONTROL Rinomina]**.

1. Se le risorse che state spostando dispongono di pagine, risorse o raccolte di riferimento, accanto alla scheda **[!UICONTROL Seleziona destinazione]** viene visualizzata la scheda **[!UICONTROL Regola riferimenti]**.

   Effettuare una delle seguenti operazioni nella schermata **[!UICONTROL Regola riferimenti]**:

   * Specificate i riferimenti da modificare in base ai nuovi dettagli, quindi toccate o fate clic su **[!UICONTROL Sposta]** per proseguire.

   * Dalla colonna **[!UICONTROL Regola]**, selezionate/deselezionate i riferimenti alle risorse.
   * Toccate/fate clic su **[!UICONTROL Indietro]** per tornare alla schermata **[!UICONTROL Seleziona destinazione]**.

   * Toccate/fate clic su **[!UICONTROL Annulla]** per interrompere l&#39;operazione di spostamento.

   Se non aggiornate i riferimenti, continueranno a indicare il percorso precedente della risorsa. Se regolate i riferimenti, questi vengono aggiornati al nuovo percorso della risorsa.

### Gestire le rappresentazioni {#managing-renditions}

1. Potete aggiungere o rimuovere rappresentazioni per una risorsa, tranne l’originale. Andate alla posizione della risorsa per la quale desiderate aggiungere o rimuovere le rappresentazioni.

1. Toccate o fate clic sulla risorsa per aprirne la pagina.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Toccate/fate clic sull&#39;icona di navigazione globale, quindi selezionate **[!UICONTROL Rappresentazioni]** dall&#39;elenco.

   ![renditions_menu](assets/renditions_menu.png)

1. Nel pannello **[!UICONTROL Rappresentazioni]**, visualizzate l&#39;elenco delle rappresentazioni generate per la risorsa.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, [!DNL Experience Manager Assets] non visualizza la rappresentazione originale della risorsa in modalità di anteprima. Se siete un amministratore, potete utilizzare le sovrapposizioni per configurare [!DNL Assets] per visualizzare le rappresentazioni originali in modalità di anteprima.

1. Selezionate una rappresentazione per visualizzare o eliminare la rappresentazione.

   **Eliminazione di una rappresentazione**

   Selezionate una rappresentazione dal pannello **[!UICONTROL Rappresentazioni]**, quindi toccate o fate clic sull&#39;icona **[!UICONTROL Elimina rappresentazione]** nella barra degli strumenti. Le rappresentazioni non possono essere eliminate in blocco al termine dell’elaborazione delle risorse. Per le singole risorse, potete rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, potete personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche o per eliminare le risorse e caricare nuovamente le risorse eliminate.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Caricamento di una nuova rappresentazione**

   Vai alla pagina dei dettagli della risorsa, quindi tocca o fai clic sull’icona **[!UICONTROL Aggiungi rappresentazione]** della barra degli strumenti per caricare una nuova rappresentazione della risorsa.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Se selezioni un rendering dal pannello **[!UICONTROL Rendering]**, la barra degli strumenti cambia contesto, visualizzando solo le azioni del rendering specifico. Le opzioni non sono visualizzate, ad esempio l’icona Carica rappresentazione. Per visualizzare queste opzioni nella barra degli strumenti, vai alla pagina dei dettagli della risorsa.

   Potete configurare le dimensioni per la rappresentazione da visualizzare nella pagina dei dettagli di un’immagine o di una risorsa video. In base alle dimensioni specificate, Assets visualizza la rappresentazione con le dimensioni esatte o più vicine.

   Per configurare le dimensioni di rendering di un’immagine a livello di dettaglio della risorsa, sovrapponi il nodo `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configura il valore della proprietà larghezza.  Per personalizzare il rendering sulla pagina dei dettagli della risorsa in base alle dimensioni dell’immagine, configura la proprietà **[!UICONTROL size (Long) in KB (dimensione (lunga) in KB)]** al posto della larghezza. Per la personalizzazione basata sulle dimensioni, la proprietà `preferOriginal` assegna le preferenze all’originale se la dimensione del rendering corrispondente è maggiore.

   Analogamente, potete personalizzare l&#39;immagine della pagina Annotazione sovrapponendo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Per configurare le dimensioni di rappresentazione per una risorsa video, andate al nodo `videopicker` nell&#39;archivio CRX nella posizione `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sovrapponete il nodo, quindi modificate la proprietà appropriata.

   >[!NOTE]
   >
   >Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. Inoltre, a seconda del browser, sono supportati diversi formati video.

## Elimina risorse {#delete-assets}

Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiornate i riferimenti pertinenti prima di eliminare una risorsa.

Inoltre, disattivate il pulsante Forza eliminazione con una sovrapposizione, per impedire agli utenti di eliminare le risorse di riferimento e di lasciare i collegamenti interrotti.

1. Andate alla posizione delle risorse che desiderate eliminare.

1. Selezionate la risorsa, quindi toccate o fate clic sull&#39;icona **[!UICONTROL Elimina]** nella barra degli strumenti.

   ![delete_icon](assets/delete_icon.png)

1. Nella finestra di dialogo di conferma, fate clic su:

   * **[!UICONTROL Annulla per]** interrompere l’azione
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

Consultate [Scaricare risorse da [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Pubblicare risorse {#publish-assets}

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

1. Toccate/fate clic su **[!UICONTROL Pubblica]** per confermare l&#39;attivazione delle risorse.

>[!CAUTION]
>
>Se pubblicate una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano le rappresentazioni. Attendere il completamento dell’elaborazione, quindi pubblicare o pubblicare nuovamente la risorsa al termine dell’elaborazione.

## Annulla pubblicazione risorse {#unpublishing-assets}

1. Andate alla posizione della cartella di risorse o risorse che desiderate rimuovere dall’ambiente di pubblicazione (Annulla pubblicazione).

1. Selezionate la risorsa o la cartella da annullare la pubblicazione, quindi toccate o fate clic sull&#39;icona **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti.

   ![manage_publication](assets/manage_publication.png)

1. Selezionare l&#39;azione **[!UICONTROL Annulla pubblicazione]** dall&#39;elenco.

   ![unpublish_action](assets/unpublish_action.png)

1. Per annullare la pubblicazione della risorsa in un secondo momento, selezionate **[!UICONTROL Annulla pubblicazione più tardi]**, quindi selezionate una data per l’annullamento della pubblicazione della risorsa.
1. Pianificate una data in cui la risorsa non sarà disponibile dall’ambiente di pubblicazione.
1. Se la risorsa fa riferimento ad altre risorse, scegliete i riferimenti da annullare la pubblicazione. Toccate/fate clic su **[!UICONTROL Annulla pubblicazione]**.
1. Nella finestra di dialogo di conferma, toccate o fate clic su:

   * **[!UICONTROL Annulla per]** interrompere l’azione
   * **[!UICONTROL Annulla]** pubblicazione per confermare che le risorse non sono pubblicate (non sono più disponibili nell’ambiente di pubblicazione) alla data specificata.

   >[!NOTE]
   >
   >Quando si annulla la pubblicazione di una risorsa complessa, è necessario annullare la pubblicazione solo della risorsa. Evitate di annullare la pubblicazione dei riferimenti, in quanto ad essi potrebbero fare riferimento altre risorse pubblicate.

## Gruppo utenti chiuso {#closed-user-group}

Un gruppo di utenti chiuso (CUG) viene usato per limitare l’accesso a specifiche cartelle di risorse pubblicate da [!DNL Experience Manager]. Se create un gruppo di utenti chiuso per una cartella, l’accesso alla cartella (comprese le risorse e le sottocartelle) è limitato solo ai membri o ai gruppi assegnati. Per accedere alla cartella, devono accedere utilizzando le credenziali di protezione.

I COG consentono di limitare l’accesso alle risorse. Potete anche configurare una pagina di login per la cartella.

1. Selezionate una cartella dall’interfaccia utente Risorse, quindi toccate o fate clic sull’icona Proprietà dalla barra degli strumenti per visualizzare la pagina delle proprietà.
1. Dalla scheda **[!UICONTROL Autorizzazioni]**, aggiungere membri o gruppi in **[!UICONTROL Gruppo utenti chiuso]**.

   ![add_user](assets/add_user.png)

1. Per visualizzare una schermata di login quando gli utenti accedono alla cartella, selezionate l&#39;opzione **[!UICONTROL Abilita]**. Quindi, seleziona il percorso di una pagina di login in [!DNL Experience Manager] e salva le modifiche.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Se non si specifica il percorso di una pagina di login, [!DNL Experience Manager] visualizza la pagina di login predefinita nell&#39;istanza di pubblicazione.

1. Pubblicate la cartella, quindi provate ad accedervi dall’istanza di pubblicazione. Viene visualizzata una schermata di login.
1. Se siete un membro CUG, immettete le vostre credenziali di protezione. La cartella viene visualizzata dopo l&#39;autenticazione di [!DNL Experience Manager].

## Cercare risorse {#search-assets}

La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e degli esperti di marketing, sia per l’amministrazione da parte degli amministratori DAM.

Per ricerche semplici, avanzate e personalizzate per individuare e utilizzare le risorse più appropriate, consultate [cercare risorse in [!DNL Experience Manager]](/help/assets/search-assets.md).

## Azioni rapide {#quick-actions}

Le icone delle azioni rapide sono disponibili per una singola risorsa alla volta. A seconda del dispositivo, effettuate le seguenti operazioni per visualizzare le icone delle azioni rapide:

* Dispositivi touch: Toccate e tenete premuto. Ad esempio, su un iPad potete toccare e tenere premuto un contenuto per visualizzare le azioni rapide.
* Dispositivi non touch: Puntatore al passaggio del mouse. Ad esempio, su un dispositivo desktop, se passate il puntatore sulla miniatura della risorsa viene visualizzata la barra delle azioni rapide.

## Modificare le immagini {#editing-images}

Gli strumenti di modifica nell&#39;interfaccia [!DNL Experience Manager Assets] consentono di eseguire piccoli processi di modifica sulle risorse di immagine. Potete ritagliare, ruotare, capovolgere ed eseguire altri processi di modifica sulle immagini. Potete anche aggiungere mappe immagine alle risorse.

>[!NOTE]
>
>Per alcuni componenti, la modalità Schermo intero dispone di opzioni aggiuntive.

1. Per aprire una risorsa in modalità di modifica, effettuate una delle seguenti operazioni:

   * Selezionate la risorsa, quindi toccate o fate clic sull&#39;icona **[!UICONTROL Modifica]** nella barra degli strumenti.
   * Toccate/fate clic sull&#39;icona **[!UICONTROL Modifica]** visualizzata su una risorsa nella vista a schede.
   * Nella pagina della risorsa, tocca o fai clic sull&#39;icona **[!UICONTROL Modifica]** nella barra degli strumenti.

   ![edit_icon](assets/edit_icon.png)

1. Per ritagliare l&#39;immagine, toccate o fate clic sull&#39;icona **Ritaglia**.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Seleziona l’opzione desiderata dall’elenco. L’area di ritaglio viene visualizzata sull’immagine in base all’opzione scelta. L’opzione **Mano libera** consente di ritagliare l’immagine senza limitazioni di proporzioni.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Selezionate l’area da ritagliare e ridimensionatela o riposizionatela sull’immagine.
1. Utilizzate l&#39;icona **Fine** (angolo in alto a destra) per ritagliare l&#39;immagine. Facendo clic sull&#39;icona **Fine** si attiva anche la rigenerazione delle rappresentazioni.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Utilizza le icone **Annulla** e **Ripeti** in alto a destra rispettivamente per ripristinare l’immagine non ritagliata o mantenere l’immagine ritagliata.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Toccate/fate clic sull’icona Ruota appropriata per ruotare l’immagine in senso orario o antiorario.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Toccate/fate clic sull’icona Rifletti per riflettere l’immagine in orizzontale o verticale.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Toccate/fate clic sull&#39;icona **Fine** per salvare le modifiche.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>La modifica delle immagini è supportata per i formati di file BMP, GIF, PNG e JPEG.

<!-- You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md). -->

>[!NOTE]
>
>Per modificare un file TXT, impostare **Day CQ Link Externalizer** da Configuration Manager.

## Timeline  {#timeline}

La timeline consente di visualizzare vari eventi per un elemento selezionato, ad esempio flussi di lavoro attivi per una risorsa, commenti/annotazioni, registri attività e versioni.

![Ordinare le voci della timeline per una ](assets/sort_timeline.gif)
*risorsaFigura: Ordinare le voci della cronologia per una risorsa*

>[!NOTE]
>
>Nella [console Raccolte](/help/assets/manage-collections.md#navigate-the-collections-console), l&#39;elenco **[!UICONTROL Mostra tutto]** contiene opzioni per visualizzare solo i commenti e i flussi di lavoro. Inoltre, la timeline viene visualizzata solo per le raccolte di livello principale elencate nella console. Non viene visualizzato se vi spostate all&#39;interno di una qualsiasi delle raccolte.

>[!NOTE]
>
>La timeline contiene diverse opzioni [specifiche per i frammenti di contenuto](content-fragments/content-fragments.md).

## Annotazione {#annotating}

Le annotazioni sono commenti o note esplicative aggiunti alle immagini o ai video. Le annotazioni consentono agli addetti al marketing di collaborare e lasciare commenti sulle risorse.

Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. I formati video supportati da Risorse dipendono dal browser.

>[!NOTE]
>
>Per i frammenti di contenuto, nell&#39;editor frammento [ vengono create delle annotazioni.](content-fragments/content-fragments.md)

1. Andate alla posizione della risorsa alla quale desiderate aggiungere delle annotazioni.
1. Toccate/fate clic sull&#39;icona **[!UICONTROL Annota]** da una delle seguenti opzioni:

   * [Azioni rapide](#quick-actions)
   * Dalla barra degli strumenti dopo aver selezionato la risorsa o aver aperto la pagina della risorsa

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Aggiungi un commento nella casella **[!UICONTROL Commento]** posta nella parte inferiore della timeline. In alternativa, contrassegna un’area sull’immagine e aggiungi un’annotazione nella finestra di dialogo **[!UICONTROL Aggiungi annotazione]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Per un utente non amministratore, i suggerimenti vengono visualizzati solo se l&#39;utente dispone di autorizzazioni di lettura in `/home` in CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. Dopo aver aggiunto l&#39;annotazione, fare clic su **[!UICONTROL Aggiungi]** per salvarla. Una notifica per l’annotazione viene inviata ad Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >Potete aggiungere più annotazioni prima di salvarle.

1. Toccate/fate clic su **[!UICONTROL Chiudi]** per uscire dalla modalità Annotazione.
1. Per visualizzare la notifica, accedi a Risorse con le credenziali di Aaron MacDonald e fai clic sull&#39;icona **[!UICONTROL Notifiche]** per visualizzare la notifica.

   >[!NOTE]
   >
   >Potete anche aggiungere delle annotazioni alle risorse video. Durante l&#39;annotazione dei video, il lettore si mette in pausa per consentire di inserire delle annotazioni in un fotogramma. Per informazioni dettagliate, consultate [Gestione delle risorse video](manage-video-assets.md).

1. Per scegliere un colore diverso in modo da poter differenziare tra gli utenti, tocca o fai clic sull&#39;icona Profilo e tocca **[!UICONTROL Preferenze personali]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Nella casella **[!UICONTROL Colore annotazione]**, specifica il colore desiderato, infine tocca o fai clic su **[!UICONTROL Accetta]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>Potete inoltre aggiungere annotazioni a una raccolta. Tuttavia, se una raccolta contiene raccolte figlie, potete aggiungere solo annotazioni/commenti alla raccolta principale. L&#39;opzione Annota non è disponibile per le raccolte figlie.

### Visualizzare le annotazioni salvate {#viewing-saved-annotations}

1. Per visualizzare le annotazioni salvate per una risorsa, andate alla posizione della risorsa e aprite la pagina della risorsa.

1. Toccate/fate clic sull&#39;icona di navigazione globale e scegliete **[!UICONTROL Timeline]** dall&#39;elenco.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. Dall’elenco **[!UICONTROL Mostra tutti]** nella timeline, seleziona **[!UICONTROL Commenti]** per filtrare i risultati in base alle annotazioni.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Toccate/fate clic su un commento nel pannello **[!UICONTROL Timeline]** per visualizzare l&#39;annotazione corrispondente sull&#39;immagine.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Toccate/fate clic su **[!UICONTROL Elimina]** per eliminare un particolare commento.

### Stampa annotazioni {#printing-annotations}

Se una risorsa dispone di annotazioni o è stata sottoposta a un flusso di lavoro di revisione, potete stampare la risorsa insieme alle annotazioni e rivedere lo stato come file PDF per la revisione offline.

Potete anche scegliere di stampare solo le annotazioni o lo stato della revisione.

Per stampare le annotazioni e verificare lo stato, toccate o fate clic sull&#39;icona **[!UICONTROL Stampa]** e seguite le istruzioni della procedura guidata. L&#39;icona **[!UICONTROL Stampa]** viene visualizzata nella barra degli strumenti solo se alla risorsa è assegnata almeno un&#39;annotazione o uno stato di revisione.

1. Nell’interfaccia utente delle risorse, apri la pagina di anteprima per una risorsa.
1. Effettua una delle operazioni seguenti:

   * Per stampare tutte le annotazioni e lo stato della revisione, saltate il punto 3 e andate direttamente al punto 4.
   * Per stampare annotazioni specifiche e verificare lo stato, aprite la [timeline](/help/assets/manage-digital-assets.md#timeline) e passate al punto 3.

1. Per stampare annotazioni specifiche, selezionate le annotazioni dalla timeline.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Per stampare solo lo stato della revisione, selezionatelo dalla timeline.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Toccate/fate clic sull&#39;icona **[!UICONTROL Stampa]** nella barra degli strumenti.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Nella finestra di dialogo Stampa, scegliete la posizione in cui visualizzare le annotazioni o lo stato della revisione sul PDF. Ad esempio, per stampare le annotazioni/lo stato in alto a destra della pagina contenente l&#39;immagine stampata, utilizzare l&#39;impostazione **In alto a sinistra**. È selezionato per impostazione predefinita.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   È possibile scegliere altre impostazioni, a seconda della posizione in cui si desidera visualizzare le annotazioni o lo stato nel PDF stampato. Se vuoi che le annotazioni o lo stato vengano visualizzati in una pagina separata dalla risorsa stampata, scegli **[!UICONTROL Pagina successiva]**.

   >[!NOTE]
   >
   >Il rendering delle annotazioni lunghe potrebbe non essere corretto nel file PDF. Per un rendering ottimale,  Adobe consiglia di limitare le annotazioni a 50 parole.

1. Tocca o fai clic su **[!UICONTROL Stampa]**. A seconda dell’opzione scelta al passaggio 2, il PDF generato visualizza annotazioni/stato nella posizione specificata. Ad esempio, se scegli di stampare sia le annotazioni che lo stato di revisione utilizzando l’impostazione **In alto a sinistra**, l’output generato sarà simile al file PDF qui riportato.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Scaricate o stampate il PDF utilizzando le opzioni in alto a destra.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   Per modificare l&#39;aspetto del file PDF sottoposto a rendering, ad esempio il colore, la dimensione e lo stile del font, il colore di sfondo dei commenti e degli stati, aprire la **[!UICONTROL configurazione PDF delle annotazioni]** in Gestione configurazione e modificare le opzioni desiderate. Ad esempio, per modificare il colore di visualizzazione dello stato approvato, modificate il codice colore nel campo corrispondente. Per informazioni sulla modifica del colore font delle annotazioni, vedere [Annotazione](/help/assets/manage-digital-assets.md#annotating).

   ![chlimage_1-248](assets/chlimage_1-248.png)

   Tornare al file PDF di cui è stato effettuato il rendering e aggiornarlo. Il PDF aggiornato riflette le modifiche apportate.

## Versione risorsa {#asset-versioning}

Il controllo delle versioni crea un’istantanea delle risorse digitali in un momento preciso. La gestione delle versioni consente di ripristinare le risorse a uno stato precedente in un secondo momento. Ad esempio, se desiderate annullare una modifica apportata a una risorsa, ripristinate la versione non modificata della risorsa.

Di seguito sono riportati gli scenari in cui si creano le versioni:

* Potete modificare un’immagine in un’altra applicazione e caricarla in Risorse. Viene creata una versione dell’immagine in modo che l’immagine originale non venga sovrascritta.
* Potete modificare i metadati di una risorsa.
* Utilizzate l&#39;app desktop [!DNL Experience Manager] per estrarre una risorsa esistente e salvare le modifiche. Una nuova versione viene creata ogni volta che la risorsa viene salvata.

Potete inoltre abilitare il controllo automatico delle versioni tramite un flusso di lavoro. Quando create una versione per una risorsa, i metadati e le rappresentazioni vengono salvati insieme alla versione. Le rappresentazioni sono alternative per il rendering delle stesse immagini, ad esempio una rappresentazione PNG di un file JPEG caricato.

La funzione di controllo delle versioni consente di effettuare le seguenti operazioni:

* Create una versione di una risorsa.
* Visualizzare la revisione corrente per una risorsa.
* Ripristinare una versione precedente della risorsa.

1. Andate alla posizione della risorsa per la quale desiderate creare una versione e toccatela o fate clic per aprire la pagina della risorsa.

1. Toccate/fate clic sull&#39;icona di navigazione globale e scegliete **[!UICONTROL Timeline]** dal menu.

   ![timeline](assets/timeline.png)

1. Toccate/fate clic sull&#39;icona **[!UICONTROL Azioni]** (freccia) in basso per visualizzare le azioni disponibili che potete eseguire sulla risorsa.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Toccate/fate clic su **[!UICONTROL Salva come versione]** per creare una versione per la risorsa.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Aggiungete un&#39;etichetta e un commento, quindi fate clic su **[!UICONTROL Crea]** per creare una versione. In alternativa, toccate o fate clic su **Annulla** per uscire dall&#39;operazione.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Per visualizzare la nuova versione, apri l’elenco **[!UICONTROL Mostra tutti]** nella timeline dalla pagina dei dettagli della risorsa o dall’interfaccia utente Assets, quindi scegli **[!UICONTROL Versioni]**. Tutte le versioni create per una risorsa sono elencate nella scheda della timeline. Puoi filtrare l’elenco Versioni, facendo clic sulla freccia rivolta verso il basso e selezionando **[!UICONTROL Versioni]** dall’elenco.

   ![version_option](assets/versions_option.png)

1. Selezionate una versione specifica della risorsa per visualizzarla in anteprima o consentirne la visualizzazione nell’interfaccia utente delle risorse.

   ![select_version](assets/select_version.png)

1. Aggiungi un’etichetta e un commento alla versione per ripristinare la versione specifica nell’interfaccia utente delle risorse.

   ![save_version](assets/save_version.png)

1. Per generare un’anteprima per la versione, tocca o fai clic su **[!UICONTROL Anteprima versione]**.
1. Per visualizzare questa versione nell&#39;interfaccia utente delle risorse, seleziona **[!UICONTROL Ripristina questa versione]**.
1. Per confrontare tra due versioni, andate alla pagina delle risorse e toccate o fate clic sulla versione da confrontare con la versione corrente.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. Dalla timeline, selezionate la versione da confrontare e trascinate il cursore verso sinistra per sovrapporre la versione corrente alla versione corrente e confrontarla.

   ![compare_version](assets/compare_versions.png)

### Avviare un flusso di lavoro su una risorsa {#starting-a-workflow-on-an-asset}

1. Andate alla posizione della risorsa per la quale desiderate avviare un flusso di lavoro, quindi toccate o fate clic sulla risorsa per aprire la pagina della risorsa.
1. Toccate/fate clic sull&#39;icona GlobalNav, quindi scegliete **[!UICONTROL Timeline]** dal menu per visualizzare la timeline.

   ![timeline-1](assets/timeline-1.png)

1. Toccate/fate clic sull&#39;icona **[!UICONTROL Azioni]** (freccia) in basso per aprire l&#39;elenco delle azioni disponibili per la risorsa.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Toccate/fate clic su **[!UICONTROL Avvia flusso di lavoro]** dall&#39;elenco.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. Nella finestra di dialogo **[!UICONTROL Avvia flusso di lavoro]**, selezionare un modello di workflow dall&#39;elenco.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Facoltativo) Specificate un titolo per il flusso di lavoro, che può essere utilizzato per fare riferimento all’istanza del flusso di lavoro.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tocca o fai clic su **[!UICONTROL Avvia]**, quindi, per confermare, tocca o fai clic su **[!UICONTROL Procedi]** nella finestra di dialogo. Ciascun passaggio del flusso di lavoro viene visualizzato nella timeline come un evento.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Raccolte {#collections}

Una raccolta è un set ordinato di risorse. Utilizzate le raccolte per condividere le risorse tra gli utenti.

* Una raccolta può includere risorse da posizioni diverse perché contiene solo riferimenti a tali risorse. Ciascuna raccolta mantiene l&#39;integrità referenziale delle risorse.
* Potete condividere le raccolte con più utenti con diversi livelli di privilegi, tra cui la modifica, la visualizzazione e così via.

Per informazioni dettagliate sulla gestione delle raccolte, consultate [Gestione delle raccolte](/help/assets/manage-collections.md).
