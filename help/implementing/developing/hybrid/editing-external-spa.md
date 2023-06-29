---
title: Modifica di uno SPA esterno in AEM
description: Questo documento descrive i passaggi consigliati per caricare un SPA autonomo in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.
exl-id: 7978208d-4a6e-4b3a-9f51-56d159ead385
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2421'
ht-degree: 2%

---

# Modifica di uno SPA esterno in AEM {#editing-external-spa-within-aem}

Quando si decide [quale livello di integrazione](/help/implementing/developing/headful-headless.md) vorresti avere una relazione tra il tuo SPA esterno e l’AEM; tieni presente che devi essere in grado di modificare e visualizzare spesso l’SPA all’interno dell’AEM.

## Panoramica {#overview}

Questo documento descrive i passaggi consigliati per caricare un SPA autonomo in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.

## Prerequisiti {#prerequisites}

I prerequisiti sono semplici.

* Verificare che un&#39;istanza dell&#39;AEM sia in esecuzione localmente.
* Creare un progetto AEM SPA di base utilizzando [l’archetipo del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties).
   * Forms la base del progetto AEM che viene aggiornato per includere l&#39;SPA esterno.
   * Per gli esempi di questo documento, l’Adobe utilizza il punto di partenza di [il progetto WKND SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor).
* Avere l&#39;SPA React funzionante esterno che si desidera integrare a portata di mano.

## Carica SPA in progetto AEM {#upload-spa-to-aem-project}

Innanzitutto, devi caricare l’SPA esterno nel tuo progetto AEM.

