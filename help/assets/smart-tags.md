---
title: Applicare tag alle immagini con servizi intelligenti artificialmente.
description: Applicate tag alle immagini con servizi intelligenti artificialmente che applicano tag commerciali contestuali e descrittivi utilizzando i servizi Adobe Sensei.
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf7bb91dd488f39181a08adc592971d6314817de
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 5%

---


# Applicazione di tag alle immagini tramite i servizi avanzati {#smart-tag-assets}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre di più il vocabolario controllato dalla tassonomia nei metadati delle risorse. Comprende in sostanza un elenco di parole chiave utilizzate comunemente da dipendenti, partner e clienti per fare riferimento e cercare le risorse digitali. L’assegnazione di tag alle risorse mediante il vocabolario controllato dalla tassonomia consente di identificare e recuperare facilmente le risorse mediante ricerche basate sui tag.

Rispetto ai vocabolari di lingua naturale, l’assegnazione di tag in base alla tassonomia aziendale consente di allineare le risorse all’attività aziendale e garantisce che le risorse più rilevanti vengano visualizzate nelle ricerche. Ad esempio, un produttore di auto può assegnare tag alle immagini di un&#39;auto con nomi di modelli in modo che vengano visualizzate solo immagini rilevanti quando viene effettuata una ricerca per progettare una campagna promozionale.

In background, lo Smart Tags utilizza un framework di intelligenza artificiale di [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) per formare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e la tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un altro set di risorse.

<!-- TBD: Create a similar flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

Per utilizzare i tag avanzati, effettuate le seguenti operazioni:

