---
title: Identificazione del contenuto da tradurre
description: Scopri come le regole di traduzione identificano il contenuto da tradurre.
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 95%

---

# Identificazione del contenuto da tradurre {#identifying-content-to-translate}

Le regole di traduzione identificano il contenuto da tradurre per le pagine, i componenti e le risorse inclusi o esclusi nei progetti di traduzione. Quando una pagina o una risorsa viene tradotta, AEM estrae questo contenuto in modo che possa essere inviato al servizio di traduzione.

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta il [Percorso di traduzione Sites](/help/journey-sites/translation/overview.md) per una guida attraverso la traduzione di contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideali per chi non ha esperienza di AEM o di traduzione.

## Frammenti di contenuto e regole di traduzione {#content-fragments}

Le regole di traduzione descritte in questo documento si applicano ai frammenti di contenuto solo se l’opzione **Abilita campi del modello di contenuto per la traduzione** non è stata abilitata nel [livello di configurazione del framework di integrazione della traduzione.](integration-framework.md#assets-configuration-properties)

Se l’opzione **Abilita campi del modello di contenuto per la traduzione** è attiva, AEM utilizzerà il campo **Traducibile** su [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties) per determinare se il campo deve essere tradotto e crea automaticamente le conseguenti regole di traduzione. Questa opzione sostituisce eventuali regole di traduzione create e non richiede alcun intervento o passaggi aggiuntivi.

Se desideri utilizzare le regole di traduzione per tradurre i frammenti di contenuto, il **Abilita campi modello di contenuto per la traduzione** l’opzione sulla configurazione del framework di integrazione della traduzione deve essere disabilitata e devi seguire i passaggi descritti di seguito per creare le regole.

## Panoramica {#overview}

Le pagine e le risorse sono rappresentate come nodi nell’archivio JCR. Il contenuto estratto è uno o più valori di proprietà dei nodi. Le regole di traduzione identificano le proprietà che contengono il contenuto da estrarre.

Le regole di traduzione sono espresse in formato XML e memorizzate nelle seguenti posizioni possibili:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

Il file si applica a tutti i progetti di traduzione.

Le regole includono le seguenti informazioni:

* Percorso del nodo a cui si applica la regola
   * La regola si applica anche ai discendenti del nodo.
* Nomi delle proprietà del nodo che contengono il contenuto da tradurre
   * La proprietà può essere specifica per un tipo di risorsa specifico o per tutti i tipi di risorsa.

Ad esempio, puoi creare una regola che traduca il contenuto aggiunto dagli autori a tutti i componenti di testo nelle tue pagine. La regola può identificare il nodo `/content` e la proprietà `text` per il componente `core/wcm/components/text/v2/text`.

C’è una [console](#translation-rules-ui) aggiunta per la configurazione delle regole di traduzione. Le definizioni nell’interfaccia utente compileranno il file per tuo conto.

Per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](overview.md).

>[!NOTE]
>
>AEM supporta la mappatura uno-a-uno tra i tipi di risorse e gli attributi di riferimento per la traduzione del contenuto di riferimento su una pagina.

## Sintassi delle regole per pagine, componenti e risorse {#rule-syntax-for-pages-components-and-assets}

Una regola è un `node` elemento con uno o più elementi secondari `property` e zero o più elementi figlio secondari`node`:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Ognuno di questi elementi `node` presentano le seguenti caratteristiche:

* L’attributo `path` contiene il percorso del nodo principale del ramo a cui si applicano le regole.
* Gli elementi secondari `property` identificano le proprietà del nodo da tradurre per tutti i tipi di risorse:
   * L’attributo `name` contiene il nome della proprietà.
   * L’attributo opzionale `translate` è uguale a `false` se la proprietà non è tradotta. Il valore per impostazione predefinita è `true`. Questo attributo è utile quando si ignorano le regole precedenti.
* Gli elementi secondari `node` identificano le proprietà del nodo da tradurre per tipi di risorsa specifici:
   * L’attributo `resourceType` contiene il percorso che viene risolto nel componente che implementa il tipo di risorsa.
   * Gli elementi secondari `property` identificano la proprietà nodo da tradurre. Usa questo nodo nello stesso modo degli elementi secondari `property` per le regole dei nodi.

La regola di esempio seguente causa il contenuto di tutte le proprietà `text` da tradurre per tutte le pagine al di sotto del nodo `/content`. La regola è efficace per qualsiasi componente che memorizza il contenuto in una proprietà `text`, ad esempio il componente testo.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

L’esempio seguente traduce il contenuto di tutte le proprietà `text` e traduce anche altre proprietà del componente immagine. Se altri componenti hanno proprietà con lo stesso nome, la regola non si applica a essi.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Sintassi delle regole per l’estrazione delle risorse dalle pagine  {#rule-syntax-for-extracting-assets-from-pages}

Utilizza la sintassi della regola seguente per includere le risorse incorporate nei componenti o a cui si fa riferimento da essi:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Ogni elemento `assetNode` presenta le seguenti caratteristiche:

* Un attributo `resourceType` è uguale al percorso che viene risolto nel componente
* Un attributo `assetReferenceAttribute` che è uguale al nome della proprietà che memorizza il binario della risorsa (per le risorse incorporate) o il percorso della risorsa di riferimento

L’esempio seguente estrae le immagini dal componente immagine:

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## Regole di sovrascrittura {#overriding-rules}

Il file `translation_rules.xml` è costituito da un elemento `nodelist` con diversi elementi secondari `node`. AEM legge l’elenco dei nodi dall’alto verso il basso. Quando più regole sono indirizzate allo stesso nodo, viene utilizzata la regola inferiore nel file. Ad esempio, le seguenti regole causano la traduzione di tutto il contenuto in proprietà `text` ad eccezione del ramo `/content/mysite/en` di pagine:

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## Proprietà filtro {#filtering-properties}

Puoi filtrare i nodi con una proprietà specifica utilizzando un elemento `filter`.

Ad esempio, le seguenti regole causano la traduzione di tutto il contenuto in proprietà `text`, ad eccezione dei nodi che hanno la proprietà `draft` impostata su `true`.

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Interfaccia utente per le regole di traduzione {#translation-rules-ui}

È disponibile anche una console per configurare le regole di traduzione.

Per accedervi:

1. Passa a **Strumenti** e poi a **Generale**.

1. Seleziona **Configurazione traduzione**.

Nell’interfaccia utente delle regole di traduzione puoi:

1. **Aggiungi contesto**, che ti consente di aggiungere un percorso.

   ![Aggiungi contesto di traduzione](../assets/add-translation-context.png)

1. Utilizza il browser Percorsi per selezionare il contesto desiderato e selezionare **Conferma** per salvare.

   ![Seleziona contesto](../assets/select-context.png)

1. Poi devi selezionare il contesto e fare clic su **Modifica**. Viene aperto l’Editor regole di traduzione.

   ![Editor regole di traduzione](../assets/translation-rules-editor.png)

Puoi modificare quattro attributi tramite l’interfaccia utente:

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  è applicabile nei filtri dei nodi ed è true per impostazione predefinita. Controlla se il nodo (o i suoi predecessori) contiene tale proprietà con il valore della proprietà specificato nel filtro. Se false, controlla solo il nodo corrente.

Ad esempio, i nodi secondari vengono aggiunti a un processo di traduzione anche quando il nodo principale ha la proprietà `draftOnly` impostata su true per contrassegnare il contenuto in formato bozza. Qui `isDeep` entra in gioco e controlla se i nodi principali hanno proprietà `draftOnly` come true ed esclude tali nodi secondari.

Nell&#39;editor, puoi selezionare/deselezionare **Deep** nella scheda **Filtri**.

![Regole filtro](../assets/translation-rules-editor-filters.png)

Esempio del codice XML risultante quando **Deep** non è spuntato nell’interfaccia utente:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### eredita {#inherit}

**`inherit`** è applicabile alle proprietà. Per impostazione predefinita ogni proprietà viene ereditata, ma se vuoi che alcune non vengano ereditate dall&#39;elemento secondario, puoi contrassegnarle come false in modo che venga applicata solo a quel nodo specifico.

Nell’interfaccia utente, puoi selezionare/deselezionare **Eredita** nella scheda **Proprietà**.

### traduci {#translate}

**`translate`** viene utilizzato semplicemente per specificare se tradurre o meno una proprietà.

Nell’interfaccia utente, puoi selezionare/deselezionare **Traduci** nella scheda **Proprietà**.

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** viene utilizzato per proprietà che non hanno testo ma codici di lingua, ad esempio `jcr:language`. L&#39;utente non traduce il testo, ma la lingua locale dal sorgente alla destinazione. Tali proprietà non vengono inviate per la traduzione.

Nell&#39;interfaccia utente, puoi selezionare/deselezionare **Traduci** nella scheda **Proprietà** per modificare questo valore, ma per le proprietà specifiche che hanno come valore i codici lingua.

Per chiarire la differenza tra `updateDestinationLanguage` e `translate`, ecco un semplice esempio di contesto con due sole regole:

![esempio updateDestinationLanguage](../assets/translation-rules-updatedestinationlanguage.png)

Il risultato nel file xml sarà simile al seguente:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Modifica manuale del file delle regole {#editing-the-rules-file-manually}

Il file `translation_rules.xml` installato con AEM contiene un set predefinito di regole di traduzione. Puoi modificare il file per supportare i requisiti dei tuoi progetti di traduzione. Ad esempio, puoi aggiungere regole per tradurre il contenuto dei componenti personalizzati.

Se modifichi il file `translation_rules.xml`, conserva una copia di backup in un pacchetto di contenuti. La reinstallazione di alcuni pacchetti AEM può sostituire l&#39;attuale file `translation_rules.xml` con l&#39;originale. Per ripristinare le regole in questa situazione, puoi installare il pacchetto che contiene la copia di backup.

>[!NOTE]
>
>Dopo aver creato il pacchetto di contenuti, ricostruisci il pacchetto ogni volta che modifichi il file.

## Esempio di file delle regole di traduzione {#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
