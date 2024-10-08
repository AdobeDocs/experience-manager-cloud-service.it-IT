---
title: Come aggiungere il testo della guida per i campi Forms adattivi dell’AEM?
description: AEM Forms consente di aggiungere assistenza contestuale ai campi e ai pannelli del modulo adattivo come testo o file multimediali avanzati, inclusi i video.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: d661f869f1264e4a2317692ab6fd22263c89e072
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---


# Creazione della Guida contestuale per i campi modulo{#authoring-in-context-help-for-form-fields}

## Introduzione {#introduction}

In alcune situazioni, gli utenti finali che compilano un modulo non sono sicuri di come compilare i dettagli di un determinato campo modulo. Per risolvere tali problemi, Forms adattivo fornisce supporto per aggiungere testo o assistenza contestuale avanzata a un campo modulo. Consente di migliorare l’esperienza di compilazione dei moduli ed evita ambiguità per gli utenti finali.

Questo articolo illustra come gli autori di moduli possono aggiungere aiuto contestuale durante l’authoring di Adaptive Forms.

## Aggiungi guida nel contesto {#add-in-context-help}

Puoi specificare la guida contestuale utilizzando le seguenti opzioni nella sezione Contenuto della guida della scheda Proprietà nella barra laterale.

* [Descrizione breve](authoring-in-field-help.md#p-short-description-p)
* [Descrizione lunga](authoring-in-field-help.md#p-long-description-p)

![Guida contestuale per i campi modulo](assets/descriptions.png)

>[!NOTE]
>
>La descrizione lunga sostituisce la descrizione breve. Se sono stati specificati entrambi, verrà visualizzata solo la descrizione Long.

### Descrizione breve {#short-description}

Il campo Descrizione breve fornisce suggerimenti rapidi e brevi sulla compilazione di un campo modulo. Il testo specificato nel campo Descrizione breve viene visualizzato come descrizione comando quando si passa il puntatore del mouse sul campo.

![Breve descrizione per l&#39;aggiunta della guida contestuale per i campi modulo](assets/tooltip.png)

>[!NOTE]
>
>Selezionare **Mostra sempre descrizione breve** per visualizzare in modo permanente il testo della Guida sotto il campo.

![Guida contestuale breve permanente sotto il campo](assets/short1.png)

### Descrizione lunga {#long-description}

È possibile utilizzare il campo Descrizione lunga per specificare testo lungo o incorporare contenuti rich media, inclusi i video, come guida contestuale. Ad esempio, l’immagine seguente mostra come incorporare un video come aiuto contestuale.

![Aggiunta di rich media come guida contestuale per i campi modulo](assets/long-descriptions.png)

Se si aggiunge una descrizione lunga, verrà visualizzato **?Icona** accanto al campo. Facendo clic sull’icona viene visualizzato il contenuto aggiunto nella sezione descrizione lunga.

![Esempio di aiuto nel contesto di rich media](assets/photoshop.png)

### Guida a livello di pannello {#panel-level-help}

Oltre alla guida contestuale per i campi modulo, è possibile specificare la guida a livello di pannello nella scheda Contenuto guida della finestra di dialogo di modifica del pannello.

![Aggiunta della guida contestuale a un pannello del modulo](assets/panel-level-help.png)

L&#39;aggiunta della Guida per il pannello visualizza **?Icona** accanto alla descrizione del pannello. Facendo clic sull’icona viene visualizzato il contenuto aggiunto nella sezione Contenuto della guida della finestra di dialogo per modifica del pannello.

![Esempio di guida contestuale a livello di pannello del modulo](assets/photoshop-1.png)