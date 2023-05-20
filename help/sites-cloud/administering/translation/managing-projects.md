---
title: Gestione dei progetti di traduzione
description: Scopri come creare e gestire progetti di traduzione automatica e umana in AEM.
feature: Language Copy
role: Admin
exl-id: dc2f3958-72b5-4ae3-a224-93d8b258bc80
source-git-commit: 05723d602362fd8fe8ed2318d42a669f00f79f87
workflow-type: tm+mt
source-wordcount: '4086'
ht-degree: 99%

---

# Gestione dei progetti di traduzione {#managing-translation-projects}

I progetti di traduzione consentono di gestire la traduzione dei contenuti AEM. Un progetto di traduzione è un tipo di [progetto](/help/sites-cloud/authoring/projects/overview.md) AEM che contiene risorse da tradurre in altre lingue. Queste risorse sono le pagine e le risorse delle [copie per lingua](preparation.md) create dal master lingua.

>[!TIP]
>
>Se non hai ancora tradotto contenuti, consulta il nostro [Percorso di traduzione Sites,](/help/journey-sites/translation/overview.md) per una guida sulla traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideali per chi non ha esperienza di AEM o traduzione.

Quando si aggiungono risorse a un progetto di traduzione, viene creato un processo di traduzione apposito. I processi forniscono i comandi e le informazioni sullo stato, utili per gestire i flussi di lavoro di traduzione umana e automatica che vengono eseguiti sulle risorse.

I progetti di traduzione sono elementi a esecuzione prolungata, definiti per lingua e metodo/fornitore di traduzione per l’allineamento alla governance organizzativa di globalizzazione. Devono essere avviati una volta, durante la traduzione iniziale o manualmente, e rimangono in funzione per tutte le attività di aggiornamento del contenuto e della traduzione.

I progetti e i processi di traduzione vengono creati con flussi di lavoro di preparazione della traduzione. Questi flussi di lavoro hanno tre opzioni, sia per la traduzione iniziale (Crea e traduci) che per gli aggiornamenti (Aggiorna traduzione):

