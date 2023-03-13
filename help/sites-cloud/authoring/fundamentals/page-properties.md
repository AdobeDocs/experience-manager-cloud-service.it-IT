---
title: Modifica delle proprietà di una pagina
description: Puoi impostare le proprietà richieste per una pagina.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: d0a698a8f8685b1e5957a9d93d805ca3f825354a
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 100%

---

# Modifica delle proprietà di una pagina   {#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine possono essere connesse a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno disponibili ove appropriato.

## Proprietà pagina   {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

* **Titolo &amp; tag**

   * **Titolo**: il titolo della pagina viene visualizzato in diverse aree. Ad esempio, nell’elenco della scheda **Siti Web** e nelle viste a elenco/scheda di **Sites**.
      * Questo campo è obbligatorio.
   * **Tag** - Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione.
      * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. Per rimuovere un tag dall’elenco, utilizza l’icona x.
      * Per aggiungere un tag nuovo, digita il nome in una casella di selezione vuota.
         * Il nuovo tag viene creato quando premi Invio.
         * Un asterisco a destra del nome lo identifica come nuovo tag.
      * L’elenco a discesa consente di selezionare uno dei tag esistenti.
      * Quando sposti il mouse su un tag nella casella di selezione viene visualizzata una x, che consente di rimuovere il tag dalla pagina in questione.
      * Per ulteriori informazioni sui tag, consulta [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md).
   * **Nascondi in navigazione** - Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito finale.

* **Marchio**

   Applica un’identità del brand coerente tra le pagine aggiungendo un marchio a ciascun titolo della pagina. Questa funzionalità richiede l’utilizzo del Componente Pagina dalla versione 2.14.0 o successiva di [Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)

   * **Override**: selezionalo per definire il marchio su questa pagina.
      * Il valore viene ereditato da tutte le pagine figlie a meno che non abbiano impostati anche i loro valori **Override**.
   * **Valore di override**: testo del marchio da aggiungere al titolo della pagina.
      * Il valore viene aggiunto al titolo della pagina dopo un carattere di barra come &quot;Cycling Tuscany | Always ready for the WKND&quot;

* **ID HTML**

   * **ID**: ID HTML da applicare al componente.

* **Altri titoli e descrizioni**

   * **Titolo pagina**: titolo da utilizzare nella pagina. Generalmente utilizzato dai componenti titolo. Se questo campo è vuoto, viene utilizzato il **Titolo**.
   * **Titolo navigazione**: puoi specificare un diverso titolo da usare per la navigazione (ad esempio un titolo più conciso). Se questo campo viene lasciato vuoto, verrà utilizzato il **Titolo**.
   * **Sottotitolo**: sottotitolo da utilizzare nella pagina.
   * **Descrizione**: descrizione della pagina, il suo ruolo o altri dettagli.

