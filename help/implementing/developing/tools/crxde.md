---
title: Utilizzo di CRXDE Lite
description: CRXDE Lite fa parte del quickstart AEM ed è disponibile per accedere e modificare l’archivio negli ambienti di sviluppo locali all’interno del browser.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: a9c646d24378e67df84c00a4355c692cac85e50b
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 1%

---

# Utilizzo di CRXDE Lite {#using-crxde-lite}

CRXDE Lite fa parte del quickstart AEM ed è disponibile per accedere e modificare l’archivio negli ambienti di sviluppo locali all’interno del browser. Con CRXDE Lite è possibile modificare file, cartelle, nodi e proprietà. L’intero archivio è accessibile tramite questa interfaccia di facile utilizzo.

>[!NOTE]
>
>CRXDE Lite è disponibile solo negli ambienti di sviluppo locali. Non è disponibile in AEM as a Cloud Service.

## Guida introduttiva di CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare a utilizzare CRXDE Lite:

1. Avvia l&#39;avvio rapido dello sviluppo AEM locale.
1. Nel browser, apri l’URL `https://<host>:<port>/crx/de`.
1. Inserisci il tuo **username** e **password**.
1. Fai clic su **OK**.

L’interfaccia utente di CRXDE Lite viene visualizzata come segue nel browser:

![Interfaccia di CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>È inoltre possibile accedere ad CRXDE Lite dal menu AEM. Dal menu principale seleziona **Strumenti** -> **Generale** -> **CRXDE Lite**.

## Panoramica dell’interfaccia utente {#overview-of-the-user-interface}

L’interfaccia utente di CRXDE Lite ha molte parti e numerose funzioni.

### Barra di commutazione superiore {#top-switcher-bar}

La barra di commutazione superiore consente di passare rapidamente da CRXDE Lite a [Gestione pacchetti.](package-manager.md)

### Widget percorso nodo {#node-path-widget}

Il widget Percorso nodo visualizza il percorso del nodo attualmente selezionato.

È inoltre possibile utilizzarlo per passare a un nodo inserendo il percorso a mano o incollandolo da un altro punto e premendo Invio.

Fornisce inoltre il supporto per la ricerca di nodi con un nome di nodo specifico. Inserisci il nome del nodo da trovare e attendi (oppure seleziona l’icona di ricerca sul lato destro). Se nel riquadro Esplora risorse viene caricato uno o più nodi, viene visualizzato l&#39;elenco, che consente di selezionare il percorso e premere Invio per passare a tale percorso. Si noti che funziona solo per i nodi attualmente caricati nell&#39;applicazione client CRXDE nel browser. Se desideri eseguire una ricerca nell’intero archivio, utilizza **Strumenti** ->: **Query**.

### Riquadro di Esplora risorse {#explorer-pane}

La **Riquadro di Esplora risorse** visualizza una struttura ad albero di tutti i nodi della directory archivio.

Fai clic su un nodo per visualizzarne le proprietà nel **Proprietà** scheda . Dopo aver fatto clic su un nodo, puoi selezionare un’azione nella barra degli strumenti. Fare nuovamente clic sul nodo per rinominarlo.

Filtro di navigazione ad albero (icona binocolo) consente di filtrare i nodi nell’archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi caricati localmente.

### Riquadro di modifica {#edit-pane}

La **Riquadro di modifica** consente di visualizzare il contenuto del file attualmente selezionato nella directory archivio. Ogni file aperto viene rappresentato come una propria scheda nel riquadro .

La **Pagina principale** La scheda ti consente di cercare contenuti e/o documentazione e di accedere alla documentazione per gli sviluppatori e al supporto per gli Adobi.

Fai doppio clic su un file nel **Riquadro di Esplora risorse** per visualizzare il relativo contenuto nel **Riquadro di modifica**. Puoi quindi modificarlo e salvare le modifiche.

Una volta modificato un file nella **Riquadro di modifica**, nella barra degli strumenti sono disponibili i seguenti strumenti:

* **Mostra nella struttura** - Mostra il file nella struttura del repository.
* **Ricerca/Sostituisci** - Esegue una ricerca o una sostituzione.

Fare doppio clic sulla linea di stato del **Riquadro di modifica** apre **Vai alla riga** consente di immettere un numero di riga specifico.

### Scheda Proprietà {#properties-tab}

La **Scheda Proprietà** visualizza le proprietà del nodo selezionato. È possibile aggiungere nuove proprietà o eliminare quelle esistenti.

### Scheda Controllo accesso {#access-control-tab}

La **Scheda Controllo accesso** visualizza le autorizzazioni in base al percorso, al repository o all&#39;entità corrente.

Le autorizzazioni sono suddivise nelle seguenti categorie.

* **Criteri applicabili per il controllo degli accessi** - Criteri applicabili alla selezione corrente
* **Criteri di controllo accessi locali** - Le attuali politiche applicate localmente alla selezione corrente
* **Politiche di controllo dell&#39;accesso efficaci** - Criteri correnti applicati per la selezione corrente, che possono essere impostati localmente o ereditati dai nodi principali

>[!NOTE]
Per poter visualizzare le informazioni sul controllo di accesso, l&#39;utente che ha effettuato l&#39;accesso a CRXDE Lite deve disporre dei diritti per leggere le voci ACL.

### Scheda Replica {#replication-tab}

La **Scheda Replica** visualizza lo stato di replica del nodo corrente. Puoi replicare e replicare l’eliminazione del nodo corrente.

### Scheda Console {#console-tab}

La **Scheda Console** visualizza i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e abilitare/disabilitare la visualizzazione dei messaggi.

### Scheda Informazioni build {#build-info-tab}

La **Scheda Informazioni build** visualizza informazioni quando viene generato un bundle.

### Pulsante Aggiorna {#refresh-button}

La **Pulsante Aggiorna** aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella visualizzazione dell’archivio. Le modifiche apportate non vengono modificate.

### Pulsante Salva tutto {#save-all-button}

La **Pulsante Salva tutto** salva tutte le modifiche apportate. Fino a quando non scegli di salvare, le modifiche sono temporanee e andranno perse quando esci dalla console.

* **Ripristina** - Ignora tutte le modifiche apportate al nodo selezionato dall&#39;ultima azione di salvataggio, quindi ricarica lo stato corrente dell&#39;archivio per il nodo selezionato
* **Ripristina tutto** - Elimina tutte le modifiche apportate all’intero archivio dall’ultima azione di salvataggio, quindi ricarica lo stato corrente dell’archivio

### Pulsante Crea {#create-button}

La **Pulsante Crea** è un menu a discesa per creare quanto segue sotto il nodo selezionato:

* Nodo: un nodo con un tipo di nodo arbitrario
* File - un `nt:file` nodo e relativo sottonodo nt:resource
* Cartella - un `nt:folder` nodo

### Pulsante Elimina {#delete-button}

La **Pulsante Elimina** elimina il nodo selezionato.

### Pulsante Copia {#copy-button}

La **Pulsante Copia** copia il nodo selezionato.

## Pulsante Incolla {#paste-button}

La **Pulsante Incolla** incolla il nodo copiato sotto il nodo selezionato.

### Pulsante Sposta {#move-button}

La **Pulsante Sposta** sposta il nodo selezionato sul nodo impostato tramite la finestra di dialogo.

### Rinomina {#rename-button}

La **Pulsante Rinomina** rinomina il nodo selezionato.

### Mixins {#mixins-button}

La **Pulsante Mixins** consente di aggiungere tipi mixin al tipo di nodo. I tipi di mixin vengono utilizzati principalmente per aggiungere funzioni avanzate.

### Strumenti {#tools-button}

La **Pulsante Strumenti** è un menu a discesa con i seguenti strumenti disponibili:

* **Configurazione server** - per accedere alla console Felix (disponibile anche all&#39;indirizzo `https://<host>:<port>/system/console/configMgr`)
* **Query** - per eseguire query sul repository
* **Privilegi** - per visualizzare e aggiungere privilegi
* **Controllo dell&#39;accesso ai test** - per verificare l&#39;autorizzazione per un determinato percorso e/o entità principale
* **Esporta tipo di nodo** - per esportare i tipi di nodo nel sistema come notazione CND
* **Importa tipo di nodo** - per importare i tipi di nodo utilizzando la notazione CND.

### Widget di accesso {#login-widget}

La **Widget di accesso** visualizza l&#39;utente attualmente connesso.

Fai clic su di esso per accedere o riaccedere come un altro utente. La `@crx.default` rappresenta che ti trovi nell’area di lavoro predefinita (e solo) nell’archivio.

La **Preferenze** può essere utilizzata per impostare la lingua dell’interfaccia utente e per visualizzare e personalizzare gli hot key per varie azioni quali salvataggio, ricerca, creazione di note, ecc.

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettere la cartella **Nome** e fai clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. In [**Riquadro Esploer**,](#explorer-pane) fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, selezionare **Crea**, quindi **Crea nodo**.
1. Inserisci il **Nome** e seleziona la **Tipo**.
1. Fai clic su **OK**.
1. Fai clic sul pulsante [**Pulsante Salva tutto**](#save-all-button) per salvare le modifiche sul server.

Ora puoi adattare il nodo alle tue esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
La maggior parte delle operazioni di modifica, tra cui **Crea nodo**, mantiene tutte le modifiche nella memoria e le memorizza solo nel repository al momento del salvataggio (utilizzando il [**Pulsante Salva tutto**](#save-all-button)). Tuttavia, alcune operazioni come lo spostamento vengono mantenute automaticamente.
La convalida relativa al fatto che il nodo appena creato sia consentito dal tipo di nodo del nodo padre viene eseguita anche dall&#39;archivio al momento del salvataggio delle modifiche. Se ricevi un messaggio di errore durante il salvataggio di un nodo, controlla se la struttura del contenuto è valida (ad esempio, non puoi creare un `nt:unstructured` come nodo figlio di `nt:folder` node).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. In [**Riquadro Esploer**,](#explorer-pane) seleziona il nodo in cui desideri aggiungere la nuova proprietà.
1. In [**Scheda Proprietà**](#properties-tab) nel riquadro inferiore, immetti il **Nome**, **Tipo** e **Valore**.
1. Fate clic su **Aggiungi**.
1. Fai clic sul pulsante [**Pulsante Salva tutto**](#save-all-button) per salvare le modifiche sul server.

## Creazione di un file {#creating-a-file}

Per creare un nuovo file con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. In [**Riquadro Esploer**,](#explorer-pane) fai clic con il pulsante destro del mouse sul componente in cui desideri creare il file, seleziona **Crea**, quindi **Crea file**.
1. Inserisci il file **Nome** compresa la sua estensione.
1. Fai clic su **OK**.
1. Il nuovo file viene aperto come scheda nel [**Riquadro di modifica**.](#edit-pane)
1. Modifica il file.
1. Fai clic sul pulsante [**Pulsante Salva tutto**](#save-all-button) per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo in [Notazione CND (Node Type Definition) e spazio dei nomi compatto](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare una definizione del tipo di nodo in CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Seleziona il nodo richiesto.
1. Seleziona **Strumenti** then **Esporta tipo di nodo**.
1. La definizione verrà visualizzata in notazione CND in una nuova scheda nel browser.
1. Se necessario, salva le informazioni.

Per importare una definizione del tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona **Strumenti** then **Importa tipo di nodo**.
1. Viene visualizzata una nuova scheda in [**Riquadro di modifica**](#edit-pane) etichettato **Importa tipo di nodo**.
1. Immettere la notazione CND per la definizione nella casella di testo della **Importa tipo di nodo** scheda .
1. Controlla **Consenti aggiornamento** se stai aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<aem-install-dir>/crx-quickstart/logs` e filtrarlo con il livello di log appropriato. Procedere come segue:

1. Apri CRXDE Lite nel browser.
1. Nel nel menu a discesa a destra di [**Scheda Console**](#console-tab) nella parte inferiore della finestra, selezionare **Registri server**.
1. Fai clic sul pulsante **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Per regolare i parametri di registro nella console Felix, fai clic sul pulsante **Configurazioni di registrazione** icona.
* Cancella i messaggi facendo clic sul pulsante **Cancella console** icona.
* Aggiungi il messaggio alla selezione corrente facendo clic sul pulsante **Console a blocchi** icona.
* Attiva o disattiva la visualizzazione dei messaggi facendo clic sul pulsante **Interrompi** icona.
