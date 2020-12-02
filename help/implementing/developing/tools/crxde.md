---
title: Utilizzo di CRXDE Lite
description: CRXDE Lite fa parte del AEM quickstart ed è disponibile per accedere e modificare il repository negli ambienti di sviluppo locali all'interno del browser.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 0%

---


# Utilizzo del CRXDE Lite {#using-crxde-lite}

CRXDE Lite fa parte del AEM quickstart ed è disponibile per accedere e modificare il repository negli ambienti di sviluppo locali all&#39;interno del browser. Con CRXDE Lite, potete modificare file, cartelle, nodi e proprietà. L&#39;intero repository è accessibile tramite questa interfaccia di facile utilizzo.

>[!NOTE]
>
>CRXDE Lite è disponibile solo negli ambienti di sviluppo locali. Non è disponibile in AEM come Cloud Service.

## Guida introduttiva all&#39;CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare con CRXDE Lite:

1. Avviate la procedura di sviluppo AEM locale.
1. Nel browser, aprite l&#39;URL `https://<host>:<port>/crx/de`.
1. Immettere **username** e **password**.
1. Fai clic su **OK**.

L’interfaccia utente CRXDE Lite si presenta come segue nel browser:

![Interfaccia CRXDE Lite](assets/crxde-lite.png)

È ora possibile utilizzare CRXDE Lite per sviluppare l&#39;applicazione.

>[!TIP]
>
>È inoltre possibile accedere al CRXDE Lite dal menu AEM. Dal menu principale, selezionare **Strumenti** -> **Generale** -> **CRXDE Lite**.

## Panoramica dell&#39;interfaccia utente {#overview-of-the-user-interface}

L&#39;interfaccia utente di CRXDE Lite ha molte parti e molte funzioni.

### Barra di commutazione superiore {#top-switcher-bar}

La barra di commutazione superiore consente di passare rapidamente da CRXDE Lite, Package Manager e Package Share.

### Widget percorso nodo {#node-path-widget}

Il widget Percorso nodo visualizza il percorso del nodo attualmente selezionato.

