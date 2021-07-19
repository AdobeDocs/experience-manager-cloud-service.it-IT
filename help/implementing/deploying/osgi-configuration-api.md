---
title: API di configurazione OSGi
description: Descrizione della AEM come superficie di configurazione OSGi Cloud Service
feature: Distribuzione
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# API di configurazione OSGi

I due elenchi seguenti riflettono l’AEM come superficie di configurazione OSGi di Cloud Service, descrivendo cosa i clienti possono configurare.

1. Un elenco di configurazioni OSGi che non devono essere configurate dal codice cliente
1. Elenco delle configurazioni OSGi le cui proprietà possono essere configurate, ma devono rispettare le regole di convalida indicate. Queste regole includono se la dichiarazione della proprietà è obbligatoria, il suo tipo e, in alcuni casi, l&#39;intervallo di valori consentito.

Se una configurazione OSGI non è elencata, potrebbe essere configurata dal codice cliente.

Queste regole vengono convalidate durante il processo di compilazione di Cloud Manager. È possibile aggiungere ulteriori regole nel tempo e la data prevista per l’applicazione è indicata nella tabella. I clienti sono tenuti a rispettare queste regole entro la data di implementazione prevista. Il mancato rispetto delle regole dopo la data di rimozione genera errori nel processo di compilazione di Cloud Manager. I progetti Maven devono includere il [AEM come Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) per contrassegnare gli errori di configurazione OSGI durante lo sviluppo dell&#39;SDK locale.

Ulteriori informazioni sulla configurazione OSGI sono disponibili in [questa posizione](/help/implementing/deploying/configuring-osgi.md).

## Configurazioni OSGi che non possono essere modificate {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
* **`org.apache.felix.http (Factory)`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)

## Configurazioni OSGi soggette a regole di convalida della generazione {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Tipo: integer
      * Intervallo richiesto: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Tipo: double
   * `org.apache.felix.eventadmin.Timeout`
      * Tipo: integer
   * `org.apache.felix.eventadmin.RequireTopic`
      * Tipo: booleano
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Obbligatorio
      * Tipo: array di stringhe
      * Intervallo richiesto: Deve includere almeno tutti i valori `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Tipo: array di stringhe
* **`org.apache.felix.http`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: integer
   * `org.apache.felix.http.session.timeout`
      * Tipo: integer
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: integer
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: integer
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: string
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: string
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: integer
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: integer
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: string
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: array di stringhe
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: array di stringhe
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: integer
      * Intervallo richiesto: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obbligatorio
      * Tipo: array di stringhe
      * Intervallo richiesto: deve includere js
* **`com.day.cq.mailer.DefaultMailService`** (Data annuncio: 30/04/2021, Data di applicazione: 31/07/2021)
   * `smtp.host`
      * Tipo: string
   * `smtp.port`
      * Tipo: integer
      * Intervallo richiesto: 465, 587 o 25
   * `smtp.user`
      * Tipo: string
   * `smtp.password`
      * Tipo: string
   * `from.address`
      * Tipo: string
   * `smtp.ssl`
      * Tipo: string
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
