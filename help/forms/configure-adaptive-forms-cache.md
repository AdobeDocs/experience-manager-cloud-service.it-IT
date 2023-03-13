---
title: Configurare la cache di Adaptive Forms
seo-title: Configure Adaptive Forms cache
description: La cache di Adaptive Forms è progettata appositamente per Forms e documenti adattivi. Memorizza nella cache il Forms adattivo e i documenti adattivi con l’obiettivo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client.
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---


# Configurare la cache di Adaptive Forms {#configure-adaptive-forms-cache}

La cache è un meccanismo che consente di ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di input/output (I/O). La cache di Forms adattiva memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per il rendering di un modulo adattivo sul client. È stato progettato appositamente per Adaptive Forms.

## Configurare la cache di Adaptive Forms nelle istanze di authoring e pubblicazione {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vai a Gestione configurazione console web AEM all’indirizzo `https://[server]:[port]/system/console/configMgr`.
1. Clic **[!UICONTROL Configurazione di un modulo adattivo e di un canale web di comunicazione interattiva]** per modificarne i valori di configurazione.
1. In [!UICONTROL modificare i valori di configurazione] specificare il numero massimo di moduli o documenti per un&#39;istanza dell&#39;AEM [!DNL Forms] il server può memorizzare in cache **[!UICONTROL Numero di Forms adattivi]** campo. Il valore predefinito è 100.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disattiva o si modifica la configurazione della cache.

   ![Finestra di dialogo di configurazione per la cache di Adaptive Forms HTML](assets/cache-configuration-edit.png)

1. Clic **[!UICONTROL Salva]** per salvare la configurazione.

L’ambiente è configurato per l’utilizzo di cache Adaptive Forms e delle risorse correlate.


## (Facoltativo) Configurazione della cache dei moduli adattivi in Dispatcher {#configure-the-cache}

Puoi anche configurare il caching dei moduli adattivi nel dispatcher per un ulteriore miglioramento delle prestazioni.

### Prerequisiti {#pre-requisites}

* Abilita [unione o precompilazione dei dati nel client](prepopulate-adaptive-form-fields.md#prefill-at-client) opzione. Consente di unire dati univoci per ogni istanza di un modulo precompilato.
* [Abilita l’agente di svuotamento per ogni istanza di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Consente di ottenere migliori prestazioni di caching per Adaptive Forms. L’URL predefinito degli agenti di svuotamento è `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Considerazioni per la memorizzazione nella cache di Adaptive Forms su un dispatcher {#considerations}

* Quando utilizzi la cache di Forms adattivo, utilizza l’AEM [!DNL Dispatcher] per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, sul server utilizzato per lo sviluppo, mantieni disabilitata la cache di Forms adattivo.
* Gli URL senza estensione non vengono memorizzati in cache. Ad esempio, URL con pattern`/content/forms/[folder-structure]/[form-name].html` vengono memorizzati nella cache e la memorizzazione nella cache ignora gli URL con pattern `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Pertanto, utilizza gli URL con estensioni per sfruttare i vantaggi del caching.
* Considerazioni per Adaptive Forms localizzato:
   * Usa formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Disattiva utilizzando le impostazioni locali del browser <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->per URL con formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`, e **[!UICONTROL Usa impostazioni internazionali del browser]** in configuration manager è disattivato, viene distribuita la versione non localizzata del modulo adattivo. Il linguaggio non localizzato è il linguaggio utilizzato durante lo sviluppo del modulo adattivo. Le impostazioni locali configurate per il browser (impostazioni locali del browser) non vengono prese in considerazione e viene distribuita una versione non localizzata del modulo adattivo.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`, e **[!UICONTROL Usa impostazioni internazionali del browser]** in configuration manager è abilitato, viene distribuita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulle impostazioni locali configurate per il browser (impostazioni locali del browser). Può portare a [memorizzazione nella cache solo della prima istanza di un modulo adattivo]. Per evitare che il problema si verifichi nell’istanza, consulta [risoluzione dei problemi](#only-first-insatnce-of-adptive-forms-is-cached).

### Abilita il caching in Dispatcher

Per abilitare e configurare la memorizzazione in cache di Forms adattivi su Dispatcher, effettua le seguenti operazioni:

1. Apri il seguente URL per ogni istanza di pubblicazione dell’ambiente e configura l’agente di replica:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Aggiungi quanto segue al file dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Quando aggiungi quanto sopra:

   * Un modulo adattivo rimane nella cache fino a quando non viene pubblicata una versione aggiornata del modulo.

   * Quando viene pubblicata una versione più recente della risorsa a cui si fa riferimento in un modulo adattivo, il Forms adattivo interessato viene automaticamente invalidato. Esistono alcune eccezioni all’annullamento automatico della validità delle risorse di riferimento. Per risolvere le eccezioni, consulta [risoluzione dei problemi](#troubleshooting) sezione.
1. [Aggiungi il file rules dispatcher.any o personalizzato seguente](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). Sono esclusi gli URL che non supportano il caching. Ad esempio, la comunicazione interattiva.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Aggiungi i seguenti parametri all’elenco dei parametri degli URL da ignorare](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

L’ambiente AEM è configurato per memorizzare in cache il Forms adattivo. Memorizza nella cache tutti i tipi di Forms adattivo. Se hai la necessità di controllare le autorizzazioni di accesso utente per una pagina prima di distribuire la pagina memorizzata in cache, consulta [caching di contenuto protetto](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it).

## Risoluzione dei problemi {#troubleshooting}

### Alcuni Forms adattivi contenenti immagini o video non vengono invalidati automaticamente dalla cache del dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema   {#issue1}

Quando selezioni e aggiungi immagini o video tramite il browser delle risorse a un modulo adattivo e queste immagini e video vengono modificati nell’editor delle risorse, il Forms adattivo contenente tali immagini non viene invalidato automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution1}

Dopo aver pubblicato le immagini e il video, annulla esplicitamente la pubblicazione e pubblica l’Adaptive Forms che fa riferimento a tali risorse.

### Alcuni Forms adattivi contenenti frammenti di contenuto o frammenti di esperienza non vengono invalidati automaticamente dalla cache del dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema   {#issue2}

Quando aggiungi un frammento di contenuto o un frammento di esperienza a un modulo adattivo e queste risorse vengono modificate e pubblicate in modo indipendente, il Forms adattivo contenente tali risorse non viene invalidato automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution2}

Dopo aver pubblicato un frammento di contenuto o un frammento di esperienza aggiornato, annulla esplicitamente la pubblicazione e pubblica il Forms adattivo che utilizza queste risorse.

### Solo la prima istanza di un modulo adattivo è memorizzata nella cache{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema   {#issue3}

Se l’URL del modulo adattivo non contiene informazioni sulla localizzazione, e **[!UICONTROL Usa impostazioni internazionali del browser]** In Configuration Manager è abilitato, viene distribuita una versione localizzata del Modulo adattivo e solo la prima istanza del Modulo adattivo viene memorizzata nella cache e distribuita a ogni utente successivo.

#### Soluzione {#Solution3}

Per risolvere il problema, effettua le seguenti operazioni:

1. Apri il file conf.d/httpd-dispatcher.conf o qualsiasi altro file di configurazione configurato per il caricamento in fase di esecuzione.

1. Aggiungi il seguente codice al file e salvalo. Si tratta di un codice di esempio per modificarlo in base all’ambiente in uso.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
