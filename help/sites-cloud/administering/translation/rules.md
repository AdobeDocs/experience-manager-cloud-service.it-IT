---
title: Identificazione del contenuto da tradurre
description: Scopri come le regole di traduzione identificano i contenuti da tradurre.
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: 0c75a367861c9e4c77ee537322fa49330c70db85
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 1%

---

# Identificazione del contenuto da tradurre {#identifying-content-to-translate}

Le regole di traduzione identificano il contenuto da tradurre per le pagine, i componenti e le risorse inclusi nei progetti di traduzione o esclusi da essi. Quando una pagina o una risorsa viene tradotta, AEM estrae questo contenuto in modo che possa essere inviato al servizio di traduzione.

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta la nostra [Percorso di traduzione dei siti,](/help/journey-sites/translation/overview.md) percorso guidato attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideali per chi non ha esperienza di AEM o traduzione.

## Frammenti di contenuto e regole di traduzione {#content-fragments}

Le regole di traduzione descritte in questo documento si applicano ai frammenti di contenuto solo se il **Abilita campi del modello di contenuto per la traduzione** l&#39;opzione non è stata attivata nella [livello di configurazione del framework di integrazione della traduzione.](integration-framework.md#assets-configuration-properties)

Se la **Abilita campi del modello di contenuto per la traduzione** è attiva, AEM utilizzerà **Traducibile** campo su [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md#properties) per determinare se il campo deve essere tradotto e crea automaticamente le regole di traduzione di conseguenza. Questa opzione sostituisce eventuali regole di traduzione create e non richiede alcun intervento o passaggi aggiuntivi.

Se desideri utilizzare le regole di traduzione per tradurre i Frammenti di contenuto, l’ **Abilita campi del modello di contenuto per la traduzione** l&#39;opzione sulla configurazione del framework di integrazione della traduzione deve essere disabilitata e devi seguire i passaggi descritti di seguito per creare le regole.

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

Ad esempio, puoi creare una regola che traduca il contenuto aggiunto dagli autori a tutti i componenti di testo sulle tue pagine. La regola può identificare `/content` e `text` per `core/wcm/components/text/v2/text` componente.

C&#39;è una [console](#translation-rules-ui) aggiunta per la configurazione delle regole di traduzione. Le definizioni nell’interfaccia utente compileranno il file per tuo conto.

Per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](overview.md).

>[!NOTE]
>
>AEM supporta la mappatura uno-a-uno tra i tipi di risorse e gli attributi di riferimento per la traduzione del contenuto di riferimento su una pagina.

## Sintassi delle regole per pagine, componenti e risorse {#rule-syntax-for-pages-components-and-assets}

Una regola è `node` elemento con uno o più elementi secondari `property` elementi e zero o più elementi figlio `node` elementi:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Ognuna di queste `node` gli elementi presentano le seguenti caratteristiche:

* La `path` l&#39;attributo contiene il percorso del nodo principale del ramo a cui si applicano le regole.
* Bambino `property` gli elementi identificano le proprietà del nodo da tradurre per tutti i tipi di risorse:
   * La `name` l&#39;attributo contiene il nome della proprietà.
   * L&#39;opzione `translate` attributo è uguale a `false` se la proprietà non è tradotta. Per impostazione predefinita, il valore è `true`. Questo attributo è utile quando si ignorano le regole precedenti.
* Bambino `node` gli elementi identificano le proprietà del nodo da tradurre per tipi di risorse specifici:
   * La `resourceType` L&#39;attributo contiene il percorso che viene risolto nel componente che implementa il tipo di risorsa.
   * Bambino `property` gli elementi identificano la proprietà nodo da tradurre. Usa questo nodo nello stesso modo del figlio `property` elementi per le regole dei nodi.

La regola di esempio seguente causa il contenuto di tutti `text` proprietà da tradurre per tutte le pagine al di sotto del `/content` nodo. La regola è efficace per qualsiasi componente che memorizza il contenuto in un `text` , ad esempio il componente testo.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

L’esempio seguente traduce il contenuto di tutti `text` e traduce anche altre proprietà del componente immagine. Se altri componenti hanno proprietà con lo stesso nome, la regola non si applica ad essi.

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

Ogni `assetNode` presenta le seguenti caratteristiche:

* Uno `resourceType` è uguale al percorso che viene risolto nel componente
* Uno `assetReferenceAttribute` attributo che è uguale al nome della proprietà che memorizza il binario della risorsa (per le risorse incorporate) o il percorso della risorsa di riferimento

L’esempio seguente estrae le immagini dal componente immagine:

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## Regole di sovrascrittura {#overriding-rules}

