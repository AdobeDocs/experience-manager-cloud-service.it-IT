---
title: Guida all’authoring nel contesto per i campi del modulo
seo-title: Authoring in-context help for form fields
description: AEM Forms consente di aggiungere aiuto contestuale ai campi e ai pannelli dei moduli adattivi, come testo o rich media, compresi i video.
seo-description: AEM Forms allows you to add in-context help to Adaptive Form fields and panels, as text or rich media, including videos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---


# Guida all’authoring nel contesto per i campi del modulo{#authoring-in-context-help-for-form-fields}

## Introduzione {#introduction}

In alcune situazioni gli utenti finali che compilano un modulo non sono sicuri di come compilare i dettagli in un particolare campo del modulo. Per risolvere tali problemi, Adaptive Forms fornisce il supporto per aggiungere testo o aiuto contestuale avanzato a un campo del modulo. Consente di migliorare l’esperienza di compilazione del modulo ed evita qualsiasi ambiguità per gli utenti finali.

Questo articolo illustra come gli autori dei moduli possono aggiungere aiuto contestuale durante la creazione di Forms adattivo.

## Aggiungi aiuto nel contesto {#add-in-context-help}

È possibile specificare la guida contestuale utilizzando le seguenti opzioni nella sezione Contenuto della Guida della scheda delle proprietà nella barra laterale.

* [Breve descrizione](authoring-in-field-help.md#p-short-description-p)
* [Descrizione lunga](authoring-in-field-help.md#p-long-description-p)

![Aiuto contestuale per i campi modulo](assets/descriptions.png)

>[!NOTE]
>
>La descrizione lunga sostituisce la descrizione breve. Se sono stati specificati entrambi, verrà visualizzata solo la descrizione lunga.

### Breve descrizione {#short-description}

Il campo Breve descrizione fornisce suggerimenti rapidi e brevi sulla compilazione di un campo del modulo. Il testo specificato nel campo Descrizione breve viene visualizzato come descrizione comando quando si passa il mouse sul campo.

![Breve descrizione dell’aggiunta della guida contestuale per i campi modulo](assets/tooltip.png)

>[!NOTE]
>
>Seleziona **Mostra sempre una breve descrizione** per visualizzare in modo permanente il testo della guida sotto il campo.

![Aiuto permanente nel contesto sotto il campo](assets/short1.png)

### Descrizione lunga {#long-description}

Puoi utilizzare il campo Descrizione lunga per specificare il testo lungo o incorporare contenuti rich media, compresi video, come aiuto contestuale. Ad esempio, l’immagine seguente mostra come incorporare un video come aiuto contestuale.

![Aggiunta di contenuti multimediali avanzati come aiuto contestuale per i campi modulo](assets/long-descriptions.png)

Aggiunta di una descrizione lunga **?** accanto al campo . Fai clic sull’icona per visualizzare il contenuto aggiunto nella sezione della descrizione lunga.

![Esempio di aiuto contestuale rich media](assets/photoshop.png)

### Aiuto a livello di pannello {#panel-level-help}

Oltre alla guida contestuale per i campi modulo, è possibile specificare la guida a livello di pannello nella scheda Contenuto della Guida della finestra di dialogo di modifica del pannello.

![Aggiunta di aiuto contestuale a un pannello del modulo](assets/panel-level-help.png)

Aggiunta di aiuto per la visualizzazione di un pannello **?** accanto alla descrizione del pannello. Facendo clic sull’icona viene visualizzato il contenuto aggiunto nella sezione Contenuto della Guida della finestra di dialogo di modifica del pannello.

![Esempio di aiuto contestuale a livello di pannello del modulo](assets/photoshop-1.png)

