---
title: Utilizzo di CRXDE Lite
description: CRXDE Lite fa parte di AEM quickstart ed è disponibile per accedere e modificare l’archivio negli ambienti di sviluppo locali all’interno del browser.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 1%

---

# Utilizzo di CRXDE Lite {#using-crxde-lite}

CRXDE Lite fa parte di AEM quickstart ed è disponibile per accedere e modificare l’archivio negli ambienti di sviluppo locali all’interno del browser. Con CRXDE Lite puoi modificare file, cartelle, nodi e proprietà. L’intero archivio è accessibile da questa interfaccia di facile utilizzo.

>[!NOTE]
>
>CRXDE Lite è disponibile solo negli ambienti di sviluppo locali. Non è disponibile in AEM as a Cloud Service.

## Guida introduttiva a CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare a utilizzare CRXDE Lite:

1. Avvia l’avvio rapido di sviluppo AEM locale.
1. Nel browser, aprire l&#39;URL `https://<host>:<port>/crx/de`.
1. Immetti **username** e **password**.
1. Fai clic su **OK**.

L’interfaccia utente di CRXDE Lite viene visualizzata come segue nel browser:

![Interfaccia di CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Puoi accedere a CRXDE Lite anche dal menu AEM. Dal menu principale selezionare **Strumenti** > **Generale** > **CRXDE Lite**.

## Panoramica dell’interfaccia utente {#overview-of-the-user-interface}

L&#39;interfaccia utente di CRXDE Lite è composta da numerose parti e da numerose funzioni.

### Barra del commutatore superiore {#top-switcher-bar}

La barra di commutazione superiore consente di passare rapidamente da CRXDE Lite a [Gestione pacchetti](package-manager.md).

### Widget percorso nodo {#node-path-widget}

Il widget Percorso nodo visualizza il percorso del nodo attualmente selezionato.

Puoi anche utilizzarlo per passare a un nodo immettendo manualmente il percorso o incollandolo da un’altra posizione e premendo Invio.

Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Inserisci il nome del nodo che desideri trovare e attendi (oppure seleziona l’icona di ricerca a destra). Se uno o più nodi vengono caricati nel riquadro dell&#39;elenco delle cartelle, verrà visualizzato l&#39;elenco e sarà possibile selezionare il percorso e premere Invio per individuarlo. Funziona solo per i nodi attualmente caricati nell’applicazione client CRXDE nel browser. Per eseguire ricerche nell&#39;intero repository, utilizzare **Strumenti** -&amp;gt: **Query**.

### Riquadro Explorer {#explorer-pane}

Nel **riquadro Esplora risorse** viene visualizzata una struttura di tutti i nodi del repository.

Fare clic su un nodo per visualizzarne le proprietà nella scheda **Proprietà**. Dopo aver fatto clic su un nodo, puoi selezionare un’azione nella barra degli strumenti. Fai di nuovo clic sul nodo per rinominarlo.

Il filtro di navigazione ad albero (icona binocolo) consente di filtrare i nodi del repository per i quali il nome contiene il testo di input. Si applica solo ai nodi che sono stati caricati localmente.

### Modifica riquadro {#edit-pane}

Il **riquadro di modifica** consente di visualizzare il contenuto del file attualmente selezionato nell&#39;archivio. Ogni file aperto viene rappresentato come la relativa scheda nel riquadro.

La scheda **Home** consente di eseguire ricerche nel contenuto e/o nella documentazione e di accedere alla documentazione per gli sviluppatori e al supporto di Adobe.

Fare doppio clic su un file nel **riquadro di Explorer** per visualizzarne il contenuto nel **riquadro di modifica**. Puoi quindi modificarlo e salvare le modifiche.

Dopo aver modificato un file nel **riquadro di modifica**, sulla barra degli strumenti sono disponibili i seguenti strumenti:

* **Mostra nella struttura** - Mostra il file nella struttura dell&#39;archivio.
* **Ricerca/Sostituzione** - Esegue una ricerca o una sostituzione.

Fare doppio clic sulla riga di stato del **riquadro di modifica** per aprire la finestra di dialogo **Vai alla riga** e immettere un numero di riga specifico.

### Scheda Proprietà {#properties-tab}

La **scheda Proprietà** visualizza le proprietà del nodo selezionato. Puoi aggiungere nuove proprietà o eliminare quelle esistenti.

### Scheda Controllo accesso {#access-control-tab}

La **scheda Controllo di accesso** visualizza le autorizzazioni in base al percorso, all&#39;archivio o all&#39;entità corrente.

Le autorizzazioni sono suddivise nelle seguenti categorie.

* **Criteri di controllo di accesso applicabili** - Criteri che possono essere applicati alla selezione corrente
* **Criteri di controllo dell&#39;accesso locali** - Criteri correnti applicati localmente alla selezione corrente
* **Criteri di controllo dell&#39;accesso effettivi** - I criteri correnti applicati per la selezione corrente, che potrebbero essere impostati localmente o ereditati dai nodi padre

>[!NOTE]
>
>Per poter visualizzare le informazioni sul controllo di accesso, l’utente che ha effettuato l’accesso a CRXDE Lite deve disporre dei diritti per la lettura delle voci ACL.

### Scheda Replica {#replication-tab}

La **scheda Replica** visualizza lo stato di replica del nodo corrente. Puoi replicare e replicare per eliminare il nodo corrente.

### Scheda Console {#console-tab}

La **scheda Console** visualizza i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e abilitare/disabilitare la visualizzazione dei messaggi.

### Scheda Informazioni sulla build {#build-info-tab}

La **scheda Informazioni sulla compilazione** visualizza le informazioni durante la generazione di un bundle.

### Pulsante Aggiorna {#refresh-button}

Il **pulsante Aggiorna** aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella vista dell’archivio. Le modifiche apportate non vengono modificate.

### Pulsante Salva tutto {#save-all-button}

Il **pulsante Salva tutto** salva tutte le modifiche apportate. Fino a quando non scegli di salvare, le modifiche sono temporanee e vengono perse quando esci dalla console.

* **Ripristina** - Elimina tutte le modifiche apportate al nodo selezionato dall&#39;ultima azione di salvataggio, quindi ricarica lo stato corrente dell&#39;archivio per il nodo selezionato
* **Ripristina tutto** - Elimina tutte le modifiche apportate nell&#39;intero archivio dall&#39;ultima azione di salvataggio, quindi ricarica lo stato corrente dell&#39;archivio

### Pulsante Crea {#create-button}

Il **pulsante Crea** è un menu a discesa per creare quanto segue nel nodo selezionato:

* Nodo: un nodo con un tipo di nodo arbitrario
* File: un nodo `nt:file` e il relativo sottonodo nt:resource
* Cartella - un nodo `nt:folder`

### Pulsante Elimina {#delete-button}

Il **pulsante Elimina** elimina il nodo selezionato.

### Pulsante Copia {#copy-button}

Il **pulsante Copia** copia il nodo selezionato.

## Pulsante Incolla {#paste-button}

Il **pulsante Incolla** incolla il nodo copiato sotto il nodo selezionato.

### Pulsante Sposta {#move-button}

Il **pulsante Sposta** sposta il nodo selezionato nel nodo impostato tramite la finestra di dialogo.

### Rinomina {#rename-button}

Il **pulsante Rinomina** rinomina il nodo selezionato.

### Mixin {#mixins-button}

Il pulsante **Mixin** consente di aggiungere tipi mixin al tipo di nodo. I tipi mixin vengono utilizzati principalmente per aggiungere funzioni avanzate.

### Strumenti {#tools-button}

Il **pulsante Strumenti** è un menu a discesa con i seguenti strumenti disponibili:

* **Configurazione server** - per accedere alla console Felix (disponibile anche in `https://<host>:<port>/system/console/configMgr`)
* **Query** - per eseguire una query sull&#39;archivio
* **Privilegi** - per visualizzare e aggiungere privilegi
* **Verifica controllo dell&#39;accesso** - per verificare l&#39;autorizzazione per un determinato percorso e/o entità
* **Esporta tipo di nodo** - per esportare i tipi di nodo nel sistema come notazione CND
* **Importa tipo di nodo** - per importare tipi di nodo utilizzando la notazione CND.

### Widget di accesso {#login-widget}

Il **widget di accesso** visualizza l&#39;utente attualmente connesso.

Fai clic su di esso per accedere o accedere nuovamente come altro utente. `@crx.default` indica che ci si trova nell&#39;area di lavoro predefinita (e solo) nell&#39;archivio.

L&#39;opzione **Preferenze** può essere utilizzata per impostare la lingua dell&#39;interfaccia utente e per visualizzare e personalizzare i tasti di scelta rapida per varie azioni quali salvataggio, ricerca, creazione di note e così via.

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettere la cartella **Name** e fare clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel [**riquadro Exploerer**](#explorer-pane), fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, selezionare **Crea**, quindi **Crea nodo**.
1. Immetti **Name** e seleziona **Type**.
1. Fai clic su **OK**.
1. Fare clic sul pulsante [**Salva tutto**](#save-all-button) per salvare le modifiche nel server.

Ora puoi adattare il nodo alle tue esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
>
>La maggior parte delle operazioni di modifica, incluso **Crea nodo**, mantiene tutte le modifiche in memoria e le archivia nell&#39;archivio solo al momento del salvataggio (utilizzando il [**pulsante Salva tutto**](#save-all-button)). Tuttavia, alcune operazioni, come lo spostamento, vengono mantenute automaticamente.
>
>La convalida relativa all’autorizzazione o meno del nodo creato dal tipo di nodo del nodo principale viene eseguita anche dall’archivio durante il salvataggio delle modifiche. Se durante il salvataggio di un nodo viene visualizzato un messaggio di errore, verificare che la struttura del contenuto sia valida (ad esempio, non è possibile creare un nodo `nt:unstructured` come nodo figlio di `nt:folder`).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel [**riquadro Esplosione**](#explorer-pane), selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. Nella [**scheda Proprietà**](#properties-tab) nel riquadro inferiore, immettere **Nome**, **Tipo** e **Valore**.
1. Fai clic su **Aggiungi**.
1. Fare clic sul pulsante [**Salva tutto**](#save-all-button) per salvare le modifiche nel server.

## Creazione di un file {#creating-a-file}

Per creare un file con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel [**riquadro Esplora risorse**](#explorer-pane), fare clic con il pulsante destro del mouse sul componente in cui si desidera creare il file, selezionare **Crea**, quindi **Crea file**.
1. Immetti il file **Name** inclusa la relativa estensione.
1. Fai clic su **OK**.
1. Il nuovo file si apre come scheda nel [**riquadro di modifica**](#edit-pane).
1. Modifica il file.
1. Fare clic sul pulsante [**Salva tutto**](#save-all-button) per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo in [Notazione Compact Namespace and Node Type Definition (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare la definizione di un tipo di nodo in CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Seleziona il nodo richiesto.
1. Selezionare **Strumenti** e quindi **Esporta tipo di nodo**.
1. La definizione viene visualizzata in notazione CND in una nuova scheda nel browser.
1. Se necessario, salva le informazioni.

Per importare una definizione di tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona **Strumenti** e poi **Importa tipo di nodo**.
1. Nel [**riquadro di modifica**](#edit-pane) con etichetta **Importa tipo di nodo** viene visualizzata una nuova scheda.
1. Immettere la notazione CND per la definizione nella casella di testo della scheda **Importa tipo di nodo**.
1. Selezionare **Consenti aggiornamento** se si sta aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<aem-install-dir>/crx-quickstart/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Apri CRXDE Lite nel browser.
1. Nel menu a discesa sulla destra della [**scheda Console**](#console-tab) nella parte inferiore della finestra, seleziona **Registri server**.
1. Fai clic sull&#39;icona **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Regola i parametri di registro nella console Felix facendo clic sull&#39;icona **Configurazioni di registrazione**.
* Cancellare i messaggi facendo clic sull&#39;icona **Cancella console**.
* Aggiungere il messaggio alla selezione corrente facendo clic sull&#39;icona **Aggiungi console**.
* Attiva o disattiva la visualizzazione dei messaggi facendo clic sull&#39;icona **Interrompi**.
