---
title: Come si utilizzano le chiamate di funzioni asincrone nell’Editor di regole visive?
description: Chiamate di funzione asincrone nell’editor di regole visive
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Utilizzo di funzioni asincrone in un modulo adattivo basato su componenti core

L&#39;editor di regole [in Adaptive Forms](/help/forms/rule-editor-core-components.md) supporta funzioni asincrone, consentendo di integrare e gestire le operazioni che richiedono l&#39;attesa di processi esterni o il recupero dei dati senza interrompere l&#39;interazione dell&#39;utente con il modulo.

## Quali fattori determinano l&#39;uso di funzioni asincrone o sincrone?

Gestire l’interazione dell’utente in modo efficace è fondamentale per creare un’esperienza fluida. Due approcci comuni per la gestione delle operazioni sono le funzioni sincrone e asincrone.

**Le funzioni sincrone** eseguono attività una dopo l&#39;altra, facendo in modo che l&#39;applicazione attenda il completamento di ogni operazione prima di procedere. Questo può portare a ritardi e a un’esperienza utente meno coinvolgente, soprattutto quando le attività richiedono l’attesa di risorse esterne, come il caricamento di file o il recupero di dati.

Ad esempio, si consideri uno scenario in cui un utente carica un’immagine, l’intero modulo si interrompe, in attesa del completamento del caricamento. Questa pausa impedisce all’utente di interagire con altri campi, causando frustrazione e ritardi. In attesa che l’immagine venga elaborata, qualsiasi informazione immessa potrebbe andare persa se il visitatore si allontana o perde la pazienza, rendendo l’esperienza difficile e inefficiente.

**Le funzioni asincrone**, invece, consentono l&#39;esecuzione simultanea di attività. Ciò significa che gli utenti possono continuare a interagire con l’applicazione durante l’esecuzione dei processi in background. Le operazioni asincrone migliorano la reattività, consentendo agli utenti di ricevere feedback immediati e mantenere il coinvolgimento senza interruzioni.

Al contrario, con un approccio asincrono, gli utenti possono caricare immagini in background continuando a compilare il resto del modulo senza problemi. L’interfaccia rimane reattiva e consente aggiornamenti in tempo reale e feedback immediati man mano che il caricamento procede. Migliora il coinvolgimento degli utenti, garantendo un’esperienza fluida senza interruzioni.

![Funzioni asincrone e sincrone](/help/forms/assets/sync-async.png){align=center}

## Implementazione di funzioni asincrone per Forms adattivo

Puoi implementare le funzioni asincrone per Adaptive Forms utilizzando i seguenti tipi di regole nell’editor di regole:

* [Chiamata funzione asincrona](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [Uscita funzione](#how-to-use-function-output-rule-type)

## Come si utilizza il tipo di regola Chiamata funzione asincrona?

È possibile scrivere le [funzioni personalizzate](/help/forms/custom-function-core-component-create-function.md) per le operazioni asincrone e configurare le funzioni asincrone utilizzando il tipo di regola **[!UICONTROL Chiamata funzione asincrona]** nell&#39;editor di regole.

### Esplorazione del tipo di regola della chiamata di funzione asincrona tramite un caso d’uso

Considerare un modulo di registrazione su un sito Web in cui gli utenti immettono una password monouso (OTP). Il pannello per l’aggiunta dei dettagli utente viene visualizzato solo dopo l’immissione dell’OTP corretto. Se OTP non è corretto, il pannello rimane nascosto e sullo schermo viene visualizzato un messaggio di errore.

![Modulo di accesso](/help/forms/assets/rule-editor-login-form.png) {width-50%}

In un modulo di registrazione, quando l&#39;utente fa clic sul pulsante **Conferma**, la funzione `matchOTP()` viene chiamata in modo asincrono per verificare l&#39;OTP immesso. La funzione `matchOTP()` è implementata come [funzione personalizzata](/help/forms/custom-function-core-component-create-function.md). Utilizzando il tipo di regola **[!UICONTROL Chiamata funzione asincrona]** nell&#39;editor di regole, puoi configurare la funzione `matchOTP()` nell&#39;editor di regole di un modulo adattivo. Puoi anche implementare i callback di esito positivo e negativo nell’editor di regole.

La figura seguente illustra i passaggi per utilizzare il tipo di regola **[!UICONTROL Chiamata funzione asincrona]** per richiamare funzioni asincrone per Forms adattivo:

![Flusso di lavoro per aggiungere funzioni asincrone](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. Scrivere una funzione personalizzata per l’operazione asincrona nel file JS

>[!NOTE]
>
> * Quando si seleziona il tipo di regola **Chiamata funzione asincrona**, nell&#39;editor di regole di un modulo vengono visualizzate solo le funzioni con tipo restituito `Promise`.
> * Per informazioni su come creare una funzione personalizzata, consulta l&#39;articolo [Creare una funzione personalizzata per un modulo adattivo basato su componenti core](/help/forms/custom-function-core-component-create-function.md).

La funzione `matchOTP()` è implementata come funzione personalizzata. Il codice seguente viene aggiunto al file JS della funzione personalizzata:

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

Il codice definisce una funzione `matchOTP()` che genera una promessa di convalida di una password monouso (OTP) in modo asincrono. Utilizza una funzione `asyncOperationForOTPMatch()` per simulare il processo di corrispondenza OTP. La funzione controlla se l&#39;OTP fornito è uguale a `111`. Se l&#39;OTP immesso è corretto, chiama il callback con null per l&#39;errore e un oggetto che indica che l&#39;OTP è valido `({'valid':'true'})`. Se l&#39;OTP non è valido, chiama il callback con un oggetto errore `({'valid':'false'})` e null per il risultato.

### 2. Configurare la funzione asincrona nell’editor di regole

Per configurare la funzione asincrona nell’editor di regole, effettua le seguenti operazioni:

1. [Creare una regola per utilizzare la funzione asincrona utilizzando il tipo di regola di chiamata della funzione asincrona](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [Implementare i callback per la funzione asincrona](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 Creare una regola per utilizzare la funzione asincrona utilizzando il tipo di regola di chiamata della funzione asincrona

Per creare una regola per l&#39;utilizzo di un&#39;operazione asincrona, utilizzare il tipo di regola **[!UICONTROL Chiamata funzione asincrona]**, eseguire la procedura seguente:

1. Apri un modulo adattivo in modalità di creazione, seleziona un componente modulo e seleziona **[!UICONTROL Editor regole]** per aprire l&#39;editor regole.
1. Seleziona **[!UICONTROL Crea]**.
1. Crea una condizione nella sezione **When** della regola per fare clic su un pulsante. Ad esempio, **Quando[Conferma]** è selezionato.
1. Nella sezione **Then**, seleziona **[!UICONTROL Chiamata funzione asincrona]** dall&#39;elenco a discesa **Seleziona azione**.
Quando si seleziona **[!UICONTROL Chiamata funzione asincrona]** e vengono visualizzate le funzioni con il tipo restituito `Promise`.
1. Seleziona la funzione asincrona dall’elenco. Ad esempio, selezionare la funzione `matchOTP()` e i relativi callback come `Add success callback` e `add failure callback`.
1. Selezionare ora le associazioni **[!UICONTROL Input]**. Selezionare ad esempio **[!UICONTROL Input]** come `Form Object` e confrontarlo con il campo `OTP`.

La schermata seguente mostra la regola:

![tipo di regola](/help/forms/assets/asyn-function-rule-type.png)

Ora è possibile procedere con l&#39;implementazione dei callback: `Success` e `Failure` per la funzione `matchOTP`.

#### 2.2 Implementare i callback per la funzione asincrona

Implementa i metodi di callback di esito positivo e negativo per la funzione asincrona utilizzando l’editor di regole visive.

**Crea una regola per il metodo `Add Success callback`**

Creiamo una regola per visualizzare il pannello `userdetails`, se l&#39;OTP corrisponde al valore `111`.

1. Fai clic su **[!UICONTROL Aggiungi callback di successo]**.
1. Fai clic su **[!UICONTROL Aggiungi istruzione]** per creare la regola.
1. Crea una condizione nella sezione **When** della regola.
1. Selezionare **[!UICONTROL Output funzione]** > **[!UICONTROL Ottieni payload evento]**.

   >[!NOTE]
   >
   > La funzione **[!UICONTROL Get Event Payload]** recupera i dati associati a un evento specifico per gestire dinamicamente le interazioni utente.

1. Seleziona le associazioni corrispondenti dalla sezione **Input**. Selezionare ad esempio **[!UICONTROL Stringa]** e immettere `valid`. Confrontare la stringa immessa con `true`.
1. Nella sezione **Then**, seleziona **[!UICONTROL Show]** dall&#39;elenco a discesa **Select Action**. Mostra ad esempio il pannello `userdetails`.
1. Fare clic su **[!UICONTROL Aggiungi istruzione]**.
1. Seleziona **[!UICONTROL Nascondi]** dall&#39;elenco a discesa **Seleziona azione**. Nascondere ad esempio la casella di testo `error message`.
1. Fai clic su **[!UICONTROL Fine]**.

![Chiamata riuscita](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

Fare riferimento alla schermata seguente, in cui l&#39;utente immette OTP come `111` e il pannello `User Details` viene visualizzato quando si fa clic sul pulsante `Confirm`.

![Operazione completata](/help/forms/assets/success.gif)

**Crea una regola per il metodo `Add Failure callback`**

Creiamo una regola per visualizzare un messaggio di errore se il valore OTP non corrisponde a `111`.

1. Fare clic su **[!UICONTROL Aggiungi callback di errore]**.

1. Fai clic su **[!UICONTROL Aggiungi istruzione]** per creare la regola.
1. Crea una condizione nella sezione **When** della regola.
1. Selezionare **[!UICONTROL Output funzione]** > **[!UICONTROL Ottieni payload evento]**.
1. Seleziona le associazioni corrispondenti dalla sezione **Input**. Selezionare ad esempio **[!UICONTROL Stringa]** e immettere `valid`. Confrontare la stringa immessa con `false`.
1. Nella sezione **Then**, seleziona **[!UICONTROL Show]** dall&#39;elenco a discesa **Select Action**. Visualizzare ad esempio la casella di testo `error message`.
1. Fare clic su **[!UICONTROL Aggiungi istruzione]**.
1. Seleziona **[!UICONTROL Nascondi]** dall&#39;elenco a discesa **Seleziona azione**. Ad esempio, nascondi il pannello `userdetails`.
1. Fai clic su **[!UICONTROL Fine]**.

![Metodo di callback di errore](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

Fare riferimento alla schermata seguente, in cui l&#39;utente immette OTP come `123` e il messaggio di errore viene visualizzato quando si fa clic sul pulsante `Confirm`.

![Errore](/help/forms/assets/failure.gif)

La schermata seguente mostra la regola completa per l&#39;utilizzo di **[!UICONTROL Chiamata funzione asincrona]** per implementare una funzione asincrona:

![Regola per chiamata funzione asincrona](/help/forms/assets/rule-editor-async-callbacks.png)

Puoi anche modificare i callback facendo clic su **[!UICONTROL Modifica callback riuscito]** e **[!UICONTROL Modifica callback non riuscito]**.

## Come si utilizza il tipo di regola Output funzione?

È inoltre possibile chiamare le funzioni asincrone indirettamente utilizzando le funzioni sincrone. Le funzioni sincrone vengono eseguite utilizzando il tipo di regola **[!UICONTROL Output funzione]** nell&#39;editor di regole di un modulo adattivo.

Osservare il codice seguente per vedere come richiamare funzioni asincrone utilizzando il tipo di regola **[!UICONTROL Output funzione]**:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

Nell&#39;esempio precedente, la funzione asyncFunction è un `asynchronous function`. Esegue un&#39;operazione asincrona effettuando una richiesta `GET` a `https://petstore.swagger.io/v2/store/inventory`. Attende la risposta utilizzando `await`, analizza il corpo della risposta come JSON utilizzando `response.json()`, quindi restituisce i dati. La funzione `callAsyncFunction` è una funzione personalizzata sincrona che richiama la funzione `asyncFunction` e visualizza i dati di risposta nella console. Sebbene la funzione `callAsyncFunction` sia sincrona, chiama la funzione asyncFunction asincrona e gestisce il risultato con `then` e `catch` istruzioni.

Per vedere come funziona, aggiungiamo un pulsante e creiamo una regola per il pulsante che richiama la funzione asincrona al clic di un pulsante.

![creazione regola per funzione asincrona](/help/forms/assets/rule-for-async-funct.png){width=50%}

Fare riferimento alla schermata della finestra della console seguente per dimostrare che quando l&#39;utente fa clic sul pulsante `Fetch`, viene richiamata la funzione personalizzata `callAsyncFunction`, che a sua volta chiama una funzione asincrona `asyncFunction`. Ispeziona la finestra della console per visualizzare la risposta al clic del pulsante:

![Finestra della console](/help/forms/assets/async-custom-funct-console.png)

## Consulta anche

{{see-also-rule-editor}}
