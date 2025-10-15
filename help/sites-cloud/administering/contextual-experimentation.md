---
title: Sperimentazione contestuale in AEM as a Cloud Service
description: Scopri come utilizzare il plug-in di sperimentazione per aggiungere funzionalità di sperimentazione al sito.
feature: Administering
role: Admin
source-git-commit: 66ee08babae1f6640158260af051f8ad5f9bde85
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 0%

---

# Sperimentazione contestuale in AEM as a Cloud Service {#contextual-experimentation}

>[!NOTE]
>Attualmente, la funzione di sperimentazione contestuale è disponibile solo tramite il programma beta. Contatta il supporto Adobe o il tuo account manager per accedere al programma beta.

La sperimentazione è la pratica di testare la progettazione, le funzionalità e il codice del sito per migliorarne le prestazioni e renderlo più efficace e semplice. Ciò si ottiene modificando il contenuto o la funzionalità, confrontando i risultati con una versione precedente e scegliendo i miglioramenti che hanno effetti misurabili.

Se fatto correttamente, si tratta di un pattern potente per migliorare le conversioni, il coinvolgimento e l’esperienza del visitatore. In generale, ci sono un paio di problemi da evitare quando si cerca di adottare la pratica:

* **Troppo poco**: la maggior parte delle aziende non sta sperimentando a sufficienza e, quando lo fanno, sperimenta con troppo poco traffico per ottenere risultati significativi.
* **Troppo lento**: molti framework di sperimentazione rallentano il sito così tanto che le potenziali nuove conversioni non possono compensare il traffico perso e i mancati recapiti a causa di un rendering lento.
* **Troppo complesso**: se l&#39;impostazione di un nuovo esperimento richiede troppo tempo, verranno eseguiti meno esperimenti.

Per i siti in esecuzione su Adobe Experience Manager, è disponibile il **plug-in di sperimentazione** &quot;pronto all&#39;uso&quot; che consente agli sviluppatori di aggiungere una funzionalità di sperimentazione ai propri siti. Tre cose rendono questo approccio diverso da altri quadri di sperimentazione:

* È facile impostare i test con gli strumenti che gli autori hanno già familiarità e non è necessario alcun accesso separato.
* È profondamente integrato nel sistema di consegna di AEM, non rallenta il tuo sito ed è resiliente alle modifiche nel codice e nei contenuti.
* Consente di testare semplici modifiche ai contenuti e di eseguire esperimenti su progettazione, funzionalità e codice.

## Prima di iniziare {#before-start}

