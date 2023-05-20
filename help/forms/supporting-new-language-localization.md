---
title: Aggiungere il supporto per nuove lingue a un modulo adattivo
seo-title: Learn to add support for new locales to your adaptive forms
description: AEM Forms consente di aggiungere nuove lingue per la localizzazione dei moduli adattivi. Inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-taiwanese (zh-TW) e coreano (ko-KR).
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Supporto di nuove lingue per la localizzazione di Forms adattivi {#supporting-new-locales-for-adaptive-forms-localization}

AEM Forms fornisce supporto predefinito per le lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). È possibile aggiungere il supporto anche per altre impostazioni internazionali, come Hindi(hi_IN).

## Informazioni sui dizionari delle impostazioni internazionali {#about-locale-dictionaries}

La localizzazione dei moduli adattivi si basa su due tipi di dizionari locali:

* **Dizionario specifico per modulo** Contiene le stringhe utilizzate nei moduli adattivi. Ad esempio, etichette, nomi dei campi, messaggi di errore, descrizioni dell’Aiuto. Viene gestito come un insieme di file XLIFF per ogni lingua e puoi accedervi all’indirizzo `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Dizionari globali** Nella libreria client AEM sono disponibili due dizionari globali gestiti come oggetti JSON. Questi dizionari contengono messaggi di errore predefiniti, nomi dei mesi, simboli di valuta, modelli di data e ora e così via. Puoi trovare questi dizionari all&#39;indirizzo `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Questi percorsi contengono cartelle separate per ogni lingua. Poiché i dizionari globali non vengono aggiornati frequentemente, la separazione dei file JavaScript per ciascuna lingua consente ai browser di memorizzarli nella cache e di ridurre l’utilizzo della larghezza di banda di rete quando si accede a moduli adattivi diversi sullo stesso server.

## Aggiunta del supporto per le nuove lingue {#add-support-for-new-locales}

Per aggiungere il supporto per una nuova lingua, effettua le seguenti operazioni:

1. [Aggiunta del supporto per la localizzazione per le lingue non supportate](#add-localization-support-for-non-supported-locales)
1. [Utilizzare le lingue aggiunte in Adaptive Forms](#use-added-locale-in-af)

### Aggiunta del supporto per la localizzazione per le lingue non supportate {#add-localization-support-for-non-supported-locales}

AEM Forms attualmente supporta la localizzazione di contenuti Forms adattivi nelle lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).

Per aggiungere il supporto per una nuova lingua in fase di esecuzione di Adaptive Forms:

1. [Clonare l’archivio](#clone-the-repository)
1. [Aggiungere una lingua al servizio GuideLocalizationService](#add-a-locale-to-the-guide-localization-service)
1. [Aggiungi cartella specifica per il nome della lingua](#add-locale-name-specific-folder)
1. [Aggiungere il supporto delle impostazioni locali per il dizionario](#add-locale-support-for-the-dictionary)
1. [Eseguire il commit delle modifiche nell’archivio e distribuire la pipeline](#commit-changes-in-repo-deploy-pipeline)

#### 1. Clonare l’archivio {#clone-the-repository}

1. Dalla riga di comando, individua il punto in cui desideri duplicare l’archivio di Cloud Service di Forms.
1. Esegui il comando [recuperato da Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) È simile a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Utilizza il nome utente e la password Git per clonare l’archivio.
1. Apri la cartella clonata dell’archivio di Cloud Service di Forms nell’editor preferito.

#### 2. Aggiungere una lingua al servizio di localizzazione della Guida TV {#add-a-locale-to-the-guide-localization-service}

1. Individua il `Guide Localization Service.cfg.json` e aggiungere le impostazioni locali da aggiungere all&#39;elenco delle impostazioni locali supportate.

   >[!NOTE]
   >
   > Crea un file con il nome `Guide Localization Service.cfg.json` file, se non già presente.

#### 3. Aggiungere una libreria client di cartelle specifica per il nome della lingua {#add-locale-name-specific-folder}

1. Nella cartella UI.content, crea `etc/clientlibs` cartella.
1. Crea ulteriormente una cartella denominata come `locale-name` in `etc/clientlibs` per fungere da contenitore per clientlibs xfa e af.

##### 3.1 Aggiungere una libreria client XFA per una lingua nella cartella dei nomi delle impostazioni internazionali

Crea un nodo denominato come `[locale-name]_xfa` e digita come `cq:ClientLibraryFolder` in `etc/clientlibs/locale_name`, con categoria `xfaforms.I18N.<locale>`e aggiungi i seguenti file:

* **I18N.js** definizione `xfalib.locale.Strings` per `<locale>` come definito in `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** contenente:
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Aggiungere la libreria client di Moduli adattivi per una cartella dei nomi delle impostazioni locali

1. Crea un nodo denominato come `[locale-name]_af` e digita come `cq:ClientLibraryFolder` in `etc/clientlibs/locale_name`, con categoria come `guides.I18N.<locale>` dipendenze e come `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`.
1. Crea una cartella denominata come `javascript` e aggiungi i seguenti file:

   * **i18n.js** definizione `guidelib.i18n`, con pattern di &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` per `<locale>` secondo le specifiche XFA descritte in [Specifica set di impostazioni internazionali](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** definizione `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` per `<locale>` come definito in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Aggiungi **js.txt** contenente:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Aggiungere il supporto delle impostazioni internazionali per il dizionario {#add-locale-support-for-the-dictionary}

Esegui questo passaggio solo se `<locale>` stai aggiungendo non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Creare una cartella `languages` in `etc`, se non già presente.

1. Aggiungere una proprietà stringa multivalore `languages` al nodo, se non già presente.
1. Aggiungi il `<locale-name>` valori predefiniti per le impostazioni locali `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se non già presente.

1. Aggiungi il `<locale>` ai valori del `languages` proprietà di `/etc/languages`.
1. Aggiungi le cartelle appena create in `filter.xml` in etc/META-INF/[gerarchia di cartelle] come:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Prima di eseguire il commit delle modifiche nell’archivio Git dell’AEM, devi accedere al tuo [Informazioni sull’archivio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Eseguire il commit delle modifiche nell’archivio e distribuire la pipeline {#commit-changes-in-repo-deploy-pipeline}

Apporta le modifiche all’archivio GIT dopo l’aggiunta di un nuovo supporto delle impostazioni internazionali. Distribuisci il codice utilizzando la pipeline full stack. Scopri [come impostare una pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) per aggiungere nuovo supporto per le impostazioni internazionali.
Una volta completata la pipeline, nell’ambiente AEM viene visualizzata la lingua appena aggiunta.

### Usa le impostazioni locali aggiunte in Adaptive Forms {#use-added-locale-in-af}

Per utilizzare ed eseguire il rendering di un modulo adattivo utilizzando le impostazioni locali appena aggiunte, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring dell’AEM.
1. Vai a **Forms** >  **Forms e documenti**.
1. Seleziona un modulo adattivo e fai clic su **Aggiungi dizionario** e **Aggiungi dizionario a progetto di traduzione** viene visualizzata la procedura guidata.
1. Specifica la **Titolo progetto** e seleziona la **Lingue di destinazione** dal menu a discesa nella **Aggiungi dizionario a progetto di traduzione** procedura guidata.
1. Clic **Fine** ed esegui il progetto di traduzione creato.
1. Seleziona un modulo adattivo e fai clic su **Anteprima come HTML**.
1. Aggiungi `&afAcceptLang=<locale-name>` nell’URL di un modulo adattivo.
1. Aggiorna la pagina e viene eseguito il rendering del modulo adattivo in una lingua specificata.

Esistono due metodi per identificare le impostazioni locali di un modulo adattivo. Quando viene eseguito il rendering di un modulo adattivo, questo identifica le impostazioni locali richieste tramite:

* Recupero di `[local]` nell’URL del modulo adattivo. Il formato dell’URL è `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Utilizzo di `[local]` consente di memorizzare in cache un modulo adattivo.

* Recupero dei seguenti parametri nell&#39;ordine elencato:

   * Parametro di richiesta `afAcceptLang`
Per ignorare le impostazioni locali del browser per gli utenti, puoi trasmettere il 
`afAcceptLang` per forzare le impostazioni locali. Ad esempio, l’URL seguente forza il rendering del modulo nelle impostazioni locali canadesi-francesi:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * Impostazioni locali del browser impostate per l&#39;utente, specificate nella richiesta utilizzando `Accept-Language` intestazione.

Se non esiste una libreria client per le impostazioni locali richieste, verifica la presenza di una libreria client per il codice della lingua presente nelle impostazioni locali. Ad esempio, se la lingua richiesta è `en_ZA` (inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizza la libreria client per `en` (Inglese), se esiste. Tuttavia, se non esiste nessuno di questi, il modulo adattivo utilizza il dizionario per `en` lingua.


Una volta identificate le impostazioni locali, il modulo adattivo seleziona il dizionario specifico per il modulo. Se non viene trovato il dizionario specifico per la lingua richiesta, viene utilizzato il dizionario per la lingua in cui viene creato il modulo adattivo.

Se non sono presenti informazioni sulle impostazioni internazionali, il modulo adattivo viene consegnato nella lingua originale del modulo. La lingua originale è quella utilizzata durante lo sviluppo del modulo adattivo.

Ottenere [libreria client di esempio](/help/forms/assets/locale-support-sample.zip) per aggiungere il supporto per le nuove impostazioni locali. È necessario modificare il contenuto della cartella nelle impostazioni internazionali richieste.

## Procedure consigliate per il supporto della nuova localizzazione {#best-practices}

* L’Adobe consiglia di creare un progetto di traduzione dopo la creazione di un modulo adattivo.

* Quando vengono aggiunti nuovi campi in un modulo adattivo esistente:
   * **Per la traduzione automatica**: ricrea il dizionario ed esegui il progetto di traduzione. I campi aggiunti a un modulo adattivo dopo la creazione di un progetto di traduzione rimangono non tradotti.
   * **Per traduzione umana**: esporta il dizionario tramite `[server:port]/libs/cq/i18n/gui/translator.html`. Aggiorna il dizionario per i campi appena aggiunti e caricalo.
