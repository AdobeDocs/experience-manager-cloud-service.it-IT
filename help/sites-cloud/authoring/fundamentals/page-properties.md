---
title: Modifica delle proprietà di una pagina
description: Scopri come definire le proprietà necessarie per gestire una pagina in AEM.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 02ad83eb9fa9ed3bf06cf7fe0ef10fd9577f66a9
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 89%

---

# Modifica delle proprietà di una pagina {#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni della Live Copy vengono rese disponibili a seconda delle necessità.

## Proprietà pagina {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

* **Titolo &amp; tag**

   * **Titolo** - Il titolo della pagina viene visualizzato in varie posizioni. Ad esempio, l&#39;elenco di schede **Siti Web** e le visualizzazioni **Siti** per schede/elenchi.
      * Questo campo è obbligatorio.
   * **Tag**: qui puoi aggiungere o rimuovere i tag dalla pagina aggiornando l’elenco nella casella di selezione.
      * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
      * Per aggiungere un tag completamente nuovo, digitane il nome in una casella di selezione vuota.
         * Il nuovo tag viene creato quando premi Invio.
         * Il nuovo tag viene quindi mostrato con un asterisco a destra che lo identifica come nuovo tag.
      * Con l’elenco a discesa puoi selezionare uno dei tag esistenti.
      * Quando passi il mouse su uno dei tag nella casella di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere quel tag per quella pagina.
      * Per ulteriori informazioni sui tag, consulta [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md).
   * **Nascondi nella navigazione**: indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito risultante.

* **Marchio**

  Applica un’identità del brand coerente tra le pagine aggiungendo un marchio a ciascun titolo della pagina. Questa funzionalità richiede l’utilizzo del Componente Pagina dalla versione 2.14.0 o successiva di [Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)

   * **Brand Slug**

      * **Override**: selezionalo per definire il marchio su questa pagina.
         * Il valore viene ereditato da tutte le pagine secondarie a meno che non abbiano impostati anche i loro valori **Override**.
      * **Valore di override**: testo del marchio da aggiungere al titolo della pagina.
         * Il valore viene aggiunto al titolo della pagina dopo un carattere di barra come &quot;Cycling Tuscany | Always ready for the WKND&quot;

* **ID HTML**

   * **ID**: ID HTML da applicare al componente.

* **Altri titoli e descrizioni**

   * **Titolo pagina**: titolo da utilizzare nella pagina. Generalmente utilizzato dai componenti titolo. Se vuoto, il **Titolo** è utilizzato.
   * **Titolo navigazione** : puoi specificare un titolo diverso da usare nella navigazione (ad esempio, se ne desideri uno più conciso). Se vuoto, il **Titolo** è utilizzato.
   * **Didascalia**: sottotitolo da utilizzare nella pagina.
   * **Descrizione**: descrizione della pagina, il suo ruolo o altri dettagli.

