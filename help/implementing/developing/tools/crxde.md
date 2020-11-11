---
title: Utilizzo di CRXDE Lite
description: CRXDE Lite fa parte del AEM quickstart ed è disponibile per accedere e modificare il repository negli ambienti di sviluppo locali all'interno del browser.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 0%

---


# Utilizzo di CRXDE Lite {#using-crxde-lite}

CRXDE Lite fa parte del AEM quickstart ed è disponibile per accedere e modificare il repository negli ambienti di sviluppo locali all&#39;interno del browser. Con CRXDE Lite, potete modificare file, cartelle, nodi e proprietà. L&#39;intero repository è accessibile tramite questa interfaccia di facile utilizzo.

>[!NOTE]
>
>CRXDE Lite è disponibile solo negli ambienti di sviluppo locali. Non è disponibile in AEM come Cloud Service.

## Guida introduttiva ai CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare con CRXDE Lite:

1. Avviate la procedura di sviluppo AEM locale.
1. Nel browser, aprite l’URL `https://<host>:<port>/crx/de`.
1. Inserite **nome utente** e **password**.
1. Fai clic su **OK**.

L’interfaccia utente CRXDE Lite si presenta come segue nel browser:

![Interfaccia CRXDE Lite](assets/crxde-lite.png)

È ora possibile utilizzare CRXDE Lite per sviluppare l&#39;applicazione.

>[!TIP]
>
>È inoltre possibile accedere al CRXDE Lite dal menu AEM. Dal menu principale selezionate **Strumenti** -> **Generali** -> **CRXDE Lite**.

## Panoramica dell&#39;interfaccia utente {#overview-of-the-user-interface}

L&#39;interfaccia utente di CRXDE Lite ha molte parti e molte funzioni.

### Barra di commutazione superiore {#top-switcher-bar}

La barra di commutazione superiore consente di passare rapidamente da CRXDE Lite, Package Manager e Package Share.

### Widget Percorso nodo {#node-path-widget}

Il widget Percorso nodo visualizza il percorso del nodo attualmente selezionato.

