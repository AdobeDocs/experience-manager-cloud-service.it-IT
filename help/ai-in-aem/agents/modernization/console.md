---
title: Console di modernizzazione esperienza
description: Guida di riferimento per l’interfaccia e le funzionalità della Console di modernizzazione esperienza
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c2f258bfcfff8392af2863d874d4a4235f042193
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---


# Console di modernizzazione esperienza {#console-reference}

Guida di riferimento per l’interfaccia e le funzionalità della Console di modernizzazione esperienza

>[!NOTE]
>
>Se ti interessa utilizzare la console di modernizzazione esperienza, puoi richiedere l’accesso per garantire un’esperienza di onboarding fluida.

## Panoramica {#overview}

La console di modernizzazione esperienza è un ambiente di sviluppo ospitato e assistito da IA per Edge Delivery Services, esposto come interfaccia web in [`aemcoder.adobe.io`.](https://aemcoder.adobe.io) Dopo la connessione al progetto GitHub, è possibile iniziare immediatamente a richiedere le modifiche in lingua naturale senza ulteriori configurazioni o configurazioni dell&#39;ambiente locale.

>[!TIP]
>
>Se ti interessa iniziare subito a utilizzare la console, consulta il documento [Guida introduttiva all&#39;agente di modernizzazione esperienza.](/help/ai-in-aem/agents/modernization/getting-started.md)

## Funzionalità {#capabilities}

Funzionalità di base della console:

* Pannello di chat interattiva con l’agente e le sue competenze
* Anteprima live di AEM per un feedback visivo immediato sulle modifiche
* Browser dei file di contenuto e visualizzatore markdown
* Sincronizzazione contenuti con [Authoring documenti](https://da.live)
* Browser codici e visualizzatore differenze per rivedere le modifiche apportate
* Integrazione GitHub con possibilità di creare richieste pull da modifiche

Gli sviluppatori mantengono il pieno controllo sulle spedizioni. Tutte le modifiche apportate tramite la console richiedono revisione e approvazione prima dell’implementazione, garantendo governance, coerenza del brand e sicurezza.

## Navigazione {#navigation}

Dopo aver effettuato l&#39;accesso alla console alle [`aemcoder.adobe.io`,](https://aemcoder.adobe.io) si aprirà la schermata iniziale della console.

![Schermata iniziale della console](assets/console-home.png)

### Barra dei menu {#menu-bar}

La barra dei menu superiore fornisce:

* Un pulsante **Apri menu** a sinistra per espandere e comprimere i dettagli del pannello laterale sinistro
* Un pulsante **Account** a destra per passare alla modalità scura ed uscire dalla console

### Barra laterale a sinistra {#sidebar}

La barra laterale a sinistra consente di accedere rapidamente a importanti viste della console.

* **[Visualizzazione Home](#home-view)** (icona Home) - Punto di partenza per l&#39;utilizzo della console
* **[Visualizzazione contenuto](#content-view)** (icona file) - Contenuto importato
* **[Vista Codice](#code-view)** (`</>` icona) - Codice del sito su cui stai lavorando
* **[Visualizzazione impostazioni](#settings-view)** (icona ingranaggio) - Impostazioni della console

## Vista Home {#home-view}

La visualizzazione **Home** è il punto di partenza per l&#39;utilizzo della console.

* Nella parte superiore è presente un [pannello di richiesta](#prompt-panel) per effettuare le richieste della console.
* Di seguito sono riportati i prompt da utilizzare per avviare il progetto.

### Pannello Prompt {#prompt-panel}

Il pannello dei prompt fornisce i controlli per interagire con l’intelligenza artificiale.

* **Pianifica/Esegui modalità** (icone a forma di lampadina e bacchetta magica): consente di passare rispettivamente dalla modalità Pianificazione alla modalità Esecuzione.
   * **Modalità piano**: l&#39;intelligenza artificiale analizza le richieste e delinea un approccio senza apportare modifiche, utile per comprendere la strategia prima di eseguire il commit.
   * **Modalità di esecuzione**: IA esegue il piano e apporta le modifiche effettive al file.
* **Allega file** (icona a forma di graffetta): carica e allega i file alla richiesta di ulteriore contesto (ad esempio progettazioni di riferimento, schermate, specifiche)
* **Impostazioni** (icona ingranaggio): scegli di saltare le domande di conferma dall&#39;IA
* **Cancella chat**: la conversazione verrà ripristinata e la finestra di contesto dell&#39;intelligenza artificiale verrà cancellata. Utilizzare questa opzione quando si avvia una nuova attività non correlata alla conversazione precedente.

## Vista contenuto {#content-view}

La **visualizzazione contenuto** fornisce gli strumenti per la visualizzazione e l&#39;anteprima del contenuto. Per impostazione predefinita, la vista è divisa in tre pannelli, da sinistra a destra:

* Pannello Prompt per interagire con la console e il progetto
* Browser file per una panoramica dei file di contenuto (attiva/disattiva la visualizzazione del pannello con l’icona a forma di freccia)
* Pannello Anteprima per la visualizzazione del contenuto selezionato nel browser dei file

![Visualizzazione contenuto](assets/content-imported.png)

Il pannello di anteprima offre tre modalità:

* **Anteprima** (documento con icona della lente di ingrandimento) per visualizzare il contenuto HTML sottoposto a rendering
* **Visualizzazione HTML** (icona del documento) per visualizzare rispettivamente la struttura di contenuto di authoring del documento sottostante
* **Modalità progettazione** (icona del pennello) per selezionare gli elementi della pagina da contestualizzare al prompt

Puoi sempre fare clic sull&#39;icona **Aggiorna anteprima** per aggiornare il pannello di anteprima.

Il pulsante **Carica contenuto** apre una finestra modale per caricare i file in AEM Document Authoring.

* Il campo **Organizzazione** e **Archivio** sono precompilati se il progetto contiene un file `fstab.yaml`
* La selezione dei file fornisce percorsi di destinazione modificabili
* Il caricamento in JCR (per l’editor universale) non è supportato

![Carica contenuto](assets/upload-content.png)

## Vista Codice {#code-view}

La **vista Codice** fornisce gli strumenti per sfogliare il codice e gestire le modifiche al codice. La vista è divisa in tre pannelli, da sinistra a destra:

* Pannello Prompt per interagire con la console e il progetto
* Browser file per una panoramica dei file di codice o delle modifiche in base alle differenze
* Pannello Anteprima per la visualizzazione di un file di codice o di una differenza selezionata nel browser di file

![Visualizzazione codice](assets/code-view.png)

Il pannello di anteprima offre due modalità diverse:

* **File Workspace** per visualizzare i file di codice nell&#39;area di lavoro corrente
* **Modifiche Git** per visualizzare le differenze delle modifiche ai file create dal lavoro sul progetto
   * Fai clic sull&#39;icona `+` per posizionare nell&#39;area intermedia il file modificato
   * Fare clic sull&#39;icona freccia per eliminare il file modificato

L&#39;icona **Informazioni** elenca l&#39;account e il progetto GitHub attualmente connessi.

Il menu **Azioni GitHub** (in alto a destra) fornisce le operazioni dell&#39;archivio.

* **Connetti / Riconnetti**: avvia OAuth GitHub
* **Cambia archivio**: sostituisce l&#39;area di lavoro con un altro archivio. Qualsiasi lavoro non impegnato andrà perso.
* **Cambia ramo**: cambia ramo all&#39;interno dello stesso archivio
* **Sincronizzazione**: richiama le modifiche più recenti dall&#39;origine remota
* **Push**: apre una finestra modale per inviare le modifiche dell&#39;area di lavoro a GitHub
* **Disconnessione**: disconnette da GitHub

Quando esegui il push delle modifiche, devi avere le prime modifiche di staging da includere nel push. Quando premi puoi scegliere di creare una nuova PR o di inviare messaggi push direttamente al ramo corrente

![Modifiche push](assets/push-changes.png)

## Visualizzazione impostazioni {#settings-view}

La vista Impostazioni consente di gestire le impostazioni di base della console.

![Visualizzazione impostazioni](assets/settings-view.png)

* **Credenziali** consente di specificare un token di accesso personale per Figma in modo che la console possa accedere ai blocchi di progettazione per il progetto.
* **Ripristina area di lavoro** ripristina lo stato iniziale della console e tutte le modifiche non inviate o non caricate andranno perse.
