---
title: Configurazione del contenitore di layout e della modalità di layout
description: Scopri come configurare il contenitore di layout e la modalità di layout per abilitare i layout reattivi per gli autori di contenuti.
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 70a35cfeb163967b0f627d3ac6495f112d922974
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 2%

---


# Configurazione del contenitore di layout e della modalità di layout {#configuring-layout-container-and-layout-mode}

Scopri come configurare il contenitore di layout e la modalità di layout per abilitare i layout reattivi per gli autori di contenuti.

>[!TIP]
>
>Questo documento descrive come un amministratore del sito può configurare il contenitore di layout per supportare la progettazione web responsive. Sono disponibili risorse aggiuntive:
>
>* Per gli autori di contenuto, i dettagli sull&#39;utilizzo delle funzionalità di progettazione reattiva in una pagina di contenuto sono disponibili nel documento [Layout reattivo.](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
>* Per gli sviluppatori, i dettagli del Contenitore di layout e della griglia reattiva sono descritti nel documento [Progettazione reattiva,](/help/implementing/developing/introduction/responsive-design.md) che fornisce suggerimenti e suggerimenti per l&#39;utilizzo dei contenitori di layout e della griglia reattiva durante la progettazione del sito.

## Panoramica {#overview}

Il layout reattivo è un meccanismo per la realizzazione di [responsive web design](https://en.wikipedia.org/wiki/Responsive_web_design). Questo consente all’autore di contenuto di creare pagine web con un layout e dimensioni che dipendono dai dispositivi utilizzati dagli utenti.

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* **[Contenitore layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)** - Questo componente fornisce un sistema paragrafo griglia che consente di aggiungere e posizionare i componenti all&#39;interno di una griglia reattiva.
   * Può essere utilizzato come parsys predefinito per la pagina e/o reso disponibile agli autori nel browser componenti.
   * Il componente predefinito **Contenitore di layout** è definito in `/libs/wcm/foundation/components/responsivegrid`.
   * Puoi definire i contenitori di layout:
      * Come componente che l’utente può aggiungere a una pagina.
      * Come parsys predefinito per la pagina.
      * Come componente e come parsys di default.
         * Puoi avere il contenitore di layout come standard per la pagina, consentendo allo stesso tempo all’utente di aggiungere ulteriori contenitori di layout all’interno di questo; ad esempio, per ottenere il controllo delle colonne.
* **[Modalità Layout](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)** - Una volta che il Contenitore di layout è posizionato nella pagina, è possibile utilizzare la modalità **Layout** per posizionare il contenuto all&#39;interno della griglia reattiva.
* **[Emulatore](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)** - Consente di creare e modificare siti Web dinamici che riorganizzano il layout in base alle dimensioni del dispositivo o della finestra ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare come viene eseguito il rendering del contenuto utilizzando l’emulatore.

Con questi meccanismi basati su una griglia dinamica è possibile:

* Utilizza i punti di interruzione (che indicano il raggruppamento del dispositivo) per definire un comportamento di contenuto diverso in base al layout del dispositivo.
* Nascondi i componenti in base al gruppo di dispositivi (definisci il punto di interruzione in cui un componente verrà nascosto).
* Utilizzate l&#39;aggancio orizzontale alla griglia (posizionate i componenti nella griglia, ridimensionate secondo necessità, definite quando comprimerli o rifluirli per essere affiancati o superiori/inferiori).
* Gestire il controllo delle colonne.

>[!NOTE]
>
>Durante la creazione di un sito da [Archetipo progetto](#addlink) o dal [Modello di sito standard](#addlink), il layout reattivo è generalmente configurato. In caso contrario, devi [attivare il componente Contenitore di layout](#enable-the-layout-container-component-for-page) per le pagine.

## Abilitazione dell’emulatore {#enabling-emulator}

L&#39;[Archetipo progetto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) e il [Modello di sito standard](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template) sono già abilitati per utilizzare l&#39;emulatore. Se hai sviluppato contenuti personalizzati non basati sui Componenti core o sull&#39;archetipo, consulta il documento [Progettazione reattiva](/help/implementing/developing/introduction/responsive-design.md) per informazioni dettagliate su come sviluppare i componenti sfruttando queste funzioni.

## Attiva modalità layout per il sito {#activate-layout-mode-for-your-site}

La modalità **Layout** consente di utilizzare l&#39;emulatore per regolare il layout del contenuto per dispositivi diversi. Il sito di esempio WKND è già abilitato per la modalità **Layout**. Per abilitare il tuo sito, segui la procedura riportata di seguito.

### Configurare i punti di interruzione {#configure-breakpoints}

I punti di interruzione sono vitali per la progettazione reattiva e definiscono come e quando il contenuto viene regolato sul dispositivo di destinazione. Tuttavia, presta attenzione, poiché ogni punto di interruzione introdotto genererà ulteriore lavoro per gli autori in modo da includere il contenuto. Spesso possono essere sufficienti due punti di interruzione, incluso il punto di interruzione predefinito che è sempre presente. Adobe consiglia di non creare più di tre punti di interruzione, incluso il valore predefinito, ovvero non più di due nodi sotto `cq:responsive/breakpoint`.

* I punti di interruzione hanno un titolo e una larghezza:
   * Il titolo descrive il raggruppamento di dispositivi generico, se necessario con orientamento.
      * Ad esempio, `phone`, `tablet`
   * La larghezza definisce la larghezza massima in pixel per il raggruppamento di dispositivi generico.
      * Ad esempio, se il telefono del punto di interruzione ha una larghezza di 768, deve corrispondere alla larghezza massima del layout utilizzato per un dispositivo telefonico.
* I punti di interruzione possono essere definiti:
   * Nel modello della pagina, da dove le impostazioni vengono copiate nelle pagine create con tale modello.
   * Nel nodo della pagina, da dove le impostazioni vengono ereditate da eventuali pagine figlie.
* I punti di interruzione sono visibili come marcatori nella parte superiore dell’editor di pagine quando si utilizza l’emulatore.
* I punti di interruzione vengono ereditati dalla gerarchia dei nodi padre e possono essere sostituiti a piacimento.
* Esiste un punto di interruzione predefinito (predefinito) che copre tutto ciò che si trova oltre l’ultimo punto di interruzione configurato.
* I punti di interruzione possono essere definiti utilizzando CRXDE Lite o XML.

I punti di interruzione dovrebbero essere presi in considerazione sia per i progetti nuovi che per quelli esistenti.

* Se stai impostando un nuovo progetto, devi aggiungere punti di interruzione ai modelli.
* Se stai eseguendo la migrazione di un progetto esistente (con contenuto esistente), devi:
   * Aggiungere punti di interruzione ai modelli.
   * Aggiungere gli stessi punti di interruzione alle pagine esistenti.

A causa dell’ereditarietà, è necessario eseguire questa operazione solo per la pagina principale del contenuto.

#### Configurazione dei punti di interruzione tramite CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Utilizzando CRXDE Lite, accedi a:

   * Definizione del modello.
   * Il nodo `jcr:content` della pagina.

1. In `jcr:content` creare il nodo:

   * Nome: `cq:responsive`
   * Tipo: `nt:unstructured`

1. In questo caso, crea il nodo:

   * Nome: `breakpoints`
   * Tipo: `nt:unstructured`

1. Nel nodo dei punti di interruzione è possibile creare un numero qualsiasi di punti di interruzione. Ogni definizione è un singolo nodo con le seguenti proprietà:

   * Nome: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Titolo: `String <descriptive title seen in Emulator>`
   * Larghezza: `Decimal <value of breakpoint>`

#### Configurazione dei punti di interruzione tramite XML {#configuring-breakpoints-using-xml}

I punti di interruzione si trovano all&#39;interno della sezione `<jcr:content>` di `.context.html` nella cartella del modello (o del contenuto) appropriata.

Esempio di definizione:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## Abilita il ridimensionamento dei componenti per la pagina {#enable-component-resizing-for-the-page}

Il ridimensionamento dei componenti in modalità **Layout** è una parte importante della progettazione reattiva, che può essere utilizzata nel sito di esempio WKND. Per abilitare il tuo sito, segui la procedura riportata di seguito.

### Imposta contenitore layout come parsys principale {#set-layout-container-as-main-parsys}

Per impostare il parsys principale della pagina come contenitore di layout, definisci il parsys come:

`wcm/foundation/components/responsivegrid`

In:

* Componente pagina
* Modello pagina (per utilizzi futuri)

I due esempi seguenti illustrano la definizione:

* **HTL:**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### Includi CSS reattivo {#include-the-responsive-css}

#### CSS per i punti di interruzione che utilizzano MENO {#css-for-breakpoints-using-less}

AEM utilizza LESS per generare parti del CSS necessario, che devono essere incluse nei progetti.

È necessario creare una [libreria client](/help/implementing/developing/introduction/clientlibs.md) per fornire ulteriori chiamate di configurazione e funzione. Il seguente estratto LESS è un esempio del minimo da aggiungere al progetto:

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

La definizione della griglia di base è disponibile in:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Considerazioni sullo stile {#styling-considerations}

I componenti contenuti in un contenitore reattivo vengono ridimensionati (insieme ai rispettivi elementi DOM HTML) in base alla dimensione della griglia reattiva. Pertanto, in queste circostanze, si consiglia di evitare (o aggiornare) le definizioni degli elementi DOM a larghezza fissa (contenuti).

Ad esempio:

* Prima:

   * `width=100px`

* Dopo:

   * `max-width=100px`

#### Ridimensionamento e conformità dell&#39;immagine adattiva {#resizing-and-adaptive-image-compliance}

Qualsiasi ridimensionamento di un componente all’interno della griglia attiva i seguenti listener, a seconda delle necessità:

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

Per ridimensionare e aggiornare correttamente il contenuto di un&#39;immagine adattiva inclusa in una griglia reattiva, è necessario aggiungere un set `afterEdit` al listener `REFRESH_PAGE` nel file `EditConfig` di ogni componente contenuto.

Ad esempio:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Il meccanismo di immagine adattiva è reso disponibile tramite uno script che controlla la selezione dell’immagine corretta per le dimensioni correnti della finestra. Si attiva dopo che il DOM è pronto o quando si riceve un evento dedicato. Attualmente è necessario aggiornare la pagina per riflettere correttamente il risultato dell’azione dell’utente.

>[!CAUTION]
>
>Le librerie client dei fogli di stile personalizzati devono essere caricate come parte dell’intestazione affinché funzionino correttamente sia sull’authoring che sulla pubblicazione.

## Abilitare il componente Contenitore di layout per la pagina {#enable-the-layout-container-component-for-page}

Per un layout dinamico efficace, l’autore di contenuto deve essere in grado di trascinare le istanze del componente Contenitore di layout sulla pagina. Questa opzione è già abilitata per il sito di esempio WKND. Per abilitare il tuo sito, segui la procedura riportata di seguito.

### Abilitare il componente Contenitore di layout per la modifica delle pagine {#enable-the-layout-container-component-for-page-editing}

Per consentire agli autori di aggiungere ulteriori griglie reattive alle pagine di contenuto, devi abilitare il componente Contenitore di layout per la pagina. Puoi eseguire questa operazione utilizzando:

* **Tramite l&#39;ambiente di authoring** - [Modifica i modelli di pagina](/help/sites-cloud/authoring/page-editor/templates.md) per abilitare il contenitore di layout per una pagina.
* **Definizione componente**. Utilizzare `allowedComponent` o un&#39;inclusione statica durante la definizione del componente.

### Configurare la griglia del contenitore di layout {#configure-the-grid-of-the-layout-container}

Puoi configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout [modificando i modelli di pagina](/help/sites-cloud/authoring/page-editor/templates.md).

### Griglie reattive nidificate {#nested-responsive-grids}

La best practice consigliata da Adobe è mantenere la struttura il più piatto possibile.

Se non puoi evitare di utilizzare le griglie reattive nidificate, consulta il documento per sviluppatori [Progettazione reattiva.](/help/implementing/developing/introduction/responsive-design.md#nested-responsive-grids)
