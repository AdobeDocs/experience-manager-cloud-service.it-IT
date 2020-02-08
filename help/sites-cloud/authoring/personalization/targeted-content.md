---
title: Creazione di contenuti di destinazione utilizzando la modalità di targeting
description: La modalità di targeting e il componente Target forniscono strumenti per la creazione di contenuti per esperienze
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Creazione di contenuti di destinazione utilizzando la modalità di targeting {#authoring-targeted-content-using-targeting-mode}

Puoi creare contenuti mirati (di destinazione) utilizzando la modalità di targeting di AEM. La modalità di targeting e il componente Target forniscono strumenti per la creazione di contenuti per esperienze:

* Facile riconoscimento del contenuto di destinazione presente sulla pagina. Tutti i contenuti di destinazione sono contrassegnati da un bordo tratteggiato.
* Selezione di un marchio e un’attività per vedere le esperienze.
* Aggiunta o rimozione di esperienze a un’attività.
* Esecuzione di test A/B e conversione dei vincitori (solo Adobe Target).
* Aggiunta di offerte a un’esperienza creando offerte o utilizzando offerte da una libreria.
* Configurazione di obiettivi e monitoraggio delle prestazioni.
* Simulazione dell’esperienza utente.
* Per ulteriori personalizzazioni, configura il componente Target.

Puoi utilizzare AEM o Adobe Target come motore di targeting (per utilizzare Adobe Target devi disporre di un account Adobe Target valido). Se utilizzi Adobe Target, devi prima di tutto configurare l’integrazione. See the instructions for integrating with Adobe Target. <!--See the[instructions for integrating with Adobe Target](/help/sites-administering/target.md).-->

![Targeting del contenuto](/help/sites-cloud/authoring/assets/targeted-content.png)

The activities and experiences that you see in Target mode reflect the [Activities console](/help/sites-cloud/authoring/personalization/activities.md):

* Le modifiche apportate alle attività e alle esperienze utilizzando la modalità di targeting si riflettono nella console Attività.
* Le modifiche apportate nella console Attività vengono riflesse nella modalità di targeting.

>[!NOTE]
>
>Quando crei una campagna in Adobe Target, questo assegna una proprietà denominata `thirdPartyId` a ogni campagna. Quando elimini la campagna in Adobe Target, thirdPartyId non viene eliminato. Non è possibile riutilizzare `thirdPartyId` per campagne di tipo diverso (AB, XT) e non può essere rimosso manualmente. Per evitare questo problema, assegnate a ciascuna campagna un nome univoco; i nomi delle campagne non possono quindi essere riutilizzati in tipi di campagne diversi.
>
>Se utilizzi lo stesso nome nello stesso tipo di campagna, sovrascriverai la campagna esistente.
>
>Se durante la sincronizzazione si verifica l’errore “Richiesta non riuscita. `thirdPartyId` esiste già”, modifica il nome della campagna ed esegui di nuovo la sincronizzazione.

>[!NOTE]
>
>Nelle operazioni di targeting, la combinazione di branding e attività viene mantenuta a livello di utente non a livello di canale.

## Passaggio alla modalità di targeting {#switching-to-targeting-mode}

Passa alla modalità di targeting per accedere agli strumenti per la creazione di contenuti mirati.

Per passare alla modalità di targeting:

1. Apri la pagina per la quale desideri creare il targeting dei contenuti.
1. Nella barra degli strumenti nella parte superiore della pagina, fare clic o toccare il menu a discesa della modalità per visualizzare i tipi di modalità disponibili.

   ![Modalità di targeting](/help/sites-cloud/authoring/assets/targeted-mode.png)

1. Tocca o fai clic su **Targeting**. Le opzioni di targeting vengono visualizzate nella parte superiore della pagina.

   ![Targeting, barra degli strumenti](/help/sites-cloud/authoring/assets/targeted-toolbar.png)

## Aggiunta di un’attività utilizzando la modalità di targeting {#adding-an-activity-using-targeting-mode}

Utilizza la modalità di targeting per aggiungere un’attività a un marchio. Quando aggiungi un’attività, questa contiene l’esperienza predefinita. Dopo aver aggiunto l’attività, puoi avviare il processo di targeting dei contenuti per l’attività.

Puoi inoltre creare e gestire attività di Adobe Target da AEM con la possibilità di selezionare il motore di targeting, AEM o Adobe Target, e il tipo di attività, targeting delle esperienze o test A/B.

Inoltre, puoi gestire gli obiettivi e le metriche per tutte le attività di Adobe Target e gestire il pubblico di Adobe Target. È incluso anche il reporting delle attività di Adobe Target, tra cui la conversione dei vincitori per i test A/B.

Quando aggiungi un’attività, questa viene visualizzata anche nella [console delle attività](/help/sites-cloud/authoring/personalization/activities.md).

Per aggiungere un’attività:

1. Usa il menu a comparsa **Marchio** per selezionare il marchio per il quale desideri creare l’attività.

   >[!NOTE]
   >
   >Si consiglia di [creare marchi mediante la console delle attività](/help/sites-cloud/authoring/personalization/activities.md#creating-a-brand-using-the-activities-console).
   >
   >
   >If you create a brand in any other way, make certain that the node `/campaigns/<brand>/master` exists or an error will result when you attempt to create an activity.

1. Tocca o fai clic su + accanto al menu a comparsa **Attività**.
1. Digita un nome per l’attività.

   >[!NOTE]
   >
   >Quando crei una nuova attività e disponi di una configurazione cloud di Adobe Target associata alla pagina o a una delle pagine principali, AEM assume automaticamente Adobe Target come motore.

1. Nel menu a comparsa del motore di **targeting**, seleziona il motore di targeting.

   * If you select **ContextHub AEM**, the remaining fields are dimmed and not available. Tocca o fai clic su **Crea**.

   * Se selezioni **Adobe Target**, puoi selezionare una configurazione (per impostazione predefinita, è quella fornita quando hai configurato l’account) e un tipo di attività. <!--If you select **Adobe Target**, you can select a configuration (by default, it is the configuration you provided when you [configured the account](/help/sites-administering/opt-in.md)) and Activity Type.-->

1. Nel menu Attività, seleziona **Targeting delle esperienze** o **Test A/B**.

   * Targeting delle esperienze: gestione delle attività di Adobe Target da AEM.
   * Test A/B: creazione e gestione delle attività di test A/B in Adobe Target da AEM.

## Il processo di targeting: creazione, targeting e obiettivi e impostazioni {#the-targeting-process-create-target-and-goals-settings}

La modalità di targeting consente di configurare diversi aspetti di un’attività. Utilizza il seguente processo in tre fasi per creare contenuti mirati per un’attività del marchio:

1. [Creazione:](#create-authoring-the-experiences) consente di aggiungere o rimuovere le esperienze e di aggiungere le offerte a ogni esperienza.
1. [Targeting:](#target-configuring-the-audiences) consente di specificare i tipi di pubblico al quale è mirata ciascuna esperienza. Puoi eseguire il targeting a un pubblico specifico e, se utilizzi il test A/B decidere quale percentuale di traffico è riservata a quale esperienza.
1. [Obiettivi e impostazioni](#goals-settings-configuring-the-activity-and-setting-goals): consente di programmare l’attività e impostare la priorità. Puoi anche definire gli obiettivi della metrica di successo.

Utilizza la seguente procedura per avviare il processo di targeting dei contenuti di un’attività.

>[!NOTE]
>
>Per utilizzare il processo di targeting, devi essere un membro del gruppo di utenti di Target Activity Authors.

Per aggiungere un’attività:

1. Nel menu a comparsa **Marchio**, seleziona il marchio che contiene l’attività su cui stai lavorando.
1. Nel menu a comparsa **Attività**, seleziona l’attività per la quale stai creando il targeting del contenuto.
1. Per visualizzare i controlli che guidano attraverso il processo di targeting, tocca o fai clic su **Avvia targeting**.

   ![Avvia targeting](/help/sites-cloud/authoring/assets/targeted-start-targeting.png)

   >[!NOTE]
   >
   >Per modificare l’attività con cui stai lavorando, tocca o fai clic su **Indietro**.

## Creazione: creare esperienze {#create-authoring-the-experiences}

La fase di creazione del targeting del contenuto comporta la creazione di esperienze. Durante tale passaggio puoi creare o eliminare le esperienze nell’attività e aggiungere le offerte in ogni esperienza.

### Visualizzazione delle offerte di esperienza in modalità targeting {#seeing-experience-offers-in-targeting-mode}

Dopo aver [avviato il processo di targeting](#the-targeting-process-create-target-and-goals-settings), seleziona un’esperienza per visualizzare le offerte che sono fornite per questa specifica esperienza. Quando selezioni un’esperienza, i componenti soggetti a targeting nella pagina si modificano in modo da mostrare l’offerta per questa esperienza.

>[!CAUTION]
>
>Presta attenzione quando disattivi il targeting per un componente che è già assegnato nell’istanza di authoring. Anche l&#39;attività corrispondente verrà eliminata automaticamente dall&#39;istanza di pubblicazione.

>[!NOTE]
>
>Un’offerta è il contenuto di un componente di cui è stato eseguito il targeting.

Le esperienze sono visualizzate nel riquadro Pubblico. In the following example, experiences include **Default**, **Female**, **Female over 30**, and **Female under 30**. Questo esempio mostra l’offerta predefinita di un componente **immagine** con targeting.

![Componente immagine di destinazione](/help/sites-cloud/authoring/assets/targeted-image-component.png)

Quando è selezionata un’esperienza diversa, il componente immagine mostra l’offerta per l’esperienza.

![Componente immagine di destinazione modificato](/help/sites-cloud/authoring/assets/targeted-image-different.png)

Quando si seleziona un’esperienza e il componente mirato non include un’offerta per tale esperienza, il componente mostra **Aggiungi offerta** sovrapposto all’offerta predefinita semitrasparente. Se non è stata creata alcuna offerta per un’esperienza, viene visualizzata l’offerta **predefinita** per il segmento mappato per l’esperienza.

![Aggiungi offerta](/help/sites-cloud/authoring/assets/targeted-add-offer.png)

L’esperienza predefinita viene visualizzata anche quando le proprietà del visitatore non corrispondono a nessun segmento mappato per le esperienze. See [Adding Experiences using Targeting Mode](#adding-and-removing-experiences-using-targeting-mode).

### Offerte personalizzate e offerte dalla libreria {#custom-offers-and-library-offers}

Le offerte che [vengono create sulla pagina](#adding-a-custom-offer) e vengono utilizzate per una sola esperienza sono denominate offerte personalizzate. L’immagine seguente è sovrapposta al contenuto di un’offerta personalizzata:

![Icona offerta personalizzata](/help/sites-cloud/authoring/assets/targeted-custom-offer-icon.png)

Le offerte che vengono [aggiunte da una libreria di offerte](#adding-an-offer-from-an-offer-library) sono sovrapposte con l’immagine seguente:

![Icona offerta libreria](/help/sites-cloud/authoring/assets/targeted-library-offer-icon.png)

Puoi salvare le offerte personalizzate in una libreria di offerte se decidi di riutilizzarle. Puoi anche convertire un’offerta dalla libreria in un’offerta personalizzata se desideri modificare il contenuto per un’esperienza. Dopo la modifica, puoi salvare nuovamente l’offerta nella libreria.

### Aggiunta e rimozione di esperienze con la modalità di targeting {#adding-and-removing-experiences-using-targeting-mode}

Utilizzando la fase Crea del [processo di targeting](#the-targeting-process-create-target-and-goals-settings), puoi aggiungere e rimuovere esperienze. Inoltre, puoi duplicare un’esperienza e rinominarla.

#### Aggiunta di esperienze con la modalità di targeting {#adding-experiences-using-targeting-mode}

Per aggiungere un’esperienza:

1. To add an experience, click or tap **+** **Add Experience Targeting **that appears below existing experiences in the **Audiences** pane.
1. Seleziona un pubblico. Per impostazione predefinita, questo nome è il nome dell’esperienza. Puoi digitare un altro nome, se necessario. Tocca o fai clic su **OK**.

#### Rimozione di esperienze con la modalità di targeting {#removing-experiences-using-targeting-mode}

Per eliminare un’esperienza:

1. Tocca o fai clic sulla freccia accanto al nome dell&#39;esperienza.

   ![Eliminazione ed esperienza](/help/sites-cloud/authoring/assets/targeted-delete-experiene.png)

1. Fai clic su **Elimina**.

#### Rinominare esperienze con la modalità di targeting {#renaming-experiences-using-targeting-mode}

Per rinominare le esperienze con la modalità di targeting:

1. Tocca o fai clic sulla freccia accanto al nome dell&#39;esperienza.
1. Click **Rename Experience** and type in the new name.
1. Tocca o fai clic su un altro punto dello schermo per salvare le modifiche.

#### Modifica del pubblico utilizzando la modalità di targeting {#editing-audiences-using-targeting-mode}

Per modificare il pubblico utilizzando la modalità di targeting:

1. Tocca o fai clic sulla freccia accanto al nome dell&#39;esperienza.
1. Click **Edit Audience** and select a new audience.
1. Fai clic su **OK**.

#### Duplicazione delle esperienze con la modalità di targeting {#duplicating-experiences-using-targeting-mode}

Per copiare le esperienze con la modalità di targeting:

1. Tocca o fai clic sulla freccia accanto al nome dell&#39;esperienza.
1. Fai clic su **Duplica** e scegli il pubblico.
1. Rinomina l’esperienza, se desiderato, e fai clic su **OK**.

### Creazione delle offerte che utilizzano la modalità di targeting {#creating-offers-using-targeting-mode}

Esegui il targeting di un componente per creare le offerte per le esperienze. I componenti di cui è stato eseguito il targeting forniscono il contenuto che viene utilizzato come offerte per le esperienze.

* [Esegui il targeting di un componente esistente](#creating-a-default-offer-by-targeting-an-existing-component). Il contenuto diventa l’offerta dell’esperienza predefinita.
* [Aggiungi un componente Target](#creating-an-offer-by-adding-a-target-component), quindi aggiungi il contenuto al componente.

Dopo che è stato eseguito il targeting di un componente, puoi aggiungere le offerte per ogni esperienza:

* [Aggiungi offerte personalizzate](#adding-a-custom-offer).
* [Aggiungi offerte da una libreria](#adding-an-offer-from-an-offer-library).

Sono disponibili i seguenti strumenti per lavorare con le offerte:

* [Aggiungi un’offerta personalizzato a una libreria di offerte](#adding-a-custom-offer-to-a-library).
* [Converti un’offerta dalla libreria in offerta personalizzata](#converting-a-library-offer-to-a-custom-library).
* [Apri un’offerta dalla libreria e modificane il contenuto](#editing-a-library-offer).

#### Creazione di un’offerta predefinita tramite targeting di un componente esistente {#creating-a-default-offer-by-targeting-an-existing-component}

Esegui il targeting di un componente sulla pagina per utilizzarlo come l’offerta per l’esperienza predefinita dell’attività. Quando si esegue il targeting di un componente, questo viene inviluppato in un componente Target e il suo contenuto diventa l’offerta per l’esperienza predefinita.

Quando si esegue il targeting di un componente, solo il componente può essere utilizzato nell’offerta. Non è possibile rimuovere il componente dall’offerta o aggiungere altri componenti all’offerta.

Esegui la seguente procedura dopo [aver avviato il processo di targeting](#the-targeting-process-create-target-and-goals-settings).

1. Tocca o fai clic sul componente di cui eseguire il targeting. Viene visualizzata la barra degli strumenti per il componente, come nell’esempio seguente.

   ![Componente di destinazione](/help/sites-cloud/authoring/assets/targeted-component.png)

1. Tocca o fai clic sull’icona Target.

   ![Pulsante Target](/help/sites-cloud/authoring/assets/targeted-target-button.png)

   Il contenuto del componente è l’offerta dell’esperienza predefinita. Quando viene eseguito il targeting di un componente, il suo nodo predefinito sarà replicato per ogni esperienza. Questo è necessario per modificare il nodo del contenuto corretto durante la creazione specifica dell’esperienza. For these non-default experiences, either [add a custom offer](#adding-a-custom-offer) or [add a library offer](#adding-an-offer-from-an-offer-library).

#### Creazione di un’offerta aggiungendo un componente Target {#creating-an-offer-by-adding-a-target-component}

Aggiungi un componente Target per creare l’offerta per l’esperienza predefinita. Il componente Target è un contenitore per altri componenti e viene eseguito il targeting di componenti che si trovano al suo interno. Quando utilizzi il componente Target, puoi aggiungere numerosi componenti per creare un’offerta. Inoltre, puoi usare i diversi componenti in ogni esperienza per creare le diverse offerte.

See [Configuring Target component options](#configuring-target-component-options) for information on customizing this component.

>[!NOTE]
>
>Offers that you create using the [Offers console](/help/sites-cloud/authoring/personalization/offers.md) can also contain several components. Queste offerte appartengono a una libreria di offerte e possono essere utilizzate per più esperienze.

Dato che il componente Target è un contenitore, viene visualizzato come area di rilascio per altri componenti.

In modalità Target, il componente Target ha un bordo blu e il messaggio a discesa indica la natura di targeting.

![Zona di rilascio di Target](/help/sites-cloud/authoring/assets/targeted-drop-target.png)

In modalità di modifica, il componente Target dispone di un’icona a forma di centro del bersaglio.

![Icona della zona di rilascio di destinazione](/help/sites-cloud/authoring/assets/targeted-drop-target-icon.png)

Quando trascini componenti nel componente Target, si tratta di componenti di cui è stato eseguito il targeting.

![Zona di rilascio con destinazioni](/help/sites-cloud/authoring/assets/targeted-drop-zone-populated.png)

Quando aggiungi un componente al componente Target, questo fornisce il contenuto per un’esperienza specifica. Per specificare l’esperienza, seleziona l’esperienza prima di aggiungere i componenti.

È possibile aggiungere un componente Target alla pagina in modalità di modifica o in modalità targeting. Puoi aggiungere componenti al componente Target solo in modalità di targeting. Il componente Target appartiene a un gruppo di componenti di personalizzazione.

Se modificate il contenuto di destinazione, è necessario fare clic o toccare **Avvia targeting **prima di poter eseguire questa operazione.

1. Trascinare il componente Target alla pagina in cui desideri che venga visualizzata l’offerta.
1. Per impostazione predefinita, non è impostato alcun ID di posizione. Tocca o fai clic sull’ingranaggio di configurazione per impostare la posizione.

   >[!NOTE]
   >
   >Se impostato dall’amministratore, potrebbe essere necessario impostare il percorso in modo esplicito.
   >
   >Administrators can decide whether setting this configuration is required at `https://<host>:<port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet`
   >
   >Per richiedere agli utenti di immettere una posizione, seleziona la casella di controllo **Forza posizione**.

1. Seleziona l’esperienza per cui desideri creare l’offerta.
1. Creazione dell’offerta:

   * Per esperienza predefinita, trascinate i componenti nell’area di rilascio di destinazione e modificate le proprietà dei componenti come al solito per creare il contenuto dell’offerta.
   * Per esperienze non predefinite, [aggiungi un’offerta personalizzata](#adding-a-custom-offer) oppure [aggiungi un’offerta dalla libreria](#adding-an-offer-from-an-offer-library).

#### Aggiunta di un’offerta personalizzata {#adding-a-custom-offer}

Consente di realizzare un’offerta creando il contenuto di un componente con targeting per il targeting della modalità. Quando crei un’offerta personalizzata, viene utilizzata come offerta da un’unica esperienza.

If you decide that the offer can be used for other experiences, you can create a custom offer and [add it to the library](#adding-a-custom-offer-to-a-library). Per ulteriori informazioni sull’uso della console delle offerte per creare un’offerta riutilizzabile, consulta [Aggiunta di un’offerta a una libreria di offerte](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library).

1. Seleziona l’esperienza a cui aggiungere l’offerta.
1. Per visualizzare il menu dei componenti, tocca o fai clic sul componente con targeting a cui aggiungere l’offerta.

   ![Aggiunta di un&#39;offerta](/help/sites-cloud/authoring/assets/targeted-component-menu.png)

1. Tocca o fai clic sull’icona +.

   Il contenuto dell’offerta predefinito viene utilizzato come offerta per l’esperienza corrente.

1. Tocca o fai clic sull’offerta per visualizzare il menu dell’offerta, quindi tocca o fai clic sull’icona di modifica.

   ![Barra degli strumenti del componente Target](/help/sites-cloud/authoring/assets/targeted-offer-menu.png)

1. Modifica il contenuto del componente.

#### Aggiunta di un’offerta da una libreria delle offerte {#adding-an-offer-from-an-offer-library}

Add an offer from the [offer library](/help/sites-cloud/authoring/personalization/offers.md) to an experience. Puoi aggiungere tutte le offerte dalla libreria del marchio di cui attualmente stai eseguendo il targeting.

Non puoi aggiungere offerte dalla libreria all’esperienza predefinita.

1. Seleziona l’esperienza a cui aggiungere l’offerta.
1. Per visualizzare il menu dei componenti, tocca o fai clic sul componente con targeting a cui aggiungere l’offerta.

   ![Offerta mirata](/help/sites-cloud/authoring/assets/targeted-add-offer-large.png)

1. Tocca o fai clic sull’icona della cartella.

   ![Icona cartella](/help/sites-cloud/authoring/assets/targeted-folder-button.png)

1. Seleziona l’offerta dalla libreria, quindi tocca o fai clic sull’icona a forma di segno di spunta.

   ![Libreria offerta](/help/sites-cloud/authoring/assets/targeted-select-content.png)

   Il selettore delle offerte consente di individuare o filtrare le offerte. Durante la navigazione o il filtraggio, è anche possibile ordinare le offerte e modificarne la modalità di visualizzazione. Il numero in alto a destra indica il numero di offerte disponibili nella libreria corrente.

   * Click or tap **Browse** to navigate to another folder. Il pannello di navigazione si apre e puoi fare clic sulla freccia per analizzare in profondità le cartelle. Click or tap **Browse** again to close the navigation pane.
   ![Sfoglia contenuto](/help/sites-cloud/authoring/assets/targeted-select-content-browse.png)

   * Tocca o fai clic su **Filtra** per filtrare le offerte in base a parole chiave o tag. Le parole chiave devono essere digitate, mentre i tag possono essere selezionati dal menu a comparsa. Tocca o fai clic di nuovo su **Filtra** per chiudere il pannello di filtraggio.
   ![Filtrare il contenuto](/help/sites-cloud/authoring/assets/targeted-filter.png)

   * Puoi modificare l’ordine delle offerte toccando o facendo clic sulla freccia accanto a **Dal più recente al meno recente**. Le offerte possono essere ordinate dalla più recente alla meno recente o dalla meno recente alla più recente.
   ![Filtra ordinamento](/help/sites-cloud/authoring/assets/targeted-filter-sort.png)

   Tocca o fai clic sull’icona accanto a **Visualizza** per visualizzare le offerte come miniature o come elenco.

   ![Visualizza come pulsante](/help/sites-cloud/authoring/assets/targeted-view-as-button.png)

#### Aggiunta di un’offerta personalizzata a una libreria {#adding-a-custom-offer-to-a-library}

Aggiungi un’offerta personalizzata alla [libreria delle offerte](/help/sites-cloud/authoring/personalization/offers.md) se desideri riutilizzarla come offerta da più esperienze. Puoi aggiungere offerte alla libreria del marchio corrente per i quali stai eseguendo il targeting.

Per ulteriori informazioni sull’uso della console delle offerte per creare un’offerta riutilizzabile, consulta [Aggiunta di un’offerta a una libreria di offerte](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library).

1. Seleziona l’esperienza per visualizzare l’offerta personalizzata.
1. Tocca o fai clic sull’offerta personalizzata per visualizzare il menu dell’offerta, quindi tocca o fai clic sull’icona **Salva offerta nella libreria delle offerte**.

   ![Salva l&#39;offerta nella libreria di offerte](/help/sites-cloud/authoring/assets/targeted-save-offer-library-button.png)

1. Digita un nome per l’offerta e seleziona la libreria a cui aggiungere l’offerta, quindi tocca o fai clic sull’icona a forma di segno di spunta.

#### Convertire un’offerta dalla libreria in una libreria personalizzata {#converting-a-library-offer-to-a-custom-library}

Consente di convertire un’offerta dalla libreria in offerta personalizzata per modificare l’offerta per l’esperienza corrente e senza modificare l’offerta in altre esperienze.

1. Seleziona l’esperienza per visualizzare l’offerta dalla libreria.
1. Tocca o fai clic sull’offerta dalla libreria per visualizzare il menu dell’offerta, quindi tocca o fai clic sull’icona Converti in offerta in linea.

   ![Converti in offerta in linea](/help/sites-cloud/authoring/assets/targeted-convert-inline.png)

#### Modifica dell’offerta dalla libreria {#editing-a-library-offer}

Apri un’offerta dalla libreria da un’esperienza in modalità targeting per modificare l’offerta. Le modifiche apportate vengono visualizzate in tutte le esperienze che utilizzano l’offerta.

1. Seleziona l’esperienza per visualizzare l’offerta dalla libreria.
1. Converti l’offerta dalla libreria in offerta personalizzata/locale. See [Converting a Library Offer to a Custom Library](#converting-a-library-offer-to-a-custom-library).
1. Modifica il contenuto dell’offerta. 

1. Salvalo nuovamente nella libreria. See [Adding a Custom Offer to a Library](#adding-a-custom-offer-to-a-library).

## Targeting: configurazione del pubblico {#target-configuring-the-audiences}

La fase di targeting del [processo di targeting](#the-targeting-process-create-target-and-goals-settings) comporta la mappatura del pubblico con le esperienze con cui hai lavorato nella fase di creazione. La pagina di targeting mostra il pubblico per ogni esperienza di cui stai eseguendo il targeting. Puoi specificare o modificare il pubblico per ogni esperienza. Se utilizzi Adobe Target, puoi anche creare test A/B che consentono di eseguire il targeting della percentuale del traffico per un pubblico per un’esperienza specifica.

### Se utilizzi il targeting AEM o Adobe Target (targeting delle esperienze)… {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Il pubblico viene visualizzato sul lato sinistro del diagramma di mappatura, mentre le esperienze vengono visualizzate sul lato destro.

![Mappatura delle audience](/help/sites-cloud/authoring/assets/targeted-diagram.png)

Definisci un pubblico utilizzando un segmento. La configurazione cloud per la pagina determina i segmenti disponibili. Se la pagina non è associata a una configurazione cloud di Adobe Target, sono disponibili segmenti AEM per la definizione del pubblico. Se la pagina è associata a una configurazione cloud di Adobe Target, utilizza i segmenti Target.

Per informazioni sui motori di targeting, consulta [Motore di targeting](/help/sites-cloud/authoring/personalization/overview.md#targeting-engine).

Un pubblico non deve essere utilizzato da più di un’esperienza. Un simbolo di avviso viene visualizzato accanto a un’esperienza quando viene mappata verso a un pubblico che viene associato a un’altra esperienza.

![Icona di avviso](/help/sites-cloud/authoring/assets/targeted-warn.png)

### Associazione delle esperienze con il pubblico (AEM o Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Segui la procedura seguente per associare un’esperienza a un pubblico quando utilizzi il targeting di AEM (o il targeting delle esperienze di Adobe Target):

1. Tocca o fai clic sulla freccia a discesa nella casella del pubblico mappata all’esperienza.
1. (Optional) Click or tap **Edit** and then type a keyword to search for the desired segment.
1. Nell’elenco del pubblico, seleziona il pubblico e tocca o fai clic su **OK**.

### Se utilizzi i test A/B (Adobe Target)… {#if-you-are-using-a-b-testing-adobe-target}

Se disponi di un’attività di test A/B, il pubblico è alla tua sinistra, la percentuale di visualizzazione di ogni esperienza viene visualizzata è al centro e le esperienze sono a destra.

Le percentuali possono essere modificate fino a un massimo del 100 per cento. Un pubblico può essere utilizzato da più esperienze nei test A/B.

![Targeting A/B](/help/sites-cloud/authoring/assets/targeted-ab.png)

### Associazione di percentuali di pubblico e traffico con il test A/B {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Tocca o fai clic sulla casella a discesa accanto al pubblico mappato all’esperienza.
1. (Facoltativo) Fai clic su **Modifica**, quindi scrivi una parola chiave per la ricerca del segmento desiderato.
1. Tocca o fai clic su **OK.**
1. Immetti le percentuali per configurare il modo in cui il traffico del pubblico viene instradato a ciascuna esperienza. Il numero totale deve essere uguale a 100.
1. (Facoltativo) Modifica il nome dell’esperienza facendo clic sul menu a discesa accanto al nome dell’esperienza.

## Obiettivi e impostazioni: configurazione dell’attività e definizione degli obiettivi {#goals-settings-configuring-the-activity-and-setting-goals}

The Goals &amp; Settings step of [the targeting process](#the-targeting-process-create-target-and-goals-settings) involves configuring the behavior of the brand activity. Specifica quando l’attività inizia e finisce, come anche la priorità dell’attività. Inoltre, è anche possibile monitorare gli obiettivi. In particolare, puoi decidere cosa desideri misurare con le attività.

Le metriche degli obiettivi sono disponibili solo se usi Adobe Target per il motore di targeting. Devi specificare almeno una metrica di obiettivo. Se Adobe Analytics è stato configurato e disponi di una configurazione cloud A4T Analytics, puoi scegliere se l’origine per la generazione dei rapporti deve essere Adobe Target o Adobe Analytics.

Le metriche di obiettivo sono misurate solo per la campagna pubblicata.

Se utilizzi AEM come motore di targeting:

![AEM come motore di destinazione](/help/sites-cloud/authoring/assets/targeted-goals.png)

Se utilizzi Adobe Target come motore di targeting:

![Adobe Target come motore di destinazione](/help/sites-cloud/authoring/assets/targeted-engine.png)

Se utilizzi Adobe Target come motore di targeting e disponi di A4T Analytics configurato per l’account, è disponibile un ulteriore menu a discesa **Origine per la generazione dei rapporti**:

![A4T](/help/sites-cloud/authoring/assets/targeted-source.png)

Sono disponibili le seguenti metriche di successo (utilizzate solo per la pubblicazione):

| Metrica | Descrizione | Opzioni |
|---|---|---|
| Conversione | La percentuale di visitatori che hanno fatto clic su qualsiasi parte dell&#39;esperienza in fase di test. Una conversione può essere conteggiata una volta per ogni visitatore o ogni volta che un visitatore completa una conversione. La metrica di conversione è impostata su uno dei seguenti | Visualizzata una pagina: potete definire la pagina visualizzata selezionando l&#39;URL e quindi definendo l&#39;URL o più URL, oppure selezionando l&#39;URL che contiene e aggiungendo un percorso o una parola chiave. Visualizzata una mbox - Potete definire quale mbox il pubblico ha visualizzato immettendo il nome della mbox. Potete immettere più mbox facendo clic su Aggiungi una mbox. |
| Ricavo | Entrate generate dalla visita. Puoi scegliere tra le metriche delle entrate elencate. Per ciascuna di queste opzioni, se una mbox è stata visualizzata indica che l&#39;obiettivo è stato raggiunto. Puoi definire la mbox o più mbox. | Entrate per visitatore (RPV), Valore ordine medio (AOV), Vendite totali, Ordini |
| Coinvolgimento | Potete misurare tre tipi di coinvolgimento | Visualizzazioni pagina, punteggio personalizzato, Tempo sul sito |

Inoltre, esistono impostazioni avanzate che consentono di determinare come calcolare le metriche di successo. Le opzioni includono il conteggio della metrica per impression o una volta per ogni visitatore e la scelta se mantenere gli utenti nell’attività o rimuoverli.

Utilizza le impostazioni avanzate per determinare che cosa succede **dopo** che l’utente raggiunge la metrica di obiettivo. La tabella seguente mostra le opzioni disponibili.

| Dopo che un utente ha incontrato questa metrica di obiettivo... | Selezionare il seguente evento da eseguire... |
|---|---|
| Incremento conteggio e mantenimento utente nell&#39;attività | Specificate come viene incrementato il conteggio: Una volta per partecipante, Su ogni impressione, ad esclusione degli aggiornamenti di pagina, Su ogni impressione |
| Incremento conteggio, Rilascia utente e Consenti rientro | Selezionate l&#39;esperienza che il visitatore vede se accede nuovamente all&#39;attività: Stessa esperienza, esperienza casuale, esperienza invisibile |
| Incremento conteggio, rilascio utente e rientro a barre | Determinate cosa vede l&#39;utente invece del contenuto dell&#39;attività: Stessa esperienza, senza tracciamento, contenuto predefinito o altro contenuto dell&#39;attività |

Consulta la [documentazione di Adobe Target](https://marketing.adobe.com/resources/help/en_US/target/target/r_success_metrics.html) per ulteriori informazioni sulle metriche di successo.

### Impostazioni di configurazione (targeting di AEM) {#configuring-settings-aem-targeting}

Per configurare le impostazioni utilizzando il targeting di AEM:

1. Per specificare quando avviare l’attività, utilizza il menu a comparsa **Avvia** per selezionare uno dei seguenti valori:

   * **Quando viene attivato**: l’attività viene avviata quando la pagina contenente il contenuto di destinazione viene attivata.
   * **Data e ora specificate**: in un momento specifico. Quando selezioni questa opzione, tocca o fai clic sull’icona del calendario, seleziona una data e specifica l’ora di inizio dell’attività.

1. Per specificare quando l’attività termina, usa il menu a comparsa **Fine** per selezionare uno dei seguenti valori:

   * **Quando viene disattivato**: l’attività termina quando la pagina contenente il contenuto di destinazione viene disattivata.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, tocca o fai clic sull’icona del calendario, seleziona una data e specifica l’ora di fine dell’attività.

1. Per specificare una priorità per l’attività, usa il cursore per selezionare un valore **Bassa**, **Media** o **Alta**.

### Configurazione di obiettivi e impostazioni (Adobe Target) {#configuring-goals-settings-adobe-target}

Per configurare obiettivi e impostazioni con Adobe Target:

1. Per specificare quando avviare l’attività, utilizza il menu a comparsa **Avvia** per selezionare uno dei seguenti valori:

   * **Quando viene attivato**: l’attività viene avviata quando la pagina contenente il contenuto di destinazione viene attivata.
   * **Data e ora specificate**: in un momento specifico. Quando selezioni questa opzione, tocca o fai clic sull’icona del calendario, seleziona una data e specifica l’ora di inizio dell’attività.

1. Per specificare quando l’attività termina, usa il menu a comparsa **Fine** per selezionare uno dei seguenti valori:

   * **Quando viene disattivato**: l’attività termina quando la pagina contenente il contenuto di destinazione viene disattivata.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, tocca o fai clic sull’icona del calendario, seleziona una data e specifica l’ora di fine dell’attività.

1. Per specificare una priorità per l&#39;attività, usa il cursore per selezionare un valore **Basso**, **Medio** o **Alto**.
1. If you have configured Adobe Analytics with your Adobe Target Account, then you see the **Reporting Source** drop-down menu. Seleziona **Adobe Target** o **Adobe Analytics** come origine.

   Se selezioni **Adobe Analytics**, seleziona la società e la suite di rapporti. Se hai selezionato **Adobe Target**, non è necessaria alcuna azione.

   ![Origine reporting](/help/sites-cloud/authoring/assets/targeted-reporting-source.png)

1. Nell’area **Metrica di obiettivo**, nella sezione **Obiettivo principale** seleziona la metrica di successo che desideri monitorare (Conversione, Entrate, Coinvolgimento) e specifica come tale metrica deve essere misurata (o quale azione il pubblico intraprende per indicare che un obiettivo è stato raggiunto). Vedi la definizione delle metriche di obiettivo nella tabella precedente e consulta la [documentazione di Adobe Target](https://marketing.adobe.com/resources/help/en_US/target/target/r_success_metrics.html) sulle metriche di successo.

   Puoi rinominare l’obiettivo facendo clic su i tre punti nell’angolo superiore a destra e selezionando **Rinomina**.

   Se devi cancellare tutti i campi, fai clic sui tre punti nell’angolo in alto a destra e seleziona **Cancella tutti i campi**.

   Tutte le metriche hanno anche impostazioni avanzate che è possibile definire. Seleziona **Impostazioni avanzate** per accedere a queste impostazioni. See definition of how success metrics are counted in previous table and see [Adobe Target documentation](https://marketing.adobe.com/resources/help/en_US/target/target/r_success_metrics.html).

   >[!NOTE]
   >
   >Devi avere almeno un obiettivo definito.

   ![Metrica obiettivo](/help/sites-cloud/authoring/assets/targeted-goal-metric.png)

   >[!NOTE]
   >
   >Se mancano informazioni nella metrica, una linea rossa circonda la metrica.

1. Fai clic su **Aggiungi una nuova metrica** per configurare le metriche di successo aggiuntive.

   ![Metriche aggiuntive](/help/sites-cloud/authoring/assets/targeted-additional-metrics.png)

   >[!NOTE]
   >
   >Puoi rimuovere gli obiettivi aggiuntivi toccando o facendo clic sui tre punti e toccando o facendo clic su **Elimina**. AEM richiede che sia impostata almeno un obiettivo.

1. If you want more control over how success metrics are counted, click or tap **Advanced Settings** to access those.
1. Fai clic su **Salva**.

Dopo la configurazione, puoi [visualizzare le prestazioni delle attività](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test) che utilizzano Adobe Target (sia il targeting di esperienza che del test A/B). Inoltre, con il targeting del test A/B, puoi [convertire i vincitori.](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test) 

## Simulazione dell’esperienza {#simulating-an-experience}

Consente di simulare l’esperienza di un visitatore per verificare che il contenuto della pagina appaia come previsto in base al progetto del contenuto desiderato. Durante la simulazione, carica diversi profili utente e vedi il contenuto con targeting per quell’utente.

I seguenti criteri determinano il contenuto che appare quando si simula l’esperienza di un visitatore:

* I dati nell’archivio di sessione dell’utente (tramite Context Hub).
* Le [attività che sono in corso](/help/sites-cloud/authoring/personalization/activities.md).
* Le [regole che definiscono i segmenti](/help/sites-cloud/authoring/personalization/segmentation.md).
* Il contenuto delle esperienze nel componente Target.
* La [configurazione del motore di targeting](/help/sites-cloud/authoring/personalization/activities.md).

Se nella pagina vengono visualizzati contenuti imprevisti quando si carica un profilo, controlla la configurazione di ogni elemento dell’elenco.

>[!NOTE]
>
>Se utilizzi il test A/B, quando si simulano le esperienze, queste vengono mostrate in base alla percentuale di traffico. Questa funzionalità è controllata da Adobe Target, che può causare risultati imprevisti per gli autori. (L’attività _author è sincronizzata con le impostazioni specifiche che consentono una nuova valutazione durante la simulazione). Gli autori potrebbero dover aggiornare per vedere le altre esperienze in base alle impostazioni del traffico.

Per simulare l’esperienza del visitatore, utilizza i seguenti strumenti:

* L’attività di simulazione in modalità targeting: nella pagina vengono visualizzate le offerte per l’utente attualmente selezionato in Context Hub. È possibile modificare le offerte con targeting per l’utente.
* Modalità anteprima: utilizza Context Hub per selezionare gli utenti e le posizioni che soddisfano i criteri dei segmenti su cui si basa l’esperienza. Quando le selezioni di Context Hub cambiano, i contenuti con targeting cambiano di conseguenza.

1. To switch to Preview mode, on the toolbar click or tap **Preview**.
1. Nella barra degli strumenti, tocca o fai clic sull’icona centrale di Context Hub.

   ![Pulsante ContextHub](/help/sites-cloud/authoring/assets/targeted-contexthub-button.png)

1. Usa Context Hub per modificare le proprietà di contesto. Ad esempio, tocca o fai clic su Proprietà personale per selezionare un utente diverso.

   ![Barra degli strumenti ContextHub](/help/sites-cloud/authoring/assets/targeted-contexthub-toolbar.png)

   La pagina viene modificata per visualizzare il contenuto a cui è destinato il contesto corrente.

1. Per apportare modifiche alle offerte visualizzate, passa alla modalità di targeting. Una volta selezionata l’attività di simulazione, modifica le offerte per il contesto configurato nella modalità di anteprima.

## Configurazione delle opzioni dei componenti Target {#configuring-target-component-options}

È possibile personalizzare il componente Target accedendo alle opzioni del componente in base a uno dei due modi seguenti:

1. Dopo aver eseguito il targeting del componente, nel componente Target tocca o fai clic sul componente, quindi sull’icona delle impostazioni (ingranaggio).

   ![Impostazioni dei componenti](/help/sites-cloud/authoring/assets/targeted-component-settings.png)

   AEM mostra la finestra delle opzioni del componente Target.

   ![Finestra di dialogo Target](/help/sites-cloud/authoring/assets/targeted-dialog.png)

1. In alternativa, per accedere a queste impostazioni in modalità a schermo intero, nella finestra delle opzioni del componente Target, tocca o fai clic sull’icona a schermo intero.

   ![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/targeted-fullscreen.png)

   AEM mostra la finestra delle opzioni del componente Target a schermo intero.

   ![Componente a schermo intero](/help/sites-cloud/authoring/assets/targeted-target-as-enging.png)

1. Configura le impostazioni del componente Target come descritto nelle tabelle seguenti.

| Opzione | Descrizione |
|---|---|
| Dove si trova | La posizione è una stringa che assegna un nome alla posizione del contenuto di destinazione e collega le offerte con i punti (o posizioni o componenti) della pagina in cui tali offerte devono essere inserite. Questo campo è un valore generico. Se inserisci un’offerta in un componente, l’offerta ricorda l’ID della posizione. Quando la pagina viene eseguita, il motore valuta i segmenti dell’utente e in base a questo, risolve le esperienze dalle campagne attive che devono essere visualizzate. Quindi, controlla gli ID di posizione sulla pagina e cerca di far corrispondere le offerte con tali ID. |
| Motore | Scegli tra le regole lato client (senza tracciamento), Adobe Target, ContextHub e Adobe Campaign a seconda del motore da utilizzare. |

Se hai selezionato Adobe Target come motore:

![Target come motore](/help/sites-cloud/authoring/assets/targeted-target-as-enging.png)

| Opzione | Descrizione |
|---|---|
| Impostazione destinazione precisa | L&#39;attivazione di un targeting preciso indica al componente di attendere la disponibilità dei dati contestuali del client o dell&#39;hub di contesto prima di inviare la richiesta ad Adobe Target. Può aumentare il tempo di caricamento. Per la creazione, il targeting accurato è sempre abilitato. Se selezionate la casella di controllo Impostazione destinazione accurata, la mbox esegue una mboxDefine prima e una mboxUpdate più tardi, generando una richiesta Ajax dopo che i dati sono disponibili. Se non selezionate la casella di controllo Impostazione destinazione accurata, la mbox esegue mboxCreate e genera immediatamente una richiesta sincrona (in questo caso, non tutti i dati contestuali potrebbero essere ancora disponibili). Nota: L&#39;attivazione o la disattivazione di un targeting preciso su un componente specifico non influisce sulle impostazioni impostate a livello globale. Puoi sempre ignorare le impostazioni globali selezionando Targeting accurato nel componente. |
| Includi segmenti risolti | La selezione di questa casella di controllo include tutti i segmenti risolti nella chiamata alla mbox ed eventuali parametri configurati nella pagina e nel framework. Questo funziona solo in situazioni con API XML dove stai sincronizzando i segmenti AEM. Se disponi di segmenti in AEM che non vengono gestiti da Adobe Target (come i segmenti di script), questa opzione consente di risolvere il segmento in AEM e segnalare ad Adobe Target che il segmento è attivo. |
| Parametri di contesto ereditati | Elenca gli eventuali parametri contestuali ereditati dal framework di Adobe Target, associati alla pagina selezionata. |
| Param contesto | Tocca o fai clic su Aggiungi campo per configurare parametri di contesto aggiuntivi (come avviene per ciò che è disponibile nel framework di Target). I parametri di contesto aggiunti al componente si applicano solo al componente e non ad altro componente, come accadrebbe se si aggiungessero parametri di contesto direttamente al framework. |
| Param statici | Tocca o fai clic su Aggiungi campo per configurare parametri statici aggiuntivi (come avviene per i parametri disponibili nel framework di Target). I parametri statici aggiunti al componente si applicano solo al componente e non ad altro componente, come accadrebbe se si aggiungessero parametri statici direttamente al framework. I parametri statici non sono contenuti nel contesto (contesto cliente del Content Hub). |

>[!NOTE]
>
>Quando selezioni un componente e lo rendi idoneo per Target, AEM sostituisce anche il componente e integra in un componente di Adobe Target. (Il componente di Adobe Target non viene utilizzato solo quando lo aggiungi manualmente alla pagina, ma anche quando esegui il targeting di un componente esistente).
>
>Seleziona **Adobe Campaign** come motore se stai integrando AEM con Adobe Campaign. Consulta Integrazione di AEM con Adobe Campaign per ulteriori informazioni.
>
>Seleziona **ContextHub** come motore se stai utilizzando ContextHub per il targeting. Consultate Configurazione di ContextHub per ulteriori informazioni.
<!--You select **Adobe Campaign** as the engine if you are integrating AEM with Adobe Campaign. See [Integrating AEM with Adobe Campaign](/help/sites-administering/campaign.md) for more information.-->
<!--Select **ContextHub** as the engine if you are using ContextHub for targeting. See [Configuring ContextHub.](/help/sites-administering/contexthub-config.md)-->
