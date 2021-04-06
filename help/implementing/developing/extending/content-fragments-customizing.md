---
title: Personalizzazione ed estensione dei frammenti di contenuto
description: Un frammento di contenuto estende una risorsa standard.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
translation-type: tm+mt
source-git-commit: 24da05afce75a16ed2223130ac1825b10ee964e1
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 3%

---

# Personalizzazione ed estensione dei frammenti di contenuto{#customizing-and-extending-content-fragments}

All’interno di Adobe Experience Manager come Cloud Service un frammento di contenuto estende una risorsa standard; vedi:

* [Creazione e gestione di ](/help/assets/content-fragments/content-fragments.md) frammenti di contenuto e authoring delle  [pagine con ](/help/sites-cloud/authoring/fundamentals/content-fragments.md) frammenti di contenuto per ulteriori informazioni sui frammenti di contenuto.

* [Gestione delle ](/help/assets/manage-digital-assets.md) risorse per ulteriori informazioni sulle risorse standard.

<!-- Removing the extend-asset-editor article for now as I'm unsure of its accuracy. Hence commenting this link.
* [Managing Assets](/help/assets/manage-digital-assets.md) and [Customizing and Extending the Asset Editor](/help/assets/extend-asset-editor.md) for further information about standard assets.
-->

## Architettura {#architecture}

Le [parti costituenti di base](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) di un frammento di contenuto sono:

* A *Frammento di contenuto*,
* costituito da uno o più *elementi di contenuto*,
* e che possono avere una o più *Varianti di contenuto*.

I singoli frammenti di contenuto si basano su modelli di frammenti di contenuto:

* I modelli di frammento di contenuto definiscono la struttura di un frammento di contenuto al momento della creazione.
* Un frammento fa riferimento al modello; le modifiche al modello possono quindi influire su eventuali frammenti dipendenti.
* I modelli sono formati da tipi di dati.
* Le funzioni per aggiungere nuove varianti, ecc., devono aggiornare di conseguenza il frammento.

   >[!NOTE]
   >
   >Affinché sia possibile visualizzare/eseguire il rendering di un frammento di contenuto, l’account deve disporre delle autorizzazioni `read` per il modello.

   >[!CAUTION]
   >
   >Qualsiasi modifica apportata a un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti; questo può portare a proprietà orfane in tali frammenti.

### Integrazione di siti con risorse {#integration-of-sites-with-assets}

Content Fragment Management (CFM) fa parte di AEM Assets come:

* I frammenti di contenuto sono risorse.
* Utilizzano la funzionalità Assets esistente.
* Sono completamente integrati con Assets (console di amministrazione, ecc.).

I frammenti di contenuto sono considerati una funzione di Sites come:

* Vengono utilizzati per la creazione delle pagine.

#### Mappatura dei frammenti di contenuto sulle risorse {#mapping-content-fragments-to-assets}

![frammento di contenuto nelle risorse](assets/content-fragment-to-assets.png)

I frammenti di contenuto, basati su un modello di frammento di contenuto, sono mappati su una singola risorsa:

* Tutto il contenuto viene memorizzato sotto il nodo `jcr:content/data` della risorsa:

   * I dati dell’elemento vengono memorizzati sotto il sotto-nodo principale:
      `jcr:content/data/master`

   * Le varianti sono memorizzate sotto un nodo secondario che porta il nome della variante:
ad esempio `jcr:content/data/myvariation`

   * I dati di ciascun elemento vengono memorizzati nel rispettivo sottonodo come proprietà con il nome dell’elemento:
Ad esempio, il contenuto dell’elemento `text` viene memorizzato come proprietà `text` in `jcr:content/data/master`

* I metadati e il contenuto associato sono memorizzati sotto `jcr:content/metadata`
Ad eccezione del titolo e della descrizione, che non sono considerati metadati tradizionali e memorizzati su 
`jcr:content`

#### Posizione risorsa {#asset-location}

Come per le risorse standard, un frammento di contenuto è conservato in:

`/content/dam`

