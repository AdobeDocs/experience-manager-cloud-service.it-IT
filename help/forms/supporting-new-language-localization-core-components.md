---
title: Come si aggiunge il supporto per le nuove lingue in un modulo adattivo basato su componenti core?
description: Scopri come aggiungere nuove lingue per un modulo adattivo.
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
source-git-commit: 8730383d26c6f4fbe31a25a43d33bf314251d267
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 3%

---

# Aggiungere una lingua per un modulo adattivo basato sui componenti core {#supporting-new-locales-for-adaptive-forms-localization}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| Componenti di base | [Fai clic qui](supporting-new-language-localization.md) |
| Componenti core | Questo articolo |

<span class="preview"> La funzione di supporto per le lingue da destra a sinistra è disponibile nel primo programma per utenti. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

AEM Forms fornisce supporto predefinito per le lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). È possibile aggiungere il supporto anche per altre lingue, come Hindi(hi_IN). È inoltre possibile presentare Forms adattivo in una lingua RTL (Right-to-Left) come l’arabo, il persiano e l’urdu aggiungendo queste lingue.

## In che modo AEM Forms determina le impostazioni locali di un modulo adattivo?

Per una corretta localizzazione è fondamentale comprendere in che modo AEM Forms seleziona le impostazioni locali per il rendering di un modulo adattivo. Ecco una suddivisione del processo di selezione:

### Selezione delle impostazioni locali basata su priorità

Per determinare le impostazioni locali di un modulo adattivo, AEM Forms dà priorità ai seguenti metodi:

1. **Selettore impostazioni internazionali URL ([lingua])**:

   Il sistema assegna la priorità alle impostazioni locali specificate nell&#39;URL utilizzando [lingua] selettore. Questo formato consente la memorizzazione nella cache per prestazioni migliori.

   Formato: L’URL segue questo formato: http:/[URL del server AEM Forms]/content/forms/af/[afName].[lingua].html?wcmmode=disabled.

   Esempio: https://[server]/content/forms/af/contact-us.hi.html esegue il rendering del modulo in hindi.


1. **Parametro di richiesta afAcceptLang**:

   Per ignorare le impostazioni locali del browser dell&#39;utente, è possibile utilizzare `afAcceptLang` nell&#39;URL.

   Esempio: https://[server]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr forza il rendering della forma in francese canadese.

1. **Impostazioni locali browser dell&#39;utente (intestazione Accept-Language)**:

   Se non viene specificata nessun&#39;altra lingua, AEM Forms considera le impostazioni locali del browser dell&#39;utente inviate utilizzando `Accept-Language` intestazione.


### Meccanismo di fallback:


* Se non è disponibile una libreria client (procedura per aggiungere una nuova lingua, descritta più avanti in questo documento) per le impostazioni locali richieste, AEM Forms verifica la presenza di una libreria basata sul codice della lingua.

  Esempio: se viene richiesto en_ZA (inglese sudafricano) e non esiste una libreria en_ZA, utilizza en (inglese) se disponibile.

  Se non viene trovata alcuna libreria client adatta, il dizionario predefinito (per lo più `en`) per la lingua di authoring del modulo.

  In assenza di informazioni sulle impostazioni internazionali, il modulo adattivo viene visualizzato nella lingua originale utilizzata durante lo sviluppo.


## Prerequisiti per l&#39;aggiunta di una lingua

Prima di iniziare ad aggiungere una nuova lingua per il Forms adattivo, verifica di disporre dei seguenti elementi:

**Software:**

