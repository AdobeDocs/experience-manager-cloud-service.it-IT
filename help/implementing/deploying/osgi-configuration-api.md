---
title: API di configurazione OSGi
description: Descrizione della superficie di configurazione OSGi as a Cloud Service per AEM
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---

# API di configurazione OSGi

I due elenchi seguenti riflettono l’area di configurazione OSGi as a Cloud Service all’AEM e descrivono cosa possono configurare i clienti.

1. Elenco di configurazioni OSGi che non devono essere configurate dal codice cliente
1. Un elenco di configurazioni OSGi le cui proprietà possono essere configurate, ma devono rispettare le regole di convalida indicate. Queste regole includono se è necessaria la dichiarazione della proprietà, il suo tipo e, in alcuni casi, l’intervallo di valori consentito.

Se una configurazione OSGI non è elencata, potrebbe essere configurata dal codice del cliente.

Queste regole vengono convalidate durante il processo di build di Cloud Manager. Con il passare del tempo è possibile aggiungere altre regole e la data di applicazione prevista è indicata nella tabella. I clienti sono tenuti a rispettare queste regole entro la data di applicazione prevista. Il mancato rispetto delle regole dopo la data di rimozione genererà errori nel processo di compilazione di Cloud Manager. I progetti Maven devono includere [Plug-in Maven per SDK Build Analyzer per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it) per segnalare gli errori di configurazione OSGI durante lo sviluppo dell’SDK locale.

Ulteriori informazioni sulla configurazione OSGI sono disponibili all’indirizzo [questa posizione](/help/implementing/deploying/configuring-osgi.md).

## Configurazioni OSGi che non possono essere modificate {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
* **`org.apache.felix.http (Factory)`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Data notifica: 8/25/2021, Data applicazione: 11/26/2021)

## Configurazioni OSGi soggette alle regole di convalida della build {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Tipo: numero intero
      * Intervallo richiesto: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Tipo: doppio
   * `org.apache.felix.eventadmin.Timeout`
      * Tipo: numero intero
   * `org.apache.felix.eventadmin.RequireTopic`
      * Tipo: booleano
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Obbligatorio
      * Tipo: matrice di stringhe
      * Intervallo richiesto: deve includere almeno tutti `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Tipo: matrice di stringhe
* **`org.apache.felix.http`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: numero intero
   * `org.apache.felix.http.session.timeout`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: numero intero
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: numero intero
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: stringa
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: matrice di stringhe
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: matrice di stringhe
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: matrice di stringhe
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: matrice di stringhe
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: matrice di stringhe
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: matrice di stringhe
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: matrice di stringhe
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: numero intero
      * Intervallo richiesto: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obbligatorio
      * Tipo: matrice di stringhe
      * Intervallo richiesto: deve includere js
* **`com.day.cq.mailer.DefaultMailService`** (Data notifica: 4/30/2021, Data applicazione: 7/31/2021)
   * `smtp.host`
      * Tipo: stringa
   * `smtp.port`
      * Tipo: numero intero
      * Intervallo richiesto: 465, 587 o 25
   * `smtp.user`
      * Tipo: stringa
   * `smtp.password`
      * Tipo: stringa
   * `from.address`
      * Tipo: stringa
   * `smtp.ssl`
      * Tipo: stringa
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Data notifica: 11/16/21, Data applicazione: 2/16/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumerazione
      * Intervallo richiesto: INFO, DEBUG o TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: stringa
   * `org.apache.sling.commons.log.file`
      * Tipo: stringa
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano