---
title: Guida rapida alle linee guida WCAG 2.1
seo-title: Guida rapida alle linee guida WCAG 2.1
translation-type: tm+mt
source-git-commit: 921334705578626ac0ea75765496d4f379bb00fc

---


# Guida rapida alle linee guida WCAG 2.1{#quick-guide-to-wcag}

Adobe Experience Manager (AEM) as a Cloud Service è stato sviluppato per garantire una conformità ottimale alle linee guida per l’accessibilità dei contenuti web.

The [Web Content Accessibility Guidelines (WCAG) version 2.1](https://www.w3.org/TR/WCAG/) are a set of internationally recognized guidelines developed by the [World Wide Web Consortium (W3C)](https://www.w3.org/) under their [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

Le linee guida WCAG 2.1 sono costituite da un insieme di criteri di successo e linee guida che non dipendono dalla tecnologia in uso e hanno l’obiettivo di rendere i contenuti web accessibili e utilizzabili da persone con disabilità. Includono suggerimenti e indicazioni per autori, designer e sviluppatori di contenuti web al fine di garantire che le risorse prodotte siano progettate in modo da essere accessibili per un pubblico che sia il più ampio possibile, indipendentemente da eventuali disabilità o limitazioni, quali disabilità visive o uditive, difficoltà di apprendimento o limiti correlati all’età.

Ad esempio, la descrizione di un’immagine (o di qualsiasi altro contenuto non testuale) tramite l’attributo `alt` nel linguaggio HTML offre notevoli vantaggi alle persone non vedenti o ipovedenti. La descrizione testuale contenuta nell’attributo `alt` può essere convertita in un output vocale o trasmessa a display Braille elettronici aggiornabili.

Inoltre, la conformità alle linee guida WCAG 2.1 può offrire vantaggi anche ad altri beneficiari, tra cui persone con *disabilità situazionale*: persone che, a causa di fattori quali tecnologia di navigazione, velocità della connessione di rete o ambiente di navigazione, possono incontrare barriere simili alle persone con disabilità.

Utilizzando Adobe Experience Manager, gli autori di contenuti e/o i proprietari di siti web possono creare contenuti web che soddisfano i criteri di successo WCAG 2.1 pertinenti di livello A e AA.

È quindi importante comprendere gli obiettivi e la struttura delle linee guida WCAG 2.1, per capire il ruolo dell’accessibilità web e come le linee guida consentano di creare contenuti web accessibili.

WCAG 2.1 intende fornire linee guida con le caratteristiche indicate di seguito.

* **Indipendenti dalla tecnologia utilizzata**:
in altre parole, si tratta di linee guida che possono essere applicate a diversi formati di contenuti web, non solo a contenuti HTML. Le linee guida WCAG 2.1 sono quindi applicabili anche a contenuti generati o forniti tramite PDF, Flash, JavaScript o altre tecnologie web attuali e future. <!-- This aims to address a recognized weakness of WCAG 1.0, in that it was focused on HTML at the expense of other web content formats. -->

* **Testabili**:
ogni istruzione è redatta in modo da poter essere testata in modo oggettivo affinché un gruppo di esperti di accessibilità possa concordare in linea generale sul fatto che la linea guida sia stata rispettata. Una delle problematiche correlate all’accessibilità, infatti, consiste nel fatto che alcune linee guida possono essere tecnicamente testabili, mentre altre richiedono una valutazione umana per verificare se siano state rispettate o meno. <!-- WCAG 2.1 has been written with the aim of reducing the subjectivity that was present in some of the WCAG 1.0 guidelines and checkpoints. -->

* **Implementazione contestuale e con priorità**:
   <!-- As with WCAG 1.0, --> WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. This allows authors to make an informed decision on the most important guidelines for their particular situation. In addition, the concept of *accessibility supported* is introduced. This allows authors to make decisions on how best to use web technologies that may not have full accessibility support, or may require users to have specific assistive technologies and/or browsers in order to benefit from accessibility features.

Tali obiettivi hanno influenzato in modo significativo la struttura delle linee guida WCAG 2.1.

>[!NOTE]
>
>Non è possibile creare un sito web che tenga in considerazione ogni possibile disabilità o tipo di persona. Le linee guida WCAG 2.1 intendono aiutare gli autori di siti web a creare, per quanto possibile, siti ragionevolmente accessibili per determinate condizioni.

<!--
>[!NOTE]
>
>If you are familiar with WCAG 1.0, you will notice some changes in WCAG 2.1. These relate to scope, organization and aim.
-->

## Struttura {#structure}

Le linee guida WCAG 2.1 sono strutturate in modo da introdurre i concetti di creazione di contenuti web accessibili in ordine progressivo, dal più semplice al più dettagliato. Questa caratteristica può dare l’impressione che le linee guida WCAG 2.1 siano un insieme molto complesso di documenti interconnessi. In realtà l’obiettivo è quello di fornire le informazioni in modo progressivamente più dettagliato, a cui gli autori possono accedere come e quando ne hanno bisogno, anziché fornire tutte le istruzioni in un unico documento molto esteso.

Le linee guida WCAG 2.1 si basano su quattro principi chiave per la progettazione accessibile, a volte indicati tramite l’acronimo **POUR (Perceivable, Operable, Understandable, Robust)**. Secondo questi principi, il contenuto deve essere:

1. **Percepibile**: un utente è in grado di percepire il contenuto web in questione?
1. **Utilizzabile**: un utente ha la possibilità di navigare, inserire dati o interagire in altro modo con il contenuto web?
1. **Comprensibile**: un utente è in grado di elaborare e comprendere il contenuto web presentato?
1. **Robusto**: il contenuto web è disponibile nel modo previsto in un’ampia gamma di ambienti di navigazione, inclusi quelli legacy ed emergenti?

In particolare:
* Ogni **principio** è costituito da una o più **linee guida**.

* Le linee guida sono formulate come istruzioni, che possono essere positive (cose da fare) o negative (cose da non fare).
* Le linee guida sono numerate da 1.1 a 4.1 e la prima cifra corrisponde al principio padre.
* Ogni linea guida è costituita da uno o più **criteri di successo**.
* I criteri di successo sono formulati come istruzioni, che possono essere `True` o `False` per una determinata pagina web.
* I criteri di successo possono includere una o più opzioni oppure eccezioni, ovvero situazioni in cui non è necessario soddisfare i criteri di successo.
* I criteri di successo sono numerati in base alla linea guida e al principio padre, da 1.1.1 a 4.1.1. Hanno anche un nome breve che riassume l’intento del criterio, per un riferimento più semplice. Ad esempio, il criterio di successo 1.1.1 prevede un’alternativa non testuale.
* I criteri di successo includono un elenco delle **tecniche** correlate (descritte più in dettaglio di seguito).

## Risorse di supporto {#supporting-resources}

Oltre alle componenti WCAG 2.1 di base, ovvero principi, linee guida e criteri di successo, è disponibile una serie di documenti di supporto. Alcuni forniscono consigli specifici su come soddisfare gli aspetti delle linee guida; altri sono riferimenti più generali che aiutano gli autori, i designer e gli sviluppatori a comprendere e utilizzare le linee guida WCAG 2.1 nel modo più efficace possibile, a prescindere dal loro livello di competenza.

Mentre le linee guida WCAG 2.1 rappresentano un documento stabile che non verrà modificato, la maggior parte delle risorse di supporto è costituita da documenti dinamici che verranno modificati e incrementati nel tempo, man mano che emergono nuove tecnologie e si scoprono nuovi esempi di come l’obiettivo di accessibilità dei contenuti web possa essere conseguito.

### Risorse WCAG 2.1 {#wcag-resources}

L’elenco non è esaustivo, ma fornisce un’introduzione alle risorse disponibili:
* [Panoramica di tutti i documenti correlati alle WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [Riepilogo dei diversi documenti](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Linee guida per l’accessibilità dei contenuti web (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [Novità delle linee guida WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [Guida di riferimento rapido per soddisfare le linee guida WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Domande frequenti sulle linee guida WCAG 2](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### Novità delle linee guida WCAG 2.1 {#what-is-new}

Il documento che illustra le [novità delle linee guida WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) fornisce informazioni utili sulle differenze tra le versioni WCAG 2.0 e WCAG 2.1.

La sezione [WCAG 2.0 e WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) approfondisce ulteriormente il confronto.

### Tecniche per WCAG 2.1 {#techniques-for-wcag}

La pagina dedicata alle [tecniche per WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/) contiene informazioni dettagliate.

Nella gerarchia WCAG 2.1, le **tecniche** rappresentano il livello inferiore ai criteri di successo e sono classificate da WAI come informative anziché normative. In altre parole, non è necessario seguire una tecnica specifica affinché una risorsa sia conforme a WCAG 2.1.

Poiché le tecniche sono molto più specifiche dei criteri di successo, in genere fanno riferimento a una particolare tecnologia, a un tipo di contenuto specifico (ad esempio HTML o video) oppure a una situazione particolare, come un’applicazione di e-commerce o di e-learning. È possibile considerarle esempi comprovati di come possono essere soddisfatti specifici criteri di successo e linee guida, e rappresentano quindi strumenti utili per autori e sviluppatori che lavorano in contesti specifici.

È possibile accedere alle tecniche nei seguenti modi:

* In base alla raccolta - Le tecniche possono essere generali o correlate a una tecnologia oppure a un formato specifico, ad esempio HTML, CSS o script sul lato client.
* Da criteri di successo correlati - Le tecniche possono essere applicate a più criteri di successo.

Ogni tecnica ha un numero univoco, relativo alla raccolta corrispondente. Ad esempio, una delle tecniche ARIA è *ARIA2: identificazione dei campi obbligatori con la proprietà “required”*.

Le tecniche possono essere sufficienti, consigliate o di errore.

* Una *tecnica sufficiente*, se seguita, sarà sufficiente per soddisfare un particolare criterio di successo.
* Una *tecnica consigliata*, se seguita, avrà un impatto positivo sull’accessibilità, ma potrebbe non essere sufficiente da sola per garantire il rispetto di un particolare criterio di successo.
* Un *tecnica di errore* descrive un esempio specifico in cui i criteri di successo non sono stati soddisfatti.

I dettagli delle tecniche includono descrizione, applicabilità, esempi, risorse per ulteriori informazioni e dettagli su come gli autori possono eseguire un test per verificare se l’applicazione della tecnica è efficace.

L’elenco delle tecniche non è statico: WAI lo aggiorna costantemente con nuovi esempi, che riflettono gli sviluppi della tecnologia web, degli approcci di progettazione e dei risultati della ricerca. Si consiglia quindi di controllare regolarmente l’elenco delle tecniche per verificare eventuali nuove aggiunte.

### Informazioni sulle linee guida WCAG 2.1 {#understanding-wcag}

Si tratta di una serie di documenti che forniscono consigli ai lettori per approfondire lo scopo di linee guida e criteri di successo specifici. È possibile [scaricare un’introduzione con collegamenti a informazioni più dettagliate](https://www.w3.org/WAI/WCAG21/Understanding/).

Per ogni linea guida e criterio di successo è disponibile anche un breve documento esplicativo con informazioni su:

* Intento della linea guida
* Criteri di successo specifici
* Tecniche consigliate, che contribuiscono a soddisfare i requisiti della linea guida, ma che non rientrano in alcun criterio di successo specifico.

Il documento esplicativo per ogni criterio di successo fornisce informazioni su:

* Intento del criterio di successo
* Esempi generali di come può essere soddisfatto il criterio di successo
* Risorse correlate (non W3C) su come soddisfare il criterio di successo
* Tecniche ed errori - Esempi specifici e dettagliati su come soddisfare il criterio di successo (descritti più dettagliatamente di seguito)
* Termini chiave - Glossario dei termini importanti per la comprensione del criterio di successo

Nella sezione per la [comprensione del criterio di successo 1.1.1 (“Contenuti non testuali”)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content) è disponibile un esempio.

### Come soddisfare le linee guida WCAG 2.1 {#how-to-meet-wcag}

Nella pagina dedicata a [come soddisfare le linee guida WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/) sono disponibili indicazioni sulla conformità alle linee guida. Viene fornita una presentazione alternativa delle linee guida WCAG, che consente di ottenere i contenuti delle linee guida pertinenti in base agli interessi o agli obiettivi del lettore. È possibile filtrare le tecniche relative ai criteri di successo da visualizzare specificando particolari tecnologie di contenuti web, ad esempio Cascading Style Sheets o script oppure specificando un particolare livello di priorità.

Se non viene applicato alcun filtro, vengono presentati tutti i criteri di successo raggruppati per linea guida. Per ciascun criterio di successo, vengono fornite le seguenti informazioni:

* Testo del criterio di successo
* Collegamento al corrispondente documento per la comprensione
* Elenco delle tecniche sufficienti correlate, con collegamento ai dettagli di ciascuna tecnica
* Elenco delle tecniche consigliate correlate, con collegamento ai dettagli di ciascuna tecnica (se disponibile)
* Elenco degli errori correlati, con collegamento ai dettagli di ogni errore
