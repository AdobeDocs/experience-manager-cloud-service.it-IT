---
title: Personalizzazione ed estensione dei frammenti di contenuto
description: Un frammento di contenuto estende una risorsa standard.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 3%

---

# Personalizzazione ed estensione dei frammenti di contenuto{#customizing-and-extending-content-fragments}

All’interno di Adobe Experience Manager as a Cloud Service, un frammento di contenuto estende una risorsa standard; vedi:

* [Creazione e gestione di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md) e [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md) per ulteriori informazioni sui frammenti di contenuto.

* [Gestione delle risorse](/help/assets/manage-digital-assets.md) per ulteriori informazioni sulle risorse standard.

## Architettura {#architecture}

La base [parti costitutive](/help/sites-cloud/administering/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) di un frammento di contenuto:

* A *Frammento di contenuto*,
* costituito da uno o più *Elementi contenuto*,
* e che possono avere uno o più *Varianti di contenuto*.

I singoli frammenti di contenuto sono basati su modelli per frammenti di contenuto:

* I modelli per frammenti di contenuto definiscono la struttura di un frammento di contenuto al momento della creazione.
* Un frammento fa riferimento al modello, pertanto le modifiche apportate al modello possono influire o influenzeranno eventuali frammenti dipendenti.
* I modelli sono costituiti da tipi di dati.
* Le funzioni per aggiungere nuove varianti, ecc., devono aggiornare di conseguenza il frammento.

  >[!NOTE]
  >
  >Per visualizzare/eseguire il rendering di un frammento di contenuto, il tuo account deve avere `read` autorizzazioni per il modello.

  >[!CAUTION]
  >
  >Eventuali modifiche apportate a un modello per frammenti di contenuto esistente possono influire sui frammenti dipendenti, con conseguenti proprietà orfane.

### Integrazione di Sites con Assets {#integration-of-sites-with-assets}

La gestione dei frammenti di contenuto (CFM) fa parte di AEM Assets in quanto:

* I frammenti di contenuto sono risorse.
* Utilizzano la funzionalità Assets esistente.
* Sono completamente integrati con Assets (console di amministrazione, ecc.).

I frammenti di contenuto sono considerati una funzione di Sites in quanto:

* Vengono utilizzati per la creazione delle pagine.

#### Mappatura di frammenti di contenuto su risorse {#mapping-content-fragments-to-assets}

![frammento di contenuto in risorse](assets/content-fragment-to-assets.png)

I frammenti di contenuto, basati su un modello per frammenti di contenuto, sono mappati su una singola risorsa:

* Tutto il contenuto viene archiviato in `jcr:content/data` nodo della risorsa:

   * I dati dell’elemento vengono memorizzati nel sottonodo principale:
     `jcr:content/data/master`

   * Le varianti vengono memorizzate in un sottonodo che porta il nome della variante: ad esempio, `jcr:content/data/myvariation`

   * I dati di ciascun elemento vengono memorizzati nel rispettivo sottonodo come una proprietà con il nome dell’elemento: ad esempio, il contenuto dell’elemento `text` viene memorizzato come proprietà `text` il `jcr:content/data/master`

* I metadati e il contenuto associato sono memorizzati di seguito `jcr:content/metadata`
Ad eccezione del titolo e della descrizione, che non sono considerati metadati tradizionali e memorizzati in `jcr:content`

#### Posizione risorsa {#asset-location}

Come per le risorse standard, un frammento di contenuto si trova in:

`/content/dam`

#### Autorizzazioni risorse {#asset-permissions}

Per maggiori dettagli vedi [Frammento di contenuto - Considerazioni sull’eliminazione](/help/sites-cloud/administering/content-fragments/content-fragments-delete.md).

#### Integrazione delle funzioni {#feature-integration}

Per l’integrazione con Assets Core:

* La funzione di gestione dei frammenti di contenuto (CFM) si basa sulla versione di base di Assets.

* CFM fornisce implementazioni proprie per gli elementi nelle viste a schede/colonne/elenchi; queste si collegano alle implementazioni di rendering dei contenuti delle risorse esistenti.

* Sono stati estesi diversi componenti Assets per gestire i frammenti di contenuto.

### Utilizzo dei frammenti di contenuto nelle pagine {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Il [Il componente Frammento di contenuto fa parte dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it). Consulta [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) per ulteriori dettagli.

È possibile fare riferimento ai frammenti di contenuto dalle pagine dell’AEM, come qualsiasi altro tipo di risorsa. L&#39;AEM fornisce **[Componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it)** - a [componente che consente di includere frammenti di contenuto nelle pagine](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Puoi anche estendere questo **[Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** Componente core.

* Il componente utilizza `fragmentPath` per fare riferimento al frammento di contenuto effettivo. Il `fragmentPath` viene gestita nello stesso modo di proprietà simili di altri tipi di risorse, ad esempio quando il frammento di contenuto viene spostato in un’altra posizione.

* Il componente ti consente di selezionare la variante da visualizzare.

* Inoltre, è possibile selezionare un intervallo di paragrafi per limitare l’output; ad esempio, può essere utilizzato per l’output a più colonne.

