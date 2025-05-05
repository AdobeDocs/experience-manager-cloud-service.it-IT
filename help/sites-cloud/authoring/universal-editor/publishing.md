---
title: Pubblicazione di contenuti con l’editor universale
description: Scopri in che modo l’editor universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 64c257adc7e1f22531c0fe45b44b27ab4e0badb8
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 42%

---


# Pubblicazione di contenuti con l’editor universale {#publishing}

Scopri in che modo l’editor universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.

>[!TIP]
>
>Il processo di pubblicazione qui descritto è la funzionalità standard preconfigurata di Universal Editor.
>
>L&#39;editor universale supporta anche [estensioni ed estensibilità dell&#39;interfaccia utente](/help/implementing/universal-editor/extending.md) per consentire ai flussi di lavoro di supportare il processo di pubblicazione, in modo che il flusso di pubblicazione possa variare.

## Pubblicazione di contenuti dall’editor universale {#publishing-content}

Quando sei un autore di contenuti pronto per pubblicare i tuoi contenuti, devi semplicemente toccare o fare clic sull&#39;icona **Pubblica** nella barra degli strumenti dell&#39;editor universale.

![Pubblicazione pagine](assets/publish-menu.png)

1. Nell&#39;editor universale, toccare o fare clic sull&#39;icona [Pubblica **&#x200B;**&#x200B;nella barra degli strumenti dell&#39;editor universale.](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)
1. Se disponi di un [servizio di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md), puoi scegliere dove pubblicare i contenuti, in **Anteprima** o **Pubblicazione**.
1. Nella sezione **Elementi** sono elencati i contenuti inclusi nella pubblicazione, tra cui:
   * **Nuovi** elementi non ancora pubblicati.
   * **Contenuto con modiff** pubblicato ma modificato dopo l&#39;ultima pubblicazione.
   * **Pubblicato** contenuto che è stato pubblicato e non modificato dopo tale pubblicazione.

   Tocca o fai clic sulle caselle di controllo accanto a tali elementi per includerli o escluderli dalla pubblicazione come richiesto. Tocca o fai clic su **Estendi** per visualizzare i singoli elementi inclusi nei totali per le tre categorie e per poterli inserire/escludere singolarmente.

   ![Pubblica elementi](assets/publish-items.png)

   Tocca o fai clic sulla freccia indietro accanto all&#39;intestazione **Elementi** per tornare alla panoramica.

1. Tocca o fai clic su **Pubblica** per pubblicare o su **Annulla** per interrompere.

## Annullamento della pubblicazione di contenuti dall’editor universale {#unpublishing-content}

L’annullamento della pubblicazione dei contenuti ha un funzionamento simile alla pubblicazione dei contenuti. Quando l&#39;autore di contenuto è pronto a rimuovere il contenuto dalla pubblicazione, tocca o fai clic sull&#39;icona con i puntini di sospensione nella barra degli strumenti dell&#39;editor universale e quindi **Annulla pubblicazione**.

Per annullare la pubblicazione del contenuto sono quindi disponibili le stesse opzioni disponibili per [.](#publishing-content) incluso l&#39;annullamento della pubblicazione da un&#39;istanza di anteprima se disponibile e quali elementi includere nell&#39;annullamento della pubblicazione.

## Pubblicazione e annullamento della pubblicazione dalla console Sites {#publishing-sites-console}

Puoi anche pubblicare [dalla console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), utile quando desideri pubblicare più pagine di contenuto o pianificare la pubblicazione o l&#39;annullamento della pubblicazione.

## Somiglianze con l’Editor pagina {#similarities}

Per gli utenti dell&#39;[Editor pagina di AEM](/help/sites-cloud/authoring/page-editor/introduction.md) il processo di pubblicazione dei contenuti con l&#39;Editor universale funziona come di consueto: al momento della pubblicazione in AEM, i contenuti vengono replicati dal livello di authoring a quello di pubblicazione.

## Differenze {#differences}

Ciò che rende la pubblicazione con Universal Editor un po&#39; diversa non è tanto l&#39;editor stesso, ma piuttosto l&#39;hosting esterno dell&#39;app reso possibile da Universal Editor.

Quando è ospitata esternamente, è compito della web app assicurare che il contenuto venga caricato dal livello di authoring quando l’app viene aperta dagli autori all’interno dell’editor, e che venga caricato dal livello di pubblicazione quando i visitatori possono accedere all’app.

## Rilevamento del livello nell’app {#detecting}

Per determinare se il livello di authoring o pubblicazione deve essere accessibile, nell’app puoi usare una semplice istruzione condizionale per scegliere l’endpoint di authoring o pubblicazione appropriato al momento di rilevare l’apertura nell’editor.

Un’altra opzione consiste nell’implementare l’app in due ambienti diversi configurati in maniera diversa, in modo che uno recuperi il contenuto dal livello di authoring e un altro lo recuperi dal livello di pubblicazione. Per consentire agli autori di aprire l’URL pubblicato nell’editor universale, è possibile creare un piccolo script per &quot;convertire&quot; l’URL lato pubblicazione nel suo equivalente nell’ambiente di authoring (ad esempio, anteponendo un sottodominio `author`), in modo che gli autori vengano automaticamente reindirizzati.

## Riepilogo {#summary}

L’obiettivo dell’editor universale è di non imporre alcun modello particolare, in modo che l’implementazione possa raggiungere al meglio i suoi obiettivi in una modalità completamente separata, assicurando al tempo stesso che tutto risulti semplice e chiaro per l’implementazione.

Allo stesso modo, l’editor universale non detta i requisiti su come un particolare progetto debba determinare da quale livello distribuire il contenuto. Al contrario, offre diverse possibilità e consente al progetto di determinare quale soluzione soddisfa al meglio le proprie esigenze.

## Risorse aggiuntive {#additional-resources}

Per informazioni su come creare contenuti con l’editor universale, consulta questo documento.

* [Authoring dei contenuti con l’editor universale](authoring.md): scopri quanto è semplice e intuitivo per gli autori di contenuto creare contenuto utilizzando l’editor universale.

Per ulteriori informazioni sui dettagli tecnici di Universal Editor, consulta questi documenti per gli sviluppatori.

* [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](/help/implementing/universal-editor/authentication.md): scopri come l’editor universale effettua l’autenticazione.
