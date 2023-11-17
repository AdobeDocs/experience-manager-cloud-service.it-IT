---
title: Creazione e organizzazione delle pagine
description: Scopri come organizzare il sito web creando e gestendo pagine con AEM.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2429'
ht-degree: 86%

---


# Creazione e organizzazione delle pagine {#creating-and-organizing-pages}

Questo documento illustra come creare e gestire le pagine in Adobe Experience Manager Cloud Service, per poi [creare contenuti](/help/sites-cloud/authoring/fundamentals/editing-content.md) su di esse.

>[!NOTE]
>
>Il tuo account necessita dei diritti di accesso e delle autorizzazioni adeguati per intervenire sulle pagine, ad esempio per creare, copiare, spostare, modificare ed eliminare elementi.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to act on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Ce ne sono diversi [scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) che puoi utilizzare dalla console dei siti web per organizzare le pagine in modo più efficiente.

{{edge-delivery-authoring}}

## Organizzazione del sito web {#organizing-your-website}

In qualità di autore, devi organizzare il tuo sito web all’interno dell’AEM. A tale scopo, dovrai creare e denominare le pagine di contenuto affinché:

* siano facilmente reperibili nell’ambiente di authoring;
* i visitatori possano facilmente sfogliare le pagine nell’ambiente di pubblicazione.

