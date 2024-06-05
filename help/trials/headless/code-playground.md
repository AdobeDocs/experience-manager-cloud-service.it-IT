---
title: Eseguire il rendering del contenuto in un’app semplice
description: Scopri come recuperare i contenuti JSON dall’ambiente di prova con un’app CodePen di esempio e il client AEM Headless per JavaScript.
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 100%

---


# Eseguire il rendering del contenuto in un’app semplice {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="Eseguire il rendering del contenuto in un’app semplice"
>abstract="Scopri come recuperare i contenuti JSON dall’ambiente di prova con un’app CodePen di esempio e il client AEM Headless per JavaScript."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="Avvia l’app CodePen di esempio"
>abstract="Questa guida descrive come eseguire query sui dati JSON dall’ambiente di prova in un’app web JavaScript di base. Puoi utilizzare i Frammenti di contenuto che hai creato e modellato nei moduli di apprendimento precedenti. Se necessario, consulta quelle guide prima di passare a questa."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="In questo modulo, hai imparato a utilizzare il client AEM Headless per JavaScript per recuperare dati JSON dall’ambiente di prova utilizzando query GraphQL persistenti.<br><br>Ora sai come utilizzare questo client per utilizzare i dati dall’interno della tua applicazione web."
>abstract=""

## CodePen {#codepen}

CodePen è un editor di codice online con un ambiente playground per lo sviluppo web front-end. Consente di scrivere codice HTML, CSS e JavaScript nel browser e vedere i risultati quasi all’istante. Puoi anche salvare il lavoro e condividerlo. È stata creata un’app in CodePen da usare per recuperare dati JSON dall’ambiente di prova utilizzando il [client AEM headless per JavaScript](https://github.com/adobe/aem-headless-client-js). Puoi utilizzare questa app così com’è o inserirla nel tuo account CodePen per personalizzarla ulteriormente.

Facendo clic sul pulsante **Avvia l’app CodePen di esempio** dalla versione di prova, passerai all’app in CodePen. L’app funge da esempio minimo per il recupero di dati JSON con JavaScript. L’app di esempio è progettata per eseguire il rendering di qualsiasi contenuto JSON restituito, indipendentemente dalla struttura del modello di frammento di contenuto sottostante. Così com’è, l’app recupererà i dati da una query `aem-demo-assets` persistente inclusa nell’ambiente di prova. Dovresti vedere una risposta JSON simile alla seguente:

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

Se invece visualizzi un errore, controlla la console del browser per ulteriori dettagli o contattaci Se invece visualizzi un errore, controlla la console del browser per ulteriori dettagli o contattaci [via e-mail](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request).

Ora che conosci qualcosa di CodePen, puoi configurare l’app per recuperare i dati dalla query persistente creata in un modulo precedente.

## Descrizione dettagliata del codice JavaScript {#code-walkthrough}

Il pannello **JS** a destra in CodePen contiene il codice JavaScript dell’app di esempio. A partire dalla riga 2, il client AEM headless per JavaScript viene importato dalla CDN Skypack. Skypack è utilizzato per semplificare lo sviluppo senza un passaggio di compilazione, ma nei progetti è possibile anche utilizzare il client AEM Headless con NPM o Yarn. Per ulteriori dettagli, dai un’occhiata alle istruzioni sull’utilizzo nella sezione [README](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript).

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

Nella riga 6, i dettagli dell’host di pubblicazione sono stati letti dal parametro di query `publishHost`. Questo parametro è l’host da cui il client headless AEM recupera i dati. In genere questa funzionalità viene codificata nell’app, ma viene utilizzato un parametro di query per semplificare il funzionamento dell’app CodePen in ambienti diversi.

Configura il client AEM headless alla riga 12:

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
>**serviceURL** è impostato per utilizzare una funzione Adobe I/O Runtime proxy per evitare problemi CORS. Questo non è necessario per i tuoi progetti, ma lo è per il funzionamento dell’app CodePen nell’ambiente di prova. La funzione proxy è configurata per utilizzare il valore **publishHost** fornito nel parametro di query.

Infine, la funzione `fetchJsonFromGraphQL()` viene utilizzata per eseguire la richiesta di recupero utilizzando il client AEM Headless. Viene richiamata ogni volta che il codice viene modificato oppure può essere attivata premendo il collegamento **Recupera di nuovo**. La chiamata `aemHeadlessClient.runPersistedQuery(..)` effettiva avviene alla riga 34. In seguito, il modo in cui i dati JSON vengono renderizzati verrà cambiato, ma per il momento verrà stampato solo nell’elemento div `#output` utilizzando la funzione `resultToPreTag(queryResult)`.

## Recuperare i dati dalla query persistente {#use-persisted-query}

Alla riga 25, viene indicato da quale query GraphQL persistente l’app deve recuperare i dati. Il nome della query persistente è una combinazione del nome dell’endpoint (ovvero `your-project` o `aem-demo-assets`), seguito da una barra e quindi dal nome della query. Se hai seguito esattamente le istruzioni del modulo precedente, la query persistente creata sarà nell’endpoint `your-project`.

1. Aggiorna la variabile `persistedQueryName` per utilizzare la query persistente creata nel modulo precedente. Se hai seguito esattamente il suggerimento per la denominazione, dovresti aver creato una query persistente denominata `adventure-list` nell’endpoint `your-project` e impostato la variabile `persistedQueryName` su `your-project/adventure-list`:

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. Una volta apportata questa modifica, l’app dovrebbe aggiornarsi automaticamente e stampare la risposta JSON non elaborata dalla query persistente all’elemento div `#output`. Se viene visualizzato un messaggio di errore, verifica la console per ulteriori dettagli. Se hai ancora problemi con questo passaggio, contattaci [via e-mail](mailto:aem-headless-trials-support@adobe.com?subject=AEM%20Trials%20support%20request).

1. Questo codice JSON contiene le proprietà esatte necessarie per la tua app? In caso contrario, torna alla guida di apprendimento [Estrarre contenuto utilizzando l’API GraphQL](https://experience.adobe.com/it/experiencemanager/learn/extract_content_using_graphql) per apportare modifiche. Al termine, non dimenticare di salvare e pubblicare la query.

## Modificare il rendering JSON {#change-rendering}

Attualmente, il codice JSON viene renderizzato così com’è in un tag `pre`, ma non è un modo molto creativo. La CodePen può essere cambiata per utilizzare invece la funzione `resultToDom()` per illustrare come è possibile iterare la risposta JSON per creare un risultato più interessante.

1. Per apportare questa modifica, commenta la riga 37 e rimuovi il commento dalla riga 40:

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. Questa funzione eseguirà anche il rendering di tutte le immagini incluse nella risposta JSON come tag `img`. Se i frammenti di contenuto **Adventure** creati non includono immagini, puoi provare a usare la query persistente `aem-demo-assets/adventures-all` modificando la riga 25:

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

Questa query produce una risposta JSON che include le immagini e la funzione `resultToDom()` li renderizza in linea.

![Risultato della query adventures-all e della funzione di rendering resultToDom](assets/do-not-localize/adventures-all-query-result.png)

Ora che hai creato modelli e query, il tuo team addetto ai contenuti può procedere con il lavoro. Nel modulo successivo viene mostrato il flusso dell’autore di contenuto.