1. [Crea nuovo progetto](#creating-translation-projects-using-the-references-panel)
1. [Aggiungi a progetto esistente](#adding-pages-to-a-translation-project)
1. [Solo struttura del contenuto](#creating-the-structure-of-a-language-copy)

AEM rileva se viene creato un progetto per la traduzione iniziale del contenuto o per aggiornare copie per lingua già tradotte. Quando crei un progetto di traduzione per una pagina e indichi le copie per lingua di cui ti stai occupando, AEM rileva se la pagina sorgente esiste già nelle copie per lingua di destinazione:

* **La copia per lingua non include la pagina:** AEM tratta questa situazione come traduzione iniziale. La pagina viene immediatamente copiata nella copia per lingua e inclusa nel progetto. Quando la pagina tradotta viene importata in AEM, AEM la inserisce direttamente nella copia per lingua.
* **La copia per lingua include già la pagina:** AEM tratta questa situazione come traduzione aggiornata. Viene creato un lancio a cui viene aggiunta una copia della pagina inclusa nel progetto. I lanci consentono di rivedere le traduzioni aggiornate prima di inviarle alla copia per lingua:

   * Quando la pagina tradotta viene importata in AEM, sovrascrive la pagina nel lancio.
   * La pagina tradotta sovrascrive la copia per lingua solo quando il lancio viene promosso.

Ad esempio, viene creata la directory principale della lingua `/content/wknd/fr` per la traduzione francese dal master lingua `/content/wknd/en`. Non ci sono altre pagine nella copia per lingua francese.

* Viene creato un progetto di traduzione per la pagina `/content/wknd/en/products` e tutte le pagine figlie, con targeting per la copia in lingua francese. Poiché la copia per lingua non include la pagina `/content/wknd/fr/products`, AEM copia immediatamente la pagina `/content/wknd/en/products` e tutte le pagine figlie nella copia in lingua francese. Le copie sono incluse anche nel progetto di traduzione.
* Viene creato un progetto di traduzione per la pagina `/content/wknd/en` e tutte le pagine figlie, con targeting per la copia in lingua francese. Poiché la copia per lingua include la pagina che corrisponde alla pagina `/content/wknd/en` (directory principale della lingua), AEM copia la pagina `/content/wknd/en` e tutte le pagine figlie e le aggiunge a un lancio. Le copie sono incluse anche nel progetto di traduzione.

## Traduzioni dalla console Sites {#performing-initial-translations-and-updating-existing-translations}

I progetti di traduzione possono essere creati o aggiornati direttamente dalla console Sites.

### Creazione di progetti di traduzione tramite il pannello Riferimenti {#creating-translation-projects-using-the-references-panel}

Crea progetti di traduzione in modo da poter eseguire e gestire il flusso di lavoro per la traduzione delle risorse del master lingua. Quando si creano i progetti, è possibile specificare la pagina nel master lingua che si sta traducendo e le copie per lingua per le quali si sta eseguendo la traduzione:

* La configurazione cloud del framework di integrazione della traduzione associato alla pagina selezionata determina molte proprietà dei progetti di traduzione, ad esempio il flusso di lavoro di traduzione da utilizzare.
* Viene creato un progetto per ogni copia per lingua selezionata.
* Viene creata e aggiunta a ciascun progetto una copia della pagina selezionata e delle risorse associate. Queste copie vengono successivamente inviate al fornitore di traduzione per la lavorazione.

È possibile specificare anche la selezione delle pagine figlie insieme alla pagina selezionata. In questo caso, a ogni progetto vengono aggiunte anche copie delle pagine figlie in modo che vengano tradotte. Se alle pagine figlie sono associate diverse configurazioni del framework di integrazione della traduzione, AEM crea ulteriori progetti.

È inoltre possibile [creare manualmente progetti di traduzione](#creating-a-translation-project-using-the-projects-console).

>[!NOTE]
>
>Per creare un progetto, il tuo account deve essere un membro del gruppo `project-administrators`.

### Traduzioni iniziali e aggiornamento delle traduzioni {#initial-and-updating}

Il pannello Riferimenti indica se si stanno aggiornando le copie per lingua esistenti o se si sta creando la prima versione delle copie per lingua. Quando esiste una copia per lingua della pagina selezionata, viene visualizzata la scheda Aggiorna copie per lingua per consentire l’accesso ai comandi relativi al progetto.

![Aggiorna copie per lingua](../assets/update-language-copies.png)

Dopo aver tradotto, puoi [rivedere la traduzione](#reviewing-and-promoting-updated-content) prima di utilizzarla per sovrascrivere la copia per lingua. Se non esiste una copia per lingua della pagina selezionata, viene visualizzata la scheda Crea e traduci per consentire l’accesso ai comandi relativi al progetto.

![Crea e traduci](../assets/create-and-translate.png)

### Creare progetti di traduzione per una nuova copia per lingua {#create-translation-projects-for-a-new-language-copy}

1. Usa la console Sites per selezionare la pagina che stai aggiungendo ai progetti di traduzione.

1. Utilizzando la barra degli strumenti, apri la barra **Riferimenti**.

   ![Riferimenti](../assets/references.png)

1. Scegli **Copie per lingua**, quindi seleziona le copie per lingua per le quali stai traducendo le pagine sorgente.
1. Tocca o fai clic su **Crea e traduci** quindi configura il processo di traduzione:

   * Utilizza il menu a discesa **Lingue** per selezionare una copia per lingua per cui desideri tradurre. Seleziona le lingue aggiuntive come richiesto. Le lingue visualizzate nell’elenco corrispondono alle [directory principali della lingua create](preparation.md#creating-a-language-root).
      * Selezionando più lingue si crea un progetto con un processo di traduzione per ogni lingua.
   * Per tradurre la pagina selezionata e tutte le pagine figlie, seleziona l’opzione **Seleziona tutte le sottopagine**. Per tradurre solo la pagina selezionata, deseleziona l’opzione.
   * Per **Progetto**, seleziona **Crea progetti di traduzione**.
   * Facoltativamente per **Master progetto**, seleziona un progetto da cui ereditare i ruoli utente e le autorizzazioni.
   * In **Titolo** digita un nome per il progetto.

   ![Crea progetto di traduzione](../assets/create-translation-project.png)

1. Tocca o fai clic su **Crea**.

### Creare progetti di traduzione per una copia per lingua esistente {#create-translation-projects-for-an-existing-language-copy}

1. Usa la console Sites per selezionare la pagina da aggiungere ai progetti di traduzione.

1. Utilizzando la barra degli strumenti, apri la barra **Riferimenti**.

   ![Riferimenti](../assets/references.png)

1. Scegli **Copie per lingua**, quindi seleziona le copie per lingua per le quali stai traducendo le pagine sorgente.
1. Tocca o fai clic su **Aggiorna copie per lingua** quindi configura il processo di traduzione:

   * Per tradurre la pagina selezionata e tutte le pagine figlie, seleziona l’opzione **Seleziona tutte le sottopagine**. Per tradurre solo la pagina selezionata, deseleziona l’opzione.
   * Per **Progetto**, seleziona **Crea progetti di traduzione**.
   * Facoltativamente per **Master progetto**, seleziona un progetto da cui ereditare i ruoli utente e le autorizzazioni.
   * In **Titolo** digita un nome per il progetto.

   ![Crea un progetto per aggiornare le copie per lingua](../assets/create-update-language-copies-project.png)

1. Tocca o fai clic su **Crea**.

### Aggiunta di pagine a un progetto di traduzione {#adding-pages-to-a-translation-project}

Dopo aver creato un progetto di traduzione, puoi utilizzare la barra **Risorse** per aggiungere pagine al progetto. L’aggiunta di pagine è utile quando si includono pagine di rami diversi nello stesso progetto.

Quando aggiungi delle pagine a un progetto di traduzione, queste vengono incluse in un nuovo processo di traduzione. È inoltre possibile [aggiungere pagine a un processo esistente](#adding-pages-assets-to-a-translation-job).

Come per la creazione di un nuovo progetto, quando si aggiungono pagine, le copie delle pagine vengono aggiunte a un lancio, quando necessario, per evitare la sovrascrittura delle copie per lingua esistenti. Consulta [Creazione di progetti di traduzione per copie per lingua esistenti](#performing-initial-translations-and-updating-existing-translations).

1. Usa la console Sites per selezionare la pagina che stai aggiungendo al progetto di traduzione.

1. Utilizzando la barra degli strumenti, apri la barra **Riferimenti**.

   ![Riferimenti](../assets/references.png)

1. Seleziona **Copie per lingua**, quindi seleziona le copie per lingua per le quali stai traducendo le pagine sorgente.

   ![Aggiorna copie per lingua dalla barra dei riferimenti](../assets/update-language-copies-references.png)

1. Tocca o fai clic su **Aggiorna copie per lingua** quindi configura le proprietà:

   * Per tradurre la pagina selezionata e tutte le pagine figlie, seleziona l’opzione **Seleziona tutte le sottopagine**. Per tradurre solo la pagina selezionata, deseleziona l’opzione.
   * Per **Progetto**, seleziona **Aggiungi al progetto di traduzione esistente**.
   * Seleziona il progetto in **Progetto di traduzione esistente**.

   >[!NOTE]
   >
   >La lingua di destinazione impostata nel progetto di traduzione deve corrispondere al percorso della copia per lingua, come mostrato nella barra dei riferimenti.

1. Tocca o fai clic su **Aggiorna**.

### Creazione della struttura di una copia per lingua {#creating-the-structure-of-a-language-copy}

È possibile creare solo la struttura della copia per lingua, che consente di copiare il contenuto e le modifiche strutturali del master lingua nelle copie per lingua (non tradotte). Questo non è correlato a un processo o a un progetto di traduzione. Puoi utilizzarlo per mantenere sincronizzati i master lingua, anche senza traduzione.

Compila la copia per lingua in modo che contenga il contenuto del master lingua che si sta traducendo. Prima di compilare la copia per lingua, è necessario [creare la directory principale della lingua](preparation.md#creating-a-language-root) della copia per lingua.

1. Utilizza la console Sites per selezionare la directory principale del master lingua utilizzato come origine.
1. Apri la barra dei riferimenti facendo clic o toccando **Riferimenti** nella barra degli strumenti.

   ![Riferimenti](../assets/references.png)

1. Seleziona **Copie per lingua**, quindi seleziona le copie per lingua che desideri compilare.

   ![Seleziona copie per lingua](../assets/language-copy-structure-select.png)

1. Tocca o fai clic su **Aggiorna copie per lingua** per visualizzare gli strumenti di traduzione e configurare le proprietà:

   * Scegli l’opzione **Seleziona tutte le sottopagine**.
   * Per **Progetto**, seleziona **Crea solo struttura**.

   ![Solo struttura](../assets/language-copy-structure-only.png)

1. Tocca o fai clic su **Aggiorna**.

### Aggiornamento della memoria di traduzione {#updating-translation-memory}

Le modifiche manuali dei contenuti tradotti possono essere sincronizzate con il sistema di gestione della traduzione (TMS) per addestrare la memoria di traduzione.

1. Dalla console Sites, dopo aver aggiornato il contenuto di testo in una pagina tradotta, seleziona **Aggiorna memoria di traduzione**.
1. Una vista a elenco mostra un confronto affiancato dell’originale e della traduzione per ogni componente di testo modificato. Seleziona gli aggiornamenti da sincronizzare con la memoria di traduzione e quindi **Aggiorna memoria**.

![Confronta le modifiche per la memoria di traduzione](../assets/update-translation-memory-compare.png)

AEM aggiorna la traduzione delle stringhe esistenti nella memoria di traduzione del TMS configurato.

* L’azione aggiorna la traduzione delle stringhe esistenti nella memoria di traduzione del TMS configurato.
* Non crea nuovi processi di traduzione.
* Invia le traduzioni al TMS tramite l’API di traduzione di AEM (vedi sotto).

Per utilizzare questa funzione:

* deve essere configurato un TMS per l’utilizzo in AEM.
* Il connettore deve implementare il metodo [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * Il codice all’interno di questo metodo determina cosa accade alla richiesta di aggiornamento della memoria di traduzione.
   * Il framework di traduzione di AEM invia nuovamente le coppie di valori stringa (traduzione originale e aggiornata) al TMS tramite questa implementazione del metodo.

Nei casi in cui viene utilizzata una memoria di traduzione proprietaria, gli aggiornamenti della memoria di traduzione possono essere intercettati e inviati a una destinazione personalizzata.

### Verifica dello stato di traduzione di una pagina {#check-translation-status}

È possibile selezionare una proprietà nella vista a elenco della console Sites per verificare se una pagina è stata tradotta, è in traduzione o non è ancora stata tradotta.

1. Nella console Sites, passa a [vista a elenco.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Tocca o fai clic su **Visualizza impostazioni** nel menu a discesa.
1. Nella finestra di dialogo, seleziona la proprietà **Tradotto** e tocca o fai clic su **Aggiorna**.

Nella console Sites viene ora visualizzata la colonna **Tradotto** che mostra lo stato di traduzione delle pagine elencate.

![Stato della traduzione nella vista a elenco](../assets/translation-status-list-view.png)

## Gestione dei progetti di traduzione dalla console Progetto

Nella console Progetti è possibile accedere a numerose attività di traduzione e opzioni avanzate.

### Informazioni sulla console Progetti

I progetti di traduzione in AEM utilizzano la console standard [Progetti AEM.](/help/sites-cloud/authoring/projects/overview.md) Se non conosci Progetti AEM, consulta la relativa documentazione.

Come qualsiasi altro progetto, un progetto di traduzione è costituito da riquadri che presentano una panoramica delle attività del progetto.

![Progetto di traduzione](../assets/translation-project.png)

* **Riepilogo**: panoramica del progetto
* **Attività**: una o più attività di traduzione
* **Team**: utenti che collaborano al progetto di traduzione
* **Attività**: elementi che devono essere completati nell’ambito del progetto di traduzione

Utilizza i comandi e i puntini di sospensione nella parte superiore e inferiore dei riquadri (rispettivamente) per accedere ai controlli e alle opzioni specifiche.

![Pulsante Comandi](../assets/context.png)

![Pulsante Puntini di sospensione](../assets/ellipsis.png)

### Creazione di un progetto di traduzione tramite la console Progetti {#creating-a-translation-project-using-the-projects-console}

Puoi creare manualmente un progetto di traduzione se preferisci utilizzare la console Progetti invece che la console Sites.

>[!NOTE]
>
>Per creare un progetto, il tuo account deve far parte del gruppo `project-administrators`.

Quando crei manualmente un progetto di traduzione, devi fornire valori per le seguenti proprietà relative alla traduzione, oltre alle [proprietà di base](/help/sites-cloud/authoring/projects/managing.md#creating-a-project):

* **Nome:** nome del progetto
* **Lingua di origine:** lingua del contenuto sorgente
* **Lingua di destinazione:** lingua o lingue in cui il contenuto è tradotto
   * Se sono selezionate più lingue, viene creato un processo per ogni lingua all’interno del progetto.
* **Metodo di traduzione:** seleziona **Traduzione umana** per indicare che la traduzione deve essere eseguita manualmente.

1. Nella barra degli strumenti della console Progetti, tocca o fai clic su **Crea**.
1. Seleziona il modello **Progetto di traduzione** e tocca o fai clic su **Avanti**.
1. Immetti i valori per la scheda proprietà **Base**.
1. Tocca o fai clic su **Avanzate** e fornisci i valori delle proprietà relative alla traduzione.
1. Tocca o fai clic su **Crea**. Nella casella di conferma, tocca o fai clic su **Fine** per tornare alla console dei progetti, oppure tocca o fai clic su **Apri progetto** per aprire e iniziare a gestire il progetto.

### Aggiunta di pagine e risorse a un processo di traduzione {#adding-pages-assets-to-a-translation-job}

Puoi aggiungere pagine, risorse o tag al processo del progetto di traduzione. Per aggiungere pagine o risorse:

1. Nella parte inferiore del riquadro del processo del progetto di traduzione, tocca o fai clic sui puntini di sospensione.

   ![Riquadro del processo di traduzione](../assets/translation-job.png)

1. Nella finestra successiva, tocca o fai clic sul pulsante **Aggiungi** nella barra degli strumenti, quindi seleziona **Risorse/pagine**.

   ![Aggiungi pagine](../assets/add-to-project.png)

1. Nella finestra modale, seleziona l’elemento più in alto del ramo che desideri aggiungere, quindi tocca o fai clic sull’icona del segno di spunta. La selezione multipla è abilitata in questa finestra.

   ![Seleziona pagine](../assets/select-pages.png)

1. In alternativa, puoi selezionare l’icona di ricerca per cercare facilmente le pagine o le risorse da aggiungere al processo di traduzione.

   ![Ricerca contenuti](../assets/search-for-content.png)

1. Una volta selezionata, tocca o fai clic su **Seleziona**. Le pagine e/o le risorse vengono aggiunte al processo di traduzione.

>[!TIP]
>
>Questo metodo aggiunge al progetto le pagine/risorse e i relativi elementi secondari. Seleziona **Risorsa/Pagina (senza elementi secondari)** se desideri aggiungere solo i principali.

### Aggiunta di tag a un processo di traduzione {#adding-tags-to-a-translation-job}

Puoi aggiungere tag a un progetto di traduzione in modo analogo a [come aggiungi risorse e pagine a un progetto.](#adding-pages-assets-to-a-translation-job) Seleziona **Tag** nel menu **Aggiungi** quindi segui gli stessi passaggi.

### Visualizzazione dei dettagli del progetto di traduzione {#seeing-translation-project-details}

Le proprietà del progetto di traduzione sono accessibili tramite il pulsante con i puntini di sospensione del riquadro di riepilogo del progetto. Oltre alle generiche [informazioni sul progetto](/help/sites-cloud/authoring/projects/overview.md#project-info), le proprietà del progetto di traduzione contengono specifiche per la traduzione.

Nel progetto di traduzione, tocca o fai clic sui puntini di sospensione nella parte inferiore del riquadro Riepilogo traduzione. La maggior parte delle proprietà specifiche del progetto si trovano nella scheda **Avanzate**.

* **Lingua di origine:** lingua delle pagine che vengono tradotte
* **Lingua di destinazione:** lingua o lingue in cui le pagine vengono tradotte
* **Configurazione cloud:** configurazione cloud per il connettore del servizio di traduzione utilizzato per il progetto
* **Metodo di traduzione:** il flusso di lavoro di traduzione, **Traduzione umana** o **Traduzione automatica**
* **Fornitore di traduzione:** il fornitore di servizi di traduzione che esegue la traduzione
* **Categoria di contenuto:** (traduzione automatica) la categoria di contenuto utilizzata per la traduzione
* **Credenziali fornitore di traduzione:** credenziali per accedere al fornitore
* **Promuovi automaticamente i lanci di traduzione:** dopo aver ricevuto i contenuti tradotti, i lanci di traduzione vengono promossi automaticamente
   * **Elimina lancio dopo la promozione:** se i lanci di traduzione vengono promossi automaticamente, elimina il lancio dopo la promozione
* **Approva automaticamente traduzioni:** dopo aver ricevuto il contenuto tradotto, i lavori di traduzione vengono automaticamente approvati
* **Ripeti traduzione:** configura l’esecuzione ricorrente di un progetto di traduzione selezionando la frequenza con cui il progetto creerà ed eseguirà automaticamente i processi di traduzione

Quando un progetto viene creato utilizzando la barra dei riferimenti di una pagina, queste proprietà vengono configurate automaticamente in base alle proprietà della pagina sorgente.

![Proprietà progetto di traduzione](../assets/translation-project-properties.png)

### Monitoraggio dello stato di un processo di traduzione {#monitoring-the-status-of-a-translation-job}

Il riquadro del processo di un progetto di traduzione fornisce lo stato del processo nonché il numero di pagine e risorse che ne fanno parte.

![Processo di traduzione](../assets/translation-job.png)

La tabella seguente descrive ogni stato di un processo o di un elemento del processo:

| Stato | Descrizione |
|---|---|
| **Bozza** | Il processo di traduzione non è stato avviato. I processi di traduzione sono in stato **Bozza**** al momento della creazione. |
| **Inviato** | I file nel processo di traduzione sono in questo stato quando risultano inviati correttamente al servizio di traduzione. Questo stato può verificarsi dopo l’esecuzione del comando **Richiedi valutazione** o **Avvia**. |
| **Valutazione richiesta** | Per il flusso di lavoro di traduzione umana, i file nel processo sono stati inviati al fornitore di traduzione per una valutazione. Questo stato viene visualizzato l’emissione del comando **Richiedi valutazione**. |
| **Valutazione completata** | Il fornitore ha valutato il processo di traduzione. |
| **Confermato per traduzione** | Il proprietario del progetto ha accettato la valutazione. Questo stato indica che il fornitore deve iniziare a tradurre i file nel processo. |
| **Traduzione in corso** | Per un processo, la traduzione di uno o più file nel processo non è ancora completa. Per un elemento del processo, l’elemento è in traduzione. |
| **Tradotto** | Per un processo, la traduzione di tutti i file nel processo è completa. Per un elemento del processo, l’elemento viene tradotto. |
| **Pronto per la revisione** | L’elemento nel processo è stato tradotto e il file importato in AEM. |
| **Completa** | Il proprietario del progetto ha indicato che il contratto di traduzione è completo. |
| **Annulla** | Indica che il fornitore deve interrompere il lavoro su un processo di traduzione. |
| **Errore aggiornamento** | Errore durante il trasferimento dei file tra AEM e il servizio di traduzione. |
| **Stato sconosciuto** | Si è verificato un errore sconosciuto. |

Per visualizzare lo stato di ciascun file nel processo, tocca o fai clic sui puntini di sospensione nella parte inferiore del riquadro.

### Impostazione della data di termine dei processi di traduzione {#setting-the-due-date-of-translation-jobs}

Specifica la data prima della quale il fornitore di traduzione deve restituire i file tradotti. L’impostazione della data di termine funziona correttamente solo quando il fornitore di traduzione utilizzato supporta questa funzione.

1. Tocca o fai clic sui puntini di sospensione nella parte inferiore del riquadro di riepilogo della traduzione.

   ![Riquadro di riepilogo della traduzione](../assets/translation-summary-tile.png)

1. Sulla scheda **Base**, utilizza il selettore della proprietà **Data di termine** per la selezione.

   ![Proprietà progetto di traduzione](../assets/translation-project-properties-basic.png)

1. Tocca o fai clic su **Salva e chiudi**.

### Valutazione di un processo di traduzione {#scoping-a-translation-job}

La valutazione di un processo di traduzione serve per ottenere una stima del costo dal fornitore del servizio. Quando si esegue la valutazione di un processo, i file di origine vengono inviati al fornitore di traduzione che confronta il testo con il proprio pool di traduzioni memorizzate (memoria di traduzione). In genere, la valutazione corrisponde al numero di parole che devono essere tradotte.

Per ottenere ulteriori informazioni sui risultati della valutazione, contatta il fornitore della traduzione.

>[!NOTE]
>
>La valutazione è facoltativa e si applica solo alla traduzione umana. Puoi avviare un processo di traduzione senza valutazione.

Quando esegui la valutazione di un processo di traduzione, lo stato del processo è **Valutazione richiesta**. Quando il fornitore di traduzione restituisce la valutazione, lo stato viene modificato in **Valutazione completata**. Al termine della valutazione, puoi utilizzare il comando **Mostra valutazione** per esaminarne i risultati.

La valutazione funziona correttamente solo quando il fornitore di traduzione utilizzato la supporta.

1. Nella console Progetti, apri il progetto di traduzione.
1. Nel titolo del processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su **Richiedi valutazione**.
1. Quando lo stato del processo cambia in **Valutazione completata**, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su **Mostra valutazione**.

### Avvio dei processi di traduzione {#starting-translation-jobs}

Avvia un processo di traduzione per tradurre le pagine di origine nella lingua di destinazione. La traduzione viene eseguita in base ai valori delle proprietà del riquadro di riepilogo della traduzione.

Puoi avviare un singolo processo dall’interno del progetto.

1. Nella console Progetti, apri il progetto di traduzione.
1. Nel riquadro del processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su **Avvia**.
1. Nella finestra di dialogo che conferma l’avvio della traduzione, tocca o fai clic su **Chiudi**.

Dopo aver avviato il processo di traduzione, il riquadro del processo di traduzione mostra la traduzione nello stato **In corso**.

Puoi anche avviare tutti i processi di traduzione per un progetto.

1. Nella console del progetto, seleziona il progetto di traduzione.
1. Nella barra degli strumenti tocca o fai clic su **Avvia processi di traduzione**.
1. Nella finestra di dialogo, controlla l’elenco dei processi che verranno avviati e quindi conferma con **Avvia** o interrompi con **Annulla**.

### Annullamento di un processo di traduzione {#canceling-a-translation-job}

Annulla un processo di traduzione per interromperlo e impedire al fornitore di traduzione di eseguire ulteriori traduzioni. È possibile annullare un processo quando il processo è nello stato **Confermato per traduzione** o **Traduzione in corso**.

1. Nella console Progetti, apri il progetto di traduzione.
1. Nel riquadro del processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su **Annulla**.
1. Nella finestra di dialogo che conferma l’annullamento della traduzione, tocca o fai clic su **OK**.

### Accettare e rifiutare un flusso di lavoro {#accept-reject-workflow}

Quando il contenuto torna dopo la traduzione ed è in stato **Pronto per la revisione** è possibile accedere al processo di traduzione e accettare/rifiutare il contenuto.

Se selezioni **Rifiuta traduzione**, puoi aggiungere un commento.

Il contenuto rifiutato viene inviato nuovamente al fornitore di traduzione, che potrà visualizzare il commento.

### Completamento e archiviazione dei processi di traduzione {#completing-and-archiving-translation-jobs}

Completa un processo di traduzione dopo aver esaminato i file tradotti dal fornitore.

1. Nella console Progetti, apri il progetto di traduzione.
1. Nel riquadro del processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su **Completa**.
1. Il processo ora è in stato **Completo**.

Per i flussi di lavoro di traduzione umana, il completamento di una traduzione indica al fornitore che il contratto di traduzione è stato rispettato e che deve salvare la traduzione nella propria memoria di traduzione.

Archivia un processo di traduzione quando è terminato e non è più necessario visualizzare i dettagli relativi allo stato.

1. Nella console Progetti, apri il progetto di traduzione.
1. Nel riquadro del processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su **Archivia**.

Quando archivi il processo di traduzione, il riquadro relativo viene rimosso dal progetto.

## Revisione e utilizzo di contenuti tradotti {#reviewing-and-promoting-updated-content}

Puoi utilizzare la console Sites per esaminare il contenuto, confrontare le copie per lingua e attivare il contenuto.

### Promozione di contenuti aggiornati {#promoting-updated-content}

Quando il contenuto viene tradotto per una copia per lingua esistente, rivedi le traduzioni, apporta modifiche se necessario e quindi promuovi le traduzioni per spostarlo nella copia per lingua. È possibile rivedere i file tradotti quando il processo di traduzione è in stato **Pronto per la revisione**.

![Processo pronto per la revisione](../assets/job-ready-for-review.png)

1. Seleziona la pagina nel master lingua, tocca o fai clic su **Riferimenti**, quindi tocca o fai clic su **Copie per lingua**.
1. Tocca o fai clic sulla copia per lingua da rivedere.

   ![Copia per lingua pronta per la revisione](../assets/language-copy-ready-for-review.png)

1. Tocca o fai clic su **Lancio** per visualizzare i comandi relativi al lancio.

   ![Lancio](../assets/language-copy-launch.png)

1. Per aprire la copia di lancio della pagina per esaminare e modificare il contenuto, fai clic su **Apri pagina**.
1. Dopo aver rivisto il contenuto e apportato le modifiche necessarie, per promuovere la copia di lancio fai clic su **Promuovi**.
1. Sulla pagina **Promuovi lancio**, specifica le pagine da promuovere, quindi tocca o fai clic su **Promuovi**.

### Confronto di copie per lingua {#comparing-language-copies}

Per confrontare le copie per lingua con il master:

1. Nella console Sites individua la copia per lingua da confrontare.
1. Apri la [Barra dei riferimenti.](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)
1. Sotto l’intestazione **Copie** seleziona **Copie per lingua.**
1. Seleziona la specifica copia per lingua e fai clic su **Confronta con master** o **Confronta con precedente** se del caso.

   ![Confronta copie per lingua](../assets/language-copy-compare.png)

1. Le due pagine (lancio e sorgente) verranno aperte una accanto all’altra.
   * Per informazioni complete sull’utilizzo di questa funzione, consulta [Differenza di pagina](/help/sites-cloud/authoring/features/page-diff.md).

## Spostamento o ridenominazione di una pagina di origine {#move-source}

Se una pagina di origine già tradotta deve essere [rinominata o spostata](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page), e viene ritradotta dopo lo spostamento, verrà creato un nuovo testo in lingua in base al nuovo nome/posizione della pagina. Il testo in lingua precedente basato sul nome/posizione precedente sarà ancora presente.

La best practice per questo scenario prevede di seguire questa procedura:
1. Annulla la pubblicazione dei testi in lingua associati alla pagina sorgente che desideri spostare.
1. Eliminali.
1. Crea nuovi testi in lingua dalla pagina sorgente appena spostata.
1. Pubblica i nuovi testi in lingua.

## Importazione ed esportazione di processi di traduzione {#import-export}

Anche se AEM offre diverse soluzioni e interfacce di traduzione, è possibile anche importare ed esportare manualmente le informazioni sul processo di traduzione.

### Esportazione di un processo di traduzione {#exporting-a-translation-job}

È possibile scaricare il contenuto di un processo di traduzione, ad esempio per l’invio a un fornitore di traduzione che non è integrato con AEM tramite un connettore o per esaminare il contenuto.

1. Dal menu a discesa del riquadro del processo di traduzione, tocca o fai clic su **Esporta**.
1. Nella finestra di dialogo, tocca o fai clic su **Scarica file esportato**, e se necessario, utilizza la finestra di dialogo del browser web per salvare il file.
1. Nella finestra di dialogo, tocca o fai clic su **Chiudi**.

### Importazione di un processo di traduzione {#importing-a-translation-job}

Puoi importare contenuti tradotti in AEM, ad esempio se il fornitore di traduzione li invia a te perché non è integrato con AEM tramite un connettore.

1. Dal menu a discesa del riquadro del processo di traduzione, tocca o fai clic su **Importa**.
1. Utilizza la finestra di dialogo del browser web per selezionare il file da importare.
1. Nella finestra di dialogo, tocca o fai clic su **Chiudi**.
