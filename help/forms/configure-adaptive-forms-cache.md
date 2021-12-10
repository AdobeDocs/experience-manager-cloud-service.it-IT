---
title: Configurare la cache Forms adattiva
seo-title: Configure Adaptive Forms cache
description: 'La cache Adaptive Forms è progettata appositamente per Forms e documenti adattivi. Memorizza in cache i documenti adattivi Forms e adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo o di un documento sul client. '
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


# Configurare la cache Forms adattiva {#configure-adaptive-forms-cache}

Una cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di input/output (I/O). La cache Forms adattiva memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo sul client. È stato progettato appositamente per l&#39;Adaptive Forms.

## Configurare la cache Forms adattiva nelle istanze di authoring e pubblicazione {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vai AEM gestione della configurazione della console Web all&#39;indirizzo `https://[server]:[port]/system/console/configMgr`.
1. Fai clic su **[!UICONTROL Configurazione del canale web per moduli adattivi e comunicazioni interattive]** per modificare i valori di configurazione.
1. In [!UICONTROL modificare i valori di configurazione] specificare il numero massimo di moduli o documenti e un&#39;istanza del AEM [!DNL Forms] il server può memorizzare nella cache **[!UICONTROL Numero di Forms adattivi]** campo . Il valore predefinito è 100.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivo su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

   ![Finestra di dialogo di configurazione per la cache Adaptive Forms HTML](assets/cache-configuration-edit.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare la configurazione.

L’ambiente è configurato per utilizzare la cache di Adaptive Forms e le risorse correlate.


## (Facoltativo) Configura la cache dei moduli adattivi al dispatcher {#configure-the-cache}

Puoi anche configurare la memorizzazione in cache dei moduli adattivi al dispatcher per un ulteriore miglioramento delle prestazioni.

### Prerequisiti {#pre-requisites}

* Abilita la [unione o precompilazione dei dati sul client](prepopulate-adaptive-form-fields.md#prefill-at-client) opzione . Consente di unire dati univoci per ogni istanza di un modulo precompilato.
* [Abilita l&#39;agente flush per ogni istanza di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Consente di ottenere migliori prestazioni di memorizzazione in cache per Adaptive Forms. L&#39;URL predefinito degli agenti di flush è `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Considerazioni per la memorizzazione in cache di Adaptive Forms su un dispatcher {#considerations}

* Quando utilizzi la cache Forms adattiva, utilizza il AEM [!DNL Dispatcher] per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, sul server utilizzato per lo sviluppo, mantieni disabilitata la cache di Forms adattiva.
* Gli URL senza estensione non vengono memorizzati nella cache. Ad esempio, URL con pattern di pattern`/content/forms/[folder-structure]/[form-name].html` vengono memorizzati nella cache e la memorizzazione in cache ignora gli URL con pattern `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Utilizza quindi gli URL con estensioni per sfruttare i vantaggi della memorizzazione in cache.
* Considerazioni per Forms adattivo localizzato:
   * Usa formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Disattiva con le impostazioni internazionali del browser <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->per gli URL con formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL Usa impostazioni internazionali browser]** in configuration manager (gestione configurazione) disattivato, viene fornita la versione non localizzata del modulo adattivo. La lingua non localizzata è la lingua utilizzata durante lo sviluppo del Modulo adattivo. Le impostazioni internazionali configurate per il browser (impostazioni internazionali del browser) non vengono prese in considerazione e viene fornita una versione non localizzata del modulo adattivo.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL Usa impostazioni internazionali browser]** in configuration manager (gestione configurazioni) abilitato, viene fornita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulle impostazioni internazionali configurate per il browser (impostazioni internazionali del browser). Può portare a [memorizzazione in cache solo della prima istanza di un modulo adattivo]. Per evitare che il problema si verifichi nell’istanza, vedi [risoluzione](#only-first-insatnce-of-adptive-forms-is-cached).

### Abilita la memorizzazione in cache al dispatcher

Esegui i seguenti passaggi elencati per abilitare e configurare la memorizzazione in cache di Adaptive Forms sul dispatcher:

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

   * Quando viene pubblicata una versione più recente della risorsa a cui si fa riferimento in un modulo adattivo, l’impatto su Forms adattivo viene automaticamente invalidato. Sono presenti alcune eccezioni all’annullamento automatico della validità delle risorse di riferimento. Per la soluzione alle eccezioni, vedi [risoluzione](#troubleshooting) sezione .
1. [Aggiungi il seguente file di regole dispatcher.any o il file di regole personalizzate](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). Sono esclusi gli URL che non supportano la memorizzazione in cache. Ad esempio, la comunicazione interattiva.

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

1. [Aggiungi i seguenti parametri all’elenco dei parametri dell’URL di ignoramento](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

L’ambiente AEM è configurato per memorizzare nella cache Adaptive Forms. Memorizza in cache tutti i tipi di Forms adattivo. Se hai l’obbligo di controllare le autorizzazioni di accesso utente per una pagina prima di consegnare la pagina in cache, consulta [memorizzazione in cache di contenuto protetto](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Risoluzione dei problemi {#troubleshooting}

### Alcuni Forms adattivi contenenti immagini o video non vengono invalidati automaticamente dalla cache del dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema   {#issue1}

Quando selezioni e aggiungi immagini o video tramite il browser risorse a un modulo adattivo e queste immagini e video vengono modificati nell’editor di Assets, la funzione Adattivo Forms contenente tali immagini non viene invalidata automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution1}

Dopo aver pubblicato le immagini e il video, annulla esplicitamente la pubblicazione e pubblica l’Adaptive Forms che fa riferimento a queste risorse.

### Alcuni Forms adattivi contenenti frammenti di contenuto o frammenti di esperienza non vengono invalidati automaticamente dalla cache del dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema   {#issue2}

Quando aggiungi un frammento di contenuto o un frammento di esperienza a un modulo adattivo e queste risorse vengono modificate e pubblicate in modo indipendente, l’Adattivo Forms contenente tali risorse non viene invalidato automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution2}

Dopo aver pubblicato un frammento di contenuto aggiornato o un frammento di esperienza, annulla esplicitamente la pubblicazione e pubblica l’Adaptive Forms che utilizza queste risorse.

### Solo la prima istanza di un modulo adattivo viene memorizzata nella cache{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema   {#issue3}

Se l’URL del modulo adattivo non dispone di informazioni sulla localizzazione e **[!UICONTROL Usa impostazioni internazionali browser]** in configuration manager è abilitato, viene fornita una versione localizzata del modulo adattivo e solo la prima istanza del modulo adattivo viene memorizzata nella cache e distribuita a ogni utente successivo.

#### Soluzione {#Solution3}

Esegui i seguenti passaggi per risolvere il problema:

1. Apri conf.d/httpd-dispatcher.conf o qualsiasi altro file di configurazione configurato per il caricamento in fase di runtime.

1. Aggiungi il seguente codice al file e salvalo. Si tratta di un codice di esempio modificarlo in base all’ambiente.

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