È inoltre possibile utilizzarlo per passare a un nodo immettendo il percorso a mano o incollandolo da un&#39;altra ubicazione e premendo Invio.

Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Immettere il nome del nodo da trovare e attendere (oppure selezionare l&#39;icona di ricerca sul lato destro). Se un nodo o nodi specifici vengono caricati nel riquadro di esplorazione, verrà visualizzato l&#39;elenco, quindi è possibile selezionare il percorso e premere Invio per individuare il percorso. Si noti che funziona solo per i nodi attualmente caricati nell&#39;applicazione client CRXDE nel browser. Se si desidera eseguire una ricerca nell&#39;intero repository, utilizzare **Strumenti** -&amp;gt: **Query**.

### Riquadro Esplora risorse {#explorer-pane}

Nel riquadro **Esplora risorse** viene visualizzata una struttura ad albero di tutti i nodi della directory archivio.

Fare clic su un nodo per visualizzarne le proprietà nella scheda **Proprietà**. Dopo aver fatto clic su un nodo, è possibile selezionare un&#39;azione nella barra degli strumenti. Fare di nuovo clic sul nodo per rinominarlo.

Filtro navigazione albero (icona binocolo) consente di filtrare i nodi della directory archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi caricati localmente.

### Riquadro di modifica {#edit-pane}

Il **riquadro di modifica** consente di visualizzare il contenuto del file attualmente selezionato nella directory archivio. Ogni file aperto sarà rappresentato come una propria scheda nel riquadro.

La scheda **Home** consente di eseguire ricerche nei contenuti e/o nella documentazione e di accedere alla documentazione sviluppatore e al supporto  Adobe.

Fare doppio clic su un file nel **riquadro Esplora risorse** per visualizzarne il contenuto nel **riquadro di modifica**. Potete quindi modificarlo e salvare le modifiche.

Dopo aver modificato un file nel **riquadro di modifica**, sulla barra degli strumenti sono disponibili i seguenti strumenti:

* **Mostra nella struttura ad albero** : mostra il file nella struttura ad albero del repository.
* **Ricerca/Sostituisci**  - Esegue una ricerca o una sostituzione.

Fare doppio clic sulla riga di stato del **riquadro di modifica** per aprire la finestra di dialogo **Vai alla riga** in modo da inserire un numero di riga specifico.

### Scheda Proprietà {#properties-tab}

Nella scheda **Proprietà** vengono visualizzate le proprietà del nodo selezionato. È possibile aggiungere nuove proprietà o eliminare quelle esistenti.

### Scheda Controllo accesso {#access-control-tab}

La **scheda Controllo accesso** visualizza le autorizzazioni in base al percorso, al repository o all&#39;entità corrente.

Le autorizzazioni sono suddivise nelle seguenti categorie.

* **Criterio**  di controllo degli accessi applicabile - Criteri che possono essere applicati alla selezione corrente
* **Criteri**  di controllo degli accessi locali - I criteri correnti applicati localmente alla selezione corrente
* **Criteri**  di controllo di accesso effettivi - Criteri correnti applicati per la selezione corrente, che possono essere impostati localmente o ereditati dai nodi padre

>[!NOTE]
Per poter visualizzare le informazioni sul controllo di accesso, l&#39;utente che ha eseguito l&#39;accesso al CRXDE Lite deve disporre dei diritti per la lettura delle voci ACL.

### Scheda Replica {#replication-tab}

La scheda **Replica** visualizza lo stato di replica del nodo corrente. È possibile replicare e replicare l&#39;eliminazione del nodo corrente.

###  Scheda Console {#console-tab}

Nella scheda **Console** vengono visualizzati i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e attivare/disattivare la visualizzazione dei messaggi.

### Scheda Informazioni build {#build-info-tab}

La **scheda Informazioni build** visualizza informazioni quando viene creato un bundle.

### Pulsante Aggiorna {#refresh-button}

Il **Pulsante Aggiorna** aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella visualizzazione della directory archivio. Le modifiche apportate non vengono alterate.

### Salva tutto {#save-all-button}

Il **Pulsante Salva tutto** salva tutte le modifiche apportate. Fino a quando non si sceglie di salvare, le modifiche sono temporanee e andranno perse quando si esce dalla console.

* **Ripristina** : tutte le modifiche apportate al nodo selezionato dall&#39;ultima azione di salvataggio vengono eliminate e quindi viene ricaricato lo stato corrente del repository per il nodo selezionato
* **Ripristina tutto** : ignora tutte le modifiche apportate all’intero repository dall’ultima azione di salvataggio, quindi ricarica lo stato corrente dell’archivio

### Pulsante Crea {#create-button}

Il **Pulsante Crea** è un menu a discesa per creare quanto segue sotto il nodo selezionato:

* Nodo: un nodo con un tipo di nodo arbitrario
* File - un nodo `nt:file` e il relativo nodo secondario nt:resource
* Cartella - un nodo `nt:folder`

### Pulsante Elimina {#delete-button}

Il **Pulsante Elimina** elimina il nodo selezionato.

### Pulsante Copia {#copy-button}

Il **Pulsante Copia** copia il nodo selezionato.

## Pulsante Incolla {#paste-button}

Il **Pulsante Incolla** incolla il nodo copiato sotto il nodo selezionato.

### Pulsante Sposta {#move-button}

Il **Pulsante Sposta** sposta il nodo selezionato sul nodo impostato attraverso la finestra di dialogo.

### Rinomina {#rename-button}

Il **Pulsante Rinomina** rinomina il nodo selezionato.

### Mixins {#mixins-button}

Il **Pulsante Mixins** consente di aggiungere tipi di mixin al tipo di nodo. I tipi di mixin vengono utilizzati principalmente per aggiungere funzioni avanzate.

### Strumenti {#tools-button}

Il **Pulsante Strumenti** è un menu a discesa con i seguenti strumenti disponibili:

* **Configurazione**  server - per accedere alla console Felix (disponibile anche in  `https://<host>:<port>/system/console/configMgr`)
* **Query** - per eseguire una query sull&#39;archivio
* **Privilegi**  per visualizzare e aggiungere privilegi
* **Controllo**  dell&#39;accesso di prova - per verificare l&#39;autorizzazione per un determinato percorso e/o entità
* **Esporta tipo**  nodo - per esportare i tipi di nodi nel sistema come notazione CND
* **Importa tipo**  nodo - per importare i tipi di nodi utilizzando la notazione CND.

### Widget di login {#login-widget}

Il **Widget di accesso** visualizza l&#39;utente attualmente connesso.

Fate clic su di esso per effettuare il login o effettuare nuovamente il login come altro utente. L&#39; `@crx.default` rappresenta l&#39;utente che si trova nell&#39;area di lavoro predefinita (e solo) nella directory archivio.

L&#39;opzione **Preferenze** può essere utilizzata per impostare la lingua dell&#39;interfaccia utente e per visualizzare e personalizzare i tasti di scelta rapida per diverse azioni, ad esempio salvare, cercare, creare note e così via.

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettere la cartella **Name** e fare clic su **OK**.

1. Fare clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel [**riquadro Esploratore**,](#explorer-pane) fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, selezionare **Crea**, quindi **Crea nodo**.
1. Immettere il **Nome** e selezionare il **Tipo**.
1. Fai clic su **OK**.
1. Fare clic sul pulsante [**Salva tutto**](#save-all-button) per salvare le modifiche sul server.

È ora possibile adattare il nodo alle proprie esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
La maggior parte delle operazioni di modifica, inclusa la **Crea nodo**, conserva tutte le modifiche in memoria e le memorizza solo nella directory archivio al momento del salvataggio (utilizzando il [**Salva tutto pulsante**](#save-all-button)). Tuttavia, alcune operazioni come quella di spostamento vengono automaticamente mantenute.
La convalida relativa all&#39;eventuale autorizzazione del nodo appena creato da parte del tipo di nodo padre viene eseguita anche dall&#39;archivio al momento del salvataggio delle modifiche. Se ricevete un messaggio di errore durante il salvataggio di un nodo, verificate che la struttura del contenuto sia valida (ad esempio, non potete creare un nodo `nt:unstructured` come elemento secondario di `nt:folder` nodo).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel [**riquadro dell&#39;esploratore**,](#explorer-pane) selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. Nella scheda [**Proprietà**](#properties-tab) del riquadro inferiore, immettere **Nome**, **Tipo** e **Valore**.
1. Fate clic su **Aggiungi**.
1. Fare clic sul pulsante [**Salva tutto**](#save-all-button) per salvare le modifiche sul server.

## Creazione di un file {#creating-a-file}

Per creare un nuovo file con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel [**riquadro Esploratore**,](#explorer-pane) fare clic con il pulsante destro del mouse sul componente in cui si desidera creare il file, selezionare **Crea**, quindi **Crea file**.
1. Immettere il file **Name**, inclusa l&#39;estensione.
1. Fai clic su **OK**.
1. Il nuovo file viene aperto come scheda nel [**riquadro di modifica**.](#edit-pane)
1. Modificate il file.
1. Fare clic sul pulsante [**Salva tutto**](#save-all-button) per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo in [Nomi compatti e Definizione del tipo di nodo (CND) notazione](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare una definizione di tipo di nodo in CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Selezionare il nodo desiderato.
1. Selezionare **Strumenti**, quindi **Esporta tipo di nodo**.
1. La definizione verrà visualizzata nella notazione CND in una nuova scheda del browser.
1. Se necessario, salvate le informazioni.

Per importare una definizione di tipo di nodo:

1. Aprite il CRXDE Lite nel browser.
1. Selezionare **Strumenti**, quindi **Importa tipo di nodo**.
1. Si apre una nuova scheda nel [**riquadro di modifica**](#edit-pane) con etichetta **Importa tipo di nodo**.
1. Immettere la notazione CND per la definizione nella casella di testo della scheda **Importa tipo di nodo**.
1. Selezionare **Consenti aggiornamento** se si sta aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<aem-install-dir>/crx-quickstart/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Aprite il CRXDE Lite nel browser.
1. Nel menu a discesa nella parte destra della [**scheda Console**](#console-tab) nella parte inferiore della finestra, selezionare **Registri server**.
1. Fare clic sull&#39;icona **Stop** per visualizzare i messaggi.

Operazioni disponibili:

* Per regolare i parametri di registro nella console Felix, fai clic sull&#39;icona **Configurazioni di registrazione**.
* Cancella i messaggi facendo clic sull&#39;icona **Cancella console**.
* Fissare il messaggio alla selezione corrente facendo clic sull&#39;icona **Fissa console**.
* Abilita o disabilita la visualizzazione dei messaggi facendo clic sull&#39;icona **Stop**.
