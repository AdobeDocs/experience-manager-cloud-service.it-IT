---
title: Modifica delle proprietà di una pagina
description: Puoi impostare le proprietà richieste per una pagina.
translation-type: tm+mt
source-git-commit: 5d72645aa3a5296e7b616101955734f03425ab59
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 99%

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

* **ID HTML**

   * ID HTML da applicare al componente.

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
   * Lascia questi campi vuoti per un’azione immediata.

* **URL personalizzato**

   * Consente di immettere un URL personalizzato per questa pagina, se desideri inserire un URL più breve e/o più significativo.
   * Ad esempio, se l’URL personalizzato è impostato su `welcome` per la pagina identificata dal percorso `/v1.0/startpage` del sito web `http://example.com`, `http://example.com/welcome` sarà l’URL personalizzato di `http://example.com/content/v1.0/startpage`.

   >[!CAUTION]
   >
   >Gli URL personalizzati:
   >
   >* devono essere univoci, quindi accertati che il valore scelto non sia già utilizzato per un’altra pagina;
   >* non supportano le espressioni regolari;
   >* non devono essere impostati su una pagina esistente.


* **Reindirizza URL personalizzato**

   * Specifica se vuoi che la pagina usi l’URL personalizzato.

### Avanzate  {#advanced}

* **Lingua**

   * Indica la lingua della pagina.

* **Directory principale lingua**

   * Deve essere selezionata, se la pagina è la pagina principale di una copia lingua.

* **Reindirizza**

   * Indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente.

* **Progettazione**

   * Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito finale.

* **Alias**

   * Specifica un alias da utilizzare per la pagina.
   >[!NOTE]
   >
   >L’alias consente di impostare la proprietà `sling:alias` per definire un nome di alias per la risorsa (influisce solo sulla risorsa, non sul percorso).
   >
   >Ad esempio, se definisci un alias di `latin-lang` per il nodo `/content/we-retail/spanish`, è possibile accedere a questa pagina tramite `/content/we-retail/latin-language`.
   >
   >Per maggiori dettagli, consulta la sezione sui nomi di pagina localizzati nelle best practice per la gestione di SEO e URL.

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

<!--
* **Inherited from &lt;*path*&gt;**

  * Indicates whether the page is inherited. and where from.
-->

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

### Miniatura  {#thumbnail}

Mostra la miniatura della pagina. Operazioni disponibili:

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
      * Consente di definire la variante del frammento esperienza utilizzato per generare i metadati della pagina.

### Cloud Services {#cloud-services}

* **Configurazioni Cloud Service**

   * Consente di definire le proprietà per Cloud Services.

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

   * Consente di selezionare la configurazione ContextHub e il percorso dei segmenti.

   <!--Select the [ContextHub Configuration](/help/sites-administering/contexthub-config.md) and [Segments Path](/help/sites-administering/segmentation.md).
  -->

* **Configurazione targeting**

   * Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Questa opzione richiede che l’account utente appartenga al gruppo `Target Adminstrators`.

### Autorizzazioni  {#permissions}

* **Autorizzazioni**

   * Aggiungere autorizzazioni
   * Modificare un gruppo utenti chiuso
   * Visualizzare le autorizzazioni effettive

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

* **Blueprint**

   * Consente di definire le proprietà per una pagina Blueprint nella gestione multisito.

   <!--Define properties for a Blueprint page within [multi-site management](/help/sites-administering/msm.md).-->

   * Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.


### Live Copy  {#live-copy}

* **Livecopy**

   * Consente di definire le proprietà per una pagina Live Copy nella gestione multisito. <!--Define properties for a Live Copy page within [multi-site management](/help/sites-administering/msm.md).-->
   * Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisce i collegamenti alle pagine che offrono funzionalità a livello di sito, tra cui **Pagina registrazione** e **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

* Dalla console **Sites**:
   * [Crea una nuova pagina](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (un sottoinsieme delle proprietà)
   * Tocca o fai clic su **Proprietà**
      * Per una singola pagina
      * Per più pagine (solo un sottoinsieme di proprietà è disponibile per la modifica in blocco)
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
1. Seleziona **Apri proprietà** per aprire una finestra di dialogo che consente di modificare le proprietà, organizzate nella scheda appropriata. A destra della barra degli strumenti sono disponibili anche i seguenti pulsanti:
   * **Annulla**
   * **Salva e chiudi**
1. Usa il pulsante **Salva e chiudi** per salvare le modifiche.

### Dalla console Sites - Pagine multiple {#from-the-sites-console-multiple-pages}

Dalla console **Sites** è possibile selezionare più pagine e quindi utilizzare **Visualizza proprietà** per visualizzare e/o modificare le proprietà della pagina. Questa operazione è definita modifica in serie delle proprietà di pagina.

>[!NOTE]
>
>La modifica in serie delle proprietà è disponibile anche per le risorse. È molto simile, ma differisce per alcuni aspetti. Per ulteriori informazioni, consulta Modifica delle proprietà di più risorse.
>
>È anche disponibile la funzione Modifiche in serie, che consente di cercare contenuti in più pagine tramite GQL (Google Query Language), e quindi di modificarli direttamente con Modifiche in serie prima di salvare le modifiche apportate alle pagine originarie.

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

Puoi selezionare più pagine per la modifica in serie utilizzando diversi metodi, tra i quali:

* Utilizzare la console **Sites**.
* Dopo aver utilizzato **Cerca** per individuare un insieme di pagine.

Dopo aver selezionato le pagine e aver toccato o fatto clic sull’opzione **Proprietà**, vengono visualizzate le proprietà per la modifica in serie:

![Modifica in serie delle proprietà di pagina](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Puoi eseguire la modifica in serie solo su pagine che:

* condividono lo stesso tipo di risorsa;
* non fanno parte di una Live Copy.
   * Se una delle pagine fa parte di una Live Copy, all’apertura delle proprietà viene visualizzato un messaggio di avviso.

Dopo aver attivato la funzione Modifica in serie, puoi effettuare le seguenti operazioni:

* **Visualizza**

   * Un elenco delle pagine interessate.
      * Puoi selezionarle/deselezionarle se necessario.
      * Schede
         * Come per la visualizzazione delle proprietà di una pagina singola, le proprietà sono ordinate in schede.
   * Un sottoinsieme di proprietà.
      * Puoi vedere le proprietà che sono disponibili su tutte le pagine selezionate e che sono state esplicitamente definite come disponibili per la modifica in serie.
      * Se la tua selezione include una sola pagina, tutte le proprietà sono visibili.
   * Proprietà condivise con un valore comune
      * Nella modalità Visualizza vengono mostrate solo le proprietà con un valore comune.
      * Quando il campo ha più valori (ad esempio Tag), questi vengono visualizzati solo se *tutti* i valori sono applicati alle pagine selezionate. Se le pagine hanno in comune solo alcuni valori, questi verranno visualizzati solo in fase di modifica.
      * Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

   * Puoi aggiornare i valori nei campi disponibili.
      * I nuovi valori saranno applicati a tutte le pagine selezionate quando fai clic su **Fine**.
      * Quando il campo ha valori multipli (ad esempio i Tag), puoi aggiungere un nuovo valore o rimuovere un valore comune.
   * I campi in comune ma con valori diversi nelle varie pagine saranno contraddistinti da uno speciale valore, ad esempio `<Mixed Entries>`. Presta attenzione quando modifichi tali campi per evitare perdite di dati.

>[!NOTE]
>
>Il componente di pagina può essere configurato in modo da specificare i campi disponibili per la modifica in serie. Consulta Configurazione della pagina per la modifica in serie delle proprietà di pagina.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
