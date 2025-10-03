---
title: Anteprima dei frammenti di contenuto
description: Scopri come visualizzare in anteprima i frammenti di contenuto con una serie di metodi.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 3781b494394405f69892686790c17ffa9c69f28b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# Anteprima dei frammenti di contenuto {#previewing-content-fragments}

I frammenti di contenuto possono essere utilizzati sia per la distribuzione headless che per l’authoring delle pagine. Poiché i frammenti sono esclusivamente contenuti, senza formattazione, la loro revisione può risultare più complessa. Vengono quindi forniti diversi metodi per visualizzare in anteprima i frammenti in diversi scenari.

Sono disponibili diversi metodi per Frammenti di contenuto, accessibili dalla console Frammenti di console e dall’editor. La console e l’editor descritti in questa sezione sono stati sviluppati per la distribuzione di contenuti headless (anche se possono essere utilizzati per tutti gli scenari).

Puoi visualizzare in anteprima il frammento:

* utilizzo del [pattern URL anteprima](#preview-url-pattern)

* pubblicando in e annullando la pubblicazione dall&#39;istanza [Anteprima](#preview-instance)

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

Naturalmente, puoi anche visualizzare il frammento nell&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md).

>[!IMPORTANT]
>
>È possibile accedere ai frammenti di contenuto da due console: **Frammenti di contenuto** e **Assets**.
>
>Esistono anche due editor per l’authoring dei frammenti di contenuto; sebbene la funzionalità di base sia la stessa, vi sono alcune differenze. Entrambi gli editor sono accessibili da entrambe le console.
>
>Questa sezione tratta la console **Frammenti di contenuto** e l&#39;editor frammenti di contenuto *new*. Questi sono stati sviluppati per la distribuzione di contenuti headless (anche se possono essere utilizzati in tutti gli scenari)
>
>Per ulteriori informazioni, consulta:
>
>* utilizzo della console **Assets** per [gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)
>* utilizzo dell&#39;[*editor frammento di contenuto originale*](/help/assets/content-fragments/content-fragments-variations.md),
>* utilizzo di [Frammenti di contenuto per l&#39;authoring delle pagine](/help/sites-cloud/authoring/fragments/content-fragments.md).

## Pattern URL di anteprima {#preview-url-pattern}

L’editor dei frammenti di contenuto offre agli autori la possibilità di visualizzare in anteprima le modifiche apportate in un’applicazione front-end esterna.

Per utilizzare questa funzione, devi innanzitutto:

* Collabora con il tuo team IT per configurare l’applicazione front-end esterna che eseguirà il rendering del frammento di contenuto consumando il relativo output JSON.

* Quando l&#39;applicazione front-end esterna è configurata, il **Pattern URL di anteprima predefinito** deve essere definito come [proprietà del modello per frammenti di contenuto appropriato](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties).

L’URL di anteprima deve seguire questo pattern:

    `https://<preview_url>?param=${expression}`

Le espressioni disponibili sono:

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

Una volta definito l&#39;URL, il pulsante **[Anteprima](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)** è attivo nella barra degli strumenti superiore dell&#39;editor. Puoi selezionare questo pulsante per avviare l’applicazione esterna (in una scheda separata) per eseguire il rendering del frammento di contenuto.

## Anteprima istanza {#preview-instance}

Puoi **Pubblicare** e **Annullare la pubblicazione**, il frammento nel **[Servizio di anteprima](/help/headless/deployment/architecture.md)** (nonché nell&#39;istanza di pubblicazione).

Puoi pubblicare il frammento dall’editor o dalla console.

Consulta:

* [Pubblicazione e anteprima di un frammento](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) per dettagli completi.

* [Annullamento della pubblicazione di un frammento](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) per dettagli completi.

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
