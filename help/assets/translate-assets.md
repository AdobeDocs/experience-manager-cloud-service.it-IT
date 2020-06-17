---
title: Creazione e gestione di risorse digitali in più lingue ed esecuzione di flussi di lavoro di traduzione
description: Scoprite come automatizzare i flussi di lavoro per la traduzione di risorse, inclusi file binari, metadati e tag in più lingue.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '2612'
ht-degree: 24%

---


# Risorse in più lingue {#multilingual-assets}

Per risorse in più lingue si intendono risorse con file binari, metadati e tag in più lingue. In genere, i file binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue. Risorse  Adobe Experience Manager (AEM) consente di automatizzare i flussi di lavoro di traduzione delle risorse (inclusi file binari, metadati e tag) per generare risorse in altre lingue da usare in progetti multilingue.

Per automatizzare i flussi di lavoro di traduzione, integrate i fornitori di servizi di traduzione con AEM e create progetti per la traduzione delle risorse in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

Traduzione umana: Le risorse convertite vengono restituite e importate in AEM. Quando il fornitore di traduzione è integrato con AEM, le risorse vengono inviate automaticamente da AEM al fornitore di traduzione.

Traduzione automatica: Il servizio di traduzione automatica traduce immediatamente i metadati e i tag delle risorse.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/translation-projects.html
https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://docs.adobe.com/content/help/en/experience-manager-65/administering/introduction/tc-prep.html

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

Per risorse in più lingue si intendono risorse con file binari, metadati e tag in più lingue. In genere, i file binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In Risorse  Adobe Experience Manager (AEM), le risorse in più lingue sono incluse nelle cartelle, dove ciascuna cartella contiene le risorse in un’altra lingua.

Ogni cartella lingua è denominata copia per lingua. La cartella principale di una copia della lingua, nota come radice della lingua, identifica la lingua del contenuto nella copia della lingua. Ad esempio, `/content/dam/it` è la radice della lingua italiana per la copia in lingua italiana. Le copie della lingua devono utilizzare una radice [della lingua configurata](#create-a-language-root) correttamente, in modo che venga utilizzata la lingua corretta quando vengono eseguite le traduzioni delle risorse di origine.

La copia per la lingua per la quale avete aggiunto originariamente le risorse è la lingua principale. La lingua primaria è l&#39;origine tradotta in altre lingue. Una gerarchia di cartelle di esempio include diverse origini di lingua:

```shell
/content
&nbsp; &nbsp; /- dam
&nbsp; &nbsp; &nbsp; |- en
&nbsp; &nbsp; &nbsp; |- fr
&nbsp; &nbsp; &nbsp; |- de
&nbsp; &nbsp; &nbsp; |- es
&nbsp; &nbsp; &nbsp; |- it
&nbsp; &nbsp; &nbsp; |- ja
&nbsp; &nbsp; &nbsp; |- zh
```

Per preparare le risorse alla conversione, effettuate le seguenti operazioni:

1. Creare la radice della lingua della lingua principale. Ad esempio, la radice della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Verificare che la radice della lingua sia configurata correttamente in base alle informazioni contenute in [Creare una radice](#create-a-language-root)della lingua.

1. Aggiungere risorse alla lingua principale.
1. Create la radice della lingua di ciascuna lingua di destinazione per la quale è necessaria una copia della lingua.

### Creare una directory principale della lingua {#create-a-language-root}

Per creare la directory principale della lingua, create una cartella e utilizzate un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la lingua principale, è possibile creare una copia della lingua a qualsiasi livello all&#39;interno della lingua principale.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia di esempi ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nella directory archivio e pertanto determina il percorso delle risorse. (*&lt;server>:&lt;porta>/assets.html/content/dam/it/*)

1. Dalla console Assets, tocca o fai clic su **[!UICONTROL Crea]** e scegli dal menu la voce **[!UICONTROL Cartella]**.
1. Nel campo Nome digitare il codice del paese nel formato di `<language-code>`.
1. Tocca o fai clic su **[!UICONTROL Crea]**. L’elemento principale della lingua viene creato nella console Risorse.

### Visualizzare le origini della lingua {#view-language-roots}

L’interfaccia touch fornisce un pannello Riferimenti che mostra un elenco delle origini delle lingue create all’interno dei AEM Assets.

1. Nella console Risorse, selezionate la lingua principale per la quale desiderate creare delle copie in lingua.
1. Tocca o fai clic sull’icona GlobalNav, quindi scegli **[!UICONTROL Riferimenti]** per aprire il riquadro Riferimento.
1. Nel riquadro Riferimenti, fare clic o toccare Copie **[!UICONTROL lingua]**. Il pannello Copie lingua mostra le copie in lingua delle risorse.

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project}

Se utilizzate questa opzione, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desiderate tradurre. A seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o eseguito automaticamente non appena viene creato il progetto di traduzione.

1. Nell’interfaccia utente Risorse, seleziona la cartella di origine per la quale vuoi creare una copia per la lingua.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e tocca o fai clic su **[!UICONTROL Copie per lingua]** sotto **[!UICONTROL Copie]**.
1. Tocca o fai clic su **[!UICONTROL Crea e traslina]** in basso.
1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]** , selezionate **[!UICONTROL Crea un nuovo progetto]** di traduzione.
1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.
1. Click/tap on **[!UICONTROL Create]**. Le risorse della cartella di origine vengono copiate nelle cartelle di destinazione per le impostazioni internazionali selezionate al punto 4.
1. Per passare alla cartella, selezionate la copia della lingua e fate clic su **[!UICONTROL Mostra nelle risorse]**.
1. Passate alla console Progetti. La cartella di traduzione viene copiata nella console Progetti.
1. Aprite la cartella per visualizzare il progetto di traduzione.
1. Tocca o fai clic sul progetto per aprire la pagina dei dettagli.
1. Per visualizzare lo stato del processo di traduzione, fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Nell’interfaccia utente Risorse, aprite la pagina Proprietà per ciascuna risorsa convertita per visualizzare i metadati convertiti.

