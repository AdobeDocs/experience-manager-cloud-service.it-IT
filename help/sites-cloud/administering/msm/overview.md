---
title: Riutilizzo dei contenuti - Multi-Site Manager e Live Copy
description: Ottieni un’introduzione al riutilizzo dei contenuti con AEM potenti Live Copy e le funzioni di Multi Site Manager .
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '2686'
ht-degree: 1%

---


# Riutilizzo del contenuto: Multi-Site Manager e Live Copy {#multi-site-manager-and-live-copy}

Multi Site Manager (MSM) consente di utilizzare lo stesso contenuto del sito in più posizioni. MSM utilizza la funzionalità Live Copy per ottenere questo risultato.

* Con MSM è possibile:
   * Crea contenuto una volta e poi
   * Riutilizza questo contenuto in altre aree (tramite [Live Copy](#live-copies)) dello stesso sito o di altri siti.
* MSM mantiene quindi le relazioni in tempo reale tra il contenuto sorgente e le relative Live Copy in modo che:
   * Quando apporti modifiche al contenuto sorgente, l’origine e le Live Copy vengono sincronizzate.
   * Puoi apportare modifiche solo al contenuto delle Live Copy scollegando la relazione in tempo reale per le singole sottopagine e/o componenti.

Questa pagina fornisce una panoramica del riutilizzo dei contenuti con MSM. Nelle pagine seguenti vengono descritti in dettaglio i problemi correlati.

* [Creazione e sincronizzazione di Live Copy](creating-live-copies.md)
* [Console Panoramica di Live Copy](live-copy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](live-copy-sync-config.md)
* [Conflitti di rollout MSM](rollout-conflicts.md)
* [Best practice MSM](best-practices.md)

## Scenari possibili {#possible-scenarios}

Ci sono molti casi d’uso per MSM e Live Copy. Alcuni scenari includono:

* **Multinazionali - Azienda globale a locale**

   Un caso d’uso tipico supportato da MSM è quello di riutilizzare i contenuti in diversi siti multinazionali nella stessa lingua. Ciò consente di riutilizzare i contenuti principali, consentendo al contempo l’utilizzo di varianti nazionali.

   Ad esempio, per i clienti degli Stati Uniti viene creata la sezione inglese del [campione di esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) . La maggior parte dei contenuti di questo sito può essere utilizzata anche per altri siti WKND che soddisfano clienti di lingua inglese di diversi paesi e culture. Il contenuto principale rimane lo stesso in tutti i siti, mentre è possibile apportare modifiche regionali.

   La seguente struttura può essere utilizzata per i siti per gli Stati Uniti e il Canada. Nota che il nodo `language-masters` mantiene la copia master non solo dell&#39;inglese ma anche di altri contenuti in lingua. Questo contenuto può essere utilizzato come base per contenuti in lingua regionale aggiuntivi insieme all’inglese.

   ```xml
   /content
       |- wknd
           |- language-masters
               |- en
               |- es
               |- fr
           |- us
               |- en
               |- es
           |- ca
               |- en
               |- fr
   ```

   >[!NOTE]
   >
   >MSM non traduce il contenuto. Viene utilizzato per creare la struttura richiesta e distribuire il contenuto.
   >
   >
   >Per un esempio di questo tipo, consulta [Traduzione di contenuti per siti multilingue](/help/sites-cloud/administering/translation/overview.md) .

* **Nazionale - sede principale per le succursali regionali**

   In alternativa, un&#39;azienda con una rete di rivenditori potrebbe volere siti web separati per i suoi singoli concessionari, ognuno dei quali rappresenta una variazione del sito principale fornito dalla sede centrale. Questo potrebbe essere per una singola azienda con più uffici regionali, o un sistema di franchising nazionale composto da un franchisor centrale e da più affiliati locali.

   La sede centrale può fornire le informazioni di base, mentre gli enti regionali possono aggiungere informazioni locali, quali i dati di contatto, gli orari di apertura e gli eventi.

   ```xml
   /content
       |- head-office-berlin
       |- branch-hamburg
       |- branch-stuttgart
       |- branch-munich
       |- branch-frankfurt
   ```

* **Più versioni**

   MSM può creare versioni di un ramo specifico. Ad esempio, un sito secondario di supporto può contenere i dettagli delle diverse versioni di un prodotto specifico, dove le informazioni di base rimangono costanti e devono essere modificate solo le funzioni aggiornate:

   ```xml
   /content
       |- game-support
           |- polybius
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!TIP]
   >
   >In tale scenario, si tratta di stabilire se effettuare una copia diretta o utilizzare Live Copy, il che rappresenta un equilibrio tra:
   >
   >* Quanto contenuto principale deve essere aggiornato su più versioni.
   >
   >Contrari:
   >
   >* Quanto delle singole copie deve essere regolato.


## MSM dall&#39;interfaccia utente {#msm-from-the-ui}

MSM è direttamente accessibile nell’interfaccia utente utilizzando diverse opzioni dalla console appropriata.

* **Crea sito**  (**Sites**)

   * MSM consente di gestire più siti web che condividono contenuti comuni. Ad esempio, i siti web sono spesso disponibili per il pubblico internazionale in modo che la maggior parte dei contenuti sia comune in tutti i paesi, con un sottoinsieme di contenuti specifici per il singolo paese. MSM consente di [creare Live Copy che aggiornano automaticamente uno o più siti in base al sito di origine](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Questo consente anche di applicare una struttura di base comune, utilizzare i contenuti comuni tra più siti, mantenere un aspetto comune e ottimizzare gli sforzi per gestire i contenuti che differiscono effettivamente tra i siti. Creazione di un sito in questo modo:
      * Richiede una configurazione blueprint predefinita per specificare l’origine.
      * Crea una Live Copy della sorgente (predefinita).
      * Fornisce all&#39;utente il pulsante **Rollout** .

* **Crea Live Copy**  (**Sites**)

   * MSM ti consente di [creare una Live Copy ad hoc (una tantum) di una singola pagina o ramo di un sito web.](creating-live-copies.md#creating-a-live-copy-of-a-page) Ad esempio, duplicare un ramo secondario per fornire informazioni su una versione nuova/aggiornata di un prodotto. Creazione di una Live Copy in questo modo:
      * Crea una Live Copy ad-hoc (non è richiesta alcuna configurazione blueprint).
      * Può essere utilizzato per creare (immediatamente) una Live Copy di qualsiasi pagina/ramo.
      * Richiede **Sincronizza** (non fornisce il pulsante **Rollout**).

* **Visualizza proprietà**  (**Sites**)

   * Se appropriato, questa opzione ti aiuta a [monitorare la Live Copy](creating-live-copies.md#monitoring-your-live-copy) fornendo informazioni sulla relativa **Live Copy** o **Blueprint**.

* **Riferimenti**  (**Sites**)

   * La barra [Riferimenti](/help/sites-cloud/authoring/getting-started/basic-handling.md#references) fornisce informazioni su **Live Copy** e sull’accesso alle azioni appropriate.

* **Panoramica di Live Copy**  (**Sites**)

   * Questa console consente di [visualizzare e gestire la blueprint e le relative Live Copy.](live-copy-overview.md)

* **Blueprint**  (**Strumenti**  -  **Sites**)

   * Questa console consente di [creare e gestire le configurazioni di blueprint.](creating-live-copies.md#creating-a-blueprint-configuration)

>[!NOTE]
>
>Aspetti della funzionalità MSM sono utilizzati in diverse altre funzioni AEM come Launch. In questi casi la Live Copy è gestita da tale funzione.

### Termini utilizzati {#terms-used}

Come introduzione, la tabella seguente fornisce una panoramica dei termini principali utilizzati con MSM. Tali informazioni saranno descritte più dettagliatamente nelle sezioni e nelle pagine successive.

| Termine | Definizione | Maggiori dettagli |
|---|---|---|
| Origine | Le pagine originali utilizzate come base per le Live Copy | sinonimo di pagine Blueprint e/o Blueprint |
| Live Copy  | La copia (dell’origine), gestita dalle azioni di sincronizzazione definite dalle configurazioni di rollout |  |
| Configurazione Live Copy | Definizione dei dettagli di configurazione per una Live Copy |  |
| Relazione Live | Definizione effettiva dell’ereditarietà per una determinata risorsa, ovvero le connessioni tra l’origine e Live Copy | Garantisce che le modifiche alla sorgente possano essere sincronizzate con la Live Copy |
| Blueprint | Sinonimo di Sorgente | Può essere definito da una configurazione blueprint |
| Configurazione Blueprint | Configurazione predefinita che specifica un percorso sorgente | Quando si fa riferimento a una pagina blueprint in una configurazione blueprint, il comando Rollout diventa disponibile |
| Capitolo | Le sezioni della blueprint da includere nella Live Copy | Si tratta in genere di sottopagine della radice |
| Sincronizzazione | Termine generico per la sincronizzazione del contenuto tra l&#39;origine e le Live Copy (tramite le opzioni **Rollout** e **Sincronizza**) |  |
| Rollout | Sincronizza dalla sorgente alla Live Copy | Può essere attivato da un autore (in una pagina blueprint) o da un evento di sistema (come definito dalla configurazione di rollout) |
| Configurazione rollout | Regole che determinano le proprietà da sincronizzare, come e quando |  |
| Sincronizza | Una richiesta manuale di sincronizzazione, effettuata dalle pagine Live Copy |  |
| Ereditarietà | Una pagina/componente Live Copy eredita il contenuto dalla pagina/componente sorgente quando si verifica la sincronizzazione |  |
| Sospendi | Rimuove temporaneamente la relazione live tra una Live Copy e la relativa pagina blueprint |  |
| Stacca | Rimuove definitivamente la relazione live tra una Live Copy e la relativa pagina blueprint |  |
| Ripristina | Ripristina una pagina Live Copy per rimuovere tutte le cancellazioni di ereditarietà e ripristinare la pagina sullo stesso stato della pagina sorgente | La reimpostazione influisce su tutte le modifiche apportate alle proprietà della pagina, al sistema di paragrafi e ai componenti. |
| Bassa | Una Live Copy di una singola pagina |  |
| Profondo | Una Live Copy di una pagina, insieme alle relative pagine figlie |  |

<!--
>[!TIP]
>
>See [Overview of the Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) for the object names.
-->

## Live Copy {#live-copies}

Una MSM Live Copy è una copia del contenuto specifico del sito per il quale viene mantenuta una relazione live con la sorgente originale:

* La Live Copy eredita il contenuto dalla relativa sorgente.
* La sincronizzazione esegue il trasferimento effettivo del contenuto quando vengono apportate modifiche all&#39;origine.
* Una Live Copy può essere considerata come:
   * superficiale: una singola pagina
   * Profondo: la pagina, insieme alle relative pagine figlie
* Le regole di sincronizzazione, denominate configurazioni di rollout, determinano le proprietà sincronizzate e quando si verifica la sincronizzazione.

Nell’esempio precedente, `/content/wknd/language-masters/en` è il sito master globale in inglese. Per riutilizzare il contenuto di questo sito, vengono create le Live Copy MSM:

* Il contenuto seguente `/content/wknd/language-masters/en` è l’origine.
* Il contenuto sotto `/content/wknd/language-masters/en` viene copiato sotto i nodi `/content/wknd/us/en/` e `/content/wknd/ca/en`. Queste sono le Live Copy.
* Gli autori possono apportare modifiche alle pagine sottostanti `/content/wknd/language-masters/en`.
* Quando viene attivato, MSM sincronizza queste modifiche con le Live Copy.

### Live Copy - Composizione {#live-copies-composition}

>[!NOTE]
>
>I diagrammi e le descrizioni contenuti in questa sezione rappresentano istantanee di potenziali Live Copy. Non sono complete, ma forniscono una panoramica per evidenziare caratteristiche specifiche.

Quando crei inizialmente una Live Copy, le pagine sorgente selezionate vengono riportate in 1:1 in Live Copy. In seguito, è possibile creare nuove risorse (pagine e/o paragrafi) direttamente all’interno della Live Copy, pertanto è utile essere consapevoli di queste varianti e del loro impatto sulla sincronizzazione. Le possibili composizioni includono:

* [Live Copy con pagine non Live Copy](#live-copy-with-non-live-copy-pages)
* [Live Copy nidificate](#nested-live-copies)

La forma di base di Live Copy include:

* Pagine Live Copy che riflettono le pagine sorgente selezionate su base 1:1.
* Una definizione di configurazione.
* Una relazione live definita per ogni risorsa:
   * Collega la risorsa Live Copy alla relativa blueprint/sorgente.
   * Vengono utilizzati per la realizzazione di ereditarietà e rollout.

Le modifiche possono essere [sincronizzate](creating-live-copies.md#synchronizing-your-live-copy) in base ai requisiti.

![Panoramica sulla composizione di Live Copy](../assets/live-copy-composition.png)

#### Live Copy con pagine non Live Copy {#live-copy-with-non-live-copy-pages}

Quando crei una Live Copy in AEM, puoi visualizzare e navigare attraverso il ramo Live Copy e utilizzare le normali funzionalità AEM sul ramo Live Copy. Questo significa che puoi creare (o un processo) nuove risorse (pagine e/o paragrafi) all’interno della Live Copy. Ad esempio, un prodotto per una determinata regione o paese.

* Tali risorse non hanno alcuna relazione diretta con le pagine sorgente/blueprint e non sono sincronizzate.
* Si possono verificare scenari che MSM gestisce come casi speciali. Ad esempio, quando crei una pagina con la stessa posizione e lo stesso nome nei rami sorgente/blueprint e Live Copy. Per tali situazioni, consulta [Conflitti di rollout MSM](rollout-conflicts.md) per ulteriori informazioni.

![Live Copy con pagine non Live Copy](../assets/live-copy-with-non-live-copy-pages.png)

#### Live Copy nidificate {#nested-live-copies}

Quando crei (o esegui un processo) una [nuova pagina all&#39;interno di una Live Copy esistente](#live-copy-with-non-live-copy-pages) questa nuova pagina può anche essere impostata come Live Copy di un&#39;altra blueprint. Questa è nota come Live Copy nidificata. Nelle Live Copy nidificate il comportamento della seconda o della Live Copy interna è interessato dalla prima o dalla Live Copy esterna nei seguenti modi:

* Un rollout profondo attivato per la Live Copy di livello superiore può essere proseguito nella Live Copy nidificata.
* Eventuali collegamenti tra le sorgenti verranno riscritti in Live Copy.

Ad esempio, i collegamenti che puntano dal secondo al primo modello verranno riscritti come collegamenti che puntano dalla Live Copy nidificata/seconda alla prima Live Copy.

![Live Copy nidificate](../assets/live-copy-nested.png)

>[!NOTE]
>
>Se sposti o rinomini una pagina all’interno del ramo Live Copy, questa verrà trattata come una Live Copy nidificata per consentire AEM tenere traccia delle relazioni.

#### Live Copy sovrapposte {#stacked-live-copies}

Una Live Copy è nota come Live Copy sovrapposta quando viene creata come figlia di una Live Copy poco profonda. Si comporta nello stesso modo di una [Live Copy nidificata](#nested-live-copies).

### Configurazioni di origine, blueprint e blueprint {#source-blueprints-and-blueprint-configurations}

Qualsiasi pagina o ramo di pagine può essere utilizzato come origine di una Live Copy. Tuttavia, MSM consente anche di definire una configurazione blueprint che specifica un percorso sorgente. I vantaggi dell’utilizzo di una configurazione blueprint sono i seguenti:

* Consenti all&#39;autore di utilizzare l&#39;opzione **Rollout** su una blueprint. ovvero di inviare in modo esplicito modifiche a Live Copy che ereditano da questa blueprint.
* Consenti all&#39;autore di utilizzare **Crea sito**. Questo consente all’utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definisci una configurazione di rollout predefinita per le Live Copy che hanno una relazione con la blueprint.

La sorgente di una Live Copy può essere costituita da pagine normali o da pagine incluse in una configurazione blueprint. Entrambi sono casi d’uso validi.

La sorgente forma la blueprint per la Live Copy. La blueprint viene definita quando:

* [Creare una configurazione Blueprint](creating-live-copies.md#creating-a-blueprint-configuration)  - La configurazione definisce in anticipo le pagine da utilizzare per creare la Live Copy.
* [Crea una Live Copy di una pagina](creating-live-copies.md#creating-a-live-copy-of-a-page) : le pagine utilizzate per creare la Live Copy (le pagine sorgente) sono le pagine blueprint. Una configurazione blueprint potrebbe fare riferimento o meno alla pagina sorgente.

### Rollout e sincronizzazione {#rollout-and-synchronize}

Un rollout è l’azione MSM centrale che sincronizza Live Copy con le loro sorgenti. Puoi eseguire i rollout manualmente o in automatico.

* È possibile definire una [configurazione di rollout](#rollout-configurations) in modo che eventi [specifici](live-copy-sync-config.md#rollout-triggers) possano causare un rollout automatico.
* Quando crei una pagina blueprint puoi usare il comando **[Rollout](creating-live-copies.md#rolling-out-a-blueprint)** per inviare le modifiche in Live Copy.
   * Il comando **Rollout** è disponibile in una pagina blueprint a cui fa riferimento una configurazione blueprint.

   ![Rollout](../assets/live-copy-rollout.png)

* Quando crei una pagina Live Copy puoi utilizzare il comando **[Sincronizza](creating-live-copies.md#synchronizing-a-live-copy)** per richiamare le modifiche dalla sorgente alla Live Copy.
   * Il comando **Sincronizza** è sempre disponibile nella pagina Live Copy indipendentemente dal fatto che la pagina sorgente/blueprint sia inclusa in una configurazione blueprint.

   ![Sincronizza](../assets/live-copy-synchronize.png)

### Configurazioni rollout {#rollout-configurations}

Una configurazione di rollout definisce quando e come una Live Copy viene sincronizzata con il contenuto sorgente. Una configurazione di rollout è costituita da un trigger e da una o più azioni di sincronizzazione:

* **Trigger**  - Un trigger è un evento che causa la sincronizzazione di azioni live, ad esempio l&#39;attivazione di una pagina sorgente. MSM definisce i trigger che è possibile utilizzare.
* **Azioni di sincronizzazione** : le azioni di sincronizzazione vengono eseguite sulla Live Copy per sincronizzarla con l’origine. Le azioni di esempio sono la copia del contenuto, l’ordine dei nodi figlio e l’attivazione della pagina Live Copy. MSM fornisce una serie di azioni di sincronizzazione.

>[!NOTE]
>
>Puoi creare azioni personalizzate per la tua istanza utilizzando l’API Java.

Le configurazioni di rollout possono essere riutilizzate, in modo che più di una Live Copy possano utilizzare la stessa configurazione di rollout. Diverse [configurazioni di rollout](live-copy-sync-config.md#installed-rollout-configurations) sono incluse in un&#39;installazione standard.

### Conflitti di rollout {#rollout-conflicts}

I rollout possono diventare complicati, specialmente quando gli autori modificano il contenuto sia nella sorgente che nella Live Copy. È quindi utile sapere come AEM gestire eventuali conflitti che potrebbero verificarsi durante il rollout.](rollout-conflicts.md)[

### Sospensione e annullamento dell&#39;ereditarietà e della sincronizzazione {#suspending-and-cancelling-inheritance-and-synchronization}

Ogni pagina e componente di una Live Copy è associato alla relativa pagina sorgente e al relativo componente tramite una relazione live. La relazione live configura la sincronizzazione del contenuto Live Copy dall’origine.

Puoi **Sospendere** l’ereditarietà Live Copy per una pagina Live Copy in modo da poter modificare le proprietà e i componenti della pagina. Quando sospendi l’ereditarietà, le proprietà e i componenti della pagina non vengono più sincronizzati con l’origine.

Durante la modifica di una singola pagina, gli autori possono **Annullare l’ereditarietà** per un componente. Quando l’ereditarietà viene annullata, la relazione live viene sospesa e la sincronizzazione non viene eseguita per quel componente. L’annullamento dell’ereditarietà e della sincronizzazione è utile quando è necessario personalizzare le sottosezioni del contenuto.

### Scollegamento di una Live Copy {#detaching-a-live-copy}

Puoi anche [scollegare una Live Copy](creating-live-copies.md#detaching-a-live-copy) dalla relativa blueprint per rimuovere tutte le connessioni.

>[!CAUTION]
>
>L&#39;azione Stacca è permanente e non reversibile.

L’azione di scollegamento rimuove definitivamente la relazione live tra una Live Copy e la relativa pagina blueprint. Tutte le proprietà relative a MSM vengono rimosse dalla Live Copy e le pagine Live Copy diventano una copia autonoma.

>[!TIP]
>
>Per informazioni dettagliate, compreso l’impatto correlato sulle pagine secondarie e principali, consulta [Scollegamento di una Live Copy](creating-live-copies.md#detaching-a-live-copy) .

## Passaggi standard per l&#39;utilizzo di MSM {#standard-steps-for-using-msm}

I passaggi seguenti descrivono la procedura standard per utilizzare MSM per riutilizzare il contenuto e sincronizzare le modifiche a Live Copy.

1. Sviluppa il contenuto del sito di origine.
1. Determina la configurazione di rollout da utilizzare.

   1. MSM [installa diverse configurazioni di rollout](live-copy-sync-config.md#installed-rollout-configurations) che possono soddisfare una serie di casi d&#39;uso.
   1. Facoltativamente, puoi [creare una configurazione di rollout](live-copy-sync-config.md#creating-a-rollout-configuration) se necessario.

1. Stabilisci dove devi [specificare le configurazioni di rollout da utilizzare](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use) e configura come necessario.
1. Se necessario, [crea una configurazione blueprint](creating-live-copies.md#creating-a-blueprint-configuration) che identifica il contenuto sorgente della Live Copy.
1. [Crea una Live Copy.](creating-live-copies.md#creating-a-live-copy)
1. Apporta le modifiche necessarie al contenuto sorgente. È necessario utilizzare il normale processo di revisione e approvazione del contenuto stabilito dalla propria organizzazione.
1. [Esegui il rollout ](creating-live-copies.md#rolling-out-a-blueprint) della blueprint o  [sincronizza la Live ](creating-live-copies.md#synchronizing-a-live-copy) Copy con le modifiche.

## Personalizzazione di MSM {#customizing-msm}

MSM fornisce strumenti che consentono all’implementazione di adattarsi alle complessità eccezionali che possono esistere durante la condivisione dei contenuti.

* **Configurazioni di rollout personalizzate**  -  [Crea una ](live-copy-sync-config.md#creating-a-rollout-configuration) configurazione di rollout quando le configurazioni di rollout installate non soddisfano le tue esigenze. Puoi utilizzare qualsiasi azione di trigger di rollout e sincronizzazione disponibile.

<!--
* **Custom Synchronization Actions** - [Create a custom synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) when the installed actions do not meet your specific application requirements. MSM provides a Java API for creating custom synchronization actions.
-->

## Best practice   {#best-practices}

La pagina [Best practice MSM](best-practices.md) contiene informazioni importanti sull&#39;implementazione.
