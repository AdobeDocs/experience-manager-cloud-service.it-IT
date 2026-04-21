---
title: Lanci per frammenti di contenuto
description: Scopri come utilizzare Launches per frammenti di contenuto in Adobe Experience Manager as a Cloud Service. I lanci consentono di sviluppare in modo efficiente i contenuti per una versione futura, mantenendo al contempo i frammenti di contenuto correnti.
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
badgeSaas: label="AEM Sites" type="Positive" tooltip="Si applica ad AEM Sites)."
exl-id: c0b9e571-3be5-42ab-8d56-d93e8ef4c2f7
source-git-commit: e59faf3943b18fac50d1d504f633ab2ff0236aee
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 2%

---

# Lanci per frammenti di contenuto {#launches-for-content-fragments}

In Adobe Experience Manager (AEM) as a Cloud Service, Launches consente di sviluppare in modo efficiente contenuti per una versione futura.

Viene creato un *lancio* per consentire di apportare modifiche in preparazione alla pubblicazione futura, mantenendo al contempo il contenuto corrente. Per i frammenti di contenuto ciò significa che stai modificando effettivamente due versioni contemporaneamente: il contenuto attualmente pubblicato e una versione di tale contenuto da pubblicare in futuro. Una volta arrivato questo momento, puoi sostituire il contenuto dei frammenti di contenuto originali e pubblicare le nuove versioni.

>[!NOTE]
>
>I lanci sono disponibili anche per le pagine. I concetti di base sono gli stessi, ma esistono differenze nella loro gestione in AEM.
>
>Per informazioni dettagliate, vedere [Lanci per pagine](/help/sites-cloud/authoring/launches/overview.md).

Crea un *lancio*, quindi modifica e aggiorna i frammenti di contenuto nel tuo *lancio*. Se durante questa fase vengono apportate modifiche ai frammenti *Source*, è possibile copiare *Source* (incluse le modifiche) in *Launch* con l&#39;operazione **[Rebase](#rebase-a-launch-from-source)**. Quando è pronto, *Promuovi* duplica il contenuto del lancio all&#39;origine. Puoi quindi attivare i frammenti di origine, manualmente o automaticamente (in base ai campi impostati durante la creazione e la modifica del lancio). Puoi anche specificare se i frammenti di riferimento devono essere inclusi in questo processo.

Ad esempio, i frammenti di prodotto stagionali del tuo negozio online vengono aggiornati trimestralmente in modo che i prodotti in questione siano in linea con la stagione corrente. Per prepararti al prossimo aggiornamento trimestrale, puoi creare un lancio dei frammenti appropriati. Nel corso del trimestre, nella copia del lancio vengono accumulate le seguenti modifiche:

* Modifiche che vengono eseguite direttamente sui frammenti di lancio in preparazione al trimestre successivo.
* Modifiche ai frammenti di contenuto di origine trasferiti alle pagine di lancio con *Rebase*.
* Puoi anche navigare nel contenuto del ramo lancio, aggiungendo o rimuovendo frammenti in base alle esigenze.

Nel trimestre successivo, promuovi le pagine del lancio, in modo da poter pubblicare le pagine sorgente (mantenendo i contenuti aggiornati). Puoi promuovere tutti i frammenti o solo quelli modificati.

![Panoramica sui lanci - Rebase e Promote](/help/sites-cloud/administering/content-fragments/assets/cf-launches-overview.png)

In questa sezione viene descritto come creare, modificare, gestire, ricreare, promuovere e, se necessario, eliminare i lanci dalla [console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md):