* [Integrare Experience Manager con Adobe I/O](#integrate-aem-with-aio).
* [Informazioni sui modelli e sulle linee guida](#understand-tag-models-guidelines)dei tag.
* [Formare il modello](#train-model).
* [Assegnare tag alle risorse](#tag-assets)digitali.
* [Gestire tag e ricerche](#manage-smart-tags-and-searches).

I tag avanzati sono applicabili solo ai [!DNL Adobe Experience Manager Assets] clienti. I tag avanzati sono disponibili per l&#39;acquisto come componente aggiuntivo per [!DNL Experience Manager].

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? -->

## Integrazione [!DNL Experience Manager] con Adobe I/O {#integrate-aem-with-aio}

È possibile effettuare l’integrazione [!DNL Adobe Experience Manager] con i tag avanzati utilizzando l’I/O di Adobe. Utilizzate questa configurazione per accedere al servizio Smart Tags dall&#39;interno [!DNL Experience Manager].

Consultate [configurare Experience Manager per l’assegnazione di tag avanzati alle risorse](smart-tags-configuration.md) per le attività di configurazione dei tag avanzati. Sul lato posteriore, il [!DNL Experience Manager] server autentica le credenziali del servizio con il gateway di I/O Adobe prima di inoltrare la richiesta al servizio Smart Tags.

## Informazioni sui modelli e sulle linee guida dei tag {#understand-tag-models-guidelines}

Un modello di tag è un gruppo di tag correlati che si trovano per aspetto visivo dell’immagine. Ad esempio, una raccolta di scarpe può avere tag diversi, ma tutti i tag sono correlati a scarpe e possono appartenere allo stesso modello di tag. I tag possono essere correlati solo con gli aspetti visivi delle immagini chiaramente diversi. Per comprendere la rappresentazione del contenuto di un modello di formazione in [!DNL Experience Manager], visualizzate un modello di formazione come entità di livello principale composta da un gruppo di tag aggiunti manualmente e immagini di esempio per ciascun tag. Ogni tag può essere applicato esclusivamente a un’immagine.

I tag che non possono essere gestiti in modo realistico si riferiscono a:

* Aspetti non visivi e astratti come l&#39;anno o la stagione di rilascio di un prodotto, l&#39;umore o le emozioni evocate da un&#39;immagine.
* Riduzioni visive di prodotti quali camicie con e senza collari o loghi di prodotti di piccole dimensioni incorporati nei prodotti.

Prima di creare un modello di tag e di formare il servizio, identificate un set di tag univoci che meglio descrivano gli oggetti contenuti nelle immagini nel contesto della vostra attività. Assicurati che le risorse del set selezionato siano conformi alle linee guida [](#training-guidelines)di formazione.

### Linee guida per la formazione {#training-guidelines}

Le immagini nel set di formazione devono essere conformi alle seguenti linee guida:

**Quantità e dimensioni:** Almeno 10 immagini e massimo 50 immagini per tag.

**Coerenza**: Le immagini di un tag devono essere visivamente simili. È consigliabile unire i tag relativi agli stessi aspetti visivi (come lo stesso tipo di oggetti in un’immagine) in un singolo modello di tag. Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/coherence.png)

**Copertura**: Dovrebbe esserci una varietà sufficiente nelle immagini della formazione. L’idea è di fornire alcuni esempi, ma con una discreta diversità, in modo che AEM possa concentrarsi sulle cose giuste. Se applicate lo stesso tag a immagini visivamente diverse, includete almeno cinque esempi di ciascun tipo. Ad esempio, per il tag *model-down-pose*, includete più immagini di formazione simili all’immagine evidenziata di seguito per il servizio, in modo da identificare immagini simili con maggiore precisione durante l’assegnazione dei tag.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: Il servizio si allena meglio sulle immagini con meno distrazioni (sfondi visibili, accompagnamento indipendenti, come oggetti/persone con il soggetto principale). Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per l&#39;addestramento.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali *raincoat* e *model-side-view*, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/completeness.png)

**Numero di tag**: Adobe consiglia di addestrare un modello utilizzando almeno due tag distinti e almeno 10 immagini diverse per ciascun tag. In un singolo modello di tag, non aggiungete più di 50 tag.

**Numero di esempi**: Per ciascun tag, aggiungete almeno 10 esempi. Tuttavia, Adobe consiglia circa 30 esempi. È supportato un massimo di 50 esempi per tag.

**Prevenire falsi positivi e conflitti**: Adobe consiglia di creare un singolo modello di tag per un singolo aspetto visivo. Strutturate i modelli di tag in modo da evitare la sovrapposizione di tag tra i modelli. Ad esempio, non utilizzate tag comuni come `sneakers` in due diversi nomi di modelli di tag `shoes` e `footwear`. Il processo di formazione sovrascrive un modello di tag formattato con l’altro per una parola chiave comune.

**Esempi**: Altri esempi sono:

* Create un modello di tag che includa:
   * solo i tag relativi ai modelli di auto.
   * solo i tag relativi ai colori delle camicie.
   * solo i tag relativi alle giacche per donne e uomini.
* Non creare,
   * un modello di tag che include modelli di auto rilasciati nel 2019 e 2020.
   * modelli di tag multipli che includono gli stessi pochi modelli di auto.

**Immagini utilizzate per la formazione**: Potete usare le stesse immagini per formare diversi modelli di tag. Tuttavia, non associano un’immagine a più tag in un modello di tag. È quindi possibile assegnare alla stessa immagine tag diversi appartenenti a diversi modelli di tag.

Non potete annullare la formazione. Le linee guida di cui sopra dovrebbero aiutarvi a scegliere buone immagini da formare.

## Formazione del modello per i tag personalizzati {#train-model}

Per creare e formare un modello per i tag aziendali specifici, procedere come segue:

1. Create i tag necessari e la struttura di tag appropriata. Caricate le immagini rilevanti nell&#39;archivio DAM.
1. Nell’interfaccia [!DNL Experience Manager] utente, accedi a **[!UICONTROL Risorse]** > Modello **** formazione.
1. Fai clic su **[!UICONTROL Crea]**. Specificate un **[!UICONTROL Titolo]**, una **[!UICONTROL Descrizione]**.
1. Sfogliare e selezionare i tag presenti nei tag esistenti per `cq:tags` cui si desidera formare il modello. Fai clic su **[!UICONTROL Avanti]**.
1. Nella finestra di dialogo **[!UICONTROL Seleziona risorse]** , fate clic su **[!UICONTROL Aggiungi risorse]** per ciascun tag. Cercate nell&#39;archivio DAM o sfogliate l&#39;archivio per selezionare almeno 10 e al massimo 50 immagini. Selezionate le risorse e non la cartella. Dopo aver selezionato le immagini, fate clic su **[!UICONTROL Seleziona]**.
1. Per visualizzare in anteprima le miniature delle immagini selezionate, fate clic sulla struttura di navigazione davanti a un tag. Per modificare la selezione, fai clic su **[!UICONTROL Aggiungi risorse]**. Una volta completata la selezione, fate clic su **[!UICONTROL Invia]**. L’interfaccia utente visualizza una notifica nella parte inferiore della pagina per indicare che la formazione è avviata.
1. Controllate lo stato della formazione nella colonna **[!UICONTROL Stato]** per ciascun modello di tag. Gli stati possibili sono [!UICONTROL In attesa], [!UICONTROL Formazione]e [!UICONTROL Non riuscito].

![Flusso di lavoro per formare il modello di tag per smart tag](assets/smart-tag-model-training-flow.png)

*Figura: Passaggi del flusso di lavoro di formazione per formare il modello di tag.*

### Visualizzazione dello stato e del rapporto della formazione {#training-status}

Per verificare se il servizio Smart Tags è addestrato sui tag nel set di risorse di formazione, controllate il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell&#39; [!DNL Experience Manager] interfaccia, accedi a **[!UICONTROL Strumenti > Risorse > Rapporti]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Then, click **[!UICONTROL Create]** from the toolbar.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. To view the report, click **[!UICONTROL View]** from the toolbar.
1. Rivedete i dettagli del rapporto. Il rapporto mostra lo stato di formazione per i tag che hai appreso. The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Tags service is trained for the tag. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag. Se i tag non vengono visualizzati in questo rapporto, eseguite di nuovo il flusso di lavoro di formazione per questi tag.Tags
1. Per scaricare il rapporto, selezionatelo dall’elenco e fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo di Microsoft Excel.

## Assegnare tag alle risorse {#tag-assets}

Dopo aver preparato il servizio Smart Tags, potete attivare il flusso di lavoro dei tag per applicare automaticamente i tag appropriati a un altro set di risorse simili. Potete applicare il flusso di lavoro dei tag periodicamente o ogni volta che lo desiderate. Il flusso di lavoro dei tag si applica a risorse e cartelle.

### Assegnare tag alle risorse dalla console del flusso di lavoro {#tagging-assets-from-the-workflow-console}

1. Nell’interfaccia di Experience Manager, andate a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]** , individuate la cartella payload contenente le risorse per le quali desiderate applicare automaticamente i tag.
1. Specificate un titolo per il flusso di lavoro e un commento facoltativo. Fate clic su **[!UICONTROL Esegui]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Andate alla cartella delle risorse e controllate i tag per verificare se i tag delle risorse sono correttamente associati. Per informazioni dettagliate, consultate [Gestione di smart tag](#manage-smart-tags-and-searches).

### Applicare tag alle risorse dalla timeline {#tagging-assets-from-the-timeline}

1. Dall’interfaccia utente di Risorse, selezionate la cartella contenente le risorse o risorse specifiche a cui desiderate applicare gli smart tag.
1. Dall&#39;angolo superiore sinistro, aprite la **[!UICONTROL timeline]**.
1. Aprite le azioni nella parte inferiore della barra laterale sinistra e fate clic su **[!UICONTROL Avvia flusso di lavoro]**.

   ![start_workflow](assets/start_workflow.png)

1. Selezionate il flusso di lavoro **[!UICONTROL DAM Smart Tag Assets]** e specificate un titolo per il flusso di lavoro.
1. Fate clic su **[!UICONTROL Avvia]**. Il flusso di lavoro applica i tag alle risorse. Andate alla cartella delle risorse e verificate i tag necessari per verificare se i tag delle risorse sono stati impostati correttamente. Per informazioni dettagliate, consultate [Gestione di smart tag](#manage-smart-tags-and-searches).

>[!NOTE]
>
>Nei cicli di assegnazione dei tag successivi, solo le risorse modificate dispongono di tag di nuova formazione. Tuttavia, vengono assegnati tag anche alle risorse inalterate se lo spazio tra l’ultimo ciclo di tag e quello corrente per il flusso di lavoro dei tag supera le 24 ore. Per i flussi di lavoro con tag periodici, le risorse inalterate vengono contrassegnate con tag quando l’intervallo di tempo supera i 6 mesi.

### Assegnare tag alle risorse caricate {#tag-uploaded-assets}

Experience Manager consente di assegnare automaticamente i tag alle risorse che gli utenti caricano in DAM. A questo scopo, gli amministratori configurano un flusso di lavoro per aggiungere un passaggio disponibile alle risorse degli smart tag. Scoprite [come abilitare i tag avanzati per le risorse](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)caricate.

## Gestione di smart tag e ricerche di immagini {#manage-smart-tags-and-searches}

Potete curare gli smart tag per rimuovere eventuali tag non accurati eventualmente assegnati alle immagini del vostro marchio, in modo da visualizzare solo i tag più rilevanti.

La moderazione degli smart tag consente inoltre di perfezionare le ricerche basate sui tag per le immagini, assicurando che l’immagine venga visualizzata nei risultati di ricerca per i tag più rilevanti. In sostanza, elimina la possibilità che immagini non collegate vengano visualizzate nei risultati della ricerca.

Potete anche assegnare un rango più alto a un tag per aumentarne la rilevanza rispetto a un’immagine. La promozione di un tag per un’immagine aumenta le probabilità che l’immagine venga visualizzata nei risultati di ricerca quando viene eseguita una ricerca in base al tag specifico.

1. Nella casella di ricerca Omnico, cercate le risorse in base a un tag.
1. Controllate i risultati della ricerca per identificare un’immagine che non trovate rilevante per la ricerca.
1. Selezionate l’immagine, quindi fate clic sull’icona **[!UICONTROL Gestisci tag]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Gestisci tag]** , ispezionate i tag. Se non desiderate che l’immagine venga cercata in base a un tag specifico, selezionate il tag e fate clic sull’icona Elimina nella barra degli strumenti. In alternativa, fare clic sul `X` simbolo visualizzato accanto all&#39;etichetta.
1. Per assegnare un livello superiore a un tag, selezionatelo e fate clic sull’icona di promozione nella barra degli strumenti. Il tag promosso viene spostato nella sezione **[!UICONTROL Tag]** .
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. Passate alla pagina delle proprietà dell’immagine. Osservate che al tag promosso è stata assegnata un’elevata rilevanza e, di conseguenza, appare più alta nei risultati della ricerca.

### Comprendere i risultati della ricerca AEM con gli smart tag {#understandsearch}

Per impostazione predefinita, la ricerca AEM combina i termini di ricerca con una `AND` clausola. L&#39;utilizzo di smart tag non modifica questo comportamento predefinito. L&#39;utilizzo di smart tag aggiunge una `OR` clausola aggiuntiva per individuare qualsiasi termine di ricerca negli smart tag applicati. For example, consider searching for `woman running`. Per impostazione predefinita, le risorse con una sola parola chiave `woman` o una sola `running` parola chiave nei metadati non vengono visualizzate nei risultati della ricerca. Tuttavia, in una query di ricerca di questo tipo viene visualizzata una risorsa con `woman` o `running` tramite smart tag. Quindi i risultati della ricerca sono una combinazione di:

* risorse con `woman` e `running` parole chiave nei metadati.

* assets smart tag con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a uno qualsiasi dei termini di ricerca negli smart tag. Nell&#39;esempio precedente, l&#39;ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrispondenze di `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` in smart tag.
1. corrispondenze di `woman` o di `running` in smart tag.

### Limiti per i tag {#limitations}

Gli smart tag avanzati si basano su modelli di apprendimento delle immagini del marchio e dei relativi tag. Questi modelli non sempre sono perfetti per identificare i tag. La versione corrente dei tag avanzati presenta le seguenti limitazioni:

* Incapacità di riconoscere sottili differenze nelle immagini. Ad esempio, camicie sottili o regolari.
* Impossibile identificare i tag in base a piccoli pattern/parti di un’immagine. Ad esempio, i logo delle T-shirt.
* I tag sono supportati nelle impostazioni internazionali in cui AEM è supportato. Per un elenco delle lingue, consultate [Note](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)sulla versione dei tag avanzati.

Per cercare le risorse con gli smart tag (regolari o avanzati), usate la ricerca Omnisearch delle risorse (ricerca full-text). Non esiste un predicato di ricerca separato per gli smart tag.

>[!NOTE]
>
>La capacità dei tag avanzati di formare i tag e applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione.
>Per risultati ottimali, Adobe consiglia di usare immagini visivamente simili per addestrare il servizio per ciascun tag.

>[!MORELIKETHIS]
>
>* [Configurare Experience Manager per l&#39;assegnazione di smart tag](smart-tags-configuration.md)
>* [Come gli smart tag consentono di gestire le risorse](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)

