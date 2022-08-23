---
title: Esternalizzazione degli URL
description: L’esternalizzatore è un servizio OSGi che consente di trasformare programmaticamente un percorso di risorsa in un URL esterno e assoluto.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: 28903c1cbadece9d0ef575cdc0f0d7fd32219538
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Esternalizzazione degli URL {#externalizing-urls}

In AEM, il **Esternalizzatore** è un servizio OSGi che consente di trasformare programmaticamente un percorso di risorsa (ad esempio `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) prefissando il percorso con un DNS preconfigurato.

Poiché un’istanza AEM as a Cloud Service non può conoscere il proprio URL visibile esternamente e poiché a volte un collegamento deve essere creato al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare tali URL esterni e generarli.

Questo articolo spiega come configurare il servizio Externalizer e come utilizzarlo. Per i dettagli tecnici del servizio, si prega di fare riferimento al [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamento predefinito dell&#39;esternalizzatore e modalità di esclusione {#default-behavior}

Il servizio Externalizer mappa una manciata di identificatori di dominio con prefissi URL assoluti che corrispondono agli URL del servizio AEM generati per l’ambiente, ad esempio `author https://author-p12345-e6789.adobeaemcloud.com` e `publish https://publish-p12345-e6789.adobeaemcloud.com`. Gli URL di base per ciascuno di questi domini predefiniti vengono letti dalle variabili di ambiente definite da Cloud Manager.

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
>Il valore predefinito `local`, `author`, `preview`e `publish` Le mappature del dominio Externalizer nella configurazione OSGi devono essere mantenute con l&#39;originale `$[env:...]` i valori elencati sopra.
>
>Implementazione di un `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` file AEM as a Cloud Service che omette uno di questi mapping di dominio predefiniti potrebbe causare un comportamento imprevedibile dell&#39;applicazione.

Per ignorare il `preview` e `publish` , utilizza le variabili di ambiente di Cloud Manager come descritto nell’articolo [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e l&#39;impostazione dei predefiniti `AEM_CDN_DOMAIN_PUBLISH` e `AEM_CDN_DOMAIN_PREVIEW` variabili.

## Configurazione del servizio Externalizer {#configuring-the-externalizer-service}

Il servizio Externalizer ti consente di definire centralmente il dominio che può essere utilizzato per prefisso programmatico dei percorsi delle risorse. Il servizio Externalizer deve essere utilizzato solo per le applicazioni con un singolo dominio.

>[!NOTE]
>
>Come quando si applicano [Configurazioni OSGi per AEM as a Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) i passaggi seguenti devono essere eseguiti su un’istanza di sviluppo locale e quindi essere impegnati nel codice del progetto per la distribuzione.

Per definire una mappatura del dominio per il servizio Externalizer:

1. Passa a Configuration Manager tramite:

   `https://<host>:<port>/system/console/configMgr`

1. Fai clic su **Day CQ Link Externalizer** per aprire la finestra di dialogo di configurazione.

   ![Configurazione OSGi dell’esternalizzatore](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >Il collegamento diretto alla configurazione è `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definire un **Domini** mappatura. Una mappatura consiste in un nome univoco che può essere utilizzato nel codice per fare riferimento al dominio, a uno spazio e al dominio:

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
   >Una configurazione personalizzata consente di aggiungere una nuova categoria, ad esempio `production`, `staging` o anche sistemi esterni non AEM quali `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse della codebase di un progetto.

1. Fai clic su **Salva** per salvare le modifiche.

### Utilizzo del servizio Externalizer {#using-the-externalizer-service}

Questa sezione mostra alcuni esempi di utilizzo del servizio Externalizer.

>[!NOTE]
>
>Non è necessario creare collegamenti assoluti nel contesto di HTML. Pertanto, in tali casi, questa utilità non deve essere utilizzata.

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
>Puoi trovare ulteriori esempi nella sezione [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
