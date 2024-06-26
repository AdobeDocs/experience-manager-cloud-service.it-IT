---
title: Registrare una transazione per le implementazioni personalizzate
description: Utilizzare l'API TransactionRecorder per registrare automaticamente le azioni non contabilizzate come transazioni
feature: Adaptive Forms, Foundation Components
exl-id: cb584f78-30af-4a58-be99-843352e8249c
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 16%

---

# Registrare una transazione per le implementazioni personalizzate {#record-a-transaction-for-custom-implementations}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-osgi/record-transaction-custom-implementation) |
| AEM as a Cloud Service | Questo articolo |

Utilizzare l&#39;API TransactionRecorder per registrare automaticamente le azioni che non vengono contabilizzate come transazioni.

Puoi utilizzare un codice personalizzato per inviare un modulo PDF. In alternativa, è possibile inviare un modulo utilizzando metodi personalizzati anziché i metodi di invio forniti con AEM Forms. Tutte le azioni e le implementazioni personalizzate precedentemente menzionate delle API di AEM Forms non vengono contabilizzate come transazioni. AEM Forms fornisce un’API, [TransactionRecorder](https://javadoc.io/doc/com.adobe.aem/aem-forms-sdk-api/latest/com/adobe/aem/transaction/core/ITransactionRecorder.html), per registrare azioni quali le transazioni.

Per registrare una transazione, scrivere il [servlet sling standard](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) e chiama il servlet da un client per registrare una transazione. Puoi chiamare il servlet utilizzando l’AJAX o qualsiasi altro metodo standard.

## Esempio di codice lato server {#sample-server-sided-code}

Puoi utilizzare il codice di esempio seguente per eseguire l’API TransactionRecorder da una classe Java™ utilizzando un bundle OSGi personalizzato.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Esempio di codice lato client {#sample-client-side-code}

Puoi utilizzare il codice di esempio seguente per chiamare il servlet che ha `TransactionRecorder`API.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Articoli correlati {#related-articles}

* [API rapporti di transazioni fatturabili](/help/forms/transaction-reports-billable-apis.md)
