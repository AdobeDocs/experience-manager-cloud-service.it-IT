---
title: Assegnare tag automatici alle risorse con tag generati dall’intelligenza artificiale
description: Assegna tag alle risorse utilizzando servizi intelligenti artificialmente che applicano tag aziendali contestuali e descrittivi utilizzando il servizio  [!DNL Adobe Sensei] .
contentOwner: AG
feature: Smart Tags,Tagging
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 6%

---


# Aggiungi tag avanzati alle risorse per migliorare l’esperienza di ricerca {#smart-tag-assets-for-faster-search}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più vocabolario controllato dalla tassonomia nei metadati delle risorse. In sostanza, include un elenco di parole chiave a cui i dipendenti, i partner e i clienti utilizzano comunemente per fare riferimento e cercare le loro risorse digitali. L’assegnazione di tag alle risorse tramite un vocabolario controllato dalla tassonomia consente di identificare e recuperare facilmente le risorse nelle ricerche.

Rispetto ai vocabolari linguistici naturali, l’assegnazione di tag basati sulla tassonomia aziendale consente di allineare le risorse al business di un’azienda e garantisce che le risorse più rilevanti vengano visualizzate nelle ricerche. Ad esempio, un produttore di automobili può assegnare tag alle immagini di un&#39;automobile con nomi di modello in modo che vengano visualizzate solo le immagini pertinenti quando viene eseguita una ricerca per progettare una campagna promozionale.

