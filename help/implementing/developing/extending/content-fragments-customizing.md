---
title: Personalizzazione ed estensione dei frammenti di contenuto
description: Un frammento di contenuto estende una risorsa standard. Scopri come personalizzarli.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 2%

---

# Personalizzazione ed estensione dei frammenti di contenuto{#customizing-and-extending-content-fragments}

All’interno di Adobe Experience Manager as a Cloud Service, un frammento di contenuto estende una risorsa standard; vedi:

* [Creazione e gestione di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md) e [Authoring di pagine con frammenti di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md) per ulteriori informazioni sui frammenti di contenuto.

* [Gestione di Assets](/help/assets/manage-digital-assets.md) per ulteriori informazioni sulle risorse standard.

## Architettura {#architecture}

Le [parti](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment) di base di un frammento di contenuto sono le seguenti:

* Un *frammento di contenuto* stesso
* È costituito da uno o più *elementi contenuto*
* Può avere una o più *Varianti di contenuto*

I singoli frammenti di contenuto sono basati su modelli per frammenti di contenuto:

* I modelli per frammenti di contenuto definiscono la struttura di un frammento di contenuto al momento della creazione.
* Un frammento fa riferimento al modello, pertanto le modifiche apportate al modello possono influire su qualsiasi frammento dipendente o influire su di esso.
* I modelli sono costituiti da tipi di dati.
* Le funzioni per aggiungere nuove varianti e così via devono aggiornare di conseguenza il frammento.

  >[!NOTE]
  >
  >Per visualizzare/eseguire il rendering di un frammento di contenuto, il tuo account deve disporre di autorizzazioni `read` per il modello.

  >[!CAUTION]
  >
  >Eventuali modifiche apportate a un modello per frammenti di contenuto esistente possono influire sui frammenti dipendenti, con conseguenti proprietà orfane.

### Integrazione di Sites con Assets {#integration-of-sites-with-assets}

La gestione dei frammenti di contenuto (CFM) fa parte di Adobe Experience Manager (AEM) Assets in quanto:

* I frammenti di contenuto sono risorse.
* Utilizzano le funzionalità esistenti di Assets.
* Sono completamente integrati con Assets (console di amministrazione, ecc.).

I frammenti di contenuto sono considerati una funzione di AEM Sites in quanto:

* Vengono utilizzati per la creazione delle pagine.

#### Mappatura di frammenti di contenuto su Assets {#mapping-content-fragments-to-assets}

![frammento di contenuto in risorse](assets/content-fragment-to-assets.png)

I frammenti di contenuto, basati su un modello per frammenti di contenuto, sono mappati su una singola risorsa:

* Tutto il contenuto è archiviato nel nodo `jcr:content/data` della risorsa:

   * I dati dell’elemento vengono memorizzati nel sottonodo principale:
     `jcr:content/data/master`

   * Le varianti vengono memorizzate in un sottonodo che porta il nome della variante:
ad esempio, `jcr:content/data/myvariation`

   * I dati di ciascun elemento vengono memorizzati nel rispettivo sottonodo come proprietà con il nome dell’elemento:
ad esempio, il contenuto dell&#39;elemento `text` è archiviato come proprietà `text` in `jcr:content/data/master`

* I metadati e il contenuto associato sono memorizzati sotto `jcr:content/metadata`
Ad eccezione del titolo e della descrizione, che non sono considerati metadati tradizionali e memorizzati in `jcr:content`

#### Posizione risorsa {#asset-location}

Come per le risorse standard, un frammento di contenuto si trova in:

`/content/dam`

#### Autorizzazioni risorse {#asset-permissions}

