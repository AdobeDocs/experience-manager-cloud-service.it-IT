---
title: Come si aggiunge il supporto per nuove lingue in un modulo adattivo basato su componenti core?
description: Scopri come aggiungere nuove lingue per un modulo adattivo.
source-git-commit: 0d2e353208e4e59296d551ca5270be06e574f7df
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 2%

---


# Aggiungere una lingua per Forms adattivo basato sui componenti core {#supporting-new-locales-for-adaptive-forms-localization}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| Componenti di base | [Fai clic qui](supporting-new-language-localization.md) |
| Componenti core | Questo articolo |

AEM Forms fornisce supporto predefinito per le lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). È possibile aggiungere il supporto anche per altre lingue, come Hindi(hi_IN).

## Come viene selezionata la lingua per un modulo adattivo?

Prima di iniziare ad aggiungere una lingua per Forms adattivo, è necessario comprendere come viene selezionata una lingua per un modulo adattivo. Esistono due metodi per identificare e selezionare le impostazioni locali di un modulo adattivo al momento del rendering:

* **Utilizzo di `locale` Selettore nell’URL**: durante il rendering di un modulo adattivo, il sistema identifica le impostazioni locali richieste esaminando [lingua] nell’URL del modulo adattivo. L’URL segue questo formato: http:/[URL del server AEM Forms]/content/forms/af/[afName].[lingua].html?wcmmode=disabled. L&#39;uso del [lingua] consente la memorizzazione nella cache del modulo adattivo. Ad esempio, l’URL `www.example.com/content/forms/af/contact-us.hi.html?wcmmmode=disabled` esegue il rendering del modulo in lingua hindi.

* Recupero dei parametri nell&#39;ordine elencato di seguito:

   * **Utilizzo di `afAcceptLang`parametro di richiesta**: per ignorare le impostazioni locali del browser dell’utente, puoi trasmettere il parametro della richiesta afAcceptLang. Ad esempio, il `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr` L’URL impone ad AEM Forms Server di eseguire il rendering del modulo nelle impostazioni internazionali francesi canadesi.

   * **Utilizzo delle impostazioni locali del browser (Intestazione Accept-Language)**: il sistema considera anche le impostazioni locali del browser dell’utente, specificate nella richiesta utilizzando `Accept-Language` intestazione.

  Se non è disponibile una libreria client (il processo di creazione e utilizzo della libreria è descritto più avanti in questo articolo) per le impostazioni locali richieste, il sistema controlla se esiste una libreria client per il codice della lingua nelle impostazioni locali. Ad esempio, se la lingua richiesta è `en_ZA` (Inglese sudafricano) e non esiste una libreria client per `en_ZA`, il modulo adattivo utilizza la libreria client per en (inglese), se disponibile. Se non viene trovato nessuno dei due, il modulo adattivo utilizza il dizionario per il `en` lingua.

  Una volta identificate le impostazioni locali, il modulo adattivo seleziona il dizionario corrispondente specifico per il modulo. Se non viene trovato il dizionario per le impostazioni locali richieste, per impostazione predefinita viene utilizzato nella lingua in cui è stato creato il modulo adattivo.

  Nei casi in cui non siano disponibili informazioni sulle impostazioni internazionali, il modulo adattivo viene visualizzato nella lingua originale, che è quella utilizzata durante lo sviluppo del modulo


## Prerequisiti {#prerequistes}

Prima di iniziare ad aggiungere una lingua:

* Installa un editor di testo normale (IDE) per semplificarne la modifica. Gli esempi contenuti in questo documento si basano su [Codice Microsoft® Visual Studio](https://code.visualstudio.com/download).
* Installare una versione di [Git](https://git-scm.com), se non disponibile sul computer.
* Clona il [Componenti core Forms adattivi](https://github.com/adobe/aem-core-forms-components) archivio. Per clonare l’archivio:
   1. Aprire la riga di comando o la finestra del terminale e passare a una posizione in cui archiviare l&#39;archivio. Ad esempio `/adaptive-forms-core-components`
   1. Esegui il comando seguente per clonare l’archivio:

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  L&#39;archivio include una libreria client necessaria per aggiungere una lingua.

  Una volta eseguito correttamente il comando, l’archivio viene clonato in `aem-core-forms-components` nel computer. Nel resto dell’articolo, la cartella viene indicata come, [Archivio dei componenti core di Forms adattivi].


## Aggiungi una lingua {#add-localization-support-for-non-supported-locales}

Per aggiungere il supporto per una nuova lingua, eseguire la procedura seguente:

![Aggiungere una lingua a un repository](add-a-locale-adaptive-form-core-components.png)

### 1. Clonare l’archivio Git as a Cloud Service per AEM {#clone-the-repository}

1. Apri la riga di comando e scegli una directory in cui memorizzare l’archivio as a Cloud Service di AEM Forms, ad esempio `/cloud-service-repository/`.

1. Esegui il comando seguente per clonare l’archivio:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   Sostituisci `<my-org>` e `<my-program>` nell’URL precedente con il nome dell’organizzazione e del programma. Per istruzioni dettagliate su come ottenere il nome dell’organizzazione, il nome del programma o il percorso completo dell’archivio Git e le credenziali necessarie per clonare l’archivio, consulta [Accesso a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) articolo.

   Dopo aver completato correttamente il comando, una cartella `<my-program>` viene creato. Contiene il contenuto clonato dall’archivio Git. Nel resto dell’articolo, la cartella viene indicata come, `[AEM Forms as a Cloud Service Git repository]`.


### 2. Aggiungere le nuove impostazioni locali al servizio di localizzazione della Guida TV {#add-a-locale-to-the-guide-localization-service}

1. Apri la cartella dell’archivio, clonata nella sezione precedente, in un editor di testo normale.
1. Accedi a `[AEM Forms as a Cloud Service Git repository]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` cartella. È possibile trovare `<appid>` nel `archetype.properties` file del progetto.
1. Apri `[AEM Forms as a Cloud Service Git repository]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` file per la modifica. Se il file non esiste, crealo. Un file di esempio con impostazioni internazionali supportate si presenta come segue:

   ![Esempio di Guida a Localization Service.cfg.json](locales.png)

1. Aggiungi il [codice locale della lingua](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) che stai cercando di aggiungere, ad esempio, aggiungi &quot;hi&quot; per hindi.
1. Salva e chiudi il file 

### 3. Creare una libreria client per aggiungere una lingua

AEM Forms fornisce una libreria client di esempio per aiutarti ad aggiungere facilmente nuove lingue. Puoi scaricare e aggiungere `clientlib-it-custom-locale` libreria client da [Archivio dei componenti core di Forms adattivi] su GitHub nell’archivio as a Cloud Service di Forms. Per aggiungere la libreria client, effettua le seguenti operazioni:

1. Apri il [Archivio dei componenti core di Forms adattivi] nell’editor di testo normale. Se non hai clonato l’archivio, consulta [Prerequisiti](#prerequistes) per istruzioni su come clonare l’archivio.
1. Accedi a `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` directory.
1. Copia il `clientlib-it-custom-locale` directory.
1. Accedi a `[AEM Forms as a Cloud Service Git repository]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` e incolla `clientlib-it-custom-locale` directory.


### 4. Creare un file specifico per le impostazioni internazionali {#locale-specific-file}

1. Accedi a `[AEM Forms as a Cloud Service Git repository]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/`
1. Individua il [File .json locale inglese su GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json), che contiene il set più recente di stringhe predefinite incluse nel prodotto.
1. Crea un file .json per la lingua specifica.
1. Nel file .json appena creato, esegui il mirroring della struttura del file locale in inglese.
1. Sostituisci le stringhe in lingua inglese nel file .json con le stringhe localizzate corrispondenti per la tua lingua.
1. Salvare e chiudere il file.


### 5. Aggiungere il supporto delle impostazioni internazionali al dizionario {#add-locale-support-for-the-dictionary}

Esegui questo passaggio solo se `<locale>` stai aggiungendo non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Accedi a `[AEM Forms as a Cloud Service Git repository]/ui.content/src/main/content/jcr_root/etc/` cartella.

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

### 6. Eseguire il commit delle modifiche e distribuire la pipeline {#commit-changes-in-repo-deploy-pipeline}

Apporta le modifiche all’archivio GIT dopo l’aggiunta della nuova lingua. Distribuisci il codice utilizzando la pipeline full stack. Scopri [come impostare una pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) per aggiungere nuovo supporto per le impostazioni internazionali.

Una volta completata l’esecuzione della pipeline, la lingua appena aggiunta è pronta per l’uso.

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

## Procedure consigliate per il supporto della nuova localizzazione {#best-practices}

* L’Adobe consiglia di creare un progetto di traduzione dopo la creazione di un modulo adattivo.

* Quando vengono aggiunti nuovi campi in un modulo adattivo esistente:
   * **Per la traduzione automatica**: ricrea il dizionario e [esegui il progetto di traduzione](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md). I campi aggiunti a un modulo adattivo dopo la creazione di un progetto di traduzione rimangono non tradotti.
   * **Per traduzione umana**: esporta il dizionario utilizzando l’interfaccia utente di `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. Aggiorna il dizionario per i campi appena aggiunti e caricalo.

## Vedi altro

* [Utilizzare la traduzione automatica o la traduzione umana per tradurre un modulo adattivo basato su componenti core](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)
* [Genera documento di record per Adaptive Forms](/help/forms/generate-document-of-record-core-components.md)
* [Aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)


