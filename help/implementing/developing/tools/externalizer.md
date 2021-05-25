---
title: Esternalizzazione degli URL
description: L’esternalizzatore è un servizio OSGi che consente di trasformare programmaticamente un percorso di risorsa in un URL esterno e assoluto.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: ce43bdc94f14faa69add16139e22ea3f34dfc52f
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Esternalizzazione degli URL {#externalizing-urls}

In AEM, il **esternalizzatore** è un servizio OSGi che consente di trasformare programmaticamente un percorso di risorse (ad esempio `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) prefissando il percorso con un DNS preconfigurato.

Poiché un’istanza di Cloud Service di AEM non può conoscere il proprio URL visibile esternamente e poiché a volte un collegamento deve essere creato al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare tali URL esterni e generarli.

Questo articolo spiega come configurare il servizio Externalizer e come utilizzarlo. Per informazioni tecniche sul servizio, fare riferimento a [Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html).

## Comportamento predefinito dell&#39;Externalizer e Come ignorare {#default-behavior}

Preconfigurato, il servizio Externalizer dispone di valori quali `author-p12345-e6789.adobeaemcloud.com` e `publish-p12345-e6789.adobeaemcloud.com`.

Per ignorare tali valori, utilizza le variabili di ambiente di Cloud Manager come descritto nell’articolo [Configurazione di OSGi per AEM come Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e imposta le variabili predefinite `AEM_CDN_DOMAIN_AUTHOR` e `AEM_CDN_DOMAIN_PUBLISH`.

## Configurazione del servizio Externalizer {#configuring-the-externalizer-service}

Il servizio Externalizer ti consente di definire centralmente il dominio che può essere utilizzato per prefisso programmatico dei percorsi delle risorse. Il servizio Externalizer deve essere utilizzato solo per le applicazioni con un singolo dominio.

>[!NOTE]
>
>Come quando si applicano [configurazioni OSGi per AEM come Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) i passaggi seguenti devono essere eseguiti su un&#39;istanza di sviluppo locale e quindi impegnati nel codice del progetto per la distribuzione.

Per definire una mappatura del dominio per il servizio Externalizer:

1. Passa a Configuration Manager tramite:

   `https://<host>:<port>/system/console/configMgr`

1. Fai clic su **Day CQ Link Externalizer** per aprire la finestra di dialogo di configurazione.

   ![Configurazione OSGi dell’esternalizzatore](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >Il collegamento diretto alla configurazione è `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definire una mappatura **Domains**. Una mappatura consiste in un nome univoco che può essere utilizzato nel codice per fare riferimento al dominio, a uno spazio e al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Dove:

   * **`scheme`** di solito è http o https, ma può essere un altro protocollo.

      * Si consiglia di utilizzare https per applicare i collegamenti https.
      * Sarà utilizzato se il codice client non sostituisce lo schema quando si richiede l’esternalizzazione di un URL.
   * **`server`** è il nome host (un nome di dominio o un indirizzo ip).
   * **`port`** (facoltativo) è il numero di porta.
   * **`contextpath`** (facoltativo) è impostato solo se AEM è installato come applicazione web in un percorso contestuale diverso.

   Esempio: `production https://my.production.instance`

   I seguenti nomi di mappatura sono predefiniti e devono sempre essere impostati in base a AEM:

   * `local` - l&#39;istanza locale
   * `author` - DNS del sistema di authoring
   * `publish` - DNS del sito web pubblico

   >[!NOTE]
   >
   >Una configurazione personalizzata consente di aggiungere una nuova categoria, ad esempio `production`, `staging` o anche sistemi esterni non AEM come `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse della codebase di un progetto.

1. Fai clic su **Salva** per salvare le modifiche.

### Utilizzo del servizio Externalizer {#using-the-externalizer-service}

Questa sezione mostra alcuni esempi di utilizzo del servizio Externalizer.

>[!NOTE]
>
>Nessun collegamento assoluto deve essere creato nel contesto di HTML. Pertanto, in tali casi, questa utilità non deve essere utilizzata.

* **Per esternalizzare un percorso con il dominio &quot;pubblica&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Supponendo la mappatura del dominio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina con il valore:

   * `https://www.website.com/contextpath/my/page.html`

* **Per esternalizzare un percorso con il dominio &quot;author&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Supponendo la mappatura del dominio:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina con il valore:

   * `https://author.website.com/contextpath/my/page.html`

* **Per esternalizzare un percorso con il dominio &quot;locale&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Supponendo la mappatura del dominio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina con il valore:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Puoi trovare altri esempi in [Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html).
