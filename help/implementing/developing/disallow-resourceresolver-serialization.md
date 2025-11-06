---
title: Non consentire la serializzazione di ResourceResolver tramite Sling Model Exporter
description: Non consentire la serializzazione di ResourceResolver tramite Sling Model Exporter
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 5%

---

# Non consentire la serializzazione di ResourceResolver tramite Sling Model Exporter {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

La funzione Sling Model Exporter consente di serializzare gli oggetti del modello Sling in formato JSON. Questa funzione è ampiamente utilizzata in quanto consente alle applicazioni a pagina singola di accedere facilmente ai dati da AEM. Sul lato dell&#39;implementazione, per serializzare questi oggetti viene utilizzata la libreria Jackson Databind.

La serializzazione è un&#39;operazione ricorsiva. Partendo da un &quot;oggetto principale&quot;, esegue l&#39;iterazione ricorsiva in tutti gli oggetti idonei e li serializza insieme ai relativi elementi secondari. È possibile trovare una descrizione dei campi serializzati nell&#39;articolo [Jackson - Decide quali campi vengono serializzati/deserializzati](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Questo approccio serializza tutti i tipi di oggetti in JSON. Naturalmente può anche serializzare un oggetto Sling `ResourceResolver`, se è coperto dalle regole di serializzazione. Si tratta di un problema, in quanto il servizio `ResourceResolver` (e quindi anche l&#39;oggetto del servizio che lo rappresenta) contiene informazioni potenzialmente riservate che non devono essere divulgate. Ad esempio:

* ID utente
* Percorsi di ricerca per risolvere i percorsi relativi
* `propertyMap`

Particolarmente sensibile è `propertyMap` (vedi la documentazione API di [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), in quanto si tratta di una struttura di dati interna che può essere utilizzata per molti scopi, ad esempio per memorizzare in cache oggetti che condividono lo stesso ciclo di vita di `ResourceResolver`. La serializzazione di questi può causare la perdita di dettagli sull’implementazione e potenzialmente avere un impatto sulla sicurezza, in quanto vengono esposti dati che non dovrebbero essere leggibili e accessibili a un utente finale. Per questo motivo `ResourceResolvers` non deve essere serializzato in JSON.

Adobe prevede di disabilitare la serializzazione di `ResourceResolvers` in un approccio in due passaggi:

1. A partire dalla 14697 sulla versione di AEM as a Cloud Service, ogni volta che un `ResourceResolver` viene serializzato, AEM registrerà un messaggio di avviso. Tutti i clienti sono invitati a controllare i registri dell’applicazione per individuare queste istruzioni di registro e ad adattare di conseguenza la base di codice.
1. In seguito Adobe disabiliterà la serializzazione di `ResourceResolver` come JSON.

## Implementazione {#implementation}

Il messaggio WARN viene registrato sia nelle istanze AEM as a Cloud Service che nelle istanze AEM SDK locali ed è simile al seguente:

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Questo messaggio di registro indica che durante il processo di serializzazione di `/content/…/page` in JSON un `ResourceResolver` è già serializzato. Richiedendo `/content/../page.model.json` è possibile verificare esattamente dove vengono visualizzati i campi di `ResourceResolver` e utilizzarli per identificare la classe del modello Sling che attiva effettivamente questo comportamento.


>[!NOTE]
>
>[I componenti core di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/introduction) sono stati convalidati per non essere interessati da questo problema.

## Azione richiesta {#requested-action}

Adobe richiede a tutti i clienti di controllare i registri applicazioni e le basi di codice per verificare se sono interessati da questo problema e di modificare l’applicazione personalizzata, se necessario, in modo che questo messaggio di avviso non venga più visualizzato nei registri.

Si presume che nella maggior parte dei casi le modifiche necessarie siano immediate. Gli oggetti `ResourceResolver` non sono affatto necessari nell&#39;output JSON, poiché le informazioni in essi contenute non sono normalmente richieste dalle applicazioni front-end, il che significa che nella maggior parte dei casi dovrebbe essere sufficiente per escludere l&#39;oggetto `ResourceResolver` dall&#39;essere considerato da Jackson (vedi le [regole](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

Nel caso in cui un modello Sling sia interessato dal problema ma non modificato, la disabilitazione esplicita della serializzazione dell&#39;oggetto `ResourceResolver` (come eseguito da Adobe come secondo passaggio) forzerà una modifica nell&#39;output JSON.
