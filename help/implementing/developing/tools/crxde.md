---
title: Utilizzo di CRXDE Lite
description: CRXDE Lite fa parte del modulo quickstart dell’AEM ed è disponibile per accedere e modificare l’archivio negli ambienti di sviluppo locali all’interno del browser.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---

# Utilizzo di CRXDE Lite {#using-crxde-lite}

CRXDE Lite fa parte del modulo quickstart dell’AEM ed è disponibile per accedere e modificare l’archivio negli ambienti di sviluppo locali all’interno del browser. Con CRXDE Lite puoi modificare file, cartelle, nodi e proprietà. L’intero archivio è accessibile da questa interfaccia di facile utilizzo.

>[!NOTE]
>
>CRXDE Lite è disponibile solo negli ambienti di sviluppo locali. Non è disponibile nell’AEM as a Cloud Service.

## Guida introduttiva di CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare a utilizzare CRXDE Lite:

1. Avvia rapidamente lo sviluppo locale dell’AEM.
1. Nel browser, apri l’URL `https://<host>:<port>/crx/de`.
1. Immetti il **nome utente** e **password**.
1. Fai clic su **OK**.

L’interfaccia utente di CRXDE Lite viene visualizzata come segue nel browser:

![Interfaccia CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Puoi anche accedere a CRXDE Lite dal menu AEM. Dal menu principale, seleziona **Strumenti** -> **Generale** -> **CRXDE Lite**.

## Panoramica dell’interfaccia utente {#overview-of-the-user-interface}

L&#39;interfaccia utente di CRXDE Lite ha molte parti e molte funzioni.

### Barra del commutatore superiore {#top-switcher-bar}

La barra di commutazione superiore consente di passare rapidamente da CRXDE Lite a [Gestione pacchetti.](package-manager.md)

### Widget percorso nodo {#node-path-widget}

Il widget Percorso nodo visualizza il percorso del nodo attualmente selezionato.

Puoi anche utilizzarlo per passare a un nodo immettendo manualmente il percorso o incollandolo da un’altra posizione e premendo Invio.

Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Inserisci il nome del nodo che desideri trovare e attendi (oppure seleziona l’icona di ricerca a destra). Se uno o più nodi vengono caricati nel riquadro dell&#39;elenco delle cartelle, verrà visualizzato l&#39;elenco e sarà possibile selezionare il percorso e premere Invio per individuarlo. Si noti che funziona solo per i nodi attualmente caricati nell’applicazione client CRXDE nel browser. Se desideri cercare nell’intero archivio, utilizza **Strumenti** ->: **Query**.

### Riquadro Explorer {#explorer-pane}

Il **Riquadro Explorer** visualizza una struttura di tutti i nodi del repository.

Fai clic su un nodo per visualizzarne le proprietà nel **Proprietà** scheda. Dopo aver fatto clic su un nodo, puoi selezionare un’azione nella barra degli strumenti. Fai di nuovo clic sul nodo per rinominarlo.

Il filtro di navigazione ad albero (icona binocolo) consente di filtrare i nodi del repository per i quali il nome contiene il testo di input. Si applica solo ai nodi che sono stati caricati localmente.

### Modifica riquadro {#edit-pane}

Il **Modifica riquadro** consente di visualizzare il contenuto del file attualmente selezionato nel repository. Ogni file aperto verrà rappresentato come la relativa scheda nel riquadro.

Il **Home** Questa scheda ti consente di cercare contenuti e/o documentazione e di accedere alla documentazione per gli sviluppatori e al supporto per gli Adobi.

Fare doppio clic su un file in **Riquadro Explorer** per visualizzarne il contenuto in **Modifica riquadro**. Puoi quindi modificarlo e salvare le modifiche.

Dopo aver modificato un file in **Modifica riquadro**, sulla barra degli strumenti sono disponibili i seguenti strumenti:

* **Mostra nella struttura** : mostra il file nella struttura del repository.
* **Cerca/Sostituisci** - Esegue una ricerca o una sostituzione.

Fare doppio clic sulla riga di stato del **Modifica riquadro** apre il **Vai alla riga** in modo da poter immettere un numero di riga specifico.

### Scheda Proprietà {#properties-tab}

Il **Scheda Proprietà** visualizza le proprietà del nodo selezionato. Puoi aggiungere nuove proprietà o eliminare quelle esistenti.

### Scheda Controllo accesso {#access-control-tab}

Il **Scheda Controllo accesso** visualizza le autorizzazioni in base al percorso, all&#39;archivio o all&#39;entità corrente.

Le autorizzazioni sono suddivise nelle seguenti categorie.

* **Criterio di controllo dell’accesso applicabile** - Criteri applicabili alla selezione corrente
* **Criteri di controllo dell&#39;accesso locale** - I criteri correnti applicati localmente alla selezione corrente
* **Criteri di controllo dell&#39;accesso effettivi** - I criteri correnti applicati per la selezione corrente, che possono essere impostati localmente o ereditati dai nodi padre

>[!NOTE]
Per poter visualizzare le informazioni sul controllo di accesso, l’utente connesso a CRXDE Lite deve disporre dei diritti per la lettura delle voci ACL.

### Scheda Replica {#replication-tab}

Il **Scheda Replica** visualizza lo stato di replica del nodo corrente. Puoi replicare e replicare per eliminare il nodo corrente.

### Scheda Console {#console-tab}

Il **Scheda Console** visualizza i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e abilitare/disabilitare la visualizzazione dei messaggi.

### Scheda Informazioni sulla build {#build-info-tab}

Il **Scheda Informazioni sulla build** visualizza informazioni quando viene creato un bundle.

### Pulsante Aggiorna {#refresh-button}

Il **Pulsante Aggiorna** aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella vista dell’archivio. Le modifiche apportate non vengono modificate.

### Pulsante Salva tutto {#save-all-button}

Il **Pulsante Salva tutto** salva tutte le modifiche apportate. Fino a quando non scegli di salvare, le modifiche sono temporanee e andranno perse quando esci dalla console.

* **Ripristina** - Elimina tutte le modifiche apportate al nodo selezionato dall&#39;ultima azione di salvataggio, quindi ricarica lo stato corrente dell&#39;archivio per il nodo selezionato
* **Ripristina tutto** : ignora tutte le modifiche apportate in tutto l’archivio dall’ultima azione di salvataggio, quindi ricarica lo stato corrente dell’archivio.

### Pulsante Crea {#create-button}

Il **Pulsante Crea** è un menu a discesa per creare quanto segue sotto il nodo selezionato:

* Nodo: un nodo con un tipo di nodo arbitrario
* File - an `nt:file` nodo e il relativo sottonodo nt:resource
* Cartella - an `nt:folder` nodo

### Pulsante Elimina {#delete-button}

Il **Pulsante Elimina** elimina il nodo selezionato.

### Pulsante Copia {#copy-button}

Il **Pulsante Copia** copia il nodo selezionato.

## Pulsante Incolla {#paste-button}

Il **Pulsante Incolla** incolla il nodo copiato sotto il nodo selezionato.

### Pulsante Sposta {#move-button}

Il **Pulsante Sposta** sposta il nodo selezionato sul nodo impostato tramite la finestra di dialogo.

### Rinomina {#rename-button}

Il **Pulsante Rinomina** rinomina il nodo selezionato.

### Mixin {#mixins-button}

Il **Pulsante Mixin** consente di aggiungere tipi mixin al tipo di nodo. I tipi mixin vengono utilizzati principalmente per aggiungere funzioni avanzate.

### Strumenti {#tools-button}

Il **Pulsante Strumenti** è un menu a discesa con i seguenti strumenti disponibili:

* **Configurazione server** - accedere alla console Felix (disponibile anche all&#39;indirizzo `https://<host>:<port>/system/console/configMgr`)
* **Query** - per eseguire una query sull’archivio
* **Privilegi** - per visualizzare e aggiungere privilegi
* **Test del controllo degli accessi** - per verificare l&#39;autorizzazione per determinati percorsi e/o entità
* **Esporta tipo di nodo** - per esportare i tipi di nodo nel sistema come notazione CND
* **Importa tipo di nodo** : per importare tipi di nodo utilizzando la notazione CND.

### Widget di accesso {#login-widget}

Il **Widget di accesso** visualizza l&#39;utente attualmente connesso.

Fai clic su di esso per accedere o accedere nuovamente come altro utente. Il `@crx.default` indica che ci si trova nell&#39;area di lavoro predefinita (e solo) dell&#39;archivio.

Il **Preferenze** Questa opzione può essere utilizzata per impostare la lingua dell’interfaccia utente e per visualizzare e personalizzare i tasti di scelta rapida per varie azioni quali salvataggio, ricerca, creazione di note e così via.

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella e selezionare **Crea...**, quindi **Crea cartella...**.

1. Inserisci la cartella **Nome** e fai clic su **OK**.

1. Clic **Salva tutto** per salvare le modifiche sul server.

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. In [**Riquadro Exploerer**,](#explorer-pane) fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, quindi selezionare **Crea**, quindi **Crea nodo**.
1. Inserisci il **Nome** e seleziona la **Tipo**.
1. Fai clic su **OK**.
1. Fai clic su [**Pulsante Salva tutto**](#save-all-button) per salvare le modifiche sul server.

Ora puoi adattare il nodo alle tue esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
La maggior parte delle operazioni di modifica, tra cui **Crea nodo**, conserva tutte le modifiche in memoria e le archivia nell&#39;archivio solo al momento del salvataggio (utilizzando [**Pulsante Salva tutto**](#save-all-button)). Tuttavia, alcune operazioni, come lo spostamento, vengono mantenute automaticamente.
La convalida relativa alla possibilità che il nodo appena creato sia consentito dal tipo di nodo del nodo principale viene eseguita anche dall’archivio durante il salvataggio delle modifiche. Se ricevi un messaggio di errore durante il salvataggio di un nodo, controlla se la struttura del contenuto è valida (ad esempio, non è possibile creare un nodo). `nt:unstructured` nodo come elemento secondario di `nt:folder` nodo ).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. In [**Riquadro Exploerer**,](#explorer-pane) seleziona il nodo in cui desideri aggiungere la nuova proprietà.
1. In [**Scheda Proprietà**](#properties-tab) nel riquadro inferiore, immettere **Nome**, il **Tipo** e **Valore**.
1. Fate clic su **Aggiungi**.
1. Fai clic su [**Pulsante Salva tutto**](#save-all-button) per salvare le modifiche sul server.

## Creazione di un file {#creating-a-file}

Per creare un nuovo file con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. In [**Riquadro Exploerer**,](#explorer-pane) fai clic con il pulsante destro del mouse sul componente in cui desideri creare il file e seleziona (crea file) **Crea**, quindi **Crea file**.
1. Immetti il file **Nome** inclusa la sua estensione.
1. Fai clic su **OK**.
1. Il nuovo file si apre come scheda in [**Modifica riquadro**.](#edit-pane)
1. Modifica il file.
1. Fai clic su [**Pulsante Salva tutto**](#save-all-button) per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo in [Notazione CND (Node Type Definition) e spazio dei nomi compatto](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare la definizione di un tipo di nodo in CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Seleziona il nodo richiesto.
1. Seleziona **Strumenti** allora **Esporta tipo di nodo**.
1. La definizione verrà visualizzata in notazione CND in una nuova scheda nel browser.
1. Se necessario, salva le informazioni.

Per importare una definizione di tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona **Strumenti** allora **Importa tipo di nodo**.
1. Viene visualizzata una nuova scheda in [**Modifica riquadro**](#edit-pane) etichettato **Importa tipo di nodo**.
1. Immetti la notazione CND per la definizione nella casella di testo della **Importa tipo di nodo** scheda.
1. Verifica **Consenti aggiornamento** se stai aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<aem-install-dir>/crx-quickstart/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Apri CRXDE Lite nel browser.
1. Nel menu a discesa a destra della sezione [**Scheda Console**](#console-tab) nella parte inferiore della finestra, seleziona **Registri server**.
1. Fai clic su **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Regolare i parametri di registro nella console Felix facendo clic sul pulsante **Configurazioni di registrazione** icona.
* Cancellare i messaggi facendo clic sul pulsante **Cancella console** icona.
* Fissa il messaggio alla selezione corrente facendo clic sul pulsante **Aggiungi console** icona.
* Attiva o disattiva la visualizzazione dei messaggi facendo clic sul pulsante **Interrompi** icona.
