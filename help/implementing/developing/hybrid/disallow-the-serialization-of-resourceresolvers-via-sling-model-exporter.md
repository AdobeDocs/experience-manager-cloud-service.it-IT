---
title: Non consentire la serializzazione di ResourceResolver tramite Sling Model Exporter
description: Non consentire la serializzazione di ResourceResolver tramite Sling Model Exporter
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 5%

---

# Non consentire la serializzazione di ResourceResolver tramite Sling Model Exporter {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

La funzione Sling Model Exporter consente di serializzare gli oggetti Sling Models in formato JSON. Questa funzione è ampiamente utilizzata in quanto consente all’SPA (applicazioni a pagina singola) di accedere facilmente ai dati dell’AEM. Sul lato dell’implementazione, per serializzare questi oggetti viene utilizzata la libreria Jacson Databind.

La serializzazione è un&#39;operazione ricorsiva. Partendo da un &quot;oggetto principale&quot;, esegue un&#39;iterazione ricorsiva in tutti gli oggetti idonei e serializza questi e i relativi elementi secondari. È possibile trovare una descrizione dei campi serializzati nell&#39;articolo [Jackson - Decide quali campi vengono serializzati/deserializzati](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Questo approccio serializza tutti i tipi di oggetti in JSON e naturalmente può anche serializzare un oggetto Sling `ResourceResolver`, se è coperto dalle regole di serializzazione. Si tratta di un problema, in quanto il servizio `ResourceResolver` (e quindi anche l&#39;oggetto del servizio che lo rappresenta) contiene informazioni potenzialmente riservate che non devono essere divulgate. Ad esempio:

* ID utente
* Percorsi di ricerca per risolvere i percorsi relativi
* `propertyMap`.

Particolarmente sensibile è `propertyMap` (consulta la documentazione API di [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), in quanto si tratta di una struttura di dati interna che può essere utilizzata per molti scopi, ad esempio per memorizzare in cache oggetti che condividono lo stesso ciclo di vita di `ResourceResolver`. La serializzazione di questi può causare la perdita di dettagli sull’implementazione e potenzialmente avere un impatto sulla sicurezza, in quanto vengono esposti dati che non dovrebbero essere leggibili e accessibili a un utente finale. Per questo motivo `ResourceResolvers` non deve essere serializzato in JSON.

Adobe prevede di disabilitare la serializzazione di `ResourceResolvers` in un approccio in due fasi:

1. A partire dalla 14697 sulla versione di AEM as a Cloud Service, ogni volta che un AEM `ResourceResolver` viene serializzato verrà registrato un messaggio di avviso. Tutti i clienti sono invitati a controllare i registri dell’applicazione per individuare queste istruzioni di registro e ad adattare di conseguenza la base di codice.
1. In un Adobe successivo, la serializzazione di ResourceResolvers come JSON verrà disabilitata.

## Implementazione {#implementation}

Il messaggio WARN viene registrato sia nelle istanze AEM as a Cloud Service che nell’SDK AEM locale e si presenta così:

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Questo messaggio di registro indica che durante il processo di serializzazione di `/content/…/page` in JSON un `ResourceResolver` è già serializzato. Richiedendo `/content/../page.model.json` è possibile verificare esattamente dove vengono visualizzati i campi di `ResourceResolver` e utilizzarli per identificare la classe del modello Sling che attiva effettivamente questo comportamento.


>[!NOTE]
>
>È stato verificato che i Componenti core AEM non sono interessati da questo problema.

## Azione richiesta {#requested-action}

Adobe richiede a tutti i clienti di controllare i registri applicazioni e le basi di codice per verificare se sono interessati da questo problema e di modificare l’applicazione personalizzata, se necessario, in modo che questo messaggio di AVVERTENZA non venga più visualizzato.

Si presume che nella maggior parte dei casi queste modifiche richieste siano dirette, in quanto gli oggetti `ResourceResolver` non sono affatto necessari nell&#39;output JSON, in quanto le informazioni in essi contenute normalmente non sono richieste dalle applicazioni front-end. Ciò significa che nella maggior parte dei casi dovrebbe essere sufficiente escludere l&#39;oggetto `ResourceResolver` dall&#39;essere considerato da Jackson (vedi le [regole](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

Nel caso in cui un modello Sling sia interessato da questo problema ma non modificato, la disabilitazione esplicita della serializzazione dell&#39;oggetto `ResourceResolver` (come eseguito da Adobe come secondo passaggio) applicherà una modifica nell&#39;output JSON.
