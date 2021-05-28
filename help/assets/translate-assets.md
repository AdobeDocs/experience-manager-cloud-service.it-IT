---
title: Creare e gestire risorse digitali in più lingue
description: Scopri come automatizzare i flussi di lavoro per la traduzione di risorse, inclusi binari, metadati e tag in più lingue.
contentOwner: AG
feature: Gestione risorse, traduzione
role: Administrator,Business Practitioner
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 24%

---

# Risorse multilingue {#multilingual-assets}

Per risorse multilingue si intendono le risorse con file binari, metadati e tag in più lingue. In genere, i binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue. Risorse Adobe Experience Manager (AEM) consente di automatizzare i flussi di lavoro di traduzione sulle risorse (inclusi binari, metadati e tag) per generare risorse in altre lingue da utilizzare nei progetti multilingue.

Per automatizzare i flussi di lavoro di traduzione, è possibile integrare fornitori di servizi di traduzione con AEM e creare progetti per la traduzione delle risorse in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

Traduzione umana: Le risorse tradotte vengono restituite e importate in AEM. Quando il provider di traduzione è integrato con AEM, le risorse vengono inviate automaticamente tra AEM e il provider di traduzione.

Traduzione automatica: Il servizio di traduzione automatica traduce immediatamente i metadati e i tag delle risorse.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting AEM with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with AEM, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## Preparare le risorse per la traduzione {#prepare-assets-for-translation}

Per risorse multilingue si intendono le risorse con file binari, metadati e tag in più lingue. In genere, i binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In Risorse Adobe Experience Manager (AEM), le risorse multilingue sono incluse nelle cartelle, in cui ogni cartella contiene le risorse in una lingua diversa.

