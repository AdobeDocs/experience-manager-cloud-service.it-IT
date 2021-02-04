---
title: Modifica di una SPA esterna all'interno di AEM
description: Questo documento descrive i passaggi consigliati per caricare un SPA standalone in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# Modifica di una SPA esterna in AEM {#editing-external-spa-within-aem}

Quando si decide [quale livello di integrazione ](/help/implementing/developing/headful-headless.md) si desidera avere tra il SPA esterno e il AEM, spesso è necessario essere in grado di modificare e visualizzare il SPA all&#39;interno AEM.

## Panoramica {#overview}

Questo documento descrive i passaggi consigliati per caricare un SPA standalone in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.

## Prerequisiti {#prerequisites}

I prerequisiti sono semplici.

* Assicurarsi che un&#39;istanza di AEM sia in esecuzione localmente.
* Crea un progetto di base AEM SPA utilizzando [il tipo di archivio AEM progetti.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * Questo costituirà la base del progetto AEM che verrà aggiornato per includere il SPA esterno.
   * Per gli esempi in questo documento, stiamo utilizzando il punto di partenza di [il progetto di SPA WKND.](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* Avere a portata di mano la React SPA operativa ed esterna che si desidera integrare.

## Carica SPA in AEM progetto {#upload-spa-to-aem-project}

Innanzitutto, è necessario caricare la SPA esterna nel progetto AEM.

1. Sostituire `src` nella cartella del progetto `/ui.frontend` con la cartella `src` dell&#39;applicazione React.
1. Includi eventuali dipendenze aggiuntive nel file `package.json` dell&#39;app nel file `/ui.frontend/package.json`.
   * Assicurati che SPA dipendenze SDK siano delle [versioni consigliate.](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. Includi eventuali personalizzazioni nella cartella `/public`.
1. Includere eventuali script o stili in linea aggiunti nel file `/public/index.html`.

## Configurare il SPA remoto {#configure-remote-spa}

Ora che il SPA esterno fa parte del progetto AEM, deve essere configurato all’interno di AEM.

### Includere  Adobe SPA pacchetti SDK {#include-spa-sdk-packages}

Per sfruttare AEM funzionalità SPA, esistono dipendenze dai tre pacchetti seguenti.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` fornisce l&#39;API per l&#39;inizializzazione di Model Manager e il recupero del modello dall&#39;istanza AEM. Questo modello può quindi essere utilizzato per eseguire il rendering AEM componenti utilizzando le API di `@adobe/aem-react-editable-components` e `@adobe/aem-spa-component-mapping`.

#### Installazione {#installation}

Eseguite il seguente comando npm per installare i pacchetti richiesti.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inizializzazione ModelManager {#model-manager-initialization}

Prima del rendering dell&#39;app, è necessario inizializzare [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) per gestire la creazione del AEM `ModelStore`.

Questa operazione deve essere eseguita all&#39;interno del file `src/index.js` dell&#39;applicazione o ovunque venga eseguito il rendering della radice dell&#39;applicazione.

A tal fine, è possibile utilizzare l&#39;API `initializationAsync` fornita da `ModelManager`.

La schermata seguente mostra come abilitare l&#39;inizializzazione di `ModelManager` in una semplice applicazione React. L&#39;unico vincolo è che `initializationAsync` deve essere chiamato prima di `ReactDOM.render()`.

![Inizializza ModelManager](assets/external-spa-initialize-modelmanager.png)

In questo esempio, `ModelManager` viene inizializzato e viene creato un `ModelStore` vuoto.

`initializationAsync` Facoltativamente, è possibile accettare un  `options` oggetto come parametro:

* `path` - Al momento dell&#39;inizializzazione, il modello nel percorso definito viene recuperato e memorizzato nel  `ModelStore`. Questo può essere utilizzato per recuperare il `rootModel` all&#39;inizializzazione, se necessario.
* `modelClient` - Consente di fornire un client personalizzato responsabile per il recupero del modello.
* `model` - Un  `model` oggetto passato come parametro generalmente popolato quando si  [utilizza SSR.](/help/implementing/developing/hybrid/ssr.md)

### AEM Componenti Leaf Autorizzati {#authorable-leaf-components}

1. Creare/identificare un componente AEM per il quale verrà creato un componente React autorizzabile. In questo esempio, stiamo utilizzando il componente di testo del progetto WKND.

   ![Componente Testo WKND](assets/external-spa-text-component.png)

1. Create un semplice componente di testo React (Reazione) nella SPA. In questo esempio, è stato creato un nuovo file `Text.js` con il seguente contenuto.

   ![Text.js](assets/external-spa-textjs.png)

1. Create un oggetto di configurazione per specificare gli attributi necessari per abilitare AEM modifica.

   ![Crea oggetto config](assets/external-spa-config-object.png)

   * `resourceType` è obbligatorio mappare il componente React sul componente AEM e attivarlo all’apertura nell’editor AEM.

1. Utilizzare la funzione wrapper `withMappable`.

   ![Usa conMappable](assets/external-spa-withmappable.png)

   Questa funzione wrapper mappa il componente React sul AEM `resourceType` specificato nella configurazione e abilita le funzionalità di modifica quando aperto nell&#39;editor AEM. Per i componenti standalone, recupererà anche il contenuto del modello per il nodo specifico.

   >[!NOTE]
   >
   >In questo esempio sono disponibili diverse versioni del componente: AEM componenti React con wrapper e senza wrapper. La versione a capo deve essere utilizzata quando si utilizza esplicitamente il componente. Quando il componente fa parte di una pagina, potete continuare a usare il componente predefinito come avviene attualmente nell’editor SPA.

1. Eseguire il rendering del contenuto nel componente.

   Le proprietà JCR del componente di testo vengono visualizzate come segue in AEM.

   ![Proprietà dei componenti di testo](assets/external-spa-text-properties.png)

   Questi valori vengono passati come proprietà al componente `AEMText` React appena creato e possono essere utilizzati per il rendering del contenuto.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   Questo è il modo in cui il componente viene visualizzato al termine delle configurazioni AEM.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >In questo esempio, sono state apportate ulteriori personalizzazioni al componente di cui è stato effettuato il rendering in modo che corrisponda al componente di testo esistente. Questo tuttavia non è correlato all’authoring in AEM.

#### Aggiungere componenti modificabili alla pagina {#add-authorable-component-to-page}

Una volta creati i componenti React che possono essere utilizzati in tutta l’applicazione.

Prendiamo una pagina di esempio in cui è necessario aggiungere un testo dal progetto WKND SPA. Per questo esempio, vogliamo visualizzare il testo &quot;Hello World!&quot; su `/content/wknd-spa-react/us/en/home.html`.

1. Determinare il percorso del nodo da visualizzare.

   * `pagePath`: La pagina che contiene il nodo, nel nostro esempio  `/content/wknd-spa-react/us/en/home`
   * `itemPath`: Percorso del nodo all&#39;interno della pagina, nel nostro esempio  `root/responsivegrid/text`
      * È costituito dai nomi degli elementi che li contengono sulla pagina.

   ![Percorso del nodo](assets/external-spa-path.png)

1. Aggiungere un componente alla posizione desiderata nella pagina.

   ![Aggiungere un componente alla pagina](assets/external-spa-add-component.png)

   Il componente `AEMText` può essere aggiunto alla posizione desiderata all&#39;interno della pagina con i valori `pagePath` e `itemPath` impostati come proprietà. `pagePath` è una proprietà obbligatoria.

#### Verifica della modifica del contenuto del testo su AEM {#verify-text-edit}

Ora è possibile testare il componente nell’istanza di AEM in esecuzione.

1. Eseguite il seguente comando Maven dalla directory `aem-guides-wknd-spa` per creare e distribuire il progetto in AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Nell&#39;istanza AEM, passare a `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Modifica del SPA in AEM](assets/external-spa-edit-aem.png)

Il componente `AEMText` è ora compatibile con AEM.

### AEM Pagine Autorizzate {#aem-authorable-pages}

1. Identificare una pagina da aggiungere per l’authoring nel SPA. In questo esempio viene utilizzato `/content/wknd-spa-react/us/en/home.html`.
1. Creare un nuovo file (ad es. `Page.js`) per il componente Pagina modificabile. Qui è possibile riutilizzare il componente Pagina fornito in `@adobe/cq-react-editable-components`.
1. Ripetere il passaggio 4 nella sezione [AEM componenti foglia autorizzabili.](#authorable-leaf-components) Utilizzare la funzione wrapper  `withMappable` sul componente.
1. Come già fatto in precedenza, applicare `MapTo` ai tipi di risorse AEM per tutti i componenti secondari all&#39;interno della pagina.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >In questo esempio stiamo utilizzando il componente di testo React non racchiuso invece del `AEMText` racchiuso creato in precedenza. Questo perché quando il componente fa parte di una pagina/contenitore e non è il solo contenitore, il contenitore si occuperà di mappare in modo ricorsivo il componente e di abilitare le funzionalità di authoring, e il wrapper aggiuntivo non è necessario per ogni elemento secondario.

1. Per aggiungere una pagina modificabile nella SPA, procedere come segue nella sezione [Aggiungi componenti modificabili alla pagina.](#add-authorable-component-to-page) Qui è possibile saltare la  `itemPath` proprietà.

#### Verifica contenuto pagina su AEM {#verify-page-content}

Per verificare che la pagina possa essere modificata, procedere come segue nella sezione [Verifica della modifica del contenuto di testo in AEM.](#verify-text-edit)

![Modifica di una pagina in AEM](assets/external-spa-edit-page.png)

La pagina è ora modificabile su AEM con un Contenitore di layout e un Componente testo secondario.

### Componenti foglia virtuale {#virtual-leaf-components}

Negli esempi precedenti, abbiamo aggiunto componenti al SPA con contenuti AEM esistenti. Tuttavia, in alcuni casi il contenuto non è ancora stato creato in AEM, ma deve essere aggiunto successivamente dall’autore del contenuto. A tal fine, lo sviluppatore front-end può aggiungere componenti nelle posizioni appropriate all’interno del SPA. Questi componenti visualizzeranno dei segnaposto quando vengono aperti nell&#39;editor in AEM. Una volta che il contenuto viene aggiunto all’interno di questi segnaposto dall’autore del contenuto, i nodi vengono creati nella struttura JCR e il contenuto viene mantenuto. Il componente creato consentirà lo stesso set di operazioni dei componenti a foglia autonoma.

In questo esempio, stiamo riutilizzando il componente `AEMText` creato in precedenza. Il nuovo testo deve essere aggiunto sotto il componente di testo esistente nella home page WKND. L’aggiunta di componenti è la stessa dei normali componenti foglia. Tuttavia, è possibile aggiornare `itemPath` al percorso in cui è necessario aggiungere il nuovo componente.

Poiché il nuovo componente deve essere aggiunto sotto il testo esistente in `root/responsivegrid/text`, il nuovo percorso sarà `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

Dopo l&#39;aggiunta del componente virtuale, il componente `TestPage` si presenta come segue.

![Verifica del componente virtuale](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Verificare che il componente `AEMText` sia `resourceType` impostato nella configurazione per abilitare questa funzione.

È ora possibile distribuire le modifiche AEM seguendo la procedura indicata nella sezione [Verifica della modifica del contenuto di testo in AEM.](#verify-text-edit) Verrà visualizzato un segnaposto per il  `text_20` nodo attualmente non esistente.

![Il nodo text_20 in Aem](assets/external-spa-text20-aem.png)

Quando l&#39;autore del contenuto aggiorna questo componente, viene creato un nuovo nodo `text_20` in `root/responsivegrid/text_20` in `/content/wknd-spa-react/us/en/home`.

![Il nodo text20](assets/external-spa-text20-node.png)

#### Requisiti e limitazioni {#limitations}

Esistono diversi requisiti per aggiungere componenti foglia virtuale e alcuni limiti.

* La proprietà `pagePath` è obbligatoria per la creazione di un componente virtuale.
* Il nodo di pagina fornito nel percorso in `pagePath` deve esistere nel progetto AEM.
* Il nome del nodo da creare deve essere specificato in `itemPath`.
* Il componente può essere creato a qualsiasi livello.
   * Se forniamo un `itemPath='text_20'` nell&#39;esempio precedente, il nuovo nodo verrà creato direttamente sotto la pagina, ovvero `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* Il percorso del nodo in cui viene creato un nuovo nodo deve essere valido se fornito tramite `itemPath`.
   * In questo esempio, `root/responsivegrid` deve esistere in modo che sia possibile creare il nuovo nodo `text_20`.
* È supportata solo la creazione di componenti foglia. Il contenitore virtuale e la pagina saranno supportati nelle versioni future.

## Personalizzazioni aggiuntive {#additional-customizations}

Se avete seguito gli esempi precedenti, la vostra SPA esterna ora è modificabile in AEM. Tuttavia, potete personalizzare ulteriormente alcuni aspetti della vostra SPA esterna.

### ID nodo radice {#root-node-id}

Per impostazione predefinita, il rendering dell&#39;applicazione React viene eseguito all&#39;interno di un `div` ID elemento `spa-root`. Se necessario, può essere personalizzato.

Ad esempio, supponiamo che sia presente un SPA in cui l&#39;applicazione viene rappresentata all&#39;interno di un `div` ID elemento `root`. Questo deve essere riflesso in tre file.

1. In `index.js` dell&#39;applicazione React (o dove viene chiamato `ReactDOM.render()`)

   ![ReactDOM.rendering() nel file index.js](assets/external-spa-root-index.png)

1. Nell&#39; `index.html` dell&#39;applicazione React

   ![index.html dell’applicazione](assets/external-spa-index.png)

1. Nel corpo del componente della pagina dell&#39;app AEM tramite due passaggi:

   1. Create un nuovo elemento `body.html` per il componente pagina.

   ![Creare un nuovo file body.html](assets/external-spa-update-body.gif)

   1. Aggiungete il nuovo elemento principale nel nuovo file `body.html`.

   ![Aggiungere l&#39;elemento principale a body.html](assets/external-spa-add-root.png)

### Modifica di un SPA React con Routing {#editing-react-spa-with-routing}

Se l&#39;applicazione React SPA esterna ha più pagine, [può utilizzare il routing per determinare la pagina/il componente da eseguire.](/help/implementing/developing/hybrid/routing.md) L’esempio di base prevede la corrispondenza dell’URL attualmente attivo rispetto al percorso fornito per una route. Per abilitare la modifica su tali applicazioni abilitate per il routing, il percorso a cui confrontarsi deve essere trasformato per contenere informazioni specifiche per AEM.

Nell&#39;esempio seguente è disponibile una semplice applicazione React con due pagine. La pagina di cui eseguire il rendering è determinata dalla corrispondenza del percorso fornito al router rispetto all&#39;URL attivo. Ad esempio, se il numero è impostato su `mydomain.com/test`, verrà eseguito il rendering di `TestPage`.

![Routing in un SPA esterno](assets/external-spa-routing.png)

Per abilitare la modifica entro AEM per questo SPA di esempio, sono necessari i seguenti passaggi.

1. Identificare il livello che fungerebbe da radice su AEM.

   * Per il nostro campione, stiamo considerando wknd-spa-response/us/en come la radice del SPA. Ciò significa che tutto ciò che precede tale percorso è AEM solo pagine/contenuti.

1. Create una nuova pagina al livello desiderato.

   * In questo esempio, la pagina da modificare è `mydomain.com/test`. `test` si trova nel percorso principale dell&#39;app. Questo deve essere mantenuto anche durante la creazione della pagina in AEM. È quindi possibile creare una nuova pagina al livello principale definito nel passaggio precedente.
   * La nuova pagina creata deve avere lo stesso nome della pagina da modificare. In questo esempio per `mydomain.com/test`, la nuova pagina creata deve essere `/path/to/aem/root/test`.

1. Aggiungere gli assistenti all&#39;interno SPA routing.

   * La pagina appena creata non esegue ancora il rendering del contenuto previsto in AEM. Questo perché il router prevede un percorso di `/test` mentre il percorso attivo AEM è `/wknd-spa-react/us/en/test`. Per contenere la porzione AEM specifica dell’URL, è necessario aggiungere alcuni assistenti sul lato SPA.

   ![Helper di routing](assets/external-spa-router-helper.png)

   * A questo scopo è possibile utilizzare il supporto `toAEMPath` fornito da `@adobe/cq-spa-page-model-manager`. Trasforma il percorso fornito per il routing in modo da includere porzioni specifiche AEM quando l&#39;applicazione è aperta in un&#39;istanza AEM. Accetta tre parametri:
      * Percorso richiesto per il routing
      * L&#39;URL di origine dell&#39;istanza AEM in cui viene modificato il SPA
      * Radice del progetto su AEM come determinato nel primo passaggio
   * Questi valori possono essere impostati come variabili di ambiente per una maggiore flessibilità.



1. Verificare la modifica della pagina in AEM.

   * Distribuisci il progetto per AEM e passare alla nuova pagina `test` creata. È ora possibile eseguire il rendering del contenuto della pagina e AEM componenti sono modificabili.

## Risorse aggiuntive {#additional-resources}

Il seguente materiale di riferimento può essere utile per comprendere SPA nel contesto di AEM.

* [Cefalea e senza testa in AEM](/help/implementing/developing/headful-headless.md)
* [Tipo di archivio del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [Progetto WKND SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [Guida introduttiva alle SPA in AEM Utilizzo di React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Materiali di riferimento SPA (riferimenti API)](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA Blueprint e PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [Routing modello SPA](/help/implementing/developing/hybrid/routing.md)
* [Rendering lato SPA e lato server](/help/implementing/developing/hybrid/ssr.md)
