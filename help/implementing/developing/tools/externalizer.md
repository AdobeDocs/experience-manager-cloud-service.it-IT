---
title: Esternalizzazione degli URL
description: Externalizer è un servizio OSGi che consente di trasformare in modo programmatico un percorso di risorsa in un URL esterno e assoluto.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Esternalizzazione degli URL {#externalizing-urls}

Nell&#39;AEM, la **Esternalizzatore** è un servizio OSGi che consente di trasformare in modo programmatico un percorso di risorsa (ad esempio, `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) inserendo un prefisso DNS nel percorso.

Poiché un’istanza as a Cloud Service dell’AEM non può conoscere il proprio URL visibile esternamente e poiché a volte è necessario creare un collegamento al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare tali URL esterni e generarli.

Questo articolo spiega come configurare il servizio Externalizer e come utilizzarlo. Per informazioni tecniche dettagliate sul servizio, consultare il [JavaScript](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamento predefinito di Externalizer e Procedura di sostituzione {#default-behavior}

Il servizio Externalizer associa una serie di identificatori di dominio a prefissi URL assoluti che corrispondono agli URL del servizio AEM generati per l’ambiente, ad esempio `author https://author-p12345-e6789.adobeaemcloud.com` e `publish https://publish-p12345-e6789.adobeaemcloud.com`. Gli URL di base per ciascuno di questi domini predefiniti vengono letti dalle variabili di ambiente definite da Cloud Manager.

Per riferimento, la configurazione OSGi predefinita per `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` è effettivamente:

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>Il valore predefinito `local`, `author`, `preview`, e `publish` Le mappature del dominio esternalizzatore nella configurazione OSGi devono essere mantenute con l’originale `$[env:...]` i valori elencati sopra.
>
>Distribuzione di un `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` su AEM as a Cloud Service che omette una qualsiasi di queste mappature di dominio predefinite può causare un comportamento imprevedibile dell’applicazione.

Per ignorare `preview` e `publish` , utilizza le variabili di ambiente di Cloud Manager come descritto nell’articolo [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e l&#39;impostazione della `AEM_CDN_DOMAIN_PUBLISH` e `AEM_CDN_DOMAIN_PREVIEW` variabili.

## Configurazione del servizio Externalizer {#configuring-the-externalizer-service}

Il servizio Externalizer ti consente di definire a livello centrale il dominio da utilizzare per prefissare in modo programmatico i percorsi delle risorse. Il servizio Externalizer deve essere utilizzato solo per le applicazioni con un singolo dominio.

>[!NOTE]
>
>Come quando si applica [Configurazioni OSGi per AEM as a Cloud Service](/help/implementing/deploying/overview.md#osgi-configuration) i seguenti passaggi devono essere eseguiti in un’istanza sviluppatore locale e quindi eseguiti nel codice del progetto per la distribuzione.

Per definire un mapping di dominio per il servizio Externalizer:

1. Passa a Configuration Manager tramite:

   `https://<host>:<port>/system/console/configMgr`

1. Clic **Day CQ Link Externalizer** per aprire la finestra di dialogo configurazione.

   ![Configurazione OSGi di Externalizer](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >Il collegamento diretto alla configurazione è `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definisci un **Domini** mappatura. Una mappatura è costituita da un nome univoco che può essere utilizzato nel codice per fare riferimento al dominio, a uno spazio e al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Dove:

   * **`scheme`** è solitamente http o https, ma può essere un altro protocollo.

      * Si consiglia di utilizzare https per applicare i collegamenti https.
      * Viene utilizzato se il codice client non sostituisce lo schema quando viene richiesta l’esternalizzazione di un URL.

   * **`server`** è il nome host (un nome di dominio o un indirizzo ip).
   * **`port`** (facoltativo) è il numero della porta.
   * **`contextpath`** (facoltativo) è impostato solo se AEM è installato come app web in un percorso di contesto diverso.

   Esempio: `production https://my.production.instance`

   I seguenti nomi di mappatura sono predefiniti e devono sempre essere impostati in quanto AEM si basa su di essi:

   * `local` : l’istanza locale
   * `author` - DNS del sistema di authoring
   * `publish` - il sito web pubblico DNS

   >[!NOTE]
   >
   >Una configurazione personalizzata consente di aggiungere una nuova categoria, ad esempio `production`, `staging` o anche sistemi esterni non AEM come `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse nella base di codice di un progetto.

1. Clic **Salva** per salvare le modifiche.

### Utilizzo del servizio Externalizer {#using-the-externalizer-service}

Questa sezione mostra alcuni esempi di utilizzo del servizio Externalizer.

>[!NOTE]
>
>Non è necessario creare collegamenti assoluti nel contesto di HTML. Pertanto questa utilità non deve essere utilizzata in tali casi.

* **Per esternalizzare un percorso con il dominio &quot;publish&quot;:**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  Supponendo il mapping del dominio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` finisce con il valore:

   * `https://www.website.com/contextpath/my/page.html`

* **Per esternalizzare un percorso con il dominio &quot;author&quot;:**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  Supponendo il mapping del dominio:

   * `author https://author.website.com`

   * `myExternalizedUrl` finisce con il valore:

   * `https://author.website.com/contextpath/my/page.html`

* **Per esternalizzare un percorso con il dominio &quot;locale&quot;:**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  Supponendo il mapping del dominio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` finisce con il valore:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Puoi trovare altri esempi nella sezione [JavaScript](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