>[!NOTE]
>
>Questa funzione è disponibile sia per le risorse che per le cartelle. Quando una risorsa viene selezionata al posto di una cartella, viene copiata l’intera gerarchia di cartelle fino alla directory principale della lingua per creare una copia della lingua per la risorsa.

### Add to an existing translation project {#add-to-existing-translation-project}

Se utilizzate questa opzione, il flusso di lavoro di traduzione viene eseguito per le risorse aggiunte alla cartella di origine dopo aver eseguito un flusso di lavoro di traduzione precedente. Solo le risorse appena aggiunte vengono copiate nella cartella di destinazione che contiene le risorse tradotte in precedenza. In questo caso non viene creato alcun nuovo progetto di traduzione.

1. Nell’interfaccia utente Risorse, passa alla cartella di origine contenente le risorse non tradotte.
1. Seleziona una risorsa da tradurre e apri il **[!UICONTROL riquadro Riferimento]**. Nella sezione **[!UICONTROL Copie per lingua]** viene visualizzato il numero di copie di traduzione attualmente disponibili.
1. Nella sezione **[!UICONTROL Copie per lingua]**, tocca o fai clic su **[!UICONTROL Copie]**. Viene visualizzato un elenco delle copie di traduzione disponibili.
1. Tocca o fai clic su **[!UICONTROL Crea e traslina]** in basso.
1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.
1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Aggiungi al progetto di traduzione esistente]** per eseguire il flusso di lavoro di traduzione nella cartella.
   >[!NOTE]
   >
   >Se scegliete l’opzione **[!UICONTROL Aggiungi al progetto]** di traduzione esistente, il progetto di traduzione viene aggiunto a un progetto preesistente solo se le impostazioni del progetto corrispondono esattamente alle impostazioni del progetto preesistente. In caso contrario, viene creato un nuovo progetto.
