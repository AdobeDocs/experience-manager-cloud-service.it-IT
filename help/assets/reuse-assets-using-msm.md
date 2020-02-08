---
title: Riutilizzare le risorse con MSM per le risorse
description: Utilizzate le risorse tra più pagine/cartelle derivate e collegate alle risorse principali. Le risorse restano sincronizzate con una copia principale e, con pochi clic, ricevono gli aggiornamenti dalle risorse principali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Riutilizzare le risorse con MSM per le risorse{#reuse-assets-using-msm-for-assets}

La funzionalità Multi Site Manager (MSM) di Adobe Experience Manager (AEM) consente agli utenti di riutilizzare contenuti creati una volta e riutilizzati in più posizioni Web. Lo stesso è disponibile per le risorse digitali come MSM per la funzionalità Assets. Utilizzando MSM per Assets, puoi:

* Create una volta e quindi copiate le risorse da riutilizzare in altre aree del sito.
* Mantenete più copie in sincronizzazione e aggiornate la copia master originale una volta per inviare le modifiche alle copie figlio.
* Apportate modifiche locali sospendendo temporaneamente o permanentemente il collegamento tra risorse padre e risorse figlio.

## Comprendere i vantaggi e i concetti {#concepts}

### Come funziona e vantaggi {#how-it-works-and-the-benefits}

AEM gestisce un collegamento tra la risorsa originale e le relative copie collegate, denominate Live Copy (LC). Il collegamento mantenuto consente di trasferire le modifiche centralizzate a molte copie live. Questo consente di velocizzare gli aggiornamenti eliminando i limiti di gestione delle copie duplicate. La propagazione delle modifiche è senza errori e centralizzata. Questa funzione consente di aggiornare le copie in diretta selezionate. Gli utenti possono scollegare il collegamento, ossia interrompere l’ereditarietà, e apportare modifiche locali che non verranno sovrascritte al successivo aggiornamento della copia master e al rollout delle modifiche. Lo scollegamento può essere eseguito per alcuni campi di metadati selezionati o per un’intera risorsa. Consente di aggiornare localmente le risorse che sono state originariamente ereditate da una copia master.

MSM mantiene una relazione live tra la risorsa di origine e le sue copie in tempo reale in modo che:

* Le modifiche apportate alle risorse sorgente vengono applicate anche alle copie in diretta, ossia le copie in diretta vengono sincronizzate con l’origine.
* Potete aggiornare le copie in diretta sospendendo la relazione in diretta o rimuovendo l&#39;ereditarietà per alcuni campi limitati. Le modifiche all&#39;origine non vengono più applicate alla Live Copy.

### Glossario di MSM per i termini di Risorse {#glossary}

**Origine** Le risorse o le cartelle originali. Copia principale da cui derivano le copie in diretta.

**Live Copy** La copia delle risorse/delle cartelle sorgente in sincronizzazione con l’origine. Le copie in diretta possono essere fonte di ulteriori copie in diretta. Scopri come creare LC.

**Ereditarietà** Un collegamento/riferimento tra una risorsa/cartella Live Copy e la relativa origine utilizzata dal sistema per ricordare dove inviare gli aggiornamenti. L’ereditarietà esiste a un livello granulare per i campi di metadati. L’ereditarietà può essere rimossa per i campi di metadati selettivi, mantenendo al contempo la relazione live tra l’origine e la copia dal vivo.

**Rollout** Un&#39;azione che invia le modifiche apportate all&#39;origine a valle alle sue copie live. È possibile aggiornare una o più copie live in una sola volta mediante l&#39;azione di rollout. Consultate Rollout.

**Regole di configurazione** rollout che determinano le proprietà da sincronizzare, come e quando. Queste configurazioni vengono applicate durante la creazione di copie live; può essere modificato successivamente; e un figlio può ereditare la configurazione di rollout dalla risorsa principale. Per MSM for Assets, usa solo la configurazione rollout standard. Le altre configurazioni di rollout non sono disponibili per MSM for Assets.

**Sincronizza** un’altra azione, oltre al rollout, che porta la parità tra l’origine e la sua live copy inviando gli aggiornamenti dall’origine alle Live Copy. Viene avviata la sincronizzazione per una particolare Live Copy e l&#39;azione richiama le modifiche dall&#39;origine. Utilizzando questa azione, è possibile aggiornare solo una delle Live Copy. Consultate Sincronizzare l’azione.

**Sospendi** Rimuove temporaneamente la relazione dal vivo tra una Live Copy e la risorsa/cartella di origine. È possibile riprendere la relazione. Consultate sospensione dell’azione.

**Riprendi** Riprendi la relazione dal vivo in modo che una live copy riceva nuovamente gli aggiornamenti dall&#39;origine. Consultate Azione di ripresa.

**Con l’azione Ripristina** , la Live Copy viene nuovamente trasformata in una replica dell’origine, sovrascrivendo eventuali modifiche locali. Inoltre rimuove le cancellazioni dell’ereditarietà e ripristina l’ereditarietà in tutti i campi di metadati. Per apportare modifiche locali in futuro, è necessario annullare nuovamente l&#39;ereditarietà di campi specifici. Consultate le modifiche locali a LC.

**Scollega** in modo irreversibile rimuove la relazione live di una risorsa o una cartella Live Copy. Dopo l&#39;azione di scollegamento, le copie live non potranno mai ricevere gli aggiornamenti dall&#39;origine e non saranno più una live copy. Consultate rimuovere la relazione.

## Creare una Live Copy di una risorsa {#createlc}

Per creare una Live Copy da una o più risorse o cartelle sorgente, effettuate le seguenti operazioni:

* Metodo 1: Selezionate le risorse sorgente e fate clic su **[!UICONTROL Crea > Live Copy]** dalla barra degli strumenti nella parte superiore.

* Metodo 2: Nell’interfaccia utente di AEM, fai clic su **[!UICONTROL Crea > Live Copy]** nell’angolo in alto a destra dell’interfaccia.

Potete creare copie live di una risorsa o di una cartella una per volta. Potete creare delle copie dal vivo derivate da una risorsa o da una cartella che è una Live Copy stessa.  I frammenti di contenuto (CF) non sono supportati per il caso di utilizzo. Quando tentano di creare le loro copie dal vivo, i CF vengono copiati così come non esiste alcuna relazione. Gli CF copiati sono un&#39;istantanea nel tempo e non si aggiornano quando gli CF originali vengono aggiornati.

Per creare copie live con il primo metodo, attenetevi alla seguente procedura:

1. Selezionate le risorse o le cartelle sorgente. Dalla barra degli strumenti, fate clic su **[!UICONTROL Crea > Live Copy]**.

   ![Creare una live copy dall’interfaccia di AEM](assets/create_lc1.png)

   Creare una live copy dall’interfaccia di AEM

1. Selezionate una cartella di destinazione. Fai clic su **[!UICONTROL Avanti]**.
1. Fornire titolo e nome. Le risorse non hanno elementi figlio. Quando create una Live Copy di cartelle, potete scegliere di includere o escludere elementi figlio.
1. Selezionate una configurazione di rollout. Fai clic su **[!UICONTROL Crea]**. 

Per creare copie live con il secondo metodo, attenetevi alla seguente procedura:

1. Nell’interfaccia di AEM, dall’angolo in alto a destra, fate clic su **[!UICONTROL Crea > Live Copy]**.

   ![Creare una live copy dall’interfaccia di AEM](assets/create_lc2.png)

   Creare una live copy dall’interfaccia di AEM

1. Selezionate la risorsa o la cartella sorgente. Fai clic su **[!UICONTROL Avanti]**.
1. Selezionate la cartella di destinazione. Fai clic su **[!UICONTROL Avanti]**.
1. Fornire titolo e nome. Le risorse non hanno elementi figlio. Quando create una Live Copy di cartelle, potete scegliere di includere o escludere elementi figlio.
1. Selezionate una configurazione di rollout. Fai clic su **[!UICONTROL Crea]**. 

>[!NOTE]
>
>Quando si sposta un&#39;origine o una Live Copy, le relazioni vengono mantenute. Quando una Live Copy viene eliminata, le relazioni vengono rimosse.

## Visualizzare le varie proprietà e gli stati di origine e live copy {#properties}

Potete visualizzare le informazioni e gli stati relativi a MSM della Live Copy, ad esempio relazione, sincronizzazione, rollout e molto altro dalle varie aree dell&#39;interfaccia utente di AEM.

Per risorse e cartelle funzionano i due metodi seguenti:

* Selezionate la risorsa Live Copy e cercate le informazioni nella relativa pagina Proprietà.
* Seleziona la cartella di origine e trova le informazioni dettagliate di ogni live copy dalla Live Copy Console.

**Suggerimento**: Per verificare lo stato di alcune Live Copy separate, utilizzate il primo metodo che consiste nella visualizzazione della pagina Proprietà. Per verificare lo stato di molte copie live, utilizzare il secondo metodo, ovvero vedere la pagina Stato **** relazione.

### Informazioni e stato di una Live Copy {#statuslcasset}

Per verificare le informazioni e gli stati di una risorsa Live Copy o di una cartella, effettuate le seguenti operazioni.

1. Selezionate una risorsa Live Copy o una cartella. Click **[!UICONTROL Properties]** from the toolbar. In alternativa, utilizzare la scelta rapida da tastiera `p`.
1. Fate clic su **[!UICONTROL Live Copy]**. Potete controllare il percorso dell&#39;origine, lo stato di sospensione, lo stato di sincronizzazione, l&#39;ultima data di rollout e l&#39;utente che ha eseguito l&#39;ultimo rollout.

   ![Le informazioni e gli stati della Live Copy vengono visualizzati in una console in Proprietà](assets/lcfolder_info_properties.png)

   Informazioni e stati Live Copy

1. Potete attivare o disattivare se le risorse secondarie prendono in prestito la configurazione della Live Copy.

1. Potete scegliere l&#39;opzione per la Live Copy per ereditare la configurazione di rollout dall&#39;elemento padre o modificare la configurazione.

### Informazioni e stati di tutte le copie in diretta di una cartella {#statuslcfolder}

In AEM è disponibile una console per controllare le statue di tutte le copie in diretta di una cartella sorgente. In questa console viene visualizzato lo stato di tutte le risorse figlio.

1. Selezionate una cartella sorgente. Click **[!UICONTROL Properties]** from the toolbar. In alternativa, utilizzare la scelta rapida da tastiera `p`.
1. Fate clic su Origine **** Live Copy. Per aprire la console, fate clic su Panoramica **[!UICONTROL Live Copy]**. Questo dashboard fornisce uno stato di livello principale per tutte le risorse secondarie.

   ![Visualizzare gli stati delle copie in diretta nella console Live Copy di origine](assets/livecopy_statuses.png)

   Visualizzare gli stati delle copie in diretta nella console Live Copy di origine

1. Per visualizzare le informazioni dettagliate su ciascuna risorsa nella cartella Live Copy, selezionate una risorsa e fate clic su Stato **** relazione dalla barra degli strumenti.

   ![Informazioni dettagliate e stato di una risorsa figlia Live Copy in una cartella](assets/livecopy_relationship_status.png)

   Informazioni dettagliate e stato di una risorsa figlia Live Copy in una cartella

**Suggerimento**: È possibile visualizzare rapidamente gli stati delle Live Copy di altre cartelle senza dover consultare troppo. È sufficiente cambiare la cartella nell&#39;elenco a comparsa nella parte superiore centrale dell&#39;interfaccia Panoramica **[!UICONTROL di]** Live Copy.

### Azioni rapide dalla barra laterale Riferimenti per la sorgente {#refrailsource}

Per una risorsa o una cartella sorgente, potete visualizzare le informazioni seguenti ed effettuare le seguenti operazioni direttamente dalla barra laterale Riferimenti:

* Visualizzare i percorsi delle copie dal vivo.
* Aprite o visualizzate una Live Copy specifica nell’interfaccia utente di AEM.
* Sincronizzate gli aggiornamenti con una Live Copy specifica.
* Sospendi relazione o modifica configurazione rollout per una Live Copy specifica.
* Accedete alla console della panoramica Live Copy.

Selezionate la risorsa o la cartella sorgente, aprite la barra a sinistra e fate clic su **[!UICONTROL Riferimenti]**. In alternativa, selezionate una risorsa o una cartella e utilizzate la scelta rapida da tastiera `Alt + 4`.  ![Azioni e informazioni disponibili nella barra laterale Riferimenti per l&#39;origine selezionata](assets/referencerail_source.png)

Azioni e informazioni disponibili nella barra laterale Riferimenti per l&#39;origine selezionata

Per una Live Copy specifica, fate clic su **[!UICONTROL Modifica Live Copy]** per sospendere la relazione o modificare la configurazione del rollout.

![Per una Live Copy specifica, l&#39;opzione per sospendere la relazione o modificare la configurazione del rollout è accessibile dalla barra laterale Riferimenti quando la risorsa di origine è selezionata](assets/referencerail_editlc_options.png)

Sospendere la relazione o modificare la configurazione di rollout di una Live Copy specifica

### Azioni rapide dalla barra laterale Riferimenti per la Live Copy {#refraillc}

Per una risorsa o una cartella Live Copy, potete visualizzare le informazioni seguenti ed effettuare le seguenti operazioni direttamente dalla barra laterale Riferimenti:

* Visualizzare il percorso della relativa origine.
* Aprite o visualizzate una Live Copy specifica nell’interfaccia utente di AEM.
* Implementate gli aggiornamenti.

Selezionate una risorsa o una cartella Live Copy, aprite la barra a sinistra e fate clic su **[!UICONTROL Riferimenti]**. In alternativa, selezionate una risorsa o una cartella e utilizzate la scelta rapida da tastiera `Alt + 4`.  ![Azioni disponibili nella barra laterale Riferimenti per la Live Copy selezionata](assets/referencerail_livecopy.png)

Azioni disponibili nella barra laterale Riferimenti per la Live Copy selezionata

## Propagare le modifiche dall’origine alle Live Copy {#rolloutsync}

Dopo la modifica di un&#39;origine, le modifiche possono essere propagate alle Live Copy tramite un&#39;azione di sincronizzazione o un&#39;azione di rollout. Per comprendere la differenza tra entrambe le azioni, consultare il [glossario](#glossary).

### Azione di rollout {#rollout}

Potete avviare un’azione di rollout dalla risorsa di origine e aggiornare tutte o alcune copie attive selezionate.

1. Selezionate una risorsa Live Copy o una cartella. Click **[!UICONTROL Properties]** from the toolbar. In alternativa, utilizzare la scelta rapida da tastiera `p`.
1. Fate clic su Origine **** Live Copy. Fate clic su **[!UICONTROL Rollout]** nella barra degli strumenti nella parte superiore.

1. Selezionate le Live Copy da aggiornare. Fate clic su **[!UICONTROL Rollout]**.

   Per distribuire gli aggiornamenti apportati alle risorse figlio, selezionate Origine **[!UICONTROL rollout e tutti gli elementi figlio]**.

   ![Distribuire le modifiche di origine a alcune o tutte le copie live](assets/livecopy_rollout_page.png)

   Distribuire le modifiche di origine a alcune o tutte le copie live

>[!NOTE]
>
>Le modifiche apportate in una risorsa di origine vengono distribuite solo alle copie live direttamente correlate. Se una Live Copy viene derivata da un’altra Live Copy, le modifiche non vengono implementate nella Live Copy derivata.

In alternativa, potete avviare un’azione di rollout dalla barra laterale Riferimenti dopo aver selezionato una Live Copy specifica. Per ulteriori informazioni, consultate Azioni [rapide dalla barra laterale Riferimenti per la Live Copy](#refraillc). In questo metodo di rollout, vengono aggiornati solo la Live Copy selezionata e facoltativamente i relativi elementi figlio.

![Rollout delle modifiche dell&#39;origine sulla Live Copy selezionata](assets/livecopy_rollout_dialog.png)

Rollout delle modifiche dell&#39;origine sulla Live Copy selezionata

### Informazioni sull&#39;azione di sincronizzazione {#aboutsync}

Un&#39;azione di sincronizzazione richiama le modifiche da un&#39;origine solo alla Live Copy selezionata. L’azione di sincronizzazione rispetta e mantiene le modifiche locali apportate dopo l’annullamento dell’ereditarietà. Le modifiche locali non vengono sovrascritte e l&#39;ereditarietà annullata non viene ripristinata. Puoi avviare un&#39;azione di sincronizzazione in tre modi.

<table>
 <tbody>
  <tr>
   <th><strong>Posizione nell’interfaccia AEM</strong><br /> </th>
   <th><strong>Quando e perché utilizzare</strong><br /> </th>
   <th><strong>Come utilizzare</strong><br /> </th>
  </tr>
  <tr>
   <td>Barra dei riferimenti</td>
   <td>Sincronizzazione rapida quando la sorgente è già selezionata.<br /> </td>
   <td>Consultate Azioni <a href="#refrailsource">rapide dalla barra laterale Riferimenti per la sorgente</a></td>
  </tr>
  <tr>
   <td>Barra degli strumenti nella pagina Proprietà<br /> </td>
   <td>Avviate una sincronizzazione quando avete già le proprietà Live Copy aperte.<br /> </td>
   <td>Consultate <a href="#synclc">Sincronizzazione di una Live Copy</a></td>
  </tr>
  <tr>
   <td>Console Panoramica Live Copy</td>
   <td>Sincronizzate rapidamente più risorse (non necessariamente tutte) quando la cartella sorgente è selezionata o la console Panoramica Live Copy è già aperta. L’azione di sincronizzazione viene avviata per una risorsa alla volta, ma rappresenta un modo più rapido per eseguire la sincronizzazione per più risorse contemporaneamente.<br /> </td>
   <td>Consultate <a href="#bulkactions">Azioni su più risorse in una cartella Live Copy</a></td>
  </tr>
 </tbody>
</table>

### Sincronizzazione di una Live Copy {#synclc}

Per avviare un&#39;azione di sincronizzazione, aprite la pagina **[!UICONTROL Proprietà]** di una Live Copy, fate clic su **[!UICONTROL Live Copy]** e fate clic sull&#39;azione desiderata dalla barra degli strumenti.

Per visualizzare gli stati e le informazioni relativi a un&#39;azione di sincronizzazione, consulta [Informazioni e stato di una Live Copy](#statuslcasset) , [Informazioni e stati di tutte le Live Copy di una cartella](#statuslcfolder).

![L’azione di sincronizzazione richiama le modifiche apportate all’origine](assets/livecopy_sync.png)

L’azione di sincronizzazione richiama le modifiche apportate all’origine

>[!NOTE]
>
>Se la relazione è sospesa, l’azione di sincronizzazione non è disponibile nella barra degli strumenti. Mentre l’azione di sincronizzazione è disponibile nella barra laterale Riferimenti, le modifiche non vengono propagate nemmeno dopo l’implementazione corretta.

## Sospendi e riprendi relazione {#suspendresume}

Potete sospendere temporaneamente la relazione per impedire a una Live Copy di ricevere le modifiche apportate alla risorsa o alla cartella di origine. È inoltre possibile riprendere la relazione affinché la Live Copy inizi a ricevere le modifiche dall&#39;origine.

Per sospendere o riprendere, aprite la pagina **[!UICONTROL Proprietà]** di una Live Copy, fate clic su **[!UICONTROL Live Copy]** e fate clic sull’azione desiderata dalla barra degli strumenti.

In alternativa, potete sospendere o riprendere rapidamente le relazioni di più risorse in una cartella Live Copy dalla console Panoramica **[!UICONTROL di]** Live Copy. Consultate [Azioni su molte risorse presenti nelle cartelle](#bulkactions)Live Copy.

## Apportate modifiche locali a una Live Copy {#localmods}

Una Live Copy è una replica dell&#39;origine originale al momento della creazione. I valori dei metadati di una Live Copy vengono ereditati dall&#39;origine. I campi di metadati mantengono l’ereditarietà singolarmente con i rispettivi campi della risorsa sorgente.

Tuttavia, potete apportare modifiche locali a una Live Copy per modificare alcune proprietà selezionate. Per apportare modifiche locali, annullare l’ereditarietà della proprietà desiderata. Quando l’ereditarietà di uno o più campi di metadati viene annullata, la relazione in tempo reale della risorsa e l’ereditarietà degli altri campi di metadati vengono mantenute. Qualsiasi sincronizzazione o implementazione non sovrascrive le modifiche locali. Per farlo, aprite la pagina **[!UICONTROL Proprietà]** di una risorsa Live Copy, fate clic sull&#39;icona **[!UICONTROL Annulla ereditarietà]** accanto a un campo di metadati.

Potete annullare tutte le modifiche locali e ripristinare lo stato della risorsa all’origine. L’azione Reimposta sostituisce in modo irrevocabile e immediato tutte le modifiche locali e ripristina l’ereditarietà in tutti i campi di metadati. Per ripristinare, dalla pagina **[!UICONTROL Proprietà]** di una risorsa Live Copy, fate clic su **[!UICONTROL Ripristina]** nella barra degli strumenti.

![L’azione Reimposta sovrascrive le modifiche locali e inserisce la Live Copy nella relativa origine.](assets/livecopy_reset.png)

L’azione Reimposta sovrascrive le modifiche locali e inserisce la Live Copy nella relativa origine.

## Rimuovi relazione diretta {#detach}

È possibile rimuovere completamente la relazione tra un&#39;origine e una Live Copy utilizzando l&#39;azione Scollega. Una volta scollegata, la live copy diventa una risorsa o una cartella autonoma. Viene visualizzata come nuova risorsa nell’interfaccia di AEM, subito dopo lo scollegamento. Per scollegare una Live Copy dall&#39;origine, attenetevi alla seguente procedura.

1. Selezionate una risorsa o una cartella Live Copy. Click **[!UICONTROL Properties]** from the toolbar. In alternativa, utilizzare la scelta rapida da tastiera `p`.

1. Fate clic su **[!UICONTROL Live Copy]**. Fare clic su **[!UICONTROL Scollega]** nella barra degli strumenti. Fate clic su **[!UICONTROL Scollega]** dalla finestra di dialogo visualizzata.

   ![L&#39;azione Scollega rimuove completamente la relazione tra sorgente e live copy](assets/livecopy_detach.png)

   L&#39;azione Scollega rimuove completamente la relazione tra sorgente e live copy

   >[!CAUTION]
   >
   >La relazione viene rimossa immediatamente quando si fa clic su **[!UICONTROL Scollega]** dalla finestra di dialogo. Non è possibile annullare l’operazione facendo clic su **[!UICONTROL Annulla]** nella pagina Proprietà.

In alternativa, potete scollegare rapidamente più risorse in una cartella Live Copy dalla console Panoramica **[!UICONTROL di]** Live Copy. Consultate [Azioni su molte risorse presenti nelle cartelle](#bulkactions)Live Copy.

## Azioni su più risorse in una cartella Live Copy {#bulkactions}

Se in una cartella di Live Copy sono presenti più risorse, l’avvio di azioni su ciascuna risorsa può risultare noioso. Puoi avviare rapidamente le azioni di base su più risorse dalla console Live Copy. I metodi indicati sopra continuano a funzionare per singole risorse.

1. Selezionate una cartella sorgente. Click **[!UICONTROL Properties]** from the toolbar. In alternativa, utilizzare la scelta rapida da tastiera `p`.
1. Fate clic su Origine **** Live Copy. Per aprire la console, fate clic su Panoramica **[!UICONTROL Live Copy]**.

1. In questo dashboard, selezionate una risorsa Live Copy da una cartella Live Copy. Fate clic sulle azioni desiderate nella barra degli strumenti. Le azioni disponibili sono **[!UICONTROL Sincronizza]**, **[!UICONTROL Reimposta]**, **[!UICONTROL Sospendi]** e **[!UICONTROL Scollega]**.

   Potete avviare rapidamente queste azioni su qualsiasi risorsa presente in un numero qualsiasi di cartelle di Live Copy che si trovano in una relazione live con la cartella sorgente selezionata.

   ![Aggiornare facilmente molte risorse nelle cartelle di Live Copy dalla console Panoramica di Live Copy](assets/livecopyconsole_update_many_assets.png)

   Aggiornare facilmente molte risorse nelle cartelle di Live Copy dalla console Panoramica di Live Copy

<!--
## Extend MSM for Assets {#extendapi}

AEM allows you to extend the functionality using the MSM Java APIs. For Assets, the extending works just the same as it works with MSM for Site. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)

* [Create a new synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a new rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)

* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* Blueprint in MSM for Site is called Live Copy source in MSM for Assets.
>* Removing the chapters step in the create site wizard is not supported in MSM for Assets.
>* Configuring MSM locks on page properties (Touch-enabled UI) is not supported in MSM for Assets.

-->

## Impatto delle attività di gestione delle risorse sulle copie live {#manageassets}

Le copie e le origini dal vivo sono risorse o cartelle che possono essere gestite, in una certa misura, come risorse digitali. Alcune attività di gestione delle risorse in AEM hanno un impatto specifico sulle copie live.

* Copiando una Live Copy, viene creata una risorsa Live Copy con la stessa origine della prima live copy.
* Quando si sposta un&#39;origine o la sua Live Copy, la relazione live viene mantenuta.
* L&#39;azione di modifica non funziona per le risorse Live Copy. Se l&#39;origine di una Live Copy è di per sé una Live Copy, l&#39;azione di modifica non funziona.
* L’azione di estrazione non è disponibile per le risorse Live Copy.
* Per la cartella di origine, è disponibile l&#39;opzione per creare le attività di revisione.
* Quando visualizzate l’elenco delle risorse nelle viste a elenco e a colonne, viene visualizzata una risorsa o una cartella Live Copy con il comando Live Copy. Questo consente di identificare facilmente le copie dal vivo in una cartella.

## Confronta MSM per risorse e siti {#comparison}

In più scenari, MSM for Assets corrisponde al comportamento di MSM per la funzionalità Sites. Alcune delle principali differenze da sottolineare sono:

* Blueprint in MSM for Site è denominata origine Live Copy in MSM for Assets.
* In Siti puoi confrontare un modello e la relativa Live Copy, ma non è possibile in Risorse confrontare un’origine con la sua Live Copy.
* Non puoi modificare una Live Copy in Assets.
* I siti in genere hanno elementi figlio, ma le risorse no. L’opzione per includere o escludere elementi figlio non è presente quando si creano copie live di singole risorse.
* La rimozione del passaggio dei capitoli nella procedura guidata di creazione del sito non è supportata in MSM for Assets.
* La configurazione dei blocchi MSM sulle proprietà della pagina (interfaccia touch) non è supportata in MSM for Assets.
* Per MSM for Assets, usa solo la configurazione **[!UICONTROL rollout]** Standard. Le altre configurazioni di rollout non sono disponibili per MSM for Assets.

## Best practices {#bestpractices}

Alcune best practice per MSM sono:

* Pianificate le relazioni padre-figlio dei flussi di risorse e contenuti prima di avviare l&#39;implementazione.
* 

## Limitazioni e problemi noti di MSM per Assets {#limitations}

Di seguito è riportata una limitazione di MSM per Assets.

* I frammenti di contenuto (CF) non sono supportati per il caso di utilizzo. Quando tentano di creare le loro copie dal vivo, i CF vengono copiati così come non esiste alcuna relazione. Gli CF copiati sono un&#39;istantanea nel tempo e non si aggiornano quando gli CF originali vengono aggiornati.

