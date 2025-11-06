---
title: Come tradurre le risorse in AEM?
description: Scopri come automatizzare i flussi di lavoro per tradurre le risorse in AEM, inclusi file binari, metadati e tag, in più lingue.
contentOwner: AG
feature: Asset Management, Translation
role: Admin, User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2615'
ht-degree: 18%

---

# Tradurre le risorse in AEM {#multilingual-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/multilingual-assets.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Risorse multilingue significa risorse con binari, metadati e tag in più lingue. In genere, i file binari, i metadati e i tag per le risorse esistono in una lingua e vengono quindi tradotti in altre lingue per l’utilizzo in progetti multilingue. Adobe Experience Manager Assets consente di automatizzare i flussi di lavoro per tradurre le risorse (inclusi file binari, metadati e tag) e generare risorse in altre lingue da utilizzare nei progetti multilingue.

Per automatizzare la traduzione delle risorse in AEM, puoi integrare fornitori di servizi di traduzione con Experience Manager e creare progetti per tradurre le risorse in più lingue. Experience Manager supporta flussi di lavoro di traduzione umana e automatica.

Traduzione delle risorse umane in AEM: le risorse tradotte vengono restituite e importate in Experience Manager. Quando il provider di traduzione è integrato con Experience Manager, le risorse vengono inviate automaticamente tra Experience Manager e il provider di traduzione.

Traduzione automatica delle risorse in AEM: il servizio di traduzione automatica traduce immediatamente i metadati e i tag per le risorse.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html?lang=it
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html?lang=it
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html?lang=it)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html?lang=it

-->

<!-- 
Translating assets includes the following:

1. [Connecting Experience Manager with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## Preparare la traduzione delle risorse {#prepare-to-translate-assets}

Risorse multilingue significa risorse con binari, metadati e tag in più lingue. In genere, i file binari, i metadati e i tag per le risorse esistono in una lingua e vengono quindi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In Adobe Experience Manager Assets, le risorse multilingue sono incluse nelle cartelle, dove ogni cartella contiene le risorse in una lingua diversa.

Ogni cartella della lingua è denominata copia per lingua. La cartella principale di una copia per lingua, nota come directory principale della lingua, identifica la lingua del contenuto nella copia per lingua. `/content/dam/it`, ad esempio, è la directory principale della lingua italiana per la copia in lingua italiana. Le copie per lingua devono utilizzare una [directory principale lingua configurata correttamente](#create-a-language-root) in modo che la lingua corretta venga utilizzata quando vengono eseguite le traduzioni delle risorse di origine.

La copia per lingua per la quale originariamente hai aggiunto le risorse è la lingua principale. La lingua primaria è la fonte che viene tradotta in altre lingue. Una gerarchia di cartelle di esempio include diverse directory principali della lingua:

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

Per preparare la traduzione delle risorse, effettua le seguenti operazioni:

1. Crea la directory principale della lingua principale. Ad esempio, la directory principale della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Verificare che la directory principale della lingua sia configurata correttamente in base alle informazioni in [Creare una directory principale della lingua](#create-a-language-root).

1. Aggiungi risorse alla lingua principale.
1. Crea la directory principale della lingua di ogni lingua di destinazione per la quale hai bisogno di una copia per lingua.

### Creare una directory principale della lingua {#create-a-language-root}

Per creare la directory principale della lingua, è necessario creare una cartella e utilizzare un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la directory principale della lingua, puoi creare una copia per lingua a qualsiasi livello all’interno della directory principale della lingua.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia di esempio ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nell’archivio e quindi determina il percorso delle risorse. (*&lt;server>:&lt;porta>/assets.html/content/dam/it/*)

1. Dalla console di Assets, seleziona **[!UICONTROL Crea]** e scegli **[!UICONTROL Cartella]** dal menu.
1. Nel campo Nome digitare il codice del paese nel formato `<language-code>`.
1. Seleziona **[!UICONTROL Crea]**. La directory principale della lingua viene creata nella console Assets.

### Visualizza directory principali della lingua {#view-language-roots}

L&#39;interfaccia utente ottimizzata per il tocco fornisce un pannello Riferimenti che mostra un elenco di directory principali della lingua create in [!DNL Assets].

1. Nella console Assets, seleziona la lingua principale per la quale desideri creare le copie per lingua.
1. Seleziona l&#39;icona GlobalNav e scegli **[!UICONTROL Riferimenti]** per aprire il riquadro Riferimenti.
1. Nel riquadro Riferimenti selezionare **[!UICONTROL Copie per lingua]**. Il pannello Copie per lingua mostra le copie per lingua delle risorse.

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project}

Se utilizzi questa opzione, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. A seconda delle opzioni scelte, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o eseguito automaticamente non appena viene creato.

1. Nell’interfaccia utente di Assets, seleziona la cartella di origine per la quale desideri creare una copia in lingua.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e seleziona **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**.
1. Seleziona **[!UICONTROL Crea e traduci]** in basso.
1. Dall&#39;elenco **[!UICONTROL Lingue di destinazione]**, selezionare le lingue per le quali si desidera creare una struttura di cartelle.
1. Dall&#39;elenco **[!UICONTROL Progetto]**, selezionare **[!UICONTROL Crea un nuovo progetto di traduzione]**.
1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.
1. Seleziona **[!UICONTROL Crea]**. Assets dalla cartella di origine viene copiato nelle cartelle di destinazione per le impostazioni internazionali selezionate al passaggio 4.
1. Per passare alla cartella, selezionare la copia per lingua e fare clic su **[!UICONTROL Mostra in Assets]**.
1. Passa alla console Progetti. La cartella di traduzione viene copiata nella console Progetti.
1. Apri la cartella per visualizzare il progetto di traduzione.
1. Seleziona il progetto per aprire la pagina dei dettagli.
1. Per visualizzare lo stato del processo di traduzione, fai clic sui puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Nell’interfaccia utente di Assets, apri la pagina Proprietà di ciascuna delle risorse tradotte per visualizzare i metadati tradotti.

>[!NOTE]
>
>Questa funzione è disponibile sia per le risorse che per le cartelle. Quando viene selezionata una risorsa invece di una cartella, l’intera gerarchia di cartelle fino alla directory principale della lingua viene copiata per creare una copia per lingua della risorsa.

### Aggiungi a un progetto di traduzione esistente {#add-to-existing-translation-project}

Se utilizzi questa opzione, il flusso di lavoro di traduzione viene eseguito per le risorse aggiunte alla cartella di origine dopo l’esecuzione di un flusso di lavoro di traduzione precedente. Solo le risorse appena aggiunte vengono copiate nella cartella di destinazione che contiene le risorse tradotte in precedenza. In questo caso non viene creato alcun nuovo progetto di traduzione.

1. Nell’interfaccia utente di Assets, passa alla cartella di origine che contiene le risorse non tradotte.
1. Seleziona una risorsa da tradurre e apri il **[!UICONTROL riquadro Riferimento]**. Nella sezione **[!UICONTROL Copie per lingua]** viene visualizzato il numero di copie di traduzione attualmente disponibili.
1. Seleziona **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**. Viene visualizzato un elenco delle copie di traduzione disponibili.
1. Seleziona **[!UICONTROL Crea e traduci]** in basso.
1. Dall&#39;elenco **[!UICONTROL Lingue di destinazione]**, selezionare le lingue per le quali si desidera creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Aggiungi al progetto di traduzione esistente]** per eseguire il flusso di lavoro di traduzione nella cartella.

   >[!NOTE]
   >
   >Se si sceglie l&#39;opzione **[!UICONTROL Aggiungi al progetto di traduzione esistente]**, il progetto di traduzione verrà aggiunto a un progetto preesistente solo se le impostazioni del progetto corrispondono esattamente a quelle del progetto preesistente. In caso contrario, viene creato un nuovo progetto.

1. Dall&#39;elenco **[!UICONTROL Progetto di traduzione esistente]**, seleziona un progetto per aggiungere la risorsa per la traduzione.
1. Seleziona **[!UICONTROL Crea]**. Le risorse da tradurre vengono aggiunte alla cartella di destinazione. La cartella aggiornata è elencata nella sezione **[!UICONTROL Copie per lingua]**.
1. Passa alla console Progetti e apri il progetto di traduzione esistente aggiunto a.
1. Seleziona il progetto di traduzione per visualizzare la pagina dei dettagli del progetto.
1. Seleziona i puntini di sospensione nella parte inferiore del riquadro **Processo di traduzione** per visualizzare le risorse nel flusso di lavoro di traduzione. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

   >[!NOTE]
   >
   >* Se elimini la voce per tag o metadati, nessun tag o metadati viene tradotto per nessuna delle risorse.
   >* Se utilizzi la traduzione automatica, i file binari delle risorse non vengono tradotti.
   >* Se la risorsa aggiunta al processo di traduzione include risorse secondarie, selezionale e rimuovile affinché la traduzione possa procedere senza errori.

1. Per avviare la traduzione delle risorse, seleziona la freccia nella sezione **[!UICONTROL Processo di traduzione]** e seleziona **[!UICONTROL Inizio]** dall&#39;elenco. Un messaggio notifica l’inizio del processo di traduzione.
1. Per visualizzare lo stato del processo di traduzione, seleziona i puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Al termine della traduzione, lo stato diventa Pronto per la revisione. Passa all’interfaccia utente di Assets e apri la pagina Proprietà di ciascuna delle risorse tradotte per visualizzare i metadati tradotti.

### Aggiorna copie per lingua {#update-language-copies}

Esegui questo flusso di lavoro per tradurre qualsiasi set aggiuntivo di risorse e includerlo in una copia per lingua specifica. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già le risorse tradotte in precedenza. A seconda della scelta di opzioni, viene creato un progetto di traduzione o viene aggiornato un progetto di traduzione esistente per le nuove risorse. Il flusso di lavoro Aggiorna copie per lingua include le seguenti opzioni:

* Crea un nuovo progetto di traduzione
* Aggiungi al progetto di conversione corrente

### Aggiungi al progetto di conversione corrente {#add-to-existing-translation-project-1}

Se si utilizza questa opzione, il set di risorse viene aggiunto a un progetto di traduzione esistente per aggiornare la copia per lingua scelta.

1. Dall’interfaccia utente di Assets, seleziona la cartella di origine in cui hai aggiunto una cartella di risorse.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e seleziona **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare l&#39;elenco delle copie per lingua.
1. Per selezionare tutte le copie della lingua, seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**. Deseleziona le altre copie, ad eccezione della copia (o copie) per la lingua (o lingue) verso cui vuoi tradurre.
1. Seleziona **[!UICONTROL Aggiorna copie per lingua]** in basso.
1. Dall&#39;elenco **[!UICONTROL Progetto]** scegliere **[!UICONTROL Aggiungi al progetto di traduzione esistente]**.
1. Dall&#39;elenco **[!UICONTROL Progetto di traduzione esistente]**, seleziona un progetto per aggiungere la risorsa per la traduzione.
1. Seleziona **[!UICONTROL Inizia]**.
1. Vedere i passaggi 9-14 di [Aggiungi al progetto di traduzione esistente](#add-to-existing-translation-project) per completare il resto della procedura.

### Creare copie per lingua temporanee {#creating-temporary-language-copies}

Quando esegui un flusso di lavoro di traduzione per aggiornare una copia per lingua con le versioni modificate delle risorse originali, la copia per lingua esistente viene mantenuta finché non approvi le risorse tradotte. [!DNL Assets] archivia le risorse appena tradotte in una posizione temporanea e aggiorna la copia per lingua esistente dopo l&#39;approvazione esplicita delle risorse. Se rifiuti le risorse, la copia per lingua rimane invariata.

1. Seleziona la cartella principale di origine in **[!UICONTROL Copie per lingua]** per la quale hai già creato una copia per lingua, quindi seleziona **[!UICONTROL Mostra in Assets]** per aprire la cartella in [!DNL Assets].
1. Dall&#39;interfaccia utente di Assets, seleziona una risorsa già tradotta e fai clic sull&#39;icona **[!UICONTROL Modifica]** nella barra degli strumenti per aprire la risorsa in modalità di modifica.
1. Modifica la risorsa, quindi salva le modifiche.
1. Eseguire i passaggi da 2 a 14 della procedura [Aggiungi al progetto di traduzione esistente](#add-to-existing-translation-project) per aggiornare la copia per lingua.
1. Seleziona i puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**. Dall&#39;elenco delle risorse nella pagina **[!UICONTROL Processo di traduzione]**, puoi visualizzare chiaramente il percorso temporaneo in cui è memorizzata la versione tradotta della risorsa.
1. Seleziona la casella di controllo accanto a **[!UICONTROL Titolo]**.
1. Dalla barra degli strumenti, seleziona **[!UICONTROL Accetta traduzione]**, quindi seleziona **[!UICONTROL Accetta]** nella finestra di dialogo per sovrascrivere la risorsa tradotta nella cartella di destinazione con la versione tradotta della risorsa modificata.

   >[!NOTE]
   >
   >Per abilitare il flusso di lavoro di traduzione per aggiornare le risorse di destinazione, accetta sia la risorsa che i metadati.

   Selezionare **[!UICONTROL Rifiuta traduzione]** per mantenere la versione tradotta in origine della risorsa nella directory principale delle impostazioni locali di destinazione e rifiutare la versione modificata.

1. Passa alla console Assets e apri la pagina Proprietà di ciascuna delle risorse tradotte per visualizzare i metadati tradotti.

<!-- TBD: Possibly this blog was not migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## Creare progetti di traduzione {#creating-translation-projects}

Per creare una copia per lingua, attiva uno dei seguenti flussi di lavoro per la copia della lingua disponibili nella barra Riferimenti dell’interfaccia utente di Assets:

**Crea e traduci**

In questo flusso di lavoro, le risorse da tradurre vengono copiate nella directory principale della lingua nella quale desideri tradurre. Inoltre, a seconda delle opzioni scelte, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato.

**Aggiorna copie per lingua**

Esegui questo flusso di lavoro per tradurre un gruppo aggiuntivo di risorse e includerlo in una copia per lingua specifica. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già le risorse tradotte in precedenza.

>[!NOTE]
>
>I file binari delle risorse vengono tradotti solo se il fornitore di servizi di traduzione supporta la traduzione dei file binari.

>[!NOTE]
>
>Se avvii un flusso di lavoro di traduzione per risorse complesse, come file PDF e file Adobe InDesign, le relative risorse secondarie o rappresentazioni (se presenti) non vengono inviate per la traduzione.

### Creare e tradurre il flusso di lavoro {#create-and-translate-workflow}

Puoi utilizzare il flusso di lavoro Crea e traduci per generare per la prima volta copie per una determinata lingua. Il flusso di lavoro fornisce le seguenti opzioni:

* Crea solo struttura
* Crea un nuovo progetto di traduzione
* Aggiungi al progetto di conversione corrente

### Crea solo struttura {#create-structure-only}

Utilizza l’opzione **Crea solo struttura** per creare una gerarchia di cartelle di destinazione all’interno della directory principale lingua di destinazione, in modo che corrisponda alla gerarchia della cartella di origine all’interno della directory principale lingua di origine. In questo caso, le risorse di origine vengono copiate nella cartella di destinazione. Tuttavia, non viene generato alcun progetto di traduzione.

1. Nell’interfaccia utente di Assets, seleziona la cartella di origine per la quale desideri creare una struttura nella directory principale della lingua di destinazione.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e seleziona **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**.
1. Seleziona **[!UICONTROL Crea e traduci]** in basso.
1. Dall&#39;elenco **[!UICONTROL Lingue di destinazione]**, selezionare la lingua per la quale si desidera creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea solo struttura]**.
1. Seleziona **[!UICONTROL Crea]**. La nuova struttura per la lingua di destinazione è elencata in **[!UICONTROL Copie per lingua]**.
1. Selezionare la struttura dall&#39;elenco, quindi selezionare **[!UICONTROL Mostra in Assets]** per passare alla struttura di cartelle nella lingua di destinazione.

## Applicare i servizi cloud di traduzione alle cartelle {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager consente di avvalersi di servizi di traduzione basati su cloud dal provider di traduzione scelto per garantire che le risorse vengano tradotte in base alle tue esigenze.

Puoi applicare il servizio cloud di traduzione direttamente alla cartella delle risorse, in modo che possa essere utilizzato durante i flussi di lavoro di traduzione.

### Applicare i servizi di traduzione {#applying-the-translation-services}

L’applicazione dei servizi cloud di traduzione direttamente nella cartella delle risorse elimina la necessità di configurare i servizi di traduzione quando crei o aggiorni i flussi di lavoro di traduzione.

1. Dall’interfaccia utente di Assets, seleziona la cartella a cui desideri applicare i servizi di traduzione.
1. Dalla barra degli strumenti, seleziona l&#39;icona **[!UICONTROL Proprietà]** per visualizzare la pagina **[!UICONTROL Proprietà cartella]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vai alla scheda **[!UICONTROL Cloud Services]**.
1. Dall’elenco Configurazioni Cloud Service, scegli il provider di traduzione desiderato. Se ad esempio si desidera utilizzare i servizi di traduzione di Microsoft, scegliere **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Scegli il connettore per il provider di traduzione.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Dalla barra degli strumenti, seleziona **[!UICONTROL Salva]**, quindi fai clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Il servizio di traduzione viene applicato alla cartella.

### Applica connettore di traduzione personalizzato {#applying-custom-translation-connector}

Se vuoi applicare un connettore personalizzato per i servizi di traduzione che desideri utilizzare nei flussi di lavoro di traduzione, attieniti alla seguente procedura. Per applicare un connettore personalizzato, installarlo da [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md). Quindi, configura il connettore dalla console Cloud Services. Dopo aver configurato il connettore, questo è disponibile nell’elenco dei connettori nella scheda Cloud Services descritta in [Applicazione dei servizi di traduzione](#applying-the-translation-services). Dopo aver applicato il connettore personalizzato e aver eseguito i flussi di lavoro di traduzione, nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione vengono visualizzati i dettagli del connettore, rispettivamente sotto le head **[!UICONTROL Provider]** e **[!UICONTROL Metodo]**.

1. Installa il connettore da [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).
1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti > Distribuzione > Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, individua il connettore installato in **[!UICONTROL Servizi di terze parti]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Seleziona il collegamento **[!UICONTROL Configura ora]** per aprire la finestra di dialogo **[!UICONTROL Crea configurazione]**.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specificare un titolo e un nome per il connettore, quindi selezionare **[!UICONTROL Crea]**. Il connettore personalizzato è disponibile nell’elenco dei connettori nella scheda **[!UICONTROL Cloud Services]** descritta nel passaggio 5 di [Applicazione dei servizi di traduzione](#applying-the-translation-services).
1. Dopo aver applicato il connettore personalizzato, esegui uno dei flussi di lavoro di traduzione descritti in creazione di progetti di traduzione. Puoi verificare i dettagli del connettore nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione della console **[!UICONTROL Progetti]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)

**Consulta anche**

* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
