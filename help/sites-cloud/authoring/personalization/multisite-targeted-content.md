---
title: Utilizzo dei contenuti di destinazione in più siti
description: Se devi gestire contenuti mirati, ad esempio attività, esperienze e offerte tra siti diversi, puoi sfruttare il supporto multisito integrato dell’AEM per contenuti mirati
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '2844'
ht-degree: 89%

---

# Utilizzo dei contenuti di destinazione in più siti {#working-with-targeted-content-in-multisites}

Se devi gestire contenuti mirati, ad esempio attività, esperienze e offerte tra siti diversi, puoi sfruttare il supporto multisito integrato dell’AEM per contenuti mirati.

>[!NOTE]
>
>L’utilizzo del supporto multisito per contenuti mirati è una funzione avanzata. Per utilizzare questa funzionalità, è necessario avere dimestichezza con [Multi Site Manager](/help/sites-cloud/administering/msm/overview.md) e [l’integrazione Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) con AEM.

Questo documento descrive quanto segue:

* Fornisce una breve panoramica del supporto multisito AEM per contenuti mirati.
* Descrive alcuni possibili scenari di utilizzo su come collegare i siti (in un unico marchio).
* Fornisce un esempio di progressione di come gli addetti al marketing utilizzeranno questa funzione.
* Istruzioni dettagliate su come implementare il supporto multisito per contenuti mirati.

Per impostare la modalità di condivisione dei contenuti personalizzati da parte dei siti, è necessario effettuare le seguenti operazioni:

1. [Crea una nuova area](#creating-new-areas) o [creare un’area come live copy](#creating-new-areas). Un’area include tutte le attività disponibili per un’*area* della pagina, ovvero la posizione sulla pagina di destinazione del componente. La creazione di una nuova area crea un’area vuota, mentre la creazione di un’area come Live Copy consente di ereditare il contenuto tra le strutture del sito.

1. [Collega il sito o la pagina](#linking-sites-to-an-area) a un’area.

In qualsiasi momento puoi sospendere o ripristinare l’ereditarietà. Inoltre, se non desideri sospendere l’ereditarietà, puoi anche creare esperienze locali. Per impostazione predefinita, tutte le pagine utilizzano l’Area master, a meno che non venga specificato diversamente.

## Introduzione al supporto multisito per contenuti mirati {#introduction-to-multisite-support-for-targeted-content}

Il supporto multisito per contenuti mirati è disponibile come funzionalità predefinita e consente di inviare contenuti mirati dalla pagina master gestita tramite MSM a una Live Copy locale o di gestire modifiche globali e locali di tali contenuti.

È possibile gestirlo in un’**area**. Le aree separano il contenuto di destinazione (attività, esperienze e offerte) utilizzato in siti diversi e forniscono un meccanismo MSM per creare e gestire l’ereditarietà di contenuti di destinazione insieme all’ereditarietà del sito. Questo impedisce la necessità di ricreare contenuti mirati in siti ereditati.

In un’area, solo le attività collegate a tale area vengono inviate alle Live Copy. Per impostazione predefinita, è selezionata l’Area master. Dopo aver creato altre aree, puoi collegarle ai siti o alle pagine per indicare a quale contenuto di destinazione viene inviato.

Un sito o una Live Copy si collega a un’area contenente le attività che devono essere disponibili su tale sito o Live Copy. Per impostazione predefinita, il sito o la Live Copy si collegano all’area master, tuttavia puoi collegare altre aree oltre a quelle.

>[!NOTE]
>
>Quando utilizzi il supporto multisito per contenuti mirati, tieni presente quanto segue:
>
>* Quando utilizzi i rollout o le Live Copy, è necessaria una licenza MSM.
>* Quando si utilizza la sincronizzazione con Adobe Target, è necessaria una licenza di Adobe Target.
>

## Casi di utilizzo {#use-cases}

Puoi impostare il supporto multisito per contenuti mirati in diversi modi, a seconda del caso d’uso. Questa sezione descrive come ciò potrebbe funzionare teoricamente con un marchio. Inoltre, nell’[esempio: targeting del contenuto in base ai dati geografici](#example-targeting-content-based-on-geography), puoi vedere un’applicazione reale di targeting del contenuto multisito.

Il contenuto di destinazione viene racchiuso in cosiddette aree, che definiscono l’ambito dei siti o delle pagine. Queste aree sono definite a livello di marchio. Un marchio può contenere più aree. Le aree possono essere distinte tra i marchi. Anche se un marchio può contenere solo l’area primaria e quindi è condiviso tra tutti i marchi, un altro marchio può contenere più marchi (ad esempio, per regione). I marchi, pertanto, non devono rispecchiare l’insieme delle aree che li separano.

Grazie al supporto multisito per il contenuto di destinazione, è possibile, ad esempio, disporre di due (o più) siti con **un** marchio che presenta una delle caratteristiche seguenti:

* Un insieme completamente *distinto* di contenuti di destinazione: la modifica dei contenuti di destinazione in uno non influisce sull’altro. I siti che rimandano alle aree distinte sono in grado di leggere e scrivere sulla propria area configurata. Esempio:
   * Il sito A si collega all’area X
   * Il sito B si collega all’area Y
* Un insieme *comune* di contenuti di destinazione: la modifica in uno ha un impatto diretto su entrambi i siti; puoi eseguire questa operazione con due siti che fanno riferimento alla stessa area. I siti che si collegano alla stessa area condividono il contenuto di destinazione all’interno di quest’area. Esempio:
   * Il sito A si collega all’area X
   * Il sito B si collega all’area X
* Un set distinto di contenuti mirati *ereditato* da un altro sito tramite MSM: il contenuto può essere implementato in modo unidirezionale dalla pagina master alla Live Copy. Esempio:
   * Il sito A si collega all’area X
   * Il sito B si collega all’area Y (che è una Live Copy dell’area X)

È anche possibile che marchi **multipli** vegano utilizzati in un sito, il che potrebbe essere più complesso di questo esempio.

![Esempio multisito](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Per informazioni tecniche su questa funzione, consulta [Struttura della gestione multisito per contenuti mirati](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Esempio: targeting del contenuto in base alla geografia {#example-targeting-content-based-on-geography}

L’utilizzo di più siti per contenuti mirati consente di condividere, distribuire o isolare i contenuti di personalizzazione. Per illustrare meglio come viene utilizzata questa funzione, considera uno scenario in cui desideri controllare come viene implementato il contenuto di destinazione in base alla geografia, come nello scenario seguente:

Esistono quattro versioni dello stesso sito basate sulla geografia:

* Il sito degli **Stati Uniti** si trova nell’angolo superiore sinistro ed è il sito master. In questo esempio, è aperto in modalità di targeting.
* Le altre tre versioni di questo sito sono **Canada**, **Gran Bretagna**, e **Australia**, che sono tutte Live Copy. Questi siti sono aperti in modalità Anteprima.

![Versioni multisito](/help/sites-cloud/authoring/assets/multisite-versions.png)

Ogni sito condivide contenuti personalizzati in aree geografiche:

* Il Canada condivide l’area master con gli Stati Uniti.
* La Gran Bretagna è collegata all’area europea ed eredita dall’area master.
* L’Australia, poiché si trova nell’emisfero australe e i prodotti stagionali non sarebbero adatti, dispone di un proprio contenuto personalizzato.

![Diagramma multisito](/help/sites-cloud/authoring/assets/multisite-diagram.png)

Per l’emisfero Nord abbiamo creato un’attività invernale, ma nel pubblico maschile l’addetto al marketing in America del Nord vorrebbe un’immagine diversa per l’inverno, perciò la cambia nel sito degli Stati Uniti.

![Versione per Stati Uniti](/help/sites-cloud/authoring/assets/multisite-us.png)

Dopo aver aggiornato la scheda, il sito canadese diventa la nuova immagine senza alcuna azione da parte nostra. Lo fa perché condivide l’area master con gli Stati Uniti. Nei siti di Gran Bretagna e Australia, l’immagine non viene modificata.

![Modifica delle versioni](/help/sites-cloud/authoring/assets/multisite-us-change.png)

L’addetto al marketing desidera introdurre questi cambiamenti nella regione europea ed [esegue il rollout della live copy](/help/sites-cloud/administering/msm/creating-live-copies.md) toccando o facendo clic su **Rollout pagina**. Dopo aver aggiornato la scheda, il sito Gran Bretagna presenta la nuova immagine mentre l’area Europa eredita dall’area master (dopo il rollout).

![Live Copy rollout](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

L’immagine nel sito australiano rimane invariata, che è il comportamento desiderato, poiché è estate in Australia e l’addetto al marketing non desidera modificare tale contenuto. Il sito dell’Australia non cambia perché non condivide un’area con altre regioni né è una Live Copy di un’altra regione. L’addetto al marketing non deve mai preoccuparsi che il contenuto mirato del sito australiano venga sovrascritto.

Inoltre, per la Gran Bretagna, la cui area è una Live Copy dell’area master puoi vedere lo stato di ereditarietà dall’indicatore verde accanto al nome dell’attività. Se un’attività viene ereditata, non puoi modificarla a meno che non sospendi o scolleghi la Live Copy.

In qualsiasi momento, puoi sospendere l’ereditarietà o scollegarla completamente. È inoltre possibile aggiungere sempre esperienze locali disponibili solo per tale esperienza senza sospendere l’ereditarietà.

>[!NOTE]
>
>Per informazioni tecniche su questa funzione, consulta [Struttura della gestione di più siti per contenuti mirati](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Creazione di una nuova area e creazione di una nuova area come Live Copy a confronto {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

In AEM, puoi creare una nuova area o creare una nuova area come Live Copy. La creazione di una nuova area raggruppa le attività e tutto ciò che appartiene a tali attività, ad esempio offerte, esperienze e così via. Puoi creare un’area se desideri creare un set completamente distinto di contenuti di destinazione o se desideri condividere un set di contenuti di destinazione.

Se, tuttavia, l’ereditarietà è impostata tramite MSM tra i due siti, allora potresti voler ereditare le attività. In questo caso, crei un’area come Live Copy, dove Y è una Live Copy di X e quindi eredita anche tutte le attività.

>[!NOTE]
>
>Il rollout predefinito attiva i rollout successivi di contenuti di destinazione ogni volta che una pagina è una Live Copy, attraverso il collegamento a un’area che è una Live Copy dell’area associata alle pagine blueprint.

Ad esempio, nel diagramma seguente, sono disponibili quattro siti in cui due condividono l’area master (e tutte le attività che fanno parte di tale area), un sito ha un’area che è una Live Copy di un’area, quindi condivide le attività dopo il rollout, e un sito è completamente diverso (che quindi richiede un’area per le relative attività).

![Dettaglio del diagramma](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

Per ottenere questo risultato in AEM, effettua le seguenti operazioni:

* Il sito A si collega all’Area master: non è necessaria alcuna creazione di area. L’Area master è selezionata per impostazione predefinita in AEM. I siti A e B condividono le attività e così via.
* Il sito B si collega all’Area master: non è necessaria alcuna creazione di area. L’Area master è selezionata per impostazione predefinita in AEM. I siti A e B condividono le attività e così via.
* Il sito C si collega all’Area ereditata, che è una Live Copy dell’Area master: crea un’Area come Live Copy in cui puoi creare una Live Copy basata sull’Area master. L’Area ereditata eredita le attività dall’Area Master al momento del rollout.
* Il sito D si collega alla propria Area isolata: crea un’Area in cui si crea un’area completamente nuova senza attività ancora definite. L&#39;area isolata non condividerà attività con altri siti.

## Creazione di nuove aree {#creating-new-areas}

Le aree possono estendersi su attività e offerte. Dopo aver creato un’area in una di queste (ad esempio, attività), l’area è disponibile anche nell’altra (ad esempio, offerte).

>[!NOTE]
>
>L’area predefinita denominata Area mastro viene ridotta per impostazione predefinita quando si seleziona il nome di un marchio **fino a** si crea un&#39;altra area. Quindi, quando selezioni un marchio nella console **Attività** o **Offerte**, viene visualizzata la console **Area**.

Per creare un&#39;area:

1. Passa a **Personalizzazione** > **Attività** o **Offerte** per poi, infine, arrivare al tuo marchio.
1. Seleziona **Crea area**.

   ![Crea area](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Fai clic sull’icona **Area** e poi su **Avanti**.
1. Nel campo **Titolo**, immetti un nome per la nuova area. Facoltativamente, seleziona i tag.
1. Seleziona **Crea**.

   AEM reindirizza alla finestra del marchio, dove elenca le aree create. Se è presente un’altra area oltre all’Area Master, puoi creare aree direttamente nella console Marchio.

   ![Creare](/help/sites-cloud/authoring/assets/multisite-create.png)

## Creazione di aree come Live Copy {#creating-areas-as-live-copies}

Crea un’area come Live Copy per ereditare il contenuto di destinazione tra le strutture del sito.

Per creare un’area come Live Copy:

1. Passa a **Personalizzazione** > **Attività** o **Offerte** e infine, al tuo marchio.
1. Seleziona **Crea area come Live Copy**.

   ![Crea area come Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Seleziona l’area di cui desideri effettuare una Live Copy e fai clic su **Avanti**.

   ![Crea Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. Nel campo **Nome**, inserisci un nome per la Live Copy. Per impostazione predefinita, le sottopagine sono incluse, escludile selezionando la casella di controllo **Escludi sottopagine**.

   ![Crea Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. In **Configurazioni di rollout** dal menu a discesa, seleziona la configurazione appropriata.

   Consulta [Configurazioni di rollout installate](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations) per le descrizioni di ciascuna opzione.

   Consulta [Creazione e sincronizzazione di Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md) per ulteriori informazioni sulle live copy.

   >[!NOTE]
   >
   >Quando si effettua il rollout di una pagina su una Live Copy e l’area viene configurata per la pagina del Blueprint, il Blueprint per l’area viene configurato per le Pagine Live Copy, **personalizationContentRollout** attiva un subRollout in sincronia, che fa parte di **Configurazione rollout standard**.

1. Seleziona **Crea**.

   AEM reindirizza alla finestra del marchio, dove elenca le aree create. Se è presente un’altra area oltre all’Area master, è possibile creare aree direttamente dalla finestra del marchio.

   ![Crea area](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Collegamento di siti a un’area {#linking-sites-to-an-area}

È possibile collegare aree a pagine o siti. Le aree vengono ereditate da tutte le sottopagine a meno che non siano sovrascritte da una mappatura su una sottopagina. In genere, tuttavia, crei collegamenti a livello del sito.

Quando esegui un collegamento, sono disponibili solo le attività, le esperienze e le offerte dell’area selezionata. In questo modo si evita il mixup accidentale di contenuti gestiti in modo indipendente. Se non è configurata nessuna altra area, viene utilizzata l’Area master di ciascun marchio.

>[!NOTE]
>
>Le pagine o i siti che fanno riferimento alla stessa area utilizzano *lo stesso* insieme comune delle attività, delle esperienze e delle offerte. La modifica di attività, esperienze o offerte che viene condivisa da più siti agisce su tutti i siti.

Per collegare un sito a un’area:

1. Passa al sito (o alla pagina) che desideri collegare a un’area.
1. Seleziona il sito o la pagina e seleziona **Visualizza proprietà**.
1. Seleziona la **Personalizzazione** scheda.
1. Dal menu **Marchio**, seleziona il marchio a cui desideri collegare l’area. Dopo aver selezionato il marchio, le aree disponibili sono presenti nel menu **Riferimento area**.

   ![Collegamento di siti](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Seleziona l’area dal menu **Riferimento area** menu a discesa e selezionare **Salva**.

   ![Riferimento area](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Scollegare la Live Copy o sospendere l’ereditarietà dei contenuti mirati {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Puoi sospendere o scollegare l’ereditarietà dei contenuti mirati. La sospensione o lo scollegamento della Live Copy viene eseguito per ogni attività. Ad esempio, puoi modificare le esperienze nell’attività, ma se tale attività è ancora collegata alla copia ereditata, non puoi modificare l’esperienza o una qualsiasi delle proprietà dell’attività.

La sospensione della Live Copy interrompe temporaneamente l’ereditarietà, ma in futuro sarà possibile ripristinarla. Lo scollegamento della Live Copy interrompe definitivamente l’ereditarietà.

Sospendi o scolleghi l’ereditarietà dei contenuti di destinazione ristabilendola in un’attività. Se una pagina o un sito si collega a un’area che è una Live Copy, puoi visualizzare lo stato di ereditarietà di un’attività.

Un’attività che eredita da un altro sito è contrassegnata in verde accanto al nome dell’attività. Un’ereditarietà sospesa è contrassegnata in rosso e un’attività creata localmente non ha un’icona.

>[!NOTE]
>
>* Puoi solo sospendere o scollegare le Live Copy in un’attività.
>* Non è necessario sospendere o scollegare le Live Copy per estendere un’attività ereditata. Puoi sempre creare **nuove** esperienze e offerte locali per quell’attività. Se desideri modificare un’attività esistente, devi sospendere l’ereditarietà.
>

### Sospensione dell’ereditarietà {#suspending-inheritance}

Per sospendere o scollegare l’ereditarietà dei contenuti mirati in un’attività:

1. Passa alla pagina in cui desideri scollegare o sospendere l’ereditarietà e seleziona **Targeting** nel menu a discesa mode.
1. Se la pagina è collegata a un’area che è una Live Copy, viene visualizzato lo stato di ereditarietà. Fai clic su **Inizia impostazione destinazione**.
1. Per sospendere un’attività, effettua una delle seguenti operazioni:

   1. Seleziona un elemento dell’attività, ad esempio il pubblico. AEM visualizza automaticamente una casella di conferma Sospendi Live Copy. (Puoi sospendere la Live Copy toccando o facendo clic su qualsiasi elemento durante tutto il processo di targeting).
   1. Dal menu a discesa nella barra degli strumenti, seleziona **Sospendi la Live Copy**.

   ![Sospendi la Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Seleziona **Sospendi** per sospendere l’attività. Le attività sospese sono contrassegnate in rosso.

   ![Live Copy sospesa](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Interruzione dell’ereditarietà {#breaking-inheritance}

Per interrompere l’ereditarietà di contenuti mirati in un’attività:

1. Passa alla pagina in cui desideri scollegare la Live Copy dalla pagina mastro e seleziona **Targeting** nel menu a discesa mode.
1. Se la pagina è collegata a un’area che è una Live Copy, viene visualizzato lo stato di ereditarietà. Fai clic su **Inizia impostazione destinazione**.
1. Dal menu a discesa nella barra degli strumenti, seleziona **Stacca Live Copy**. AEM conferma che vuoi scollegare la Live Copy.
1. Seleziona **Stacca** per scollegare la live copy dall’attività. Una volta scollegata, il menu a discesa relativo all’ereditarietà non viene più visualizzato. L’attività è ora un’attività locale.

   ![Attività locale](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Ripristino dell’ereditarietà del contenuto di destinazione {#restoring-inheritance-of-targeted-content}

Se hai sospeso l’ereditarietà di contenuti di destinazione in un’attività, puoi ripristinarla in qualsiasi momento. Tuttavia, se hai scollegato la Live Copy, non puoi ripristinare l’ereditarietà.

Per ripristinare l’ereditarietà di contenuti di destinazione in un’attività:

1. Passa alla pagina in cui desideri ripristinare l’ereditarietà e seleziona **Targeting** nel menu a discesa mode.
1. Fai clic su **Inizia impostazione destinazione**.
1. Dal menu a discesa nella barra degli strumenti, seleziona **Riprendi Live Copy**.

   ![Ripresa della Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Seleziona **Riprendi** per confermare che desideri riprendere l’ereditarietà della live copy. Se riprendi l’ereditarietà, eventuali modifiche apportate all’attività corrente andranno perse.

## Eliminazione di aree {#deleting-areas}

Quando si elimina un’area, vengono eliminate anche tutte le attività in tale area. AEM ti avvisa prima di poter eliminare un’area. Se elimini un’area a cui è collegato un sito, la mappatura per questo marchio riassocia automaticamente all’area master.

Eliminare un’area:

1. Vai su **Personalizzazione** > **Attività** or **Offerte** e quindi al tuo marchio.
1. Seleziona l’icona accanto all’area da eliminare.
1. Seleziona **Elimina** e confermare che si desidera eliminare l&#39;area.
