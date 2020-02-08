---
title: Modifica delle proprietà di una pagina
description: Puoi impostare le proprietà richieste per una pagina.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Modifica delle proprietà di una pagina {#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine possono essere connesse a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno disponibili ove appropriato.

## Proprietà pagina {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

* **Titolo**

   * Il titolo della pagina viene visualizzato in diversi punti. Ad esempio, nell’elenco della scheda **Siti web** e nelle viste a scheda o elenco di **Sites**.
   * Questo campo è obbligatorio.

* **Tag**

   * Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione.
   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. Per rimuovere un tag dall’elenco, utilizza l’icona x.
   * Per aggiungere un tag nuovo, digita il nome in una casella di selezione vuota.
      * Il nuovo tag viene creato quando premi Invio.
      * Un asterisco a destra del nome lo identifica come nuovo tag.
   * L’elenco a discesa consente di selezionare uno dei tag esistenti.
   * Quando sposti il mouse su un tag nella casella di selezione viene visualizzata una x, che consente di rimuovere il tag dalla pagina in questione.
   * Per ulteriori informazioni sui tag, consulta [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md).

* **Nascondi in navigazione**

   * Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito finale.

* **Titolo pagina**

   * Titolo da utilizzare nella pagina. Generalmente utilizzato dai componenti titolo. Se questo campo è vuoto, viene utilizzato il **Titolo**.

* **Titolo navigazione**

   * Puoi specificare un diverso titolo da usare per la navigazione (ad esempio un titolo più conciso). Se questo campo è vuoto, viene utilizzato il **Titolo**.

* **Sottotitolo**

   * Sottotitolo da utilizzare nella pagina.

* **Descrizione**

   * La descrizione della pagina, del suo ruolo o altri dettagli.

* **Ora di attivazione**

   * Data e ora in cui verrà attivata la pagina pubblicata. Dopo la pubblicazione, la pagina rimarrà inattiva fino alla data e all’ora specificate. 
   * Lascia vuoti questi campi per le pagine da pubblicare immediatamente (lo scenario più consueto).

* **Ora di disattivazione**

   * Data e ora in cui verrà disattivata la pagina pubblicata.
   * Lasciate vuoti questi campi per un’azione immediata.

* **URL personalizzato**

   * Consente di immettere un URL personalizzato per questa pagina, se desideri inserire un URL più breve e/o più significativo.
   * Ad esempio, se l’URL personalizzato è impostato `welcome` sulla pagina identificata dal percorso `/v1.0/startpage` del sito Web `http://example.com`, `http://example.com/welcome` sarà l’URL personalizzato di `http://example.com/content/v1.0/startpage`
   >[!CAUTION]
   >
   >Gli URL personalizzati:
   >
   >* devono essere univoci, quindi accertati che il valore scelto non sia già utilizzato per un’altra pagina;
   >* non supportano le espressioni regolari.
   >* Non deve essere impostato su una pagina esistente.


* **Reindirizza URL personalizzato**

   * Specifica se vuoi che la pagina usi l’URL personalizzato.

### Avanzate {#advanced}

* **Lingua**

   * Indica la lingua della pagina.

* **Directory principale lingua**

   * Deve essere selezionata, se la pagina è la pagina principale di una copia lingua.

* **Reindirizza**

   * Indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente.

* **Alias**

   * Specifica un alias da utilizzare per la pagina.
   >[!NOTE]
   >
   >Alias imposta la `sling:alias` proprietà per definire un nome alias per la risorsa (questo interessa solo la risorsa, non il percorso).
   >
   >Ad esempio: se si definisce un alias di `latin-lang` per il nodo `/content/we-retail/spanish` , è possibile accedere alla pagina tramite `/content/we-retail/latin-language`
   >
   >Per ulteriori dettagli, consultate Nomi delle pagine localizzate in SEO e Best practice per la gestione degli URL.
   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **Ereditato da &lt;*percorso*>**

   * Indica se la pagina viene ereditata e da dove.

* **Configurazione cloud**

   * Percorso della configurazione.

* **Modelli consentiti**

   * [Definisci l’elenco di modelli che saranno disponibili](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) in questo ramo secondario.

* **Attiva** (richiesta di autenticazione)

   * Attiva (o disattiva) l’uso dell’autenticazione per accedere alla pagina.
   >[!NOTE]
   >
   >Nella scheda **[Autorizzazioni](#permissions)**è possibile definire gruppi utenti chiusi per la pagina.

* **Pagina di accesso**

   * Indica la pagina da utilizzare per l’accesso.

* **Configurazione esportazione**

   * Consente di specificare una configurazione di esportazione.

### Miniatura {#thumbnail}

Mostra la miniatura della pagina. Tieni presente quanto segue:

* **Genera anteprima**

   * Genera un’anteprima della pagina da usare come miniatura.

* **Carica immagine**

   * Carica un’immagine da usare come miniatura.

* **Seleziona immagine**

   * Seleziona una risorsa esistente da usare come miniatura.

* **Versione precedente**

   * Questa opzione diventa disponibile dopo aver apportato una modifica alla miniatura. Se non desideri mantenere la modifica, puoi ripristinarla prima di salvare.

### Social media {#social-media}

* **Condivisione social media**

   Definisce le opzioni di condivisione disponibili sulla pagina. Rende disponibili le opzioni per la [Condivisione dei componenti di base](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/sharing.html).

   * **Abilita condivisione da parte degli utenti su Facebook**
   * **Abilita condivisione da parte degli utenti su Pinterest**
   * **Variante XF preferita**
      * Definizione della variante del frammento esperienza utilizzata per generare i metadati per la pagina

### Servizi cloud {#cloud-services}

* **Servizi cloud**

   * Consente di definire le proprietà per i servizi cloud. <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).-->

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

   * Seleziona la Configurazione ContextHub e il Percorso segmenti. <!--Select the [ContextHub Configuration](/help/sites-administering/contexthub-config.md) and [Segments Path](/help/sites-administering/segmentation.md).-->

* **Configurazione targeting**

   * Seleziona un [marchio per specificare l’ambito di impostazione della destinazione](/help/sites-cloud/authoring/personalization/targeted-content.md).

### Autorizzazioni {#permissions}

* **Autorizzazioni**

   * Aggiungere autorizzazioni <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->
   * Modificare un gruppo utenti chiuso <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->
   * Visualizzare le Autorizzazioni effettive <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

* **Blueprint**

   * Define properties for a Blueprint page within multi-site management. <!--Define properties for a Blueprint page within [multi-site management](/help/sites-administering/msm.md).-->
   * Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy {#live-copy}

* **Livecopy**

   * Define properties for a Live Copy page within multi-site management. <!--Define properties for a Live Copy page within [multi-site management](/help/sites-administering/msm.md).-->
   * Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito {#site-structure}

* Fornisce dei collegamenti verso pagine che offrono funzionalità a livello di sito, come **Pagina registrazione**, **Pagina offline** e altre.

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

* Dalla console **Sites**:
   * [Crea una nuova pagina](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (un sottoinsieme delle proprietà)
   * Clicking or tapping **Properties**
      * Per una singola pagina
      * Per più pagine (solo un sottoinsieme di proprietà è disponibile per la modifica in blocco)
* Dall’Editor di pagina:
   * Using **Page Information** (then **Open Properties**)

### Dalla console Sites - Pagina singola {#from-the-sites-console-single-page}

Tocca o fai clic su **Proprietà** per definire le proprietà di pagina:

1. Nella console **Siti**, individuate il percorso della pagina di cui desiderate visualizzare e modificare le proprietà.
1. Select the **Properties** option for the required page using either:
   * [Azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * Le proprietà di pagina vengono visualizzate utilizzando le relative schede.
1. Visualizza o modifica le proprietà a seconda delle tue esigenze.
1. Quindi, seleziona **Salva** per salvare le modifiche e **Chiudi** per tornare alla console.

### Durante la modifica di una pagina {#when-editing-a-page}

Quando modifichi una pagina puoi utilizzare **Informazioni di pagina** per definire le proprietà della pagina:

1. Aprite la pagina di cui desiderate modificare le proprietà.
1. Seleziona l’icona **Informazioni di pagina** per aprire il menu di selezione.
1. Select **Open Properties** and a dialog will open allowing you to edit the properties, sorted by the appropriate tab. I seguenti pulsanti sono disponibili anche a destra della barra degli strumenti:
   * **Annulla**
   * **Salva e chiudi**
1. Usa il pulsante **Salva e chiudi** per salvare le modifiche. 

### Dalla console Sites - Pagine multiple {#from-the-sites-console-multiple-pages}

Dalla console **Sites** è possibile selezionare più pagine e quindi utilizzare **Visualizza proprietà** per visualizzare e/o modificare le proprietà della pagina. Questa operazione è definita modifica collettiva delle proprietà di pagina.

>[!NOTE]
>
>La modifica collettiva delle proprietà è disponibile anche per le Risorse. È molto simile, ma differisce per alcuni aspetti. Per ulteriori informazioni, consulta Modificare le proprietà di risorse multiple.
>
>È disponibile anche lo strumento di Modifica collettiva, che consente di cercare contenuti da più pagine tramite GQL (Google Query Language), e quindi di modificare il contenuto direttamente sullo strumento prima di salvare le modifiche sulle pagine originate.
<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

Puoi selezionare più pagine per la modifica collettiva utilizzando diversi metodi, tra i quali:

* Utilizzare la console **Sites**.
* Dopo aver utilizzato **Cerca** per individuare un insieme di pagine.

After selecting the pages and then clicking or tapping the **Properties option**, the bulk properties will be shown:

![Modifica in blocco delle proprietà della pagina](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Puoi eseguire la modifica collettiva solo su pagine che:

* Condividono lo stesso tipo di risorsa;
* Non fanno parte di una live copy.
   * Se una delle pagine fa parte di una live copy, all’apertura delle proprietà viene visualizzato un messaggio di avviso.

Dopo aver attivato la funzione di modifica collettiva, puoi effettuare le seguenti operazioni:

* **Visualizzazione**

   * Un elenco delle pagine interessate.
      * Puoi selezionarle/deselezionarle se necessario.
      * Schede
         * Come per la visualizzazione delle proprietà di una pagina singola, le proprietà sono ordinate in schede.
   * Un sottoinsieme di proprietà.
      * Puoi vedere le proprietà che sono disponibili su tutte le pagine selezionate, e che sono state esplicitamente definite come disponibili per la modifica collettiva.
      * Se la tua selezione include una sola pagina, tutte le proprietà sono visibili.
   * Proprietà condivise con un valore comune
      * Solo le proprietà con un valore comune vengono mostrate nella modalità Visualizzazione.
      * Quando il campo ha valori multipli (ad esempio i Tag), questi vengono visualizzati solo se *tutti* i valori sono applicati alle pagine selezionate. Se le pagine hanno in comune solo alcuni valori, questi verranno visualizzati solo in fase di modifica.
      * Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

   * Puoi aggiornare i valori nei campi disponibili.
      * I nuovi valori saranno applicati a tutte le pagine selezionate quando fai clic su **Fine**.
      * Quando il campo ha valori multipli (ad esempio i Tag), puoi aggiungere un nuovo valore o rimuovere un valore comune.
   * Fields that are common, but have different values across the various pages will be indicated with a special value such as the text `<Mixed Entries>`. Presta attenzione quando modifichi tali campi per evitare una perdita di dati.

>[!NOTE]
>
>Il componente di pagina può essere configurato in modo da specificare i campi disponibili per la modifica collettiva. Consulta Configurazione della pagina per la modifica collettiva delle proprietà di pagina.
<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