* **Ora di attivazione/disattivazione**

   >[!NOTE]
   >
   > Vedi [Tempi di attivazione e disattivazione - Configurazione del trigger](/help/operations/replication.md#on-and-off-times-trigger-configuration) per informazioni dettagliate su come configurare la replica automatica correlata.

   >[!NOTE]
   >Se l&#39;**Ora di attivazione** o l&#39;**Ora di disattivazione** è nel passato e la replica automatica è configurata, l&#39;azione pertinente verrà attivata immediatamente.

   * **Ora di attivazione**: la data e l’ora in cui la pagina pubblicata verrà resa visibile (renderizzata) nell’ambiente di pubblicazione. La pagina deve essere pubblicata, manualmente o tramite replica automatica preconfigurata.

      * Se già [pubblicata (manualmente)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) questa pagina rimarrà inattiva (nascosta) fino al rendering alla data e all’ora specificate.
      * Se non è pubblicata, ma è configurata per la replica automatica, la pagina verrà pubblicata automaticamente e quindi sottoposta a rendering al momento specificato.
      * Se non è pubblicata e non è configurata per la replica automatica, la pagina non verrà pubblicata automaticamente, quindi viene visualizzato un errore 404 quando si tenta di accedere alla pagina.
   * **Ora di disattivazione**: simile e spesso utilizzata in combinazione con l&#39;**Ora di attivazione**, definisce l’ora in cui la pagina pubblicata verrà nascosta nell’ambiente di pubblicazione.

   * Lascia questi campi (**Ora di attivazione** e **Ora di disattivazione**) vuoti per le pagine da pubblicare immediatamente e disponibili nell’ambiente di pubblicazione fino a quando non vengono disattivate (lo scenario più consueto).


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


   * **Aggiungi**: tocca o fai clic per visualizzare un campo e definire un URL personalizzato per la pagina.
      * Tocca o fai di nuovo clic per aggiungere più elementi.
      * Tocca o fai clic sull&#39;icona **Rimuovi** per eliminare il Vanity URL.
   * **Reindirizza Vanity URL**: specifica se la pagina deve utilizzare il Vanity URL.


### Avanzate  {#advanced}

* **Impostazioni**

   * **Lingua**: indica la lingua della pagina
   * **Lingua root**: deve essere selezionato, se la pagina è la root di una copia in lingua
   * **Reindirizza**: indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente con uno stato HTML `302 Found`.
      * **Reindirizzamento permanente**: se questa opzione è selezionata, la pagina viene reindirizzata al percorso di destinazione fornito, con uno stato HTML `301 Moved Permanently`.
   * **Design**: indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito risultante
   * **Alias**: specifica un alias da utilizzare per la pagina
      * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
      * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
      * Le pagine a cui si accede tramite alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **Configurazione**

   * **Configurazione cloud**: il percorso della configurazione

* **Impostazioni modello**

   * **Modelli permessi**: [definisce l’elenco di modelli che saranno disponibili](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) in questo ramo secondario

* **Autenticazione richiesta**

   * **Attiva**: attiva l’uso dell’autenticazione per accedere alla pagina

      >[!NOTE]
      >
      >Nella scheda **[Autorizzazioni](#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

   * **Pagina di accesso**: indica la pagina da utilizzare per l’accesso

* **Esporta**

   * **Configurazione di esportazione**: specifica una configurazione di esportazione

### Miniatura  {#thumbnail}

Configurare la miniatura della pagina

* **Genera anteprima**: genera un’anteprima della pagina da usare come miniatura
* **Carica immagine**: consente di caricare un’immagine da usare come miniatura
* **Seleziona immagine**: seleziona una risorsa esistente da usare come miniatura
* **Annulla**: questa opzione diventa disponibile dopo aver apportato una modifica alla miniatura. Se non desideri mantenere la modifica, puoi ripristinarla prima di salvare.

### Social media {#social-media}

* **Condivisione social media**

   Definisce le opzioni di condivisione disponibili sulla pagina. Rende disponibili le opzioni per la [Condivisione dei componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html?lang=it).

   * **Abilita condivisione da parte degli utenti su Facebook**
   * **Abilita condivisione da parte degli utenti su Pinterest**
   * **Variante XF preferita**
      * Consente di definire la variante del frammento esperienza utilizzato per generare i metadati della pagina.

### Servizi cloud {#cloud-services}

* **Configurazioni Servizi cloud**: definizione delle proprietà per i servizi cloud

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

   * **Percorso ContextHub**: definizione della [Configurazione ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Percorso segmenti**: definizione dell [Percorso dei segmenti](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Configurazione targeting**

   * **Marchio**: seleziona un [marchio per specificare l’ambito del targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Questa opzione richiede che l’account utente appartenga al gruppo `Target Administrators`.

### Autorizzazioni  {#permissions}

* **Autorizzazioni**

   * Aggiungere autorizzazioni
   * Modificare un gruppo utenti chiuso
   * Visualizzare le autorizzazioni effettive

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

Questa scheda è visibile solo per le pagine che fungono da blueprint. Le blueprint fungono da base per le Live Copy e fanno parte della [Gestione multisito.](/help/sites-cloud/administering/msm/overview.md)

* **Live Copy attuali**: elenca le pagine basate su (ad esempio, Live Copy di) questa pagina blueprint

* **Configurazioni di Rollout**: controlla le circostanze in cui le modifiche verranno propagate alla Live Copy

### Live Copy  {#live-copy}

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
   * **Scegli configurazione di rollout**: definisce le circostanze in cui le modifiche verranno propagate dalla Blueprint e disponibili solo quando **Eredita configurazioni di rollout dal genitore** non è selezionato

### Anteprima {#preview}

Quando un ambiente di anteprima è abilitato, vengono visualizzati i seguenti elementi:

* URL anteprima: URL utilizzato per accedere al contenuto nell’ambiente di anteprima

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
   * I campi in comune ma con valori diversi nelle varie pagine saranno contraddistinti da uno speciale valore, ad esempio `<Mixed Entries>`.

>[!NOTE]
>
>Il componente di pagina può essere configurato in modo da specificare i campi disponibili per la modifica in serie. Consulta Configurazione della pagina per la modifica in serie delle proprietà di pagina.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