La `translation_rules.xml` file costituito da `nodelist` elemento con diversi elementi figlio `node` elementi. AEM legge l&#39;elenco dei nodi dall&#39;alto verso il basso. Quando più regole eseguono il targeting dello stesso nodo, viene utilizzata la regola inferiore nel file. Ad esempio, le seguenti regole causano tutto il contenuto in `text` proprietà da tradurre ad eccezione delle `/content/mysite/en` ramo di pagine:

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## Proprietà filtro {#filtering-properties}

Puoi filtrare i nodi con una proprietà specifica utilizzando un `filter` elemento.

Ad esempio, le seguenti regole causano tutto il contenuto in `text` proprietà da tradurre, ad eccezione dei nodi che hanno la proprietà `draft` impostato su `true`.

```xml
<nodelist>
    <node path="/content”>
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

1. Passa a **Strumenti** e poi **Generale**.

1. Seleziona **Configurazione della traduzione**.

Nell’interfaccia utente delle regole di traduzione è possibile:

1. **Aggiungi contesto**, che consente di aggiungere un percorso.

   ![Aggiungi contesto di traduzione](../assets/add-translation-context.png)

1. Utilizza il browser percorsi per selezionare il contesto desiderato e tocca o fai clic sul pulsante **Conferma** per salvare.

   ![Seleziona contesto](../assets/select-context.png)

1. Quindi devi selezionare il contesto e quindi fare clic su **Modifica**. Verrà aperto l’Editor regole di traduzione.

   ![Editor regole di traduzione](../assets/translation-rules-editor.png)

Puoi modificare quattro attributi tramite l’interfaccia utente:

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  è applicabile nei filtri dei nodi ed è true per impostazione predefinita. Controlla se il nodo (o i suoi predecessori) contiene tale proprietà con il valore della proprietà specificato nel filtro. Se false, controlla solo il nodo corrente.

Ad esempio, i nodi figlio vengono aggiunti a un processo di traduzione anche quando il nodo principale ha la proprietà `draftOnly` impostato su true per contrassegnare il contenuto in bozza. Qui `isDeep` entra in gioco e controlla se i nodi principali hanno proprietà `draftOnly` true ed esclude tali nodi figlio.

Nell’editor, puoi selezionare/deselezionare **È profondo** in **Filtri** scheda .

![Regole di filtro](../assets/translation-rules-editor-filters.png)

Esempio del codice XML risultante quando **È profondo** deselezionata nell’interfaccia utente:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### eredita {#inherit}

**`inherit`** è applicabile alle proprietà. Per impostazione predefinita ogni proprietà viene ereditata, ma se si desidera che alcune proprietà non vengano ereditate dall&#39;elemento secondario, è possibile contrassegnare questa proprietà come false in modo che venga applicata solo a quel nodo specifico.

Nell’interfaccia utente, puoi selezionare/deselezionare **Eredita** in **Proprietà** scheda .

### traduci {#translate}

**`translate`** viene utilizzato semplicemente per specificare se tradurre o meno una proprietà.

Nell’interfaccia utente, puoi selezionare/deselezionare **Traduci** in **Proprietà** scheda .

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** viene utilizzato per proprietà che non hanno testo ma codici di lingua, ad esempio `jcr:language`. L&#39;utente non traduce il testo, ma le impostazioni internazionali della lingua dall&#39;origine alla destinazione. Tali proprietà non vengono inviate per la traduzione.

Nell’interfaccia utente, puoi selezionare/deselezionare **Traduci** in **Proprietà** per modificare questo valore, ma per le proprietà specifiche che hanno codici lingua come valore.

Per chiarire la differenza tra `updateDestinationLanguage` e `translate`, ecco un semplice esempio di contesto con due sole regole:

![esempio updateDestinationLanguage](../assets/translation-rules-updatedestinationlanguage.png)

Il risultato nel file xml sarà simile al seguente:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Modifica manuale del file delle regole {#editing-the-rules-file-manually}

La `translation_rules.xml` il file installato con AEM contiene un set predefinito di regole di traduzione. Puoi modificare il file per supportare i requisiti dei tuoi progetti di traduzione. Ad esempio, puoi aggiungere regole per tradurre il contenuto dei componenti personalizzati.

Se modifichi la `translation_rules.xml` conservare una copia di backup in un pacchetto di contenuti. La reinstallazione di alcuni pacchetti AEM può sostituire l&#39;attuale `translation_rules.xml` con l&#39;originale. Per ripristinare le regole in questa situazione, puoi installare il pacchetto che contiene la copia di backup.

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
