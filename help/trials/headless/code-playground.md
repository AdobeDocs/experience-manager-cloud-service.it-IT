---
title: Rendering dei contenuti in un’app semplice
description: Scopri come recuperare i contenuti JSON dall’ambiente di prova con un’app CodePen e il client AEM Headless per JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 1949ee211b4f816e05aa779deb9e287347f006ad
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 48%

---


# Rendering dei contenuti in un’app semplice {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Eseguire il rendering del contenuto in una semplice app"
>abstract="Scopri come recuperare i contenuti JSON dall’ambiente di prova con un’app CodePen e il client AEM Headless per JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Avvia l&#39;app di esempio CodePen"
>abstract="Questa guida descrive dettagliatamente come eseguire query sui dati JSON dall’ambiente di prova in un’app web JavaScript di base. Useremo i frammenti di contenuto che hai modellato e creato nei moduli di apprendimento precedenti, quindi consulta quelle guide prima di passare a questa."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="In questo modulo, hai imparato a utilizzare il client AEM Headless per JavaScript per recuperare dati JSON dall’ambiente di prova utilizzando query GraphQL persistenti.<br><br>Ora sai come utilizzare questo client per utilizzare i dati dall’interno della tua applicazione web."
>abstract=""

## CodePen {#codepen}

CodePen è un editor di codice online e un parco giochi per lo sviluppo web front-end. Consente di scrivere codice HTML, CSS e JavaScript nel browser e di visualizzare i risultati del lavoro quasi immediatamente. È inoltre possibile salvare il lavoro e condividerlo con altri utenti. Abbiamo creato un&#39;app in CodePen che puoi utilizzare per recuperare i dati JSON dall&#39;ambiente di prova utilizzando [Client AEM headless per JavaScript](https://github.com/adobe/aem-headless-client-js). Puoi utilizzare questa app così com’è, oppure puoi eseguirne il forking nel tuo account CodePen per personalizzarla ulteriormente.

Facendo clic su **Avvia l’app CodePen di esempio** dalla versione di prova ti porterà all’app in CodePen. L’app funge da esempio minimo di recupero dei dati JSON con JavaScript. L’app di esempio è progettata per eseguire il rendering di qualsiasi contenuto JSON restituito, indipendentemente dalla struttura del modello di Frammento di contenuto sottostante. Preconfigurata, l’app recupererà i dati da un `aem-demo-assets` query persistente inclusa nell’ambiente di prova. Dovresti trovare una risposta JSON simile alla seguente:

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

Se invece visualizzi un errore, controlla la console del browser per maggiori dettagli o contatta [allo Slack](https://adobe-dx-support.slack.com).

Ora che sai qualcosa su CodePen, configura l’app per recuperare i dati dalla query persistente creata in un modulo precedente.

## Procedura dettagliata sul codice JavaScript {#code-walkthrough}

Il **JS** Il riquadro a destra in CodePen contiene il codice JavaScript dell&#39;app di esempio. A partire dalla riga 2, il client AEM Headless per JavaScript viene importato dalla CDN Skypack. Skypack è utilizzato per semplificare lo sviluppo senza un passaggio di compilazione, ma nei progetti è possibile anche utilizzare il client AEM Headless con NPM o Yarn. Per ulteriori dettagli, dai un’occhiata alle istruzioni sull’utilizzo nella sezione [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript).

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Sulla riga 6, si leggono i dettagli dell’host di pubblicazione dal parametro query `publishHost`. Questo è l’host da cui il client AEM Headless recupererà i dati. In genere questo viene codificato nell’app, ma viene utilizzato un parametro di query per semplificare il funzionamento dell’app CodePen in ambienti diversi.

Configuriamo il client headless AEM in linea 12:

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>Il **serviceURL** è impostato per utilizzare una funzione proxy di Adobe IO Runtime per evitare problemi CORS. Questo non è necessario per i tuoi progetti, ma lo è per il funzionamento dell’app CodePen nell’ambiente di prova. La funzione proxy è configurata per utilizzare **publishHost** valore fornito nel parametro di query.

Infine, la funzione `fetchJsonFromGraphQL()` viene utilizzata per eseguire la richiesta di recupero utilizzando il client AEM Headless. Viene richiamato ogni volta che il codice viene modificato o può essere attivato facendo clic sul pulsante **Recupera nuovamente** collegamento. La chiamata `aemHeadlessClient.runPersistedQuery(..)` effettiva avviene alla riga 34. In seguito, il modo in cui i dati JSON vengono renderizzati verrà cambiato, ma per il momento verrà stampato solo nell’elemento div `#output` utilizzando la funzione `resultToPreTag(queryResult)`.

## Recuperare dati dalla query persistente {#use-persisted-query}

Sulla riga 25, viene indicato da quale query GraphQL persistente l’app deve recuperare i dati. Il nome della query persistente è una combinazione del nome dell’endpoint (ad esempio. `your-project` o `aem-demo-assets`), seguito da una barra e quindi dal nome della query. Se hai seguito esattamente le istruzioni del modulo precedente, la query persistente creata si troverà nel `your-project` endpoint.

1. Aggiorna la variabile `persistedQueryName` per utilizzare la query persistente creata nel modulo precedente. Se hai seguito il suggerimento di denominazione, avresti creato una query persistente denominata `adventure-list` nel `your-project` e si imposta il `persistedQueryName` variabile a `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Una volta apportata questa modifica, l’app dovrebbe aggiornare automaticamente e stampare la risposta JSON non elaborata dalla query persistente fino all’elemento div `#output`. Se viene visualizzato un messaggio di errore, verifica la console per ulteriori dettagli. Uscita portata [allo Slack](https://adobe-dx-support.slack.com) se hai ancora problemi con questo passaggio.

1. Questo JSON contiene le proprietà esatte necessarie per la tua app? In caso contrario, tornare al [Estrarre contenuti utilizzando l’API di GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) guida di apprendimento per apportare modifiche. Al termine, non dimenticare di salvare e pubblicare la query.

## Modificare il rendering JSON {#change-rendering}

Il JSON viene riprodotto così com’è in una `pre` , che non è molto creativo. La CodePen può essere cambiata per utilizzare invece la funzione `resultToDom()` per illustrare come è possibile iterare la risposta JSON per creare un risultato più interessante.

1. Per apportare questa modifica, commenta la riga 37 e rimuovi il commento dalla riga 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Questa funzione eseguirà anche il rendering di tutte le immagini incluse nella risposta JSON come tag `img`. Se il **Avventura** i frammenti di contenuto creati non includono immagini. puoi provare a utilizzare la `aem-demo-assets/adventures-all` query persistente modificando la riga 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Questa query produrrà una risposta JSON che include le immagini e la funzione `resultToDom()` li renderizzerà in linea.

![Risultato della query adventures-all e della funzione di rendering resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Dopo aver creato i modelli e le query, il team dei contenuti può assumere il controllo con facilità. Nel prossimo modulo verrà mostrato il flusso di authoring dei contenuti.