#### Autorizzazioni risorsa {#asset-permissions}

Per ulteriori dettagli, consulta [Considerazioni sulla cancellazione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-delete.md).

#### Integrazione delle funzioni {#feature-integration}

Per integrare con Assets core:

* La funzione Content Fragment Management (CFM) si basa sul core Assets.

* CFM fornisce le proprie implementazioni per gli elementi nelle viste a schede/colonne/elenco; questi plug in nelle implementazioni di rendering dei contenuti di Assets esistenti.

* Sono stati estesi diversi componenti di Assets per gestire i frammenti di contenuto.

### Utilizzo di frammenti di contenuto nelle pagine {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Il componente [Frammento di contenuto fa parte dei componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html). Per ulteriori informazioni, consulta [Sviluppo di componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html) .

È possibile fare riferimento ai frammenti di contenuto da AEM pagine, come per qualsiasi altro tipo di risorsa. AEM fornisce il **[componente di base Frammento di contenuto](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)** - un componente [che consente di includere frammenti di contenuto nelle pagine](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Puoi anche estendere questo componente di base **[Frammento di contenuto](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)**.

* Il componente utilizza la proprietà `fragmentPath` per fare riferimento al frammento di contenuto effettivo. La proprietà `fragmentPath` viene gestita allo stesso modo di proprietà simili di altri tipi di risorse; ad esempio, quando il frammento di contenuto viene spostato in un’altra posizione.

* Il componente ti consente di selezionare la variante da visualizzare.

* È inoltre possibile selezionare una serie di paragrafi per limitare l’output; ad esempio, può essere utilizzato per l’output a più colonne.

* Il componente consente il contenuto intermedio:

   * Qui il componente permette di inserire altre risorse (immagini, ecc.) tra i paragrafi del frammento a cui si fa riferimento.

   * Per il contenuto intermedio è necessario:

      * essere consapevole della possibilità di riferimenti instabili; il contenuto intermedio (aggiunto durante l’authoring di una pagina) non presenta alcuna relazione fissa con il paragrafo accanto al quale è posizionato, mediante l’inserimento di un nuovo paragrafo (nell’editor dei frammenti di contenuto) prima che la posizione del contenuto intermedio perda la posizione relativa

      * prendi in considerazione i parametri aggiuntivi (come filtri per varianti e paragrafi) per configurare il rendering sulla pagina

>[!NOTE]
>
>**Modello per frammenti di contenuto:**
>
>Quando un frammento di contenuto viene utilizzato in una pagina, viene fatto riferimento al modello di frammento di contenuto su cui si basa.
>
>Ciò significa che se il modello non è stato pubblicato al momento della pubblicazione della pagina, verrà contrassegnato e il modello verrà aggiunto alle risorse da pubblicare con la pagina.

### Integrazione con altri framework {#integration-with-other-frameworks}

I frammenti di contenuto possono essere integrati con:

* **Traduzioni**

   I frammenti di contenuto sono completamente integrati con il flusso di lavoro di traduzione AEM. A livello architettonico, ciò significa:

   * Le singole traduzioni di un frammento di contenuto sono in realtà frammenti separati; ad esempio:

      * si trovano sotto radici linguistiche diverse; ma condividono esattamente lo stesso percorso relativo sotto la radice linguistica pertinente:

         `/content/dam/<path>/en/<to>/<fragment>`

         rispetto a

         `/content/dam/<path>/de/<to>/<fragment>`
   * Oltre ai percorsi basati su regole, non esiste un’ulteriore connessione tra le diverse versioni linguistiche di un frammento di contenuto; vengono gestiti come due frammenti separati, anche se l’interfaccia utente fornisce i mezzi per navigare tra le varianti di lingua.
   >[!NOTE]
   >
   >Il flusso di lavoro di traduzione AEM funziona con `/content`:
   >
   >* Poiché i modelli di frammento di contenuto risiedono in `/conf`, non sono inclusi in tali traduzioni. Puoi internazionalizzare le stringhe di interfaccia utente.


* **Schemi metadati**

   * I frammenti di contenuto (ri)utilizzano gli [schemi di metadati](/help/assets/metadata-schemas.md), che possono essere definiti con risorse standard.

   * CFM fornisce il proprio schema specifico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      se necessario, può essere esteso.

   * Il rispettivo modulo schema viene integrato con l’editor frammento.

## API di gestione dei frammenti di contenuto - Lato server {#the-content-fragment-management-api-server-side}

Puoi utilizzare l’API lato server per accedere ai frammenti di contenuto; vedi:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>È consigliabile utilizzare l’API lato server invece di accedere direttamente alla struttura dei contenuti.

### Interfacce chiave {#key-interfaces}

Le tre interfacce seguenti possono fungere da punti di ingresso:

* **Frammento di contenuto**  ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Questa interfaccia consente di lavorare con un frammento di contenuto in modo astratto.

   L’interfaccia ti consente di:

   * Gestire i dati di base (ad esempio nome get; get/set title/description)
   * Accedere ai metadati
   * Elementi di accesso:

      * Elementi elenco
      * Ottieni elementi per nome
      * Creare nuovi elementi (vedere [Avvertenze](#caveats))

      * Accedere ai dati degli elementi (vedere `ContentElement`)
   * Varianti di elenco definite per il frammento
   * Crea nuove varianti a livello globale
   * Gestisci il contenuto associato:

      * Elencare raccolte
      * Aggiungi raccolte
      * Rimuovere le raccolte
   * Accedere al modello del frammento

   Le interfacce che rappresentano gli elementi principali di un frammento sono:

   * **Elemento di contenuto**  ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Accedere alle varianti di un elemento:

         * Varianti di elenco
         * Ottieni varianti per nome
         * Crea nuove varianti (consulta [Avvertenze](#caveats))
         * Rimuovere le varianti (vedere [Avvertenze](#caveats))
         * Accedere ai dati delle varianti (vedere `ContentVariation`)
      * Collegamento per la risoluzione delle varianti (se la variante specificata non è disponibile per un elemento, è possibile applicare una logica di fallback aggiuntiva specifica per l’implementazione)
   * **Variazione di contenuto**  ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Sincronizzazione semplice in base alle ultime informazioni modificate

   Tutte e tre le interfacce ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendono l’interfaccia `Versionable`, che aggiunge le funzionalità di controllo delle versioni richieste per i frammenti di contenuto:

   * Creare una nuova versione dell’elemento
   * Elencare versioni dell’elemento
   * Ottenere il contenuto di una versione specifica dell’elemento con versione







### Adattamento - Utilizzo di adaptTo() {#adapting-using-adaptto}

È possibile adattare quanto segue:

* `ContentFragment` può essere adattato a:

   * `Resource` - la risorsa Sling sottostante; l&#39;aggiornamento del sottostante richiede  `Resource` direttamente la ricostruzione dell&#39; `ContentFragment` oggetto.

   * `Asset` - l’ `Asset` astrazione DAM che rappresenta il frammento di contenuto; per aggiornare  `Asset` direttamente l’ `ContentFragment` oggetto è necessario ricrearlo.

* `ContentElement` può essere adattato a:

   * [`ElementTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - per accedere alle informazioni strutturali dell&#39;elemento.

* [`FragmentTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` può essere adattato a:

   * `ContentFragment`

### Avvertenze {#caveats}

Va osservato che:

* L’intera API è progettata per **non** mantenere le modifiche automaticamente (se non diversamente specificato nel JavaDoc API). Quindi sarà sempre necessario impegnare il risolutore risorse della rispettiva richiesta (o il resolver che si sta effettivamente utilizzando).

* Attività che potrebbero richiedere ulteriore sforzo:

   * Si consiglia vivamente di creare nuove varianti da `ContentFragment`. In questo modo tutti gli elementi condivideranno questa variante e le strutture di dati globali appropriate verranno aggiornate secondo le necessità per riflettere la variante appena creata nella struttura del contenuto.

   * La rimozione delle varianti esistenti tramite un elemento, utilizzando `ContentElement.removeVariation()`, non aggiornerà le strutture di dati globali assegnate alla variante. Per garantire che queste strutture di dati siano mantenute sincronizzate, utilizza invece `ContentFragment.removeVariation()` , che rimuove una variante a livello globale.

## API di gestione dei frammenti di contenuto - Lato client {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>L’API lato client è interna.

### Informazioni aggiuntive {#additional-information}

Consulta le seguenti risorse:

* `filter.xml`

   La `filter.xml` per la gestione dei frammenti di contenuto è configurata in modo che non si sovrapponga al pacchetto di contenuto core Assets.

## Modifica sessioni {#edit-sessions}

>[!CAUTION]
>
>Considera queste informazioni di base. Non devi modificare nulla qui (in quanto è contrassegnato come *area privata* nell&#39;archivio), ma potrebbe aiutare in alcuni casi a capire come funzionano le cose sotto il cofano.

La modifica di un frammento di contenuto, che può estendersi su più viste (= pagine HTML), è atomica. Poiché le funzionalità di modifica a più visualizzazioni atomiche non sono un concetto AEM tipico, i frammenti di contenuto utilizzano una *sessione di modifica*.

Una sessione di modifica viene avviata quando l’utente apre un frammento di contenuto nell’editor. La sessione di modifica è terminata quando l&#39;utente lascia l&#39;editor selezionando **Salva** o **Annulla**.

Tecnicamente, tutte le modifiche vengono eseguite sul contenuto *live*, proprio come per tutte le altre modifiche AEM. Quando la sessione di modifica viene avviata, viene creata una versione dello stato corrente e non modificato. Se un utente annulla una modifica, questa viene ripristinata. Se l&#39;utente fa clic su **Salva**, non viene fatto nulla di specifico, in quanto tutte le modifiche sono state eseguite sul contenuto *live*, pertanto tutte le modifiche sono già persistenti. Inoltre, facendo clic su **Salva** verrà attivata un&#39;elaborazione in background (ad esempio, la creazione di informazioni di ricerca full-text e/o la gestione di risorse con file multimediali diversi).

Esistono alcune misure di sicurezza per i casi di bordo; ad esempio, se l’utente tenta di uscire dall’editor senza salvare o annullare la sessione di modifica. È inoltre disponibile un salvataggio automatico periodico per evitare la perdita di dati.
Tieni presente che due utenti possono modificare contemporaneamente lo stesso frammento di contenuto e pertanto possono sovrascrivere le rispettive modifiche. Per evitare questo problema, il frammento di contenuto deve essere bloccato applicando l’azione *Checkout* dell’amministrazione DAM sul frammento.

## Esempi {#examples}

### Esempio: Accesso a un frammento di contenuto esistente {#example-accessing-an-existing-content-fragment}

A questo scopo, puoi adattare la risorsa che rappresenta l’API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Esempio:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Esempio: Creazione di un nuovo frammento di contenuto {#example-creating-a-new-content-fragment}

Per creare un nuovo frammento di contenuto a livello di programmazione, è necessario utilizzare un
`FragmentTemplate` adattato da una risorsa del modello.

Esempio:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Esempio: Specifica dell&#39;intervallo di salvataggio automatico {#example-specifying-the-auto-save-interval}

L&#39; [intervallo di salvataggio automatico](/help/assets/content-fragments/content-fragments-managing.md#save-close-and-versions) (misurato in secondi) può essere definito utilizzando il gestore di configurazione (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`
* Tipo: `Long`

* Predefinito: `600` (10 minuti); questo è definito in `/libs/settings/dam/cfm/jcr:content`

Se desideri impostare un intervallo di salvataggio automatico di 5 minuti, devi definire la proprietà sul nodo; ad esempio:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`

* Tipo: `Long`

* Valore: `300` (5 minuti equivale a 300 secondi)

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

Per ulteriori informazioni, consulta

* [Componenti core - Componente frammento di contenuto](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)  (consigliato)
