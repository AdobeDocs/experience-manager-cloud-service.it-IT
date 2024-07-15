---
title: Generare varianti
description: Scopri come generare varianti, accessibile da AEM as a Cloud Service e dal Sidekick di Edge Delivery Services
exl-id: 9114037f-37b9-4b2f-a714-10933f69b2c3
feature: Generate Variations
role: Admin, Architect, Developer
source-git-commit: bbc51796c610af02b5260c063213cde2ef610ba2
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 1%

---


# Generare varianti {#generate-variations}

Se stai cercando un modo per ottimizzare i canali digitali e accelerare la creazione di contenuti, puoi utilizzare Genera varianti. Genera varianti utilizza l’intelligenza artificiale generativa (AI) per creare varianti di contenuto in base alle richieste; queste richieste vengono fornite da Adobe oppure create e gestite dagli utenti. Dopo aver creato le varianti, puoi utilizzare il contenuto del tuo sito Web e misurarne il successo utilizzando la funzionalità [Sperimentazione](https://www.aem.live/docs/experimentation) di [Edge Delivery Services](/help/edge/overview.md).

Puoi [accedere a Genera varianti](#access-generate-variations) da:

* [in Adobe Experience Manager (AEM) as a Cloud Service](#access-aemaacs)
* [il Sidekick dei Edge Delivery Services AEM](#access-aem-sidekick)
* [nell’Editor frammenti di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai)

>[!NOTE]
>
>In tutti i casi, per utilizzare Genera varianti è necessario assicurarsi che siano soddisfatti i [prerequisiti di accesso](#access-prerequisites).

Puoi effettuare le seguenti operazioni:

* [Inizia](#get-started) utilizzando un modello di richiesta creato da Adobe per un caso d&#39;uso specifico.
* È possibile [modificare un prompt esistente](#edit-the-prompt)
* Oppure [crea e utilizza le tue richieste](#create-prompt):
   * [Salva le richieste](#save-prompt) per utilizzi futuri
   * [Accedi e utilizza i prompt condivisi](#select-prompt) dall&#39;intera organizzazione
* Definisci i segmenti di [pubblico](#audiences) da utilizzare nel prompt durante la [generazione di contenuto personalizzato specifico per il pubblico](#generate-copy).
* Visualizza l’anteprima dell’output accanto al prompt, prima di apportare modifiche e di perfezionare i risultati, se necessario.
* Utilizza [Adobe Express per generare immagini](#generate-image) in base alle varianti di copia; in questo modo vengono utilizzate le funzionalità di intelligenza artificiale generativa di Firefly.
* Seleziona il contenuto da utilizzare sul tuo sito web o in un esperimento.

## Note legali e di utilizzo {#legal-usage-note}

Generative AI e Generate Variations for AEM sono strumenti potenti, ma **tu** è responsabile dell&#39;utilizzo dell&#39;output.

I dati immessi nel servizio devono essere legati a un contesto. Questo contesto può essere costituito dai materiali di branding, dal contenuto del sito Web, dai dati, dagli schemi per tali dati, dai modelli o da altri documenti attendibili.

Devi valutare l’accuratezza di qualsiasi output in base al tuo caso d’uso.

Prima di utilizzare Genera varianti è necessario accettare le [Linee guida per utenti di IA generativa di Adobe](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

[L&#39;utilizzo di Generate Variations](#generative-action-usage) è legato al consumo di azioni generative.

## Panoramica {#overview}

Quando apri Genera varianti (ed espandi il pannello a sinistra) viene visualizzato:

![Genera varianti - pannello principale](assets/generate-variations-main-panel.png)

* Pannello a destra
   * Dipende dalla selezione effettuata nel menu di navigazione a sinistra.
   * Per impostazione predefinita, vengono visualizzati **Modelli di richiesta**.
* Navigazione a sinistra
   * A sinistra di **Genera varianti**, è presente l&#39;opzione (menu sandwich) per espandere o nascondere il pannello di navigazione sinistro.
   * **Modelli di richiesta**:
      * Mostra collegamenti ai vari prompt, che possono includere i prompt:
         * Fornito dall’Adobe per aiutarti a generare il contenuto; contrassegnato con l’icona dell’Adobe.
         * Creato da te stesso.
         * Creato nell’organizzazione IMS; contrassegnato con un’icona che mostra più teste.
      * Include il collegamento [Nuovo prompt](#create-prompt) per la creazione di un prompt personalizzato.
      * Puoi **Eliminare** prompt creati da te stesso o dall&#39;organizzazione IMS. Questa operazione viene eseguita utilizzando il menu a cui si accede con l’ellisse sulla scheda appropriata.
   * [Preferiti](#favorites): mostra i risultati delle generazioni precedenti contrassegnati come Preferiti.
   * [Recenti](#recents): fornisce collegamenti ai prompt e ai relativi input utilizzati di recente.
   * **Guida e domande frequenti**: collegamenti alla documentazione, incluse le domande frequenti.
   * **Linee guida per gli utenti**: collegamenti alle linee guida legali.

## Introduzione {#get-started}

L’interfaccia ti guida attraverso il processo di generazione dei contenuti. Dopo aver aperto l’interfaccia, il primo passaggio consiste nella selezione del prompt da utilizzare.

### Seleziona richiesta {#select-prompt}

Dal pannello principale, puoi selezionare:

* un modello di richiesta fornito da Adobe per iniziare a generare contenuti,
* [Nuovo prompt](#create-prompt) per creare un prompt personalizzato,
* un modello creato esclusivamente per l&#39;uso personale,
* un modello creato da te o da un utente dell’organizzazione.

Per differenziare:

* I prompt forniti dall&#39;Adobe sono contrassegnati con l&#39;icona Adobe
* Le richieste disponibili in tutta l’organizzazione IMS sono contrassegnate da un’icona a più testine.
* I prompt privati non sono contrassegnati in modo specifico.

![Genera varianti - Modelli di richiesta](assets/generate-variations-prompt-templates.png)

### Fornisci input {#provide-inputs}

Ogni prompt richiede di fornire determinate informazioni in modo che sia in grado di recuperare il contenuto appropriato dall’intelligenza artificiale generativa.

I campi di input ti guidano attraverso le informazioni necessarie. Per facilitare questa fase, alcuni campi dispongono di valori predefiniti che è possibile utilizzare o modificare in base alle esigenze e descrizioni che spiegano i requisiti.

Esistono diversi campi di input chiave comuni a più prompt (alcuni campi non sono sempre disponibili):

* **Conteggio di**/**Numero di**
   * Puoi selezionare quante varianti di contenuto desideri creare in una generazione.
   * A seconda del prompt, potrebbe essere presente una delle varie etichette, ad esempio Conteggio, Numero di varianti, Numero di idee e altre.
* **Pubblico Source**/**Pubblico Target**
   * Consente di generare contenuti personalizzati per un pubblico specifico.
   * Adobe fornisce tipi di pubblico predefiniti oppure è possibile specificare tipi di pubblico aggiuntivi. Vedere [Tipi di pubblico](#audiences).
* **Contesto aggiuntivo**
   * Inserisci contenuti pertinenti per consentire a Generative AI di creare una risposta migliore in base all’input. Ad esempio, se stai creando un banner web per una pagina o un prodotto particolare, potresti voler includere informazioni sulla pagina o sul prodotto.
* **Temperatura**
Utilizza per modificare la temperatura di Adobe Generative AI:
   * Una temperatura più alta si allontana dal prompt e porta a una maggiore variabilità, casualità e creatività.
   * Una temperatura più bassa è più deterministica e rimane più vicina a ciò che è nel prompt.
   * Per impostazione predefinita, la temperatura è impostata su 1. Puoi sperimentare con temperature diverse se i risultati generati non sono di tuo gradimento.
* **Modifica richiesta**
   * Il [prompt sottostante può essere modificato](#edit-the-prompt) per perfezionare i risultati generati.

### Genera copia {#generate-copy}

Dopo aver compilato i campi di input e/o modificato il prompt, è possibile generare il contenuto e rivedere le risposte.

Seleziona **Genera** per visualizzare le risposte generate da IA generativa. Le varianti di contenuto generate vengono visualizzate sotto il prompt che le ha generate.

![Genera varianti - genera copia](assets/generate-variations-generate-content.png)

>[!NOTE]
>
>La maggior parte dei modelli di prompt di Adobe include una **Motivazione IA** nella risposta della variante. Questo fornisce trasparenza sul motivo per cui l’intelligenza artificiale generativa ha generato quella particolare variante.

Quando selezioni una singola variante, sono disponibili le seguenti azioni:

* **Preferito**
   * Contrassegna come **Preferito** per utilizzi futuri (verrà visualizzato in [Preferiti](#favorites)).
* Miniature in alto/Miniature in basso
   * Utilizza gli indicatori thumbs up / down per notificare all’Adobe la qualità delle risposte.
* **Copia**
   * Copia negli Appunti da utilizzare per l&#39;authoring dei contenuti sul sito Web o in un [esperimento](https://www.aem.live/docs/experimentation).
* **Rimuovi**

Se devi perfezionare gli input o i prompt, puoi apportare le modifiche necessarie e selezionare di nuovo **Genera** per ottenere un set di nuove risposte. Il nuovo prompt e la nuova risposta vengono visualizzati sotto il prompt e la risposta iniziali; è possibile scorrere verso l&#39;alto e verso il basso per visualizzare i vari set di contenuti.

Sopra ogni set di varianti viene visualizzato il messaggio di richiesta con l&#39;opzione **Riutilizza**. Se devi eseguire nuovamente un prompt con i relativi input, seleziona **Riutilizza** per ricaricarli in **Input**.

### Genera immagine {#generate-image}

Dopo aver generato varianti di testo, puoi generare immagini in Adobe Express utilizzando le funzionalità di intelligenza artificiale generativa di Firefly.

>[!NOTE]
>
>**Genera immagine** è disponibile solo se disponi di un diritto di Adobe Express come parte dell&#39;organizzazione IMS e di accesso concesso nell&#39;Admin Console.

Seleziona una variante, seguita da **Genera immagine**, per aprire direttamente **Testo nell&#39;immagine** in [Adobe Express](https://www.adobe.com/express/). Il prompt viene precompilato in base alla selezione della variante e le immagini vengono generate automaticamente in base a tale prompt.

![Genera varianti - immagini esplicite](assets/generate-variations-express-images.png)

Puoi apportare ulteriori modifiche:

* [scrivi il tuo prompt nell&#39;Adobe Express](https://helpx.adobe.com/firefly/using/tips-and-tricks.html) descrivendo ciò che desideri visualizzare,
* modifica le opzioni **Testo in immagine**,
* quindi **Aggiorna** le immagini generate.

Puoi anche utilizzare **Esplora altro** per ulteriori possibilità.

Al termine, seleziona l&#39;immagine desiderata e **Salva** per chiudere l&#39;Adobe Express. L’immagine viene restituita e salvata con la variante.

![Genera varianti - immagine express salvata](assets/generate-variations-express-image-saved.png)

Qui puoi passare il mouse sull&#39;immagine per visualizzare le azioni relative a:

* **Copia**: [copia l&#39;immagine negli Appunti per utilizzarla altrove](#use-content)
* **Modifica**: apri l&#39;Adobe Express per apportare modifiche all&#39;immagine
* **Scarica**: scarica l&#39;immagine nel computer locale
* **Elimina**: rimuovi l&#39;immagine dalla variante

>[!NOTE]
>
>[I Content credentials](https://helpx.adobe.com/creative-cloud/help/content-credentials.html) non vengono mantenuti se utilizzati nell&#39;authoring basato su documenti.

### Usa contenuto {#use-content}

Per utilizzare il contenuto generato con IA generativa, devi copiarlo negli Appunti per utilizzarlo altrove.

Questa operazione viene eseguita utilizzando le icone di copia:

* Per il testo: utilizza l’icona Copia, visibile nel pannello delle varianti
* Per l’immagine: passa il puntatore del mouse sull’immagine per visualizzare l’icona Copia

Una volta copiati negli Appunti, puoi incollare le informazioni da utilizzare per l’authoring dei contenuti del sito web. Puoi anche eseguire un [esperimento](https://www.aem.live/docs/experimentation).

## Preferiti {#favorites}

Dopo aver esaminato il contenuto, puoi salvare le varianti selezionate come preferite.

Una volta salvati, vengono visualizzati in **Preferiti** nella barra di navigazione a sinistra. I preferiti sono persistenti (fino a **Eliminarli** o cancellare la cache del browser).

* I preferiti e le varianti possono essere copiati/incollati negli Appunti per essere utilizzati nel contenuto del sito web.
* I Preferiti possono essere **Rimossi**.

## Recenti {#recents}

Questa sezione fornisce collegamenti alle attività recenti. È stata aggiunta una voce **Recent** dopo aver selezionato **Generate**. Ha il nome del prompt e una marca temporale. Se selezioni un collegamento, questo carica il prompt, compila i campi di input in modo appropriato e mostra le varianti generate.

## Modifica la richiesta {#edit-the-prompt}

È possibile modificare il prompt sottostante. Puoi eseguire questa operazione:

* Se i risultati generati che stai ottenendo hanno bisogno di ulteriori perfezionamenti
* Desideri modificare e [salvare il prompt](#save-prompt) per utilizzi futuri

Seleziona **Modifica richiesta**:

![Genera varianti - prompt di modifica](assets/generate-variations-prompt-edit.png)

Verrà aperto l’editor dei prompt, in cui è possibile apportare le modifiche:

![Genera varianti - editor prompt](assets/generate-variations-prompt-editor.png)

### Aggiungi input prompt {#add-prompt-inputs}

Quando crei o modifichi un prompt, potrebbe essere necessario aggiungere campi di input. I campi di input fungono da variabili nel prompt e offrono la flessibilità di utilizzare lo stesso prompt in vari scenari. Consentono agli utenti di definire elementi specifici del prompt, senza dover scrivere l’intero prompt.

* Un campo è definito con parentesi graffe doppie `{{ }}` che racchiudono un nome segnaposto.
Esempio: `{{tone_of_voice}}`.

  >[!NOTE]
  >
  >Non sono consentiti spazi tra le doppie parentesi graffe.

* È definito anche in `METADATA`, con i seguenti parametri:
   * `label`
   * `description`
   * `default`
   * `type`

#### Esempio: Aggiungi nuovo campo di testo - Tono della voce {#example-add-new-text-field-tone-of-voice}

Per aggiungere un nuovo campo di testo con titolo **Tono di voce**, utilizzare la sintassi seguente nel prompt:

```prompt
{{@tone_of_voice, 
  label="Tone of voice",
  description="Indicate the desired tone of voice",
  default="optimistic, smart, engaging, human, and creative",
  type=text
}}
```

![Genera varianti - richiesta modificata con tono di voce](assets/generate-variations-prompt-edited.png)

<!--
#### Example: Add new dropdown field - Page Type {#example-add-new-dropdown-field-page-type}

To create an input field Page Type providing a dropdown selection:

1. Create a spreadsheet named `pagetype.xls` in the top-level directory of your folder structure.
1. Edit the spreadsheet:

   1. Create two columns: **Key** and **Value**.
   1. In the **Key** column, enter labels that will appear in the dropdown.
   1. In the **Value** column, describe the key value so the generative AI has context.

1. In your prompt, refer to the title of the spreadsheet along with the appropriate type. 

   ```prompt
   {{@page_type, 
     label="Page Type",
     description="Describes the type of page",
     spreadsheet=pagetype
   }}
   ```
-->

## Crea un prompt {#create-prompt}

Quando selezioni **Nuovo prompt** da **Modelli di prompt**, un nuovo pannello ti consentirà di inserire un nuovo prompt. È quindi possibile specificare questi elementi, insieme alla **Temperatura**, per **Generare** contenuto.

Per ulteriori informazioni su come salvare la richiesta in futuro, vedere [Salva richiesta](#save-prompt).

Per informazioni dettagliate sull&#39;aggiunta di input di prompt personalizzati, vedere [Aggiungi input di prompt](#add-prompt-inputs).

Se desideri mantenere la formattazione sia nell’interfaccia utente che quando viene copiata e incollata nel flusso di authoring basato su documenti, includi quanto segue nel prompt:

<!-- CHECK - are the double-quotes needed? -->

* `"Format the response as an array of valid, iterable RFC8259 compliant JSON"`

L’immagine seguente mostra i vantaggi di questa operazione:

* nel primo esempio `Title` e `Description` sono combinati
* mentre nel secondo esempio vengono formattati separatamente: questo è stato fatto includendo la richiesta JSON nel prompt.

![Genera varianti - richiesta con titolo e descrizione formattati separatamente](assets/generate-variations-prompt-formatted.png)

## Salva il prompt {#save-prompt}

Dopo aver modificato o creato i prompt, puoi salvarli per utilizzarli in futuro, sia per la tua organizzazione IMS che per te stesso. La richiesta salvata verrà visualizzata come scheda **Modello di richiesta**.

Dopo aver modificato il prompt, l&#39;opzione **Salva** è disponibile nella parte inferiore della sezione Input, a sinistra di **Genera**.

Se questa opzione è selezionata, viene visualizzata la finestra di dialogo **Richiesta salvataggio**:

![Genera varianti - finestra di dialogo per richiesta di salvataggio](assets/generate-variations-prompt-save-dialog.png)

1. Aggiungi un **Nome prompt** univoco; utilizzato per identificare il prompt all&#39;interno di **Modelli prompt**.
   1. Un nuovo nome univoco crea un nuovo modello di prompt.
   1. Un nome esistente sovrascrive tale richiesta; viene visualizzato un messaggio.
1. Facoltativamente, aggiungi una descrizione.
1. Attiva o disattiva l&#39;opzione **Condivisa tra organizzazioni**, a seconda che il prompt sia privato o disponibile nell&#39;organizzazione IMS. Questo stato viene visualizzato nella [scheda risultante mostrata nei Modelli di richiesta](#select-prompt).
1. **Salva** la richiesta oppure **Annulla** l&#39;azione.

>[!NOTE]
>
>Viene visualizzato un avviso se si sta sovrascrivendo o aggiornando un prompt esistente.

>[!NOTE]
>
>Dai **Modelli di richiesta** puoi eliminare i prompt (utilizzando il menu a cui si accede con l&#39;ellisse) creati da te stesso o nell&#39;organizzazione IMS.

## Pubblico {#audiences}

Per generare contenuti personalizzati, l’intelligenza artificiale generativa deve comprendere il pubblico. In Adobe sono disponibili diversi tipi di pubblico predefiniti, oppure puoi aggiungerne altri.

Quando aggiungi un pubblico, descrivilo nel linguaggio naturale. Ad esempio:

* per creare un pubblico:
   * `Student`
* potresti dire:
   * `The audience consists of students, typically individuals who are pursuing education at various academic levels, such as primary, secondary, or tertiary education. They are engaged in learning and acquiring knowledge in diverse subjects, seeking academic growth, and preparing for future careers or personal development.`

Sono supportate due origini di pubblico:

* [Adobe Target](#audience-adobe-target)
* [File CSV](#audience-csv-file)

![Genera varianti - Origini pubblico](assets/generate-variations-audiences.png)

### Pubblico - Adobe Target {#audience-adobe-target}

La selezione di un pubblico di **Adobe Target** nel prompt consente di personalizzare la generazione di contenuto per tale pubblico.

>[!NOTE]
>
>Per utilizzare questa opzione, l’organizzazione IMS deve avere accesso ad Adobe Target.

1. Seleziona **Adobe Target**.
1. Quindi seleziona il **Pubblico di destinazione** richiesto dall&#39;elenco fornito.

   >[!NOTE]
   >
   >Per utilizzare un pubblico di **Adobe Target** è necessario compilare il campo di descrizione. In caso contrario, il pubblico viene visualizzato nell’elenco a discesa come non disponibile. Per aggiungere una descrizione, vai a Target e [aggiungi una descrizione del pubblico](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences).

   ![Genera varianti - Origine pubblico - Adobe Target](assets/generate-variations-audiences-adobe-target.png)

#### Aggiungere un pubblico Adobe Target {#add-adobe-target-audience}

Consulta [Creare tipi di pubblico](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences) per creare un pubblico in Adobe Target.

### Pubblico - File CSV {#audience-csv-file}

La selezione di un pubblico di tipo **file CSV** nel prompt consente di personalizzare la generazione di contenuto per il pubblico di tipo **Target** selezionato.

In Adobe sono disponibili diversi tipi di pubblico da utilizzare.

1. Seleziona **file CSV**.
1. Quindi seleziona il **Pubblico di destinazione** richiesto dall&#39;elenco fornito.

   ![Genera varianti - Origine pubblico - File CSV](assets/generate-variations-audiences-csv-file.png)

#### Aggiungi file CSV del pubblico {#add-audience-csv-file}

È possibile aggiungere un file CSV da varie piattaforme (ad esempio, Google Drive, Dropbox, Sharepoint) che hanno la capacità di fornire un URL al file una volta reso pubblicamente disponibile.

>[!NOTE]
>
>Nelle piattaforme di condivisione è *necessario* rendere il file accessibile al pubblico.

Ad esempio, per aggiungere un pubblico da un file su Google Drive:

1. In Google Drive, crea un file di foglio di calcolo con due colonne:
   1. La prima colonna verrà visualizzata nel menu a discesa.
   1. La seconda colonna sarà la descrizione del pubblico.
1. Publish il file:
   1. File -> Condividi -> Pubblica sul Web -> CSV
1. Copia l’URL nel file pubblicato.
1. Vai a Genera varianti.
1. Apri l’Editor richieste.
1. Trova il pubblico **Adobe Target** nei metadati e sostituisci l&#39;URL.

   >[!NOTE]
   >
   >Assicurati che le virgolette doppie (&quot;) siano mantenute su entrambe le estremità dell’URL.

   Ad esempio:

   ![Genera varianti - aggiungi file CSV del pubblico](assets/generate-variations-audiences-csv-save.png)

## Utilizzo azione generativa {#generative-action-usage}

La gestione dell’utilizzo dipende dall’azione intrapresa:

* Generare varianti

  Una generazione di una variante di copia è uguale a una azione generativa. In qualità di cliente, hai un certo numero di azioni generative che vengono fornite con la tua licenza AEM. Una volta utilizzata l’adesione di base, puoi acquistare azioni aggiuntive.

  >[!NOTE]
  >
  >Vedere [Adobe Experience Manager: Cloud Service | Descrizione del prodotto](https://helpx.adobe.com/legal/product-descriptions/aem-cloud-service.html) per ulteriori dettagli sui diritti di base e rivolgiti al team del tuo account per acquistare azioni più generative.

* Adobe Express

  L&#39;utilizzo della generazione di immagini viene gestito tramite adesioni Adobe Express e [crediti generativi](https://helpx.adobe.com/firefly/using/generative-credits-faq.html).

## Accedi a Genera varianti {#access-generate-variations}

Dopo aver soddisfatto i prerequisiti, puoi accedere a Genera varianti da AEM as a Cloud Service o dal Sidekick dei Edge Delivery Services.

### Prerequisiti di accesso {#access-prerequisites}

Per utilizzare Genera varianti è necessario assicurarsi che i prerequisiti siano soddisfatti:

* [Accesso agli as a Cloud Service Experienci Manager con Edge Delivery Services](#access-to-aemaacs-with-edge-delivery-services)

#### Accesso agli as a Cloud Service Experienci Manager con Edge Delivery Services{#access-to-aemaacs-with-edge-delivery-services}

Experience Manager Gli utenti che hanno bisogno di accedere a Genera varianti devono avere diritto a un ambiente as a Cloud Service con Edge Delivery Services.

>[!NOTE]
>
>Se il tuo contratto per AEM Sites as a Cloud Service non include Edge Delivery Services, dovrai firmare un nuovo contratto per ottenere l’accesso.
>
>Rivolgiti al team del tuo account per scoprire come passare ad AEM Sites as a Cloud Service con i Edge Delivery Services.

Per concedere l’accesso a utenti specifici, assegna il loro account utente al rispettivo profilo di prodotto. Consulta [Assegnazione dei profili di prodotto AEM per ulteriori dettagli](/help/journey-onboarding/assign-profiles-cloud-manager.md).

### Accesso da AEM as a Cloud Service {#access-aemaacs}

Genera varianti è accessibile dal [pannello di navigazione](/help/sites-cloud/authoring/basic-handling.md#navigation-panel) di AEM as a Cloud Service:

![Pannello di navigazione](/help/sites-cloud/authoring/assets/basic-handling-navigation.png)

### Accesso dal AEM Sidekick {#access-aem-sidekick}

È necessaria una certa configurazione prima di poter accedere a Genera varianti dal Sidekick (di Edge Delivery Services).

1. Per informazioni su come installare e configurare il Sidekick, vedere il documento [Installazione di AEM Sidekick](https://www.aem.live/docs/sidekick-extension).

1. Per utilizzare Genera varianti nel Sidekick (di Edge Delivery Services), includi la seguente configurazione nei progetti di Edge Delivery Services in:

   * `tools/sidekick/config.json`

   Questo deve essere unito alla configurazione esistente e quindi distribuito.

   Ad esempio:

   ```prompt
   {
     // ...
     "plugins": [
       // ...
       {
         "id": "generate-variations",
         "title": "Generate Variations",
         "url": "https://experience.adobe.com/aem/generate-variations",
         "passConfig": true,
         "environments": ["preview","live", "edit"],
         "includePaths": ["**.docx**"]
       }
       // ...
     ]
   }
   ```

1. Potrebbe quindi essere necessario assicurarsi che gli utenti abbiano [Accesso all&#39;Experience Manager as a Cloud Service con Edge Delivery Services](#access-to-aemaacs-with-edge-delivery-services).

1. Puoi quindi accedere alla funzione selezionando **Genera varianti** dalla barra degli strumenti del Sidekick:

   ![Genera varianti - accesso da AEM Sidekicj](assets/generate-variations-sidekick-toolbar.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta:

* [Genera varianti GenAI su GitHub](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Sperimentazione Edge Delivery Services](https://www.aem.live/docs/experimentation)

## Domande frequenti {#faqs}

### Output formattato {#formatted-outpu}

**La risposta generata non mi fornisce l&#39;output formattato necessario. Come si modifica il formato? Esempio: è necessario un titolo e un sottotitolo, ma la risposta è solo titolo**

1. Apri il prompt effettivo in modalità di modifica.
1. Vai ai requisiti.
1. Troverai requisiti che parlano dell’output.
   1. Esempio: &quot;Il testo deve essere costituito da tre parti: un titolo, un corpo e un’etichetta di pulsante.&quot; o &quot;Formatta la risposta come array JSON valido di oggetti con gli attributi &quot;Title&quot;, &quot;Body&quot; e &quot;ButtonLabel&quot;.
1. Modifica i requisiti in base alle tue esigenze.

   >[!NOTE]
   >
   >Se il nuovo output inserito è soggetto a restrizioni per il conteggio di parole/caratteri, crea un requisito.

   Esempio: &quot;Il testo del titolo non deve superare le 10 parole o i 50 caratteri, spazi inclusi&quot;.
1. Salvare la richiesta per utilizzi futuri.

### Lunghezza della risposta {#length-of-response}

**La risposta generata è troppo lunga o troppo breve. Come si modifica la lunghezza?**

1. Apri il prompt effettivo in modalità di modifica.
1. Vai ai requisiti.
1. Troverai che per ogni output, esiste un limite corrispondente parola/carattere.
   1. Esempio: &quot;Il testo del titolo non deve superare le 10 parole o i 50 caratteri, spazi inclusi&quot;.
1. Modifica i requisiti in base alle tue esigenze.
1. Salvare la richiesta per utilizzi futuri.

### Migliorare le risposte {#improve-responses}

**Le risposte ricevute non sono esattamente ciò che sto cercando. Cosa posso fare per migliorarli?**

1. Provare a modificare la temperatura in Impostazioni avanzate.
   1. Una temperatura più alta si allontana dal prompt e porta a una maggiore variabilità, casualità e creatività.
   1. Una temperatura più bassa è più deterministica e aderisce a ciò che è nel prompt.
1. Apri il prompt effettivo in modalità di modifica e controlla il prompt. Presta particolare attenzione alla sezione dei requisiti che descrive il tono di voce e altri criteri importanti.

### Commenti in un prompt {#comments-in-prompt}

**Come posso usare i commenti in un prompt?**

I commenti in un prompt vengono utilizzati per includere note, spiegazioni o istruzioni che non devono far parte dell&#39;output effettivo. Questi commenti sono racchiusi in una sintassi specifica: iniziano e terminano con doppie parentesi graffe e iniziano con un hash (ad esempio, `{{# Comment Here }}`). I commenti aiutano a chiarire la struttura o l’intento del prompt senza influire sulla risposta generata.

### Trova un prompt condiviso {#find-a-shared-prompt}

**Cosa posso fare se non riesco a trovare un modello di richiesta condiviso da qualcuno?**

In questa situazione ci sono vari dettagli da verificare:

1. Utilizza l’URL per l’ambiente.
Ad esempio, https://experience.adobe.com/#/aem/generate-variations
1. Verifica che l’organizzazione IMS selezionata sia corretta.
1. Conferma che il prompt sia stato salvato come condiviso.

### Richieste personalizzate nella versione v2.0.0 {#custom-prompts-v200}

**Nella versione 2.0.0 le richieste personalizzate non sono più visibili. Come procedere?**

Il passaggio alla versione v2.0.0 causerà l’interruzione dei modelli di prompt personalizzati, che pertanto non saranno disponibili.

Per recuperarli:

1. Passare alla cartella dei modelli di prompt in Sharepoint.
1. Copia il prompt.
1. Aprire l&#39;applicazione Genera varianti.
1. Selezionare la scheda Nuovo prompt.
1. Incolla il prompt.
1. Verifica che il prompt funzioni.
1. Salva il prompt.

## Cronologia delle versioni {#release-history}

Per informazioni dettagliate sulle versioni corrente e precedente, consulta le [Note sulla versione per Genera varianti](/help/generative-ai/release-notes-generate-variations.md)