Il plug-in di sperimentazione viene utilizzato nel contesto di [Edge Delivery Services](/help/edge/overview.md), pertanto sarà necessario un account Github, un archivio di contenuti come SharePoint o Google Drive e anche il [AEM Sidekick](https://www.aem.live/docs/sidekick). Vedere anche la [Guida introduttiva - Esercitazione per sviluppatori di Universal Editor](https://www.aem.live/developer/tutorial) e la [Guida introduttiva - Esercitazione per sviluppatori](https://www.aem.live/developer/tutorial).

Dopo aver configurato tutto, **guarda questo video** intitolato [Sperimentazione immediata](https://business.adobe.com/it/products/experience-manager/sites/testing-optimization.html) per una breve dimostrazione del funzionamento del plug-in di sperimentazione.

## Termini utilizzati di frequente {#frequently-used-terms}

Prima di seguire il resto della guida per configurare il primo esperimento, dovresti conoscere alcuni termini utilizzati di frequente:

* **Controllo**: l&#39;esperienza precedente all&#39;esecuzione dell&#39;esperimento. Tutti gli esperimenti tentano di testare e dimostrare un miglioramento rispetto all’esperienza di controllo.
* **Sfida**: un&#39;esperienza diversa dall&#39;esperienza di controllo e &quot;testata&quot; rispetto a essa o insieme ad essa.
* **Varianti**: controllo e sfidante sono tutte varianti di un esperimento.
* **Rilevanza statistica**: valutazione della capacità dello sfidante di superare il controllo. Calcolare la significatività statistica consente di escludere la fortuna e concentrarsi sui risultati che hanno un effetto reale.

## Varianti dell’esperimento e flusso di lavoro generale {#experiment-variants-workflow}

In generale, durante la configurazione di un esperimento utilizzerai una pagina preesistente come pagina di controllo. Creerai quindi una pagina sfidante che sostituirà la pagina di controllo per alcuni dei tuoi visitatori. Nella pagina della sfida puoi sottoporre a test elementi diversi, come varianti di contenuto, layout di pagina diversi, call-to-action (CTA) e così via. Puoi configurare queste varianti di esperimento aggiungendo parametri di metadati nella pagina di controllo (vedi di seguito).

Il [servizio di telemetria operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) raccoglie quindi i dati, ad esempio il numero di visitatori nella pagina di controllo rispetto alla pagina della sfida. Puoi quindi utilizzare questi dati per scegliere i miglioramenti necessari per il sito. Fintanto che rimani nel linguaggio di progettazione consolidato del tuo sito web e utilizzi la funzionalità di blocco esistente, dovresti essere in grado di impostare una variante di esperimento e inviarla in produzione in pochi minuti.

>[!NOTE]
>Il plug-in non utilizza, né persiste, alcun dato dell’utente finale che possa determinarne l’identificazione. Non è richiesto il consenso esplicito dell&#39;utente finale né il consenso dei cookie quando si utilizza la configurazione predefinita che utilizza il servizio di telemetria operativa [in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

### Identificatore esperimento {#experiment-identifier}

Prima di iniziare, ogni esperimento deve avere un proprio identificatore a scopo di tracciamento e analisi. Un buon punto di partenza è quello di trovare un buon identificatore univoco per l’esperimento, che sarà l’&quot;ID esperimento&quot;. Gli esperimenti sono spesso numerati in modo lineare o correlati al loro ID problema in un sistema di tracciamento o gestione dei problemi. Gli ID esperimento utilizzano spesso un prefisso per il progetto, ad esempio: `OPT-0134`, `EXP0004` o `CCX0076`.

### Crea la pagina Challenger {#create-challenger-page}

Per convenzione, si consiglia di creare una cartella con un ID esperimento minuscolo in `/experiments/ folder` (ad esempio /experiment/ccx0076/). Tutte le pagine per le varianti sfidante si trovano in questa cartella. È possibile creare questa cartella nel repository locale, ad esempio Sharepoint o Goggle Drive.

La cartella degli esperimenti deve avere un aspetto simile al seguente:

![esperimenti-cartella](/help/sites-cloud/administering/assets/experiments-folder.png)

Una volta creata la cartella, inserisci una copia della pagina di controllo in tale cartella e applica le modifiche alla pagina che desideri testare come parte della variante dell’esperimento (vedi il video precedente). Ad esempio, supponiamo che sul sito web sia presente la seguente pagina su cui desideri eseguire un esperimento:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

La copia dello sfidante inserita nella cartella `experiments/<experiment-id>` potrebbe essere simile alla seguente:

![pagina-sfidante](/help/sites-cloud/administering/assets/challenger-page.png)

Visualizzare in anteprima e pubblicare la pagina dello sfidante utilizzando la barra laterale e al termine dell&#39;authoring della pagina dello sfidante. L’URL dello sfidante pubblicato sarà utilizzato nella sezione successiva, che descrive come configurare l’esperimento.

### Configurazione dell’esperimento {#configure-experiment}

Non appena le pagine dello sfidante sono pronte, devi tornare alla pagina di controllo e aggiungere metadati che indicano che le pagine fanno ora parte del test.

Per una variante dell’esperimento è necessario aggiungere due righe di metadati.

* **Esperimento**: contenente l&#39;ID esperimento.

* **Varianti esperimento**: contenenti URL per tutti gli sfidanti di questa pagina, separati da interruzioni di riga se si dispone di più sfidanti.

Vedi l’esempio seguente:

![pagina-metadati](/help/sites-cloud/administering/assets/metadata-page.png)

Per ogni esperimento, il traffico viene suddiviso tra tutte le varianti (controllo e sfidanti) e viene automaticamente impostato su una distribuzione uniforme. Di conseguenza, se si dispone di uno sfidante, ci sarà automaticamente una divisione 50/50 tra il controllo e lo sfidante. Se avete due sfidanti, vedrete automaticamente un terzo del traffico assegnato al controllo e ogni sfidante e così via.

Puoi sovrascrivere la suddivisione del traffico configurando i metadati. Per ulteriori informazioni su come personalizzare i metadati utilizzati negli esperimenti, consulta la [pagina](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring) seguente.

### Anteprima e staging delle varianti dell’esperimento {#preview-stage-experiment}

Non appena sei pronto per visualizzare l’anteprima e l’area intermedia dell’esperimento, fai clic su Anteprima nella barra laterale in alto a sinistra. Ogni volta che visualizzi in anteprima una pagina con un esperimento in esecuzione, visualizzerai la sovrapposizione della sperimentazione nell&#39;ambiente di anteprima `.aem.page`. La sovrapposizione della sperimentazione consente di passare tra le varianti dell’esperimento e fornisce anche i dati sul traffico.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

La raccolta dati per misurare l&#39;efficacia di ogni variante si basa sul servizio di telemetria operativa [di AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

### Invia la variante dell’esperimento all’ambiente di produzione {#production-experiment}

Seleziona le pagine dell’esperimento e fai clic su Pubblica dalla barra laterale per spingere in diretta sia il controllo che le varianti dello sfidante.

### Esempi di casi d’uso {#use-case-examples}

Di seguito sono riportati diversi esempi di casi d’uso per varianti di esperimento. In generale, il flusso di lavoro di base sarà simile a quello descritto sopra, con modifiche particolari per ogni caso d’uso (come il numero di pagine di verifica o modifiche ai metadati).

#### Esperimento a pagina intera {#full-page}

Puoi utilizzare un esperimento di pagina intera per testare due varianti della stessa pagina. Questa è una variante a pagina intera di un test a/b in cui si dispone di un controllo e di una pagina di verifica. Sostituirai l’intero contenuto della pagina di controllo &quot;originale&quot; nella variante dello sfidante con un tipo diverso di contenuto. Tieni presente che per impostazione predefinita il traffico del cliente viene suddiviso in modo uniforme (50/50), ma puoi creare suddivisioni personalizzate, se lo desideri.

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

Di seguito sono riportati diversi altri aspetti da considerare quando si utilizza la sperimentazione di contesto.

### Conversione {#conversion}

Gli esperimenti sono impostati per la conversione degli indirizzi (tiene traccia degli elementi cliccabili sulla pagina). Tutti gli esperimenti devono essere definiti per i seguenti:

* Tipo di esperimento
* A quale blocco di esperienza si applicherà l’esperimento
* Quante varianti conterrà l’esperimento
* Qual è la composizione di ciascuna variante

### Assicurati che le varianti dell’esperimento non siano indicizzate {#experiment-not-indexed}

Durante l’esecuzione di esperimenti, in genere è consigliabile escludere le varianti dalla sitemap e assicurarsi che non siano indicizzate dai motori di ricerca. Questo perché la pagina della variante potrebbe essere vista come contenuto duplicato e avere un impatto negativo sull’ottimizzazione SEO (Search Engine Optimization).

A tale scopo, è possibile utilizzare uno dei due metodi seguenti:

* Se centralizzi tutti gli esperimenti in una cartella dedicata, come `/experiments`: assicurati che il foglio `metadata.xlsx` bulk contenga una riga con `/experiments/**` come percorso e una colonna robots con i valori `noindex`, `nofollow`.
* Se mantieni il controllo dell’esperimento e le varianti con il contenuto regolare: aggiungi una voce robot nei metadati della pagina per ogni variante, con il valore `noindex`, `nofollow`.

## Risorse tecniche e per sviluppatori {#dev-resources}

Adobe Experience Manager utilizza [telemetria operativa]&#x200B;(/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md

) per raccogliere dati operativi strettamente necessari per individuare e risolvere problemi funzionali e di prestazioni sui siti basati su Adobe Experience Manager. I dati di telemetria operativa possono essere utilizzati per diagnosticare problemi di prestazioni. La telemetria operativa mantiene la privacy dei visitatori attraverso il campionamento (verrà monitorata solo una piccola parte di tutte le visualizzazioni di pagina).

### Privacy {#privacy-experimentation}

[Il servizio di telemetria operativa in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta dei dati. In qualità di visitatore, Adobe non tenterà di raccogliere informazioni personali sull’utente o informazioni che possono essere tracciate. In qualità di gestore del sito, controlla gli elementi di dati raccolti di seguito per capire se richiedono il consenso.
La telemetria operativa AEM non utilizza alcun ID o stato lato client, ad esempio cookie o `localStorage`, `sessionStorage` o simili, per raccogliere le metriche di utilizzo. I dati vengono inviati in modo trasparente tramite una chiamata `Navigator.sendBeacon`, non tramite pixel o tecniche simili. Non esiste alcuna &quot;impronta digitale&quot; di dispositivi o singoli utenti tramite il loro indirizzo IP, stringa dell’agente utente o qualsiasi altro dato allo scopo di acquisire i dati campionati.

Non è consentito inserire dati personali nella raccolta dati di telemetria operativa né utilizzare dati di telemetria operativa per casi d’uso che vadano oltre lo stretto necessario.

### Domande frequenti {#faq}

Di seguito è riportato un elenco delle domande frequenti:

D: Posso regolare il rapporto di suddivisione tra le varianti del mio esperimento, ad esempio 10% sul controllo e 90% sullo sfidante?

Sì, il rapporto di suddivisione può essere configurato tramite [metadati](#configure-experiment).

D: Posso sperimentare sia su testo che su immagini?

Sì, la variante può essere una pagina completamente diversa e puoi anche testare le modifiche al layout.
