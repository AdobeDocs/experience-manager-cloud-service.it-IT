---
title: Recuperare il contenuto JSON con JavaScript
description: Esplora il recupero del contenuto JSON dall’ambiente di prova con un’app CodePen e il client AEM Headless per JavaScript.
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Recuperare il contenuto JSON con JavaScript {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Recuperare il contenuto JSON con JavaScript"
>abstract="Esplora il recupero del contenuto JSON dall’ambiente di prova con un’app CodePen e il client AEM Headless per JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Avvia l&#39;app di esempio CodePen"
>abstract="Abbiamo creato un&#39;app CodePen minima per introdurre il recupero di dati JSON dall&#39;ambiente di prova utilizzando query GraphQL persistenti.<br><br>Avvia l&#39;esempio di CodePen facendo clic qui sotto, quindi segui questa guida per ulteriori informazioni."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="In questo modulo, hai imparato a utilizzare il client AEM Headless per JavaScript per recuperare dati JSON dal tuo ambiente di prova utilizzando query GraphQL persistenti.<br><br>Ora sai come utilizzare questo client per utilizzare dati dall’interno della tua applicazione web."
>abstract=""

## Introduzione {#intro}

Inizia nell’app CodePen, che funge da esempio minimo di recupero di dati JSON utilizzando [Client AEM headless per JavaScript](https://github.com/adobe/aem-headless-client-js). L’app di esempio è progettata per eseguire il rendering di qualsiasi contenuto JSON restituito, indipendentemente dalla struttura del modello di frammento di contenuto sottostante. L&#39;app CodePen cerca di essere dettagliata con eventuali errori riscontrati, quindi potresti vedere il seguente messaggio di errore stampato nel riquadro inferiore dell&#39;app:

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

Questo errore è previsto, in quanto l’app non è ancora configurata per utilizzare la query persistente salvata e pubblicata in un modulo precedente. Configurerai l’app per recuperare dati dalla query specifica nei passaggi seguenti.

## Procedura dettagliata di CodePen {#code-walkthrough}

Il riquadro JS (Javascript) su CodePen contiene i cervelli dell&#39;app di esempio. A partire dalla riga 2, importiamo il client headless AEM per JavaScript dalla CDN Skypack. Skypack è utilizzato per facilitare lo sviluppo senza un passaggio di compilazione, ma è anche possibile utilizzare il client headless AEM con NPM o Yarn nei propri progetti. Consulta le istruzioni d’uso nella sezione [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) per ulteriori dettagli.

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Alla riga 6 leggiamo i dettagli dell&#39;host di pubblicazione dal `publishHost` parametro query. Questo è l&#39;host da cui il client AEM headless recupererà i dati. In genere questo viene codificato nell’app, ma si utilizza un parametro di query per facilitare il funzionamento dell’app CodePen con ambienti diversi.

Configuriamo il client headless AEM alla riga 12 per utilizzare una funzione IO Runtime di Adobe proxy per evitare problemi CORS. Questo non è necessario per i tuoi progetti, ma è necessario per il funzionamento dell’app CodePen con l’ambiente di prova. La funzione proxy è configurata per l&#39;utilizzo del `publishHost` Valore fornito nel parametro di query.

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

Infine, la funzione `fetchJsonFromGraphQL()` viene utilizzato per eseguire la richiesta di recupero utilizzando il client headless AEM. Viene chiamato ogni volta che il codice viene modificato o può essere attivato premendo il collegamento &quot;Refetch&quot;. L&#39;effettivo `aemHeadlessClient.runPersistedQuery(..)` la chiamata avviene alla riga 34. Un po&#39; più tardi modificheremo il modo in cui i dati JSON vengono sottoposti a rendering, ma per il momento lo stamperemo solo al `#output` div utilizzando `resultToPreTag(queryResult)` funzione .

## Recupera dati dalla query persistente {#use-persisted-query}

Alla riga 25 indichiamo da quale query GraphQL persistente l’app deve recuperare i dati. Il nome della query persistente è una combinazione del nome del progetto (ad es. `your-project`), seguita da una barra rovesciata e quindi dal nome della query.

Aggiorna `persistedQueryName` per utilizzare la query persistente creata nel modulo precedente. Se hai seguito esattamente il suggerimento di denominazione, avresti creato una query persistente denominata `adventures` in `your-project` e impostavi il `persistedQueryName` variabile a `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

Una volta apportata questa modifica, l’app dovrebbe aggiornare automaticamente e stampare la risposta JSON non elaborata dalla query persistente fino alla `#output` div. Se viene visualizzato un messaggio di errore, controlla la console per ulteriori dettagli.

Questo JSON contiene le proprietà esatte necessarie per la tua app? In caso contrario, torna all’ambiente di authoring di AEM, agli strumenti, all’editor delle query di GraphQL (o passa a `/aem/graphiql.html` e apporta modifiche alla query persistente. Non dimenticare di salvare e pubblicare la query una volta completata.

## Modificare il rendering JSON {#change-rendering}

Attualmente, il JSON viene sottoposto a rendering così come è in un `pre` , che non è molto creativo. Possiamo cambiare la nostra CodePen per usare la `resultToDom()` per illustrare invece come è possibile iterare la risposta JSON per creare un risultato più interessante.

Per apportare questa modifica, commenta la riga 37 e rimuovi il commento dalla riga 40:

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

Questa funzione eseguirà anche il rendering di tutte le immagini incluse nella risposta JSON come `img` tag . Se i frammenti di contenuto &quot;Avventura&quot; creati non includono immagini, puoi provare a passare all’utilizzo del `aem-demo-assets/adventures-all` query persistente modificando la riga 25:

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

Questa query genera una risposta JSON che include le immagini e `resultToDom()` La funzione li renderà in linea.

![Risultato della query adventures-all e della funzione di rendering resultToDom](assets/do-not-localize/adventures-all-query-result.png)
