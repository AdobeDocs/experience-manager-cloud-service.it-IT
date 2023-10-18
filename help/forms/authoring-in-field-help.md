---
title: Come aggiungere il testo della guida per i campi Forms adattivi dell’AEM?
description: AEM Forms consente di aggiungere assistenza contestuale ai campi e ai pannelli del modulo adattivo come testo o file multimediali avanzati, inclusi i video.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---


# Creazione della Guida contestuale per i campi modulo{#authoring-in-context-help-for-form-fields}

## Introduzione {#introduction}

In alcune situazioni, gli utenti finali che compilano un modulo non sono sicuri di come compilare i dettagli di un determinato campo modulo. Per risolvere tali problemi, Forms adattivo fornisce supporto per aggiungere testo o assistenza contestuale avanzata a un campo modulo. Consente di migliorare l’esperienza di compilazione dei moduli ed evita ambiguità per gli utenti finali.

Questo articolo illustra come gli autori di moduli possono aggiungere aiuto contestuale durante l’authoring di Adaptive Forms.

## Aggiungi guida nel contesto {#add-in-context-help}

Puoi specificare la guida contestuale utilizzando le seguenti opzioni nella sezione Contenuto della guida della scheda Proprietà nella barra laterale.

* [Breve descrizione](authoring-in-field-help.md#p-short-description-p)
* [Descrizione lunga](authoring-in-field-help.md#p-long-description-p)

![Guida contestuale per i campi modulo](assets/descriptions.png)

>[!NOTE]
>
>La descrizione lunga sostituisce la descrizione breve. Se sono stati specificati entrambi, verrà visualizzata solo la descrizione Long.

### Breve descrizione {#short-description}

Il campo Descrizione breve fornisce suggerimenti rapidi e brevi sulla compilazione di un campo modulo. Il testo specificato nel campo Descrizione breve viene visualizzato come descrizione comando quando si passa il puntatore del mouse sul campo.

![Breve descrizione per l&#39;aggiunta della guida contestuale per i campi modulo](assets/tooltip.png)

>[!NOTE]
>
>Seleziona **Mostra sempre una breve descrizione** per visualizzare in modo permanente il testo della guida sotto il campo.

![Guida contestuale breve permanente sotto il campo](assets/short1.png)

### Descrizione lunga {#long-description}

È possibile utilizzare il campo Descrizione lunga per specificare testo lungo o incorporare contenuti rich media, inclusi i video, come guida contestuale. Ad esempio, l’immagine seguente mostra come incorporare un video come aiuto contestuale.

![Aggiunta di rich media come guida contestuale per i campi modulo](assets/long-descriptions.png)

Quando si aggiunge una descrizione lunga viene visualizzata una **?** accanto al campo. Facendo clic sull’icona viene visualizzato il contenuto aggiunto nella sezione descrizione lunga.

![Esempio di aiuto contestuale per rich media](assets/photoshop.png)

### Guida a livello di pannello {#panel-level-help}

Oltre alla guida contestuale per i campi modulo, è possibile specificare la guida a livello di pannello nella scheda Contenuto guida della finestra di dialogo di modifica del pannello.

![Aggiunta di informazioni della Guida contestuale a un pannello modulo](assets/panel-level-help.png)

L’aggiunta della guida per il pannello mostra una **?** accanto alla descrizione del pannello. Facendo clic sull’icona viene visualizzato il contenuto aggiunto nella sezione Contenuto della guida della finestra di dialogo per modifica del pannello.

![Esempio di guida contestuale a livello di pannello modulo](assets/photoshop-1.png)

>[!MORELIKETHIS]
>
>* [Aggiungere testo segnaposto ai campi modulo](/help/forms/placeholder-text-in-aem-forms.md)
>* [Aggiungi nota a piè di pagina a un modulo adattivo per testo RTF](/help/forms/footnotes-richtextsupport.md)