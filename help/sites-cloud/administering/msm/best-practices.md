---
title: Best practice MSM
description: Scopri le best practice compilate dai team di progettazione e consulenza di Adobe per iniziare a utilizzare AEM Multi Site Manager.
feature: Gestione di più siti
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---


# Best practice MSM {#msm-best-practices}

## Generale {#general}

MSM è un framework configurabile per automatizzare la distribuzione dei contenuti. Le implementazioni spesso coinvolgono parti importanti di un sito web e si estendono su più organizzazioni e aree geografiche. È quindi vivamente consigliato pianificare le implementazioni MSM con la stessa attenzione che pianifichi il tuo sito web:

* Pianifica attentamente **la struttura e i flussi di contenuto** prima di avviare l&#39;implementazione.
* **Personalizza il più possibile, ma il meno possibile.** Anche se MSM supporta un elevato grado di personalizzazione (ad esempio configurazioni di rollout), in genere la best practice per le prestazioni, l’affidabilità e l’aggiornamento del sito web è quella di ridurre al minimo la personalizzazione.
* Stabilire un modello **governance** in anticipo e addestrare gli utenti di conseguenza per garantire il successo. Dal punto di vista della governance, una best practice consiste nel **ridurre al minimo l’autorità di cui dispongono i produttori di contenuti locali** per allocare/collegare contenuti ad altri utenti locali e alle rispettive Live Copy. Ciò è dovuto al fatto che le ereditarietà non gestite e incatenate possono aumentare notevolmente la complessità di una struttura MSM e comprometterne le prestazioni e l&#39;affidabilità.
* Quando esiste un piano per la struttura, i flussi di contenuto, l&#39;automazione e la governance, **prototipo e test completo del sistema** prima di avviare un&#39;implementazione live.
* Tieni presente che **Adobe Consulting and Lead System Integrators** dispongono di una pianificazione approfondita dell&#39;esperienza e dell&#39;implementazione dell&#39;automazione dei contenuti con MSM, in modo che possano aiutarti a iniziare con il tuo progetto MSM e l&#39;intera implementazione.

## Origini Live Copy e configurazioni Blueprint {#live-copy-sources-and-blueprint-configurations}

Tieni presente che una Live Copy può essere creata utilizzando le pagine [normali](creating-live-copies.md#creating-a-live-copy-of-a-page) o una [configurazione blueprint](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Entrambi sono casi d’uso validi.

I vantaggi aggiuntivi dell’utilizzo di una configurazione blueprint sono i seguenti:

* Consenti all’autore di utilizzare l’opzione **Rollout** su una blueprint per inviare in modo esplicito modifiche alle Live Copy che ereditano da questa blueprint.
* Consenti all&#39;autore di utilizzare **Crea sito** per selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definisci una configurazione di rollout predefinita per le Live Copy che hanno una relazione con la blueprint.

Nel caso in cui non venga fatto riferimento a una configurazione di blueprint, i rollout possono essere avviati solo dalle Live Copy stesse, essenzialmente richiamando il contenuto dalla sorgente.

Quando crei un nuovo sito con Live Copy, è vantaggioso creare configurazioni blueprint per garantire la disponibilità dell’intero set di funzioni MSM.

## Componenti e sincronizzazione dei contenitori {#components-and-container-synchronization}

In generale, la regola di rollout in MSM per quanto riguarda la sincronizzazione dei componenti è:

* I componenti vengono implementati per sincronizzare tutte le risorse contenute nel blueprint.
* I contenitori sincronizzano solo la risorsa corrente.

Ciò significa che i componenti sono trattati come un aggregato e in un rollout il componente stesso e tutti i suoi figli vengono sostituiti con quelli nei progetti. Ciò significa che se una risorsa viene aggiunta localmente a tale componente, andrà persa per il contenuto della blueprint al momento del rollout.

Per supportare la nidificazione dei componenti in modo che i componenti aggiunti localmente siano mantenuti in un rollout, il componente deve essere dichiarato come contenitore.

>[!NOTE]
>
>Aggiungi la proprietà `cq:isContainer` al componente per designarlo come contenitore.

## Crea sito {#create-site}

AEM dispone di due approcci principali per la creazione di Live Copy:

* Quando [crei una Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page) - Questo può essere considerato come l’approccio più generico, che consente di creare Live Copy da qualsiasi pagina. La struttura del contenuto di una Live Copy corrisponde esattamente alla sorgente.

* Quando [crei un sito](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) - Si tratta di un approccio più specializzato, principalmente per la creazione di siti web con una struttura multilingue.

Di seguito sono riportate alcune considerazioni da tenere a mente durante la creazione di un sito:

* Per creare un nuovo sito, è necessaria una [configurazione blueprint](creating-live-copies.md#managing-blueprint-configurations).
* Per consentire la selezione dei percorsi linguistici da creare in un nuovo sito, le radici della lingua corrispondenti devono esistere nella blueprint (sorgente).
* Una volta creato un [nuovo sito come Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (utilizzando **Crea** e **Sito**), i primi due livelli di questa Live Copy sono *superficiali*. Gli elementi figlio della pagina non appartengono alla relazione in tempo reale, ma se viene trovata una relazione in tempo reale corrispondente al trigger, verrà comunque generato un rollout.

È utile evitare:

* Aggiunta manuale di lingue nella blueprint (sotto il primo livello).
* Aggiungendo manualmente il contenuto direttamente sotto la directory principale della lingua, poiché questo non comporta il trasferimento automatico del nuovo contenuto alla Live Copy al momento del rollout.

## Siti web MSM e multilingue {#msm-and-multilingual-websites}

MSM può contribuire alla creazione di siti web multilingue in due modi:

Quando crei un master lingua, tieni presente quanto segue:

* Anche se MSM stesso **non fornisce la traduzione dei contenuti**, può essere integrato con i connettori di traduzione di terze parti che lo fanno. Nota che:
   * MSM consente di annullare l’ereditarietà a livello di pagina e/o componente. Questo aiuta a evitare la sovrascrittura dei contenuti tradotti (da una Live Copy, con contenuti non ancora tradotti da una blueprint) al prossimo rollout.
      * Alcuni connettori di traduzione di terze parti automatizzano questa gestione delle ereditarietà MSM.
      * Per ulteriori informazioni, rivolgersi al provider di servizi di traduzione.
      * Un approccio alternativo per la creazione e la traduzione di master in lingua consiste nell’utilizzare copie in lingua insieme AEM framework di integrazione della traduzione preconfigurato.

Per ulteriori informazioni, consulta [Traduzione di contenuti per siti multilingue](/help/sites-cloud/administering/translation/overview.md) e le [Best practice per la traduzione.](/help/sites-cloud/administering/translation/best-practices.md)

## Modifiche alla struttura e rollout {#structure-changes-and-rollouts}

Le modifiche alla struttura del contenuto in una struttura blueprint/sorgente vengono riportate in modo diverso in una Live Copy. Dipende dal tipo di modifica:

* **** La creazione di nuove pagine in una blueprint determina la creazione delle pagine corrispondenti in Live Copy dopo il rollout con la configurazione di rollout standard.
* **** L’eliminazione delle pagine in una blueprint comporta l’eliminazione delle pagine corrispondenti da Live Copy dopo il rollout con configurazione di rollout standard.
* **** Lo spostamento delle pagine in una blueprint  **** non comporta lo spostamento delle pagine corrispondenti in Live Copy dopo il rollout con configurazione di rollout standard:
   * Questo comportamento si spiega con il fatto che lo spostamento di una pagina include implicitamente l’eliminazione di una pagina. Questo potrebbe causare un comportamento imprevisto al momento della pubblicazione, in quanto l’eliminazione delle pagine sull’autore disattiva automaticamente il contenuto corrispondente al momento della pubblicazione. Questo può anche avere un effetto aggiuntivo sugli elementi correlati come collegamenti, segnalibri e altri.
      * L’ereditarietà dei contenuti nelle rispettive pagine Live Copy viene aggiornata per riflettere la nuova posizione delle relative origini nella blueprint.
      * Per realizzare completamente lo spostamento di una pagina da una blueprint a Live Copy, considera le [best practice per lo spostamento delle pagine.](#page-move)

### Tecniche consigliate per lo spostamento delle pagine {#page-move}

Quando consideri lo spostamento di pagine in una Live Copy, considera la seguente best practice.

>[!NOTE]
>
>Quanto segue funziona solo con il trigger [Al momento del rollout](live-copy-sync-config.md#rollout-triggers).

1. Crea una configurazione di rollout personalizzata.
   * Questa nuova configurazione deve includere l&#39;azione `PageMoveAction`.
   * Non aggiungere altre azioni a questa configurazione.
1. Posiziona la nuova configurazione.
   * Per eseguire il rollout completo della pagina, sposta durante l’eliminazione delle rispettive pagine nella posizione precedente nella Live Copy:
      * Posiziona la configurazione appena creata prima della configurazione di rollout standard. La configurazione di rollout standard si occuperà di eliminare le pagine nelle loro posizioni precedenti.
      * Per distribuire lo spostamento della pagina mantenendo le rispettive pagine nelle vecchie posizioni in Live Copy (essenzialmente duplicando il contenuto):
         * Posiziona la configurazione appena creata dopo la configurazione di rollout standard. In questo modo nessun contenuto verrà eliminato nella Live Copy o disattivato dalla pubblicazione.

## Personalizzazione dei rollout {#customizing-rollouts}

Le configurazioni di rollout MSM sono altamente personalizzabili. Tieni presente che automatizzare i rollout può avere conseguenze di vasta portata. Come best practice, devi pianificare con molta attenzione prima di intraprendere le seguenti attività:

* Automazione di rollout, ad esempio con [onModify triggers](#onmodify)
* Personalizzazione di [tipi di nodo/proprietà](#node-types-properties)
* Avvio dei flussi di lavoro successivi
* Attivazione di contenuti come parte dei rollout

### onModify {#onmodify}

Quando utilizzi il [trigger di rollout](live-copy-sync-config.md#rollout-triggers) `onModify`, tieni presente quanto segue:

* L’automazione dei rollout con i trigger `onModify` può avere un impatto negativo sulle prestazioni di authoring in quanto attivano i rollout dopo ogni modifica della pagina.
* Il risultato del rollout può differire da quello previsto come:
   * Non è possibile specificare l’ordine degli eventi di modifica risultanti.
   * L&#39;architettura basata su eventi non può garantire la sequenza degli eventi passati al Rollout Manager.
* L’utilizzo di tale configurazione di rollout potrebbe causare conflitti se si verificano aggiornamenti simultanei della stessa risorsa.

Pertanto, si consiglia di utilizzare solo i trigger `onModify` se i vantaggi dell’avvio automatico di rollout superano eventuali problemi di prestazioni.

### Tipi di nodo/proprietà {#node-types-properties}

Oltre a personalizzare le azioni di rollout, MSM ti consente anche di personalizzare le proprietà dei nodi in fase di rollout. La configurazione [MSM OSGi ti consente di escludere i tipi di nodo](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) dalla copia dall&#39;origine alla Live Copy.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni su MSM e Live Copy, consulta i seguenti articoli .

* [Creazione e sincronizzazione di Live Copy](creating-live-copies.md)
* [Console Panoramica di Live Copy](live-copy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](live-copy-sync-config.md)
* [Conflitti di rollout MSM](rollout-conflicts.md)
