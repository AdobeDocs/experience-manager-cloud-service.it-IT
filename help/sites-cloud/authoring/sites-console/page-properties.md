---
title: Proprietà pagina
description: Scopri le diverse proprietà di una pagina, come controllano il comportamento della pagina e come viene gestita.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
mini-toc-levels: 2
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 33%

---


# Proprietà pagina {#page-properties}

Scopri le diverse proprietà di una pagina, come controllano il comportamento della pagina e come viene gestita.

>[!TIP]
>
>Per informazioni dettagliate su come modificare le proprietà di una pagina, vedere il documento [Modifica delle proprietà di una pagina.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)

## Panoramica e disponibilità delle proprietà {#overview}

Le proprietà di pagina possono controllare molti aspetti di una pagina dal titolo e dal branding della pagina alle relative autorizzazioni. Le proprietà sono distribuite in più schede, alcune delle quali possono essere nascoste a seconda del tipo di pagina. Come la maggior parte delle proprietà in AEM, [le proprietà di pagina possono essere ereditate.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#inheritance)

>[!NOTE]
>
>Questo documento descrive tutte le possibili proprietà di pagina. A seconda del tipo di pagina, non tutte le proprietà saranno disponibili.

## Scheda Base {#basic}

### Titolo e tag {#title-tags}

* **Titolo** - Definisce il metatitolo della pagina ai fini SEO e il titolo visualizzato nel contenuto della pagina (a meno che non venga sostituito)

   * Il titolo della pagina viene visualizzato in varie posizioni nell&#39;interfaccia utente di AEM, incluse le visualizzazioni a elenco/scheda di **Sites** nella console [Sites.](/help/sites-cloud/authoring/sites-console/introduction.md)
   * Questo campo è obbligatorio.

* **Tag** - Definisce i metatag della pagina a scopo SEO (Search Engine Optimization)

   * È possibile aggiungere o rimuovere tag dalla pagina aggiornando l&#39;elenco nella casella di selezione.
   * Utilizza il menu a discesa per selezionare tra i tag esistenti.
   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * Per aggiungere un tag completamente nuovo, digitane il nome in una casella di selezione vuota.

      * Il nuovo tag viene creato quando premi Invio.
      * Il nuovo tag viene quindi mostrato con un asterisco a destra che lo identifica come nuovo tag.

   * Quando passi il mouse su uno dei tag nella casella di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere quel tag per quella pagina.
   * Per ulteriori informazioni sui tag, vedere [Utilizzo del tag.](/help/sites-cloud/authoring/sites-console/tags.md)

* **Nascondi in navigazione** - Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito risultante

### Branding {#branding}

Applica un’identità del brand coerente tra le pagine aggiungendo un marchio a ciascun titolo della pagina. Questa funzionalità richiede l’utilizzo del Componente Pagina dalla versione 2.14.0 o successiva di [Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)

* **Brand Slug**

   * **Override**: selezionalo per definire il marchio su questa pagina.

      * Il valore viene ereditato da tutte le pagine secondarie a meno che non abbiano impostati anche i loro valori **Override**.

   * **Valore di override**: testo del marchio da aggiungere al titolo della pagina.

      * Il valore viene aggiunto al titolo della pagina dopo un carattere barra verticale come `Cycling Tuscany | Always ready for the WKND`

### ID HTML {#html-id}

* **ID**: ID HTML da applicare al componente.

### Altri titoli e descrizioni {#more-titles}

* **Titolo pagina** - Titolo da utilizzare nella pagina

   * Questa funzione viene in genere utilizzata dai componenti titolo.
   * Se vuoto, il **Titolo** è utilizzato.

* **Titolo navigazione** - È possibile specificare un titolo separato da utilizzare nella navigazione (ad esempio, se si desidera un titolo più conciso).

   * Se vuoto, viene utilizzato il **Titolo pagina**.

* **Sottotitolo** - Sottotitolo da utilizzare nella pagina
* **Descrizione** - Descrizione della pagina, il suo scopo o altri dettagli da aggiungere

### Ora di attivazione/disattivazione {#on-off-time}

L’ora di attivazione/disattivazione di una pagina è un modo comodo per nascondere temporaneamente il contenuto già pubblicato. Il contenuto rimane nell’istanza di pubblicazione quando è disattivato. La disattivazione di una pagina non annulla la pubblicazione del contenuto.

* **Ora di attivazione**: la data e l’ora in cui la pagina pubblicata viene resa visibile (renderizzata) nell’ambiente di pubblicazione. La pagina deve essere pubblicata, manualmente o tramite replica automatica preconfigurata.

   * Se [pubblicato,](/help/sites-cloud/authoring/sites-console/publishing-pages.md) questa pagina è già disponibile nell&#39;istanza di pubblicazione, ma è rimasta inattiva (nascosta) fino al rendering all&#39;ora specificata.
   * Se non è pubblicata e [configurata per la replica automatica,](/help/operations/replication.md#on-and-off-times-trigger-configuratio) la pagina viene pubblicata automaticamente e quindi sottoposta a rendering alla data e all&#39;ora specificate.
   * Se non è pubblicata e non è configurata per la replica automatica, la pagina non viene pubblicata automaticamente, quindi viene visualizzato un errore 404 quando si tenta di accedere alla pagina.

* **Ora di disattivazione**: simile e spesso utilizzata in combinazione con l’**Ora di attivazione**, definisce l’ora in cui la pagina pubblicata viene nascosta nell’ambiente di pubblicazione.

Lascia questi campi (**Ora di attivazione** e **Ora di disattivazione**) vuoti per le pagine da pubblicare e disponibili immediatamente e disponibili nell&#39;ambiente di pubblicazione fino a quando non vengono disattivate (lo scenario normale).

>[!NOTE]
>Se l’**Ora di attivazione** o l’**Ora di disattivazione** è nel passato e la replica automatica è configurata, l’azione pertinente verrà attivata immediatamente.

>[!TIP]
>
>I tempi di attivazione/disattivazione riguardano esclusivamente i contenuti già pubblicati (manualmente o tramite replica automatica). Per questo motivo, i flussi di lavoro di pubblicazione come quelli per l’approvazione del contenuto non vengono attivati da a orari di attivazione/disattivazione e da orari di attivazione/disattivazione non influiscono sullo stato di pubblicazione della pagina. Per questo motivo, i tempi di attivazione/disattivazione sono più appropriati per mostrare/nascondere temporaneamente il contenuto già approvato e pubblicato.
>
>Se desideri pubblicare nuovi contenuti con tutti i flussi di lavoro associati o rimuovere completamente (annullare la pubblicazione) dal sito, [gestisci la pubblicazione.](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)

### URL personalizzato {#vanity-url}

Questa proprietà consente di immettere un URL personalizzato per questa pagina, che può consentire di avere un URL più breve e/o più espressivo. Ad esempio, se l’URL personalizzato è impostato su `welcome` per la pagina identificata dal percorso `/v1.0/startpage` del sito web `http://example.com`, `http://example.com/welcome` sarà l’URL personalizzato di `http://example.com/content/v1.0/startpage`.

>[!CAUTION]
>
>Gli URL personalizzati:
>
>* Deve essere univoco.
>* non supportano le espressioni regolari;
>* non devono essere impostati su una pagina esistente.

* **Aggiungi** - Seleziona questa opzione per mostrare un campo e definire un URL personalizzato per la pagina.
   * Seleziona nuovamente per aggiungere più elementi.
   * Seleziona l&#39;icona **Rimuovi** per eliminare il Vanity URL.
* **Reindirizza Vanity URL** - Indica se la pagina deve utilizzare il Vanity URL o reindirizzare all&#39;URL effettivo della pagina

## Avanzate {#advanced}

### Impostazioni {#settings}

* **Lingua**: indica la lingua della pagina
* **Directory principale lingua**: questa opzione deve essere selezionata se la pagina corrisponde alla pagina principale di una copia per lingua
* **Reindirizza** - Indica la pagina a cui deve essere automaticamente reindirizzata la pagina con lo stato `302 Found` di HTML
   * **Reindirizzamento permanente**: se questa opzione è selezionata, la pagina viene reindirizzata al percorso di destinazione fornito, con uno stato HTML `301 Moved Permanently`.
* **Design**
* **Alias**: specifica un alias da utilizzare per la pagina
   * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
   * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
   * Le pagine accessibili da alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-cloud/authoring/sites-console/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.
   * Consulta [Nomi di pagina localizzati in Best practice per la gestione SEO e URL](/help/overview/seo-and-url-management.md#localized-page-names) per ulteriori informazioni.

### Configurazione {#configuration}

* **Ereditato da &lt;path>** - Abilita/disabilita l&#39;ereditarietà della **configurazione cloud** per la pagina
   * Attiva/disattiva la disponibilità della **configurazione cloud** per la modifica

* **Configurazione cloud**: il percorso per la configurazione selezionata

### Impostazioni modello {#template-settings}

* **Modelli permessi**: [definisce l’elenco di modelli che sono disponibili](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author) in questo ramo secondario
   * Ogni valore deve essere il percorso assoluto di un modello.
   * Utilizza `/.*` per consentire tutti i modelli presenti nel percorso.
* **Usa pagina come modello** - [Crea un nuovo modello basato sulla pagina corrente.](/help/sites-cloud/authoring/universal-editor/templates.md)
   * Applicabile solo alle pagine create per l’utilizzo con Universal Editor tramite Edge Delivery Services.

### Autenticazione richiesta {#authentication}

* **Abilita** - Abilita l&#39;utilizzo dell&#39;autenticazione per accedere alla pagina

>[!NOTE]
>
>Nella scheda **[Autorizzazioni](#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

* **Pagina di accesso**: indica la pagina da utilizzare per l’accesso

### Esporta {#export}

* **Configurazione di esportazione**: specifica una configurazione di esportazione

## SEO {#seo}

* **URL canonico** - Utilizzato per sovrascrivere l&#39;URL canonico della pagina
   * Se lasciato vuoto, l’URL della pagina corrisponde al suo URL canonico.

* **Tag robot** - Utilizzare il menu a discesa per selezionare i tag robot per controllare il comportamento dei crawler dei motori di ricerca
   * Alcune opzioni sono in conflitto tra loro, nel qual caso l’opzione più permissiva ha la precedenza.

* **Genera mappa del sito** - Se selezionata, viene generato un `sitemap.xml` per questa pagina e i relativi discendenti.

## Immagini {#images}

### Immagine in primo piano {#featured-image}

Questa sezione viene utilizzata per selezionare e configurare l’immagine da visualizzare. Viene utilizzata nei componenti che fanno riferimento alla pagina; ad esempio teaser, elenchi di pagine e così via.

* **Immagine** - È possibile **Selezionare** una risorsa o cercare un file da caricare, quindi **Modificare** o **Cancellare** l&#39;immagine selezionata.
* **Testo alternativo**: testo utilizzato per rappresentare il significato e/o la funzione dell&#39;immagine, comunemente utilizzato dagli assistenti vocali
* **Eredita - Valore tratto dalla risorsa DAM** - Se questa opzione è selezionata, nel testo alternativo viene inserito il valore dei metadati `dc:description` in DAM.

### Miniatura  {#thumbnail}

Questa sezione viene utilizzata per selezionare e configurare la miniatura dell’immagine per la pagina. Viene utilizzata nei componenti che fanno riferimento alla pagina; ad esempio teaser, elenchi di pagine e così via.

* **Genera anteprima**: genera un’anteprima della pagina da usare come miniatura
* **Carica immagine**: consente di caricare un’immagine da usare come miniatura
* **Seleziona immagine** - Seleziona una risorsa esistente da usare come miniatura
* **Annulla**: questa opzione diventa disponibile dopo aver apportato una modifica alla miniatura. Se non desideri mantenere la modifica, puoi annullarla prima di salvare.

## Servizi cloud {#cloud-services}

* **Configurazioni Cloud Service** - Definisce quale configurazione viene utilizzata per i servizi cloud per la pagina
* **Ereditato da** - Per le Live Copy e le copie per lingua, le configurazioni cloud vengono ereditate dalla blueprint per impostazione predefinita.
   * Deseleziona per ignorare l’ereditarietà

## Personalizzazione {#personalization}

### Configurazioni ContextHub {#contexthub-config}

* **Percorso ContextHub**: definizione della [Configurazione ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
* **Percorso segmenti**: definizione dell [Percorso dei segmenti](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

### Configurazione targeting {#targeting-config}

* **Marchio** - Definisce un [Marchio per specificare un ambito per il targeting](/help/sites-cloud/authoring/personalization/targeted-content.md)
   * Questa opzione richiede che l&#39;account utente appartenga al gruppo `Target Administrators`.

## Autorizzazioni {#permissions}

Utilizzare la scheda **Autorizzazioni** per definire quali utenti, gruppi o [gruppi di utenti chiusi (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=it) possono accedere alla pagina e/o modificarla.

* **Aggiungere autorizzazioni**
* **Modifica un gruppo utenti chiuso**
* Visualizza le **autorizzazioni effettive**

## Blueprint {#blueprint}

Questa scheda è visibile solo per le pagine che fungono da blueprint. Le blueprint fungono da base per le Live Copy e fanno parte della [Gestione multisito.](/help/sites-cloud/administering/msm/overview.md)

* **Rollout** - Avvia il rollout del contenuto blueprint nelle Live Copy
* **Panoramica Live Copy** - Apri una finestra per sfogliare la struttura della pagina Live Copy
* **Live Copy correnti** - Elenco di pagine basate sulla pagina blueprint selezionata (ovvero Live Copy di)

## Live Copy  {#live-copy}

Questa scheda è visibile solo per le pagine configurate come Live Copy. Come per [blueprint,](#blueprint) Live Copy fanno parte di [Gestione multisito.](/help/sites-cloud/administering/msm/overview.md)

* **Sincronizza** - Sincronizza Live Copy con blueprint, mantenendo le modifiche locali
* **Ripristina** - Ripristina Live Copy allo stato di blueprint, rimuovendo le modifiche locali
* **Sospendi**: sospendi la Live Copy da ulteriori modifiche di rollout
* **Stacca** - Stacca Live Copy dalla blueprint

### Origine {#source}

* Visualizza il percorso della blueprint per questa Live Copy

### Stato {#status}

* Elenca lo stato attuale della Live Copy della pagina

### Configurazione {#live-copy-config}

* **Ereditarietà Live Copy** - Se questa opzione è selezionata, la configurazione Live Copy ha effetto su tutti gli elementi figlio.
* **Eredita configurazioni di rollout dal padre** - Se selezionato, la configurazione di rollout viene ereditata dalla pagina padre.
* **Scegli configurazione di rollout**: definisce le circostanze in cui le modifiche vengono propagate dalla Blueprint e disponibili solo quando **Eredita configurazioni di rollout dall’elemento principale** non è selezionato
* **Elenco dei percorsi esclusi**

## Anteprima {#preview}

Quando un ambiente di anteprima [&#128279;](/help/sites-cloud/authoring/sites-console/previewing-content.md) è abilitato, sono disponibili i dettagli seguenti:

* **URL anteprima** - URL utilizzato per accedere al contenuto nell&#39;ambiente di anteprima

## App web progressiva {#progressive-web-app}

Tramite una configurazione semplice, un autore di contenuti può abilitare le funzioni dell’app web progressiva (PWA) per le esperienze create in AEM Sites. Il sito può quindi comportarsi come un’app nativa rendendola installabile nella schermata iniziale del dispositivo dei visitatori e disponibile offline.

{{pwa-deprecation}}

### Configura esperienza installabile {#config-pwa}

* **Abilita PWA** - Se abilitata, i visitatori della pagina possono installare il sito come PWA.
* **URL di avvio** - URL da caricare all&#39;avvio dell&#39;app Web da parte dell&#39;utente
   * Se l’URL è relativo, l’URL manifesto viene utilizzato come URL di base da risolvere
   * Se questo campo viene lasciato vuoto, viene utilizzato l’URL della pagina da cui è stata installata l’app.
   * È consigliabile impostare un valore.
* **Modalità di visualizzazione** - Il browser deve essere nascosto o altrimenti presentato all&#39;utente sul dispositivo locale
* **Orientamento schermo** - Gestione degli orientamenti del dispositivo da parte di PWA
* **Colore tema** - Il colore dell&#39;app che influisce sul modo in cui il sistema operativo dell&#39;utente locale visualizza la barra degli strumenti dell&#39;interfaccia utente nativa e i controlli di navigazione
* **Colore di sfondo** - Colore di sfondo dell&#39;app, visualizzato durante il caricamento dell&#39;app
* **Icona** - L&#39;icona che rappresenta l&#39;app sul dispositivo dell&#39;utente quando PWA è installato

### Gestione della cache (avanzata) {#cache-management}

* **Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti** - Definisce il modello di memorizzazione in cache per PWA.
* **File da memorizzare nella cache per uso offline**
   * **Pre-memorizzazione in cache dei file (anteprima tecnica)** - I file in hosting su AEM vengono salvati nella cache del browser locale quando il service worker si sta installando e prima di essere utilizzato.
   * **Librerie lato client** - Librerie lato client da memorizzare nella cache per l&#39;esperienza offline
   * **Inclusioni dei percorsi** - Le richieste di rete per i percorsi definiti vengono intercettate e il contenuto nella cache viene restituito in conformità alla configurazione della Strategia di memorizzazione in cache e frequenza di aggiornamento dei contenuti
   * **Esclusioni di percorso** - Questi file non verranno mai memorizzati nella cache indipendentemente dalle impostazioni in Pre-memorizzazione in cache dei file e Inclusioni dei percorsi.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Abilitazione delle funzionalità progressive dell&#39;app Web](/help/sites-cloud/authoring/sites-console/enable-pwa.md).

