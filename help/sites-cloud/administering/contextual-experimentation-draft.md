---
title: Sperimentazione contestuale in AEM as a Cloud Service
description: Scopri come utilizzare la barra di sperimentazione per aggiungere funzionalità di sperimentazione al sito.
feature: Administering
role: Admin
source-git-commit: c948abf5391e61f01912f769b17e1ac0bd81a745
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 2%

---

# Sperimentazione contestuale in AEM as a Cloud Service {#contextual-experimentation}

La sperimentazione è la pratica di testare la progettazione, le funzionalità e il codice del sito per migliorarne le prestazioni e renderlo più efficace e semplice. Ciò si ottiene modificando il contenuto o la funzionalità, confrontando i risultati con una versione precedente e scegliendo i miglioramenti che hanno effetti misurabili.

Se fatto correttamente, si tratta di un pattern potente per migliorare le conversioni, il coinvolgimento e l’esperienza del visitatore. In generale, ci sono un paio di problemi da evitare quando si cerca di adottare la pratica:

* **Troppo poco**: la maggior parte delle aziende non sta sperimentando a sufficienza e, quando lo fanno, sperimenta con troppo poco traffico per ottenere risultati significativi.
* **Troppo lento**: molti framework di sperimentazione rallentano il sito a tal punto che le potenziali nuove conversioni non possono compensare la perdita di traffico e i mancati recapiti dovuti al rendering lento.
* **Troppo complesso**: se l&#39;impostazione di un nuovo esperimento richiede troppo tempo, verranno eseguiti meno esperimenti.

Per i siti in esecuzione su Adobe Experience Manager, gli sviluppatori hanno la possibilità di aggiungere una nuova funzionalità di sperimentazione ai loro siti. Tre cose rendono questo approccio diverso da altri quadri di sperimentazione:

* È facile impostare i test con gli strumenti che gli autori hanno già familiarità e non è necessario alcun accesso separato.
* È profondamente integrato nel sistema di consegna di AEM, non rallenta il tuo sito ed è resiliente alle modifiche nel codice e nei contenuti.
* Consente di testare semplici modifiche ai contenuti e di eseguire esperimenti su progettazione, funzionalità e codice.

## Barra di sperimentazione {#experimentation-rail}