In background, la funzionalità utilizza il framework artificialmente intelligente di [Adobe Sensei](https://www.adobe.com/it/sensei/experience-cloud-artificial-intelligence.html) per addestrare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e sulla tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse.

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

Puoi assegnare i tag ai seguenti tipi di risorse:

* **Immagini**: Le immagini in molti formati vengono taggate utilizzando i servizi di contenuti avanzati di Adobe Sensei. Si [crea un modello di formazione](#train-model) e quindi [si applicano tag avanzati](#tag-assets) alle immagini.
* **Risorse** video: L’assegnazione tag video è abilitata per impostazione predefinita in  [!DNL Adobe Experience Manager] come  [!DNL Cloud Service]. [I video vengono contrassegnati automaticamente ](/help/assets/smart-tags-video-assets.md) quando carichi nuovi video o rielabori quelli esistenti.
* **Risorse** basate su testo:  [!DNL Experience Manager Assets] assegna automaticamente i tag alle risorse basate su testo supportate al momento del caricamento. Ulteriori informazioni sull’ [assegnazione tag alle risorse basate su testo](#smart-tag-text-based-assets).

## Tipi di risorse supportati {#smart-tags-supported-file-formats}

I tag avanzati vengono applicati ai tipi di file supportati che generano rappresentazioni in formato JPG e PNG. La funzionalità è supportata per i seguenti tipi di risorse:

| Immagini (tipi MIME) | Risorse basate su testo (formati di file) | Risorse video (formati di file e codec) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | JSON | FLV (H264/AVC, vp6f) |
| image/pjpeg | PDF | WMV (WMV2) |
| immagine/x-portatile-anymap | PPT |  |
| immagine/x-portatile-bitmap | PPTX |  |
| immagine/x-portatile-grigio | RTF |  |
| immagine/x-portatile-pixmap | SRT |  |
| image/x-rgb | TXT |  |
| image/x-xbitmap | VTT |  |
| image/x-xpixmap | XML |  |
| image/x-icon |  |  |
| immagine/photoshop |  |  |
| immagine/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] aggiunge automaticamente i tag avanzati alle risorse basate su testo e ai video per impostazione predefinita. Per aggiungere automaticamente tag avanzati alle immagini, completa le seguenti attività.

* [ [!DNL Adobe Experience Manager] Integrare con Adobe Developer Console](#integrate-aem-with-aio).
* [Comprendere i modelli e le linee guida dei tag](#understand-tag-models-guidelines).
* [Addestra il modello](#train-model).
* [Assegna tag alle risorse](#tag-assets) digitali.
* [Gestisci i tag e le ricerche](#manage-smart-tags-and-searches).

>[!TIP]
>
>I tag avanzati sono applicabili solo ai clienti [!DNL Adobe Experience Manager Assets] . Lo strumento Tag avanzati è acquistabile come componente aggiuntivo per [!DNL Experience Manager].

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? Provide a CTA here to buy or contacts Sales team. -->

## Assegnazione di tag alle risorse basate su testo con tag avanzati {#smart-tag-text-based-assets}

Le risorse basate su testo supportate vengono contrassegnate automaticamente da [!DNL Experience Manager Assets] al momento del caricamento. È attivata per impostazione predefinita. L’efficacia dei tag avanzati non dipende dalla quantità di testo presente nella risorsa, ma dalle parole chiave o entità pertinenti presenti nel testo della risorsa. Per le risorse basate su testo, i tag avanzati sono le parole chiave che compaiono nel testo ma quelle che descrivono meglio la risorsa. Per le risorse supportate, [!DNL Experience Manager] estrae già il testo, che viene quindi indicizzato e utilizzato per cercare le risorse. Tuttavia, i tag avanzati basati su parole chiave nel testo forniscono un facet di ricerca dedicato, strutturato e con priorità più elevata, utilizzato per migliorare l’individuazione delle risorse rispetto all’indice di ricerca completa.

Per immagini e video, invece, i tag avanzati vengono derivati in base ad alcuni aspetti visivi.

## Integrare [!DNL Experience Manager] con Adobe Developer Console {#integrate-aem-with-aio}

>[!IMPORTANT]
>
>Per impostazione predefinita, le nuove distribuzioni [!DNL Experience Manager Assets] sono integrate con [!DNL Adobe Developer Console] . Consente di configurare più rapidamente la funzionalità dei tag avanzati. Nelle implementazioni precedenti, gli amministratori possono configurare manualmente [l&#39;integrazione di tag avanzati](/help/assets/smart-tags-configuration.md#aio-integration).

Puoi integrare [!DNL Adobe Experience Manager] con Tag avanzati utilizzando [!DNL Adobe Developer Console]. Utilizza questa configurazione per accedere al servizio Tag avanzati da [!DNL Experience Manager]. Per informazioni su come configurare i tag avanzati, consulta [configurare [!DNL Experience Manager] per assegnare tag alle risorse](smart-tags-configuration.md) . Nel back-end, il server [!DNL Experience Manager] autentica le credenziali del servizio con il gateway di Adobe Developer Console prima di inoltrare la richiesta al servizio Tag avanzati.

## Comprendere i modelli e le linee guida dei tag {#understand-tag-models-guidelines}

Un modello di tag è un gruppo di tag correlati associati a vari aspetti visivi delle immagini a cui viene applicato un tag. I tag si riferiscono a diversi aspetti visivi delle immagini, in modo che, se applicati, i tag contribuiscano alla ricerca di specifici tipi di immagini. Ad esempio, una raccolta di scarpe può avere tag diversi, ma tutti i tag sono correlati alle scarpe e possono appartenere allo stesso modello di tag. Se applicati, i tag consentono di trovare diversi tipi di scarpe, ad esempio per colore, design o per uso. Per comprendere la rappresentazione dei contenuti di un modello di formazione in [!DNL Experience Manager], visualizza un modello di formazione come entità di livello superiore composta da un gruppo di tag aggiunti manualmente e immagini di esempio per ciascun tag. Ogni tag può essere applicato esclusivamente a un’immagine.

Prima di creare un modello di tag e di addestrare il servizio, identifica un set di tag univoci che descrivono al meglio gli oggetti contenuti nelle immagini nel contesto della tua attività. Assicurati che le risorse nel set curato siano conformi alle [linee guida di formazione](#training-guidelines).

### Linee guida per la formazione {#training-guidelines}

Assicurati che le immagini del set di addestramento siano conformi alle seguenti linee guida:

**Quantità e dimensioni:** almeno 10 immagini e un massimo di 50 immagini per tag.

**Coerenza**: Assicurati che le immagini di un tag siano visivamente simili. È consigliabile aggiungere tag sugli stessi aspetti visivi (come lo stesso tipo di oggetti in un’immagine) insieme in un unico modello di tag. Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/coherence.png)

**Copertura**: Dovrebbe esserci una varietà sufficiente nelle immagini nell&#39;addestramento. L&#39;idea è quella di fornire alcuni esempi, ma abbastanza diversi, in modo che AEM imparare a concentrarsi sulle cose giuste. Se applichi lo stesso tag a immagini visivamente diverse, includi almeno cinque esempi di ogni tipo. Ad esempio, per il tag *model-down-pose*, includi più immagini di formazione simili all&#39;immagine evidenziata qui sotto per consentire al servizio di identificare immagini simili con maggiore precisione durante l&#39;assegnazione dei tag.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: Il servizio si allena meglio sulle immagini che hanno meno distrazioni (sfondi ben visibili, accompagnamento indipendenti, come oggetti/persone con il soggetto principale). Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per l&#39;addestramento.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali *raincoat* e *model-side-view*, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/completeness.png)

**Numero di tag**: Adobe consiglia di addestrare un modello utilizzando almeno due tag distinti e almeno dieci immagini diverse per ciascun tag. In un singolo modello di tag, non aggiungere più di 50 tag.

**Numero di esempi**: Per ogni tag, aggiungi almeno dieci esempi. Tuttavia, l&#39;Adobe consiglia circa 30 esempi. Sono supportati un massimo di 50 esempi per tag.

**Prevenire falsi positivi e conflitti**: Adobe consiglia di creare un singolo modello di tag per un singolo aspetto visivo. Crea una struttura per i modelli di tag in modo da evitare sovrapposizioni di tag tra i modelli. Ad esempio, non utilizzare tag comuni come `sneakers` in due nomi di modelli di tag diversi `shoes` e `footwear`. Il processo di formazione sovrascrive un modello di tag addestrato con l’altro per una parola chiave comune.

**Esempi**: Altri esempi di indicazioni sono:

* Creare un modello di tag che includa:
   * solo i tag relativi ai modelli di auto.
   * solo i tag relativi ai colori delle camicie.
   * solo i tag relativi a giacche per donne e uomini.
* Non creare,
   * un modello di tag che include modelli di auto rilasciati nel 2019 e 2020.
   * modelli di tag multipli che includono gli stessi pochi modelli di auto.

**Immagini utilizzate per la formazione**: Puoi utilizzare le stesse immagini per addestrare diversi modelli di tag. Tuttavia, non associare un’immagine a più tag in un modello di tag. È possibile assegnare tag alla stessa immagine con tag diversi appartenenti a modelli di tag diversi.

Non è possibile annullare la formazione. Le linee guida di cui sopra dovrebbero aiutarti a scegliere buone immagini da addestrare.

## Addestra il modello per i tag personalizzati {#train-model}

Per creare e addestrare un modello per i tag specifici dell’azienda, effettua le seguenti operazioni:

1. Crea i tag necessari e la struttura tag appropriata. Carica le immagini rilevanti nell’archivio DAM.
1. Nell&#39;interfaccia utente [!DNL Experience Manager], accedi a **[!UICONTROL Risorse]** > **[!UICONTROL Formazione di tag avanzati]**.
1. Fai clic su **[!UICONTROL Crea]**. Fornire un **[!UICONTROL Titolo]**, **[!UICONTROL Descrizione]**.
1. Sfogliare e selezionare i tag esistenti in `cq:tags` per i quali si desidera addestrare il modello. Fai clic su **[!UICONTROL Avanti]**.
1. Nella finestra di dialogo **[!UICONTROL Seleziona risorse]**, fai clic su **[!UICONTROL Aggiungi risorse]** rispetto a ciascun tag. Cerca nell’archivio DAM o sfoglia l’archivio per selezionare almeno 10 e al massimo 50 immagini. Seleziona le risorse e non la cartella. Dopo aver selezionato le immagini, fai clic su **[!UICONTROL Seleziona]**.

   ![Visualizza stato formazione](assets/smart-tags-training-status.png)

1. Per visualizzare in anteprima le miniature delle immagini selezionate, fai clic sul pannello a soffietto davanti a un tag. Per modificare la selezione, fai clic su **[!UICONTROL Aggiungi risorse]**. Una volta effettuata la selezione, fare clic su **[!UICONTROL Invia]**. L’interfaccia utente visualizza una notifica nella parte inferiore della pagina che indica che il training è stato avviato.
1. Controlla lo stato del corso di formazione nella colonna **[!UICONTROL Stato]** per ogni modello di tag. Gli stati possibili sono [!UICONTROL Pending], [!UICONTROL Tradotto] e [!UICONTROL Non riuscito].

![Flusso di lavoro per addestrare il modello di assegnazione tag per tag avanzati](assets/smart-tag-model-training-flow.png)

*Figura: Passaggi del flusso di lavoro di formazione per addestrare il modello di assegnazione tag.*

### Visualizza lo stato e il rapporto del corso di formazione {#training-status}

Per verificare se il servizio Tag avanzati è addestrato sui tag nel set di risorse di formazione, controlla il rapporto del flusso di lavoro di formazione dalla console Rapporti .

1. Nell&#39;interfaccia [!DNL Experience Manager] vai a **[!UICONTROL Strumenti] > **[!UICONTROL Risorse] > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, fai clic su **[!UICONTROL Crea]**.
1. Seleziona il rapporto **[!UICONTROL Formazione tag avanzati]**, quindi fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi, fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il rapporto, fai clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Rivedi i dettagli del rapporto. Il rapporto mostra lo stato di formazione per i tag che hai appreso. Il colore verde nella colonna **[!UICONTROL Stato formazione]** indica che per il tag è stato eseguito il training del servizio Tag avanzati. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag. Se i tag non vengono visualizzati in questo rapporto, esegui nuovamente il flusso di lavoro di formazione per questi tag.Tags
1. Per scaricare il rapporto, selezionalo dall’elenco e fai clic su **[!UICONTROL Scarica]** nella barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo [!DNL Microsoft Excel].

## Assegnare tag alle risorse {#tag-assets}

Dopo aver completato il training del servizio Tag avanzati, puoi attivare il flusso di lavoro di assegnazione tag per applicare automaticamente i tag appropriati a un set diverso di risorse simili. Puoi applicare il flusso di lavoro di assegnazione tag periodicamente o quando necessario. Il flusso di lavoro di assegnazione tag si applica sia alle risorse che alle cartelle.

### Assegnare tag alle risorse dalla console del flusso di lavoro {#tagging-assets-from-the-workflow-console}

1. Nell&#39;interfaccia [!DNL Experience Manager] vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di flusso di lavoro]**, seleziona il flusso di lavoro **[!UICONTROL Risorse di tag avanzati DAM]** e fai clic su **[!UICONTROL Avvia flusso di lavoro]** nella barra degli strumenti.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]**, individua la cartella del payload contenente le risorse sulle quali desideri applicare automaticamente i tag.
1. Specifica un titolo per il flusso di lavoro e un commento facoltativo. Fare clic su **[!UICONTROL Esegui]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figura: Passa alla cartella delle risorse ed esamina i tag per verificare se le risorse sono state contrassegnate correttamente. Per informazioni dettagliate, consulta [gestire tag avanzati](#manage-smart-tags-and-searches).*

### Assegnare tag alle risorse dalla timeline {#tagging-assets-from-the-timeline}

1. Dall’interfaccia utente di [!DNL Assets] , seleziona la cartella contenente le risorse o le risorse specifiche a cui desideri applicare i tag avanzati.
1. Dall&#39;angolo in alto a sinistra, apri la **[!UICONTROL Timeline]**.
1. Apri le azioni dalla parte inferiore della barra laterale sinistra e fai clic su **[!UICONTROL Avvia flusso di lavoro]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleziona il flusso di lavoro **[!UICONTROL DAM Smart Tag Assets]** e specifica un titolo per il flusso di lavoro.
1. Fare clic su **[!UICONTROL Start]**. Il flusso di lavoro applica i tag alle risorse. Accedi alla cartella delle risorse ed esamina i tag per verificare che le risorse siano state contrassegnate correttamente. Per informazioni dettagliate, consulta [gestire tag avanzati](#manage-smart-tags-and-searches).

>[!NOTE]
>
>Nei cicli di assegnazione tag successivi, solo le risorse modificate vengono nuovamente taggate con tag appena addestrati. Tuttavia, anche le risorse non modificate vengono contrassegnate se il divario tra l’ultimo ciclo di assegnazione tag e quello corrente per il flusso di lavoro di assegnazione tag supera le 24 ore. Per i flussi di lavoro con tag periodici, le risorse non modificate vengono contrassegnate quando il tempo gap supera i sei mesi.

### Assegnare tag alle risorse caricate {#tag-uploaded-assets}

[!DNL Experience Manager] può assegnare automaticamente i tag alle risorse caricate dagli utenti in DAM. A questo scopo, gli amministratori configurano un flusso di lavoro per aggiungere un passaggio disponibile che contrassegna le risorse. Consulta [come abilitare i tag avanzati per le risorse caricate](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).

## Gestire tag avanzati e ricerche di risorse {#manage-smart-tags-and-searches}

È possibile curare gli smart tag per rimuovere eventuali tag non accurati assegnati alle risorse del brand, in modo da visualizzare solo i tag più rilevanti.

La moderazione degli smart tag consente inoltre di perfezionare le ricerche delle risorse in base ai tag, garantendo che le risorse vengano visualizzate nei risultati di ricerca per i tag più rilevanti. In sostanza, aiuta a eliminare le possibilità che risorse non correlate vengano visualizzate nei risultati di ricerca.

Puoi anche assegnare un rango più alto a un tag per aumentare la pertinenza del tag per la risorsa. La promozione di un tag per una risorsa aumenta le possibilità che la risorsa appaia nei risultati della ricerca quando viene eseguita una ricerca in base al tag specifico.

Per moderare gli smart tag delle risorse:

1. Nel campo di ricerca cerca le risorse basate su un tag .

1. Inspect mostra i risultati della ricerca per identificare le risorse che non sono pertinenti alla ricerca.

1. Seleziona la risorsa, quindi seleziona ![Icona Gestisci tag](assets/do-not-localize/manage-tags-icon.png) dalla barra degli strumenti.

1. Dalla pagina **[!UICONTROL Gestione tag]** , controlla i tag . Se non desideri che la risorsa venga cercata in base a un tag specifico, seleziona il tag e seleziona ![Icona Elimina](assets/do-not-localize/delete-icon.png) dalla barra degli strumenti. In alternativa, seleziona il simbolo `X` accanto all’etichetta.

1. Per assegnare un rango più alto a un tag, selezionalo e seleziona ![Icona Promuovi](assets/do-not-localize/promote-icon.png) dalla barra degli strumenti. Il tag promosso viene spostato nella sezione **[!UICONTROL Tag]** .

1. Seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]** per chiudere la finestra di dialogo [!UICONTROL Success].

1. Passa alla pagina [!UICONTROL Proprietà] della risorsa. Osserva che al tag promosso è assegnata un’elevata rilevanza e, quindi, appare più alta nei risultati della ricerca.

### Comprendere AEM risultati della ricerca con tag avanzati {#understandsearch}

Per impostazione predefinita, AEM ricerca combina i termini di ricerca con una clausola `AND`. L’utilizzo di smart tag non modifica questo comportamento predefinito. L’utilizzo di tag avanzati aggiunge una clausola `OR` per trovare uno dei termini di ricerca negli smart tag applicati. Ad esempio, è consigliabile cercare `woman running`. Le risorse con una semplice `woman` o una semplice `running` parola chiave nei metadati non vengono visualizzate nei risultati di ricerca per impostazione predefinita. Tuttavia, una risorsa con tag `woman` o `running` utilizzando tag avanzati viene visualizzata in una query di ricerca di questo tipo. Quindi i risultati della ricerca sono una combinazione di:

* risorse con `woman` e `running` parole chiave nei metadati.

* risorse con tag avanzati con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrisponde a `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` negli smart tag.
1. corrispondenze di `woman` o di `running` negli smart tag.

## Limitazioni e best practice per l’assegnazione di tag {#limitations}

L’assegnazione tag avanzati è basata su modelli di apprendimento delle immagini e dei relativi tag. Questi modelli non sono sempre perfetti per identificare i tag. La versione corrente dei tag avanzati presenta le seguenti limitazioni:

* Incapacità di riconoscere sottili differenze nelle immagini. Ad esempio, camicie sottili o regolari.
* Incapacità di identificare i tag in base a piccoli pattern/parti di un’immagine. Ad esempio, i loghi sulle T-shirt.
* L’assegnazione tag è supportata nelle lingue supportate da [!DNL Experience Manager]. Per un elenco delle lingue, consulta [Note sulla versione del Servizio di contenuti avanzati](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* I tag che non vengono gestiti in modo realistico sono correlati a:

   * Aspetti non visivi e astratti. Ad esempio, l&#39;anno o la stagione di rilascio di un prodotto, l&#39;umore o le emozioni evocate da un&#39;immagine, la connotazione soggettiva di un video e così via.
   * Differenze visive fini in prodotti quali camicie con e senza collari o loghi di prodotti di piccole dimensioni incorporati nei prodotti.

<!-- TBD: Add limitations related to text-based assets. -->

Per cercare le risorse con tag avanzati (regolari o migliorati), utilizza la ricerca [!DNL Assets] (ricerca full-text). Non esiste un predicato di ricerca separato per gli smart tag.

>[!NOTE]
>
>La capacità dei tag avanzati di addestrare i tag e applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione.
>Per ottenere risultati ottimali, l’Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager] Configurazione per l’assegnazione tag avanzati](smart-tags-configuration.md)
>* [Informazioni sulla gestione delle risorse tramite tag avanzati](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Assegnazione di tag avanzati alle risorse video](smart-tags-video-assets.md)

