---
title: Eseguire il rendering del contenuto in un’app semplice
description: Scopri come recuperare i contenuti JSON dall’ambiente di prova con un’app CodePen e il client AEM Headless per JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 1949ee211b4f816e05aa779deb9e287347f006ad
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 48%

---


# Eseguire il rendering del contenuto in un’app semplice {#render-content-simple-app}

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

CodePen è un editor di codice online e un parco giochi per lo sviluppo web front-end. Ti consente di scrivere codice HTML, CSS e JavaScript nel browser e visualizzare i risultati del tuo lavoro quasi istantaneamente. Puoi anche salvare il tuo lavoro e condividerlo con altri. È stata creata un’app in CodePen da usare per recuperare dati JSON dall’ambiente di prova utilizzando [Client AEM headless per JavaScript](https://github.com/adobe/aem-headless-client-js). Puoi utilizzare questa app così com&#39;è o inserirla nel tuo account CodePen per personalizzare ulteriormente.

Fai clic su **Avvia l&#39;app di esempio CodePen** dalla versione di prova passerai all’app in CodePen. L’app funge da esempio minimo di recupero di dati JSON con JavaScript. L’app di esempio è progettata per eseguire il rendering di qualsiasi contenuto JSON restituito, indipendentemente dalla struttura del modello di frammento di contenuto sottostante. Predefinito, l’app recupererà i dati da un `aem-demo-assets` query persistente inclusa nell&#39;ambiente di prova. Dovresti vedere una risposta JSON simile alla seguente:

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

Se viene visualizzato un errore, controlla la console del browser per ulteriori dettagli o contatta l’utente [su Slack](https://adobe-dx-support.slack.com).

Ora che sai qualcosa di CodePen, configurerai l’app per recuperare i dati dalla query persistente creata in un modulo precedente.

## Procedura dettagliata sul codice JavaScript {#code-walkthrough}

La **JS** Il riquadro a destra in CodePen contiene il codice JavaScript dell&#39;app di esempio. A partire dalla riga 2, il client AEM Headless per JavaScript viene importato dalla CDN Skypack. Skypack è utilizzato per semplificare lo sviluppo senza un passaggio di compilazione, ma nei progetti è possibile anche utilizzare il client AEM Headless con NPM o Yarn. Per ulteriori dettagli, dai un’occhiata alle istruzioni sull’utilizzo nella sezione [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript).

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Sulla riga 6, si leggono i dettagli dell’host di pubblicazione dal parametro query `publishHost`. Questo è l’host da cui il client AEM Headless recupererà i dati. In genere questo viene codificato nell’app, ma viene utilizzato un parametro di query per semplificare il funzionamento dell’app CodePen in ambienti diversi.

Configuriamo il client headless AEM alla riga 12:

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
>La **serviceURL** è impostato per utilizzare una funzione IO Runtime di Adobe proxy per evitare problemi CORS. Questo non è necessario per i tuoi progetti, ma lo è per il funzionamento dell’app CodePen nell’ambiente di prova. La funzione proxy è configurata per l&#39;utilizzo del **publishHost** Valore fornito nel parametro di query.

Infine, la funzione `fetchJsonFromGraphQL()` viene utilizzata per eseguire la richiesta di recupero utilizzando il client AEM Headless. Viene chiamato ogni volta che il codice viene modificato o può essere attivato facendo clic sul pulsante **Recupero** link. La chiamata `aemHeadlessClient.runPersistedQuery(..)` effettiva avviene alla riga 34. In seguito, il modo in cui i dati JSON vengono renderizzati verrà cambiato, ma per il momento verrà stampato solo nell’elemento div `#output` utilizzando la funzione `resultToPreTag(queryResult)`.

## Recupera dati dalla query persistente {#use-persisted-query}

Sulla riga 25, viene indicato da quale query GraphQL persistente l’app deve recuperare i dati. Il nome della query persistente è una combinazione del nome dell’endpoint (ad esempio. `your-project` o `aem-demo-assets`), seguita da una barra rovesciata e quindi dal nome della query. Se hai seguito esattamente le istruzioni del modulo precedente, la query persistente creata sarà `your-project` punto finale.

1. Aggiorna la variabile `persistedQueryName` per utilizzare la query persistente creata nel modulo precedente. Se hai seguito il suggerimento di denominazione, avresti creato una query persistente denominata `adventure-list` in `your-project` e si imposta l&#39;endpoint `persistedQueryName` variabile a `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Una volta apportata questa modifica, l’app dovrebbe aggiornare automaticamente e stampare la risposta JSON non elaborata dalla query persistente fino all’elemento div `#output`. Se viene visualizzato un messaggio di errore, verifica la console per ulteriori dettagli. Raggiungi [su Slack](https://adobe-dx-support.slack.com) se hai ancora problemi con questo passaggio.

1. Questo JSON contiene le proprietà esatte necessarie per la tua app? In caso contrario, torna al [Estrarre contenuto utilizzando l’API di GraphQL](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql) guida all’apprendimento per apportare modifiche. Non dimenticare di salvare e pubblicare la query una volta completata.

## Modificare il rendering JSON {#change-rendering}

Il JSON viene rappresentato così come è in un `pre` , che non è molto creativo. La CodePen può essere cambiata per utilizzare invece la funzione `resultToDom()` per illustrare come è possibile iterare la risposta JSON per creare un risultato più interessante.

1. Per apportare questa modifica, commenta la riga 37 e rimuovi il commento dalla riga 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Questa funzione eseguirà anche il rendering di tutte le immagini incluse nella risposta JSON come tag `img`. Se la **Avventura** i frammenti di contenuto creati non includono immagini, puoi provare a passare a `aem-demo-assets/adventures-all` query persistente modificando la riga 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Questa query produrrà una risposta JSON che include le immagini e la funzione `resultToDom()` li renderizzerà in linea.

![Risultato della query adventures-all e della funzione di rendering resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Ora che hai fatto il lavoro per creare modelli e query, il tuo team di contenuti può prendere il sopravvento con facilità. Verrà mostrato il flusso dell’autore del contenuto nel modulo successivo.
