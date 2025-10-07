---
title: Integrare l’API nell’editor di regole per Forms
description: Scopri gli ultimi miglioramenti al servizio Invoke nell’editor di regole, tra cui come integrare le API per Forms adattivo basate su componenti core senza utilizzare un modello di dati modulo.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: integrazione dell’API nell’editor di regole, richiama i miglioramenti del servizio
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: 0dba0003d8b13631e91147fa08c3b986c11b61d3
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 2%

---

# Integrazione dell’API nell’editor di regole

<span>L&#39;integrazione dell&#39;API nell&#39;editor di regole si trova nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, puoi inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal tuo ID e-mail ufficiale.</span>

>[!NOTE]
>
> L&#39;editor di regole visive supporta l&#39;integrazione API in Forms adattivo basato su Componenti core e [Edge Delivery Services Forms creato in Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

L’Editor di regole visive in Forms adattivo supporta l’integrazione API diretta senza creare un modello dati per moduli. Puoi connetterti a un endpoint API immettendo l’URL API (in formato JSON) o importando la configurazione tramite un comando cURL. Una volta integrata, è possibile utilizzare l&#39;azione **Invoke Service** per richiamare l&#39;API.

I campi modulo possono essere mappati direttamente ai parametri di input definiti nella configurazione API. Analogamente, i parametri di output possono essere mappati ai campi modulo utilizzando l&#39;opzione **payload evento** per la risposta API corrispondente.

Inoltre, l&#39;Editor di regole visive consente di definire **success** e **gestori di errori** quando si richiama un servizio. I gestori di operazioni riuscite specificano le azioni da eseguire dopo una chiamata API riuscita, mentre i gestori di operazioni non riuscite definiscono la modalità di risposta del modulo in caso di errore.

## Confronto: Metodi di integrazione API

| Aspetto | Integrazione API con il modello dati del modulo (FDM) | Integrazione API diretta (tramite *Crea integrazione API*) |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **Scopo** | Integrazione API centralizzata e riutilizzabile in più moduli | Integrazione API rapida e specifica per modulo |
| **Percorso installazione** | Creato e modificato nell’Editor modello dati modulo (console AEM) | Creato e modificato direttamente nell’editor di regole per moduli adattivi |
| **Complessità** | Maggiore impegno di configurazione (richiede mappatura e configurazione) | Semplice e leggero |
| **Più Adatto Per** | Casi d’uso aziendali o su larga scala con più moduli | Piccoli moduli, prototipi o chiamate API una tantum |

## Configurazione integrazione API

La schermata seguente mostra la finestra di configurazione dell’integrazione API:

![Configurazione integrazione API](/help/forms/assets/api-integration-configuration.png)

### Opzioni di configurazione chiave

**Configurazione integrazione API**

* **Importa da cURL**: configura l&#39;integrazione API incollando un comando cURL predefinito invece di immettere manualmente dettagli quali URL API, metodo HTTP, intestazioni e parametri.
* **Nome visualizzato**: nome personalizzato per il servizio API.
* **URL API**: endpoint del servizio API.
* **Seleziona metodo HTTP**: metodo di richiesta HTTP utilizzato per chiamare l&#39;API.
* **Tipo di contenuto**: definisce il formato della richiesta e della risposta.
* **Crittografia richiesta**: (facoltativo) assicura che i dati sensibili vengano crittografati durante la trasmissione.
* **Esegui al client**: se abilitata, la chiamata API viene effettuata dal client (browser) anziché dal server.

**Tipo di autenticazione**

* **Opzioni**: nessuna, Base, Chiave API, OAuth 2.0.

**Parametri di input**

* **Carica JSON per l&#39;input**: carica un file JSON di esempio per popolare automaticamente i mapping di input.
   * **Nome**: nome del parametro di input richiesto dall&#39;API.
   * **Tipo**: tipo di dati dell&#39;input (stringa, numero, booleano, ecc.).
   * **In**: posizione del parametro (query, intestazione o corpo).
   * **Valore predefinito**: valore precompilato se non fornito dall&#39;utente.
   * **Aggiungi**: opzione per aggiungere altri parametri di input.

**Parametri di output**

* **Carica JSON per l&#39;output**: carica una risposta API di esempio per generare automaticamente le mappature.
   * **Nome**: restituisce il nome del parametro dalla risposta API.
   * **Tipo**: previsto tipo di dati del parametro di output (stringa, numero e così via).
   * **In**: definisce dove è previsto il valore mappato.
   * **Aggiungi/Elimina**: aggiungi nuovi mapping o rimuovi quelli esistenti.