La barra di sperimentazione è il modo principale per impostare gli esperimenti. Può essere utilizzato con il progetto in un contesto [Edge Delivery Services](/help/edge/overview.md) o in [Universal Editor](/help/implementing/universal-editor/introduction.md). Di conseguenza, sarà necessario un account Github, un archivio dei contenuti come SharePoint o Google Drive e il plug-in [AEM Sidekick](https://www.aem.live/docs/sidekick). Se desideri utilizzare l&#39;editor universale, dovrai anche accedere a un [ambiente AEM as a Cloud Service](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Vedere anche la [pagina della guida introduttiva - Esercitazione per sviluppatori di Universal Editor](https://www.aem.live/developer/tutorial).

>[!WARNING]
>Il motore di sperimentazione è necessario per utilizzare la capacità di sperimentazione. Assicurati che il motore sia installato e aggiornato correttamente prima di implementare i passaggi seguenti. Per ulteriori dettagli, vedere la [pagina di installazione](https://github.com/adobe/aem-experimentation/tree/v2?tab=readme-ov-file#installation) seguente.

### Impostazione della sperimentazione utilizzando AEM Sidekick in Edge Delivery Services

Per accedere alle funzionalità della barra di sperimentazione all&#39;interno del progetto Edge Delivery Services è necessario il plug-in [AEM Sidekick](https://www.aem.live/docs/sidekick). Per impostare la barra laterale, effettuare le seguenti operazioni:

1. Aggiungi l&#39;estensione della barra laterale [AEM](https://chromewebstore.google.com/search/AEM%20Sidekick?hl=en-US&utm_source=ext_sidebar) e fissala nel browser.
1. Apri la pagina del progetto in modalità anteprima.
1. Sulla barra di AEM Sidekick fare clic sull&#39;icona Impostazioni ![Impostazioni](/help/sites-cloud/administering/assets/settings-1.png) e selezionare **Aggiungi il progetto**.
1. Fai clic sulla scheda Sperimentazione per aprire la barra di sperimentazione.

### Impostazione della sperimentazione nell’editor universale

Prima di impostare gli esperimenti, tieni presente che per poter creare in Universal Editor dovrai utilizzare i siti AEM come origine di contenuto. Se necessario, puoi convertire il progetto esistente in siti AEM come origine di contenuto seguendo l&#39;esercitazione presentata nella pagina [Configura AEM Sites come Source di contenuto](https://www.aem.live/developer/ue-tutorial). Quando sei pronto a configurare esperimenti in Universal Editor, segui questi passaggi:

1. Apri il progetto in Universal Editor e controlla l&#39;estensione icona **A/B**. Nel caso in cui l’icona non sia visibile, verifica di aver abilitato la funzione nel gestore estensioni. Se non è abilitata, abilitala o richiedi l’accesso.
   <!--1. Open your GitHub repository and check if the `plugins/experimention` folder exists. If not, you will need to set up the experimentation engine and MFE first (see the note above).-->
1. Puntare la configurazione di `fstab.yaml` alla configurazione del progetto e collegarla all&#39;istanza di authoring di AEM. Vedi anche [Collegare il codice al contenuto](https://www.aem.live/developer/ue-tutorial#connect-your-code-to-your-content)
1. Apri l’istanza di AEM e, se il progetto è pronto, aprilo direttamente in Universal Editor.
1. Apri il progetto e la pagina dell&#39;indice in cui desideri eseguire gli esperimenti e fai clic su **Modifica** nella barra superiore.
1. Fai clic sull’icona A/B per aprire l’estensione di sperimentazione.

>[!NOTE]
>In caso di problemi durante la configurazione della sperimentazione per il progetto, contattare `aem-contextual-experimentation@adobe.com`.

>[!NOTE]
>Per ulteriori dettagli su come impostare e configurare il motore di sperimentazione, consulta la sezione della documentazione dal seguente [archivio](https://github.com/adobe/aem-experimentation/tree/v2-ui) .

## Varianti dell’esperimento e flusso di lavoro generale {#experiment-variants-workflow}

Prima di seguire il resto della guida per configurare il primo esperimento, è necessario conoscere alcuni termini utilizzati di frequente:

* **Controllo**: l&#39;esperienza precedente all&#39;esecuzione dell&#39;esperimento. Tutti gli esperimenti tentano di testare e dimostrare un miglioramento rispetto all’esperienza di controllo.
* **Sfida**: un&#39;esperienza diversa dall&#39;esperienza di controllo e &quot;testata&quot; rispetto a essa o insieme ad essa.
* **Varianti**: controllo e sfidante sono tutte varianti di un esperimento.
* **Significatività statistica**: valutare se lo sfidante è davvero migliore del controllo. Calcolare la significatività statistica consente di escludere la fortuna e concentrarsi sui risultati che hanno un effetto reale.

In generale, durante la configurazione di un esperimento utilizzerai una pagina preesistente come pagina di controllo. Utilizzando la barra di sperimentazione, creerai una pagina sfidante che è inizialmente una copia della pagina di controllo. Nella pagina della sfida puoi sottoporre a test elementi diversi, come varianti di contenuto, layout di pagina diversi, call-to-action (CTA) e così via. Puoi anche utilizzare le varianti generate da IA, utilizzando la funzionalità **Genera variante** nella barra di sperimentazione.

Per ogni esperimento, il traffico viene inizialmente suddiviso 50/50 tra il controllo e lo sfidante, ma puoi configurare il modo in cui il traffico viene suddiviso in base alle esigenze. Dopo aver attivato l’esperimento, riceverai dati tramite il servizio di telemetria operativa.

Il [servizio di telemetria operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) raccoglie dati, ad esempio il numero di visitatori nella pagina di controllo rispetto alla pagina della sfida. Puoi quindi utilizzare questi dati per scegliere i miglioramenti necessari per il sito. Fintanto che rimani nel linguaggio di progettazione consolidato del tuo sito web e utilizzi le funzionalità esistenti, dovresti essere in grado di impostare una variante di esperimento e inviarla in produzione in pochi minuti.

>[!NOTE]
>Il plug-in non utilizza, né persiste, alcun dato dell’utente finale che possa determinarne l’identificazione. Non è richiesto il consenso esplicito dell&#39;utente finale né il consenso dei cookie quando si utilizza la configurazione predefinita che utilizza il servizio di telemetria operativa [in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

<!--### Frequently used terms {#frequently-used-terms}

Before following the rest of the guide to set up your first experiment, there are a few frequently used terms that you should be familiar with:

* **Control**: the experience prior to running the experiment. All experiments try to test and demonstrate an improvement over the control experience.
* **Challenger**: an experience that is different from the control experience and is "tested" against it or alongside it.
* **Variants**: control and challenger are all variants of an experiment.
* **Statistical Significance**: Evaluating if your challenger is really better than the control. Calculating statistical significance allows you to rule out luck and concentrate on the results that have a real effect. -->

### Creazione di esperimenti nell’editor universale

Per utilizzare le funzionalità di sperimentazione nell’editor universale, devi innanzitutto impostare la barra di sperimentazione come descritto nei capitoli presentati in precedenza e assicurarti di utilizzare i siti AEM come origine di contenuto. Dopo aver configurato tutto, segui questi passaggi.

### Inizia a modificare il progetto in Universal Editor

Apri l’istanza di AEM e, se il progetto è pronto, aprilo direttamente in Universal Editor. Se non disponi di un progetto pronto e AEM Sites configurato come origine di contenuto, crea un nuovo progetto standard dal modello fornito. Puoi collegare il tuo archivio o il nostro archivio di esempio per guidarlo [https://github.com/sudo-buddy/ue-experimentation](https://github.com/sudo-buddy/ue-experimentation). Vedere anche la pagina [Configurazione di AEM Sites as a Content Source](https://www.aem.live/developer/ue-tutorial). Dopo aver configurato il progetto, aprirlo e la pagina dell&#39;indice in cui desideri eseguire gli esperimenti e fare clic su **Modifica** nella barra superiore.

### Avviare l’estensione A/B

Fai clic sull&#39;icona **A/B** per aprire l&#39;estensione di sperimentazione. Al primo utilizzo, l’interfaccia sarà vuota. Fai clic su **Crea nuovo** per avviare un nuovo esperimento.

![a-b](/help/sites-cloud/administering/assets/a-b.png)

### Configurare i dettagli dell’esperimento

Alcuni dei valori dell’esperimento sono predefiniti, come segue:

**Tipo di esperimento**: test A/B (per il momento è supportato solo il tipo)
**Ottimizzazione per**: conversione (solo il tipo supportato per il momento)

È inoltre possibile rinominare l&#39;esperimento in modo più descrittivo, ad esempio `homepage-head-experiment`.

![Dettagli esperimento](/help/sites-cloud/administering/assets/exp-values.png)

### Aggiungi e modifica varianti

Prima di continuare, accertati di comprendere i concetti di sfidante e variante descritti in precedenza. Fai clic su **Aggiungi nuovo** per creare una variante di sfidante:

* Nella stessa scheda, si apre la pagina dello sfidante, che all&#39;inizio rappresenta solo una copia del controllo.
* Modificare la pagina direttamente nel contesto oppure fare clic su **Genera variante** per utilizzare l&#39;assistenza AI.
* Dopo aver apportato le modifiche, torna all’estensione per procedere.

![Variante di controllo](/help/sites-cloud/administering/assets/control-variant.png)

### Definire altre proprietà e salvare come bozza

Nella barra di sperimentazione è possibile impostare una data di inizio e una data di fine (entrambe facoltative). Se non viene fornita una data di inizio, il test inizia una volta pubblicato. Se non viene fornita una data di fine, il test viene eseguito indefinitamente. Puoi anche regolare la suddivisione del traffico, consigliamo di iniziare con una suddivisione pari a 50/50.

Al termine, fai clic su **Salva**. L&#39;esperimento verrà salvato come bozza. L’esperimento non è ancora attivo. Puoi tornare alla panoramica facendo clic su **Torna all&#39;esperimento** oppure puoi rimanere nell&#39;interfaccia Modifica per attivare l&#39;esperimento.

![Bozza](/help/sites-cloud/administering/assets/draft-save.png)

### Attiva l’esperimento

Quando sei pronto, fai clic su **Attiva** per avviare l&#39;esperimento e pubblicare la pagina dell&#39;esperimento. Il test inizierà a raccogliere i dati di telemetria operativa (RUM) (vedi ulteriori dettagli nei capitoli seguenti).

![Attiva](/help/sites-cloud/administering/assets/activate.png)

### Monitorare e promuovere

Dopo che l&#39;esperimento ha raggiunto la rilevanza statistica, fare clic su **Promuovi** per rendere la variante desiderata il nuovo controllo. Tieni presente che puoi promuovere la variante dell’esperimento in qualsiasi punto dopo l’attivazione, anche se non raggiunge la rilevanza statistica.

### Utilizzo della sperimentazione con AEM Sidekick in Edge Delivery Services

Se hai installato la barra laterale di AEM, puoi utilizzare la barra di sperimentazione direttamente con il progetto in Edge Delivery Service senza utilizzare Universal Editor. La funzionalità è essenzialmente la stessa del test A/B descritto in precedenza, tieni presente che devi essere in modalità **Anteprima** per modificare e configurare il test. Dopo aver completato la configurazione del test, fare clic su **Attiva** per inviare in diretta sia il controllo che la variante della sfida e iniziare a raccogliere i dati di telemetria.

<!-- ### Experiment Identifier {#experiment-identifier}

Before you start, every experiment should have its own identifier for tracking and analytics purposes. A good starting point is to come up with a good, unique identifier for your experiment which will be the “Experiment ID”. Experiments are often numbered linearly or correlated to their Issue ID in an issue tracker or management system. Experiment IDs often use a prefix for the project, for example: `OPT-0134`, `EXP0004` or `CCX0076`.

### Create your Challenger Page {#create-challenger-page}

By convention, it is recommended to create a folder with a lowercase experiment ID in your `/experiments/ folder` (for example /experiments/ccx0076/). All the pages for the challenger variants are located in this folder. You create this folder in your local repository, for example, Sharepoint or Goggle Drive.

Your experiments folder should look something like this:

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

Once the folder is created, put a copy of your control page into that folder, and apply the changes on the page that you would like to test as part of your experiment variant (see video above). As an example let’s assume we have the following page on the website that we want to run an experiment on:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

Your copy of the challenger placed in the experiments/experiment-id folder might look like this:

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

Preview and publish the challenger page using the sidekick and when you are done authoring the challenger page. The URL of the published challenger will be used in the next section - configuring the experiment.

### Configuring the experiment {#configure-experiment}

As soon as the challenger pages are ready to go, you need to go back to the control page and add metadata indicating that the page(s) are now part of the test.

There are two metadata rows that need to be added for an experiment variant.

* **Experiment**: containing your experiment ID.

* **Experiment Variants**: containing URLs for all the challengers of this page, separated by line breaks if you have more than one challenger.

See the example below:

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

For each experiment, the traffic is split between all the variants (control and challengers) and is automatically set to an even distribution. As such, if you have one challenger, there will automatically be an even 50/50 split between control and the challenger. If you have two challengers, you will automatically see a third of the traffic allocated to control and each challenger and so on.

You can override the traffic split by configuring the metadata. For more information on how you can customize the metadata used in your experiments, see the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Preview and Stage your Experiment Variants {#preview-stage-experiment}

As soon as you are ready to preview and stage your experiment, click Preview from the side-kick in the upper left side. Whenever you are previewing a page that has a running experiment, you will see the experimentation overlay in your `.aem.page` preview environment. The experimentation overlay lets you switch between the experiment variants and also provides traffic data.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

<!--- The data collection to measure the effectiveness of each variant is based on the [Operational Telemetry service in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md). -->

<!--- ### Send your Experiment Variant to Production {#production-experiment}

Select the experiment pages and click Publish from the side-kick to push both the control and the challenger variant(s) live.

### Use Case Examples {#use-case-examples}

Presented below are several use case examples for experiment variants. Generally speaking, the basic worklflow will be similar to the one described above, with particular changes for each use case (like the number of challenger pages or metadata changes).

#### Full Page Experiment {#full-page}

You use a full page experiment to test between two variants of the same page. This is a full page variant of an a/b test where you have a control and a challenger page. You will replace the whole content of the "original" control page in the challenger variant with a different type of content. Keep in mind that by default the customer traffic is split evenly (50/50), but you can create custom splits if you like. -->

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## Altre considerazioni {#other-considerations}

Di seguito sono illustrati diversi aspetti da considerare quando si utilizza la sperimentazione di contesto.

### Conversione {#conversion}

Gli esperimenti sono impostati per la conversione degli indirizzi (tiene traccia degli elementi cliccabili sulla pagina). Attualmente, supportiamo gli esperimenti a livello di pagina con un esperimento per pagina.

<!--### Make sure experiment Variants are not indexed {#experiment-not-indexed}

When running experiments, it is usually best practice to exclude the variants from the sitemap and ensure they are not indexed by search engines. This is because the variant page could be seen as duplicate content and negatively impact SEO.

You can do this by using either of the following two methods:

* If you centralize all experiments in a dedicated folder, like `/experiments`: make sure your bulk `metadata.xlsx` sheet contains a row with `/experiments/**` as path, and a robots column with the values `noindex`, `nofollow`.
* If you keep the experiment control and variants with the regular content: add a robots entry in the page metadata for each variant, with the value `noindex`, `nofollow`.-->

## Risorse tecniche e per sviluppatori {#dev-resources}

Adobe Experience Manager utilizza la [telemetria operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) per raccogliere i dati delle operazioni strettamente necessari per individuare e risolvere i problemi funzionali e di prestazioni sui siti basati su Adobe Experience Manager. I dati di telemetria operativa possono essere utilizzati per diagnosticare problemi di prestazioni. La telemetria operativa mantiene la privacy dei visitatori attraverso il campionamento (verrà monitorata solo una piccola parte di tutte le visualizzazioni di pagina).

### Privacy {#privacy-experimentation}

[Il servizio di telemetria operativa in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta dei dati. In qualità di visitatore, Adobe non tenterà di raccogliere informazioni personali sull’utente o informazioni che possono essere tracciate. In qualità di gestore del sito, controlla gli elementi di dati raccolti di seguito per capire se richiedono il consenso.
La telemetria operativa AEM non utilizza alcun ID o stato lato client, ad esempio cookie o `localStorage`, `sessionStorage` o simili, per raccogliere le metriche di utilizzo. I dati vengono inviati in modo trasparente tramite una chiamata `Navigator.sendBeacon`, non tramite pixel o tecniche simili. Non esiste alcuna &quot;impronta digitale&quot; di dispositivi o singoli utenti tramite il loro indirizzo IP, stringa dell’agente utente o qualsiasi altro dato allo scopo di acquisire i dati campionati.

Non è consentito inserire dati personali nella raccolta dati di telemetria operativa né utilizzare dati di telemetria operativa per casi d’uso che vadano oltre lo stretto necessario.