* **Ora di attivazione/disattivazione**

  >[!NOTE]
  >
  > Vedi [Tempi di attivazione e disattivazione - Configurazione del trigger](/help/operations/replication.md#on-and-off-times-trigger-configuration) per informazioni dettagliate su come configurare la replica automatica correlata.

  >[!NOTE]
  >Se l’**Ora di attivazione** o l’**Ora di disattivazione** è nel passato e la replica automatica è configurata, l’azione pertinente verrà attivata immediatamente.

   * **Ora di attivazione**: la data e l’ora in cui la pagina pubblicata viene resa visibile (renderizzata) nell’ambiente di pubblicazione. La pagina deve essere pubblicata, manualmente o tramite replica automatica preconfigurata.

      * Se già [pubblicata (manualmente)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) questa pagina rimane inattiva (nascosta) fino al rendering alla data e all’ora specificate.
      * Se non è pubblicata, ma è configurata per la replica automatica, la pagina viene pubblicata automaticamente e quindi sottoposta a rendering al momento specificato.
      * Se non è pubblicata e non è configurata per la replica automatica, la pagina non viene pubblicata automaticamente, quindi viene visualizzato un errore 404 quando si tenta di accedere alla pagina.

   * **Ora di disattivazione**: simile e spesso utilizzata in combinazione con l’**Ora di attivazione**, definisce l’ora in cui la pagina pubblicata viene nascosta nell’ambiente di pubblicazione.

   * Lascia questi campi (**Ora di attivazione** e **Ora di disattivazione**) vuoti per le pagine da pubblicare immediatamente e disponibili nell’ambiente di pubblicazione fino a quando non vengono disattivate (lo scenario più consueto).

* **URL personalizzato**

   * Consente di immettere un URL personalizzato per questa pagina, che può consentire di avere un URL più breve e/o più espressivo.
   * Ad esempio, se l’URL personalizzato è impostato su `welcome` per la pagina identificata dal percorso `/v1.0/startpage` del sito web `http://example.com`, `http://example.com/welcome` sarà l’URL personalizzato di `http://example.com/content/v1.0/startpage`.

  >[!CAUTION]
  >
  >Gli URL personalizzati:
  >
  >* devono essere univoci, quindi accertati che il valore scelto non sia già utilizzato per un’altra pagina;
  >* non supportano le espressioni regolari;
  >* non devono essere impostati su una pagina esistente.

   * **Aggiungi** - Seleziona questa opzione per mostrare un campo e definire un URL personalizzato per la pagina.
      * Seleziona nuovamente per aggiungere più elementi.
      * Seleziona l&#39;icona **Rimuovi** per eliminare il Vanity URL.
   * **Reindirizza Vanity URL**: specifica se la pagina deve utilizzare il Vanity URL.

### Avanzate  {#advanced}

* **Impostazioni**

   * **Lingua**: indica la lingua della pagina
   * **Lingua root**: deve essere selezionato, se la pagina è la root di una copia in lingua
   * **Reindirizza** - Indica la pagina a cui deve essere automaticamente reindirizzata la pagina con lo stato HTML `302 Found`.
      * **Reindirizzamento permanente**: se questa opzione è selezionata, la pagina viene reindirizzata al percorso di destinazione fornito, con uno stato HTML `301 Moved Permanently`.
   * **Design**: indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito risultante
   * **Alias**: specifica un alias da utilizzare per la pagina
      * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
      * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
      * Le pagine accessibili da alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.
      * Consulta [Nomi di pagina localizzati in Best practice per la gestione SEO e URL](/help/overview/seo-and-url-management.md#localized-page-names).

* **Configurazione**

   * **Ereditata da &lt;path>**: abilitare/disabilitare l’ereditarietà; attivare/disattivare la disponibilità di **Configurazione cloud** con la selezione

   * **Configurazione cloud**: il percorso per la configurazione selezionata

* **Impostazioni modello**

   * **Modelli permessi**: [definisce l’elenco di modelli che sono disponibili](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) in questo ramo secondario

* **Autenticazione richiesta**

   * **Attiva**: attiva l’uso dell’autenticazione per accedere alla pagina

     >[!NOTE]
     >
     >Nella scheda **[Autorizzazioni](#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

   * **Pagina di accesso**: indica la pagina da utilizzare per l’accesso

* **Esporta**

   * **Configurazione di esportazione**: specifica una configurazione di esportazione

* **SEO**

   * **Url canonico**: può essere utilizzato per sovrascrivere l’URL canonico della pagina; se lasciato vuoto, l’URL della pagina è il relativo URL canonico

   * **Tag robot**: seleziona i tag robot per controllare il comportamento dei crawler dei motori di ricerca.

     >[!NOTE]
     >
     >Alcune delle opzioni sono in conflitto tra loro. In caso di conflitto, l’opzione più permissiva ha la precedenza.

   * **Genera mappa del sito**: se selezionata, per questa pagina viene generato un file sitemap.xml con i relativi discendenti

### Immagini {#images}

* **Immagine in primo piano**

  Seleziona e configura l’immagine da presentare. Viene utilizzato nei componenti che fanno riferimento alla pagina, ad esempio teaser, elenchi di pagine e così via.

   * **Immagine**

     Si può scegliere **Seleziona** una risorsa oppure cerca un file da caricare, quindi **Modifica** oppure **Cancella**.

   * **Testo alternativo**: un testo utilizzato per esprimere il significato e/o la funzione dell’immagine; ad esempio, per essere utilizzato dalle utilità per la lettura dello schermo.

   * **Eredita - Valore tratto dalla risorsa DAM**: se questa opzione è selezionata, il testo alternativo verrà compilato con il valore dei metadati`dc:description` in DAM

* **Miniatura**

  Configurare la miniatura della pagina

   * **Genera anteprima**: genera un’anteprima della pagina da usare come miniatura
   * **Carica immagine**: consente di caricare un’immagine da usare come miniatura
   * **Seleziona immagine**: seleziona una risorsa esistente da usare come miniatura
   * **Annulla**: questa opzione diventa disponibile dopo aver apportato una modifica alla miniatura. Se non desideri mantenere la modifica, puoi annullarla prima di salvare.

### Servizi cloud {#cloud-services}

* **Configurazioni Servizi cloud**: definizione delle proprietà per i servizi cloud

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

   * **Ereditato da &lt;path>**: abilita/disabilita l’ereditarietà; alternanza della disponibilità di **Percorso ContextHub** e **Percorso segmenti** per la selezione

   * **Percorso ContextHub**: definizione della [Configurazione ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Percorso segmenti**: definizione dell [Percorso dei segmenti](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Configurazione targeting**

   * **Marchio**: seleziona un [marchio per specificare l’ambito del targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).

  >[!NOTE]
  >Questa opzione richiede che l’account utente appartenga al gruppo `Target Administrators`.

### Autorizzazioni  {#permissions}

* **Autorizzazioni**

   * **Aggiungere autorizzazioni**
   * **Modifica un gruppo utenti chiuso**
   * Visualizza le **autorizzazioni effettive**

### Blueprint {#blueprint}

Questa scheda è visibile solo per le pagine che fungono da blueprint. Le blueprint fungono da base per le Live Copy e fanno parte della [Gestione multisito](/help/sites-cloud/administering/msm/overview.md).

* **Live Copy attuali**: elenca le pagine basate su (ovvero, Live Copy di) questa pagina blueprint

* **Configurazioni di Rollout**: controlla le circostanze in cui le modifiche vengono propagate alla Live Copy

### Live Copy  {#live-copy}

Questa scheda è visibile solo per le pagine configurate come Live Copy. Come per le blueprint, le Live Copy fanno parte della [Gestione multisito](/help/sites-cloud/administering/msm/overview.md).

* **Sincronizza**: sincronizza le Live Copy con blueprint, mantenendo le modifiche locali
* **Ripristina**: ripristina le Live Copy allo stato di blueprint, rimuovendo le modifiche locali
* **Sospendi**: sospendi la Live Copy da ulteriori modifiche di rollout
* **Scollega**: scollega le Live Copy da blueprint

* **Origine**

   * Visualizza il percorso della blueprint per questa Live Copy

* **Stato**

   * Elenca lo stato attuale della Live Copy della pagina

* **Configurazione**

   * **Ereditarietà della Live Copy**: se selezionato, la configurazione Live Copy ha effetto su tutti gli elementi figli
   * **Eredita configurazioni di rollout dal genitore**: se selezionato, la configurazione di rollout viene ereditata dalla pagina genitore
   * **Scegli configurazione di rollout**: definisce le circostanze in cui le modifiche vengono propagate dalla Blueprint e disponibili solo quando **Eredita configurazioni di rollout dall’elemento principale** non è selezionato

### Anteprima {#preview}

Quando un ambiente di anteprima è abilitato, vengono visualizzati i seguenti elementi:

* URL anteprima: URL utilizzato per accedere al contenuto nell’ambiente di anteprima

### App web progressiva {#progressive-web-app}

Grazie a una configurazione semplice, un autore di contenuti può ora abilitare le funzioni delle web app progressive (progressive web app, PWA) per le esperienze create in AEM Sites.

>[!NOTE]
>
>Consulta [Abilitazione delle funzionalità progressive delle app Web](/help/sites-cloud/authoring/features/enable-pwa.md).

* **Configura esperienza installabile**

   * **Abilita PWA**: abilita/disabilita la funzione; consente agli utenti di installare il sito come PWA
   * **URL di avvio**: URL di avvio preferito
   * **Modalità di visualizzazione**: definiscono come il browser deve essere nascosto o altrimenti presentato all’utente sul dispositivo locale
   * **Orientamento dello schermo**: come PWA gestirà gli orientamenti del dispositivo
   * **Colore tema**: il colore dell’app che influisce sul modo in cui il sistema operativo dell’utente locale visualizza la barra degli strumenti dell’interfaccia utente nativa e i controlli di navigazione
   * **Colore di sfondo**: il colore di sfondo dell’app, che viene visualizzato durante il caricamento dell’app
   * **Icona**: l’icona che rappresenta l’app sul dispositivo dell’utente

* **Gestione della cache (avanzata)**

   * **Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti**: definisce il modello di memorizzazione in cache per PWA
   * **File da memorizzare nella cache per uso offline**
      * **Pre-memorizzazione in cache dei file (anteprima tecnica)**: i file ospitati su AEM vengono salvati nella cache del browser locale quando il service worker si sta installando e prima di essere utilizzato
      * **Librerie lato client**: le librerie lato client per memorizzare in cache l’esperienza offline
      * **Inclusioni dei percorsi**: le richieste di rete per i percorsi definiti vengono intercettate e il contenuto memorizzato nella cache viene restituito in conformità alla configurazione della strategia di memorizzazione in cache e alla frequenza di aggiornamento dei contenuti
      * **Esclusioni di percorsi**: questi file non verranno mai memorizzati nella cache indipendentemente dalle impostazioni in Pre-memorizzazione in cache dei file e Inclusioni dei percorsi

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

* Dalla console **Sites**:
   * [Crea una nuova pagina](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (un sottoinsieme delle proprietà)
   * Tocca o fai clic su **Proprietà**
      * Per una singola pagina
      * Per più pagine (solo un sottoinsieme delle proprietà è disponibile per la modifica in blocco)
* Dall’editor di pagine:
   * Tramite **Informazioni pagina** (quindi **Apri proprietà**)

### Dalla console Sites - Pagina singola {#from-the-sites-console-single-page}

Tocca o fai clic su **Proprietà** per definire le proprietà di pagina:

1. Nella console **Sites** individua il punto della pagina di cui desideri visualizzare e modificare le proprietà.
1. Seleziona l’opzione **Proprietà** per la pagina desiderata, utilizzando:
   * [Azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * Le proprietà di pagina vengono visualizzate utilizzando le relative schede.
1. Visualizza o modifica le proprietà a seconda delle esigenze.
1. Quindi, seleziona **Salva** per salvare le modifiche e **Chiudi** per tornare alla console.

### Durante la modifica di una pagina {#when-editing-a-page}

Quando modifichi una pagina puoi utilizzare **Informazioni pagina** per definire le proprietà di pagina:

1. Apri la pagina di cui desideri modificare le proprietà.
1. Seleziona l’icona **Informazioni pagina** per aprire il menu di selezione.
1. Seleziona **Apri proprietà** e viene visualizzata una finestra di dialogo che consente di modificare le proprietà, ordinate in base alla scheda appropriata. A destra della barra degli strumenti sono disponibili anche i seguenti pulsanti:
   * **Annulla**
   * **Salva e chiudi**
1. Usa il pulsante **Salva e chiudi** per salvare le modifiche.

### Dalla console Sites - Pagine multiple {#from-the-sites-console-multiple-pages}

Dalla console **Sites** è possibile selezionare più pagine e quindi utilizzare **Visualizza proprietà** per visualizzare e/o modificare le proprietà della pagina. Questa operazione è definita modifica in serie delle proprietà di pagina.

Puoi selezionare più pagine per la modifica in serie utilizzando diversi metodi, tra i quali:

* Quando esplori la console **Sites**
* Dopo l’utilizzo di **Ricerca** per individuare un set di pagine

Dopo aver selezionato le pagine e aver toccato o fatto clic sull’opzione **Proprietà**, vengono visualizzate le proprietà per la modifica in serie:

![Modifica in serie delle proprietà di pagina](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Puoi eseguire la modifica in serie solo su pagine che:

* condividono lo stesso tipo di risorsa;
* non fanno parte di una Live Copy.
   * Se una delle pagine fa parte di una Live Copy, all’apertura delle proprietà viene visualizzato un messaggio di avviso.

Dopo aver attivato la funzione Modifica in serie, puoi effettuare le seguenti operazioni:

* **Visualizza**

   * Un elenco delle pagine interessate
      * Se necessario, puoi selezionare/deselezionare
      * Schede
         * Come per la visualizzazione delle proprietà di una singola pagina, le proprietà sono ordinate in schede.
   * Un sottoinsieme di proprietà
      * Puoi vedere le proprietà che sono disponibili su tutte le pagine selezionate e che sono state esplicitamente definite come disponibili per la modifica in serie.
      * Se la tua selezione include una sola pagina, tutte le proprietà sono visibili.
   * Proprietà condivise con un valore comune
      * Nella modalità Visualizza vengono mostrate solo le proprietà con un valore comune.
      * Se il campo ha più valori (ad esempio Tag), questi verranno visualizzati solo se *tutti* sono comuni. Se solo alcune sono comuni, verranno visualizzate solo durante la modifica.
      * Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

   * Puoi aggiornare i valori nei campi disponibili.
      * I nuovi valori vengono applicati a tutte le pagine selezionate quando selezioni **Fine**.
      * Quando il campo ha più valori (ad esempio Tag), puoi aggiungere un nuovo valore o rimuovere un valore comune.
   * I campi in comune ma con valori diversi nelle varie pagine sono contraddistinti da uno speciale valore, ad esempio il testo `<Mixed Entries>`.
