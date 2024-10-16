---
title: Ambienti di sviluppo rapidi
description: Scopri come utilizzare gli ambienti di sviluppo rapido per le iterazioni di sviluppo rapido in un ambiente cloud.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: fd57437b16a87de2b279b0f8bc10c12a7d3f721a
workflow-type: tm+mt
source-wordcount: '4537'
ht-degree: 3%

---

# Ambienti di sviluppo rapidi {#rapid-development-environments}

Per distribuire le modifiche, gli ambienti di sviluppo cloud attuali richiedono l’utilizzo di un processo che utilizza regole estese di qualità e sicurezza del codice, denominate pipeline CI/CD. Per le situazioni in cui sono necessari cambiamenti rapidi e iterativi, Adobe ha introdotto ambienti di sviluppo rapido (RDE, Rapid Development Environments).

Gli RDE consentono agli sviluppatori di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale.

Una volta testate in un RDE, le modifiche possono essere distribuite in un ambiente di sviluppo cloud regolare tramite la pipeline Cloud Manager.

>[!NOTE]
> Contatta gli sviluppatori RDE sul nostro [canale Discord](https://discord.com/channels/1131492224371277874/1245304281184079872). Puoi porre domande o fornire feedback su argomenti RDE.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Sono disponibili altri video che mostrano [come configurarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [come utilizzarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) e il [ciclo di vita dello sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) utilizzando RDE.

## Introduzione {#introduction}

Gli RDE possono essere utilizzati per codice, contenuto e configurazioni Apache o Dispatcher. A differenza dei normali ambienti di sviluppo cloud, gli sviluppatori possono utilizzare strumenti della riga di comando locali per sincronizzare il codice generato localmente con un RDE.

A ogni programma viene fornito un RDE. Se sono presenti account Sandbox, vengono sospesi dopo alcune ore di non utilizzo.

Al momento della creazione, gli RDE vengono impostati sulla versione di Adobe Experience Manager (AEM) più recente disponibile. Un ripristino RDE, che può essere eseguito utilizzando Cloud Manager, esegue un ciclo RDE e lo imposta sulla versione dell’AEM disponibile più di recente.

In genere, un RDE viene utilizzato da un singolo sviluppatore in un determinato momento, per testare e eseguire il debug di una funzione specifica. Al termine della sessione di sviluppo, è possibile ripristinare lo stato predefinito dell’RDE per l’utilizzo successivo.

Ulteriori RDE possono essere concessi in licenza per programmi di produzione (non sandbox).

## Abilitazione di RDE in un programma {#enabling-rde-in-a-program}

Segui questi passaggi per utilizzare Cloud Manager per creare un RDE per il programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma al quale si desidera aggiungere un RDE per visualizzarne i dettagli.

   * Gli RDE possono essere aggiunti sia ai [programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) che ai [programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

1. Per aggiungere un ambiente, dalla pagina **Panoramica programma**, accedi alla scheda **Ambienti** e fai clic su **Aggiungi ambiente**.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

     ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente** che viene visualizzata:

   * Seleziona **Sviluppo rapido** nell&#39;intestazione **Seleziona tipo di ambiente**.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dopo il tipo di ambiente.
   * Specifica un **Nome** per l&#39;ambiente.
   * Fornisci una **Descrizione** facoltativa per l&#39;ambiente.
   * Seleziona un’**Area geografica cloud**.

   ![Finestra di dialogo Aggiungi ambiente](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Nella schermata **Panoramica** il nuovo ambiente viene ora visualizzato nella scheda **Ambienti**.

Al momento della creazione, gli RDE sono impostati sulla versione AEM più recente disponibile. Un ripristino RDE, che può essere eseguito anche utilizzando Cloud Manager, esegue un ciclo RDE e lo imposta sulla versione di AEM disponibile più di recente.

Per ulteriori informazioni sull&#39;utilizzo di Cloud Manager per la creazione di ambienti, la gestione degli utenti che possono accedervi e l&#39;assegnazione di domini personalizzati, vedere [la documentazione di Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Installazione degli strumenti della riga di comando RDE {#installing-the-rde-command-line-tools}

Dopo aver aggiunto un RDE per il programma utilizzando Cloud Manager, è possibile interagire con esso impostando gli strumenti della riga di comando come descritto nei passaggi seguenti:

>[!IMPORTANT]
>
>Assicurati di aver installato la versione 20 di [Node e NPM](https://nodejs.org/it/download/), ad Adobe I/O CLI e i relativi plug-in per funzionare correttamente.


1. Installa gli strumenti CLI Adobe I/O in base a questa [procedura](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Installare il plug-in RDE AEM strumenti CLI Adobe I/O:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Accedere utilizzando il client aio.

   ```
   aio login
   ```
   Le informazioni di accesso (token) vengono memorizzate nella configurazione globale dell&#39;aio e pertanto supportano un solo account di accesso e un&#39;unica organizzazione. Se desideri utilizzare più RDE che richiedono login o organizzazioni diversi, segui questo esempio introducendo contesti.

   <details><summary>Segui questo esempio per impostare un contesto locale per uno degli accessi RDE</summary>
   Per memorizzare localmente le informazioni di accesso in un file .aio nella directory corrente all'interno di un contesto specifico, eseguire la procedura seguente. Un contesto è anche un modo intelligente di impostare un ambiente CI/CD o uno script.  Per utilizzare questa funzione, assicurarsi di utilizzare almeno aio-cli versione 10.3.1. Aggiornalo utilizzando `npm install -g @adobe/aio-cli`

   Creiamo un contesto denominato &quot;mycontext&quot; che viene quindi impostato come contesto predefinito utilizzando il plug-in di autenticazione prima di chiamare il comando di accesso.

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```


   >[!NOTE]
   > Il comando di accesso con l&#39;opzione `--no-open` restituirà un URL nel terminale invece di aprire il browser predefinito. Così puoi copiarlo e aprirlo con una finestra **incognito** del browser. In questo modo, la sessione attualmente connessa nella normale finestra del browser rimarrà intatta e potrai assicurarti di utilizzare l’accesso e l’organizzazione specifici necessari per il tuo contesto.

   Con il primo comando viene creata una nuova configurazione del contesto di accesso, denominata `mycontext`, nel file di configurazione locale di `.aio`. Se necessario, viene creato il file. Con il secondo comando il contesto `mycontext` viene impostato come &quot;corrente&quot;, ovvero come predefinito.

   Con questa configurazione attivata, il comando di accesso archivia automaticamente i token di accesso nel contesto `mycontext`, mantenendoli quindi locali.

   È possibile gestire più contesti mantenendo le configurazioni locali in più cartelle. In alternativa, è possibile impostare più contesti all’interno di un singolo file di configurazione e passare da un file all’altro modificando il contesto &quot;corrente&quot;.
   </details>

1. Configura il plug-in RDE per utilizzare la tua organizzazione, il tuo programma e il tuo ambiente. Il comando di configurazione riportato di seguito fornirà all&#39;utente un elenco interattivo di programmi della propria organizzazione e mostrerà gli ambienti RDE di tale programma tra cui scegliere.

   ```
   aio aem:rde:setup
   ```

   Il passaggio di configurazione può essere ignorato se l’obiettivo è quello di utilizzare un ambiente con script, nel qual caso i valori dell’organizzazione, del programma e dell’ambiente possono essere inclusi in ciascun comando. [Per ulteriori informazioni, vedere i comandi rde seguenti](#rde-cli-commands).

### Configurazione interattiva {#installing-the-rde-command-line-tools-interactive}

Il comando di installazione chiederà se la configurazione fornita deve essere memorizzata localmente o globalmente.

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

Scegli `no` per
* archiviare l&#39;organizzazione, il programma e l&#39;ambiente a livello globale nella configurazione aio.
* utilizzare un solo RDE.

Scegli `yes` per
* archiviare l&#39;organizzazione, il programma e l&#39;ambiente localmente nella directory corrente, in un file `.aio`. È utile se desideri eseguire il commit del file nel controllo della versione in modo che altri utenti che clonano l’archivio Git possano utilizzarlo.
* utilizzare molti RDE, in modo che il passaggio a un’altra directory utilizzi tale configurazione.
* utilizza la configurazione in un contesto programmatico come uno script, che può farvi riferimento.


Una volta selezionata la configurazione locale o globale, il comando di configurazione tenterà di leggere l’ID organizzazione dall’accesso corrente e quindi di leggere i programmi dell’organizzazione. Nel caso in cui l’organizzazione non possa essere trovata, puoi inserirla manualmente insieme ad alcune indicazioni.

```
 Selected only organization: XYXYXYXYXYXYXYXXYY
 retrieving programs of your organization ...
```

Una volta recuperati i programmi, l’utente può selezionare dall’elenco e anche digitare per filtrare.
Quando il programma è stato selezionato, viene elencato un elenco di ambienti RDE tra cui scegliere.
Se è disponibile un solo programma e/o ambiente RDE, viene selezionato automaticamente.

Per visualizzare il contesto dell’ambiente corrente, esegui:

```aio aem rde setup --show```

Il comando risponderà con un risultato simile al seguente:

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### Procedura di configurazione manuale in un ambiente non interattivo {#manual-setup}

Per gli ambienti in cui nessun utente può eseguire il comando di configurazione in modo interattivo come descritto sopra (ad esempio CI/CD o script), i tre parametri per l’organizzazione, il programma e l’ambiente possono essere configurati manualmente come indicato nei passaggi seguenti.


<details>
  <summary>Espandi per trovare dettagli su come configurare manualmente</summary>

1. Configura l’ID organizzazione e sostituisci la stringa alfanumerica con il tuo ID organizzazione.

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * Puoi cercare il tuo ID organizzazione utilizzando il metodo documentato in [Visualizza ID organizzazione](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Quindi, configura l’ID del programma:

   `aio config:set cloudmanager_programid 12345`

1. Quindi, configura l’ID ambiente a cui verrà allegato l’RDE:

   `aio config:set cloudmanager_environmentid 123456`

1. Al termine della configurazione del plug-in, accedi eseguendo

   `aio login`

   Per questi passaggi è necessario essere membri del profilo di prodotto **Sviluppatore - Cloud Service** di Cloud Manager. Per ulteriori dettagli, vedere [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager - Assegnazione del profilo di prodotto sviluppatore](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer).

Per ulteriori informazioni e dimostrazioni, guarda il video tutorial [su come impostare un RDE (06:24)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html).
</details>

## Utilizzo di RDE durante lo sviluppo di una nuova feature {#using-rde-while-developing-a-new-feature}

L’Adobe consiglia il seguente flusso di lavoro per lo sviluppo di una nuova funzione:

* Una volta raggiunta un’attività cardine intermedia e convalidata correttamente localmente con l’SDK di AEM as a Cloud Service, invia il codice a un ramo della funzione Git. Il ramo non deve ancora far parte della riga principale, anche se l’impegno su Git è facoltativo. Ciò che costituisce un &quot;traguardo intermedio&quot; varia in base alle abitudini del team. Gli esempi includono alcune nuove righe di codice, mezza giornata di lavoro o il completamento di una sottofunzione.

* Reimpostare l&#39;RDE se è stato utilizzato da un&#39;altra funzionalità e si desidera [reimpostarlo su uno stato predefinito](#reset-rde). <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->L&#39;operazione di ripristino richiede alcuni minuti e tutti i contenuti e il codice esistenti vengono eliminati. È possibile utilizzare il comando RDE status per confermare che RDE è pronto. L’RDE viene fornito con la versione più recente dell’AEM.

  >[!IMPORTANT]
  >
  > Se gli ambienti di staging e produzione non ricevono aggiornamenti automatici della versione dell’AEM e sono in esecuzione rispetto alla versione più recente della versione dell’AEM, il codice in esecuzione sull’RDE potrebbe non corrispondere al funzionamento del codice nell’ambiente di staging e produzione. In questo caso, è particolarmente importante eseguire un test approfondito del codice sulla gestione temporanea prima di distribuirlo alla produzione.


* Utilizzando l&#39;interfaccia della riga di comando RDE, sincronizzare il codice locale con RDE. Le opzioni includono l’installazione di un pacchetto di contenuti, un bundle specifico, un file di configurazione OSGI, un file di contenuti e un file zip di una configurazione Apache/Dispatcher. È inoltre possibile fare riferimento a un pacchetto di contenuti remoto. Per ulteriori informazioni, vedere [Strumenti della riga di comando RDE](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands). È possibile utilizzare il comando di stato per verificare che la distribuzione sia stata eseguita correttamente. Facoltativamente, utilizza Gestione pacchetti per installare i pacchetti di contenuti.

* Verifica il codice nell’RDE. Gli URL Author e Publish sono disponibili in Cloud Manager.

* Se il codice non si comporta come previsto, utilizza tecniche di debug standard per comprendere il problema e apportare le modifiche appropriate. Senza eseguire il commit delle modifiche del codice in Git (poiché non sono state convalidate), utilizza la CLI locale per sincronizzare il codice in RDE. Continua a ripetere l’iterazione fino a quando il problema non viene risolto.

* Una volta che il codice si comporta come previsto, esegui il commit del codice nel ramo della funzione Git.

* Il codice sincronizzato con RDE non utilizza una pipeline Cloud Manager, pertanto ora devi utilizzare una pipeline non di produzione Cloud Manager per distribuire il ramo della funzione Git nell’ambiente di sviluppo cloud. In questo modo, si verifica che il codice passi i gate di qualità Cloud Manager e si ha la certezza che il codice venga successivamente distribuito correttamente utilizzando la pipeline di produzione Cloud Manager.

* Ripeti i passaggi precedenti per ogni fase cardine intermedia fino a quando tutto il codice per la funzione non è pronto ed è eseguito correttamente sia nell’ambiente RDE che in quello di sviluppo cloud.

* Distribuisci il codice in produzione tramite la pipeline di produzione Cloud Manager.

## Utilizzo di RDE per eseguire il debug di una feature esistente {#use-rde-to-debug-an-existing-feature}

Il flusso di lavoro è simile allo sviluppo di una nuova funzione. La differenza è che il codice da sincronizzare in RDE rifletterebbe l’etichetta Git di qualsiasi elemento inviato all’ambiente in cui è stato trovato il problema. Inoltre, può essere utile distribuire contenuti corrispondenti all’ambiente a monte. Ciò può essere ottenuto esportando e importando pacchetti di contenuti.

## Più sviluppatori che collaborano allo stesso RDE {#multiple-developers-collaborating-on-the-same-rde}

Un RDE supporta un singolo progetto alla volta. Poiché il codice viene sincronizzato da un ambiente di sviluppo locale all’ambiente RDE, è più naturale per uno sviluppatore utilizzarlo da solo in un determinato momento.

Tuttavia, con un’attenta coordinazione, è possibile per più sviluppatori convalidare una funzione specifica o eseguire il debug di un problema specifico. La chiave è che ogni sviluppatore mantiene sincronizzati i propri progetti locali in modo che le modifiche al codice apportate da un particolare sviluppatore siano assorbite dagli altri sviluppatori, altrimenti uno sviluppatore potrebbe inavvertitamente sovrascrivere il codice dell&#39;altro. La strategia consigliata è che ogni sviluppatore esegua il commit delle modifiche in un ramo Git condiviso prima di eseguire la sincronizzazione con l’RDE, in modo che gli altri sviluppatori richiamino le modifiche prima di apportare le proprie.

## Comandi Strumenti riga di comando RDE {#rde-cli-commands}

### Guida/Informazioni generali {#help}

* Per un elenco di comandi, digitare:

  `aio aem:rde`

* Per informazioni dettagliate su un comando, digitare:

  `aio aem rde <command> --help`


### Flag globali {#global-flags}

* Per un output meno dettagliato, utilizza il flag di silenziosità:

  `aio aem rde <command> --quiet`

  In questo modo vengono rimossi alcuni elementi, ad esempio i cursori e le barre di avanzamento, e viene limitata la necessità di input da parte dell&#39;utente.

* Per l’output JSON invece dell’output del registro della console, utilizza il flag json:

  `aio aem rde <command> --json`

  Questo restituisce un JSON valido durante la soppressione di qualsiasi output della console. Vedi gli esempi JSON più avanti.

* Per evitare di configurare le informazioni di connessione RDE utilizzando il comando setup o qualsiasi creazione di configurazione aio, utilizzare i tre flag per l&#39;organizzazione, il programma e l&#39;ambiente:

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  Per eseguire questa operazione è comunque necessario un ```aio login```.

### Implementazione in RDE {#deploying-to-rde}

In questa sezione viene descritto l’utilizzo di RDE CLI per la distribuzione, l’installazione o l’aggiornamento di bundle, configurazioni OSGI, pacchetti di contenuti, singoli file di contenuti e configurazioni Apache o Dispatcher.

Il modello di utilizzo generale è `aio aem:rde:install <artifact>`.

Di seguito sono riportati alcuni esempi:

<u>Distribuzione di un pacchetto di contenuti</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

La risposta per una distribuzione corretta è simile alla seguente:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Facoltativamente, puoi fare riferimento a un archivio remoto:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Per impostazione predefinita, gli artefatti vengono distribuiti sia sul livello di authoring che su quello di pubblicazione, ma il flag &quot;-s&quot; può essere utilizzato per individuare un livello specifico.

Qualsiasi pacchetto AEM può essere distribuito, ad esempio pacchetti con codice, contenuto o un [pacchetto contenitore](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (detto anche pacchetto &quot;all&quot;).

>[!IMPORTANT]
>
>La configurazione Dispatcher per il progetto WKND non viene distribuita tramite l’installazione del pacchetto di contenuti sopra indicata. Distribuiscilo separatamente seguendo i passaggi &quot;Distribuzione di una configurazione Apache/Dispatcher&quot;.

<u>Distribuzione di una configurazione OSGI</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

In cui la risposta per una distribuzione corretta è simile alla seguente:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Distribuzione di un bundle</u>

Per distribuire un bundle, utilizza:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

In cui la risposta per una distribuzione corretta è simile alla seguente:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Distribuzione di un file di contenuto</u>

Per distribuire un file di contenuto, utilizza:

`aio aem:rde:install world.txt -p /apps/hello.txt`

In cui la risposta per una distribuzione corretta è simile alla seguente:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Distribuzione di una configurazione Apache/Dispatcher</u>

Per questo tipo di configurazione, l’intera struttura di cartelle deve essere sotto forma di un file zip.

Dal modulo `dispatcher` di un progetto AEM, puoi comprimere la configurazione Dispatcher eseguendo il seguente comando maven:

`mvn clean package`

Oppure utilizzando il comando zip seguente dalla directory `src` del modulo `dispatcher`:

`zip -y -r dispatcher.zip .`

Quindi distribuisci la configurazione con questo comando:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>Il comando precedente presuppone che tu stia distribuendo le configurazioni Dispatcher del progetto [WKND](https://github.com/adobe/aem-guides-wknd). Durante la distribuzione della configurazione Dispatcher del progetto, assicurati di sostituire `X.X.X` con il numero di versione del progetto WKND corrispondente o con il numero di versione specifico del progetto.

>[!NOTE]
>
>RDE supporta la configurazione Dispatcher in &quot;modalità flessibile&quot;, ma non la configurazione Dispatcher in &quot;modalità legacy&quot;. Consulta la [documentazione di Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per informazioni sulle due modalità. È inoltre possibile consultare la documentazione relativa alla [migrazione in modalità flessibile](/help/implementing/dispatcher/validation-debug.md#migrating), se non è già stata eseguita.

Una distribuzione corretta genera una risposta simile alla seguente:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

Il codice distribuito in RDE non viene sottoposto a una pipeline Cloud Manager e ai relativi gate di qualità associati. Tuttavia, il codice viene sottoposto ad alcune analisi che segnalano gli errori, come illustrato nell’esempio di codice seguente:

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

L’esempio di codice riportato sopra illustra il comportamento se un bundle non si risolve. In questo caso, è &quot;staging&quot; e viene installato solo se i suoi requisiti (importazioni mancanti, in questo caso) sono soddisfatti tramite l&#39;installazione di un altro codice.

### Distribuzione di codice front-end basato su temi e modelli del sito {#deploying-themes-to-rde}

Gli RDE supportano il codice front-end basato su [temi](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli](/help/sites-cloud/administering/site-creation/site-templates.md) del sito. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando per distribuire pacchetti front-end, anziché la [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) di Cloud Manager utilizzata per altri tipi di ambiente.

Come sempre, crea il pacchetto front-end utilizzando npm:

`npm run build`

Deve generare una cartella `dist/`, in modo che la cartella del pacchetto front-end contenga un file `package.json` e una cartella `dist`:

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
Ora puoi distribuire il pacchetto front-end nell’RDE puntando alla cartella del pacchetto front-end:

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

In alternativa, è possibile comprimere il file `package.json` e la cartella `dist` e distribuire il file zip:

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>La denominazione dei file nel pacchetto front-end deve rispettare le seguenti convenzioni di denominazione:
> * cartella &quot;dist&quot;, per la cartella del pacchetto di output npm build
> * file &quot;package.json&quot;, per il pacchetto dipendenze npm

>[!TIP]
>
> Se hai creato il tuo RDE prima di aprile 2023 e riscontri l’errore &quot;UNEXPECTED_API_ERROR&quot; quando tenti di utilizzare la funzione front-end per la prima volta, prova a eliminare l’ambiente e a crearlo di nuovo.

### Controllo dello stato della RDE {#checking-rde-status}

È possibile utilizzare RDE CLI per verificare se l’ambiente è pronto per essere distribuito in, in quanto tramite il plug-in RDE sono state effettuate delle distribuzioni.

In esecuzione:

`aio aem:rde:status`

Restituisce quanto segue:

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

Se il comando restituisce una nota sulla distribuzione delle istanze, è comunque possibile procedere ed eseguire l&#39;aggiornamento successivo, ma l&#39;ultimo potrebbe non essere ancora visibile nell&#39;istanza.

### Mostra cronologia distribuzione {#show-deployment-history}

Puoi controllare la cronologia delle distribuzioni effettuate nell’RDE eseguendo:

`aio aem:rde:history`

Che restituisce una risposta sotto forma di:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Eliminazione da RDE {#deleting-from-rde}

È possibile eliminare configurazioni e bundle distribuiti in precedenza in RDE tramite gli strumenti CLI. Utilizzare il comando `status` per un elenco degli elementi che è possibile eliminare, che include `bsn` per i bundle e `pid` per le configurazioni a cui fare riferimento nel comando delete.

Ad esempio, se `com.adobe.granite.demo.MyServlet.cfg.json` è stato installato, `bsn` è solo `com.adobe.granite.demo.MyServlet`, senza il suffisso **cfg.json**.

L&#39;eliminazione di pacchetti di contenuti o file di contenuti non è supportata. Per rimuoverli, è necessario reimpostare l&#39;RDE, che lo riporta allo stato predefinito.

Per ulteriori informazioni, consulta l’esempio seguente:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Per ulteriori informazioni e dimostrazioni, vedere l&#39;esercitazione video [utilizzo dei comandi RDE (10:01)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html).

## Registri {#rde-logging}

Analogamente ad altri tipi di ambiente, i livelli di registro possono essere impostati modificando le configurazioni OSGi, anche se, come descritto in precedenza, il modello di distribuzione per gli RDE prevede una riga di comando anziché una distribuzione Cloud Manager. Per ulteriori informazioni su come visualizzare, scaricare e interpretare i registri, consulta la [documentazione di registrazione](/help/implementing/developing/introduction/logging.md).

RDE CLI dispone inoltre di un proprio comando log che può essere utilizzato per configurare rapidamente le classi e i pacchetti da registrare e a quale livello di log. Queste configurazioni possono essere visualizzate come temporanee, in quanto non modificano le proprietà OSGI nel controllo della versione. Questa funzione si concentra sulla suddivisione dei registri in tempo reale, anziché cercare registri di un passato remoto.

L’esempio seguente illustra come visualizzare il livello di authoring, con un pacchetto impostato su un livello di registro di debug e due pacchetti (separati da spazi) impostati su un livello di debug di informazioni. L&#39;output che include un pacchetto **auth** è evidenziato.

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>Se viene visualizzato l&#39;errore `RDECLI:UNEXPECTED_API_ERROR` durante la riproduzione con i comandi dei registri per il servizio Author, reimpostare l&#39;ambiente e riprovare. Questo errore verrà generato se l’ultima operazione di ripristino è stata eseguita prima della fine di maggio 2024.
>
```
>aio aem:rde:reset
>```

Vedere `aio aem:rde:logs --help` per l&#39;insieme completo delle opzioni della riga di comando.

Le funzioni includono:

* dichiarazione dei livelli di registro a livello di pacchetto o classe
* personalizzazione del formato di output del registro
* fino a quattro configurazioni di registro, ciascuna nel proprio terminale
* evidenziazione di registri specifici

Si noti che i registri vengono memorizzati in memoria sull&#39;RDE e che tali registri vengono riciclati e quindi eliminati se non sono in coda o se la rete è troppo lenta.


## Ripristina {#reset-rde}

Se si ripristina la RDE, verranno rimossi dalle istanze di authoring e di pubblicazione tutto il codice personalizzato, le configurazioni e il contenuto. Questo ripristino è utile, ad esempio, se l&#39;RDE è stato utilizzato per testare una caratteristica specifica e si desidera ripristinarla allo stato predefinito in modo da poter testare una caratteristica diversa.

Una reimpostazione imposta l’RDE sulla versione AEM più recente disponibile.

<!-- Alexandru: hiding for now, do not delete

Resetting can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code is deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role to use the reset feature. If not, a reset action results in an error.

### Reset the RDE by way of Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

È possibile utilizzare Cloud Manager per reimpostare la RDE seguendo la procedura riportata di seguito:

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera reimpostare l&#39;RDE.

1. Dalla pagina **Panoramica**, fai clic sulla scheda **Ambienti** nella parte superiore della schermata.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * In alternativa, per passare direttamente alla scheda **Ambienti**, fai clic sul pulsante **Mostra tutto** nella scheda **Ambienti**.

     ![Opzione Mostra tutto](/help/implementing/cloud-manager/assets/environment-showall.png)

1. La finestra **Ambienti** si apre ed elenca tutti gli ambienti del programma.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Fare clic sul pulsante con i puntini di sospensione dell&#39;RDE che si desidera reimpostare, quindi selezionare **Reimposta**.

   ![Visualizza dettagli ambiente](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Confermare la reimpostazione dell&#39;RDE facendo clic su **Reimposta** nella finestra di dialogo.

   ![Conferma reimpostazione](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager conferma mediante un banner l’avvio del processo di ripristino.

   ![Reimposta notifica banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Una volta avviato il processo di ripristino RDE, in genere sono necessari alcuni minuti per completare e ripristinare lo stato predefinito dell’ambiente. Lo stato del processo di ripristino può essere visualizzato in qualsiasi momento nella colonna **Stato** della scheda **Ambienti** o nella finestra **Ambienti**.

![Stato reimpostazione RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

Puoi anche reimpostare l&#39;RDE utilizzando il pulsante con i puntini di sospensione direttamente dalla scheda **Ambienti** nella pagina **Panoramica**.

![Ripristina RDE dalla scheda Ambienti](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Per ulteriori informazioni su come utilizzare Cloud Manager per gestire gli ambienti, consulta [la documentazione di Cloud Manager](/help/implementing/cloud-manager/manage-environments.md).

## Comandi che supportano l’output JSON {#json-commands}

La maggior parte dei comandi supporta il flag globale ```--json``` che sopprime l&#39;output della console e restituisce un JSON valido da elaborare negli script. Di seguito sono riportati alcuni comandi supportati, con esempi dell’output json.

### Stato {#status}

<details>
  <summary>Espandi per visualizzare gli esempi di stato</summary>

#### Un RDE pulito {#clean-rde}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### RDE con alcuni bundle installati {#rde-installed-bundles}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```
</details>

### Installa {#install}

<details>
  <summary>Espandi per visualizzare gli esempi di installazione</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```
</details>

### Elimina {#delete}

<details>
  <summary>Espandi per visualizzare gli esempi di eliminazione</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### Cronologia {#history}

<details>
  <summary>Espandi per visualizzare esempi di cronologia</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```
</details>

### Ripristina {#reset}

<details>
  <summary>Espandi per visualizzare gli esempi di ripristino</summary>

#### Fire and Forget, senza aspettare {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### Attendere il completamento {#wait}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```
</details>

### Riavvia {#restart}

<details>
  <summary>Espandi per visualizzare gli esempi di riavvio</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

## Modalità di esecuzione {#runmodes}

La configurazione OSGI specifica per RDE può essere applicata utilizzando i suffissi sul nome della cartella, come negli esempi seguenti:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Per informazioni generali sulle modalità di esecuzione, vedere la [documentazione sulle modalità di esecuzione](/help/implementing/deploying/overview.md#runmodes).

>[!NOTE]
>
>La configurazione OSGI RDE è univoca in quanto eredita i valori di tutte le proprietà OSGI dichiarate dalla modalità di esecuzione `dev` del bundle.

Gli RDE sono distinti da altri ambienti in quanto il contenuto può essere installato in una cartella install.rde (o install.author.rde o install.publish.rde) in /apps. Questo consente di eseguire il commit del contenuto in Git e distribuirlo all’RDE utilizzando gli strumenti della riga di comando.

## Popolamento con il contenuto {#populating-content}

Quando un RDE viene reimpostato, tutto il contenuto viene rimosso e quindi, se desiderato, è necessario eseguire un’azione esplicita per aggiungere contenuto. Come best practice, è consigliabile assemblare un set di contenuti da utilizzare come contenuti di prova per convalidare o eseguire il debug delle funzioni nell’RDE. Esistono diverse strategie possibili per popolare l’RDE con tale contenuto:

1. Sincronizzare esplicitamente il pacchetto di contenuti con l&#39;RDE utilizzando gli strumenti della riga di comando

1. Inserisci e conferma il contenuto di esempio in Git all’interno di una cartella install.rde in /apps, quindi sincronizza il pacchetto di contenuti generali con RDE utilizzando gli strumenti della riga di comando.

1. Utilizzare lo strumento [copia contenuto](/help/implementing/developing/tools/content-copy.md) per copiare un set di contenuti definito da ambienti di produzione, stage o sviluppo o da un altro RDE.

1. Utilizzare Gestione pacchetti

Il limite è di 1 GB per la sincronizzazione dei pacchetti di contenuti.


## Quali sono le differenze tra gli RDE e gli ambienti di sviluppo cloud? {#how-are-rds-different-from-cloud-development-environments}

Sebbene l’RDE sia simile per molti aspetti a un ambiente di sviluppo cloud, esistono alcune lievi differenze a livello di architettura per consentire una rapida sincronizzazione del codice. Il meccanismo per ottenere il codice da RDE è diverso: per gli RDE, si sincronizza il codice da un ambiente di sviluppo locale, mentre per gli ambienti di sviluppo cloud, si distribuisce il codice tramite Cloud Manager.

Per questi motivi, dopo aver convalidato il codice in un ambiente RDE, è consigliabile distribuirlo in un ambiente di sviluppo cloud utilizzando la pipeline non di produzione. Infine, verifica il codice prima di distribuirlo con la pipeline di produzione.

Inoltre, tieni presente le seguenti considerazioni:

* Gli RDE non includono un livello di anteprima
* Attualmente gli RDE non supportano il canale prerelease.


## Di quante RDE ho bisogno? {#how-many-rds-do-i-need}

È disponibile un RDE per ogni soluzione concessa in licenza e l’Adobe offre anche RDE aggiuntivi, che possono essere concessi in licenza per programmi di produzione (non sandbox).

Il numero di RDE necessari dipende dalla composizione e dai processi di un’organizzazione. Il modello più flessibile è quello in cui un’organizzazione acquista un RDE dedicato per ciascuno dei propri sviluppatori AEM Cloud Service. In questo modello, ogni sviluppatore può testare il proprio codice sull’RDE senza coordinarsi con gli altri membri del gruppo per determinare se è disponibile un ambiente RDE.

All’estremo opposto, un team con un singolo RDE può utilizzare processi interni per coordinare quali sviluppatori possono utilizzare l’ambiente in un dato momento. Questo può accadere quando uno sviluppatore ha raggiunto una fase cardine della funzione intermedia ed è pronto per la convalida in un ambiente Cloud in cui può apportare rapidamente le modifiche necessarie.

Un modello intermedio è un modello in cui un’organizzazione acquista diversi RDE, pertanto vi è una maggiore probabilità che sia disponibile un RDE inutilizzato. Una strategia potrebbe essere quella di allocare un RDE per team di scrum o per una funzione importante. I processi interni possono essere utilizzati per coordinare l’utilizzo degli ambienti.

## Quali sono le differenze tra AEM Forms Cloud Service Rapid Development Environment (RDE) e altri ambienti? {#how-are-forms-rds-different-from-cloud-development-environments}

Gli sviluppatori Forms possono utilizzare AEM Forms Cloud Service Rapid Development Environment per sviluppare rapidamente Forms adattivo, flussi di lavoro e personalizzazioni quali la personalizzazione di componenti core, integrazioni con sistemi di terze parti e altro ancora. AEM Forms Cloud Service Rapid Development Environment (RDE) non supporta le API di comunicazione. Inoltre, non supporta funzioni e funzionalità che richiedono documenti di record, come la generazione di un documento di record all’invio di un modulo adattivo. Le seguenti funzioni di AEM Forms non sono disponibili in un ambiente di sviluppo rapido (RDE):

* Configurazione di un documento record per un modulo adattivo
* Generazione di un documento record all’invio di un modulo adattivo o con un passaggio del flusso di lavoro
* Inviare un documento record come allegato con l’azione Invia e-mail o con il passaggio E-mail in un flusso di lavoro
* Utilizzo di Adobe Sign in un modulo adattivo o in un passaggio del flusso di lavoro
* API di comunicazione

>[!NOTE]
>
> Non c’è differenza tra l’interfaccia utente di Rapid Development Environment (RDE) e altri ambienti di Cloud Service per Forms. Tutte le opzioni relative al documento record, come la selezione di un modello di documento record per un modulo adattivo, continuano a essere visualizzate nell’interfaccia utente. Questi ambienti non dispongono di API di comunicazione e funzionalità per documenti di record per testare tali opzioni. Pertanto, quando scegli un’opzione che richiede API di comunicazione o funzionalità del documento di record, non viene eseguita alcuna azione e viene visualizzato un messaggio di errore.

## Esercitazione RDE

Per informazioni su RDE in AEM as a Cloud Service, consulta l&#39;esercitazione video che illustra [come configurarlo, come utilizzarlo e il ciclo di vita dello sviluppo (01:25)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html).

# Risoluzione dei problemi {#troubleshooting}

## Risoluzione dei problemi RDE (#rde-troublehooting)

### Come ottenere la versione più recente dell’AEM per un RDE esistente {#get-latest-aem-version}

Al momento della creazione, gli RDE vengono impostati sulla versione di Adobe Experience Manager (AEM) più recente disponibile. Un [ripristino RDE,](#reset-rde) che può essere eseguito utilizzando Cloud Manager o il comando `aio aem:rde:reset`, esegue un ciclo RDE e lo imposta sulla versione dell&#39;AEM disponibile più di recente.

## Risoluzione dei problemi del plug-in aio RDE {#aio-rde-plugin-troubleshooting}

### Errori relativi ad autorizzazioni insufficienti {#insufficient-permissions}

Per utilizzare il plug-in RDE, è necessario essere membri del profilo di prodotto Cloud Manager **Developer - Cloud Service**. Per ulteriori dettagli, vedere [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager - Assegnazione del profilo di prodotto sviluppatore](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer).

In alternativa, puoi confermare di disporre di questo ruolo di sviluppatore se puoi accedere alla console per sviluppatori eseguendo questo comando:

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>Se viene visualizzato l&#39;errore `Warning: cloudmanager:* is not a aio command.`, è necessario installare [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) eseguendo il comando seguente:
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

Verificare che l&#39;accesso sia stato completato correttamente eseguendo

`aio cloudmanager:list-programs`

Questo dovrebbe elencare tutti i programmi nella tua organizzazione configurata e confermare che ti è stato assegnato il ruolo corretto.
