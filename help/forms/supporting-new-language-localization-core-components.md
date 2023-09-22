---
title: Come si aggiunge il supporto per nuove lingue a un modulo adattivo basato su componenti core?
description: AEM Forms consente di aggiungere nuove lingue per la localizzazione dei moduli adattivi.
source-git-commit: 0a1310290c25a94ffe6f95ea6403105475ef5dda
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 1%

---

# Aggiungere una lingua per Forms adattivo basato sui componenti core {#supporting-new-locales-for-adaptive-forms-localization}


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| Componenti di base | [Fai clic qui](supporting-new-language-localization.md) |
| Componenti core | Questo articolo |

AEM Forms fornisce supporto predefinito per le lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).

È possibile aggiungere il supporto anche per altre lingue, come Hindi(hi_IN).

<!-- 
## Understanding locale dictionaries {#about-locale-dictionaries}

The localization of adaptive forms relies on two types of locale dictionaries:

*   **Form-specific dictionary** Contains strings used in adaptive forms. For example, labels, field names, error messages, help descriptions. It is managed as a set of XLIFF files for each locale and you can access it at `[AEM Forms as a Cloud Service Author instance]/libs/cq/i18n/gui/translator.html`.

*   **Global dictionaries** There are two global dictionaries, managed as JSON objects, in AEM client library. These dictionaries contain default error messages, month names, currency symbols, date and time patterns, and so on.  These locations contain separate folders for each locale. Because global dictionaries are not updated frequently, keeping separate JavaScript files for each locale enables browsers to cache them and reduce network bandwidth usage when accessing different adaptive forms on same server.

-->

## Prerequisiti {#prerequistes}

Prima di iniziare ad aggiungere il supporto per una nuova lingua,

* Installa un editor di testo normale (IDE) per semplificarne la modifica. Gli esempi contenuti in questo documento si basano su Microsoft VS Code.
* Clona l’archivio dei Componenti core Adattivi di Forms. Per clonare l’archivio:
   1. Aprire la riga di comando o la finestra finale e passare a una posizione in cui archiviare il repository. Esempio `/adaptive-forms-core-components`
   1. Esegui il comando seguente per clonare l’archivio:

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  L&#39;archivio include una libreria client necessaria per aggiungere una lingua.


## Aggiungi una lingua {#add-localization-support-for-non-supported-locales}

Per aggiungere il supporto per una nuova lingua, eseguire la procedura seguente:

![Aggiungere una lingua a un repository](add-a-locale-adaptive-form-core-components.png)

### Clonare l’archivio Git as a Cloud Service per AEM {#clone-the-repository}

1. Apri la riga di comando e scegli una directory in cui memorizzare l’archivio, ad esempio `/cloud-service-repository/`.

1. Esegui il comando seguente per clonare l’archivio:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   Sostituisci `<my-org>` e `<my-program>` nell’URL precedente con il nome dell’organizzazione e del programma. Per istruzioni dettagliate su come ottenere il nome dell’organizzazione, il nome del programma o il percorso completo dell’archivio Git e le credenziali necessarie per clonare l’archivio, consulta [Accesso a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) articolo.

   Dopo aver completato correttamente il comando, una cartella `<my-program>` viene creato. Contiene il contenuto clonato dall’archivio Git. Nel resto dell’articolo, la cartella viene indicata come, `[AEM Forms as a Cloud Service Git repostory]`.


### Aggiungere le nuove impostazioni locali al servizio di localizzazione della Guida TV {#add-a-locale-to-the-guide-localization-service}

1. Apri la cartella dell’archivio, clonata nella sezione precedente, in un editor di testo normale.
1. Accedi a `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` cartella. È possibile trovare `<appid>` nel `archetype.properties` file del progetto.
1. Apri `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` file per la modifica. Se il file non esiste, crealo. Un file di esempio con impostazioni internazionali supportate si presenta come segue:

   ![Esempio di Guida a Localization Service.cfg.json](locales.png)

1. Aggiungi il [codice locale della lingua](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) stai cercando di aggiungere, ad esempio, &quot;hi&quot; per hindi.
1. Salva e chiudi il file 

### Creare una libreria client per aggiungere una lingua

AEM Forms fornisce una libreria client di esempio per aiutarti ad aggiungere facilmente nuove lingue. Puoi scaricare e aggiungere `clientlib-it-custom-locale` libreria client dall’archivio dei componenti core adattivi Forms su GitHub all’archivio as a Cloud Service Forms. Per aggiungere la libreria client, effettua le seguenti operazioni:

1. Apri l’archivio dei componenti core Adaptive Forms nell’editor di testo normale. Se non hai clonato l’archivio, consulta [Prerequisiti](#prerequistes) per istruzioni su come clonare l’archivio.
1. Accedi a `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` directory.
1. Copia il `clientlib-it-custom-locale` directory.
1. Accedi a `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` e incolla `clientlib-it-custom-locale` directory.


### Creare un file specifico per le impostazioni internazionali {#locale-specific-file}

1. Accedi a `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/`
1. Individua il [File .json locale inglese su GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json), che contiene il set più recente di stringhe predefinite incluse nel prodotto.
1. Crea un nuovo file .json per le tue impostazioni locali specifiche.
1. Nel file .json appena creato, esegui il mirroring della struttura del file locale in inglese.
1. Sostituisci le stringhe in lingua inglese nel file .json con le stringhe localizzate corrispondenti per la tua lingua.
1. Salvare e chiudere il file.


### Aggiunta del supporto delle impostazioni locali al dizionario {#add-locale-support-for-the-dictionary}

Esegui questo passaggio solo se `<locale>` stai aggiungendo non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Accedi a `[AEM Forms as a Cloud Service Git repostory]/ui.content/src/main/content/jcr_root/etc/` cartella.

1. Creare un `etc` cartella sotto `jcr_root` cartella, se non già presente.

1. Creare una cartella `languages` sotto `etc` cartella, se non già presente.

   ![Testo alternativo](etc-content-xml.png)

1. Creare un `.content.xml` file sotto `languages` cartella. Aggiungi al file il seguente contenuto:

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr]"/>
   ```

1. Aggiungi il codice locale al `languages` proprietà. Ad esempio, hi ha aggiunto l’hindi al seguente codice di esempio.


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

1. Aggiungi le cartelle appena create in `filter.xml` in `/ui.content/src/main/content/meta-inf/vault/filter.xml` come:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Aggiungi le cartelle appena create in `filter.xml` in `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

### Eseguire il commit delle modifiche e distribuire la pipeline {#commit-changes-in-repo-deploy-pipeline}

Apporta le modifiche all’archivio GIT dopo l’aggiunta di un nuovo supporto delle impostazioni internazionali. Distribuisci il codice utilizzando la pipeline full stack. Scopri [come impostare una pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) per aggiungere nuovo supporto per le impostazioni internazionali.

Una volta completata l’esecuzione della pipeline, le nuove impostazioni locali aggiunte sono pronte per l’uso.

## Anteprima di un modulo adattivo con le nuove impostazioni internazionali aggiunte {#use-added-locale-in-af}

Per visualizzare in anteprima un adattivo con le nuove impostazioni locali aggiunte, effettua le seguenti operazioni:

1. Accedi all’istanza as a Cloud Service di AEM Forms.
1. Vai a **Forms** >  **Forms e documenti**.
1. Seleziona un modulo adattivo e fai clic su **Aggiungi dizionario** e **Aggiungi dizionario a progetto di traduzione** viene visualizzata la procedura guidata.
1. Specifica la **Titolo progetto** e seleziona la **Lingue di destinazione** dal menu a discesa nella **Aggiungi dizionario a progetto di traduzione** procedura guidata.
1. Clic **Fine** ed esegui il progetto di traduzione creato.
1. Seleziona un modulo adattivo e fai clic su **Anteprima come HTML**.
1. Aggiungi `&afAcceptLang=<locale-name>` nell’URL di un modulo adattivo.
1. Aggiorna la pagina e viene eseguito il rendering del modulo adattivo in una lingua specificata.

Esistono due metodi per identificare le impostazioni locali di un modulo adattivo. Quando viene eseguito il rendering di un modulo adattivo, questo identifica le impostazioni locali richieste tramite:

* Recupero di `[local]` nell’URL del modulo adattivo. Il formato dell’URL è `http:/[AEM Forms Server URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Utilizzo di `[local]` consente di memorizzare in cache un modulo adattivo.

* Recupero dei seguenti parametri nell&#39;ordine elencato:

   * Parametro di richiesta `afAcceptLang`
Per ignorare le impostazioni locali del browser per gli utenti, puoi trasmettere il `afAcceptLang` per forzare le impostazioni locali. Ad esempio, l’URL seguente forza il rendering del modulo nelle impostazioni locali canadesi-francesi:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * Impostazioni locali del browser impostate per l&#39;utente, specificate nella richiesta utilizzando `Accept-Language` intestazione.

Se non esiste una libreria client per le impostazioni locali richieste, verifica la presenza di una libreria client per il codice della lingua presente nelle impostazioni locali. Ad esempio, se la lingua richiesta è `en_ZA` (inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizza la libreria client per `en` (Inglese), se esiste. Tuttavia, se non esiste nessuno di questi, il modulo adattivo utilizza il dizionario per `en` lingua.

Una volta identificate le impostazioni locali, il modulo adattivo seleziona il dizionario specifico per il modulo. Se non viene trovato il dizionario specifico per il modulo per le impostazioni locali richieste, viene utilizzato il dizionario per la lingua in cui viene creato il modulo adattivo.

Se non sono disponibili informazioni sulle impostazioni internazionali, il modulo adattivo viene visualizzato nella lingua originale, la lingua utilizzata durante lo sviluppo dei moduli.

<!--
Get [sample client library](/help/forms/assets/locale-support-sample.zip) to add support for new locale. You need to change the content of the folder in the required locale.

## Best Practices to support for new localization {#best-practices}

*   Adobe recommends creating a translation project after creating an Adaptive Form.

*   When new fields are added in an existing Adaptive Form:
    * **For machine translation**: Re-create the dictionary and run the translation project. Fields added to an Adaptive Form after creating a translation project remain untranslated. 
    * **For human translation**: Export the dictionary through `[server:port]/libs/cq/i18n/gui/translator.html`. Update the dictionary for the newly added fields and upload it.
-->