## Caso d’uso: compilazione dei campi del paese in un modulo di domanda di visto

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**Scenario**: un&#39;agenzia governativa fornisce un modulo di richiesta di visto online con i campi seguenti:

1. Nome e cognome (testo)
2. Data di nascita (data)
3. Paese di cittadinanza (elenco a discesa)
4. Numero di passaporto (testo)
5. Paese di rilascio del passaporto (a discesa)
6. Paese di destinazione (a discesa)
7. Data di arrivo prevista (data)

Invece di mantenere un elenco statico di paesi, il modulo recupera dinamicamente le informazioni sul paese (continente, capitale, codici ISO Alpha, ecc.) utilizzando l&#39;**API getcountry name**:

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

In questo modo i richiedenti potranno sempre visualizzare un elenco aggiornato e accurato dei paesi durante la compilazione del modulo.

### Implementazione tramite l’integrazione API nell’editor di regole

È possibile integrare un&#39;API senza creare un modello dati modulo facendo clic sul pulsante **Crea integrazione API** nell&#39;editor di regole.

![Crea integrazione API](/help/forms/assets/create-api-integration.png)

Un servizio API denominato **getcounname** è configurato in **Configurazione integrazione API** nell&#39;editor regole:

![Configurazione endpoint REST API](/help/forms/assets/api-restendpoint.png)

* **URL endpoint API** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* **Metodo HTTP** → GET
* **Tipo di contenuto** → JSON
* **Input** → `username` passato come parametro di query (`aemforms`).
* **Output** → campi di risposta come `continent`, `capital`, `countrynames`, `isoAlpha3` e `languages` sono mappati a campi modulo.

Nel **modulo per la richiesta di visto**, i tre campi a discesa **Paese di cittadinanza**, **Paese di rilascio del passaporto** e **Paese di destinazione** sono associati all&#39;azione **Richiama servizio**.

Al caricamento del modulo, **Invoke Service** recupera l&#39;elenco dei paesi dall&#39;API. La risposta viene quindi mappata per popolare automaticamente le opzioni a discesa.

Ad esempio, quando l&#39;utente apre **Paese di cittadinanza**, l&#39;elenco dei paesi viene visualizzato in modo dinamico dalla risposta API.

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![Output integrazione API](/help/forms/assets/api-integration-output.png)

Analogamente, **Paese di rilascio Passport** e **Paese di destinazione** utilizzano la stessa chiamata API, garantendo dati coerenti e aggiornati in tutti e tre i campi.

## Implementazione del meccanismo dei tentativi per gli errori API

Quando una richiesta API ha esito negativo, spesso è utile riprovare prima di segnalare un errore all’utente. Puoi implementare un meccanismo di polling e tentativi scrivendo codice personalizzato nel file **function.js**.

L’esempio seguente illustra come gestire gli errori API con un massimo di due tentativi e un backoff esponenziale tra nuovi tentativi:

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

Nel codice riportato sopra, la funzione **retryHandler** gestisce le richieste API con tentativi automatici in caso di errore. Richiede una funzione di richiesta (requestFn) e tenta la richiesta fino a due volte, aggiungendo metadati per ogni nuovo tentativo.

>[!NOTE]
>
> Per i passaggi dettagliati su come aggiungere funzioni personalizzate, consulta l&#39;articolo [Introduzione alle funzioni personalizzate per Forms adattivo basate sui componenti core](/help/forms/create-and-use-custom-functions.md).

## Domande frequenti

* **È necessario creare un modello dati modulo per integrare un&#39;API in Forms adattivo?**\
  No. Con l&#39;Editor di regole visive, è possibile integrare direttamente le API utilizzando l&#39;opzione **Crea integrazione API** senza creare un modello dati modulo. Questo approccio è ideale per i casi d’uso leggeri o specifici di un modulo.

* **È possibile proteggere le chiamate API effettuate dall&#39;editor di regole?**\
  Sì. La configurazione dell&#39;integrazione API fornisce opzioni di autenticazione come **Basic, API Key e OAuth 2.0**. Puoi anche abilitare **Crittografia richiesta** per garantire che i dati sensibili vengano trasmessi in modo sicuro.
