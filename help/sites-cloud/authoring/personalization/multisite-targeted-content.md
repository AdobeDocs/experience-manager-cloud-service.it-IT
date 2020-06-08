---
title: Utilizzo dei contenuti di destinazione in più siti
description: Se devi gestire contenuti di destinazione, ad esempio attività, esperienze e offerte tra i vari siti, è possibile sfruttare il supporto per più siti AEM integrato per il contenuto di destinazione
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '2900'
ht-degree: 87%

---


# Utilizzo dei contenuti di destinazione in più siti {#working-with-targeted-content-in-multisites}

Per gestire i contenuti di destinazione, come le attività, le esperienze e le offerte su più siti, puoi sfruttare il supporto multisito integrato in AEM per i contenuti di destinazione.

>[!NOTE]
>
>Utilizzare il supporto per più siti per il contenuto di destinazione è una funzionalità avanzata. Per utilizzare questa funzione, è necessario avere familiarità con Multi Site Manager e con l&#39;integrazione di Adobe Target con AEM.
<!--
>Working with Multisite support for targeted content is an advanced feature. To use this feature, you should be familiar with [Multi Site Manager](/help/sites-administering/msm.md) and the [Adobe Target integration](/help/sites-administering/target.md) with AEM.
-->

Il presente documento descrive quanto segue:

* Fornisce una breve panoramica del supporto per più siti AEM per il contenuto di destinazione.
* Descrive alcuni possibili scenari di utilizzo su come collegare i siti (in un marchio).
* Fornisce un esempio di progressione di come gli addetti al marketing utilizzeranno questa funzione.
* Istruzioni dettagliate su come implementare il supporto multisito al contenuto di destinazione.

Per impostare come i siti condividono lo stesso contenuto personale, esegui i passaggi seguenti:

1. [Crea una nuova area](#creating-new-areas) o [crea una nuova area come Live Copy](#creating-new-areas). Un’area comprende tutte le attività disponibili per un’*area* di pagina; in altre parole, la posizione della pagina che rappresenta la destinazione del componente. La creazione di una nuova area crea un’area vuota, mentre la creazione di una nuova area come Live Copy consente di ereditare contenuti tra le strutture del sito.

1. [Collega il sito o la pagina](#linking-sites-to-an-area) a un’area.

Puoi sospendere o ripristinare l’ereditarietà in qualsiasi momento. Inoltre, se non desideri sospendere l’ereditarietà, puoi anche creare esperienze locali. Da impostazione predefinita, tutte le pagine utilizzano l’Area master, a meno che non sia specificato diversamente.

## Introduzione al supporto multisito per contenuti di destinazione {#introduction-to-multisite-support-for-targeted-content}

Il supporto multisito per i contenuti di destinazione è disponibile immediatamente e consente di trasferire i contenuti di destinazione dalla pagina maestro gestita tramite MSM a una Live Copy locale o di gestire le modifiche globali e locali di tali contenuti.

You manage this in an **Area**. Le aree separano il contenuto di destinazione (attività, esperienze e offerte) utilizzato in siti diversi e forniscono un meccanismo MSM per creare e gestire l’ereditarietà di contenuti di destinazione insieme all’ereditarietà del sito. In questo modo si impedisce di dover ricreare i contenuti di destinazione in siti ereditati come era richiesto in AEM prima di 6.2.

In un’area, solo le attività associate a tale area vengono inviate a Live Copy. L’Area master è selezionata per impostazione predefinita. Dopo aver creato le aree aggiuntive, puoi collegarle ai siti o le pagine per indicare quale contenuto di destinazione viene indirizzato.

Un sito o una Live Copy collegano a un’area che contiene le attività che devono essere disponibili sul sito o sulla Live Copy. Per impostazione predefinita, il sito o la Live Copy collega i collegamenti all&#39;area master, ma è possibile collegare anche altre aree oltre alle aree master.

>[!NOTE]
>
>Tieni presente quanto segue quando utilizzi un supporto multisito per contenuti di destinazione:
>
>* Quando utilizzi il rollout o le Live Copy è richiesta una licenza MSM.
>* Quando utilizzi la sincronizzazione con Adobe Target è richiesta la licenza per Adobe Target.

>



## Casi di utilizzo {#use-cases}

Puoi installare il supporto multisito per contenuti di destinazione in diversi modi, a seconda del caso. In questa sezione viene descritto il funzionamento teorico di questo supporto con un unico marchio. In addition, in [Example: Targeting Content Based on Geography](#example-targeting-content-based-on-geography), you can see a real-world application of targeting content in multiple sites.

Il contenuto di destinazione è riprodotto ciclicamente nelle cosiddette aree, che definiscono l’ambito per siti o pagine. Queste aree vengono definite a livello di marchio. Un marchio può contenere varie aree. Le aree possono essere diverse tra i marchi. Mentre un marchio può contenere solo l’area master, che di conseguenza è condivisa tra tutti i modelli, un altro marchio può contenere più marchi (ad esempio a seconda della zona). I marchi, pertanto, non devono riflettere l’insieme delle aree tra loro.

Con il supporto multisito per contenuti di destinazione è possibile, ad esempio, definire due (o più) siti con **un** marchio con una delle seguenti caratteristiche:

* Un insieme completamente *distinto* di contenuti di destinazione: la modifica dei contenuti di destinazione in uno non influisce sull’altro. I siti che rimandano alle aree distinte sono in grado di leggere e scrivere sulla propria area configurata. Ad esempio:
   * Il sito A è collegato all’area X
   * Il sito B è collegato all’Area Y
* Un insieme *comune* di contenuti di destinazione: la modifica in uno ha un impatto diretto su entrambi i siti; puoi eseguire questa operazione con due siti che fanno riferimento alla stessa area. I siti che si collegano alla stessa area condividono il contenuto di destinazione all’interno di quest’area. Ad esempio:
   * Il sito A è collegato all’area X
   * Il sito B è collegato all’Area X
* A distinct set of targeted content *inherited* from another site via MSM - Content can be unidirectionally rolled out from master to live copy. Ad esempio:
   * Il sito A è collegato all’area X
   * Il sito B è collegato all’Area Y (che è una Live Copy dell’Area X).

Puoi avere **più** marchi in un sito; la situazione reale potrebbe essere più complessa di quella illustrata in questo esempio.

![Esempio multisito](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>For a more technical look at this feature, see [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Esempio: targeting del contenuto in base all’area geografica {#example-targeting-content-based-on-geography}

L&#39;utilizzo di più siti per contenuti di destinazione consente di condividere, eseguire un rollout o isolare il contenuto della personalizzazione. Per illustrare al meglio come viene utilizzata questa funzione, considera uno scenario in cui desideri controllare il modo in cui è implementato il contenuto di destinazione in base all’area geografica, ad esempio:

Esistono quattro versioni dello stesso sito in base all’area geografica:

* Il sito degli **Stati Uniti** si trova nell’angolo superiore sinistro ed è il sito principale. In questo esempio, viene aperto nella modalità Targeting.
* Le altre tre versioni di questo sito sono del **Canada**, **della Gran Bretagna** e **dell&#39;Australia**, che sono tutte Live Copy. Questi siti vengono aperti nella modalità Anteprima.

![Versioni multisito](/help/sites-cloud/authoring/assets/multisite-versions.png)

Ogni sito condivide contenuto personalizzato nelle aree geografiche:

* Il Canada condivide l’area master con gli Stati Uniti.
* La Gran Bretagna è legata allo spazio europeo ed eredita dalla zona master.
* L’Australia, poiché si trova nell’emisfero australe e i prodotti stagionali non sarebbero adatti, dispone di un proprio contenuto personalizzato.

![Diagramma multisito](/help/sites-cloud/authoring/assets/multisite-diagram.png)

Per l’emisfero Nord abbiamo creato un’attività invernale, ma nel pubblico maschile l’addetto al marketing in America del Nord vorrebbe un’immagine diversa per l’inverno, perciò la cambia nel sito degli Stati Uniti.

![Versione Stati Uniti](/help/sites-cloud/authoring/assets/multisite-us.png)

Dopo l’aggiornamento della scheda, il sito del Canada modifica la nuova immagine senza alcuna azione da parte nostra. Ciò accade perché condivide l’area master con gli Stati Uniti. Nei siti di Gran Bretagna e Australia, l&#39;immagine non cambia.

![Modifica delle versioni](/help/sites-cloud/authoring/assets/multisite-us-change.png)

L’addetto al marketing desidera apportare queste modifiche all’area europea ed effettua un rollout della Live Copy toccando o facendo clic sul **Rollout pagina**. Dopo l’aggiornamento della scheda, il sito della Gran Bretagna ha la nuova immagine mentre l’area dell’Europa eredita dall’area master (dopo il rollout). <!--The marketer would like to roll out these changes to the European region and [rolls out the live copy](/help/sites-administering/msm-livecopy.md) by tapping or clicking **Rollout Page**. After refreshing the tab, the Great Britain site has the new image as the Europe area inherits from the master area (after rollout).-->

![Rollout live copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

L’immagine nel sito dell’Australia rimane nello stato originale, come desiderato, poiché in Australia è estate e l’addetto al marketing non desidera modificare tale contenuto. Il sito dell’Australia non cambia perché non condivide un’area nessun altra regione e non è una Live Copy di un’altra area. L’addetto al marketing non deve mai preoccuparsi che il contenuto di destinazione del sito australiano sia sovrascritto.

Inoltre, per la Gran Bretagna, la cui area è una Live Copy dell’area master, è possibile visualizzare lo stato di ereditarietà dall’indicatore verde accanto al nome dell’attività. Se un’attività è stata ereditata, non puoi modificarla a meno di sospendere o scollegare la Live Copy.

In qualsiasi momento, puoi sospendere l’ereditarietà o scollegarla completamente. Puoi sempre aggiungere anche le esperienze locali che sono disponibili per l’esperienza senza sospendere l’ereditarietà.

>[!NOTE]
>
>For a more technical look at this feature, see [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Creazione di una nuova area e creazione di una nuova area come Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

In AEM hai la possibilità di creare una nuova area o creare nuove aree come Live Copy. La creazione di una nuova area raggruppa le attività e tutto ciò che appartiene a quelle attività, come offerte, esperienze ecc. Crea una nuova area quando desideri creare un insieme completamente distinto del contenuto di destinazione o condividere un insieme di contenuti di destinazione.

Se, tuttavia, hai impostato l’ereditarietà tramite l’MSM tra i due siti, è possibile ereditare le attività. In questo caso, crea una nuova area come Live Copy, in cui Y è una Live Copy di X e pertanto eredita tutte le attività.

>[!NOTE]
>
>Il rollout predefinito attiva i rollout successivi del contenuto di destinazione ogni volta che una pagina è una Live Copy collegata a un&#39;area che è di per sé una Live Copy dell&#39;area collegata al blueprint Pages.

Ad esempio, nel diagramma seguente, sono disponibili quattro siti in cui due condividono l’area master (e tutte le attività che fanno parte di tale area), un sito ha un’area che è una Live Copy di un’area, quindi condivide le attività dopo il rollout, e un sito è completamente diverso (che quindi richiede un’area per le relative attività).

![Dettaglio diagramma](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

Per ottenere questo risultato in AEM, effettua le seguenti operazioni:

* Il sito A si collega all’Area master: non è necessaria la creazione dell’area. L’area principale viene selezionata per impostazione predefinita in AEM. I siti A e B condividono attività ecc.
* Il sito B si collega all’Area master: non è necessaria la creazione dell’area. L’area principale viene selezionata per impostazione predefinita in AEM. I siti A e B condividono attività ecc.
* Il sito C si collega all’Area ereditata, che è una Live Copy dell’Area master: Crea area come Live Copy in cui viene creata una Live Copy in base all’Area master. L’area ereditata eredita le attività dall’Area master dopo il rollout.
* Il sito D si collega alla propria Area isolata: Crea area in cui viene creata una nuova area senza attività ancora definite. L’area isolata non condivide le attività con nessun altro sito.

## Creazione di nuove aree {#creating-new-areas}

Le aree possono misurare attività e offerte. Dopo aver creato un’area in una di esse (ad esempio, attività), avrai a disposizione anche l’area disponibile nell’altra (ad esempio, offerte).

>[!NOTE]
>
>L’area predefinita denominata Area mastro viene ridotta per impostazione predefinita quando tocchi o fai clic sul nome di un marchio **fino** a creare un’altra area. Quindi, quando selezioni un marchio nella console **Attività** o **Offerte**, viene visualizzata la console **Area**.

Per creare una nuova area:

1. Passa a **Personalizzazione** > **Attività** o **Offerte** per poi, infine, arrivare al tuo marchio.
1. Tocca o fai clic su **Crea area**.

   ![Crea area](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Fai clic sull’icona **Area** e fai clic su **Avanti**.
1. Inserisci un nome per la nuova area nel campo **Titolo**. Se desideri, puoi selezionare dei tag.
1. Tocca o fai clic su **Crea**.

   AEM reindirizza alla finestra del marchio, in cui sono elencate tutte le aree che crei. Se è disponibile un’altra area oltre all’Area master, puoi creare aree direttamente nella console Marchio.

   ![Crea](/help/sites-cloud/authoring/assets/multisite-create.png)

## Creazione di aree come Live Copy {#creating-areas-as-live-copies}

Crea un’area come Live Copy per ereditare contenuti di destinazione tramite le strutture del sito.

Per creare un’area come Live Copy:

1. Passa a **Personalizzazione** > **Attività** o **Offerte** e infine, al tuo marchio.
1. Tocca o fai clic su **Crea area come Live Copy**.

   ![Crea area come Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Seleziona l’area di cui desideri effettuare una Live Copy e fai clic su **Avanti**.

   ![Crea live copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. Nel campo **Nome**, inserisci un nome per la Live Copy. Per impostazione predefinita, le sottopagine sono incluse, escludile selezionando la casella di controllo **Escludi sottopagine**.

   ![Crea live copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. Nel menu a discesa **Configurazioni rollout** seleziona la configurazione appropriata.

   Consulta Configurazione di rollout installati per una descrizione di ciascuna opzione. <!--See [Installed Rollout Configurations](/help/sites-administering/msm-sync.md#installed-rollout-configurations) for descriptions of each option.-->

   Consulta Creazione e sincronizzazione di Live Copy per ulteriori informazioni sulle Live Copy. <!--See [Creating and Synchronizing Live Copies](/help/sites-administering/msm-livecopy.md) for more information on live copies.-->

   >[!NOTE]
   >
   >Quando si effettua il rollout di una pagina su una Live Copy e l’area viene configurata per la pagina del Blueprint, il Blueprint per l’area viene configurato per le Pagine Live Copy, **personalizationContentRollout** attiva un subRollout in sincronia, che fa parte di **Configurazione rollout standard**.

1. Tocca o fai clic su **Crea**.

   AEM reindirizza alla finestra del marchio, in cui sono elencate tutte le aree che crei. Se è disponibile un’altra area oltre all’Area master, puoi creare aree direttamente dalla finestra Marchio.

   ![Crea area](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Collegamento dei siti a un’area {#linking-sites-to-an-area}

Puoi collegare le aree a pagine o a un sito. Le aree vengono ereditate da tutte le sottopagine, a meno che tali pagine non siano sovrapposte da una mappatura in una pagina secondaria. In genere, tuttavia, crei collegamenti a livello del sito.

Una volta stabilita la connessione, sono disponibili solo attività, esperienze e offerte dall’area selezionata. In questo modo si evita la confusione accidentale di contenuti gestiti in modo indipendente. Se non è configurata nessun’altra area, viene utilizzata l’area master di ogni marchio.

>[!NOTE]
>
>Pages or sites that reference the same area are using the *same* shared set of activities, experiences, and offers. La modifica di un&#39;attività, un&#39;esperienza o un&#39;offerta condivisa da più siti interessa tutti i siti.

Per collegare un sito a un’area:

1. Accedi al sito (o alla pagina) a cui desideri collegare un’area.
1. Seleziona il sito o la pagina e tocca o fai clic su **Visualizza proprietà**.
1. Tap or click the **Personalization** tab.
1. Nel menu **Marchio**, seleziona il marchio a cui desideri collegare l’area. Dopo aver selezionato il marchio, le aree disponibili sono disponibili nel menu **Riferimento area**.

   ![Collegamento di siti](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Seleziona l’area dal menu a discesa **Riferimento Area** e tocca o fati clic su **Salva**.

   ![Riferimento in area](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Distacco di Live Copy o dissociazione di ereditarietà di contenuti di destinazione.{#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

È possibile sospendere o scollegare l’ereditarietà di contenuti di destinazione. Si sospende o si scollega la Live Copy per attività. Ad esempio, puoi modificare le esperienze nell’attività, ma se l’attività è ancora collegata alla copia ereditata, non è possibile modificare l’esperienza o una qualsiasi delle proprietà dell’attività.

La sospensione di una Live Copy interrompe momentaneamente l’ereditarietà, ma è possibile ripristinare l’ereditarietà successivamente. Il distacco della Live Copy interrompe in modo permanente l’ereditarietà.

Sospendi o scolleghi l’ereditarietà dei contenuti di destinazione ristabilendola in un’attività. Se una pagina o un sito si collega a un’area che è una Live Copy, puoi visualizzare lo stato di ereditarietà di un’attività.

Un’attività che eredita da un altro sito è contrassegnata in verde accanto al nome dell’attività. Un’eredità sospesa è contrassegnata in rosso e un’attività creata localmente non ha alcuna icona.

>[!NOTE]
>
>* Puoi sospendere o scollegare solo le Live Copy in un’attività.
>* Non è necessario sospendere o scollegare le Live Copy per estendere un’attività ereditata. Puoi sempre creare **nuove** esperienze e offerte locali per l’attività. Se desideri modificare un’attività esistente, devi sospendere l’ereditarietà.

>



### Sospensione dell’ereditarietà {#suspending-inheritance}

Sospendere o scollegare ereditarietà di contenuti di destinazione in un’attività:

1. Accedi alla pagina in cui desideri dissociare o sospendere l’ereditarietà e tocca o fai clic su **Targeting** nel menu a discesa della modalità.
1. Se la pagina è collegata a un’area che è una Live Copy, viene visualizzato lo stato di ereditarietà. Tocca o fai clic su **Inizia impostazione destinazione**.
1. Per sospendere su un’attività, effettua una delle seguenti operazioni:

   1. Seleziona un elemento dell’attività, come il pubblico. AEM mostra automaticamente la casella di conferma Sospendi la Live Copy. (Puoi sospendere la Live Copy toccando o facendo clic su un elemento in tutto il processo di Targeting.)
   1. Seleziona **Stacca la Live Copy** dal menu a discesa nella barra degli strumenti.

   ![Sospendi live copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Tap or click **Suspend** to suspend the activity. Le attività sospese sono contrassegnate in rosso.

   ![Live Copy sospesa](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Interruzione dell’ereditarietà {#breaking-inheritance}

Interrompere l’ereditarietà di contenuti di destinazione in un’attività:

1. Accedi alla pagina in cui desideri dissociare la Live Copy dal master e tocca o fai clic su **Targeting** nel menu a discesa della modalità.
1. Se la pagina è collegata a un’area che è una Live Copy, viene visualizzato lo stato di ereditarietà. Tocca o fai clic su **Inizia impostazione destinazione**.
1. Dal menu a discesa nella barra degli strumenti, seleziona **Stacca Live Copy**. AEM conferma che vuoi scollegare la Live Copy.
1. Tocca o fai clic su **Scollega** per scollegare la Live Copy dall’attività. Una volta scollegato, il menu a discesa riguardante le visualizzazioni di ereditarietà non verrà più visualizzato. L’attività è ora un’attività locale.

   ![Attività locale](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Ripristino dell’ereditarietà di contenuti di destinazione {#restoring-inheritance-of-targeted-content}

Se è stata sospesa l’ereditarietà di contenuti di destinazione in un’attività, puoi ripristinarla in qualsiasi momento. Tuttavia, se hai collegato la Live Copy, non puoi ripristinare l’ereditarietà.

Per ripristinare l’ereditarietà di contenuti di destinazione in un’attività:

1. Navigate to the page where you want to restore inheritance and tap or click **Targeting** in the mode drop-down menu.
1. Tocca o fai clic su **Inizia impostazione destinazione**.
1. Dal menu a discesa nella barra degli strumenti, seleziona **Riprendi Live Copy**.

   ![Ripresa della Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Tocca o fai clic su **Ripristina** per confermare che desideri ripristinare l’ereditarietà della Live Copy. Tutte le modifiche apportate all’attività corrente andranno perse se ripristini l’ereditarietà.

## Eliminazione delle aree {#deleting-areas}

Quando elimini un’area, elimini tutte le attività in tale area. AEM ti avvisa prima di poter eliminare un’area. Se si elimina un&#39;area a cui è collegato un sito, la mappatura di questo marchio verrà automaticamente mappata all&#39;area master.

Eliminare un’area:

1. Navigate to **Personalization** > **Activities** or **Offers** and then your brand.
1. Tocca o fai clic sull’icona accanto all’area da cancellare.
1. Tocca o fai clic su **Elimina** e conferma l’eliminazione dell’area.
