---
title: Esternalizzazione degli URL
description: Externalizer è un servizio OSGi che consente di trasformare in modo programmatico un percorso di risorsa in un URL esterno e assoluto.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# Esternalizzazione degli URL {#externalizing-urls}

In AEM, **Externalizer** è un servizio OSGi che consente di trasformare in modo programmatico un percorso di risorsa (ad esempio, `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) prefissando il percorso con un DNS preconfigurato.

Poiché un’istanza di AEM as a Cloud Service non può conoscere il proprio URL visibile esternamente e poiché a volte è necessario creare un collegamento al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare tali URL esterni e generarli.

Questo articolo spiega come configurare il servizio Externalizer e come utilizzarlo. Per informazioni tecniche sul servizio, vedi [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamento predefinito di Externalizer e Procedura di sostituzione {#default-behavior}

Il servizio Externalizer associa una serie di identificatori di dominio a prefissi URL assoluti corrispondenti agli URL del servizio AEM generati per l&#39;ambiente, ad esempio `author https://author-p12345-e6789.adobeaemcloud.com` e `publish https://publish-p12345-e6789.adobeaemcloud.com`. Gli URL di base per ciascuno di questi domini predefiniti vengono letti dalle variabili di ambiente definite da Cloud Manager.

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
>Le mappature di dominio `local`, `author`, `preview` e `publish` Externalizer predefinite nella configurazione OSGi devono essere mantenute con i valori `$[env:...]` originali elencati sopra.
>
>La distribuzione di un file `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` personalizzato in AEM as a Cloud Service che omette una qualsiasi di queste mappature di dominio predefinite può causare un comportamento imprevedibile dell&#39;applicazione.

Non definire o sostituire le variabili di ambiente `EXTERNALIZER` (ad esempio, `AEM_EXTERNALIZER_AUTHOR`) in Cloud Manager. Se invece è necessario ignorare i valori di dominio `publish` o `preview`, definire e utilizzare le variabili di ambiente `AEM_CDN_DOMAIN_PUBLISH` e `AEM_CDN_DOMAIN_PREVIEW`. Queste variabili verranno assegnate automaticamente ai campi corrispondenti nella configurazione di Externalizer durante l’avvio.

<!-- Alexandru: hiding this. See CQDOC-23014 for more details

To override the `preview` and `publish` values, use Cloud Manager environment variables as described in the article [Configuring OSGi for AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) and setting the predefined `AEM_CDN_DOMAIN_PUBLISH` and `AEM_CDN_DOMAIN_PREVIEW` variables. -->

## Configurazione del servizio Externalizer {#configuring-the-externalizer-service}

Il servizio Externalizer ti consente di definire a livello centrale il dominio che può essere utilizzato per prefissare in modo programmatico i percorsi delle risorse. Il servizio Externalizer deve essere utilizzato solo per le applicazioni con un singolo dominio.

>[!NOTE]
>
>Come quando si applicano [configurazioni OSGi per AEM as a Cloud Service](/help/implementing/deploying/overview.md#osgi-configuration), è necessario eseguire i passaggi seguenti su un&#39;istanza di sviluppatore locale e quindi confermare il codice del progetto per la distribuzione.

Per definire un mapping di dominio per il servizio Externalizer:

1. Passa a Configuration Manager tramite:

   `https://<host>:<port>/system/console/configMgr`

1. Fai clic su **Day CQ Link Externalizer** per aprire la finestra di dialogo di configurazione.

   ![Configurazione OSGi di Externalizer](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >Il collegamento diretto alla configurazione è `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definisci una mappatura **Domini**. Una mappatura è costituita da un nome univoco che può essere utilizzato nel codice per fare riferimento al dominio, a uno spazio e al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Dove:

   * **`scheme`** è in genere http o https, ma può essere un altro protocollo.

      * Adobe consiglia di utilizzare https per applicare i collegamenti https.
      * Viene utilizzato se il codice client non sostituisce lo schema quando viene richiesta l’esternalizzazione di un URL.

   * **`server`** è il nome host (nome di dominio o indirizzo ip).
   * **`port`** (facoltativo) è il numero di porta.
   * **`contextpath`** (facoltativo) è impostato solo se AEM è installato come app Web in un percorso di contesto diverso.

   Esempio: `production https://my.production.instance`

   I seguenti nomi di mappatura sono predefiniti e devono sempre essere impostati in quanto AEM si basa su di essi:

   * `local` - l&#39;istanza locale
   * `author` - DNS del sistema di authoring
   * `publish` - DNS del sito Web pubblico

   >[!NOTE]
   >
   >Una configurazione personalizzata consente di aggiungere una nuova categoria, ad esempio `production`, `staging` o anche sistemi esterni non AEM come `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse nella base di codice di un progetto.

1. Fai clic su **Salva** per salvare le modifiche.

### Utilizzo del servizio Externalizer {#using-the-externalizer-service}

Questa sezione mostra alcuni esempi di utilizzo del servizio Externalizer.

>[!NOTE]
>
>Non è necessario creare collegamenti assoluti nel contesto di HTML. Pertanto, non utilizzare questa utilità in tali casi.

* **Per esternalizzare un percorso con il dominio &#39;publish&#39;:**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  Supponendo il mapping del dominio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina con il valore:

   * `https://www.website.com/contextpath/my/page.html`

* **Per esternalizzare un percorso con il dominio &#39;author&#39;:**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  Supponendo il mapping del dominio:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina con il valore:

   * `https://author.website.com/contextpath/my/page.html`

* **Per esternalizzare un percorso con il dominio &#39;locale&#39;:**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  Supponendo il mapping del dominio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina con il valore:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Puoi trovare altri esempi nei [JavaScript](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
