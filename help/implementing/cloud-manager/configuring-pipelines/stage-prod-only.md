---
title: Pipeline suddivise solo per staging e solo produzione
description: Scopri come suddividere le distribuzioni di staging e di produzione utilizzando pipeline dedicate.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: false
index: true
exl-id: 7d76a87c-122c-4c4d-8071-957bef4c9cf1
source-git-commit: 890d18778273ce60a676cb74fa8025d6b48dc70d
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 48%

---

# Dividere le pipeline solo stadio e solo produzione {#stage-prod-only}

<!-- REMOVED AS PER CQDOC-23086 ON OCTOBER 3, 2025:
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines" -->

Puoi suddividere le distribuzioni di staging e produzione utilizzando pipeline dedicate.

## Panoramica {#overview}

Gli ambienti di staging e produzione sono strettamente associati. Per impostazione predefinita, le distribuzioni ad essi sono collegate a una singola pipeline. Si tratta di una pipeline di distribuzione che distribuisce sia negli ambienti di staging che in quelli di produzione in tale programma. Sebbene questo tipo di associazione sia di norma adeguato, alcuni casi d’uso presentano degli svantaggi:

* Se desideri eseguire una distribuzione solo di staging, rifiuta il passaggio nella pipeline **Promuovi per produrre**. Tuttavia, l’esecuzione verrà contrassegnata come annullata.
* Se desideri distribuire il codice più recente in un ambiente di staging nella produzione, devi ridistribuire l’intera pipeline, inclusa la distribuzione di staging, anche se non è stato modificato alcun codice.
* Gli ambienti non possono essere aggiornati durante le distribuzioni. Se sospendi il test nell’ambiente di staging per diversi giorni prima di passare alla produzione, l’ambiente di produzione rimane bloccato e non può essere aggiornato. Questo scenario rende impossibili le attività non dipendenti come ad esempio l’aggiornamento delle [variabili di ambiente](/help/implementing/cloud-manager/environment-variables.md).

Le pipeline solo di staging e solo di produzione offrono soluzioni a questi casi d’uso fornendo opzioni di distribuzione dedicate.

* **Pipeline di distribuzione solo di staging:** vengono distribuite solo in un ambiente di staging con l’esecuzione che termina una volta completati la distribuzione e i test. Una pipeline solo di staging si comporta in modo identico alla pipeline di produzione full stack standard associata, ma senza i passaggi di distribuzione di produzione (approvazione, pianificazione, distribuzione).
* **Pipeline di distribuzione di sola produzione:** vengono distribuite solo in produzione selezionando l&#39;esecuzione della fase più recente con esito positivo. Quindi implementando i relativi artefatti in produzione. Le pipeline di sola produzione riutilizzano gli artefatti iper l’implementazione nell’ambiente di staging, ignorando la fase di build.

Le pipeline solo di staging e solo di produzione non vengono eseguite mentre è in corso una pipeline di produzione full stack e viceversa. Se sia la pipeline di produzione solo di staging che quella full stack dispongono del trigger **Cambiamenti su Git** configurato e indicano lo stesso ramo e archivio, viene avviata automaticamente la pipeline solo di staging. Le pipeline solo di produzione non avviano i **`On Git Changes`** perché non sono collegate direttamente a un archivio.

Le pipeline solo di produzione vengono attivate manualmente, in quanto non sono collegate direttamente a un archivio per **Cambiamenti su Git**.

Queste pipeline dedicate offrono maggiore flessibilità, ma tieni presente i dettagli dell’operazione e le raccomandazioni seguenti.

>[!NOTE]
>
>Le pipeline solo per produzione utilizzano sempre gli artefatti della pipeline solo per staging. Questo processo rimane valido anche se nel frattempo la pipeline di produzione standard associata ha implementato qualcos’altro per lo staging.
>
>* Tale scenario potrebbe causare rollback del codice indesiderati.
>* Adobe consiglia di interrompere l’utilizzo della pipeline di produzione standard associate dopo aver iniziato a utilizzare le pipeline solo di produzione e solo di staging.
>* Se decidi comunque di eseguire sia le pipeline standard associate che le pipeline solo per staging o produzione, considera di riutilizzare gli artefatti per evitare rollback del codice.

## Creazione di pipeline {#pipeline-creation}

