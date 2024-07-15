---
title: Come si aggiunge il supporto per le nuove lingue in un modulo adattivo basato su componenti di base?
description: Per Adaptive Forms, puoi aggiungere lingue per più lingue oltre a quella fornita come impostazione predefinita.
feature: Adaptive Forms, Foundation Components
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 1%

---

# Supporto di nuove lingue per la localizzazione di Forms adattivi {#supporting-new-locales-for-adaptive-forms-localization}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html) |
| Componenti core | [Fai clic qui](supporting-new-language-localization-core-components.md) |
| Componenti di base | Questo articolo |

AEM Forms fornisce supporto predefinito per le lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). È possibile aggiungere il supporto anche per altre lingue, come Hindi(hi_IN).

## Informazioni sui dizionari delle impostazioni internazionali {#about-locale-dictionaries}

La localizzazione dei moduli adattivi si basa su due tipi di dizionari locali:

* **Dizionario specifico per modulo** Contiene stringhe utilizzate nei moduli adattivi. Ad esempio, etichette, nomi dei campi, messaggi di errore, descrizioni dell’Aiuto. Viene gestito come un insieme di file XLIFF per ogni lingua e puoi accedervi all&#39;indirizzo `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Dizionari globali** Nella libreria client AEM sono presenti due dizionari globali gestiti come oggetti JSON. Questi dizionari contengono messaggi di errore predefiniti, nomi dei mesi, simboli di valuta, modelli di data e ora e così via. Questi dizionari sono disponibili in `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Questi percorsi contengono cartelle separate per ogni lingua. Poiché i dizionari globali non vengono aggiornati frequentemente, la separazione dei file JavaScript per ogni lingua consente ai browser di memorizzarli nella cache e di ridurre l&#39;utilizzo della larghezza di banda di rete quando si accede a moduli adattivi diversi sullo stesso server.

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
1. Eseguire il comando [ recuperato da Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) È simile a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Utilizza il nome utente e la password Git per clonare l’archivio.
1. Apri la cartella clonata dell’archivio di Cloud Service di Forms nell’editor preferito.

#### 2. Aggiungere una lingua al servizio di localizzazione della Guida TV {#add-a-locale-to-the-guide-localization-service}

1. Individuare il file `Guide Localization Service.cfg.json` e aggiungere le impostazioni locali da aggiungere all&#39;elenco delle impostazioni locali supportate.

   >[!NOTE]
   >
   > Creare un file con il nome `Guide Localization Service.cfg.json`, se non già presente.

#### 3. Aggiungere una libreria client di cartelle specifica per il nome della lingua {#add-locale-name-specific-folder}

1. Nella cartella UI.content, crea la cartella `etc/clientlibs`.
1. Creare ulteriormente una cartella denominata `locale-name` in `etc/clientlibs` per fungere da contenitore per clientlibs xfa e af.

##### 3.1 Aggiungere una libreria client XFA per una lingua in una cartella con il nome della lingua

Creare un nodo denominato `[locale-name]_xfa` e digitare `cq:ClientLibraryFolder` in `etc/clientlibs/locale_name`, con la categoria `xfaforms.I18N.<locale>`, e aggiungere i file seguenti:

* **I18N.js** che definisce `xfalib.locale.Strings` per `<locale>` come definito in `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** contenente quanto segue:
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Aggiungere la libreria client di Moduli adattivi per una cartella dei nomi delle impostazioni locali

1. Creare un nodo denominato `[locale-name]_af` e digitare `cq:ClientLibraryFolder` in `etc/clientlibs/locale_name`, con categoria `guides.I18N.<locale>` e dipendenze `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`.
1. Creare una cartella denominata `javascript` e aggiungere i seguenti file:

   * **i18n.js** che definisce `guidelib.i18n`, con pattern di &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` per `<locale>` in base alle specifiche XFA descritte in [Specifiche set di impostazioni locali](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** che definisce `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` per `<locale>` come definito in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Aggiungi **js.txt** contenente quanto segue:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Aggiungere il supporto delle impostazioni internazionali per il dizionario {#add-locale-support-for-the-dictionary}

Eseguire questo passaggio solo se il `<locale>` che si sta aggiungendo non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Creare una cartella `languages` in `etc`, se non già presente.

1. Aggiungere una proprietà stringa multivalore `languages` al nodo, se non già presente.
1. Aggiungere i valori predefiniti delle impostazioni locali `<locale-name>` `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se non già presenti.

1. Aggiungere `<locale>` ai valori della proprietà `languages` di `/etc/languages`.
1. Aggiungi le cartelle create in `filter.xml` nella gerarchia delle cartelle etc/META-INF/[] come:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Prima di confermare le modifiche nell&#39;archivio Git AEM, devi accedere alle informazioni dell&#39;archivio [Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Eseguire il commit delle modifiche nell’archivio e distribuire la pipeline {#commit-changes-in-repo-deploy-pipeline}

Apporta le modifiche all’archivio GIT dopo l’aggiunta del supporto delle impostazioni internazionali. Distribuisci il codice utilizzando la pipeline full stack. Scopri [come configurare una pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) per aggiungere il supporto delle nuove impostazioni locali.
Una volta completata la pipeline, nell’ambiente AEM viene visualizzata la lingua appena aggiunta.

### Usa le impostazioni locali aggiunte in Adaptive Forms {#use-added-locale-in-af}

Per utilizzare ed eseguire il rendering di un modulo adattivo utilizzando le impostazioni locali appena aggiunte, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring dell’AEM.
1. Vai a **Forms** > **Forms e documenti**.
1. Selezionare un modulo adattivo e fare clic su **Aggiungi dizionario**. Viene visualizzata la procedura guidata **Aggiungi dizionario al progetto di traduzione**.
1. Specifica il **Titolo progetto** e seleziona le **Lingue di destinazione** dal menu a discesa nella procedura guidata **Aggiungi dizionario al progetto di traduzione**.
1. Fai clic su **Fine** ed esegui il progetto di traduzione creato.
1. Selezionare un modulo adattivo e fare clic su **Anteprima come HTML**.
1. Aggiungi `&afAcceptLang=<locale-name>` nell&#39;URL di un modulo adattivo.
1. Aggiorna la pagina e viene eseguito il rendering del modulo adattivo in una lingua specificata.

Esistono due metodi per identificare le impostazioni locali di un modulo adattivo. Quando viene eseguito il rendering di un modulo adattivo, questo identifica le impostazioni locali richieste tramite:

* Recupero del selettore `[local]` nell&#39;URL del modulo adattivo. Il formato dell&#39;URL è `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Il selettore `[local]` consente di memorizzare in cache un modulo adattivo.

* Recupero dei seguenti parametri nell&#39;ordine elencato:

   * Parametro richiesta `afAcceptLang`
Per ignorare le impostazioni locali del browser degli utenti, è possibile passare il parametro di richiesta `afAcceptLang` per forzare le impostazioni locali. Ad esempio, l’URL seguente forza il rendering del modulo nelle impostazioni locali canadesi-francesi:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * Impostazioni locali del browser impostate per l&#39;utente, specificate nella richiesta utilizzando l&#39;intestazione `Accept-Language`.

Se non esiste una libreria client per le impostazioni locali richieste, verifica la presenza di una libreria client per il codice della lingua presente nelle impostazioni locali. Ad esempio, se le impostazioni locali richieste sono `en_ZA` (inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizza la libreria client per la lingua `en` (inglese), se esiste. Tuttavia, se non esiste nessuno di questi, il modulo adattivo utilizza il dizionario per le impostazioni locali di `en`.


Una volta identificate le impostazioni locali, il modulo adattivo seleziona il dizionario specifico per il modulo. Se non viene trovato il dizionario specifico per il modulo per le impostazioni locali richieste, viene utilizzato il dizionario per la lingua in cui viene creato il modulo adattivo.

Se non sono presenti informazioni sulle impostazioni internazionali, il modulo adattivo viene consegnato nella lingua originale del modulo. La lingua originale è quella utilizzata durante lo sviluppo del modulo adattivo.

Ottieni una [libreria client di esempio](/help/forms/assets/locale-support-sample.zip) per aggiungere il supporto per le nuove impostazioni locali. È necessario modificare il contenuto della cartella nelle impostazioni internazionali richieste.

## Procedure consigliate per il supporto della nuova localizzazione {#best-practices}

* L’Adobe consiglia di creare un progetto di traduzione dopo la creazione di un modulo adattivo.

* Quando vengono aggiunti nuovi campi in un modulo adattivo esistente:
   * **Per la traduzione automatica**: ricreare il dizionario ed eseguire il progetto di traduzione. I campi aggiunti a un modulo adattivo dopo la creazione di un progetto di traduzione rimangono non tradotti.
   * **Per la traduzione umana**: esporta il dizionario tramite `[server:port]/libs/cq/i18n/gui/translator.html`. Aggiorna il dizionario per i campi appena aggiunti e caricalo.


## Consulta anche {#see-also}

{{see-also}}