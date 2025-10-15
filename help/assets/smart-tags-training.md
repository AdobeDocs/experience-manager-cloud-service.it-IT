---
title: Assegna tag automatici alle risorse con  [!DNL Adobe Sensei] servizio avanzato
description: Assegna tag alle risorse con un servizio artificialmente intelligente che applica tag aziendali contestuali e descrittivi.
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: a579e2e25ecff93f6f1487ec0bcd317df09751cf
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 5%

---


# Apprendimento dei tag avanzati

L’apprendimento dei tag avanzati consente di addestrare i tag in modo da poter specificare i dettagli se i tag rilevanti non sono presenti. Utilizza un framework artificialmente intelligente di [Adobe Sensei](https://business.adobe.com/it/why-adobe/experience-cloud-artificial-intelligence.html) per addestrare il suo algoritmo di riconoscimento delle immagini in base alla tua struttura dei tag e alla tassonomia aziendale. Questa content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse. [!DNL Experience Manager Assets] applica automaticamente i tag avanzati alle risorse caricate, per impostazione predefinita.

## Determinazione del requisito dell’apprendimento dei tag avanzati {#smart-tag-training-requirement}

L’apprendimento dei tag avanzati è necessario nei seguenti scenari:

* Aggiungere un&#39;etichetta automatica per salvare le iterazioni di aggiunta delle etichette ogni volta che si carica la stessa risorsa.
* Migliorare la capacità delle risorse di applicare tag rilevanti.
* Per migliorare la precisione dei tag visualizzati per una risorsa.
* Per aggiungere etichette non disponibili o mancanti.


>[!NOTE]
>
>Gli smart tag di formazione sono applicabili solo a un ***tipo di immagine*** della risorsa.

## Passaggi necessari per l’apprendimento dei tag avanzati

Per impostazione predefinita, [!DNL Experience Manager] come [!DNL Cloud Service] genera automaticamente i tag avanzati nelle risorse basate su testo e nei video. Per addestrare i tag avanzati alle immagini, completa le seguenti attività:

* [Comprendere modelli e linee guida per i tag](#understand-tag-models-guidelines)
* [Addestra il modello](#train-model)
* [Assegnare tag alle risorse digitali](#tag-assets)
* [Gestire tag e ricerche](#manage-smart-tags-and-searches)

## Comprendere modelli e linee guida per i tag {#understand-tag-models-guidelines}

Un modello di tag è un gruppo di tag correlati associati a vari aspetti visivi delle immagini a cui vengono assegnati tag. I tag si riferiscono agli aspetti visivi nettamente diversi delle immagini, in modo che, se applicati, aiutino a cercare tipi specifici di immagini. Ad esempio, una raccolta di scarpe può avere tag diversi, ma tutti i tag sono correlati alle scarpe e possono appartenere allo stesso modello di tag. Quando applicati, i tag consentono di trovare diversi tipi di scarpe, ad esempio per progettazione o per utilizzo.

Prima di creare un modello di tag e addestrare il servizio, identifica un set di tag univoci che descrivono al meglio gli oggetti nelle immagini nel contesto della tua azienda. Assicurati che le risorse nel set curato confermino di [le linee guida per la formazione](#training-guidelines).

### Linee guida per la formazione {#training-guidelines}

Assicurati che le immagini nel set di formazione siano conformi alle seguenti linee guida:

<table>
   <tr>
      <th> Metrica </th>
      <th> Descrizione </th>
   </tr>
   <tr>
      <td> <b>Quantità e dimensioni </b></td>
      <td> Da un minimo di 10 a un massimo di 50 immagini per tag. </td>
   </tr>
   <tr>
      <td> <b>Coerenza</b> </td>
      <td> Assicurati che le immagini di un tag siano visivamente simili. È consigliabile aggiungere i tag relativi agli stessi aspetti visivi (come lo stesso tipo di oggetti in un’immagine) in un unico modello di tag. Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag <i>my-party</i> (per la formazione) perché non sono visivamente simili. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/coherence.png"><br><i>Figura: immagini illustrative di Coherence che illustrano le linee guida per la formazione</i>
      </td>
   </tr>
   <tr>
      <td> <b>Copertura</b></td>
      <td> Le immagini del corso di formazione devono essere sufficientemente varie. L'idea è quella di fornire alcuni esempi, ma ragionevolmente diversi, in modo che apprenda a concentrarsi sulle cose giuste. Se applichi lo stesso tag a immagini visivamente diverse, includi almeno cinque esempi per ogni tipo. Ad esempio, per il tag <i>model-down-pose</i>, includi più immagini di formazione simili all'immagine evidenziata di seguito affinché il servizio identifichi più accuratamente immagini simili durante l'assegnazione dei tag.</td>
   </tr>
   <tr>
   <td colspan="2"> <img src="assets/do-not-localize/coverage_1.png"><br><i>Figura: immagini illustrative della copertura per esemplificare le linee guida per la formazione</i>
   </td>
   </tr>
   <tr>
      <td><b>Distrazione/ostruzione</b> </td>
      <td> Il servizio si addestra meglio alle immagini che hanno meno distrazione (sfondi prominenti, accompagnamenti non correlati, come oggetti/persone con il soggetto principale). Ad esempio, per il tag <i>casual-shoe</i>, la seconda immagine non è un buon candidato per la formazione. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/distraction.png"><br><i>Figura: immagini illustrative di distrazione/ostruzione per esemplificare le linee guida per la formazione</i>
      </td>
   </tr>
   <tr>
      <td> <b>Completezza</b> </td>
      <td> Se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali <i>raincoat</i> e <i>model-side-view</i>, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/completeness.png"><br><i>Figura: immagini illustrative di completezza che illustrano le linee guida per la formazione</i>
      </td>
   </tr>
   <tr>
      <td> <b>Numero di tag</b> </td>
      <td> Adobe consiglia di addestrare un modello utilizzando almeno due tag distinti e almeno dieci immagini diverse per ogni tag. In un singolo modello di tag, non aggiungere più di 50 tag. </td>
   </tr>
   <tr>
      <td> <b>Numero di esempi</b> </td>
      <td> Per ogni tag, aggiungi almeno dieci esempi. Tuttavia, Adobe consiglia circa 30 esempi. Sono supportati un massimo di 50 esempi per tag. </td>
   </tr>
   <tr>
      <td> <b>Impedisci falsi positivi e conflitti</b> </td>
      <td> Adobe consiglia di creare un modello di tag singolo per un singolo aspetto visivo. Strutturare i modelli di tag in modo da evitare la sovrapposizione dei tag tra i modelli. Ad esempio, non utilizzare tag comuni come <i>sneakers</i> in due diversi modelli di tag con nomi di <i>scarpe</i> e <i>calzature</i>. Il processo di apprendimento sovrascrive un modello di tag addestrato con l’altro per una parola chiave comune. </td>
   </tr>
</table>

**Esempi**: ulteriori esempi a titolo di guida:

* Crea un modello di tag che includa solo:

   * I tag relativi ai modelli di auto.
   * I tag relativi a giacche per adulti e bambini.

* Non creare,

   * Un modello di tag che include i modelli di auto rilasciati nel 2019 e nel 2020.
   * Più modelli di tag che includono gli stessi pochi modelli di auto.

>[!NOTE]
>
>Puoi utilizzare le stesse immagini per addestrare diversi modelli di tag. Tuttavia, non associare un’immagine a più tag in un modello di tag. È possibile assegnare tag alla stessa immagine con tag diversi appartenenti a modelli di tag diversi.
>&#x200B;>Non è possibile annullare l’apprendimento. Le linee guida di cui sopra dovrebbero aiutarti a scegliere le immagini migliori da addestrare.

## Addestra il modello per i tag personalizzati {#train-model}

Per creare e addestrare un modello per i tag specifici per l’azienda, segui questi passaggi:

1. Crea i tag necessari e la struttura tag appropriata. Carica le immagini rilevanti nell’archivio DAM.
1. Nell&#39;interfaccia utente di [!DNL Experience Manager Cloud Service], accedere a **[!UICONTROL Assets]** > **[!UICONTROL Apprendimento dei tag avanzati]**.
1. Fai clic su **[!UICONTROL Crea]**. Fornisci un **[!UICONTROL Titolo]**, **[!UICONTROL Descrizione]**.
1. Fai clic sull&#39;icona della cartella nel campo **[!UICONTROL Tag]**. Viene visualizzata una finestra popup.
1. Cercare o selezionare i tag appropriati dai tag esistenti in `cq-tags` che si desidera aggiungere al modello. Fai clic su **[!UICONTROL Avanti]**.

   >[!NOTE]
   >
   >Puoi ordinare la struttura dei tag in ordine crescente o decrescente in base alla data **[!UICONTROL Name]** (ordine alfabetico), **[!UICONTROL Created]** o **[!UICONTROL Modified]**.


1. Nella finestra di dialogo **[!UICONTROL Seleziona Assets]**, fai clic su **[!UICONTROL Aggiungi Assets]** per ogni tag. Cerca nell’archivio DAM o sfoglia l’archivio per selezionare almeno 10 e al massimo 50 immagini. Seleziona le risorse e non la cartella. Dopo aver selezionato le immagini, fai clic su **[!UICONTROL Seleziona]**.

   ![Visualizza stato apprendimento](assets/smart-tags-training-status.png)

1. Per visualizzare in anteprima le miniature delle immagini selezionate, fai clic sul pannello a soffietto di fronte a un tag. Puoi modificare la selezione facendo clic su **[!UICONTROL Aggiungi Assets]**. Una volta effettuata la selezione, fare clic su **[!UICONTROL Invia]**. L’interfaccia utente visualizza una notifica nella parte inferiore della pagina che indica che il corso di formazione è stato avviato.
1. Controlla lo stato del corso di formazione nella colonna **[!UICONTROL Stato]** per ogni modello di tag. Gli stati possibili sono [!UICONTROL In sospeso], [!UICONTROL Addestrato] e [!UICONTROL Non riuscito].

![Flusso di lavoro per addestrare il modello di assegnazione tag per Tag avanzati](assets/smart-tag-model-training-flow.png)

*Figura: passaggi del flusso di lavoro di formazione per addestrare il modello di assegnazione tag.*

### Visualizza stato e rapporto del corso di formazione {#training-status}

Per verificare se il servizio Tag avanzati è stato addestrato sui tag nel set di apprendimento delle risorse, controlla il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell&#39;interfaccia [!DNL Experience Manager Cloud Service], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Rapporti risorse]**, fai clic su **[!UICONTROL Crea]**.
1. Seleziona il report **[!UICONTROL Apprendimento dei tag avanzati]** e fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi fare clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il report, fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Esamina i dettagli del rapporto. Il rapporto mostra lo stato di formazione per i tag che hai appreso. Il colore verde nella colonna **[!UICONTROL Training Status]** indica che il servizio Tag avanzati è stato addestrato per il tag. Il colore giallo indica che il servizio è parzialmente addestrato per un determinato tag. Per addestrare completamente il servizio per un tag, aggiungi altre immagini con il tag specifico ed esegui il flusso di lavoro di formazione. Se non trovi i tuoi tag in questo rapporto, esegui nuovamente il flusso di lavoro di formazione per questi tag.Tags
1. Per scaricare il report, selezionarlo dall&#39;elenco e fare clic su **[!UICONTROL Scarica]** nella barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo.

>[!NOTE]
>
>Cosa succede se voglio trasferire la formazione di tag avanzati da un’istanza all’altra tramite un’esportazione?
>&#x200B;>Non è necessario esportare l’apprendimento dei tag avanzati se l’ambiente appartiene alla stessa organizzazione IMS. Viene condiviso automaticamente. Se l’ambiente si trova in più organizzazioni IMS, non è possibile condividere o esportare l’apprendimento dei tag avanzati.

## Limitazioni e best practice relative agli smart tag {#limitations-smart-tags-training}

* Per addestrare il modello, utilizzate le immagini più appropriate. Non è possibile ripristinare l’addestramento o rimuovere il modello di addestramento. La precisione dei tag dipende dall&#39;addestramento corrente, quindi esegui questa operazione con attenzione.
* Non puoi addestrare il servizio che applica Tag avanzati ai video utilizzando video specifici. Funziona con le impostazioni predefinite di [!DNL Adobe Sensei].


>[!NOTE]
>
>La capacità dei tag avanzati di addestrarsi sui tag e di applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per l’apprendimento.
>&#x200B;>Per ottenere i migliori risultati, Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.