1. Sostituisci `src` nel `/ui.frontend` cartella di progetto con l&#39;applicazione React `src` cartella.
1. Includi eventuali dipendenze aggiuntive nel file `package.json` nel `/ui.frontend/package.json` file.
   * Assicurati che le dipendenze dell’SDK dell’SPA siano [versioni consigliate](/help/implementing/developing/hybrid/getting-started-react.md#dependencies).
1. Includi tutte le personalizzazioni in `/public` cartella.
1. Includi eventuali script o stili in linea aggiunti nel `/public/index.html` file.

## Configurare l’SPA remoto {#configure-remote-spa}

Ora che l’SPA esterno fa parte del progetto AEM, deve essere configurato all’interno dell’AEM.

### Includi pacchetti SDK SPA di Adobe {#include-spa-sdk-packages}

Per sfruttare le caratteristiche dell&#39;SPA dell&#39;AEM, ci sono dipendenze dai tre pacchetti seguenti.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/login?next=/package/@adobe/aem-spa-model-manager)

Il `@adobe/aem-spa-page-model-manager` fornisce l’API per inizializzare Model Manager e recuperare il modello dall’istanza AEM. Questo modello può quindi essere utilizzato per eseguire il rendering dei componenti AEM utilizzando le API di `@adobe/aem-react-editable-components` e `@adobe/aem-spa-component-mapping`.

#### Installazione {#installation}

Esegui quanto segue `npm` per installare i pacchetti richiesti.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inizializzazione di ModelManager {#model-manager-initialization}

Prima del rendering dell’app, il [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) deve essere inizializzato per gestire la creazione dell’AEM `ModelStore`.

Questa inizializzazione deve essere eseguita all&#39;interno di `src/index.js` dell’applicazione o ovunque venga eseguito il rendering della directory principale dell’applicazione.

Per eseguire questa inizializzazione, puoi utilizzare `initializationAsync` API fornite da `ModelManager`.

La schermata seguente mostra come abilitare l’inizializzazione del `ModelManager` in una semplice applicazione React. L&#39;unico vincolo è che `initializationAsync` deve essere chiamato prima di `ReactDOM.render()`.

![Inizializza ModelManager](assets/external-spa-initialize-modelmanager.png)

In questo esempio, la proprietà `ModelManager` è inizializzato e un valore vuoto `ModelStore` viene creato.

Il `initializationAsync` può facoltativamente accettare un `options` object come parametro:

* `path` - Al momento dell&#39;inizializzazione, il modello nel percorso definito viene recuperato e memorizzato nel `ModelStore`. Questo percorso può essere utilizzato per recuperare `rootModel` all’inizializzazione, se necessario.
* `modelClient` - Consente di fornire un client personalizzato responsabile del recupero del modello.
* `model` - A `model` l&#39;oggetto passato come parametro viene generalmente popolato quando [utilizzo di SSR](/help/implementing/developing/hybrid/ssr.md).

### Componenti foglia compatibili con AEM {#authorable-leaf-components}

1. Creare/identificare un componente AEM per il quale viene creato un componente React modificabile. In questo esempio, utilizza il componente testo del progetto WKND.

   ![Componente testo WKND](assets/external-spa-text-component.png)

1. Creare un componente testo React semplice nell’SPA. In questo esempio, un nuovo file `Text.js` è stato creato con il seguente contenuto.

   ![Text.js](assets/external-spa-textjs.png)

1. Crea un oggetto di configurazione in modo da poter specificare gli attributi necessari per abilitare la modifica AEM.

   ![Crea oggetto di configurazione](assets/external-spa-config-object.png)

   * `resourceType` è obbligatorio per mappare il componente React al componente AEM e abilitare la modifica quando si apre nell’editor AEM.

1. Utilizzare la funzione wrapper `withMappable`.

   ![Usa conMappable](assets/external-spa-withmappable.png)

   Questa funzione wrapper mappa il componente React all’AEM `resourceType` specificato nella configurazione e abilita le funzionalità di modifica quando viene aperto nell’editor AEM. Per i componenti autonomi, recupera anche il contenuto del modello per il nodo specifico.

   >[!NOTE]
   >
   >In questo esempio, esistono versioni separate del componente: componenti AEM wrapped e React unwrapped. La versione racchiusa deve essere utilizzata quando si utilizza esplicitamente il componente. Quando il componente fa parte di una pagina, puoi continuare a utilizzare il componente predefinito come già fatto nell’editor SPA.

1. Esegui il rendering del contenuto nel componente.

   Le proprietà JCR del componente testo vengono visualizzate come segue in AEM.

   ![Proprietà del componente Testo](assets/external-spa-text-properties.png)

   Questi valori vengono passati come proprietà al nuovo `AEMText` React e può essere utilizzato per riprodurre il contenuto.

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

   Di seguito è riportato l’aspetto del componente una volta completate le configurazioni dell’AEM.

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
   >In questo esempio, sono state apportate ulteriori personalizzazioni al componente di cui è stato eseguito il rendering, in modo che corrisponda al componente testo esistente. Non è correlato all’authoring in AEM.

#### Aggiungere componenti autorizzabili alla pagina {#add-authorable-component-to-page}

Una volta creati i componenti React, puoi utilizzarli in tutta l’applicazione.

Prendiamo una pagina di esempio in cui devi aggiungere un testo dal progetto WKND SPA. In questo esempio, si desidera visualizzare il testo &quot;Hello World!&quot; il `/content/wknd-spa-react/us/en/home.html`.

1. Determina il percorso del nodo da visualizzare.

   * `pagePath`: la pagina che contiene il nodo, in questo esempio `/content/wknd-spa-react/us/en/home`
   * `itemPath`: percorso del nodo all’interno della pagina, in questo esempio `root/responsivegrid/text`
      * È costituito dai nomi degli elementi che la contengono nella pagina.

   ![Percorso del nodo](assets/external-spa-path.png)

1. Aggiungi il componente nella posizione richiesta nella pagina.

   ![Aggiungi componente alla pagina](assets/external-spa-add-component.png)

   Il `AEMText` Il componente può essere aggiunto nella posizione desiderata all’interno della pagina con `pagePath` e `itemPath` valori impostati come proprietà. `pagePath` è una proprietà obbligatoria.

#### Verifica della modifica del contenuto di testo su AEM {#verify-text-edit}

Ora testa il componente sull’istanza AEM in esecuzione.

1. Esegui il seguente comando Maven da `aem-guides-wknd-spa` in modo da poter generare e distribuire il progetto a AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Nell’istanza AEM, passa a `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Modifica dell&#39;SPA nell&#39;AEM](assets/external-spa-edit-aem.png)

Il `AEMText` Il componente è ora disponibile per l’authoring su AEM.

### Pagine AEM modificabili {#aem-authorable-pages}

1. Identifica una pagina da aggiungere per l’authoring nell’SPA. Questo esempio utilizza `/content/wknd-spa-react/us/en/home.html`.
1. Creare un file (ad esempio, `Page.js`) per il componente Pagina modificabile. utilizzare il componente Pagina fornito in `@adobe/cq-react-editable-components`.
1. Ripeti il passaggio quattro nella sezione [Componenti foglia modificabili dall’AEM](#authorable-leaf-components). Utilizzare la funzione wrapper `withMappable` sul componente.
1. Come già fatto in precedenza, applica `MapTo` ai tipi di risorse AEM per tutti i componenti secondari all’interno della pagina.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >In questo esempio, viene utilizzato il componente testo React non racchiuso invece del componente testo racchiuso `AEMText` creato in precedenza. Il motivo è che quando il componente fa parte di una pagina o di un contenitore e non è indipendente, il contenitore si occupa della mappatura ricorsiva del componente. Inoltre, non è necessario abilitare le funzionalità di authoring e il wrapper aggiuntivo per ogni bambino.

1. Per aggiungere una pagina modificabile nell’SPA, segui gli stessi passaggi descritti nella sezione [Aggiungere componenti autorizzabili alla pagina](#add-authorable-component-to-page). In questo caso, puoi saltare `itemPath` proprietà.

#### Verifica contenuto pagina in AEM {#verify-page-content}

Per verificare che la pagina possa essere modificata, segui gli stessi passaggi descritti nella sezione [Verificare la modifica del contenuto di testo su AEM](#verify-text-edit).

![Modifica di una pagina in AEM](assets/external-spa-edit-page.png)

La pagina è ora modificabile su AEM con un contenitore di layout e un componente testo figlio.

### Componenti foglia virtuale {#virtual-leaf-components}

Negli esempi precedenti, hai aggiunto componenti all’SPA con contenuti AEM esistenti. Tuttavia, in alcuni casi il contenuto non è ancora stato creato in AEM, ma deve essere aggiunto successivamente dall’autore del contenuto. Per soddisfare questo scenario, lo sviluppatore front-end può aggiungere componenti nelle posizioni appropriate all’interno dell’SPA. Questi componenti visualizzano i segnaposto quando vengono aperti nell’editor in AEM. Dopo che il contenuto viene aggiunto all’interno di questi segnaposto dall’autore del contenuto, i nodi vengono creati nella struttura JCR e il contenuto viene mantenuto. Il componente creato consente di eseguire le stesse operazioni dei componenti foglia autonomi.

In questo esempio, stai riutilizzando `AEMText` componente creato in precedenza. Desideri che venga aggiunto nuovo testo sotto il componente testo esistente nella home page di WKND. L’aggiunta dei componenti è la stessa dei normali componenti foglia. Tuttavia, il `itemPath` può essere aggiornato al percorso in cui è necessario aggiungere il nuovo componente.

Perché il nuovo componente deve essere aggiunto sotto il testo esistente in `root/responsivegrid/text`, il nuovo percorso è `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

Il `TestPage` dopo l’aggiunta del componente virtuale, il componente si presenta come segue.

![Verifica del componente virtuale](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Assicurati che `AEMText` il componente ha il suo `resourceType` nella configurazione in modo da poter abilitare questa funzione.

Ora puoi implementare le modifiche all’AEM seguendo i passaggi descritti nella sezione [Verifica della modifica del contenuto di testo su AEM](#verify-text-edit). Viene visualizzato un segnaposto per il file attualmente non esistente `text_20` nodo.

![Nodo text_20 in AEM](assets/external-spa-text20-aem.png)

Quando l’autore di contenuto aggiorna questo componente, viene aggiunto un nuovo `text_20` il nodo viene creato alle `root/responsivegrid/text_20` in `/content/wknd-spa-react/us/en/home`.

![Nodo text20](assets/external-spa-text20-node.png)

#### Requisiti e limitazioni {#limitations}

Esistono diversi requisiti per aggiungere componenti foglia virtuali e alcune limitazioni.

* Il `pagePath` è obbligatoria per la creazione di un componente virtuale.
* Il nodo pagina fornito nel percorso in `pagePath` deve esistere nel progetto AEM.
* Il nome del nodo da creare deve essere fornito nel `itemPath`.
* Il componente può essere creato a qualsiasi livello.
   * Se fornisci un’ `itemPath='text_20'` nell’esempio precedente, il nuovo nodo viene creato direttamente sotto la pagina, ovvero `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* Il percorso del nodo in cui viene creato un nuovo nodo deve essere valido quando fornito tramite `itemPath`.
   * In questo esempio, `root/responsivegrid` deve esistere affinché il nuovo nodo `text_20` possono essere create lì.
* È supportata solo la creazione di componenti foglia. Contenitore virtuale e pagina saranno supportati nelle versioni future.

### Contenitori virtuali {#virtual-containers}

È supportata la possibilità di aggiungere contenitori, anche se il contenitore corrispondente non è ancora stato creato in AEM. Il concetto e l’approccio sono simili a [componenti foglia virtuale](#virtual-leaf-components).

Lo sviluppatore front-end può aggiungere i componenti contenitore nelle posizioni appropriate all’interno dell’SPA e questi componenti visualizzano dei segnaposto quando vengono aperti nell’editor nell’AEM. L’autore può quindi aggiungere componenti e il relativo contenuto al contenitore, che crea i nodi richiesti nella struttura JCR.

Ad esempio, se esiste un contenitore in `/root/responsivegrid`e lo sviluppatore desidera aggiungere un contenitore secondario:

![Posizione contenitore](assets/container-location.png)

Il `newContainer` non esiste ancora nel AEM.

Durante la modifica della pagina che contiene questo componente in AEM, viene visualizzato un segnaposto vuoto per un contenitore in cui l’autore può aggiungere contenuti.

![Segnaposto contenitore](assets/container-placeholder.png)

![Posizione del contenitore in JCR](assets/container-jcr-structure.png)

Una volta che l’autore aggiunge un componente secondario al contenitore, il nuovo nodo del contenitore viene creato con il nome corrispondente nella struttura JCR.

![Contenitore con contenuto](assets/container-with-content.png)

![Contenitore con contenuto in JCR](assets/container-with-content-jcr.png)

È ora possibile aggiungere al contenitore altri componenti e contenuti necessari all’autore e mantenere le modifiche.

#### Requisiti e limitazioni {#container-limitations}

Esistono diversi requisiti per aggiungere contenitori virtuali e alcune limitazioni.

* I criteri per determinare quali componenti possono essere aggiunti vengono ereditati dal contenitore principale.
* L’elemento padre diretto del contenitore da creare deve esistere in AEM.
   * Se il contenitore `root/responsivegrid` esiste nel contenitore AEM, quindi è possibile creare un nuovo contenitore fornendo il percorso `root/responsivegrid/newContainer`.
   * Tuttavia `root/responsivegrid/newContainer/secondNewContainer` non è possibile.
* È possibile creare un solo nuovo livello di componente alla volta.

## Personalizzazioni aggiuntive {#additional-customizations}

Se hai seguito gli esempi precedenti, il tuo SPA esterno è ora modificabile all’interno dell’AEM. Tuttavia, vi sono altri aspetti del vostro SPA esterno che potete personalizzare ulteriormente.

### ID nodo principale {#root-node-id}

Per impostazione predefinita, si può supporre che l&#39;applicazione React sia rappresentata all&#39;interno di un `div` di ID elemento `spa-root`. Se necessario, questa sintassi può essere personalizzata.

Ad esempio, supponiamo di avere un SPA in cui l’applicazione viene riprodotta all’interno di un `div` di ID elemento `root`. Questa sintassi deve essere riportata su tre file.

1. In `index.js` dell’applicazione React (o dove `ReactDOM.render()` è chiamato)

   ![ReactDOM.render() nel file index.js](assets/external-spa-root-index.png)

1. In `index.html` dell’applicazione React

   ![Il file index.html dell&#39;applicazione](assets/external-spa-index.png)

1. Nel corpo del componente Pagina dell’app AEM, segui questi due passaggi:

   1. Creare un `body.html` per il componente Pagina.

   ![Creare un file body.html](assets/external-spa-update-body.gif)

   1. Aggiungi l’elemento principale nel nuovo `body.html` file.

   ![Aggiungi l’elemento principale a body.html](assets/external-spa-add-root.png)

### Modifica di un SPA React con routing {#editing-react-spa-with-routing}

Se l’applicazione esterna React SPA ha più pagine, [può utilizzare il routing per determinare la pagina/componente di cui eseguire il rendering](/help/implementing/developing/hybrid/routing.md). Il caso d’uso di base prevede che l’URL attualmente attivo corrisponda al percorso fornito per una route. Per abilitare la modifica nelle applicazioni abilitate per l&#39;instradamento, il percorso a cui deve corrispondere deve essere trasformato per adattarsi alle informazioni specifiche dell&#39;AEM.

Nell&#39;esempio seguente, si dispone di una semplice applicazione React con due pagine. La pagina di cui eseguire il rendering viene determinata confrontando il percorso fornito al router con l’URL attivo. Ad esempio, se usi `mydomain.com/test`, `TestPage` è sottoposto a rendering.

![Indirizzamento in un SPA esterno](assets/external-spa-routing.png)

Per abilitare la modifica all’interno dell’AEM per questo esempio di SPA, sono necessari i seguenti passaggi.

1. Identificare il livello che fungerebbe da base per l’AEM.

   * Per il tuo campione, considera wknd-spa-react/us/en come la radice dell’SPA. Questa radice significa che tutto ciò che precede quel percorso è solo pagine/contenuti AEM.

1. Crea una pagina al livello richiesto.

   * In questo esempio, la pagina da modificare è `mydomain.com/test`. `test` si trova nel percorso principale dell’app. Questo percorso principale deve essere mantenuto anche durante la creazione della pagina in AEM. Pertanto, puoi creare una pagina al livello principale definito nel passaggio precedente.
   * La nuova pagina creata deve avere lo stesso nome della pagina da modificare. In questo esempio, per `mydomain.com/test`, la nuova pagina creata deve essere `/path/to/aem/root/test`.

1. Aggiungere helper all’interno del routing SPA.

   * La pagina appena creata non è ancora in grado di eseguire il rendering del contenuto previsto in AEM. Il motivo è che il router prevede un percorso di `/test` considerando che il percorso attivo dell&#39;AEM è `/wknd-spa-react/us/en/test`. Per includere la porzione dell’URL specifica per l’AEM, devi aggiungere alcuni helper sul lato SPA.

   ![Helper di routing](assets/external-spa-router-helper.png)

   * Il `toAEMPath` helper fornito da `@adobe/cq-spa-page-model-manager` possono essere utilizzati. Trasforma il percorso fornito per il routing in modo da includere parti specifiche dell&#39;AEM quando l&#39;applicazione è aperta su un&#39;istanza dell&#39;AEM. Accetta tre parametri:
      * Percorso necessario per il routing
      * URL di origine dell’istanza AEM in cui viene modificato l’SPA
      * Elemento di base del progetto sull’AEM come determinato nella prima fase

   * Questi valori possono essere impostati come variabili di ambiente per maggiore flessibilità.

1. Verifica la modifica della pagina in AEM.

   * Distribuisci il progetto in AEM e passa al nuovo `test` pagina. Ora viene eseguito il rendering del contenuto della pagina e i componenti AEM sono modificabili.

## Limitazioni del framework {#framework-limitations}

Il componente RemotePage prevede che l’implementazione fornisca un manifesto delle risorse come quello [trovato qui](https://github.com/shellscape/webpack-manifest-plugin). Il componente RemotePage, tuttavia, è stato testato per funzionare solo con il framework React (e Next.js tramite il componente remote-page-next ) e pertanto non supporta il caricamento remoto di applicazioni da altri framework, come ad Angular.

## Risorse aggiuntive {#additional-resources}

I seguenti materiali di riferimento possono essere utili per comprendere l&#39;SPA nel contesto dell&#39;AEM.

* [Headful e headless in AEM](/help/implementing/developing/headful-headless.md)
* [L’archetipo del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)
* [Il progetto WKND SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it)
* [Guida introduttiva alle SPA in AEM usando React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Materiali di riferimento SPA (riferimenti API)](/help/implementing/developing/hybrid/reference-materials.md)
* [Blueprint SPA e PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [Routing modello SPA](/help/implementing/developing/hybrid/routing.md)
* [Rendering lato server e SPA](/help/implementing/developing/hybrid/ssr.md)