1. Dall’elenco Progetto **[!UICONTROL di traduzione]** esistente, selezionate un progetto per aggiungere la risorsa per la traduzione.
1. Tocca o fai clic su **[!UICONTROL Crea]**. Le risorse da tradurre vengono aggiunte alla cartella di destinazione. La cartella aggiornata è elencata nella sezione **[!UICONTROL Copie per lingua]**.
1. Passate alla console Progetti e aprite il progetto di traduzione esistente a cui avete aggiunto.
1. Tocca o fai clic sulla pagina dei dettagli del progetto di traduzione.
1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

   >[!NOTE]
   >
   >* Se eliminate la voce relativa a tag o metadati, non vengono convertiti tag o metadati per nessuna risorsa.
   >* Se utilizzate Traduzione automatica, i file binari delle risorse non vengono tradotti.
   >* Se la risorsa aggiunta al processo di conversione include risorse secondarie, selezionate le risorse secondarie e rimuoverle affinché la conversione possa proseguire senza problemi.


1. Per avviare la conversione delle risorse, toccate o fate clic sulla freccia nella sezione Processo **[!UICONTROL di]** traduzione e selezionate **[!UICONTROL Avvia]** dall’elenco. Un messaggio notifica l’inizio del processo di traduzione.
1. Per visualizzare lo stato del processo di traduzione, toccate o fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Al termine della traduzione, lo stato diventa Pronto per la revisione. Andate all’interfaccia utente delle risorse e aprite la pagina Proprietà per ciascuna risorsa convertita per visualizzare i metadati tradotti.

### Aggiorna copie per lingua {#update-language-copies}

Eseguite questo flusso di lavoro per tradurre qualsiasi altro set di risorse e includerlo in una copia della lingua per una lingua specifica. In questo caso, le risorse convertite vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza. A seconda della scelta delle opzioni, viene creato un progetto di traduzione o viene aggiornato un progetto di traduzione esistente per le nuove risorse. Il flusso di lavoro Copia lingua aggiornamento include le seguenti opzioni:

* Crea un nuovo progetto di traduzione
* Aggiungi a progetto di traduzione esistente

### Aggiungi a progetto di traduzione esistente {#add-to-existing-translation-project-1}

Se utilizzate questa opzione, il set di risorse viene aggiunto a un progetto di traduzione esistente per aggiornare la copia della lingua per le impostazioni internazionali scelte.

