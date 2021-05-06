---
title: Come modellare il contenuto
description: In questa parte del Percorso di sviluppatori AEM Headless , scopri come modellare i contenuti per la distribuzione AEM Headless utilizzando la modellazione dei contenuti con modelli di frammenti di contenuto e frammenti di contenuto.
hide: true
hidefromtoc: true
index: false
exl-id: f872839b-2401-4ea4-9e09-e5dda18afd09
translation-type: tm+mt
source-git-commit: dd30bbb57d2746a7b16cb0546b90df0758fc3740
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 2%

---

# Come modellare il contenuto {#model-your-content}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless](overview.md), puoi imparare a modellare la struttura dei contenuti. Quindi realizza quella struttura per Adobe Experience Manager (AEM) utilizzando Modelli per frammenti di contenuto e Frammenti di contenuto, da riutilizzare tra i canali.

## La storia finora {#story-so-far}

All&#39;inizio [Scopri lo sviluppo headless di CMS](learn-about.md) la distribuzione di contenuti headless coperti e perché dovrebbe essere utilizzata. Quindi [Come iniziare a AEM senza testa come un Cloud Service](getting-started.md) ha descritto AEM senza testa nel contesto del tuo progetto

Nel documento precedente del percorso senza testa AEM [Percorso alla prima esperienza con AEM headless](/help/implementing/developing/headless-journey/path-to-first-experience.md), hai quindi appreso i passaggi necessari per implementare il primo progetto. Dopo la lettura dovrebbe:

* Comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti
* Comprendi i passaggi per implementare headless in base ai requisiti del livello di integrazione.
* Imposta gli strumenti e le configurazioni AEM necessarie.
* Scopri le best practice per semplificare il tuo percorso headless, garantire l’efficienza nella generazione dei contenuti e la distribuzione rapida dei contenuti.

Questo articolo si basa su questi fondamentali in modo da capire come preparare il tuo progetto AEM headless.

## Obiettivo {#objective}

* **Pubblico**: Principiante
* **Obiettivo**: Scopri come modellare la struttura del contenuto, quindi realizzare tale struttura utilizzando AEM Modelli per frammenti di contenuto e Frammenti di contenuto:
   * Introdurre concetti e terminologia relativi alla modellazione di dati/contenuti.
   * Scopri perché è necessaria la modellazione dei contenuti per la distribuzione di contenuti headless.
   * Scopri come realizzare questa struttura utilizzando AEM modelli di frammenti di contenuto (e creare contenuti con frammenti di contenuto).
   * Scopri come modellare il contenuto; principi con campioni di base.

>[!NOTE]
>
>La modellazione dei dati è un campo molto grande, in quanto viene utilizzata durante lo sviluppo di database relazionali. Ci sono molti libri, e fonti di informazione online, disponibili.
>
>Prenderemo in considerazione solo gli aspetti di interesse nella modellazione dei dati da utilizzare con AEM Headless.

## Modellazione dei contenuti {#content-modeling}

*È un mondo grande e cattivo là* fuori.

Forse, forse no, ma è certamente un grande ***complicato*** mondo là fuori e la modellazione dei dati viene utilizzata per definire una rappresentazione semplificata di una sottosezione molto (molto) piccola, utilizzando le informazioni specifiche necessarie per un certo scopo.

>[!NOTE]
>
>Poiché AEM i contenuti, ci riferiamo alla modellazione dei dati come modellazione dei contenuti.

Esempio:

Ci sono molte scuole, ma tutte hanno varie cose in comune:

* Una posizione
* Insegnante
* Molti insegnanti
* Molti membri del personale non docente
* Molti studenti
* Molti ex-insegnanti
* Molti ex allievi
* Molte classi
* Molti (molti) libri
* Molti (molti) pezzi di attrezzatura
* Molte attività extra-curriculum
* e così via....

Anche in un esempio così piccolo la lista può sembrare infinita. Ma se si desidera semplicemente che l&#39;applicazione esegua un&#39;attività semplice, è necessario limitare le informazioni alle risorse essenziali.

Ad esempio, pubblicità di eventi speciali per tutte le scuole della zona:

* Nome della scuola
* Posizione della scuola
* Insegnante
* Tipo di evento
* Data dell’evento
* Insegnante che organizza l’evento

### Concetti {#concepts}

Ciò che si desidera descrivere viene definito **Entità** - sostanzialmente le &quot;cose&quot; di cui si desidera memorizzare le informazioni.

Le informazioni che vogliamo memorizzare su di esse sono le **Attributi** (proprietà), come Nome e Qualifiche per gli insegnanti.

Poi ci sono varie **Relazioni** tra le entità. Per esempio, di solito una scuola ha solo un insegnante principale e molti insegnanti (e di solito il maestro capo è anche un insegnante).