È inoltre possibile utilizzare le [cartelle](#creating-a-new-folder) per organizzare i contenuti.

La struttura del sito web è analoga a una struttura ad albero contenente le pagine dei contenuti. I nomi di queste pagine vengono utilizzati per formare gli URL, mentre i titoli vengono mostrati durante la visualizzazione del contenuto della pagina.

Di seguito è riportato un esempio tratto dal sito [WKND Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it), in cui è possibile accedere a un articolo sugli skatepark ( `la-skateparks`):

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Questa struttura può essere visualizzata dalla console **Sites**, che consente di [navigare tra le varie pagine del sito web](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e di eseguire azioni sulle pagine. È possibile, inoltre, creare nuovi siti e [nuove pagine](#creating-a-new-page).

Da qualsiasi punto, puoi vedere il ramo verso l’alto dalle breadcrumb nella barra dell’intestazione:

![Utilizzo delle breadcrumb per la navigazione](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### Convenzioni di denominazione delle pagine {#page-naming-conventions}

Durante la creazione di una pagina sono disponibili due campi chiave:

* **[Titolo](#title)**:

   * Viene mostrato all’utente nella console ed è disponibile sopra il contenuto della pagina durante la modifica.
   * Questo campo è obbligatorio.

* **[Nome](#name)**:

   * Viene utilizzato per generare l’URI.
   * L’input dell’utente per questo campo è opzionale. Se non viene specificato, il nome viene derivato dal titolo. Per ulteriori dettagli, consulta la seguente sezione sulle [restrizioni e best practice per i nomi delle pagine](#page-name-restrictions-and-best-practices).

#### Restrizioni e best practice per i nomi delle pagine {#page-name-restrictions-and-best-practices}

Il **Titolo** e il **Nome** della pagina possono essere creati separatamente, ma sono correlati:

* Quando crei una pagina, l’unico campo obbligatorio è quello del **Titolo**. Se non viene fornito un **Nome** al momento della creazione della pagina, AEM ne genera uno dai primi 64 caratteri del titolo (rispettando le norme di convalida descritte di seguito). Per rispettare la best practice sui nomi di pagina brevi, vengono utilizzati solo i primi 64 caratteri.
* Se un nome di una pagina è specificato manualmente dall’autore, il limite di 64 caratteri non è applicabile; tuttavia, potrebbero esserci altre limitazioni tecniche sulla lunghezza del nome della pagina.

>[!TIP]
>
>Quando si definisce un nome di una pagina, è buona norma mantenere il nome breve, che deve comunque essere espressivo e facile da ricordare, in modo che il lettore possa facilmente comprenderlo. Per ulteriori informazioni, consulta la [guida allo stile W3C ](https://www.w3.org/Provider/Style/TITLE.html) per l’elemento `title`.
>
>Tieni presente che alcuni browser (ad esempio le versioni precedenti di IE) possono accettare solo gli URL fino a una certa lunghezza; pertanto, esistono anche delle ragioni tecniche per cui è bene mantenere brevi i nomi di pagina.

Durante la creazione di una pagina, AEM [convalida il nome della pagina in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposto dall&#39;AEM e dal JCR.

I caratteri minimi consentiti sono:

* Da `a` a `z`
* Da `A` a `Z`
* Da `0` a `9`
* `_` (trattino basso)
* `-` (trattino/segno meno)

Per informazioni complete su tutti i caratteri consentiti, consulta le [convenzioni di denominazione](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>I nomi delle pagine non possono superare i 150 caratteri.

#### Titolo {#title}

Se si specifica solo una pagina **Titolo** quando si crea una pagina, l’AEM la deriva **Nome** da questa stringa e [convalida il nome in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposto dall&#39;AEM e dal JCR.

Un campo **Titolo** che contiene caratteri non validi viene accettato, ma nel nome derivato dal titolo tali caratteri vengono sostituiti. Ad esempio:

| Titolo | Nome derivato |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

#### Nome {#name}

Quando si specifica una pagina **Nome** durante la creazione di una pagina, AEM [convalida il nome in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposto dall&#39;AEM e dal JCR. Non è possibile utilizzare caratteri non validi nel campo **Nome**. Quando AEM rileva caratteri non validi, il campo viene evidenziato con un messaggio esplicativo.

![Esempio di immissione di un nome di pagina non valido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>È consigliabile evitare di utilizzare, come nome di pagina, codici di due lettere specificati dallo standard ISO-639-1, a meno che non si tratti dell’identificativo della lingua.
>
>Per ulteriori informazioni, consulta l’argomento relativo alla [preparazione dei contenuti per la traduzione](/help/sites-cloud/administering/translation/preparation.md).

### Modelli {#templates}

In AEM, un modello specifica un tipo di pagina particolare. Un modello viene utilizzato come base per qualsiasi nuova pagina creata.

Il modello definisce la struttura di una pagina, comprese una miniatura e altre proprietà. Ad esempio, puoi usare modelli distinti per pagine di prodotti, sitemap e informazioni di contatto. I modelli sono costituiti da [componenti](#components).

AEM viene fornito con diversi modelli preconfigurati. I modelli disponibili dipendono dal singolo sito web. I campi chiave sono i seguenti:

* **Titolo**
Il titolo visualizzato nella pagina web risultante.

* **Nome**
Utilizzato per la denominazione della pagina.

* **Modello**
Elenco di modelli disponibili per la generazione della nuova pagina.

>[!TIP]
>
>Se la configurazione dell’istanza lo prevede, [gli autori di modelli possono creare modelli con l’Editor modelli](/help/sites-cloud/authoring/features/templates.md).

### Componenti {#components}

I componenti sono gli elementi forniti da AEM che consentono di aggiungere specifici tipi di contenuto. AEM è dotato di una serie di componenti pronti all’uso che offrono funzionalità complete. Comprendono:

* Testo
* Immagine
* Titolo
* Carosello
* E molti altri

Dopo aver creato e aperto una pagina puoi [aggiungervi il contenuto utilizzando i componenti](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component), disponibili nel [browser componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>La [console Componenti](/help/sites-cloud/authoring/features/components-console.md) fornisce una panoramica dei componenti utilizzati nell’istanza.

## Gestione delle pagine {#managing-pages}

### Creazione di una nuova pagina {#creating-a-new-page}

A meno che le pagine non siano già state create tutte, prima di poter iniziare a creare il contenuto dovrai creare una pagina:

1. Apri la console Sites (ad esempio `https://<host>:<port>/sites.html/content`.
1. Passa alla posizione in cui desideri creare la nuova pagina.
1. Apri il selettore a discesa utilizzando l’opzione **Crea** nella barra degli strumenti, quindi seleziona **Pagina** dall’elenco:

   ![Creazione di una pagina](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. Nel primo passaggio della creazione guidata puoi effettuare le seguenti operazioni:

   * Seleziona il modello da utilizzare per creare la nuova pagina, quindi seleziona **Successivo** per procedere.

   * Seleziona **Annulla** per interrompere la procedura.

   ![Selezione di un modello per una nuova pagina](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Nell’ultimo passaggio della creazione guidata puoi effettuare le seguenti operazioni:

   * Utilizza le tre schede per inserire [proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md) vuoi assegnarlo alla nuova pagina, quindi seleziona **Crea** per creare effettivamente la pagina.

   * Utilizza **Indietro** per tornare alla selezione del modello.

   I campi chiave sono:

   * **Titolo**:

      * Questo viene presentato all’utente ed è obbligatorio.

   * **Nome**:

      * Viene utilizzato per generare l’URI. Se non viene specificato, il nome viene derivato dal titolo.
      * Se si specifica una pagina **Nome** durante la creazione di una pagina, AEM [convalida il nome in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposto dall&#39;AEM e dal JCR.
      * **Non è possibile utilizzare caratteri non validi** nel campo **Nome**. Quando AEM rileva caratteri non validi, il campo viene evidenziato e viene visualizzato un messaggio esplicativo per indicare i caratteri da rimuovere o sostituire.

   >[!TIP]
   >
   >Consulta [Convenzioni di denominazione delle pagine](#page-naming-conventions).

   Le informazioni minime necessarie per creare una pagina sono **Titolo**.

   ![Fornire il titolo della pagina](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Tocca o fai clic su **Crea** per completare il processo e creare la nuova pagina. Viene visualizzata una finestra di dialogo di conferma in cui viene richiesto se desideri **aprire** subito la pagina o ritornare alla console (selezionando **Fine**):

   ![Creazione pagina completata](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Se per la pagina creata hai specificato un nome già esistente nello stesso percorso, viene automaticamente generata una variante del nome aggiungendo un numero. Se, ad esempio, esiste già `beach`, la nuova pagina diventa `beach1`.

1. Se ritorni alla console puoi visualizzare la nuova pagina:

   ![Nuova pagina risultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Una volta creata una pagina, il relativo modello non può essere modificato, a meno di [creare un lancio con un nuovo modello](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), anche se questo determinerà la perdita di eventuali contenuti esistenti.

### Apertura di una pagina per la modifica {#opening-a-page-for-editing}

Dopo aver creato una pagina o essere passato a una pagina esistente (nella console), puoi aprirla per modificarla:

1. Apri la console **Sites**.
1. Individua la pagina da modificare.
1. Seleziona la pagina mediante:

   * [Azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e barra degli strumenti

   Quindi seleziona l’icona **Modifica**:

   Pulsante ![Modifica](/help/sites-cloud/authoring/assets/edit.png)

1. La pagina verrà aperta e potrai [modificarla](/help/sites-cloud/authoring/fundamentals/editing-content.md) secondo necessità.

>[!NOTE]
>
>La navigazione verso altre pagine dall’Editor pagina è possibile solo in modalità Anteprima, in quanto i collegamenti non sono attivi nella modalità di modifica.

### Copiare e incollare una pagina    {#copying-and-pasting-a-page}

Puoi copiare una pagina e tutte le relative sottopagine in una nuova posizione:

1. Nella console **Sites**, individua la pagina da copiare.
1. Seleziona la pagina mediante:

   * [Azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e barra degli strumenti

   E quindi l’icona **Copia** pagina:

   ![Copia](/help/sites-cloud/authoring/assets/copy.png)

1. Passa al percorso in cui desideri inserire la nuova copia della pagina.
1. Seleziona la **Incolla** che è diventata disponibile.

   ![Incolla](/help/sites-cloud/authoring/assets/paste.png)

1. La finestra di dialogo Incolla presenta un riepilogo della transazione della funzione incolla e la possibilità di:
   * **Nuovo nome sito:** modificare il nome della pagina incollata
   * **Incolla senza elementi figlio:** ometti le pagine figlie della pagina selezionata quando si incollano (per impostazione predefinita le pagine figlie vengono incollate)

   ![Finestra di dialogo Incolla](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Seleziona la **Incolla** per confermare la transazione e creare le nuove pagine.

>[!NOTE]
>
>Se copi la pagina in un percorso in cui esiste già una pagina con lo stesso nome dell’originale, viene automaticamente generata una variante del nome aggiungendo un numero. Ad esempio, se `beach` esiste già, una nuova pagina con il nome `beach` diventerà `beach1`.

>[!NOTE]
>
>Se si avvia l’azione incolla in modalità selezione, questa viene chiusa automaticamente non appena la pagina viene copiata.

### Spostamento o ridenominazione di una pagina {#moving-or-renaming-a-page}

La procedura per spostare o rinominare una pagina è sostanzialmente la stessa ed entrambe le azioni sono gestite dalla procedura guidata Sposta pagina. Con questa procedura guidata è possibile:

* Rinominare una pagina senza spostarla
* Spostare la pagina senza rinominarla
* Spostare e rinominare allo stesso tempo

In AEM è disponibile una funzionalità che consente di aggiornare eventuali collegamenti interni che rimandano alla pagina da rinominare/spostare. Questa operazione può essere eseguita a livello di singola pagina, per assicurare la massima flessibilità.

1. Individua la pagina da spostare.
1. Seleziona la pagina mediante:

   * [Azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) e barra degli strumenti

   Quindi seleziona l’icona **Sposta** pagina:

   ![Pulsante Sposta](/help/sites-cloud/authoring/assets/move.png)

   Verrà avviata la procedura guidata Sposta pagina.

1. Dal passaggio **Rinomina** della procedura guidata, puoi effettuare le seguenti operazioni:

   * Specifica il nome da assegnare alla pagina spostata, quindi seleziona **Successivo** per procedere.
   * Seleziona **Annulla** per interrompere la procedura.

   ![Spostare e rinominare la pagina](/help/sites-cloud/authoring/assets/move-page-rename.png)

   Il nome della pagina può rimanere invariato se si sta solo spostando la pagina.

   >[!NOTE]
   >
   >Se sposti la pagina in una posizione in cui esiste già una pagina con lo stesso nome, il sistema genera automaticamente una variante del nome aggiungendo un numero. Ad esempio, se `beach` esiste già, una nuova pagina con il nome `beach` diventerà `beach1`.

1. Nel passaggio **Seleziona destinazione** della procedura guidata, puoi effettuare le seguenti operazioni:

   * Utilizza la [vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) per accedere alla nuova posizione della pagina:

      * Seleziona la destinazione facendo clic sulla miniatura della destinazione.
      * Fai clic su **Avanti** per continuare.

   * Utilizza **Indietro** per specificare di nuovo il nome della pagina.

   >[!NOTE]
   >
   >Per impostazione predefinita, l’elemento principale della pagina che stai spostando/rinominando viene selezionato come destinazione.

   ![Selezionare la destinazione di spostamento della pagina](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Se sposti la pagina in una posizione in cui esiste già una pagina con lo stesso nome, il sistema genera automaticamente una variante del nome aggiungendo un numero. Se, ad esempio, `winter` esiste già, `winter` diventerà `winter1`.

1. Se la pagina è collegata o utilizzata in un riferimento, oppure se è stata pubblicata, i dettagli saranno elencati nel passaggio **Regola/Ripubblica**.

   Puoi quindi indicare cosa deve essere regolato e/o ripubblicato in base alle necessità.

   >[!NOTE]
   >
   >Se la pagina non è collegata né è soggetta a riferimenti, questo passaggio non sarà disponibile.

   ![Ripubblica pagina in spostamento](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Se selezioni **Sposta**, verrà completato il processo e la pagina verrà spostata/rinominata nel modo appropriato.

>[!NOTE]
>
>Se la pagina è già stata pubblicata, lo spostamento ne determina automaticamente l’annullamento della pubblicazione. Per impostazione predefinita, viene ripubblicata al termine dello spostamento, ma questo comportamento può essere modificato deselezionando il campo **Ripubblica** nel passaggio **Regola/Ripubblica**.

>[!NOTE]
>
>Se non è presente alcun riferimento alla pagina, il passaggio **Regola/Ripubblica** verrà ignorato.

>[!NOTE]
>
>La ridenominazione di una pagina è inoltre soggetta a [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nuovo nome della pagina.

>[!NOTE]
>
>Una pagina può essere spostata solo in una posizione in cui è consentito il modello su cui si basa la pagina. Per ulteriori informazioni consulta la sezione dedicata alla [disponibilità dei modelli](/help/implementing/developing/components/templates.md#template-availability).

#### Azioni asincrone {#asynchronous-actions}

Le azioni di spostamento delle pagine vengono sempre elaborate in modo asincrono, consentendo all’utente di continuare a creare nell’interfaccia utente senza ostacoli.

* È l’utente a definire quando deve essere eseguita l’operazione asincrona.
   * **Ora** inizia subito l’esecuzione del processo asincrono.
   * **In seguito** consente di definire quando verrà avviato il processo asincrono.

<!--
  ![Asynchronous page move](assets/asynchronous-page-move.png)
-->

Lo stato dei processi asincroni può essere controllato in [**Stato processi asincroni** dashboard](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) a **Navigazione globale** > **Strumenti** > **Operazioni** > **Processi**

>[!NOTE]
>
>Per ulteriori informazioni sull’esecuzione asincrona dei processi e su come configurare il limite per le azioni di spostamento o ridenominazione delle pagine, consulta il documento [Processi asincroni](/help/operations/asynchronous-jobs.md) nella guida utente per le operazioni.

### Eliminazione di una pagina {#deleting-a-page}

1. Spostati fino a visualizzare la pagina da eliminare.
1. Utilizza la [modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) per selezionare la pagina richiesta, quindi utilizza **Elimina** dalla barra degli strumenti:

   ![Pulsante Elimina](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >Come precauzione di sicurezza, l’icona **Elimina** pagina non è disponibile come azione rapida.

1. Una finestra di dialogo chiederà una conferma.

   ![Finestra di dialogo Elimina](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Intendi archiviare le pagine prima di eliminarle?** - Se questa opzione è selezionata, al momento dell’eliminazione verranno create versioni delle pagine selezionate da eliminare.
      * [Le versioni possono essere ripristinate in un momento successivo](/help/sites-cloud/authoring/features/page-versions.md).
      * Le pagine eliminate senza versioni precedenti non possono essere ripristinate.
   * **Annulla** per interrompere l’azione
   * **Elimina** per confermare l’azione:

      * Se la pagina non contiene riferimenti, viene eliminata.
      * Se la pagina include riferimenti, viene visualizzata una finestra con il messaggio **Si fa riferimento a una o più pagine.** È possibile selezionare **Forza eliminazione** o **Annulla**.

>[!NOTE]
>
>Se una pagina è già stata pubblicata, prima di eliminarla ne verrà automaticamente annullata la pubblicazione.

### Blocco di una pagina   {#locking-a-page}

È possibile [bloccare/sbloccare una pagina](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) da una console o quando si modifica una singola pagina. L’indicazione relativa al fatto che una pagina sia bloccata o meno è visualizzata in entrambe le posizioni.

![Pulsante Blocca](/help/sites-cloud/authoring/assets/lock.png)
![Pulsante Sblocca](/help/sites-cloud/authoring/assets/unlock.png)

### Creazione di una nuova cartella {#creating-a-new-folder}

Puoi creare cartelle per organizzare file e pagine.

1. Apri la console **Sites** e passa alla posizione desiderata.
1. Per aprire l’elenco delle opzioni, seleziona **Crea** dalla barra degli strumenti
1. Seleziona **Cartella** per aprire la finestra di dialogo. Nella finestra puoi immettere il **Nome** e il **Titolo**:

   ![Crea cartella](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Seleziona **Crea** per creare la nuova cartella.

>[!NOTE]
>
>Le cartelle sono inoltre soggette a [Convenzioni di denominazione delle pagine](#page-naming-conventions) quando si specifica il nome della nuova cartella.

>[!CAUTION]
>
>* Le cartelle possono essere create solo direttamente in **Sites** o in altre cartelle. Non possono essere create sotto una pagina.
>* Le azioni standard Sposta, Copia, Incolla, Elimina, Modifica, Pubblica, Annulla pubblicazione e Visualizza/Modifica proprietà possono essere eseguite in una cartella.
>* Le cartelle non sono disponibili per la selezione all’interno di una Live Copy.
