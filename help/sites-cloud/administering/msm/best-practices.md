---
title: Best practice MSM
description: Scopri le best practice compilate dai team di progettazione e consulenza di Adobe per iniziare a utilizzare AEM Multi Site Manager.
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 95%

---

# Best practice MSM {#msm-best-practices}

## Generale {#general}

MSM è un framework configurabile per automatizzare la distribuzione dei contenuti. Le implementazioni spesso coinvolgono parti importanti di un sito Web e si estendono su più organizzazioni e aree geografiche. È quindi vivamente consigliato pianificare le implementazioni MSM con la stessa attenzione con cui pianifichi il tuo sito Web:

* Pianifica attentamente **la struttura e i flussi di contenuto** prima di iniziare l&#39;implementazione.
* **Personalizza tutto il necessario, ma il meno possibile.** Anche se MSM supporta un elevato grado di personalizzazione (ad esempio le configurazioni di rollout), in genere come best practice per prestazioni, affidabilità e aggiornamento del sito web conviene ridurre al minimo la personalizzazione.
* Stabilisci anticipatamente un modello di **governance** e forma gli utenti di conseguenza per assicurarti che proceda tutto in maniera ottimale. Dal punto di vista della governance, una buona pratica è quella di **ridurre al minimo l&#39;autorità di cui dispongono i produttori locali di contenuti** per allocare/collegare contenuti ad altri utenti locali e alle rispettive Live Copy. Ciò è dovuto al fatto che le ereditarietà chained non gestite possono aumentare notevolmente la complessità di una struttura MSM e comprometterne le prestazioni e l&#39;affidabilità.
* Una volta che esiste un piano per la struttura, i flussi di contenuti, l&#39;automazione e la governance, **crea un prototipo e testa a fondo il sistema** prima di iniziare l&#39;implementazione live.
* Tieni presente che **Adobe Consulting e i principali System Integrator** hanno una solida esperienza nella pianificazione e nell&#39;implementazione dell&#39;automazione dei contenuti con MSM, per cui possono aiutarti sia all&#39;inizio del progetto MSM che durante l&#39;intera implementazione.

## Sorgenti Live Copy e configurazioni Blueprint {#live-copy-sources-and-blueprint-configurations}

