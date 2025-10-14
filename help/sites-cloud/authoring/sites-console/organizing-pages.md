---
title: Organizzazione delle pagine
description: Scopri come organizzare il tuo sito web con AEM.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 9a700e9eb3116252f42bb08db9dadc0e8a6adbf7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 67%

---


# Organizzazione delle pagine {#creating-and-organizing-pages}

Scopri come organizzare il tuo sito web con AEM. Una volta compreso come organizzare le pagine, puoi [creare nuove pagine](/help/sites-cloud/authoring/sites-console/creating-pages.md) e [gestire le pagine esistenti](/help/sites-cloud/authoring/sites-console/managing-pages.md).

## Organizzazione del sito {#organizing-your-site}

In qualità di autore, devi organizzare il tuo sito all’interno di AEM. A tale scopo, dovrai creare e denominare le pagine di contenuto affinché:

* siano facilmente reperibili nell’ambiente di authoring;
* i visitatori possano facilmente sfogliare le pagine nell’ambiente di pubblicazione.

È inoltre possibile utilizzare le [cartelle](#creating-a-new-folder) per organizzare i contenuti.

La struttura del sito web è analoga a una struttura ad albero contenente le pagine dei contenuti. I nomi di queste pagine vengono utilizzati per formare gli URL, mentre i titoli vengono mostrati durante la visualizzazione del contenuto della pagina.

Di seguito è riportato un esempio tratto dal sito [WKND Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it), in cui è possibile accedere a un articolo sugli skatepark (`la-skateparks`):

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Questa struttura può essere visualizzata dalla console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), che consente di spostarsi tra le pagine del sito Web ed eseguire azioni sulle pagine.

## Convenzioni di denominazione delle pagine {#page-naming-conventions}

Durante la creazione di una pagina sono disponibili due campi chiave:

* **[Titolo](#title)**:
   * Viene mostrato all’utente nella console ed è disponibile sopra il contenuto della pagina durante la modifica.
   * Questo campo è obbligatorio.
* **[Nome](#name)**:
   * Viene utilizzato per generare l’URI.
   * L’input dell’utente per questo campo è opzionale. Se non viene specificato, il nome viene derivato dal titolo. Per ulteriori dettagli, consulta la seguente sezione sulle [restrizioni e best practice per i nomi delle pagine](#page-name-restrictions-and-best-practices).

### Restrizioni e best practice per i nomi delle pagine {#page-name-restrictions-and-best-practices}

Il **Titolo** e il **Nome** della pagina possono essere creati separatamente, ma sono correlati:

* Quando crei una pagina, l’unico campo obbligatorio è quello del **Titolo**. Se non viene fornito un **Nome** al momento della creazione della pagina, AEM ne genera uno dai primi 64 caratteri del titolo (rispettando le norme di convalida descritte di seguito). Per rispettare la best practice sui nomi di pagina brevi, vengono utilizzati solo i primi 64 caratteri.
* Se un nome di una pagina è specificato manualmente dall’autore, il limite di 64 caratteri non è applicabile; tuttavia, potrebbero esserci altre limitazioni tecniche sulla lunghezza del nome della pagina.

>[!TIP]
>
>Quando si definisce un nome di una pagina, è buona norma mantenere il nome breve, che deve comunque essere espressivo e facile da ricordare, in modo che il lettore possa facilmente comprenderlo. Per ulteriori informazioni, consulta la [guida allo stile W3C &#x200B;](https://www.w3.org/Provider/Style/TITLE.html) per l’elemento `title`.
>
>Tieni presente che alcuni browser (ad esempio le versioni precedenti di IE) possono accettare solo gli URL fino a una certa lunghezza; pertanto, esistono anche delle ragioni tecniche per cui è bene mantenere brevi i nomi di pagina.

Durante la creazione di una pagina, AEM [convalida il nome della pagina in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposte da AEM e JCR.

I caratteri minimi consentiti sono:

* Da `a` a `z`
* Da `A` a `Z`
* Da `0` a `9`
* `_` (trattino basso)
* `-` (trattino/segno meno)

Per informazioni complete su tutti i caratteri consentiti, consulta le [convenzioni di denominazione](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>I nomi delle pagine non possono superare i 150 caratteri.

### Titolo {#title}

Se durante la creazione di una pagina si specifica solo una pagina **Titolo**, AEM deriva la pagina **Nome** da questa stringa e [convalida il nome in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposte da AEM e JCR.

Un campo **Titolo** che contiene caratteri non validi viene accettato, ma nel nome derivato dal titolo tali caratteri vengono sostituiti. Ad esempio:

| Titolo | Nome derivato |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### Nome {#name}

Se specifichi il nome della pagina **Name** durante la creazione, AEM [lo convalida in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposte da AEM e JCR. Non è possibile utilizzare caratteri non validi nel campo **Nome**. Quando AEM rileva caratteri non validi, il campo viene evidenziato con un messaggio esplicativo.

![Esempio di immissione di un nome di pagina non valido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>È consigliabile evitare di utilizzare, come nome di pagina, codici di due lettere specificati dallo standard ISO-639-1, a meno che non si tratti dell’identificativo della lingua.
>
>Per ulteriori informazioni, consulta l’argomento relativo alla [preparazione dei contenuti per la traduzione](/help/sites-cloud/administering/translation/preparation.md).

## Modelli {#templates}

In AEM, un [modello](/help/sites-cloud/authoring/page-editor/templates.md) è un tipo di pagina specializzato utilizzato come base per qualsiasi nuova pagina creata.

Il modello definisce la struttura di una pagina, comprese una miniatura e altre proprietà. Ad esempio, puoi usare modelli distinti per pagine di prodotti, sitemap e informazioni di contatto. I modelli sono costituiti da [componenti](#components).

AEM viene fornito con diversi modelli preconfigurati. I modelli disponibili dipendono dal singolo sito web. I campi chiave sono i seguenti:

* **Titolo** - Titolo visualizzato nella pagina Web risultante
* **Nome** - Utilizzato per la denominazione della pagina
* **Modello** - Elenco di modelli disponibili per la generazione della nuova pagina

## Componenti {#components}

[I componenti](/help/implementing/developing/components/overview.md) sono gli elementi forniti da AEM che consentono di aggiungere tipi specifici di contenuto. AEM include una serie di componenti predefiniti, denominati [Componenti core](/help/implementing/developing/components/overview.md#core-components), che forniscono funzionalità complete. Alcuni esempi dei componenti sono:

* Testo
* Immagine
* Titolo
* Carosello
* E molti altri

Dopo aver creato e aperto una pagina puoi [aggiungervi il contenuto utilizzando i componenti](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component), disponibili nel [browser componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

>[!TIP]
>
>La [console Componenti](/help/sites-cloud/authoring/components-console.md) fornisce una panoramica dei componenti utilizzati nell’istanza.
