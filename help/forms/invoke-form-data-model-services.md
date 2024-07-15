---
title: Come richiamare il servizio Form Data Model (FDM) da Adaptive Forms utilizzando le API?
description: Spiega l’API invokeWebServices che è possibile utilizzare per richiamare i servizi web scritti in WSDL dall’interno di un campo Modulo adattivo.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# API per richiamare il servizio Form Data Model (FDM) da Adaptive Forms {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Panoramica {#overview}

[!DNL AEM Forms] consente agli autori dei moduli di semplificare e migliorare ulteriormente l&#39;esperienza di compilazione dei moduli richiamando i servizi configurati in un modello di dati modulo (FDM) dall&#39;interno di un campo Modulo adattivo. Per richiamare un servizio del modello dati, è possibile creare una regola nell&#39;editor visivo o specificare un JavaScript utilizzando l&#39;API `guidelib.dataIntegrationUtils.executeOperation` nell&#39;editor di codice dell&#39;[editor di regole](rule-editor.md).

Questo documento si concentra sulla scrittura di un JavaScript utilizzando l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare un servizio.

## Utilizzo dell’API {#using-the-api}

L&#39;API `guidelib.dataIntegrationUtils.executeOperation` richiama un servizio dall&#39;interno di un campo Modulo adattivo. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La struttura dell&#39;API `guidelib.dataIntegrationUtils.executeOperation` specifica i dettagli sull&#39;operazione del servizio. La sintassi della struttura è la seguente.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

La struttura API specifica i dettagli seguenti sull’operazione del servizio.

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Struttura per specificare l'identificatore del modello dati modulo, il titolo dell'operazione e il nome dell'operazione</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Specifica il percorso dell'archivio del modello dati modulo (FDM), incluso il nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Specifica il nome dell'operazione di servizio da eseguire</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Esegue il mapping di uno o più oggetti modulo agli argomenti di input per l'operazione di servizio</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Esegue il mapping di uno o più oggetti modulo ai valori di output dell'operazione del servizio per compilare i campi modulo<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Restituisce valori in base agli argomenti di input per l'operazione di servizio. Si tratta di un parametro facoltativo utilizzato come funzione di callback.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visualizza un messaggio di errore se la funzione di callback di successo non visualizza i valori di output in base agli argomenti di input. Si tratta di un parametro facoltativo utilizzato come funzione di callback.<br /> </td>
  </tr>
 </tbody>
</table>

## Script di esempio per richiamare un servizio {#sample-script-to-invoke-a-service}

Lo script di esempio seguente utilizza l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare l&#39;operazione del servizio `getAccountById` configurata nel modello dati del modulo `employeeAccount`.

L&#39;operazione `getAccountById` utilizza il valore nel campo modulo `employeeID` come input per l&#39;argomento `empId` e restituisce il nome del dipendente, il numero di conto e il saldo del conto per il dipendente corrispondente. I valori di output vengono compilati nei campi modulo specificati. Ad esempio, il valore nell&#39;argomento `name` viene popolato nell&#39;elemento modulo `fullName` e il valore per l&#39;argomento `accountNumber` nell&#39;elemento modulo `account`.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Utilizzo dell’API con la funzione di callback {#using-the-api-callback}

È inoltre possibile richiamare il servizio Modello dati modulo utilizzando l&#39;API `guidelib.dataIntegrationUtils.executeOperation` con una funzione di callback. La sintassi API è la seguente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La funzione di richiamata può avere `success` e `failure` funzioni di richiamata.

### Script di esempio con funzioni di callback riuscite e non riuscite {#callback-function-success-failure}

Lo script di esempio seguente utilizza l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per richiamare l&#39;operazione del servizio `GETOrder` configurata nel modello dati del modulo `employeeOrder`.

L&#39;operazione `GETOrder` accetta il valore nel campo modulo `Order ID` come input per l&#39;argomento `orderId` e restituisce il valore della quantità dell&#39;ordine nella funzione di callback `success`.  Se la funzione di callback `success` non restituisce la quantità dell&#39;ordine, la funzione di callback `failure` visualizza il messaggio `Error occured`.

>[!NOTE]
>
> Se si utilizza la funzione di callback `success`, i valori di output non vengono inseriti nei campi modulo specificati.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