Tieni presente che una Live Copy può essere creata utilizzando [pagine normali](creating-live-copies.md#creating-a-live-copy-of-a-page) o [configurazioni blueprint](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Entrambi sono casi d’uso validi.

I vantaggi aggiuntivi dell’utilizzo di una configurazione blueprint sono i seguenti:

* Consente all’autore di utilizzare il **rollout** su una blueprint al fine di inviare in modo esplicito modifiche alle Live Copy che la ereditano.
* Consente all’autore di utilizzare **Crea sito** per selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definisci una configurazione di rollout predefinita per le Live Copy che hanno una relazione con la blueprint.

Nel caso in cui non venga fatto riferimento a una configurazione blueprint, i rollout possono essere avviati solo dalle Live Copy stesse, essenzialmente richiamando il contenuto dal sorgente.

Quando crei un nuovo sito con Live Copy, è vantaggioso creare configurazioni blueprint per garantire la disponibilità dell’intero set di funzioni MSM.

>[!NOTE]
>
>Non è possibile eseguire il rollout dei CUG nella scheda Autorizzazioni in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione della Live Copy.

## Sincronizzazione dei componenti e dei contenitori {#components-and-container-synchronization}

In generale, la regola di rollout in MSM per quanto riguarda la sincronizzazione dei componenti è:

* I componenti vengono implementati per sincronizzare tutte le risorse contenute nella blueprint.
* I contenitori sincronizzano solo la risorsa corrente.

Ciò significa che i componenti sono trattati come un aggregato e in un rollout il componente stesso e tutti i suoi figli vengono sostituiti con quelli nei progetti. Ciò significa che se una risorsa viene aggiunta localmente a tale componente, viene persa per il contenuto della blueprint al momento del rollout.

Per supportare la nidificazione dei componenti in modo che i componenti aggiunti localmente siano mantenuti in un rollout, il componente deve essere dichiarato come contenitore.

>[!NOTE]
>
>Aggiungi la proprietà `cq:isContainer` al componente per designarlo come contenitore.

## Crea sito {#create-site}

Tieni presente che AEM dispone di due approcci principali per la creazione di Live Copy:

* Durante la [creazione di una Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page): questo può essere considerato come l’approccio più generico, che consente di creare Live Copy da qualsiasi pagina. La struttura del contenuto di una Live Copy corrisponde esattamente al sorgente.

* Durante la [creazione di un sito](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration): si tratta di un approccio più specializzato, principalmente per la creazione di siti Web con una struttura multilingue.

Di seguito sono riportate alcune considerazioni da tenere a mente durante la creazione di un sito:

* Per creare un nuovo sito, è necessario una [configurazione blueprint](creating-live-copies.md#managing-blueprint-configurations).
* Per consentire la selezione dei percorsi linguistici da creare in un nuovo sito, le lingue root corrispondenti devono esistere nella blueprint (sorgente).
* Una volta creato un [nuovo sito come Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (usando **Crea**, poi **Sito**), i primi due livelli di questa Live Copy sono *shallow*. Gli elementi figli della pagina non appartengono alla relazione live, ma se viene trovata una relazione live corrispondente al trigger, verrà comunque generato un rollout.

È utile evitare:

* L&#39;aggiunta manuale di lingue nella blueprint (sotto il primo livello).
* Aggiungendo manualmente il contenuto direttamente sotto la lingua root, poiché questo non comporta il trasferimento automatico del nuovo contenuto alla Live Copy al momento del rollout.

## Siti Web MSM e multilingue {#msm-and-multilingual-websites}

MSM può contribuire alla creazione di siti Web multilingue in due modi:

Quando crei le lingue master, tieni presente quanto segue:

* Sebbene MSM stesso **non fornisca la traduzione del contenuto**, può essere integrato con connettori di traduzione di terze parti che lo fanno. Tieni presente quanto segue:
   * MSM consente di annullare l’ereditarietà a livello di pagina e/o di componente. Questo aiuta a evitare la sovrascrittura dei contenuti tradotti (da una Live Copy, con contenuti non ancora tradotti da una blueprint) al prossimo rollout.
      * Alcuni connettori di traduzione di terze parti automatizzano questa gestione delle ereditarietà MSM.
      * Per ulteriori informazioni, rivolgiti al fornitore di servizi di traduzione.
      * Un approccio alternativo per la creazione e la traduzione di lingue master consiste nell’utilizzare copie in lingua insieme al Translation Integration Framework di AEM preconfigurato.

Per ulteriori informazioni consulta [Traduzione di contenuti per siti multilingue](/help/sites-cloud/administering/translation/overview.md) e [Best practice per la traduzione](/help/sites-cloud/administering/translation/best-practices.md).

## Modifiche alla struttura e rollout {#structure-changes-and-rollouts}

Le modifiche alla struttura del contenuto in una struttura blueprint/sorgente vengono riportate in modo diverso in una Live Copy. Dipende dal tipo di modifica:

* La **creazione** di nuove pagine in una blueprint determinerà la creazione delle pagine corrispondenti in Live Copy dopo il rollout con la configurazione di rollout standard.
* L&#39;**eliminazione** delle pagine di una blueprint determinerà l’eliminazione delle pagine corrispondenti dalla Live Copy dopo il rollout con la configurazione di rollout standard.
* Lo **spostamento** delle pagine in una blueprint **non** fa sì che le pagine corrispondenti vengano spostate in Live Copy dopo il rollout con la configurazione di rollout standard:
   * Questo comportamento si spiega con il fatto che lo spostamento di una pagina include implicitamente l’eliminazione di una pagina. Questo potrebbe causare un comportamento imprevisto al momento della pubblicazione, in quanto l’eliminazione delle pagine sull’autore disattiva automaticamente il contenuto corrispondente al momento della pubblicazione. Questo può anche avere un effetto aggiuntivo sugli elementi correlati come collegamenti, segnalibri e altri.
      * L’ereditarietà dei contenuti nelle rispettive pagine Live Copy viene aggiornata per riflettere la nuova posizione del relativo sorgente nella blueprint.
      * Per realizzare completamente lo spostamento di una pagina da una blueprint a una Live Copy, considera le [best practice per lo spostamento delle pagine.](#page-move)

### Best practice per lo spostamento delle pagine {#page-move}

Quando progetti lo spostamento di pagine in una Live Copy, considera la seguente best practice.

>[!NOTE]
>
>I seguenti elementi funzioneranno solo con il [trigger durante il rollout](live-copy-sync-config.md#rollout-triggers).

1. Crea una configurazione di rollout personalizzata.
   * Questa nuova configurazione deve includere l’azione `PageMoveAction`.
   * Non aggiungere altre azioni a questa configurazione.
1. Posiziona la nuova configurazione.
   * Per eseguire il rollout completo della pagina, spostala durante l’eliminazione della rispettiva pagina nella posizione precedente nella Live Copy:
      * Posiziona la configurazione appena creata prima della configurazione di rollout standard. La configurazione di rollout standard si occuperà di eliminare le pagine nelle loro posizioni precedenti.
      * Per distribuire lo spostamento della pagina mantenendo le rispettive pagine nelle vecchie posizioni in Live Copy (essenzialmente duplicando il contenuto):
         * Posiziona la configurazione appena creata dopo la configurazione di rollout standard. In questo modo nessun contenuto verrà eliminato nella Live Copy o disattivato dalla pubblicazione.

## Personalizzazione dei rollout {#customizing-rollouts}

Le configurazioni di rollout MSM sono altamente personalizzabili. Tieni presente che automatizzare i rollout può avere conseguenze di vasta portata. Come best practice, devi pianificare con molta attenzione prima di intraprendere le seguenti attività:

* Automatizzare i rollout, ad esempio con [trigger onModify](#onmodify)
* Personalizzare [tipi di nodo/proprietà](#node-types-properties)
* Avvio dei flussi di lavoro successivi
* Attivazione di contenuti come parte dei rollout

### onModify {#onmodify}

Quando utilizzi il [trigger di rollout](live-copy-sync-config.md#rollout-triggers) `onModify` tieni presente che:

* L&#39;automazione dei rollout con i trigger `onModify` può avere un impatto negativo sulle prestazioni dell&#39;authoring, in quanto attiva i rollout dopo ogni modifica della pagina.
* Il risultato del rollout può differire da quello previsto, ad esempio:
   * Non puoi specificare l’ordine degli eventi di modifica risultanti.
   * L&#39;architettura basata su eventi non può garantire la sequenza degli eventi passati al Rollout Manager.
* L’utilizzo di tale configurazione di rollout potrebbe causare conflitti se si verificano aggiornamenti simultanei della stessa risorsa.

Pertanto, ti consigliamo di utilizzare i trigger `onModify` solo se i vantaggi dell&#39;avvio automatico di rollout superano eventuali problemi di prestazioni.

### Tipi di nodo/proprietà {#node-types-properties}

Oltre a personalizzare le azioni di rollout, MSM ti consente anche di personalizzare le proprietà dei nodi in fase di rollout. Il [La configurazione MSM OSGi consente di escludere i tipi di nodo](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) dall&#39;origine alla Live Copy.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni su MSM e Live Copy, consulta i seguenti articoli.

* [Creazione e sincronizzazione di Live Copy](creating-live-copies.md)
* [Panoramica Live Copy](live-copy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](live-copy-sync-config.md)
* [Conflitti di rollout MSM](rollout-conflicts.md)