* Il componente consente il contenuto intermedio:

   * In questo caso il componente ti consente di inserire altre risorse (immagini, ecc.) tra i paragrafi del frammento a cui si fa riferimento.

   * Per i contenuti intermedi è necessario:

      * tieni presente la possibilità di riferimenti instabili; il contenuto intermedio (aggiunto durante l’authoring di una pagina) non ha una relazione fissa con il paragrafo a cui è posizionato, inserendo un nuovo paragrafo (nell’editor frammento di contenuto) prima che la posizione del contenuto intermedio possa perdere la posizione relativa

      * considera i parametri aggiuntivi (come i filtri di variante e di paragrafo) per configurare ciò che viene renderizzato sulla pagina

>[!NOTE]
>
>**Modello per frammenti di contenuto:**
>
>Quando un frammento di contenuto viene utilizzato in una pagina, viene fatto riferimento al modello per frammenti di contenuto su cui si basa.
>
>Ciò significa che se il modello non è stato pubblicato al momento della pubblicazione della pagina, viene contrassegnato e il modello viene aggiunto alle risorse da pubblicare con la pagina.

### Integrazione con altri framework {#integration-with-other-frameworks}

I frammenti di contenuto possono essere integrati con:

* **Traduzioni**

  I frammenti di contenuto sono completamente integrati con [Flusso di lavoro di traduzione AEM](/help/sites-cloud/administering/translation/overview.md). A livello architettonico, ciò significa:

   * Le singole traduzioni di un frammento di contenuto sono in realtà frammenti separati; ad esempio:

      * si trovano in diverse directory principali della lingua, ma condividono esattamente lo stesso percorso relativo sotto la directory principale della lingua pertinente:

        `/content/dam/<path>/en/<to>/<fragment>`

        rispetto a

        `/content/dam/<path>/de/<to>/<fragment>`

   * Oltre ai percorsi basati su regole, non esiste un’ulteriore connessione tra le diverse versioni linguistiche di un frammento di contenuto; vengono gestiti come due frammenti separati, anche se l’interfaccia utente fornisce i mezzi per navigare tra le varianti di lingua.

  >[!NOTE]
  >
  >Il flusso di lavoro di traduzione dell’AEM funziona con `/content`:
  >
  >* Come risiedono i modelli per frammenti di contenuto `/conf`, questi non sono inclusi in tali traduzioni. Puoi internazionalizzare le stringhe dell’interfaccia utente.

* **Schemi metadati**

   * I frammenti di contenuto (ri)utilizzano [schemi di metadati](/help/assets/metadata-schemas.md), che può essere definito con le risorse standard.

   * CFM fornisce uno schema specifico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     se necessario, questa funzione può essere estesa.

   * Il rispettivo modulo schema è integrato con l’editor di frammenti.

## API di gestione dei frammenti di contenuto - Lato server {#the-content-fragment-management-api-server-side}

Puoi utilizzare l’API lato server per accedere ai frammenti di contenuto; vedi:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Si consiglia vivamente di utilizzare l’API lato server invece di accedere direttamente alla struttura del contenuto.

### Interfacce chiave {#key-interfaces}

Le tre interfacce seguenti possono fungere da punti di ingresso:

* **Frammento di contenuto** ([Frammento di contenuto](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Questa interfaccia consente di lavorare con un frammento di contenuto in modo astratto.

  L’interfaccia consente di:

   * Gestisci dati di base (ad esempio, nome, titolo/descrizione get/set)
   * Accedere ai metadati
   * Elementi di accesso:

      * Elementi elenco
      * Ottieni elementi per nome
      * Creare nuovi elementi (consulta [Avvertenze](#caveats))

      * Accedere ai dati degli elementi (vedere `ContentElement`)

   * Elenca le varianti definite per il frammento
   * Creare nuove varianti a livello globale
   * Gestisci contenuto associato:

      * Elencare raccolte
      * Aggiungere raccolte
      * Rimuovi raccolte

   * Accedere al modello del frammento

  Le interfacce che rappresentano gli elementi principali di un frammento sono:

   * **Elemento contenuto** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Accedere alle varianti di un elemento:

         * Varianti elenco
         * Ottieni varianti per nome
         * Crea nuove varianti (consulta [Avvertenze](#caveats))
         * Rimuovi varianti (consulta [Avvertenze](#caveats))
         * Accedere ai dati delle varianti (vedere `ContentVariation`)

      * Scelta rapida per la risoluzione delle varianti (applicazione di alcune logiche di fallback aggiuntive specifiche per l’implementazione se la variante specificata non è disponibile per un elemento)

   * **Variante contenuto** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Sincronizzazione semplice, basata sulle informazioni modificate più di recente

  Tutte e tre le interfacce ( `ContentFragment`, `ContentElement`, `ContentVariation`a) estendere `Versionable` Interfaccia di, che aggiunge funzionalità di controllo delle versioni, necessaria per i frammenti di contenuto:

   * Crea una nuova versione dell’elemento
   * Elencare le versioni dell’elemento
   * Ottenere il contenuto di una versione specifica dell&#39;elemento con versione

### Adattamento - Utilizzo di adaptTo() {#adapting-using-adaptto}

È possibile adattare:

* `ContentFragment` può essere adattato a:

   * `Resource` - la risorsa Sling sottostante; aggiornamento della risorsa sottostante `Resource` richiede direttamente la ricostruzione del `ContentFragment` oggetto.

   * `Asset` - il DAM `Asset` astrazione che rappresenta il frammento di contenuto; aggiornamento del `Asset` richiede direttamente la ricostruzione del `ContentFragment` oggetto.

* `ContentElement` può essere adattato a:

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - per accedere alle informazioni strutturali dell&#39;elemento.

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` può essere adattato a:

   * `ContentFragment`

### Avvertenze {#caveats}

Si noti che:

* L’intera API è progettata per **non** le modifiche persistono automaticamente (se non diversamente indicato in API JavaDoc). Pertanto, dovrai sempre eseguire il commit del risolutore risorse della rispettiva richiesta (o del risolutore che stai utilizzando).

* Attività che potrebbero richiedere un ulteriore impegno:

   * Si consiglia vivamente di creare nuove varianti da `ContentFragment`. In questo modo tutti gli elementi condividono questa variante e le strutture globali di dati appropriate vengono aggiornate secondo necessità per riflettere la variante appena creata nella struttura del contenuto.

   * Rimozione delle varianti esistenti tramite un elemento, utilizzando `ContentElement.removeVariation()`, non aggiorna le strutture di dati globali assegnate alla variante. Per garantire la sincronizzazione di queste strutture di dati, utilizza `ContentFragment.removeVariation()` rimuove invece una variante a livello globale.

## API di gestione dei frammenti di contenuto - Lato client {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>L’API lato client è interna.

### Informazioni aggiuntive {#additional-information}

Consulta le seguenti risorse:

* `filter.xml`

  Il `filter.xml` per la gestione dei frammenti di contenuto è configurato in modo da non sovrapporsi al pacchetto di contenuti core Assets.

## Modifica sessioni {#edit-sessions}

>[!CAUTION]
>
>Considera queste informazioni di base. Non è necessario modificare nulla qui (in quanto contrassegnato come *area privata* nell’archivio), ma in alcuni casi potrebbe essere utile per comprendere come funzionano le cose dal punto di vista tecnico.

La modifica di un frammento di contenuto, che può estendersi su più visualizzazioni (= pagine HTML), è atomica. Poiché le funzionalità atomiche di modifica in più viste non sono un tipico concetto AEM, i frammenti di contenuto utilizzano ciò che viene definito *sessione di modifica*.

Quando l’utente apre un frammento di contenuto nell’editor, viene avviata una sessione di modifica. La sessione di modifica viene completata quando l’utente esce dall’editor selezionando una delle seguenti opzioni: **Salva** o **Annulla**.

Tecnicamente, tutte le modifiche vengono eseguite il *live* come per tutte le altre modifiche dell&#39;AEM. All&#39;avvio della sessione di modifica, viene creata una versione dello stato corrente non modificato. Se un utente annulla una modifica, la versione viene ripristinata. Se l’utente fa clic su **Salva**, non viene eseguita alcuna operazione specifica, in quanto tutte le modifiche sono state eseguite il *live* pertanto tutte le modifiche sono già persistenti. Inoltre, facendo clic su **Salva** attiverà alcune elaborazioni in background (come la creazione di informazioni di ricerca full-text e/o la gestione di risorse con file multimediali diversi).

Esistono alcune misure di sicurezza per i casi limite; ad esempio, se l’utente tenta di uscire dall’editor senza salvare o annullare la sessione di modifica. È inoltre disponibile un salvataggio automatico periodico per evitare la perdita di dati.
Due utenti possono modificare lo stesso frammento di contenuto contemporaneamente e quindi sovrascrivere le modifiche l’uno dell’altro. Per evitare questo problema, il frammento di contenuto deve essere bloccato applicando la proprietà *Pagamento* sul frammento.

## Esempi {#examples}

### Esempio: accesso a un frammento di contenuto esistente {#example-accessing-an-existing-content-fragment}

A questo scopo, puoi adattare la risorsa che rappresenta l’API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Ad esempio:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Esempio: creazione di un nuovo frammento di contenuto {#example-creating-a-new-content-fragment}

Per creare un nuovo frammento di contenuto a livello di programmazione, è necessario utilizzare una
`FragmentTemplate` adattato da una risorsa modello.

Ad esempio:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Esempio: specifica dell&#39;intervallo di salvataggio automatico {#example-specifying-the-auto-save-interval}

Il [intervallo di salvataggio automatico](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#save-close-and-versions) (misurato in secondi) può essere definito utilizzando la gestione della configurazione (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`
* Tipo: `Long`

* Predefinito: `600` (10 minuti); definito il `/libs/settings/dam/cfm/jcr:content`

Se desideri impostare un intervallo di salvataggio automatico di 5 minuti, devi definire la proprietà sul nodo; ad esempio:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`

* Tipo: `Long`

* Valore: `300` (da 5 minuti a 300 secondi)

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

Per ulteriori informazioni, consulta

* [Componenti core: componente Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) (consigliato)