1. Dall’interfaccia utente Risorse, selezionate la cartella di origine in cui avete aggiunto una cartella di risorse.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e, per visualizzare l’elenco delle copie per lingua, in **[!UICONTROL Copie]**, tocca o fai clic su **[!UICONTROL Copie per lingua]**.
1. Per selezionare tutte le copie della lingua, seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**. Deseleziona le altre copie, ad eccezione della copia (o copie) per lingua corrispondente alle impostazioni internazionali verso cui vuoi tradurre.
1. Tocca o fai clic su **[!UICONTROL Aggiorna copie]** della lingua in basso.
1. Dall’elenco **[!UICONTROL Progetto]** , scegliete **[!UICONTROL Aggiungi al progetto]** di traduzione esistente.
1. Dall’elenco Progetto **[!UICONTROL di traduzione]** esistente, selezionate un progetto per aggiungere la risorsa per la traduzione.
1. Tocca o fai clic su **[!UICONTROL Avvia]**.
1. Per completare il resto della procedura, consulta i passaggi da 9 a 14 di [Aggiungi al progetto](#add-to-existing-translation-project) di traduzione esistente.

### Creare copie in lingua temporanea {#creating-temporary-language-copies}

Quando eseguite un flusso di lavoro di traduzione per aggiornare una copia per lingua con versioni modificate di risorse originali, la copia per lingua esistente viene mantenuta fino all’approvazione delle risorse tradotte. AEM Assets memorizza le risorse appena tradotte in una posizione temporanea e aggiorna la copia della lingua esistente dopo l’approvazione esplicita delle risorse. Se rifiutate le risorse, la copia nella lingua rimane invariata.

1. Tocca o fai clic sulla cartella principale di origine di **[!UICONTROL Copie per lingua]** per la quale hai già creato una copia per lingua, quindi tocca o fai clic su **[!UICONTROL Mostra in Assets]** per aprire la cartella in AEM Assets.
1. Nell’interfaccia utente delle risorse, seleziona una risorsa già tradotta e tocca o fai clic sull’icona **[!UICONTROL Modifica]** nella barra degli strumenti per aprire la risorsa in modalità di modifica.
1. Modificate la risorsa e salvate le modifiche.
1. Per aggiornare la copia della lingua, eseguite i passaggi da 2 a 14 della procedura [Aggiungi al progetto](#add-to-existing-translation-project) di traduzione esistente.
1. Toccate o fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione. Dall’elenco delle risorse nella pagina Processo **[!UICONTROL di]** traduzione, potete visualizzare chiaramente la posizione temporanea in cui è memorizzata la versione convertita della risorsa.
1. Selezionate la casella di controllo accanto a **[!UICONTROL Titolo]**.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Accetta traduzione]**, quindi tocca o fai clic su **[!UICONTROL Accetta]** nella finestra di dialogo, così da sovrascrivere la risorsa tradotta nella cartella di destinazione con la versione tradotta della risorsa modificata.

   >[!NOTE]
   >
   >Per abilitare il flusso di lavoro di traduzione per aggiornare le risorse di destinazione, accettate sia la risorsa che i metadati.

   Tocca o fai clic su **[!UICONTROL Rifiuta traduzione]** per mantenere la versione tradotta originariamente nella directory principale delle impostazioni internazionali di destinazione e rifiutare la versione modificata.

1. Passate alla console Risorse e aprite la pagina Proprietà per ciascuna risorsa convertita per visualizzare i metadati tradotti.

Per suggerimenti su come tradurre i metadati per le risorse in modo efficiente, consultate [5 Passaggi per tradurre i metadati](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)in modo efficiente.

## Creazione di progetti di traduzione {#creating-translation-projects}

Per creare una copia per lingua, attiva uno dei seguenti flussi di lavoro di copia per lingua disponibili nella barra laterale Riferimenti nell’interfaccia utente Risorse:

**Creare e tradurre**

In questo flusso di lavoro, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desiderate tradurre. Inoltre, a seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato il progetto di traduzione.

**Aggiorna copie per lingua**

Potete eseguire questo flusso di lavoro per tradurre un ulteriore gruppo di risorse e includerlo in una copia per lingua per una lingua specifica. In questo caso, le risorse convertite vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza.

>[!NOTE]
>
>I file binari di risorse vengono tradotti solo se il provider di servizi di traduzione supporta la traduzione dei file binari.

>[!NOTE]
>
>Se avviate un flusso di lavoro di traduzione per risorse complesse, come file PDF e file Adobe InDesign, le relative risorse secondarie o rappresentazioni (se presenti) non vengono inviate per la traduzione.

### Crea e traduci flusso di lavoro {#create-and-translate-workflow}

È possibile utilizzare il flusso di lavoro di creazione e traduzione per generare per la prima volta copie della lingua per una lingua particolare. Il flusso di lavoro offre le seguenti opzioni:

* Crea solo struttura
* Crea un nuovo progetto di traduzione
* Aggiungi a progetto di traduzione esistente

### Crea solo struttura {#create-structure-only}

Utilizza l’opzione **Crea solo struttura** per creare una gerarchia di cartelle di destinazione all’interno della directory principale lingua di destinazione, in modo che corrisponda alla gerarchia della cartella di origine all’interno della directory principale lingua di origine. In questo caso, le risorse di origine vengono copiate nella cartella di destinazione. Tuttavia, non viene generato alcun progetto di traduzione.

1. Nell’interfaccia utente Risorse, seleziona la cartella di origine per la quale vuoi creare una struttura nella directory principale della lingua di destinazione.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e tocca o fai clic su **[!UICONTROL Copie per lingua]** sotto **[!UICONTROL Copie]**.
1. Tocca o fai clic su **[!UICONTROL Crea e traslina]** in basso.
1. From the **[!UICONTROL Target Languages]** list, select the language for which you want to create a folder structure.
1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea solo struttura]**.
1. Tocca o fai clic su **[!UICONTROL Crea]**. La nuova struttura per la lingua di destinazione è elencata in Copie **[!UICONTROL lingua]**.
1. Tocca o fai clic sulla struttura dall’elenco, quindi tocca o fai clic su **[!UICONTROL Mostra in risorse]** per passare alla struttura di cartelle nella lingua di destinazione.