Il processo di analisi e definizione di queste informazioni, insieme alle relazioni tra di esse, si chiama **Modellazione dei contenuti**.

### Funzioni di base {#basics}

Spesso è necessario iniziare disegnando un **Schema concettuale** che descrive le entità e le loro relazioni. Di solito questo è di alto livello (concettuale).

Una volta stabile, è possibile tradurre i modelli in un **Schema logico** che descrive le entità, insieme agli attributi e le relazioni. A questo livello, è necessario esaminare attentamente le definizioni per eliminare la duplicazione e ottimizzare la progettazione.

>[!NOTE]
>
>A volte questi due passaggi vengono uniti, spesso a seconda della complessità dello scenario.

Ad esempio, sono necessarie entità separate per `Head Teacher` e `Teacher`, oppure è sufficiente un attributo aggiuntivo sul modello `Teacher`?

### Assicurazione dell&#39;integrità dei dati {#data-integrity}

L’integrità dei dati è necessaria per garantire l’accuratezza e la coerenza dei contenuti durante l’intero ciclo di vita. Ciò include la garanzia che gli autori dei contenuti possano capire facilmente dove archiviare, per cui sono fondamentali i seguenti elementi:

* una struttura chiara
* una struttura il più concisa possibile (senza sacrificare la precisione)
* convalida di singoli campi
* se del caso, limitare il contenuto di campi specifici a ciò che è significativo

### Eliminazione della ridondanza dei dati {#data-redundancy}

La ridondanza dei dati si verifica quando le stesse informazioni vengono memorizzate due volte nella struttura del contenuto. Questo dovrebbe essere evitato in quanto può generare confusione durante la creazione del contenuto e errori durante l’esecuzione di query; per non parlare dell&#39;uso improprio dello spazio di archiviazione.

### Ottimizzazione e prestazioni {#optimization-and-performance}

Ottimizzando la struttura è possibile migliorare le prestazioni, sia per la creazione di contenuti che per l’esecuzione di query.

Tutto è un atto di bilanciamento, ma la creazione di una struttura troppo complessa o con troppi livelli può:

* Fai confusione per gli autori che generano i contenuti.

* Influisce notevolmente sulle prestazioni se la query deve accedere a più frammenti di contenuto nidificati (a cui si fa riferimento) per recuperare il contenuto richiesto.

## Modellazione dei contenuti per AEM headless {#content-modeling-for-aem-headless}

Data Modeling è un insieme di tecniche consolidate, spesso utilizzate quando si sviluppano database di relazioni, quindi cosa significa Modellazione dei contenuti per AEM Headless?

### Perché? {#why}

Per garantire che l’applicazione possa richiedere e ricevere in modo coerente ed efficiente il contenuto richiesto da AEM, questo contenuto deve essere strutturato.

Ciò significa che l&#39;applicazione conosce in anticipo la forma di risposta e quindi come elaborarla. Questo è molto più semplice della ricezione di contenuti in formato libero, che devono essere analizzati per determinare cosa contengono e quindi come possono essere utilizzati.

### Introduzione a Come? {#how}

AEM utilizza Frammenti di contenuto per fornire le strutture necessarie per la distribuzione headless dei contenuti alle applicazioni.

La struttura del modello di contenuto è la seguente:

* realizzato dalla definizione del modello per frammenti di contenuto,
* utilizzati come base dei frammenti di contenuto utilizzati per la generazione dei contenuti.

>[!NOTE]
>
>I modelli per frammenti di contenuto vengono utilizzati anche come base degli schemi AEM GraphQL, utilizzati per recuperare il contenuto. Ulteriori informazioni in una sessione successiva.

Le richieste di contenuti vengono effettuate utilizzando l’API GraphQL di AEM, un’implementazione personalizzata dell’API GraphQL standard. L’API GraphQL AEM ti consente di eseguire query (complesse) sui frammenti di contenuto, con ogni query in base a un tipo di modello specifico.

Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

## Creazione della struttura con modelli di frammenti di contenuto {#create-structure-content-fragment-models}

I modelli per frammenti di contenuto forniscono vari meccanismi che consentono di definire la struttura del contenuto.

Un modello di frammento di contenuto descrive un’entità.

>[!NOTE]
>È necessario abilitare la funzionalità Frammento di contenuto nel browser di configurazione in modo da poter creare nuovi modelli.

>[!TIP]
>
>Il modello deve essere denominato in modo che l’autore del contenuto sappia quale modello selezionare durante la creazione di un frammento di contenuto.

All&#39;interno di un modello:

1. **I** tipi di dati ti consentono di definire i singoli attributi.
Ad esempio, definisci il campo contenente il nome di un insegnante come **Testo** e i relativi anni di servizio come **Numero**.
1. I tipi di dati **Riferimento contenuto** e **Riferimento frammento** consentono di creare relazioni con altri contenuti all’interno di AEM.
1. Il tipo di dati **Riferimento frammento** ti consente di realizzare più livelli di struttura nidificando i frammenti di contenuto (in base al tipo di modello). Questo è fondamentale per la modellazione dei contenuti.