Le pipeline solo di produzione e solo di staging vengono create in modo simile alle [pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) standard associate e alle [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Per informazioni dettagliate, consulta questi documenti.

1. Nella finestra delle **Pipeline**, fai clic su **Aggiungi pipeline**.

   * Seleziona **Aggiungi pipeline non di produzione** per [creare una pipeline per sola fase](#stage-only).
   * Seleziona **Aggiungi pipeline di sola produzione** per [creare una pipeline di sola produzione](#prod-only).

![Creazione di una pipeline solo di produzione/staging](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>Alcune opzioni potrebbero essere disattivate se le pipeline corrispondenti esistono già.
>
>* **Aggiungi pipeline solo di produzione** non sarà disponibile se non esiste ancora una pipeline solo di staging.
>* **Aggiungi pipeline di produzione** non sarà disponibile se esiste già una pipeline standard associata.
>* Sono consentite pipeline solo di produzione e solo di staging per programma.

### Creare una pipeline per sola fase {#stage-only}

1. Nella scheda **Configurazione** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il campo **Pipeline di distribuzione** per la pipeline.
1. Nel campo Nome pipeline non di produzione, inserisci un nome a testo libero.
1. Selezionare le opzioni di distribuzione desiderate, quindi fare clic su **Continua**.

   ![Scheda Configurazione nella finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. Nella scheda **Codice Source**, seleziona **Codice full stack**. Questa opzione crea e distribuisce l’intera applicazione AEM (back-end, configurazione a livello Dispatcher/web ed eventuali moduli front-end nell’archivio).

1. Nell&#39;elenco a discesa **Ambienti di distribuzione idonei**, selezionare l&#39;ambiente **stage** come ambiente di distribuzione per la pipeline. Selezionando staging viene creata una pipeline dedicata all’ambiente di staging (la promozione della produzione avviene tramite una pipeline separata).

1. Seleziona il **Archivio** e il **Ramo Git** nei rispettivi elenchi a discesa, quindi fai clic su **Continua**.

   ![Scheda Codice Source nella finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. Nella scheda **Audit dell&#39;esperienza**, l&#39;URL del sito specificato è l&#39;URL pubblicato che Cloud Manager controlla per la qualità delle pagine.

1. Nel campo **Percorso pagina**, specifica le pagine da controllare, quindi fai clic su **![Icona Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) Aggiungi pagina**.

   L’audit dell’esperienza analizza ogni percorso aggiunto per quanto riguarda prestazioni, accessibilità, app web progressive, best practice, SEO e altri controlli di qualità. Per aggiungere più percorsi e rimuoverne uno, fai clic sull&#39;icona ![Dimensioni incrociate 400](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg).

   ![Scheda Audit dell&#39;esperienza nella finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. Fai clic su **Salva**.


### Creare una pipeline di sola produzione {#prod-only}

1. Nella finestra di dialogo **Aggiungi pipeline di sola produzione**, immetti il nome libero della pipeline nel campo di testo **Nome pipeline**.
1. Nel campo **Nome pipeline** digitare il nome desiderato.
1. In **Opzioni di distribuzione di produzione**, seleziona **Sospendi prima della distribuzione in produzione**.

   Questa opzione inserisce un gate di approvazione manuale subito prima del passaggio di produzione. La pipeline si interrompe e attende che un approvatore (ad esempio un Responsabile della distribuzione o un Proprietario business) approvi o annulli la distribuzione di produzione.

   Utilizzare per il controllo delle modifiche o i controlli dell&#39;ultimo minuto.

1. Fai clic su **Salva** per creare la pipeline di sola produzione con queste opzioni.

   ![Creazione di una pipeline solo di produzione](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## Eseguire pipeline solo staging e solo produzione {#running}

È possibile avviare le nuove pipeline [come qualsiasi altra pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). Puoi anche attivare una pipeline di sola produzione direttamente dai dettagli di esecuzione di una pipeline di sola fase.

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### Eseguire pipeline di sola fase {#stage-only-run}

Nei dettagli di esecuzione, dopo i passaggi di test viene visualizzato un pulsante **Promuovi build**. Fai clic su di esso per attivare una pipeline di sola produzione che distribuisce gli artefatti dell’area di visualizzazione di questa esecuzione nell’ambiente di produzione. Il pulsante viene visualizzato solo sull’ultima esecuzione riuscita della sola fase.

![Esecuzione pipeline solo di staging](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

Quando fai clic su **Promuovi build**, viene visualizzata una finestra di dialogo che consente di confermare l&#39;esecuzione della pipeline correlata di sola produzione. Fai clic su **Esegui** per avviarlo.

![Promuovi compilazione - Finestra di dialogo Esegui pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

Se non ne esiste alcuna, viene visualizzata una finestra di dialogo di impostazione in cui viene richiesto di crearne una.

![Promuovi compilazione - Finestra di dialogo Nessuna pipeline valida](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### Eseguire pipeline di sola produzione {#prod-only-run}

Per una pipeline **solo produzione**, Cloud Manager visualizza gli artefatti di origine distribuiti in produzione. Controlla il passaggio **Preparazione artefatto** per l&#39;esecuzione di origine, quindi aprila per visualizzare i dettagli e i registri.


![Dettagli artefatto](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)