* Editor di testo normale (IDE): anche se qualsiasi editor di testo normale può funzionare, un ambiente di sviluppo integrato (IDE) come [Codice Microsoft Visual Studio](https://code.visualstudio.com/download) offre funzioni avanzate per una maggiore facilità di modifica.

* Git: questo sistema di controllo della versione è necessario per gestire le modifiche al codice. Se non è installato, scaricalo da [https://git-scm.com](https://git-scm.com).


**Archivio codici:**

Clona l’archivio dei componenti core di Forms adattivi: per aggiungere una lingua è necessaria una libreria client da questo archivio. Per clonare l’archivio:

1. Apri la riga di comando o la finestra del terminale.

1. Passa alla posizione desiderata sul computer in cui desideri memorizzare l’archivio (ad esempio, /adaptive-forms-core-components).

1. Esegui il comando seguente per clonare l’archivio:

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   Questo comando scarica l’archivio e crea una cartella denominata `aem-core-forms-components` sul tuo computer. In questa guida, questa cartella viene definita `[Adaptive Forms Core Components repository]`


## Aggiungi una lingua {#add-localization-support-for-non-supported-locales}

Per aggiungere il supporto per nuove lingue a un modulo adattivo basato su componenti core, effettua le seguenti operazioni:

### Clonare l’archivio Git as a Cloud Service per AEM

1. Apri la riga di comando e scegli una directory per memorizzare l’archivio as a Cloud Service AEM, ad esempio `/cloud-service-repository/`.

1. Esegui il comando seguente per clonare l’archivio:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   Per clonare l’archivio Git, sono necessarie alcune informazioni:

   * **Nome organizzazione**: identifica il team o il progetto in Adobe Experience Manager as a Cloud Service (AEM as a Cloud Service).

   * **ID programma**: specifica il programma associato all’archivio.

   * **Credenziali**: per accedere all’archivio in modo sicuro, devi disporre di un nome utente e di una password (o di un token di accesso personale).

   **Dove si trovano queste informazioni?**

   Per istruzioni dettagliate su come individuare questi dettagli, consulta l’articolo di Adobe Experience League &quot;[Accesso a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot;.

   **Il progetto è pronto.**

   Al termine del comando viene visualizzata una nuova cartella creata nella directory locale. Questa cartella prende il nome dal programma (ad esempio, program-id). Questa cartella contiene tutti i file e il codice scaricati dall’archivio Git as a Cloud Service dall’AEM.

   In questa guida, questa cartella viene definita `[AEMaaCS project directory]`.


### Aggiungere le nuove impostazioni locali al servizio di localizzazione della Guida TV

1. Apri la cartella dell’archivio in un editor.

   ![Cartella dell’archivio in un editor](/help/forms/assets/repository-folder-in-an-editor.png)

1. Individua il `Guide Localization Service.cfg.json` file. Questo file controlla le lingue supportate dall’applicazione AEM Forms. È possibile modificare questo file per aggiungere una nuova lingua.

   * **File esistente**: se il file esiste già, individualo nella directory del progetto AEM Forms. La posizione tipica è:

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     Sostituisci `<appid>` con l’ID app specifico del progetto. Puoi trovare `<appid>` per il progetto AEM nel `archetype.properties` file.

     ![Proprietà Archetipo](/help/forms/assets/archetype-properties.png)

   * **Nuovo file**: se il file non esiste, devi crearlo nella stessa posizione indicata in precedenza. Non copiare e incollare il nome del file da questo documento, ma digitarlo manualmente. Nome del file `Guide Localization Service.cfg.json` include spazi. Questo è intenzionale e non è un errore di battitura nella documentazione.

     Di seguito è riportato un esempio di file con l&#39;elenco delle impostazioni internazionali supportate da OOTB:

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. Aggiungi al file il codice locale per la lingua desiderata.
   1. Utilizza il [Elenco dei codici ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) per trovare il codice di due lettere che rappresenta la lingua desiderata.

   1. Includi il codice locale in `Guide Localization Service.cfg.json` file. Di seguito sono riportati alcuni esempi:

      * Lingue da sinistra a destra:
         * Inglese (Stati Uniti): en-US
         * Spagnolo (Spagna): es-ES
         * Francese (Francia): fr-FR
      * Lingue da destra a sinistra:
         * Arabo (Emirati Arabi Uniti): ar-ae
         * Ebraico: he (o iw come riferimento storico)
         * Farsi: fa

1. Dopo aver apportato le modifiche, assicurati che `Guide Localization Service.cfg.json` il file è formattato correttamente come file JSON valido. Errori nella formattazione JSON possono impedirne il corretto funzionamento. Salva il file.



### Utilizzo della libreria client di esempio per una facile aggiunta delle impostazioni internazionali

AEM Forms fornisce un’utile libreria client di esempio, `clientlib-it-custom-locale`, per semplificare l&#39;aggiunta di nuove impostazioni internazionali. Questa libreria fa parte di [Archivio dei componenti core di Forms adattivi](https://github.com/adobe/aem-core-forms-components), disponibile su GitHub.


Prima di iniziare, assicurati di disporre di una copia locale [Archivio dei componenti core di Forms adattivi]. In caso contrario, puoi facilmente clonarlo utilizzando Git con il seguente comando:

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

Questo comando scarica l’intero archivio, inclusa la libreria clientlib-it-custom-locale, in una directory denominata aem-core-forms-components sul computer.

![Directory dell’archivio dei Componenti core Forms adattivi sul computer locale](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### Integrare la libreria client di esempio

Ora, incorporiamo il `clientlib-it-custom-locale` libreria nel vostro AEM as a Cloud Service, [Directory del progetto AEMaaCS]:

1. Individua la libreria client di esempio:

   Nella copia locale del [Archivio dei componenti core di Forms adattivi], passa al seguente percorso:

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. Copiare e incollare la libreria:

   1. Copia il `clientlib-it-custom-locale` cartella.

      ![Copia di clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. Passa alla seguente directory all’interno della [Directory del progetto AEMaaCS]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **Importante**: Sostituisci `<app-id>` con l’ID effettivo dell’applicazione.

   1. Incolla il copiato `clientlib-it-custom-locale` in questa directory.

      ![Incollare clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)


### Crea un file per la nuova lingua:

1. Passare alla directory delle impostazioni internazionali:

   All’interno del tuo `[AEMaaCS project directory]`, passa al seguente percorso:

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **Importante**: Sostituisci `<program-id>` con l&#39;ID applicazione effettivo.

1. Individua il file di esempio in lingua inglese:

   AEM Forms fornisce una [file locale inglese di esempio (.json) su GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   Il file in lingua inglese include il set di stringhe predefinito come riferimento. Il file specifico della lingua deve simulare la struttura del file in lingua inglese.

   Per lingue come l&#39;arabo, l&#39;ebraico e il farsi, il testo legge da destra a sinistra (RTL) invece che da sinistra a destra (LTR) come l&#39;inglese. Per garantire la corretta visualizzazione dei moduli in queste lingue, si consiglia di utilizzare i file locali di esempio come guida. Questi file forniscono un riferimento per la formattazione di testo, date e altri elementi per le lingue RTL. È possibile trovare i file delle impostazioni locali di esempio per:

   * [Arabo](/help/forms/assets/ar-ae.json)
   * [Ebraico](/help/forms/assets/he.json)
   * [Farsi](/help/forms/assets/fa.json)

   Sfruttando questi file di esempio, è possibile garantire che i moduli forniscano un’esperienza fluida agli utenti che lavorano in lingue RTL.


1. Creare il file delle impostazioni internazionali:

   1. Crea un nuovo file .json all’interno di `i18n` directory.
   1. Denomina il file utilizzando il codice locale appropriato per la lingua desiderata (ad esempio, fr-FR.json per il francese e ar-ae.json per l’arabo). La struttura di questo file deve rispecchiare il file delle impostazioni locali in inglese.


1. Struttura e traduzione:

   1. Apri il file appena creato in un editor di testo.

   1. Sostituisci i valori in inglese con le traduzioni corrispondenti per la tua lingua di destinazione.

   1. Una volta completata la traduzione delle stringhe, salva il file.




### Aggiunta del supporto delle impostazioni locali al dizionario

Questo passaggio si applica solo alle lingue diverse da quelle comunemente supportate: inglese (en), tedesco (de), spagnolo (es), francese (fr), italiano (it), portoghese brasiliano (pt-br), cinese (semplificato - zh_cn), cinese (tradizionale - zh_tw), giapponese (ja) e coreano (ko_kr).

1. Individua la cartella di configurazione:

   Passa alla seguente directory nel [Directory del progetto AEMaaCS]:

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. Crea le cartelle necessarie (se mancanti):

   Se il `etc` la cartella non esiste in `jcr_root` cartella, creala. Interno `etc`, crea un’altra cartella denominata `languages` se manca.

1. Creare il file di configurazione delle impostazioni locali:

   All&#39;interno del `languages` cartella, crea un nuovo file denominato `.content.xml`. Non copiare e incollare il nome del file da questo documento, ma digitarlo manualmente.

   ![crea un nuovo file denominato `.content.xml`](etc-content-xml.png)

   Apri questo file e incolla il seguente contenuto, sostituendo [LOCALE_CODE] con il codice locale effettivo (ad esempio, ar-ae per l’arabo).


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   AVVISO: non sostituire l&#39;elenco esistente. Aggiungi invece il nuovo codice locale tra parentesi quadre, separate da virgole, come segue (utilizzando ar-ae come esempio):

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. Includi le nuove cartelle nel file filter.xml:

   Accedi a `/ui.content/src/main/content/meta-inf/vault/filter.xml` file nel tuo [Directory del progetto AEMaaCS].

   Apri il file e aggiungi la seguente riga alla fine:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Aggiungi le cartelle create in `filter.xml` in `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

1. Salva il file.

### Distribuire le nuove impostazioni locali create nell&#39;ambiente AEM

Ora tutti potete utilizzare le nuove impostazioni internazionali con il vostro Forms adattivo. È possibile

* Mettere in funzione l&#39;AEM as a Cloud Service, [Directory del progetto AEMaaCS], nell&#39;ambiente di sviluppo locale per provare la nuova configurazione locale nel computer locale. Per implementare nell’ambiente di sviluppo locale:

   1. Assicurati che l’ambiente di sviluppo locale sia operativo. Se non hai già configurato un ambiente di sviluppo locale, consulta la guida su [Configurare l’ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Aprire la finestra del terminale o il prompt dei comandi.

   1. Accedi a [Directory del progetto AEMaaCS]

   1. Esegui il comando seguente:

      ```
      mvn -PautoInstallPackage clean install
      ```

* Mettere in funzione l&#39;AEM as a Cloud Service, [Directory del progetto AEMaaCS], nell&#39;ambiente di Cloud Service. Per eseguire l’implementazione nell’ambiente di Cloud Service:

   1. Eseguire il commit delle modifiche:

      Dopo aver aggiunto la nuova configurazione delle impostazioni locali, esegui il commit delle modifiche con un messaggio Git chiaro che descrive l’aggiunta delle impostazioni locali (ad esempio, &quot;È stato aggiunto il supporto per [Nome lingua]&quot;).

   1. Distribuisci il codice aggiornato:

      Attiva una distribuzione del codice tramite [pipeline full stack esistente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline). In questo modo viene automaticamente creato e distribuito il codice aggiornato con il nuovo supporto delle impostazioni internazionali.

      Se non hai già configurato una pipeline, consulta la guida su [come impostare una pipeline per AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).


## Anteprima di un modulo adattivo con le nuove impostazioni internazionali aggiunte

Questi passaggi ti guidano attraverso l’anteprima di un modulo adattivo con le nuove impostazioni locali aggiunte:

1. Accedi all’istanza as a Cloud Service di AEM Forms.
1. Vai a **Forms** >  **Forms e documenti**.
1. Seleziona un modulo adattivo e fai clic su **Aggiungi dizionario** e **Aggiungi dizionario a progetto di traduzione** viene visualizzata la procedura guidata.
1. Specifica la **Titolo progetto** e seleziona la **Lingue di destinazione** dal menu a discesa nella **Aggiungi dizionario a progetto di traduzione** procedura guidata.
1. Clic **Fine** ed esegui il progetto di traduzione creato.
1. Vai a **Forms** >  **Forms e documenti**.
1. Seleziona il modulo adattivo e scegli il **Anteprima come HTML** opzione.
1. Aggiungi `&afAcceptLang=<locale-name>` all’URL di anteprima e premi il tasto Invio. Sostituisci `<locale-name>` con il codice locale effettivo. Il modulo adattivo viene visualizzato nella lingua specificata.

## Procedure consigliate per il supporto della nuova localizzazione {#best-practices}

* L’Adobe consiglia di creare un progetto di traduzione dopo la creazione di un modulo adattivo. Ciò semplifica il processo di localizzazione.
* Quando i componenti Casella numerica e Selettore data vengono convertiti in una lingua specifica, possono verificarsi problemi di formattazione. Per attenuare questo problema, è necessario **Lingua** è stata incorporata nella finestra di dialogo Configura di [Componente selettore data](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input#formats-configure-tab) e [Componente casella numerica](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab).


* Gestione dei nuovi campi:

   * **Traduzione automatica**: se utilizzi la traduzione automatica, devi ricreare il dizionario e[esegui il progetto di traduzione](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) dopo aver aggiunto nuovi campi a un modulo adattivo esistente. I nuovi campi aggiunti dopo il progetto di traduzione iniziale non vengono tradotti.

   * **Traduzione umana**: per i flussi di lavoro di traduzione umana, esporta il dizionario utilizzando l’interfaccia utente in `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. Aggiorna il dizionario per i nuovi campi e carica la versione rivista.


## Consulta anche {#see-also}

{{see-also}}

* [Genera documento di record per Adaptive Forms](/help/forms/generate-document-of-record-core-components.md)
* [Aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

