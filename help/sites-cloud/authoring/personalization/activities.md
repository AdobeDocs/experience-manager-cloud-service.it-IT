---
title: Gestione delle attività
description: La console Attività consente di creare, organizzare e gestire le attività di marketing dei brand
exl-id: e7cab16d-7678-472d-b75f-7f67b303ba8d
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: ht
source-wordcount: '2020'
ht-degree: 100%

---

# Gestione delle attività {#managing-activities}

La console Attività consente di creare, organizzare e gestire le [attività](/help/sites-cloud/authoring/personalization/overview.md#activities) di marketing dei brand, o marchi:

* Aggiungi marchi
* Per ogni marchio puoi aggiungere e configurare delle attività
* Attività di amministrazione

>[!TIP]
>
>Se utilizzi Adobe Target come motore di targeting, puoi [visualizzare anche i dati di prestazione delle attività](#viewing-performance-and-converting-winning-experiences-a-b-test). Se utilizzi il Test A/B, puoi [convertire i vincitori](#viewing-performance-and-converting-winning-experiences-a-b-test).

Nella console Attività, le attività sono organizzate per brand, o marchio. Per strutturare l’organizzazione delle attività, puoi utilizzare marchi e cartelle. Per passare alla console Attività, tocca o fai clic su **Personalizzazione** e quindi su **Attività**.

Le attività sono disponibili in modalità Targeting per la [creazione di contenuti con targeting](/help/sites-cloud/authoring/personalization/targeted-content.md). dove è anche possibile creare attività. Le attività create in modalità Targeting vengono visualizzate nella console Attività.

Le attività vengono visualizzate con un’etichetta che descrive il tipo di attività definito:

* XT: targeting dell’esperienza Adobe Target
* A/B: test A/B di Adobe Target
* AEM: targeting Adobe Experience Manager (ossia basato su ContextHub)

![Tipi di attività](/help/sites-cloud/authoring/assets/activities-types.png)

>[!NOTE]
>
>Il tipo di attività disponibile viene stabilito in base ai seguenti elementi:
>
>* Se l’opzione `xt_only` è abilitata sul tenant di Adobe Target (clientcode) utilizzato sul lato AEM per connettersi ad Adobe Target, puoi creare **solo** attività XT in AEM.
>
>* Se le opzioni `xt_only` **non** sono abilitate nel tenant di Adobe Target (clientcode), puoi creare attività **sia** XT che A/B in AEM.
>
>**Nota aggiuntiva:** l’opzione `xt_only` è un’impostazione applicata a un determinato tenant Target (clientcode) e può essere modificata solo direttamente all’interno di Adobe Target. Non puoi attivare o disattivare questa opzione da AEM.

>[!CAUTION]
>
>È necessario proteggere il nodo delle impostazioni delle attività `cq:ActivitySettings`sull&#39;istanza di pubblicazione in modo che sia inaccessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>Consulta Prerequisiti per l&#39;integrazione con Adobe Target per informazioni dettagliate.
<!--
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.
-->

## Creazione di un marchio tramite la console Attività {#creating-a-brand-using-the-activities-console}

Crea un marchio per il quale desideri gestire le attività di marketing.

Quando crei un marchio utilizzando la console Attività, questa viene visualizzata anche nella [console Offerte](/help/sites-cloud/authoring/personalization/offers.md), dove puoi creare offerte per le esperienze delle tue attività.

1. Nella console Navigazione, tocca o fai clic su **Personalizzazione**. Tocca o fai clic su **Crea**.

   ![Navigazione alle attività](/help/sites-cloud/authoring/assets/activities-navigation.png)

1. Nella console Attività, tocca o fai clic su **Crea**, quindi su **Crea marchio**.
1. Seleziona il modello del marchio e tocca o fai clic su **Avanti**.
1. Digita il titolo da asegnare al marchio; questo titolo verrà visualizzato nelle console Attività e Offerte. Facoltativamente, digita o seleziona uno o più tag da associare al marchio.
1. Tocca o fai clic su **Crea**. Il marchio viene visualizzato nella console Attività.

## Aggiunta o modifica di un’attività tramite la console Attività {#adding-editing-an-activity-using-the-activities-console}

Aggiungi un’attività o modifica un’attività esistente per concentrare le tue attività di marketing su tipi di pubblico specifici. Quando crei o modifichi un’attività, è necessario specificare le seguenti informazioni:

* **Nome:** il nome dell’attività.
* **Motore di destinazione:** [AEM](/help/sites-cloud/authoring/personalization/overview.md#aem) oppure [Adobe Target](/help/sites-cloud/authoring/personalization/overview.md#adobe-target) come motore per il contenuto di destinazione.
* **Seleziona una configurazione di destinazione:** (Solo Adobe Target) la configurazione cloud che questa attività deve utilizzare per connettersi ad Adobe Target. Questa opzione viene visualizzata solo quando è selezionato Adobe Target è per il motore di destinazione.
* **Tipo di attività**: il tipo di attività, test A/B o Impostazione destinazione dell&#39;esperienza
* **Obiettivo:** (facoltativo) una descrizione dell’attività.
* **Esperienze:** mappature tra i nomi del pubblico e i segmenti di marketing di destinazione.
* **Traffic Percentages (Percentuali di traffico):** se è selezionato il test A/B, puoi modificare la quantità di traffico (in percentuale) che viene indirizzato a ogni esperienza.
* **Durata:** il periodo di tempo in cui viene applicata l’attività.
* **Priorità:** la priorità relativa dell’attività. Quando le attività forniscono contenuto per gli stessi segmenti di utenti, l’attività della priorità superiore ha la precedenza.
* **Metrica per obiettivo:** se Adobe Target è selezionato come motore di destinazione, puoi aggiungere all’attività le metriche di successo. È necessaria una metrica di successo.

>[!NOTE]
>
>Per poter **selezionare una configurazione di destinazione** devi essere nel gruppo **Autori attività di Target**.

>[!NOTE]
>
>È necessario *creare* nuove attività di Adobe Target nell’editor del contenuto di destinazione, non nella console **Attività**, in quanto la sincronizzazione con Adobe Target avrà esito negativo.
>
>Tuttavia, puoi modificare le attività Adobe Target esistenti nella console.

Per aggiungere un’attività:

1. Tocca o fai clic sul marchio per il quale stai creando l’attività, quindi tocca o fai clic su **Crea**, quindi su **Crea attività**. Se stai eseguendo una modifica, seleziona l’attività nella schermata Area mastro, quindi fai clic o tocca **Modifica attività**.
1. Fornisci le seguenti informazioni, quindi tocca o fai clic su **Avanti**:
   * Nome dell’attività.
   * Il motore di targeting da utilizzare. ContextHub (AEM) è selezionato per impostazione predefinita. Se devi utilizzare Adobe Target, crea l’attività nell’editor dei contenuti di destinazione.
   * Se hai selezionato Adobe Target come motore di targeting, seleziona o modifica la configurazione cloud da utilizzare per la connessione ad Adobe Target. (non selezionare un framework creato in precedenza per la configurazione cloud).
   * (Facoltativo) Obiettivo o descrizione dell’attività.
   * Seleziona il Tipo di attività.
1. Aggiungi una o più esperienze all’attività. Tocca o fai clic su **Aggiungi esperienza**.
1. Se utilizzi il targeting di AEM o il targgeting esperienze di Adobe Target:
   1. Tocca o fai clic su **Seleziona pubblico** e seleziona il segmento al quale viene eseguito il targeting dell&#39;esperienza.
   1. Tocca o fai clic su **Aggiungi esperienza**, digita un nome e tocca o fai clic su **OK**. 
   1. Tocca o fai clic su **Avanti**.
Se utilizzi Test A/B di Adobe Target:
   1. Tocca o fai clic sulla matita nella casella Tipi di pubblico per selezionare un pubblico.
   1. Tocca o fai clic su **Aggiungi esperienza**, digita un nome e tocca o fai clic su **OK**. 
   1. Inserisci la percentuale di traffico per la quale verrà visualizzata ogni esperienza.
   1. Tocca o fai clic su **Avanti**.
1. Per specificare quando inizia l’attività, utilizza il menu a discesa **Inizio** per selezionare uno dei seguenti valori:
   * **Quando viene attivato:** l’attività si avvia quando viene attivata la pagina con il contenuto di destinazione.
   * **Data e ora specificata:** in un momento specifico. Quando selezioni questa opzione, fai clic o tocca l’icona del calendario, seleziona una data e specifica l’ora in cui avviare l’attività.
1. Per specificare quando termina l’attività, utilizza il menu a discesa Fine per selezionare uno dei seguenti valori:
   * **Quando viene disattivato**: l’attività termina quando viene disattivata la pagina con il contenuto di destinazione.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, tocca o fai clic sull’icona del calendario, seleziona una data e specifica l’ora in cui avviare l’attività.
1. Per specificare una priorità per l’attività, utilizza il cursore per selezionare **Bassa**, **Normale**, o **Alta**.
1. Se utilizzi Adobe Target come motore di targeting, seleziona ciò che desideri misurare con questa attività. Consulta [Configurazione dell&#39;attività e definizione degli obiettivi](/help/sites-cloud/authoring/personalization/targeted-content.md) per ulteriori informazioni sulle metriche di successo disponibili. Seleziona almeno un obiettivo.
1. Tocca o fai clic su **Salva**.

   >[!NOTE]
   >
   >Dopo aver creato un’attività, pubblicala in modo che sia resa disponibile.

## Pubblicazione e annullamento della pubblicazione delle attività {#publishing-and-unpublishing-activities}

È necessario modificare le attività per renderle disponibili. Viceversa, puoi annullarne la pubblicazione per renderle non più disponibili.

>[!NOTE]
>
>Quando si annulla la pubblicazione di un’attività, lo stato dell’attività non cambia a meno che non si aggiorni la pagina.

Per pubblicare o annullare la pubblicazione delle attività:

1. Tocca o fai clic sul marchio e quindi sull’area contenente l’attività da pubblicare o di cui vuoi annullare la pubblicazione.
1. Tocca o fai clic sull’icona accanto all’attività o alle attività da pubblicare o di cui vuoi annullare la pubblicazione.

   ![Pubblicazione dalla console attività](/help/sites-cloud/authoring/assets/activities-console.png)

1. Per pubblicare, tocca o fai clic su **Pubblica**. Per annullare la pubblicazione, tocca o fai clic su **Annulla pubblicazione**. L’attività o le attività vengono pubblicate o ne viene annullata la pubblicazione e il loro stato cambia nella console Attività (potrebbe essere necessario un aggiornamento della schermata).

## Attività sulle istanze di authoring e pubblicazione {#activities-on-author-and-publish-instances}

Quando viene attivata un’attività che utilizza il motore di targeting Adobe Target, viene creata una seconda attività sull’istanza di pubblicazione:

* L’attività sull’istanza di authoring tiene traccia dell’attività su tale istanza ed è utile per simulare l’esperienza del visitatore. L’analisi registrata per questa attività riflette solo ciò che si verifica nell’istanza di authoring.
* L’attività sull’istanza di pubblicazione riflette e risponde all’attività sul server Publish. Questa è l’attività che viene eseguita sul sito web pubblico. Per il tracciamento e l’analisi dell’utilizzo del sito pubblico effettivo, è rilevante solo l’attività sull’istanza di pubblicazione.

## Visualizzazione delle prestazioni e conversione delle esperienze vincenti (test A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Puoi vedere le prestazioni di qualsiasi attività di Adobe Target (XT o A/B). Se utilizzi il test A/B, puoi anche convertire l’esperienza vincente, che diventa quindi l’esperienza predefinita.

Per visualizzare le prestazioni dell&#39;attività e convertire l&#39;esperienza vincente:

1. In **Personalizzazione**, tocca o fai clic su **Attività** per accedere alla console **Attività**.
1. Tocca o fai clic sul marchio di cui desideri visualizzare le attività.
1. Seleziona l’attività e tocca o fai clic su **Visualizza proprietà**, quindi seleziona la scheda **Rapporti** e scegli l’attività per la quale visualizzare le prestazioni o convertire le esperienze vincenti. Vengono visualizzati i dati sulle prestazioni.

   ![Verifica delle prestazioni dell’attività](/help/sites-cloud/authoring/assets/activities-performance.png)

1. Tocca o fai clic sul collegamento **Invia vincitore** per impostare l&#39;esperienza come predefinita.

   La conversione del vincitore comporta le seguenti operazioni:

   * Disattiva l&#39;attività in corso
   * Modifica tutte le pagine e sostituisce il contenuto con targeting con il contenuto effettivo dell&#39;esperienza vincente. Il contenuto dell&#39;esperienza vincente diventa parte della pagina standard **senza** targeting.

   ![Conversione del vincitore](/help/sites-cloud/authoring/assets/activities-reports.png)

   L’esperienza vincente è quella che genera un incremento maggiore nei rapporti, in base al tasso di conversione.

1. Tocca o fai clic su **Sì** per confermare che desideri convertire il vincitore, disabilitando così l’esperienza corrente che viene sostituita dal contenuto dell’esperienza vincente.

## Sincronizzazione delle attività con Adobe Target {#synchronizing-activities-with-adobe-target}

Le attività che utilizzano il motore di targeting di Adobe Target sono sincronizzate con le campagne di Adobe Target. Un’attività viene sincronizzata automaticamente con Adobe Target quando vengono soddisfatte le seguenti condizioni:

* L’attività contiene almeno un’esperienza.
* Almeno un’esperienza contiene un segmento mappato e un’offerta.
* Ogni esperienza nell’attività deve avere lo stesso numero di offerte.

Queste condizioni si applicano alle attività sulle istanze di authoring e di pubblicazione.

Quando un’attività viene sincronizzata, si crea una campagna corrispondente in Adobe Target:

* Le attività sull’istanza di pubblicazione hanno lo stesso nome della campagna Adobe Target corrispondente.
* Le attività sull&#39;istanza autore corrispondono alle campagne Target con lo stesso nome con il suffisso `_author`.

![Integrazione con Adobe Target](/help/sites-cloud/authoring/assets/activities-synch.png)

Le attività author sono sincronizzate immediatamente quando l&#39;attività viene modificata. La sincronizzazione immediata consente la simulazione delle attività con ContextHub.

Le attività di pubblicazione vengono sincronizzate quando sono pubblicate nell’istanza di pubblicazione AEM.

## Risoluzione dei problemi di sincronizzazione dell&#39;attività {#troubleshooting-activity-synchronization}

Quando AEM sincronizza un&#39;attività con Adobe Target, AEM include una proprietà dell&#39;attività denominata `thirdPartyId`. Il valore di questa proprietà è basato sul percorso dell&#39;attività nel repository AEM. Non ci sono due campagne in Adobe Target che possono avere lo stesso valore per la proprietà `thirdPartyId`. Pertanto, un&#39;attività non sarà sincronizzata se una campagna esistente (di tipo diverso AB, XT) in Adobe Target utilizza lo stesso valore per `thirdPartyId`.

Questa situazione può verificarsi nelle seguenti circostanze:

1. Un’attività viene creata e sincronizzata con Adobe Target.
1. In un’altra istanza di AEM viene creata un’attività con lo stesso marchio e lo stesso nome. Il tentativo di sincronizzazione di questa attività non va a buon fine.

Questa situazione può verificarsi anche nelle seguenti circostanze:

1. Un’attività viene creata e sincronizzata con Adobe Target. L’attività viene quindi eliminata in AEM.
1. Un’attività viene creata con lo stesso marchio e lo stesso nome dell’attività eliminata. Il tentativo di sincronizzazione di questa attività non va a buon fine.

Per evitare problemi di sincronizzazione, utilizza sempre nomi univoci per le attività. Se un&#39;attività non viene sincronizzata, puoi eliminare la campagna in Adobe Target che utilizza lo stesso nome se non viene utilizzata.

>[!NOTE]
>
>Quando crei una campagna in Adobe Target, questo assegna una proprietà denominata `thirdPartyId` a ogni campagna. Quando elimini la campagna in Adobe Target, `thirdPartyId` non viene eliminato. Non è possibile riutilizzare `thirdPartyId` per campagne di tipo diverso (AB, XT) e non può essere rimosso manualmente. Per evitare questo problema, rinomina ogni campagna con un nome univoco; i nomi delle campagne non possono quindi essere riutilizzati in diversi tipi di campagne.
>
>Se utilizzi lo stesso nome nello stesso tipo di campagna, sovrascriverai la campagna esistente.
>
>Se durante la sincronizzazione si verifica l’errore “Richiesta non riuscita. `thirdPartyId` esiste già”, modifica il nome della campagna ed esegui di nuovo la sincronizzazione.