* [Accedere e visualizzare i lanci nella console Frammenti di contenuto](#launches-in-the-content-fragment-console)
* [Creare un lancio](#create-a-launch)
* [Modifica contenuto lancio](#edit-launch-content)
* [Gestire i contenuti all’interno di un lancio](#manage-content-within-a-launch)
* [Confronta lancio e origine](#compare-launch-to-source)
* [Ricalcolare un lancio da Source](#rebase-a-launch-from-source)
* [Promuovere un lancio a Source](#promote-a-launch-to-source)
* [Eliminare un lancio](#delete-a-launch)

## Avvii nella console Frammenti di contenuto {#launches-in-the-content-fragment-console}

La scheda **Lanci** della console Frammenti di contenuto consente di creare lanci, di elencare tutti i lanci esistenti, di visualizzare le proprietà chiave e di eseguire azioni su di essi.

Se non è selezionato alcun lancio, puoi [creare un nuovo lancio](#create-a-launch).

![Scheda Lanci nella console](/help/sites-cloud/administering/content-fragments/assets/cf-launches-tab.png)

Seleziona il lancio da mostrare:

* sulla barra degli strumenti, con le azioni disponibili
* il pannello a destra, che mostra le proprietà e ulteriori azioni

![Barra delle azioni di avvio nella console](/help/sites-cloud/administering/content-fragments/assets/cf-launches-actions.png)

La barra degli strumenti consente di:

* **[Apri lancio](#edit-launch-content)**
* **[Modifica origini](#manage-content-within-a-launch)**
* **[Confronta lancio con Source](#compare-launch-to-source)**
* **[Promuovi](#promote-a-launch-to-source)**
* **[Riprendi](#promote-a-launch-to-source)**
* **[Elimina lancio](#delete-a-launch)**

Mentre il pannello a destra consente di:

* Modifica il **titolo** del lancio
* Modifica la **descrizione** del lancio
* Aggiorna i dettagli di configurazione impostati al momento della [creazione del lancio](#create-a-launch):

   * **Includi riferimenti**: crea il lancio con o senza, inclusi eventuali frammenti di contenuto di riferimento. Per impostazione predefinita, sono inclusi i frammenti di riferimento.

      * I frammenti di riferimento sono interessati anche quando [aggiungi o rimuovi frammenti dal lancio](#manage-content-within-a-launch) in una fase successiva.

     >[!NOTE]
     >
     >Vedi [Dettagli relativi ai riferimenti inclusi](#details-concerning-included-references)

   * **Pronto per la pubblicazione**; se si attiva questa opzione, i frammenti verranno pubblicati automaticamente quando il lancio viene promosso all&#39;origine.

* Definisci **Promuovi data** e ora: se il [lancio deve essere promosso automaticamente](#promote-automatically)

* Visualizza ed esegue ulteriori azioni su **[Processi](#jobs-history)** eseguiti (**Confronta lancio con Source**)

## Creare un lancio {#create-a-launch}

Per creare il lancio:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Selezionare **Crea lancio**.

1. Passa alla cartella appropriata e seleziona i frammenti da includere nel lancio:

   ![Seleziona frammenti di contenuto per il nuovo lancio](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-select-cfs.png)

1. Seleziona **Avanti**.

1. Specifica i dettagli per configurare il lancio:

   * **Titolo**
   * **Descrizione**
   * **Includi riferimenti**: crea il lancio con o senza, inclusi eventuali frammenti di contenuto di riferimento. Per impostazione predefinita, sono inclusi i frammenti di riferimento.

     >[!NOTE]
     >
     >Vedi [Dettagli relativi ai riferimenti inclusi](#details-concerning-included-references)

   * **Pronto per la pubblicazione**: se abiliti questa opzione, i frammenti verranno pubblicati automaticamente quando il lancio viene promosso all&#39;origine.

   ![Dettagli per il nuovo lancio](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-launch-details.png)

1. **Salva** la configurazione.

1. Viene visualizzata di nuovo la scheda **Lanci** della console Frammenti di contenuto, in cui:

   * il nuovo lancio è ora elencato
   * viene visualizzato un messaggio per confermare l’avvio della creazione del lancio:

      * **Il processo ha iniziato a creare un nuovo lancio, a monitorare lo stato di avanzamento in AEM e, al termine, a ricaricare la pagina.**

1. Seleziona **Visualizza** dalla finestra del messaggio per visualizzare ulteriori dettagli nella console AEM per [Operazioni in background](/help/operations/asynchronous-jobs.md).

   ![Nuovo avvio nella console](/help/sites-cloud/administering/content-fragments/assets/cf-launches-new-launch-in-console.png)

## Modifica contenuto lancio {#edit-launch-content}

Per modificare i frammenti di contenuto nel lancio:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona il lancio per visualizzare le azioni della barra degli strumenti.

1. Seleziona **Apri lancio**.

   Verrà visualizzato il lancio, insieme ai frammenti che contiene.

   ![Modifica contenuto lancio](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-launch-content.png)

1. Selezionare **Modifica** per il frammento che si desidera aggiornare. Si aprirà nell&#39;[editor frammenti](/help/sites-cloud/administering/content-fragments/authoring.md) come al solito.

## Gestire i contenuti all’interno di un lancio {#manage-content-within-a-launch}

Per gestire i frammenti di contenuto nel lancio e modificarne il contenuto:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona il lancio.

1. Selezionare **Modifica origini**.

   Verranno visualizzati i frammenti di origine del lancio.

   ![Modifica Source](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-sources.png)

1. Operazioni disponibili:

   1. **Aggiungi origini** per aggiungere altri frammenti al lancio.

      * Se **Includi riferimenti** è true per il lancio, anche tutti i frammenti di contenuto di riferimento verranno inseriti nel lancio (se non già presenti).

   1. Selezionare **Modifica** per il frammento di origine che si desidera aggiornare. Si aprirà nell&#39;[editor frammenti](/help/sites-cloud/administering/content-fragments/authoring.md) come al solito.

   1. Seleziona un frammento, quindi l&#39;azione **Elimina origini** dalla barra degli strumenti per rimuovere tale frammento dal lancio.

      * Se **Includi riferimenti** è true per il lancio, anche tutti i frammenti di contenuto di riferimento verranno rimossi dal lancio, a meno che non vi facciano riferimento anche altri frammenti di contenuto ancora presenti nel lancio.

   >[!NOTE]
   >
   >Vedi [Dettagli relativi ai riferimenti inclusi](#details-concerning-included-references)

## Confronta lancio e origine {#compare-launch-to-source}

Prima di eseguire un&#39;azione di **[Rebase](#rebase-a-launch-from-source)** o **[Promote](#promote-a-launch-to-source)**, è consigliabile confrontare sempre l&#39;origine e il lancio per confermare le modifiche e il loro impatto sul contenuto (entrambe le azioni sovrascrivono il contenuto di destinazione):

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona il lancio.

1. Selezionare **Confronta lancio con Source**.

   * I frammenti di origine e di avvio vengono visualizzati affiancati per evidenziare le differenze.
      * I frammenti di Source sono visualizzati a sinistra, i frammenti di Launch a destra.
      * Gli aggiornamenti sono evidenziati:
         * Source: blu
         * Lancio: rosa
         * Conflitti: giallo
   * **Aggiornamenti trovati**: in alto a sinistra viene visualizzato un riepilogo di tutti gli aggiornamenti. Il numero di aggiornamenti sorgente in blu, il numero di aggiornamenti lancio in rosa e gli aggiornamenti a entrambi (conflitti) in giallo.
      * Le icone a forma di occhio consentono di mostrare o nascondere gli aggiornamenti del contenuto effettivo per una panoramica più chiara.
   * I cursori **Includi** consentono di definire i frammenti di contenuto da includere nella successiva operazione di promozione o di riassegnazione:
      * **Includi tutto** in alto a destra
      * **Includi** sopra ogni frammento nel lancio

     >[!NOTE]
     >
     >I cursori si applicano solo alle azioni di promozione e di riassegnazione eseguite dalla schermata Confronta.

   * Il contenuto del frammento viene visualizzato a livello di campo (a livello di elemento Frammento di contenuto/tipo di dati); le evidenziazioni indicano le modifiche.
   * Seleziona **Visualizza** per ricalcolare le differenze.

1. Le azioni [Promuovi](#promote-a-launch-to-source) e [Riprendi](#rebase-a-launch-from-source) sono disponibili in alto a destra.

1. **Indietro** ti riporta alla console. Se desideri rivedere di nuovo queste differenze specifiche, puoi visualizzare le voci **[Processi](#jobs-history)**.

   ![Confronta Source e Launch](/help/sites-cloud/administering/content-fragments/assets/cf-launches-compare.png)

## Cronologia processi {#jobs-history}

Per visualizzare i dettagli degli ultimi **Confronta con processi Source** eseguiti:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona il lancio, viene aperto il pannello informazioni a destra.

1. Nella sezione **Processi** sono presenti **voci launchDifferences** per ciascuno dei **processi di confronto con Source** eseguiti:

   ![Cronologia processi](/help/sites-cloud/administering/content-fragments/assets/cf-launches-jobs.png)

1. Seleziona:

   * Icona della lente di ingrandimento per visualizzare tutti i dettagli relativi a un processo specifico.
Viene restituita la visualizzazione **[Confronta lancio con Source](#compare-launch-to-source)**, con le azioni disponibili.
   * **Visualizza il registro** per visualizzare una panoramica dei dettagli di tutti i processi.
Da qui puoi anche selezionare un processo specifico e quindi visualizzare i **Risultati**. Viene visualizzata di nuovo la visualizzazione **[Confronta lancio con Source](#compare-launch-to-source)**, con le azioni disponibili.

   Entrambe queste azioni ti portano al processo **Confronta lancio con Source** appropriato. Da qui puoi **[Rebase](#rebase-a-launch-from-source)** o **[Promuovere](#promote-a-launch-to-source)** il lancio come era a quel punto.

## Rebase di un lancio (da Source) {#rebase-a-launch-from-source}

Quando sono stati apportati aggiornamenti ai frammenti di origine, è possibile copiare l&#39;origine (incluse le modifiche) nel lancio con l&#39;azione **Rebase**:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona lancio e frammenti.

1. Selezionare **Rebase**.

>[!NOTE]
>
>È inoltre possibile **Rebase** un lancio da **[Confrontare il lancio con Source](#compare-launch-to-source)**.

>[!NOTE]
>
>Prima di eseguire un&#39;azione di **Rebase** o **Promote**, è consigliabile [confrontare l&#39;origine e il lancio](#compare-launch-to-source) per confermare le modifiche e il relativo impatto sul contenuto, in quanto entrambe le azioni sovrascrivono il contenuto di destinazione.

## Promuovi un lancio (a Source) {#promote-a-launch-to-source}

Quando il lancio è pronto per essere pubblicato, deve essere copiato nell’origine. Puoi eseguire questa operazione nella console oppure configurare le impostazioni affinché venga eseguita automaticamente in una data e in un’ora specifiche.

>[!NOTE]
>
>Prima di eseguire un&#39;azione di **Rebase** o **Promote**, è consigliabile [confrontare l&#39;origine e il lancio](#compare-launch-to-source) per confermare le modifiche e il relativo impatto sul contenuto, in quanto entrambe le azioni sovrascrivono il contenuto di destinazione.

### Promuovi manualmente {#promote-manually}

Quando il lancio è pronto per essere pubblicato, può essere copiato nell’origine con l’azione esplicita:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona lancio e frammenti.

1. Seleziona **Promuovi**.

>[!NOTE]
>
>Puoi anche **Promuovere** un lancio da **Confrontare lancio con Source**.

### Promuovi automaticamente {#promote-automatically}

Affinché un lancio possa essere promosso automaticamente a una data e un’ora specificate, è necessario:

1. Definisci **Promuovi data** e ora dal pannello a destra della [scheda Lanci](#launches-in-the-content-fragment-console).

1. Se il contenuto può essere pubblicato quando viene promosso, impostare **Pubblica pronto** quando [si crea il lancio](#create-a-launch) o dal pannello di destra della scheda [Lanci](#launches-in-the-content-fragment-console).

## Eliminare un lancio {#delete-a-launch}

Dopo aver promosso il lancio o deciso di non averne più bisogno, puoi eliminarlo:

1. Passa alla console Frammenti di contenuto.

1. Apri la scheda **Lanci**.

1. Seleziona il lancio.

1. Selezionare **Elimina lancio**.

   Ti viene chiesto di confermare l’azione prima che il lancio venga eliminato.

## Dettagli relativi ai riferimenti inclusi {#details-concerning-included-references}

Per i lanci vengono considerati i seguenti riferimenti ai frammenti di contenuto, a seconda del [tipo di dati](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types):

* Il tipo di dati **Riferimento frammento**, applicabile sia per i riferimenti a frammenti singoli che per i riferimenti a frammenti a più campi.
* Frammenti a cui si fa riferimento all&#39;interno del tipo di dati **Testo su più righe** quando si utilizza **Testo formattato**.

Tutti i punti sono applicabili anche ai frammenti a cui si fa riferimento all’interno delle varianti

Non sono presi in considerazione:

* Frammenti con riferimento all&#39;interno di tipi di dati di riferimento contenuto, sia **Riferimento contenuto** (basato su percorso) che **Riferimento contenuto (UUID)**.
* Frammenti a cui si fa riferimento nel tipo di dati **Riferimento frammento (UUID)**.