Ad esempio:
![Modellazione dei contenuti con frammenti di contenuto](assets/headless-modeling-01.png "Modellazione dei contenuti con frammenti di contenuto")

### Tipi di dati {#data-types}

AEM fornisce i seguenti tipi di dati per modellare il contenuto:

* Testo su riga singola
* Testo su più righe
* Numero
* Booleano
* Data e ora
* Enumerazione
* Tag
* Riferimento contenuto
* Riferimento frammento
* Oggetto JSON

### Riferimenti e contenuto nidificato {#references-nested-content}

Due tipi di dati forniscono riferimenti a contenuti esterni a uno specifico frammento:

* **Content**
ReferenceQuesto fornisce un semplice riferimento ad altri contenuti di qualsiasi tipo.
Ad esempio, è possibile fare riferimento a un&#39;immagine in una posizione specifica.

* **Riferimento frammento**
Questo fornisce riferimenti ad altri frammenti di contenuto.
Questo tipo di riferimento viene utilizzato per creare contenuti nidificati, introducendo le relazioni necessarie per modellare il contenuto.
Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
   * Modificare direttamente il frammento a cui si fa riferimento.
   * Crea un nuovo frammento di contenuto basato sul modello appropriato

### Creazione di modelli di frammenti di contenuto {#creating-content-fragment-models}

In primo luogo, i modelli di frammento di contenuto sono abilitati per il sito, questo avviene nel browser di configurazione:

![Definire la configurazione](assets/cfm-configuration.png)

Quindi i modelli dei frammenti di contenuto possono essere modellati:

![Modello per frammenti di contenuto](assets/cfm-model.png)

>[!NOTE]
>
>Consulta Utilizzo dei frammenti di contenuto .

## Uso del modello per creare contenuti con frammenti di contenuto {#use-content-to-author-content}

I frammenti di contenuto si basano sempre su un modello di frammento di contenuto. Il modello fornisce la struttura, il frammento contiene il contenuto.

### Selezione del modello appropriato {#select-model}

Il primo passaggio per creare effettivamente il contenuto è la creazione di un frammento di contenuto. Si basa su un modello specifico di frammento di contenuto, selezionato come primo passaggio del processo di creazione.

### Creazione e modifica di contenuti strutturati {#create-edit-structured-content}

Una volta creato il frammento, è possibile aprirlo nell’Editor frammento di contenuto. È possibile:

* Modifica il contenuto in modalità normale o a schermo intero.
* Formatta il contenuto come Testo completo, Testo normale o Markdown.
* Crea e gestisci le varianti dei contenuti.
* Associa contenuto.
* Modifica i metadati.
* Mostra la struttura ad albero.
* Visualizzare in anteprima la rappresentazione JSON.

### Creazione di frammenti di contenuto {#creating-content-fragments}

Dopo aver selezionato il modello appropriato, nell’Editor frammento di contenuto viene aperto un frammento di contenuto per la modifica:

![Editor frammento di contenuto ](assets/cfm-editor.png)

>[!NOTE]
>
>Consulta Utilizzo dei frammenti di contenuto .

## Guida introduttiva ad alcuni esempi {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

Per una struttura di base come esempio, vedere Struttura dei frammenti di contenuto di esempio.

## Novità {#whats-next}

Ora che hai imparato a modellare la tua struttura e a creare contenuti a seconda di essa, il passaggio successivo è [Scopri come utilizzare le query GraphQL per accedere e recuperare il contenuto dei frammenti di contenuto](access-your-content.md). Questo introdurrà e discuterà GraphQL, quindi esaminerà alcune query di esempio per vedere come funzionano le cose in pratica.

## Risorse aggiuntive {#additional-resources}

* [Utilizzo dei frammenti](/help/assets/content-fragments/content-fragments.md)  di contenuto: pagina iniziale per i frammenti di contenuto
   * [Frammenti di contenuto nel browser](/help/assets/content-fragments/content-fragments-configuration-browser.md)  di configurazione: abilitare la funzionalità Frammento di contenuto nel browser di configurazione
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) : creazione e modifica di modelli per frammenti di contenuto
   * [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) : creazione e creazione di frammenti di contenuto; questa pagina ti porterà ad altre sezioni dettagliate
* [AEM Schemi GraphQL](/help/implementing/developing/headless-journey/access-your-content.md)  - come GraphQL realizza i modelli
* [Struttura dei frammenti di contenuto di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Guida introduttiva a AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - Una breve serie di esercitazioni video che offre una panoramica dell’utilizzo di AEM funzioni headless, tra cui la modellazione dei contenuti e GraphQL