Vedi [Frammento di contenuto - Considerazioni sull&#39;eliminazione](/help/sites-cloud/administering/content-fragments/delete-considerations.md).

#### Integrazione delle funzioni {#feature-integration}

Per l’integrazione con Assets Core:

* La funzione di gestione dei frammenti di contenuto (CFM) si basa sul core Assets.

* CFM fornisce le proprie implementazioni per gli elementi nelle viste a schede/colonne/elenchi; queste si collegano alle implementazioni esistenti di rendering dei contenuti Assets.

* Diversi componenti Assets sono stati estesi per gestire i frammenti di contenuto.

### Utilizzo dei frammenti di contenuto nelle pagine {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Il componente [Frammento di contenuto fa parte dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it). Per ulteriori dettagli, vedere [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it).

È possibile fare riferimento ai frammenti di contenuto dalle pagine di AEM, come qualsiasi altro tipo di risorsa. AEM fornisce il **[componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it)** - un [componente che consente di includere frammenti di contenuto nelle pagine](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page). Puoi anche estendere questo componente core **[Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it)**.

* Il componente utilizza la proprietà `fragmentPath` per fare riferimento al frammento di contenuto effettivo. La proprietà `fragmentPath` viene gestita nello stesso modo di proprietà simili di altri tipi di risorse, ad esempio quando il frammento di contenuto viene spostato in un’altra posizione.

* Il componente ti consente di selezionare la variante da visualizzare.

* Inoltre, è possibile selezionare un intervallo di paragrafi per limitare l’output; ad esempio, può essere utilizzato per l’output a più colonne.

* Il componente consente il contenuto intermedio:

   * In questo caso, il componente consente di inserire altre risorse (immagini e così via) tra i paragrafi del frammento di riferimento.

   * Per il contenuto intermedio:

      * Presta attenzione alla possibilità di riferimenti instabili. Il contenuto intermedio (aggiunto durante l’authoring di una pagina) non ha una relazione fissa con il paragrafo posizionato accanto a esso. L’inserimento di un nuovo paragrafo (nell’editor frammento di contenuto) prima che la posizione del contenuto intermedio possa perdere la posizione relativa.

      * Considera i parametri aggiuntivi (come i filtri di variante e di paragrafo) per configurare ciò che viene renderizzato sulla pagina.

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

  I frammenti di contenuto sono completamente integrati con il [flusso di lavoro di traduzione AEM](/help/sites-cloud/administering/translation/overview.md). A livello architettonico, ciò significa:

   * Le singole traduzioni di un frammento di contenuto sono frammenti separati; ad esempio:

      * si trovano in diverse directory principali della lingua, ma condividono il percorso relativo sotto la directory principale della lingua pertinente:

        `/content/dam/<path>/en/<to>/<fragment>`

        rispetto a

        `/content/dam/<path>/de/<to>/<fragment>`

   * Oltre ai percorsi basati su regole, non esiste un’altra connessione tra le diverse versioni linguistiche di un frammento di contenuto. Sono gestiti come due frammenti separati, anche se l’interfaccia utente fornisce i mezzi per navigare tra le varianti di lingua.

  >[!NOTE]
  >
  >Il flusso di lavoro di traduzione AEM funziona con `/content`:
  >
  >* Poiché i modelli per frammenti di contenuto risiedono in `/conf`, non sono inclusi in tali traduzioni. Puoi internazionalizzare le stringhe dell’interfaccia utente.

* **Schemi metadati**

   * I frammenti di contenuto utilizzano e riutilizzano gli [schemi di metadati](/help/assets/metadata-schemas.md) che possono essere definiti con risorse standard.

   * CFM fornisce uno schema specifico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     se necessario, tale periodo può essere prolungato.

   * Il rispettivo modulo schema è integrato con l’editor di frammenti.

## API di gestione dei frammenti di contenuto - Lato server {#the-content-fragment-management-api-server-side}

Puoi utilizzare l’API lato server per accedere ai frammenti di contenuto; vedi:

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Adobe consiglia di utilizzare l’API lato server invece di accedere direttamente alla struttura del contenuto.

### Interfacce chiave {#key-interfaces}

Le tre interfacce seguenti possono fungere da punti di ingresso:

* **Frammento di contenuto** ([Frammento di contenuto](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Questa interfaccia consente di lavorare con un frammento di contenuto in modo astratto.

  L’interfaccia consente di:

   * Gestisci dati di base (ad esempio, nome, titolo/descrizione get/set)
   * Accedere ai metadati
   * Elementi di accesso:

      * Elementi elenco
      * Ottieni elementi per nome
      * Crea elementi (vedi [Avvertenze](#caveats))

      * Accedere ai dati degli elementi (vedere `ContentElement`)

   * Elenca le varianti definite per il frammento
   * Creare varianti a livello globale
   * Gestisci contenuto associato:

      * Elencare raccolte
      * Aggiungere raccolte
      * Rimuovi raccolte

   * Accedere al modello del frammento

  Le interfacce che rappresentano gli elementi principali di un frammento sono:

   * **Elemento contenuto** ([Elemento contenuto](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Accedere alle varianti di un elemento:

         * Varianti elenco
         * Ottieni varianti per nome
         * Crea varianti (vedi [Avvertenze](#caveats))
         * Rimuovi varianti (vedi [Avvertenze](#caveats))
         * Accedere ai dati della variante (vedere `ContentVariation`)

      * Scelta rapida per la risoluzione delle varianti (applicazione di alcune logiche di fallback aggiuntive specifiche per l’implementazione se la variante specificata non è disponibile per un elemento)

   * **Variante contenuto** ([Variante contenuto](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Sincronizzazione semplice, basata sulle informazioni modificate più di recente

  Tutte e tre le interfacce ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendono l&#39;interfaccia `Versionable`, che aggiunge funzionalità di controllo delle versioni, necessarie per i frammenti di contenuto:

   * Creare una versione dell’elemento
   * Elencare le versioni dell’elemento
   * Ottenere il contenuto di una versione specifica dell&#39;elemento con versione

### Adattamento - Utilizzo di adaptTo() {#adapting-using-adaptto}

È possibile adattare:

* `ContentFragment` può essere adattato a:

   * `Resource` - la risorsa Sling sottostante; per aggiornare `Resource` sottostante è necessario ricompilare direttamente l&#39;oggetto `ContentFragment`.

   * `Asset` - L&#39;astrazione DAM `Asset` che rappresenta il frammento di contenuto; l&#39;aggiornamento di `Asset` richiede direttamente la ricostruzione dell&#39;oggetto `ContentFragment`.

* `ContentElement` può essere adattato a:

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - per accedere alle informazioni strutturali dell&#39;elemento.

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` può essere adattato a:

   * `ContentFragment`

### Avvertenze {#caveats}

Si noti che:

* L&#39;intera API è progettata per **non** mantenere le modifiche automaticamente (a meno che non sia indicato diversamente in API JavaDoc). Pertanto, esegui sempre il commit del risolutore risorse della rispettiva richiesta (o del risolutore effettivamente in uso).

* Attività che potrebbero richiedere un ulteriore impegno:

   * Adobe consiglia di creare varianti da `ContentFragment`. In questo modo tutti gli elementi condividono questa variante e le strutture globali di dati appropriate vengono aggiornate secondo necessità per riflettere la nuova variante nella struttura del contenuto.

   * La rimozione delle varianti esistenti tramite un elemento, utilizzando `ContentElement.removeVariation()`, non aggiorna le strutture di dati globali assegnate alla variante. Per garantire la sincronizzazione di queste strutture di dati, utilizzare invece `ContentFragment.removeVariation()`, che rimuove una variante a livello globale.

## API di gestione dei frammenti di contenuto - Lato client {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>L’API lato client è interna.

### Informazioni aggiuntive {#additional-information}

Consulta le seguenti risorse:

* `filter.xml`

  `filter.xml` per la gestione dei frammenti di contenuto è configurato in modo da non sovrapporsi al pacchetto di contenuti di base di Assets.

## Modifica sessioni {#edit-sessions}

>[!CAUTION]
>
>Considera queste informazioni di base. Non è previsto alcun cambiamento qui (in quanto è contrassegnato come *area privata* nell&#39;archivio), ma a volte può essere utile comprendere come funzionano le cose dal punto di vista tecnico.

La modifica di un frammento di contenuto, che può estendersi su più visualizzazioni (= pagine HTML), è atomica. Poiché le funzionalità di modifica atomiche di più viste non sono un concetto tipico di AEM, i frammenti di contenuto utilizzano ciò che viene definita *sessione di modifica*.

Quando l’utente apre un frammento di contenuto nell’editor, viene avviata una sessione di modifica. La sessione di modifica è terminata quando l&#39;utente esce dall&#39;editor selezionando **Salva** o **Annulla**.

Tecnicamente, tutte le modifiche vengono eseguite sul contenuto *live*, come con tutte le altre modifiche di AEM. All&#39;avvio della sessione di modifica, viene creata una versione dello stato corrente non modificato. Se un utente annulla una modifica, la versione viene ripristinata. Se l&#39;utente fa clic su **Salva**, non viene eseguita alcuna operazione specifica, perché la modifica è stata eseguita sul contenuto *live*, pertanto tutte le modifiche sono già persistenti. Inoltre, facendo clic su **Salva** vengono attivate alcune elaborazioni in background, ad esempio la creazione di informazioni di ricerca full-text, la gestione di risorse multimediali diverse o entrambe.

Esistono alcune misure di sicurezza per i casi limite; ad esempio, se l’utente tenta di uscire dall’editor senza salvare o annullare la sessione di modifica. È inoltre disponibile un salvataggio automatico periodico per evitare la perdita di dati.
Due utenti possono modificare lo stesso frammento di contenuto contemporaneamente e quindi sovrascrivere le modifiche l’uno dell’altro. Per evitare questo problema, il frammento di contenuto deve essere bloccato applicando l&#39;azione *Estrai* dell&#39;amministrazione DAM al frammento.

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

### Esempio: creazione di un frammento di contenuto {#example-creating-a-new-content-fragment}

Per creare un frammento di contenuto a livello di programmazione, utilizzare un `FragmentTemplate` adattato da una risorsa modello.

Ad esempio:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Esempio: specifica dell&#39;intervallo di salvataggio automatico {#example-specifying-the-auto-save-interval}

L&#39;[intervallo di salvataggio automatico](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) (misurato in secondi) può essere definito utilizzando Gestione configurazione (ConfMgr):

* Nodo: `<conf-root>/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`
* Tipo: `Long`

* Predefinito: `600` (10 minuti); definito il `/libs/settings/dam/cfm/jcr:content`

Se desideri impostare un intervallo di salvataggio automatico di 5 minuti, definisci la proprietà sul nodo.

Ad esempio:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`

* Tipo: `Long`

* Valore: `300` (5 minuti equivalgono a 300 secondi)

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

Per ulteriori informazioni, consulta

* [Componenti core - Componente frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it) (consigliato)
