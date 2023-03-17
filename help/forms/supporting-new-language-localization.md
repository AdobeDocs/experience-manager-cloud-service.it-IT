---
title: Aggiunta del supporto per nuove impostazioni internazionali a un modulo adattivo
seo-title: Learn to add support for new locales to your adaptive forms
description: AEM Forms consente di aggiungere nuove impostazioni internazionali per la localizzazione di moduli adattivi. Inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: 00fcdb3530a441bde2f7f91515aaaec341615a3f
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Supporto di nuove impostazioni internazionali per la localizzazione Adaptive Forms {#supporting-new-locales-for-adaptive-forms-localization}

AEM Forms fornisce supporto preconfigurato per le impostazioni internazionali (inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreana (ko-KR). È possibile aggiungere supporto anche per più impostazioni internazionali, come Hindi(hi_IN).

## Informazioni sui dizionari internazionali {#about-locale-dictionaries}

La localizzazione dei moduli adattivi si basa su due tipi di dizionari locali:

* **Dizionario specifico per il modulo** Contiene le stringhe utilizzate nei moduli adattivi. Ad esempio, etichette, nomi di campo, messaggi di errore, descrizioni della guida. È gestito come un set di file XLIFF per ogni impostazione internazionale ed è possibile accedervi in `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Dizionari globali** Ci sono due dizionari globali, gestiti come oggetti JSON, nella libreria client AEM. Questi dizionari contengono messaggi di errore predefiniti, nomi di mese, simboli di valuta, pattern di data e ora e così via. Puoi trovare questi dizionari in `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Queste posizioni contengono cartelle separate per ogni impostazione internazionale. Poiché i dizionari globali non vengono aggiornati frequentemente, mantenere file JavaScript separati per ogni impostazione internazionale consente ai browser di memorizzarli nella cache e di ridurre l’utilizzo della larghezza di banda della rete quando si accede a diversi moduli adattivi sullo stesso server.

## Aggiungi supporto per nuove impostazioni internazionali {#add-support-for-new-locales}

Esegui le seguenti operazioni per aggiungere il supporto per una nuova impostazione internazionale:

1. [Aggiunta del supporto per la localizzazione per le impostazioni internazionali non supportate](#add-localization-support-for-non-supported-locales)
1. [Usa impostazioni internazionali aggiunte in Adaptive Forms](#use-added-locale-in-af)

### Aggiunta del supporto per la localizzazione per le impostazioni internazionali non supportate {#add-localization-support-for-non-supported-locales}

AEM Forms supporta attualmente la localizzazione di contenuti Forms adattivi in inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).

Per aggiungere il supporto per una nuova impostazione internazionale in fase di runtime di Adaptive Forms:

1. [Clonare l’archivio](#clone-the-repository)
1. [Aggiungere un’impostazione internazionale al servizio GuideLocalizationService](#add-a-locale-to-the-guide-localization-service)
1. [Aggiungi cartella specifica per il nome dell&#39;impostazione internazionale](#add-locale-name-specific-folder)
1. [Aggiungere supporto per le impostazioni internazionali del dizionario](#add-locale-support-for-the-dictionary)
1. [Conferma le modifiche nell’archivio e distribuisci la pipeline](#commit-changes-in-repo-deploy-pipeline)

#### 1. Clonare l&#39;archivio {#clone-the-repository}

1. Dalla riga di comando, individua il punto in cui desideri duplicare l’archivio del Cloud Service Forms.
1. Esegui il comando [recuperato da Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) È simile a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Usa il nome utente e la password git per clonare l’archivio.
1. Apri la cartella dell’archivio del Cloud Service Forms clonato nell’editor desiderato.

#### 2. Aggiungere un’impostazione internazionale al servizio Guide Localization {#add-a-locale-to-the-guide-localization-service}

1. Individua il `Guide Localization Service.cfg.json` e aggiungere le impostazioni internazionali da aggiungere all&#39;elenco delle impostazioni internazionali supportate.

   >[!NOTE]
   >
   > Crea un file con il nome `Guide Localization Service.cfg.json` , se non è già presente.

#### 3. Aggiungi la libreria client della cartella specifica per il nome locale {#add-locale-name-specific-folder}

1. Nella cartella UI.content, crea `etc/clientlibs` cartella.
1. Creare ulteriormente una cartella denominata come `locale-name` sotto `etc/clientlibs` da utilizzare come contenitore per clientlibs xfa e af.

##### 3.1 Aggiungi la libreria client XFA per un&#39;impostazione internazionale nella cartella locale-name

Crea un nodo denominato come `[locale-name]_xfa` e digitare come `cq:ClientLibraryFolder` sotto `etc/clientlibs/locale_name`, con categoria `xfaforms.I18N.<locale>`e aggiungi i seguenti file:

* **I18N.js** definizione `xfalib.locale.Strings` per `<locale>` come definito in `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** contenenti:
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Aggiungere una libreria client per moduli adattivi per una cartella locale-name

1. Crea un nodo denominato come `[locale-name]_af` e digitare come `cq:ClientLibraryFolder` sotto `etc/clientlibs/locale_name`, con la categoria `guides.I18N.<locale>` e dipendenze come `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`.
1. Crea una cartella denominata `javascript` e aggiungi i seguenti file:

   * **i18n.js** definizione `guidelib.i18n`, con pattern di &quot;calendarSymSymbol&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` per `<locale>` secondo le specifiche XFA descritte in [Specifiche del set di impostazioni internazionali](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** definizione `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` per `<locale>` come definito in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Aggiungi **js.txt** contenenti:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Aggiungi il supporto delle impostazioni internazionali per il dizionario {#add-locale-support-for-the-dictionary}

Esegui questo passaggio solo se `<locale>` aggiungi non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Creare una cartella `languages` sotto `etc`, se non già presente.

1. Aggiungi una proprietà stringa con più valori `languages` al nodo, se non già presente.
1. Aggiungi il `<locale-name>` valori internazionali predefiniti `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se non già presente.

1. Aggiungi il `<locale>` ai valori del `languages` proprietà di `/etc/languages`.
1. Aggiungi le cartelle appena create nel `filter.xml` in etc/META-INF/[gerarchia delle cartelle] come:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Prima di apportare le modifiche all’archivio Git AEM, devi accedere al tuo [Informazioni sull’archivio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Conferma le modifiche nell’archivio e distribuisci la pipeline {#commit-changes-in-repo-deploy-pipeline}

Dopo aver aggiunto un nuovo supporto per le impostazioni internazionali, conferma le modifiche all’archivio GIT. Distribuisci il codice utilizzando l’intera pipeline di stack. Scopri [come impostare una pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) per aggiungere nuovo supporto per le impostazioni internazionali.
Al termine della pipeline, nell’ambiente AEM viene visualizzata la nuova impostazione internazionale aggiunta.

### Usa impostazioni internazionali aggiunte in Adaptive Forms {#use-added-locale-in-af}

Esegui i seguenti passaggi per utilizzare ed eseguire il rendering di un modulo adattivo utilizzando un’impostazione internazionale appena aggiunta:

1. Accedi alla tua istanza di authoring AEM.
1. Vai a **Forms** >  **Forms e documenti**.
1. Seleziona un modulo adattivo e fai clic su **Aggiungi dizionario** e **Aggiungi Dizionario Al Progetto Di Traduzione** viene visualizzata la procedura guidata.
1. Specifica la **Titolo del progetto** e seleziona la **Lingue di destinazione** dal menu a discesa in **Aggiungi Dizionario Al Progetto Di Traduzione** procedura guidata.
1. Fai clic su **Fine** ed esegui il progetto di traduzione creato.
1. Seleziona un modulo adattivo e fai clic su **Anteprima come HTML**.
1. Aggiungi `&afAcceptLang=<locale-name>` nell’URL di un modulo adattivo.
1. Aggiorna la pagina e il modulo adattivo viene riprodotto in un’impostazione internazionale specifica.

Esistono due metodi per identificare le impostazioni internazionali di un modulo adattivo. Quando viene eseguito il rendering di un modulo adattivo, identifica le impostazioni internazionali richieste nei seguenti modi:

* Recupero del `[local]` nell’URL del modulo adattivo. Il formato dell’URL è `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Utilizzo `[local]` Il selettore consente di memorizzare in cache un modulo adattivo.

* Recupero dei seguenti parametri nell&#39;ordine elencato:

   * Parametro di richiesta `afAcceptLang`
Per ignorare le impostazioni internazionali del browser degli utenti, puoi trasmettere le 
`afAcceptLang` richiede il parametro per forzare le impostazioni internazionali. Ad esempio, l’URL seguente forza il rendering del modulo nelle impostazioni internazionali canadese-francese:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * Le impostazioni internazionali del browser impostate per l’utente, specificate nella richiesta utilizzando `Accept-Language` intestazione.

Se non esiste una libreria client per le impostazioni internazionali richieste, cerca in una libreria client il codice della lingua presente nelle impostazioni internazionali. Ad esempio, se le impostazioni internazionali richieste sono `en_ZA` (Inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizza la libreria client per `en` (Inglese), se esiste. Tuttavia, se non sono presenti, il modulo adattivo utilizza il dizionario per `en` locale.


Una volta identificate le impostazioni internazionali, il modulo adattivo seleziona il dizionario specifico per il modulo. Se il dizionario specifico per il modulo per le impostazioni internazionali richieste non viene trovato, utilizza il dizionario per la lingua in cui viene creato il modulo adattivo.

Se non sono presenti informazioni sulle impostazioni internazionali, il modulo adattivo viene distribuito nella lingua originale del modulo. La lingua originale è la lingua utilizzata durante lo sviluppo del Modulo adattivo.

Get [libreria client di esempio](/help/forms/assets/locale-support-sample.zip) per aggiungere il supporto per le nuove impostazioni internazionali. È necessario modificare il contenuto della cartella nelle impostazioni internazionali richieste.

## Best practice per supportare la nuova localizzazione {#best-practices}

* Adobe consiglia di creare un progetto di traduzione dopo la creazione di un modulo adattivo.

* Quando vengono aggiunti nuovi campi in un modulo adattivo esistente:
   * **Per la traduzione automatica**: Ricrea il dizionario ed esegui il progetto di traduzione. I campi aggiunti a un modulo adattivo dopo la creazione di un progetto di traduzione rimangono non tradotti.
   * **Per la traduzione umana**: Esporta il dizionario tramite `[server:port]/libs/cq/i18n/gui/translator.html`. Aggiorna il dizionario per i campi appena aggiunti e caricalo.