È inoltre possibile utilizzarlo per passare a un nodo immettendo il percorso a mano o incollandolo da un&#39;altra ubicazione e premendo Invio.

Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Immettere il nome del nodo da trovare e attendere (oppure selezionare l&#39;icona di ricerca sul lato destro). Se un nodo o nodi specifici vengono caricati nel riquadro di esplorazione, verrà visualizzato l&#39;elenco, quindi è possibile selezionare il percorso e premere Invio per individuare il percorso. Si noti che funziona solo per i nodi attualmente caricati nell&#39;applicazione client CRXDE nel browser. Se si desidera eseguire la ricerca nell&#39;intero repository, utilizzare **Strumenti** -&amp;gt: **Query**.

### Riquadro di Esplora risorse {#explorer-pane}

Nel riquadro **** Esplora risorse viene visualizzata una struttura ad albero di tutti i nodi della directory archivio.

Fare clic su un nodo per visualizzarne le proprietà nella scheda **Proprietà** . Dopo aver fatto clic su un nodo, è possibile selezionare un&#39;azione nella barra degli strumenti. Fare di nuovo clic sul nodo per rinominarlo.

Filtro navigazione albero (icona binocolo) consente di filtrare i nodi della directory archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi caricati localmente.

### Modifica riquadro {#edit-pane}

Il riquadro **** Modifica consente di visualizzare il contenuto del file attualmente selezionato nella directory archivio. Ogni file aperto sarà rappresentato come una propria scheda nel riquadro.

La scheda **Home** consente di eseguire ricerche nei contenuti e/o nella documentazione e di accedere alla documentazione per gli sviluppatori e al supporto  Adobe.

Fare doppio clic su un file nel riquadro **** Esplora risorse per visualizzarne il contenuto nel riquadro **** Modifica. Potete quindi modificarlo e salvare le modifiche.

Una volta modificato un file nel riquadro **di** modifica, nella barra degli strumenti sono disponibili i seguenti strumenti:

* **Mostra nella struttura** - Mostra il file nella struttura del repository.
* **Ricerca/Sostituisci** - Esegue una ricerca o una sostituzione.

Fare doppio clic sulla riga di stato del riquadro **di** modifica per aprire la finestra di dialogo **Vai alla riga** e immettere un numero di riga specifico.

### Scheda Proprietà {#properties-tab}

Nella scheda **** Proprietà sono visualizzate le proprietà del nodo selezionato. È possibile aggiungere nuove proprietà o eliminare quelle esistenti.

### Scheda Controllo accesso {#access-control-tab}

Nella scheda **Controllo** accesso sono visualizzate le autorizzazioni in base al percorso, all&#39;archivio o all&#39;entità corrente.

Le autorizzazioni sono suddivise nelle seguenti categorie.

* **Criterio** di controllo degli accessi applicabile - Criteri che possono essere applicati alla selezione corrente
* **Criteri** di controllo degli accessi locali - I criteri correnti applicati localmente alla selezione corrente
* **Criteri** di controllo di accesso effettivi - I criteri correnti applicati per la selezione corrente, che possono essere impostati localmente o ereditati dai nodi padre

>[!NOTE]
Per poter visualizzare le informazioni sul controllo di accesso, l&#39;utente che ha eseguito l&#39;accesso al CRXDE Lite deve disporre dei diritti per la lettura delle voci ACL.

### Scheda Replica {#replication-tab}

Nella scheda **** Replica viene visualizzato lo stato di replica del nodo corrente. È possibile replicare e replicare l&#39;eliminazione del nodo corrente.

###  Scheda Console {#console-tab}

Nella scheda **Console** sono visualizzati i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e attivare/disattivare la visualizzazione dei messaggi.

### Scheda Informazioni build {#build-info-tab}

Nella scheda **Informazioni** build sono visualizzate le informazioni durante la creazione di un bundle.

### Pulsante Aggiorna {#refresh-button}

Il pulsante **** Aggiorna aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella visualizzazione della directory archivio. Le modifiche apportate non vengono alterate.

### Salva tutto {#save-all-button}

Il pulsante **** Salva tutto consente di salvare tutte le modifiche apportate. Fino a quando non si sceglie di salvare, le modifiche sono temporanee e andranno perse quando si esce dalla console.

* **Ripristina** : tutte le modifiche apportate al nodo selezionato dall&#39;ultima azione di salvataggio vengono eliminate e quindi viene ricaricato lo stato corrente del repository per il nodo selezionato
* **Ripristina tutto** : tutte le modifiche apportate all&#39;intero repository dall&#39;ultima azione di salvataggio vengono eliminate, quindi viene ricaricato lo stato corrente dell&#39;archivio

### Pulsante Crea {#create-button}

Il pulsante **** Crea è un menu a discesa che consente di creare quanto segue sotto il nodo selezionato:

* Nodo: un nodo con un tipo di nodo arbitrario
* File: un `nt:file` nodo e il relativo nodo secondario nt:resource
* Cartella - un `nt:folder` nodo

### Delete Button {#delete-button}

Il pulsante **** Elimina elimina il nodo selezionato.

### Copy Button {#copy-button}

Il pulsante **** Copia copia il nodo selezionato.

## Paste Button {#paste-button}

Il pulsante **** Incolla incolla il nodo copiato sotto il nodo selezionato.

### Move Button {#move-button}

Il pulsante **** Sposta sposta il nodo selezionato sul nodo impostato nella finestra di dialogo.

### Rinomina {#rename-button}

Il pulsante **** Rinomina rinomina il nodo selezionato.

### Mixins {#mixins-button}

Il pulsante **** Mixins consente di aggiungere tipi di mixin al tipo di nodo. I tipi di mixin vengono utilizzati principalmente per aggiungere funzioni avanzate.

### Strumenti {#tools-button}

Il pulsante **** Strumenti è un menu a discesa con i seguenti strumenti disponibili:

* **Configurazione** server - per accedere alla console Felix (disponibile anche in `https://<host>:<port>/system/console/configMgr`)
* **Query** - per eseguire una query sull&#39;archivio
* **Privilegi** per visualizzare e aggiungere privilegi
* **Controllo** dell&#39;accesso di prova - per verificare l&#39;autorizzazione per un determinato percorso e/o entità
* **Esporta tipo** nodo - per esportare i tipi di nodi nel sistema come notazione CND
* **Importa tipo** di nodo: per importare tipi di nodi utilizzando la notazione CND.

### Widget di login {#login-widget}

Il widget di **accesso** visualizza l’utente attualmente connesso.

Fate clic su di esso per effettuare il login o effettuare nuovamente il login come altro utente. L’ `@crx.default` elemento rappresenta l’area di lavoro predefinita (e solo) nella directory archivio.

L’opzione **Preferenze** può essere utilizzata per impostare la lingua dell’interfaccia utente e per visualizzare e personalizzare i tasti di scelta rapida per varie azioni, quali salvataggio, ricerca, creazione di note e così via.

## Creating a Folder {#creating-a-folder}

Per creare una cartella con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettete il **nome** della cartella e fate clic su **OK**.

1. Fate clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro [**** Esplosore,](#explorer-pane) fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, selezionare **Crea**, quindi **Crea nodo**.
1. Immettere il **Nome** e selezionare il **Tipo**.
1. Fai clic su **OK**.
1. Fate clic sul pulsante [****](#save-all-button) Salva tutto per salvare le modifiche sul server.

È ora possibile adattare il nodo alle proprie esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
La maggior parte delle operazioni di modifica, incluso **Crea nodo**, conserva tutte le modifiche in memoria e le memorizza nella directory archivio solo dopo il salvataggio (utilizzando il pulsante [****](#save-all-button) Salva tutto). Tuttavia, alcune operazioni come quella di spostamento vengono automaticamente mantenute.
La convalida relativa all&#39;eventuale autorizzazione del nodo appena creato da parte del tipo di nodo padre viene eseguita anche dall&#39;archivio al momento del salvataggio delle modifiche. Se ricevete un messaggio di errore durante il salvataggio di un nodo, verificate che la struttura del contenuto sia valida (ad esempio, non è possibile creare un `nt:unstructured` nodo come figlio di un `nt:folder` nodo).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro [**** Esploratore,](#explorer-pane) selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. Nella scheda [****](#properties-tab) Proprietà del riquadro inferiore, immettere **Nome**, **Tipo** e **Valore**.
1. Fate clic su **Aggiungi**.
1. Fate clic sul pulsante [****](#save-all-button) Salva tutto per salvare le modifiche sul server.

## Creazione di un file {#creating-a-file}

Per creare un nuovo file con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro [**** Esplosore,](#explorer-pane) fare clic con il pulsante destro del mouse sul componente in cui si desidera creare il file, selezionare **Crea**, quindi **Crea file**.
1. Immettere il **nome** del file, inclusa l&#39;estensione.
1. Fai clic su **OK**.
1. Il nuovo file viene aperto come scheda nel riquadro [**** Modifica.](#edit-pane)
1. Modificate il file.
1. Click the [**Save All Button**](#save-all-button) to save the changes.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo nella notazione [CND (](https://jackrabbit.apache.org/jcr/node-type-notation.html)Compact Namespace and Node Type Definition).

Per esportare una definizione di tipo di nodo in CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Selezionare il nodo desiderato.
1. Selezionare **Strumenti** , quindi **Esporta tipo** nodo.
1. La definizione verrà visualizzata nella notazione CND in una nuova scheda del browser.
1. Se necessario, salvate le informazioni.

Per importare una definizione di tipo di nodo:

1. Aprite il CRXDE Lite nel browser.
1. Selezionare **Strumenti** , quindi **Importa tipo** di nodo.
1. Nel riquadro [**Modifica**](#edit-pane) viene visualizzata una nuova scheda con l’etichetta Tipo **nodo** importazione.
1. Immettete la notazione CND per la definizione nella casella di testo della scheda **Importa tipo** nodo.
1. Se state aggiornando una definizione esistente, selezionate **Consenti aggiornamento** .
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<aem-install-dir>/crx-quickstart/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Aprite il CRXDE Lite nel browser.
1. Nel menu a discesa a destra della scheda [****](#console-tab) Console nella parte inferiore della finestra, selezionate Registri **** server.
1. Fai clic sull&#39;icona **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Per regolare i parametri di registro nella console Felix, fai clic sull’icona **Registrazioni configurazioni** .
* Cancella i messaggi facendo clic sull&#39;icona **Cancella console** .
* Per fissare il messaggio alla selezione corrente, fai clic sull’icona **Fissa console** .
* Abilita o disabilita la visualizzazione dei messaggi facendo clic sull&#39;icona **Interrompi** .