Ogni cartella della lingua è denominata copia della lingua. La cartella principale di una copia per lingua, nota come radice lingua, identifica la lingua del contenuto nella copia per lingua. Ad esempio, `/content/dam/it` è la directory principale della lingua italiana per la copia in lingua italiana. Le copie in lingua devono utilizzare una [directory principale della lingua configurata correttamente](#create-a-language-root) in modo che la lingua corretta venga utilizzata durante l&#39;esecuzione delle traduzioni delle risorse di origine.

La copia per lingua per la quale hai originariamente aggiunto le risorse è la lingua principale. Il linguaggio primario è la fonte tradotta in altre lingue. Una gerarchia di cartelle di esempio include diverse directory principali della lingua:

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

Esegui i seguenti passaggi per preparare le risorse per la traduzione:

1. Creare la directory principale lingua della lingua primaria. Ad esempio, la directory principale della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Assicurati che la directory principale della lingua sia configurata correttamente in base alle informazioni in [Crea una directory principale della lingua](#create-a-language-root).

1. Aggiungi le risorse alla tua lingua primaria.
1. Crea la directory principale della lingua di ogni lingua di destinazione per la quale è necessaria una copia della lingua.

### Creare una directory principale della lingua {#create-a-language-root}

Per creare la directory principale della lingua, creare una cartella e utilizzare un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la directory principale lingua, è possibile creare una copia della lingua a qualsiasi livello all’interno della directory principale lingua.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia di esempio ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nell’archivio e quindi determina il percorso delle risorse. (*&lt;server>:&lt;port>/assets.html/content/dam/it/*)

1. Dalla console Assets, tocca o fai clic su **[!UICONTROL Crea]** e scegli dal menu la voce **[!UICONTROL Cartella]**.
1. Nel campo Nome digitare il codice del paese nel formato `<language-code>`.
1. Tocca o fai clic su **[!UICONTROL Crea]**. La directory principale della lingua viene creata nella console Risorse.

### Visualizza le radici della lingua {#view-language-roots}

L’interfaccia touch fornisce un pannello Riferimenti che mostra un elenco delle radici della lingua create in AEM Assets.

1. Nella console Assets, seleziona la lingua principale per la quale vuoi creare delle copie per lingua.
1. Tocca o fai clic sull&#39;icona di navigazione globale e scegli **[!UICONTROL Riferimenti]** per aprire il riquadro Riferimento.
1. Nel riquadro Riferimenti, tocca o fai clic su **[!UICONTROL Copie per lingua]**. Il pannello Copie per lingua mostra le copie in lingua delle risorse.

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project}

Se utilizzi questa opzione, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. A seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti . A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o viene eseguito automaticamente non appena viene creato il progetto di traduzione.

1. Nell’interfaccia utente Assets, seleziona la cartella di origine per la quale vuoi creare una copia in lingua.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e tocca o fai clic su **[!UICONTROL Copie per lingua]** sotto **[!UICONTROL Copie]**.
1. Tocca o fai clic su **[!UICONTROL Crea e traduci]** in basso.
1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Crea un nuovo progetto di traduzione]**.
1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.
1. Tocca o fai clic su **[!UICONTROL Crea]**. Le risorse della cartella di origine vengono copiate nelle cartelle di destinazione per le impostazioni internazionali selezionate al passaggio 4.
1. Per passare alla cartella, seleziona la copia per lingua e fai clic su **[!UICONTROL Mostra in Assets]**.
1. Passa alla console Progetti . La cartella di traduzione viene copiata nella console Progetti .
1. Apri la cartella per visualizzare il progetto di traduzione.
1. Tocca o fai clic sul progetto per aprire la pagina dei dettagli.
1. Per visualizzare lo stato del lavoro di traduzione, fai clic sull&#39;ellissi nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** . <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Nell’interfaccia utente Assets, apri la pagina Proprietà per ciascuna risorsa tradotta per visualizzare i metadati tradotti.

>[!NOTE]
>
>Questa funzione è disponibile sia per le risorse che per le cartelle. Quando una risorsa viene selezionata al posto di una cartella, l’intera gerarchia di cartelle fino alla directory principale lingua viene copiata per creare una copia per la lingua della risorsa.

### Aggiungi a un progetto di traduzione esistente {#add-to-existing-translation-project}

Se utilizzi questa opzione, il flusso di lavoro di traduzione viene eseguito per le risorse aggiunte alla cartella di origine dopo aver eseguito un flusso di lavoro di traduzione precedente. Solo le risorse appena aggiunte vengono copiate nella cartella di destinazione che contiene le risorse tradotte in precedenza. In questo caso non viene creato alcun nuovo progetto di traduzione.

1. Nell’interfaccia utente Assets, passa alla cartella di origine contenente le risorse non tradotte.
1. Seleziona una risorsa da tradurre e apri il **[!UICONTROL riquadro Riferimento]**. Nella sezione **[!UICONTROL Copie per lingua]** viene visualizzato il numero di copie di traduzione attualmente disponibili.
1. Nella sezione **[!UICONTROL Copie per lingua]**, tocca o fai clic su **[!UICONTROL Copie]**. Viene visualizzato un elenco delle copie di traduzione disponibili.
1. Tocca o fai clic su **[!UICONTROL Crea e traduci]** in basso.
1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Aggiungi al progetto di traduzione esistente]** per eseguire il flusso di lavoro di traduzione nella cartella.
   >[!NOTE]
   >
   >Se scegli l’opzione **[!UICONTROL Aggiungi al progetto di traduzione esistente]**, il progetto di traduzione viene aggiunto a un progetto preesistente solo se le impostazioni del progetto corrispondono esattamente alle impostazioni del progetto preesistente. In caso contrario, viene creato un nuovo progetto.
1. Dall’elenco **[!UICONTROL Progetto di traduzione esistente]** , seleziona un progetto per aggiungere la risorsa da tradurre.
1. Tocca o fai clic su **[!UICONTROL Crea]**. Le risorse da tradurre vengono aggiunte alla cartella di destinazione. La cartella aggiornata è elencata nella sezione **[!UICONTROL Copie per lingua]**.
1. Passa alla console Progetti e apri il progetto di traduzione esistente a cui hai aggiunto.
1. Tocca o fai clic sulla pagina dei dettagli del progetto di traduzione.
1. Tocca o fai clic sui puntini di sospensione nella parte inferiore della sezione **Processo di traduzione** per visualizzare le risorse nel flusso di lavoro di traduzione. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

   >[!NOTE]
   >
   >* Se elimini la voce per tag o metadati, non vengono tradotti tag o metadati per nessuna delle risorse.
   >* Se utilizzi la traduzione automatica, i file binari delle risorse non vengono tradotti.
   >* Se la risorsa aggiunta al processo di traduzione include le risorse secondarie, selezionale e rimuoverle affinché la traduzione prosegua senza problemi.


1. Per avviare la traduzione delle risorse, tocca o fai clic sulla freccia nella sezione **[!UICONTROL Processo di traduzione]** e seleziona **[!UICONTROL Avvia]** dall’elenco. Un messaggio notifica l’inizio del processo di traduzione.
1. Per visualizzare lo stato del lavoro di traduzione, tocca o fai clic sui puntini di sospensione nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** . <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Al termine della traduzione, lo stato diventa Pronto per la revisione. Passa all’interfaccia utente Assets e apri la pagina Proprietà per ciascuna risorsa tradotta per visualizzare i metadati tradotti.

### Aggiorna copie per lingua {#update-language-copies}

Esegui questo flusso di lavoro per tradurre qualsiasi set aggiuntivo di risorse e includerlo in una copia per lingua per una particolare impostazione internazionale. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza. A seconda della scelta delle opzioni, viene creato un progetto di traduzione o viene aggiornato un progetto di traduzione esistente per le nuove risorse. Il flusso di lavoro per la copia in lingua di aggiornamento include le seguenti opzioni:

* Crea un nuovo progetto di traduzione
* Aggiungi a progetto di traduzione esistente

### Aggiungi a progetto di traduzione esistente {#add-to-existing-translation-project-1}

Se utilizzi questa opzione, il set di risorse viene aggiunto a un progetto di traduzione esistente per aggiornare la copia per lingua relativa alle impostazioni internazionali selezionate.

1. Dall’interfaccia utente Assets, seleziona la cartella di origine in cui hai aggiunto una cartella di risorse.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e, per visualizzare l’elenco delle copie per lingua, in **[!UICONTROL Copie]**, tocca o fai clic su **[!UICONTROL Copie per lingua]**.
1. Per selezionare tutte le copie della lingua, seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**. Deseleziona le altre copie, ad eccezione della copia (o copie) per lingua corrispondente alle impostazioni internazionali verso cui vuoi tradurre.
1. Tocca o fai clic su **[!UICONTROL Aggiorna copie della lingua]** in basso.
1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Aggiungi al progetto di traduzione esistente]**.
1. Dall’elenco **[!UICONTROL Progetto di traduzione esistente]** , seleziona un progetto per aggiungere la risorsa da tradurre.
1. Tocca o fai clic su **[!UICONTROL Avvia]**.
1. Per completare il resto della procedura, vedi i passaggi 9-14 di [Aggiungi al progetto di traduzione esistente](#add-to-existing-translation-project) .

### Crea copie in lingua temporanea {#creating-temporary-language-copies}

Quando esegui un flusso di lavoro di traduzione per aggiornare una copia in lingua con le versioni modificate delle risorse originali, la copia in lingua esistente viene conservata fino all’approvazione delle risorse tradotte. AEM Assets archivia le risorse appena tradotte in una posizione temporanea e aggiorna la copia in lingua esistente dopo che le risorse sono state esplicitamente approvate. Se si rifiutano le risorse, la copia in lingua rimane invariata.

1. Tocca o fai clic sulla cartella principale di origine di **[!UICONTROL Copie per lingua]** per la quale hai già creato una copia per lingua, quindi tocca o fai clic su **[!UICONTROL Mostra in Assets]** per aprire la cartella in AEM Assets.
1. Dall’interfaccia utente di Assets, seleziona una risorsa già tradotta e tocca o fai clic sull’icona **[!UICONTROL Modifica]** nella barra degli strumenti per aprire la risorsa in modalità di modifica.
1. Modifica la risorsa e salva le modifiche.
1. Esegui i passaggi 2-14 della procedura [Aggiungi al progetto di traduzione esistente](#add-to-existing-translation-project) per aggiornare la copia per lingua.
1. Tocca o fai clic sui puntini di sospensione nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** . Dall’elenco delle risorse nella pagina **[!UICONTROL Processo di traduzione]**, puoi visualizzare chiaramente la posizione temporanea in cui è memorizzata la versione tradotta della risorsa.
1. Seleziona la casella di controllo accanto a **[!UICONTROL Titolo]**.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Accetta traduzione]**, quindi tocca o fai clic su **[!UICONTROL Accetta]** nella finestra di dialogo, così da sovrascrivere la risorsa tradotta nella cartella di destinazione con la versione tradotta della risorsa modificata.

   >[!NOTE]
   >
   >Per abilitare il flusso di lavoro di traduzione per aggiornare le risorse di destinazione, accetta sia la risorsa che i metadati.

   Tocca o fai clic su **[!UICONTROL Rifiuta traduzione]** per mantenere la versione tradotta originariamente nella directory principale delle impostazioni internazionali di destinazione e rifiutare la versione modificata.

1. Passa alla console Risorse e apri la pagina Proprietà per ciascuna risorsa tradotta per visualizzare i metadati tradotti.

<!-- TBD: Possibly this blog wasn't migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## Creare progetti di traduzione {#creating-translation-projects}

Per creare una copia per lingua, attiva uno dei seguenti flussi di lavoro di copia per lingua disponibili nella barra laterale Riferimenti nell’interfaccia utente Assets:

**Creare e tradurre**

In questo flusso di lavoro, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. Inoltre, a seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti . A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato il progetto di traduzione.

**Aggiorna copie per lingua**

Puoi eseguire questo flusso di lavoro per tradurre un gruppo aggiuntivo di risorse e includerlo in una copia per lingua per una specifica impostazione internazionale. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza.

>[!NOTE]
>
>I file binari delle risorse sono tradotti solo se il fornitore di servizi di traduzione supporta la traduzione dei file binari.

>[!NOTE]
>
>Se avvii un flusso di lavoro di traduzione per risorse complesse, come file PDF e file Adobe InDesign, le relative risorse secondarie o rappresentazioni (se presenti) non vengono inviate per la traduzione.

### Creare e tradurre un flusso di lavoro {#create-and-translate-workflow}

Utilizza il flusso di lavoro Crea e traduci per generare copie per lingua per una particolare lingua per la prima volta. Il flusso di lavoro fornisce le seguenti opzioni:

* Crea solo struttura
* Crea un nuovo progetto di traduzione
* Aggiungi a progetto di traduzione esistente

### Crea solo struttura {#create-structure-only}

Utilizza l’opzione **Crea solo struttura** per creare una gerarchia di cartelle di destinazione all’interno della directory principale lingua di destinazione, in modo che corrisponda alla gerarchia della cartella di origine all’interno della directory principale lingua di origine. In questo caso, le risorse di origine vengono copiate nella cartella di destinazione. Tuttavia, non viene generato alcun progetto di traduzione.

1. Nell’interfaccia utente di Assets, seleziona la cartella di origine per la quale vuoi creare una struttura nella directory principale della lingua di destinazione.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e tocca o fai clic su **[!UICONTROL Copie per lingua]** sotto **[!UICONTROL Copie]**.
1. Tocca o fai clic su **[!UICONTROL Crea e traduci]** in basso.
1. Dall’elenco **[!UICONTROL Lingue di destinazione]**, seleziona la lingua per la quale vuoi creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea solo struttura]**.
1. Tocca o fai clic su **[!UICONTROL Crea]**. La nuova struttura per la lingua di destinazione è elencata in **[!UICONTROL Copie per lingua]**.
1. Tocca o fai clic sulla struttura dell’elenco, quindi tocca o fai clic su **[!UICONTROL Mostra in Assets]** per accedere alla struttura delle cartelle nella lingua di destinazione.

## Applica servizi cloud di traduzione alle cartelle {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager (AEM) consente di usufruire di servizi di traduzione basati su cloud dal provider di traduzione scelto per garantire che le risorse vengano tradotte in base alle tue esigenze.

Puoi applicare il servizio cloud di traduzione direttamente alla cartella delle risorse in modo che possano essere utilizzati durante i flussi di lavoro di traduzione.

### Applicare i servizi di traduzione {#applying-the-translation-services}

L’applicazione dei servizi cloud di traduzione direttamente nella cartella delle risorse elimina la necessità di configurare i servizi di traduzione quando crei o aggiorni flussi di lavoro di traduzione.

1. Dall’interfaccia utente Assets, seleziona la cartella a cui desideri applicare i servizi di traduzione.
1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Proprietà]** per visualizzare la pagina **[!UICONTROL Proprietà cartella]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vai alla scheda **[!UICONTROL Cloud Services]**.
1. Dall’elenco Configurazioni Cloud Service, scegli il provider di traduzione desiderato. Ad esempio, se desideri usufruire di servizi di traduzione da Microsoft, scegli **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Scegliere il connettore per il provider di traduzione.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Dalla barra degli strumenti, fai clic o tocca **[!UICONTROL Salva]**, quindi fai clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo: il servizio di traduzione viene applicato alla cartella.

### Applica connettore di traduzione personalizzato {#applying-custom-translation-connector}

Se vuoi applicare un connettore personalizzato per i servizi di traduzione che desideri utilizzare nei flussi di lavoro di traduzione, attieniti alla seguente procedura. Per applicare un connettore personalizzato, procedi prima con l’installazione del connettore da Gestione pacchetti. Quindi, configura il connettore dalla console Cloud Services. Dopo aver configurato il connettore, questo è disponibile nell’elenco dei connettori nella scheda Cloud Services descritta in [Applicazione dei servizi di traduzione](#applying-the-translation-services). Dopo aver applicato il connettore personalizzato e aver eseguito i flussi di lavoro di traduzione, nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione vengono visualizzati i dettagli del connettore, rispettivamente sotto le head **[!UICONTROL Provider]** e **[!UICONTROL Metodo]**.

1. Installa il connettore da Gestione pacchetti.
1. Tocca o fai clic sul logo AEM e passa a **[!UICONTROL Strumenti > Implementazione > Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, individua il connettore installato in **[!UICONTROL Servizi di terze parti]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Tocca o fai clic sul collegamento **[!UICONTROL Configura ora]** per aprire la finestra di dialogo **[!UICONTROL Crea configurazione]**.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specifica un titolo e un nome per il connettore, quindi fai clic o tocca **[!UICONTROL Crea]**. Il connettore personalizzato è disponibile nell’elenco dei connettori nella scheda **[!UICONTROL Cloud Services]** descritta nel passaggio 5 di [Applicazione dei servizi di traduzione](#applying-the-translation-services).
1. Dopo aver applicato il connettore personalizzato, esegui uno dei flussi di lavoro di traduzione descritti in creazione di progetti di traduzione. Puoi verificare i dettagli del connettore nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione della console **[!UICONTROL Progetti]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
