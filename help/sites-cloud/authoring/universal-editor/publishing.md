---
title: Pubblicazione di contenuti con l’editor universale
description: Scopri in che modo l’editor universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: fd52e51c336e65ae698c5102cbe00b90e7038b5e
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 31%

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

1. Nell&#39;editor universale, toccare o fare clic sull&#39;icona [Pubblica **** nella barra degli strumenti dell&#39;editor universale.](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)
1. Se hai un [servizio di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) disponibile, puoi scegliere dove pubblicare i contenuti, in **[Anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md)** (se disponibile) o **Pubblica**.
1. Nella sezione **Elementi** sono elencati i contenuti inclusi nella pubblicazione. Tocca o fai clic su **Visualizza** per visualizzare i dettagli, tra cui:
   * **Nuovi** elementi non ancora pubblicati.
   * **Contenuto modificato** che è stato pubblicato, ma modificato dopo l&#39;ultima pubblicazione.
   * **Pubblicato** contenuto che è stato pubblicato e non modificato dopo tale pubblicazione.

   Tocca o fai clic sulle caselle di controllo accanto a tali elementi per includerli o escluderli dalla pubblicazione come richiesto. Tocca o fai clic su **Estendi** per visualizzare i singoli elementi inclusi nei totali per le tre categorie e per poterli inserire/escludere singolarmente.

   ![Pubblica elementi](assets/publish-items.png)

   Tocca o fai clic sulla freccia indietro accanto all&#39;intestazione **Elementi** per tornare alla panoramica.

1. Tocca o fai clic su **Pubblica** per pubblicare o su **Annulla** per interrompere.

>[!NOTE]
>
>L&#39;opzione per la pubblicazione nell&#39;anteprima [ può essere disabilitata](/help/implementing/universal-editor/customizing.md#publish-preview) e pertanto potrebbe non essere visualizzata nell&#39;editor.

## Annullamento della pubblicazione di contenuti dall’editor universale {#unpublishing-content}

L’annullamento della pubblicazione dei contenuti ha un funzionamento simile alla pubblicazione dei contenuti. Quando l&#39;autore di contenuto è pronto a rimuovere il contenuto dalla pubblicazione, tocca o fai clic sull&#39;icona con i puntini di sospensione nella barra degli strumenti dell&#39;editor universale e quindi **Annulla pubblicazione**.

Per annullare la pubblicazione del contenuto sono quindi disponibili le stesse opzioni disponibili per [.](#publishing-content) incluso l&#39;annullamento della pubblicazione da un&#39;istanza di anteprima se disponibile e quali elementi includere nell&#39;annullamento della pubblicazione.

## Pubblicazione e annullamento della pubblicazione dalla console Sites {#publishing-sites-console}

Puoi anche pubblicare [dalla console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), utile quando desideri pubblicare più pagine di contenuto o pianificare la pubblicazione o l&#39;annullamento della pubblicazione.

## Risorse aggiuntive {#additional-resources}

Per informazioni su come creare contenuti con l’editor universale, consulta questo documento.

* [Authoring dei contenuti con l’editor universale](authoring.md): scopri quanto è semplice e intuitivo per gli autori di contenuto creare contenuto utilizzando l’editor universale.

Per ulteriori informazioni sui dettagli tecnici di Universal Editor, consulta questi documenti per gli sviluppatori.

* [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](/help/implementing/universal-editor/authentication.md): scopri come l’editor universale effettua l’autenticazione.
