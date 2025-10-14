---
title: Componenti compositi negli SPA
description: Scopri come creare componenti compositi personalizzati, composti da altri componenti compatibili con l’editor di applicazioni a pagina singola di AEM.
exl-id: fa1ab1dd-9e8e-4e2c-aa9a-5b46ed8a02cb
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---


# Componenti compositi negli SPA {#composite-components-in-spas}

I componenti compositi utilizzano la natura modulare dei componenti di AEM combinando più componenti di base in un singolo componente. Un caso d’uso comune di componente composito è il componente scheda, costituito da una combinazione dei componenti immagine e testo.

Quando i componenti compositi vengono implementati correttamente nel framework dell’Editor applicazioni a pagina singola di AEM, gli autori di contenuto possono trascinare e rilasciare tali componenti come farebbero con qualsiasi altro componente, ma possono comunque modificare singolarmente ogni componente che costituisce il componente composito.

Questo articolo illustra come aggiungere un componente composito all’applicazione a pagina singola per lavorare senza problemi con l’Editor SPA di AEM.

{{ue-over-spa}}

## Caso d’uso {#use-case}

Questo articolo utilizza il componente tipico della scheda come caso d’uso di esempio. Le schede sono un elemento dell’interfaccia utente comune per molte esperienze digitali e sono in genere costituite da un’immagine e dal testo o dalla didascalia associati. L’autore desidera poter trascinare e rilasciare l’intera scheda, ma può modificare singolarmente l’immagine della scheda e personalizzare il testo associato.

## Prerequisiti {#prerequisites}

I seguenti modelli per il supporto dei casi di utilizzo dei componenti compositi richiedono i seguenti prerequisiti.

* L’istanza di sviluppo AEM è in esecuzione localmente sulla porta 4502 con un progetto di esempio.
* Hai un&#39;app React esterna funzionante [abilitata per la modifica in AEM](editing-external-spa.md).
* L&#39;app React è caricata nell&#39;editor di AEM [tramite il componente RemotePage](remote-page.md).

## Aggiunta di componenti compositi a un’applicazione a pagina singola {#adding-composite-components}

Esistono tre modelli diversi per implementare il componente composito a seconda dell’implementazione dell’applicazione a pagina singola in AEM.

* [Il componente non esiste nel progetto AEM](#component-does-not-exist).
* [Il componente è presente nel progetto AEM, ma il contenuto richiesto non lo è](#content-does-not-exist).
* [Il componente e il contenuto richiesto sono entrambi presenti nel progetto AEM](#both-exist).

Le sezioni seguenti forniscono esempi di implementazione di ogni caso utilizzando il componente scheda come esempio.

### Il componente non esiste nel progetto AEM. {#component-does-not-exist}

Inizia creando i componenti che costituiranno il componente composito, ovvero i componenti per l’immagine e il relativo testo.

1. Crea il componente testo nel progetto AEM.
1. Aggiungi il `resourceType` corrispondente dal progetto nel nodo `editConfig` del componente.

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. Utilizza l&#39;helper `withMappable` per abilitare le modifiche per il componente.

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

Il componente testo è simile al seguente.

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

Se si crea un componente immagine in modo simile, è possibile combinarlo con il componente `AEMText` in un nuovo componente scheda, utilizzando i componenti immagine e testo come elementi figlio.

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

Questo componente composito risultante può ora essere posizionato ovunque nell&#39;app e aggiungerà segnaposto per un componente testo e immagine nell&#39;editor di applicazioni a pagina singola. Nell’esempio seguente, il componente scheda viene aggiunto al componente Home sotto il titolo.

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

Nell’editor verrà visualizzato un segnaposto vuoto per un testo e un’immagine. Quando si immettono valori per questi elementi utilizzando l&#39;editor, questi vengono memorizzati nel percorso di pagina specificato, ovvero `/content/wknd-spa/home` a livello principale con i nomi specificati in `itemPath`.

![Componente scheda composita nell&#39;editor](assets/composite-card.png)

### Il componente esiste nel progetto AEM, ma il contenuto richiesto no. {#content-does-not-exist}

In questo caso, il componente scheda è già stato creato nel progetto AEM contenente i nodi titolo e immagine. I nodi secondari (testo e immagine) dispongono dei tipi di risorse corrispondenti.

![Struttura del nodo del componente scheda](assets/composite-node-structure.png)

Puoi quindi aggiungerlo all’applicazione a pagina singola e recuperarne il contenuto.

1. Crea un componente corrispondente nell’applicazione a pagina singola per questo. Assicurati che i componenti secondari siano mappati sui corrispondenti tipi di risorse AEM all’interno del progetto SPA. In questo esempio vengono utilizzati gli stessi componenti `AEMText` e `AEMImage` descritti [&#x200B; nel caso precedente](#component-does-not-exist).

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. Poiché non è presente alcun contenuto per il componente `imagecard`, aggiungi la scheda alla pagina. Includi nell’applicazione a pagina singola il contenitore esistente di AEM.
   * Se nel progetto AEM è già presente un contenitore, possiamo includerlo nell’applicazione a pagina singola e aggiungere invece il componente al contenitore da AEM.
   * Assicurati che il componente scheda sia mappato sul tipo di risorsa corrispondente nell’applicazione a pagina singola.

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. Aggiungi il componente `wknd-spa/components/imagecard` creato ai componenti consentiti per il componente contenitore [&#x200B; nel modello di pagina](/help/sites-cloud/authoring/page-editor/templates.md).

Ora il componente `imagecard` può essere aggiunto direttamente al contenitore nell&#39;editor di AEM.

![Scheda composita nell&#39;editor](assets/composite-card.gif)

### Il componente e il relativo contenuto richiesto sono entrambi presenti nel progetto AEM. {#both-exist}

Se il contenuto esiste in AEM, può essere incluso direttamente nell’applicazione a pagina singola fornendo il percorso del contenuto.

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![Percorso composito nella struttura del nodo](assets/composite-path.png)

Il componente `AEMCard` corrisponde a [&#x200B; definito nel caso d&#39;uso precedente](#content-does-not-exist). In questo caso, il contenuto definito nella posizione precedente nel progetto AEM è incluso nell’applicazione a pagina singola.