## Applicazione dei servizi di traduzione cloud alle cartelle {#applying-translation-cloud-services-to-folders}

 Adobe Experience Manager (AEM) consente di usufruire di servizi di traduzione basati sul cloud da parte del provider di traduzione di vostra scelta per garantire che le risorse vengano tradotte in base alle vostre esigenze.

Potete applicare il servizio di traduzione cloud direttamente alla cartella delle risorse in modo che possa essere utilizzato durante i flussi di lavoro di traduzione.

### Applicare i servizi di traduzione {#applying-the-translation-services}

L’applicazione dei servizi di traduzione cloud direttamente nella cartella delle risorse elimina la necessità di configurare i servizi di traduzione al momento della creazione o dell’aggiornamento dei flussi di lavoro di traduzione.

1. Dall’interfaccia utente di Risorse, selezionate la cartella a cui desiderate applicare i servizi di traduzione.
1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Proprietà]** per visualizzare la pagina **[!UICONTROL Proprietà cartella]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vai alla scheda **[!UICONTROL Cloud Services]**.
1. Dall’elenco Configurazioni Cloud Service, scegliete il provider di traduzione desiderato. Ad esempio, se desiderate utilizzare i servizi di traduzione di Microsoft, scegliete **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Scegliere il connettore per il provider di traduzione.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Dalla barra degli strumenti, fai clic o tocca **[!UICONTROL Salva]**, quindi fai clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo: il servizio di traduzione viene applicato alla cartella.

### Applica connettore conversione personalizzato {#applying-custom-translation-connector}

Se vuoi applicare un connettore personalizzato per i servizi di traduzione che desideri utilizzare nei flussi di lavoro di traduzione, attieniti alla seguente procedura. Per applicare un connettore personalizzato, procedi prima con l’installazione del connettore da Gestione pacchetti. Quindi, configura il connettore dalla console Cloud Services. Dopo aver configurato il connettore, questo è disponibile nell’elenco dei connettori nella scheda Cloud Services descritta in [Applicazione dei servizi di traduzione](#applying-the-translation-services). Dopo aver applicato il connettore personalizzato e aver eseguito i flussi di lavoro di traduzione, nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione vengono visualizzati i dettagli del connettore, rispettivamente sotto le head **[!UICONTROL Provider]** e **[!UICONTROL Metodo]**.

1. Installare il connettore da Package Manager.
1. Tocca o fai clic sul logo AEM, quindi passa a **[!UICONTROL Strumenti > Distribuzione > Servizi]** cloud.
1. Nella pagina **[!UICONTROL Cloud Services]**, individua il connettore installato in **[!UICONTROL Servizi di terze parti]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Tocca o fai clic sul collegamento **[!UICONTROL Configura ora]** per aprire la finestra di dialogo **[!UICONTROL Crea configurazione]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specifica un titolo e un nome per il connettore, quindi fai clic o tocca **[!UICONTROL Crea]**. Il connettore personalizzato è disponibile nell’elenco dei connettori nella scheda **[!UICONTROL Cloud Services]** descritta nel passaggio 5 di [Applicazione dei servizi di traduzione](#applying-the-translation-services).
1. Dopo aver applicato il connettore personalizzato, esegui uno dei flussi di lavoro di traduzione descritti in creazione di progetti di traduzione. Puoi verificare i dettagli del connettore nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione della console **[!UICONTROL Progetti]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
