---
title: Ambienti di sviluppo rapido
description: Scopri come utilizzare gli ambienti di sviluppo rapido per le iterazioni di sviluppo rapido in un ambiente cloud.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: eb87467b1cd3338a409c2aeded74b3bb38d2e58c
workflow-type: tm+mt
source-wordcount: '5446'
ht-degree: 3%

---

# Ambienti di sviluppo rapido {#rapid-development-environments}

Per distribuire le modifiche, gli ambienti di sviluppo cloud attuali richiedono l’utilizzo di un processo che utilizza regole estese di qualità e sicurezza del codice, denominate pipeline CI/CD. Nelle situazioni in cui sono necessarie modifiche rapide e iterative, Adobe ha introdotto gli ambienti di sviluppo rapido (RDE, Rapid Development Environments).

Gli RDE consentono agli sviluppatori di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale.

Una volta testate in un RDE, le modifiche possono essere distribuite in un ambiente di sviluppo cloud regolare tramite la pipeline Cloud Manager.

Gli ambienti di sviluppo e gli ambienti di sviluppo rapido devono essere limitati allo sviluppo, all’analisi degli errori e ai test funzionali e non devono essere progettati per elaborare carichi di lavoro elevati né grandi quantità di contenuti.

>[!NOTE]
> Gli ambienti di sviluppo rapido devono essere limitati allo sviluppo, all’analisi degli errori e ai test funzionali e non devono essere progettati per elaborare carichi di lavoro elevati né grandi quantità di contenuti.

>[!NOTE]
> Contatta gli sviluppatori RDE sul [canale Discord](https://discord.com/channels/1131492224371277874/1245304281184079872) di Adobe. Puoi porre domande o fornire feedback su argomenti RDE.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Sono disponibili altri video che mostrano [come configurarlo](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup), [come utilizzarlo](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use) e il [ciclo di vita dello sviluppo](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle) utilizzando RDE.

## Introduzione {#introduction}

Gli RDE possono essere utilizzati per codice, contenuto e configurazioni Apache o Dispatcher. A differenza dei normali ambienti di sviluppo cloud, gli sviluppatori possono utilizzare strumenti della riga di comando locali per sincronizzare il codice generato localmente con un RDE.

A ogni programma viene fornito un RDE. Se sono presenti account Sandbox, vengono sospesi dopo alcune ore di non utilizzo.

Al momento della creazione, gli RDE sono impostati sulla versione di Adobe Experience Manager (AEM) più recente disponibile. Un ripristino RDE, che può essere eseguito utilizzando Cloud Manager, esegue un ciclo di tale ripristino e lo imposta sulla versione di AEM più recente disponibile.

In genere, un RDE viene utilizzato da un singolo sviluppatore in un determinato momento, per testare e eseguire il debug di una funzione specifica. Al termine della sessione di sviluppo, è possibile ripristinare lo stato predefinito dell’RDE per l’utilizzo successivo.

Ulteriori RDE possono essere concessi in licenza per programmi di produzione (non sandbox).

## Abilitare RDE in un programma {#enabling-rde-in-a-program}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma al quale si desidera aggiungere un RDE per visualizzarne i dettagli.

   * Gli RDE possono essere aggiunti sia ai [programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) che ai [programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

1. Dalla pagina **Panoramica del programma**, nella scheda **Ambienti**, fai clic su **Aggiungi ambiente**.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

     ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente**, esegui le operazioni seguenti:

   * Seleziona **Sviluppo rapido** nell&#39;intestazione **Seleziona tipo di ambiente**.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dopo il tipo di ambiente.
   * Specifica un **Nome** per l&#39;ambiente.
   * Fornisci una **Descrizione** facoltativa per l&#39;ambiente.
   * Seleziona un’**Area geografica cloud**.

   ![Finestra di dialogo Aggiungi ambiente](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Nella schermata **Panoramica** il nuovo ambiente viene ora visualizzato nella scheda **Ambienti**.

Al momento della creazione, gli RDE sono impostati sulla versione di AEM più recente disponibile. Un ripristino RDE, che può essere eseguito anche utilizzando Cloud Manager, esegue un ciclo di tale ripristino e lo imposta sulla versione di AEM più recente disponibile.

Per ulteriori informazioni sull&#39;utilizzo di Cloud Manager per la creazione di ambienti, la gestione degli utenti che possono accedervi e l&#39;assegnazione di domini personalizzati, vedere [Programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) nella documentazione di Cloud Manager.

## Installare gli strumenti della riga di comando RDE {#installing-the-rde-command-line-tools}

Dopo aver aggiunto un RDE per il programma utilizzando Cloud Manager, è possibile interagire con esso impostando gli strumenti della riga di comando come descritto nei passaggi seguenti:

>[!IMPORTANT]
>
>Assicurati di aver installato la versione 20 di [Node e NPM](https://nodejs.org/en/download/) per il corretto funzionamento della CLI di Adobe I/O (AIO) e dei relativi plug-in.


1. Installare gli strumenti della CLI AIO in base a questa [procedura](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/tools/cli-install).
1. Installare il plug-in AEM RDE degli strumenti della CLI AIO:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Effettua il login utilizzando il client Adobe I/O (AIO).

   ```
   aio login
   ```

   Le informazioni di accesso (token) vengono memorizzate nella configurazione globale dell&#39;aio e pertanto supportano un solo account di accesso e un&#39;unica organizzazione. Se desideri utilizzare più RDE che richiedono diversi accessi o organizzazioni, segui l’esempio seguente introducendo i contesti.

   <details><summary>Segui questo esempio per impostare un contesto locale per uno degli accessi RDE</summary>
   Per memorizzare localmente le informazioni di accesso in un file ".aio" nella directory corrente all'interno di un contesto specifico, eseguire la procedura seguente. Un contesto è anche un modo intelligente di impostare un ambiente CI/CD o uno script.  Per utilizzare questa funzione, assicurarsi di utilizzare almeno aio-cli versione 10.3.1. Aggiornalo utilizzando `npm install -g @adobe/aio-cli`.

   Creare ora un contesto denominato m`ycontext` impostato come contesto predefinito utilizzando il plug-in di autenticazione prima di chiamare il comando di accesso.

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > Il comando di accesso con l&#39;opzione `--no-open` restituisce un URL nel terminale invece di aprire il browser predefinito. Puoi copiarlo e aprirlo con una finestra **incognito** del browser. Questa capacità assicura che la sessione corrente nella finestra principale del browser rimanga invariata, consentendoti di accedere con l’account e l’organizzazione specifici necessari per l’attività.

   Con il primo comando viene creata una nuova configurazione del contesto di accesso, denominata `mycontext`, nel file di configurazione locale di `.aio`. Se necessario, viene creato il file. Con il secondo comando il contesto `mycontext` viene impostato come &quot;corrente&quot;, ovvero come predefinito.

   Con questa configurazione attivata, il comando di accesso archivia automaticamente i token di accesso nel contesto `mycontext`, mantenendoli quindi locali.

   È possibile gestire più contesti mantenendo le configurazioni locali in più cartelle. In alternativa, è possibile impostare più contesti all’interno di un singolo file di configurazione e passare da un file all’altro modificando il contesto &quot;corrente&quot;.
   </details>

1. Configura il plug-in RDE per utilizzare la tua organizzazione, il tuo programma e il tuo ambiente. Il comando di configurazione riportato di seguito fornisce in modo interattivo all&#39;utente un elenco di programmi della propria organizzazione e consente di visualizzare gli ambienti RDE di tale programma tra cui scegliere.

   ```
   aio aem:rde:setup
   ```

   Se utilizzi un ambiente con script, puoi saltare il passaggio di configurazione. In tal caso, includere i valori dell&#39;organizzazione, del programma e dell&#39;ambiente direttamente in ciascun comando. [Per ulteriori informazioni, vedere i comandi RDE seguenti](#rde-cli-commands).

### Configurazione interattiva {#installing-the-rde-command-line-tools-interactive}

Il comando setup richiede se la configurazione fornita deve essere memorizzata localmente o globalmente.

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

Scegli `no` per

* archiviare l&#39;organizzazione, il programma e l&#39;ambiente a livello globale nella configurazione aio.
* utilizzare un solo RDE.

Scegliere `yes` per effettuare le seguenti operazioni:

* Archiviare l&#39;organizzazione, il programma e l&#39;ambiente localmente nella directory corrente, in un file `.aio`. Questo approccio è utile se desideri eseguire il commit del file nel controllo della versione in modo che altri utenti che clonano l’archivio Git possano utilizzarlo.
* Essere in grado di lavorare con molti RDE, in modo che il passaggio a un&#39;altra directory utilizzi tale configurazione.
* Utilizza la configurazione in un contesto programmatico come uno script, che può farvi riferimento.


Una volta selezionata la configurazione locale o globale, il comando di configurazione tenta di leggere l’ID organizzazione dall’accesso corrente e quindi di leggere i programmi dell’organizzazione. Nel caso in cui l’organizzazione non possa essere trovata, puoi inserirla manualmente insieme ad alcune indicazioni.

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

Una volta recuperati i programmi, l’utente può selezionare dall’elenco e anche digitare per filtrare. Quando il programma è selezionato, viene elencato un elenco di ambienti RDE tra cui scegliere. Se è disponibile un solo programma, un solo ambiente RDE o entrambi, viene selezionato automaticamente.

Per visualizzare il contesto dell’ambiente corrente, esegui le seguenti operazioni:

```aio aem rde setup --show```

Il comando risponde con un risultato simile al seguente:

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### Procedura di configurazione manuale in un ambiente non interattivo {#manual-setup}

Negli ambienti in cui nessun utente può eseguire il comando di installazione in modo interattivo (ad esempio CI/CD o script), è necessaria la configurazione manuale. Puoi impostare i parametri di organizzazione, programma e ambiente seguendo la procedura riportata di seguito.


<details>
  <summary>Espandi per trovare dettagli su come configurare manualmente</summary>

1. Configura l’ID organizzazione e sostituisci la stringa alfanumerica con il tuo ID organizzazione.

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * Puoi cercare il tuo ID organizzazione utilizzando il metodo documentato in [Visualizza ID organizzazione](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Quindi, configura l’ID del programma:

   `aio config:set cloudmanager_programid 12345`

1. Quindi, configura l’ID ambiente a cui verrà allegato l’RDE:

   `aio config:set cloudmanager_environmentid 123456`

1. Al termine della configurazione del plug-in, accedi eseguendo

   `aio login`

   Questi passaggi richiedono l&#39;appartenenza al profilo di prodotto Cloud Manager **Developer - Cloud Service**. Per ulteriori dettagli, vedere [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager - Assegnazione del profilo di prodotto sviluppatore](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer).

Per ulteriori informazioni e dimostrazioni, guarda l&#39;esercitazione video [come impostare un RDE (06:24)](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup).
</details>

## Utilizzare RDE durante lo sviluppo di una nuova funzione {#using-rde-while-developing-a-new-feature}

Adobe consiglia di utilizzare il seguente flusso di lavoro per sviluppare una nuova funzione:

* Quando viene raggiunta una milestone intermedia e la sua convalida locale con AEM as a Cloud Service SDK è riuscita, invia il codice a un ramo della funzione Git. Il ramo non deve ancora far parte della riga principale, anche se l’impegno su Git è facoltativo. Ciò che costituisce un &quot;traguardo intermedio&quot; varia in base alle abitudini del team. Gli esempi includono alcune nuove righe di codice, mezza giornata di lavoro o il completamento di una sottofunzione.

* Reimpostare l&#39;RDE se è stato utilizzato da un&#39;altra funzionalità e si desidera [reimpostarlo su uno stato predefinito](#reset-rde). <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->L&#39;operazione di ripristino richiede alcuni minuti e tutti i contenuti e il codice esistenti vengono eliminati. È possibile utilizzare il comando RDE status per confermare che RDE è pronto. Il RDE viene fornito con la versione più recente di AEM.

  >[!IMPORTANT]
  >
  >Se gli ambienti di staging e produzione non ricevono gli aggiornamenti automatici della versione di AEM e sono in ritardo rispetto all’ultima versione, RDE potrebbe eseguire una versione diversa di AEM. Di conseguenza, il comportamento del codice nell’RDE potrebbe non corrispondere al modo in cui funziona nell’ambiente di staging e produzione. In tal caso, è importante eseguire un test approfondito del codice sulla gestione temporanea prima di distribuirlo alla produzione.


* Utilizzando l&#39;interfaccia della riga di comando RDE, sincronizzare il codice locale con RDE. È possibile installare vari tipi di file, tra cui i seguenti:

   * Pacchetti di contenuti
   * Bundle specifici
   * File di configurazione OSGi
   * File di contenuto
   * File ZIP contenenti configurazioni Apache/Dispatcher

  È inoltre possibile fare riferimento a un pacchetto di contenuti remoto. Per ulteriori informazioni, vedere [Strumenti della riga di comando RDE](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands). È possibile utilizzare il comando di stato per verificare che la distribuzione sia stata eseguita correttamente. Facoltativamente, utilizza Gestione pacchetti per installare i pacchetti di contenuti.

* Verifica il codice nell’RDE. Gli URL Author e Publish sono disponibili in Cloud Manager.

* Se il codice non si comporta come previsto, utilizza tecniche di debug standard per comprendere il problema e apportare le modifiche appropriate. Senza confermare le modifiche del codice su Git (poiché non sono state convalidate), utilizza la CLI locale per sincronizzare il codice su RDE. Continua a ripetere l’iterazione fino a quando il problema non viene risolto.

* Una volta che il codice si comporta come previsto, esegui il commit del codice nel ramo della funzione Git.

* Il codice sincronizzato con RDE non utilizza una pipeline di Cloud Manager, pertanto ora devi utilizzare una pipeline non di produzione Cloud Manager per distribuire il ramo della funzione Git nell’ambiente di sviluppo cloud. Questo processo verifica che il codice passi i gate di qualità Cloud Manager e ti consente di essere certo che il codice sia stato successivamente distribuito correttamente utilizzando la pipeline di produzione Cloud Manager.

* Ripeti i passaggi precedenti per ogni fase cardine intermedia fino a quando tutto il codice per la funzione non è pronto ed è eseguito correttamente sia nell’ambiente RDE che in quello di sviluppo cloud.

* Distribuisci il codice in produzione tramite la pipeline di produzione Cloud Manager.

## Utilizzare RDE per eseguire il debug di una funzionalità esistente {#use-rde-to-debug-an-existing-feature}

Il flusso di lavoro è simile allo sviluppo di una nuova funzione. La differenza è che il codice sincronizzato in RDE riflette l’etichetta Git di ciò che è stato inviato all’ambiente in cui si è verificato il problema. Questo flusso di lavoro garantisce coerenza durante l’analisi o la riproduzione del problema. Inoltre, può essere utile distribuire contenuti corrispondenti all’ambiente a monte. Questo approccio può essere ottenuto esportando e importando pacchetti di contenuti.

## Più sviluppatori che collaborano allo stesso RDE {#multiple-developers-collaborating-on-the-same-rde}

Un RDE supporta un singolo progetto alla volta. Poiché il codice viene sincronizzato da un ambiente di sviluppo locale all’ambiente RDE, è più naturale per uno sviluppatore utilizzarlo da solo in un determinato momento.

Tuttavia, con un’attenta coordinazione, è possibile per più sviluppatori convalidare una funzione specifica o eseguire il debug di un problema specifico. La chiave è che ogni sviluppatore mantiene sincronizzati i propri progetti locali in modo che le modifiche del codice apportate da un particolare sviluppatore vengano assorbite dagli altri sviluppatori. In caso contrario, uno sviluppatore potrebbe inavvertitamente sovrascrivere il codice dell’altro. La strategia consigliata è che ogni sviluppatore esegua il commit delle modifiche in un ramo Git condiviso prima di eseguire la sincronizzazione con l’RDE, in modo che gli altri sviluppatori possano richiamare le modifiche prima di apportare le proprie.

## Strumenti della riga di comando RDE Comandi {#rde-cli-commands}

### Guida/Informazioni generali {#help}

* Per un elenco di comandi, digitare:

  `aio aem:rde`

* Per informazioni dettagliate su un comando, digitare:

  `aio aem rde <command> --help`

### Flag globali {#global-flags}

* Per un output meno dettagliato, utilizza il flag di silenziosità:

  `aio aem rde <command> --quiet`

  Questo flag rimuove alcuni elementi, come gli spiner e le barre di avanzamento, e limita la necessità di input da parte dell’utente.

* Per l’output JSON invece dell’output del registro della console, utilizza il flag json:

  `aio aem rde <command> --json`

  Questo flag restituisce un JSON valido durante la soppressione di qualsiasi output della console. Vedi gli esempi JSON più avanti.

* Per evitare di configurare le informazioni di connessione RDE utilizzando il comando setup o qualsiasi creazione di configurazione aio, utilizzare i tre flag per l&#39;organizzazione, il programma e l&#39;ambiente:

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  Richiede l&#39;esecuzione di ```aio login```.

### Distribuisci su RDE {#deploying-to-rde}

Questa sezione spiega come utilizzare RDE CLI per distribuire, installare o aggiornare varie risorse. Queste risorse includono:

* Pacchetti di contenuti
* Configurazioni OSGi
* Bundle
* File di contenuto
* Configurazioni Apache o Dispatcher

Il modello di utilizzo generale è `aio aem:rde:install <artifact>`.

Di seguito sono riportati alcuni esempi:

#### Distribuire un pacchetto di contenuti {#deploy-content-package}

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

La risposta per una distribuzione corretta è simile alla seguente:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Facoltativamente, puoi fare riferimento a un archivio remoto:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Per impostazione predefinita, gli artefatti vengono distribuiti sia sul livello di authoring che su quello di pubblicazione, ma è possibile utilizzare il flag `-s` per impostare come destinazione un livello specifico.

Qualsiasi pacchetto AEM può essere distribuito, ad esempio pacchetti con codice, contenuto o un [pacchetto contenitore](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (detto anche pacchetto &quot;all&quot;).

>[!IMPORTANT]
>
>L’installazione del pacchetto di contenuti di cui sopra non distribuisce la configurazione Dispatcher per il progetto WKND. Distribuiscilo separatamente seguendo i passaggi &quot;Distribuzione di una configurazione Apache/Dispatcher&quot;.

#### Distribuire una configurazione OSGI {#deploy-OSGI-config}

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

In cui la risposta per una distribuzione corretta è simile alla seguente:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

#### Distribuire un bundle {#deploy-bundle}

Per distribuire un bundle, utilizza:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

In cui la risposta per una distribuzione corretta è simile alla seguente:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

#### Distribuire un file di contenuto {#deploy-content-file}

Per distribuire un file di contenuto, utilizza:

`aio aem:rde:install world.txt -p /apps/hello.txt`

In cui la risposta per una distribuzione corretta è simile alla seguente:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

#### Distribuire una configurazione Apache/Dispatcher {#deploy-apache-config}

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

#### Implementa configurazione relativa alla pipeline di configurazione (configurazioni yaml) {#deploy-config-pipeline}

Le configurazioni specifiche dell&#39;ambiente (uno o più file yaml) descritte nell&#39;articolo [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md) possono essere distribuite come segue:

`aio aem:rde:install -t env-config ./my-config-folder`
Dove `my-config-folder` è la cartella principale contenente le configurazioni yaml.

In alternativa, è possibile installare un file zip contenente la struttura della cartella di configurazione:

`aio aem:rde:install -t env-config config.zip`

Si noti che la matrice envTypes del file yaml include il valore `rde`, come nell&#39;esempio seguente:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### Distribuire il codice front-end in base ai temi e ai modelli del sito {#deploying-themes-to-rde}

Gli RDE supportano il codice front-end creato con [temi](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli](/help/sites-cloud/administering/site-creation/site-templates.md) del sito. Invece di utilizzare la [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) di Cloud Manager come altri tipi di ambiente, gli RDE distribuiscono pacchetti front-end utilizzando una direttiva della riga di comando.

Come sempre, crea il pacchetto front-end utilizzando npm:

`npm run build`

Genera una cartella `dist/`, quindi la cartella del pacchetto front-end contiene un file `package.json` e una cartella `dist`:

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```

Ora puoi distribuire il pacchetto front-end nell’RDE puntando alla cartella del pacchetto front-end nel modo seguente:

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
>
> * Cartella `dist`, per la cartella del pacchetto di output di compilazione npm
> * `package.json` file, per il pacchetto dipendenze npm

>[!TIP]
>
>Se hai creato la RDE prima di aprile 2023 e incontri `UNEXPECTED_API_ERROR` quando utilizzi la funzione front-end per la prima volta, la causa potrebbe essere una configurazione obsoleta. Per risolvere questo problema, elimina l’ambiente e creane uno nuovo.

### Controllare lo stato della RDE {#checking-rde-status}

È possibile utilizzare RDE CLI per verificare se l’ambiente è pronto per essere distribuito in, in quanto tramite il plug-in RDE sono state effettuate delle distribuzioni.

Esecuzione di quanto segue:

`aio aem:rde:status`

Restituisce con quanto segue:

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

### Mostra cronologia di distribuzione {#show-deployment-history}

Puoi controllare la cronologia delle distribuzioni effettuate nell’RDE eseguendo:

`aio aem:rde:history`

Che restituisce una risposta sotto forma di:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Elimina da RDE {#deleting-from-rde}

È possibile utilizzare gli strumenti CLI per eliminare le configurazioni e i bundle distribuiti in precedenza nell&#39;RDE. Utilizzare il comando `status` per un elenco degli elementi che è possibile eliminare, che include `bsn` per i bundle e `pid` per le configurazioni a cui fare riferimento nel comando delete.

Ad esempio, se `com.adobe.granite.demo.MyServlet.cfg.json` è stato installato, `bsn` è solo `com.adobe.granite.demo.MyServlet`, senza il suffisso **cfg.json**.

L&#39;eliminazione di pacchetti di contenuti o file di contenuti non è supportata. Per rimuoverli, reimpostare l&#39;RDE e riportarlo allo stato predefinito.

Per ulteriori informazioni, consulta l’esempio seguente:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Per ulteriori informazioni e dimostrazioni, vedere l&#39;esercitazione video [utilizzo dei comandi RDE (10:01)](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use).


## Distribuire in un RDE da provider Git esterni {#deploy-to-rde}

>[!NOTE]
>
>Questa funzione è disponibile tramite il programma Beta. Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a [CloudManager_BYOG@adobe.com](mailto:cloudmanager_byog@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID. Se ti trovi in una struttura di archivio privata/pubblica o aziendale, assicurati di specificare la piattaforma Git che desideri utilizzare.

Cloud Manager supporta la distribuzione di codice in un RDE direttamente da provider Git esterni quando si utilizza la configurazione [Bring Your Own Git (BYOG)](/help/implementing/cloud-manager/managing-code/external-repositories.md).

La distribuzione degli RDE da un archivio Git esterno richiede quanto segue:

* Utilizzo di un archivio Git esterno integrato con Cloud Manager (configurazione BYOG).
* È necessario eseguire il provisioning di uno o più ambienti RDE per il progetto.
* Se utilizzi `github.com`, devi rivedere e accettare l&#39;installazione aggiornata dell&#39;app GitHub per concedere le nuove autorizzazioni richieste.

**Note sull&#39;utilizzo**

* La distribuzione in RDE è attualmente supportata solo per i pacchetti di contenuti AEM e Dispatcher.
* La distribuzione di altri tipi di pacchetti (ad esempio, pacchetti completi di applicazioni AEM) non è ancora supportata.
* Attualmente, il ripristino di un ambiente RDE utilizzando un commento non è supportato. È invece necessario utilizzare il comando di reimpostazione della CLI AIO esistente, come [descritto qui](/help/implementing/developing/introduction/rapid-development-environments.md#reset-the-rde-command-line).

**Come funziona**

1. **Messaggio di convalida della qualità del codice.**

   Quando una richiesta di pull (PR) attiva l’esecuzione di una pipeline di qualità del codice, i risultati della convalida indicano se la distribuzione può procedere a un ambiente RDE.

   Come si presenta su GitHub Enterprise:
   ![Messaggio di convalida della qualità del codice su GitHub Enterprise](/help/implementing/developing/introduction/assets/rde-gitlab-code-quality-validation-message.png)

   Come si presenta su GitLab:
   ![Messaggio di convalida della qualità del codice su GitLab](/help/implementing/developing/introduction/assets/rde-gitlab-code-quality-validation-message.png)

   Aspetto di Bitbucket:
   ![Messaggio di convalida della qualità del codice in Bitbucket](/help/implementing/developing/introduction/assets/rde-bitbucket-code-quality-validation-message.png)

1. **Attiva la distribuzione tramite un commento.**

   Per avviare la distribuzione, aggiungere un commento alla PR nel seguente formato: `deploy on rde-environment-<envName>`

   ![Attiva la distribuzione tramite un commento](/help/implementing/developing/introduction/assets/rde-trigger-deployment-using-comment.png)

   `<envName>` deve corrispondere al nome di un ambiente RDE esistente. Se il nome non viene trovato, viene restituito un commento che indica che l’ambiente non è valido.

   Se lo stato dell’ambiente non è pronto, viene visualizzato il seguente commento:

   ![Ambiente non pronto per la distribuzione](/help/implementing/developing/introduction/assets/rde-environment-not-ready.png)

1. **Verifica dell&#39;ambiente e distribuzione degli artefatti.**

   Se il RDE è pronto, Cloud Manager invia un nuovo assegno al PR.

   Come si presenta su GitHub Enterprise:

   ![Stato dell&#39;ambiente su GitHub](/help/implementing/developing/introduction/assets/rde-github-environment-status-is-ready.png)

   Come si presenta su GitLab:

   ![Stato dell&#39;ambiente in GitLab](/help/implementing/developing/introduction/assets/rde-gitlab-deployment-1.png)

   Aspetto di Bitbucket:

   ![Stato dell&#39;ambiente in Bitbucket](/help/implementing/developing/introduction/assets/rde-bitbucket-deployment-1.png)

1. **Messaggio di distribuzione riuscito.**

   Al termine della distribuzione, Cloud Manager pubblica un messaggio di successo che riepiloga gli artefatti distribuiti nell’ambiente di destinazione.

   Come si presenta su GitHub Enterprise:

   ![Stato della distribuzione dell&#39;ambiente su GitHub](/help/implementing/developing/introduction/assets/rde-github-environment-deployed-artifacts.png)

   Come si presenta su GitLab:

   ![Stato della distribuzione dell&#39;ambiente in GitLab](/help/implementing/developing/introduction/assets/rde-gitlab-deployment-2.png)

   Aspetto di Bitbucket:

   ![Stato di distribuzione dell&#39;ambiente in Bitbucket](/help/implementing/developing/introduction/assets/rde-bitbucket-deployment-2.png)




## Registri {#rde-logging}

Analogamente ad altri tipi di ambiente, i livelli di registro possono essere impostati modificando le configurazioni OSGi, anche se, come descritto in precedenza, il modello di distribuzione per gli RDE prevede una riga di comando anziché una distribuzione Cloud Manager. Per ulteriori informazioni su come visualizzare, scaricare e interpretare i registri, consulta la [documentazione di registrazione](/help/implementing/developing/introduction/logging.md).

RDE CLI dispone inoltre di un proprio comando di registro utilizzato per configurare rapidamente le classi e i pacchetti registrati e a quale livello di registro. Queste configurazioni possono essere visualizzate come temporanee, in quanto non modificano le proprietà OSGI nel controllo della versione. Questa funzione si concentra sulla suddivisione dei registri in tempo reale, anziché cercare registri di un passato remoto.

L’esempio seguente illustra come visualizzare il livello di authoring, con un pacchetto impostato su un livello di registro di debug e due pacchetti (separati da spazi) impostati su un livello di debug di informazioni. L&#39;output che include un pacchetto **auth** è evidenziato.

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>Se viene visualizzato l&#39;errore `RDECLI:UNEXPECTED_API_ERROR` durante la riproduzione con i comandi dei registri per il servizio Author, reimpostare l&#39;ambiente e riprovare. Questo errore viene generato se l’ultima operazione di ripristino è stata eseguita prima della fine di maggio 2024.
>
>```
>aio aem:rde:reset
>```

Vedere `aio aem:rde:logs --help` per l&#39;insieme completo delle opzioni della riga di comando.

Le caratteristiche includono:

* dichiarazione dei livelli di registro a livello di pacchetto o classe
* personalizzazione del formato di output del registro
* fino a quattro configurazioni di registro, ciascuna nel proprio terminale
* evidenziazione di registri specifici

Si noti che i registri vengono memorizzati in memoria sull&#39;RDE e che tali registri vengono riciclati e quindi eliminati se non sono in coda o se la rete è troppo lenta.


## Reimposta RDE {#reset-rde}

Se si ripristina la RDE, verranno rimossi dalle istanze di authoring e di pubblicazione tutto il codice personalizzato, le configurazioni e il contenuto. Il ripristino dell&#39;RDE è utile quando avete terminato il test di una feature e desiderate ripristinare lo stato predefinito dell&#39;ambiente prima di testarne un&#39;altra.

Una reimpostazione imposta l’RDE sulla versione di AEM più recente disponibile.

È possibile reimpostare la RDE utilizzando [Cloud Manager](#reset-the-rde-cloud-manager) o la [riga di comando](#reset-the-rde-command-line). Il ripristino richiede alcuni minuti e tutto il contenuto e il codice esistenti viene eliminato dall’RDE.

>[!NOTE]
>
>Assicurati di aver ricevuto il ruolo Sviluppatore Cloud Manager prima di utilizzare la funzione di ripristino. In caso contrario, l’azione di ripristino non riesce e viene visualizzato un errore.

### Reimpostare l&#39;RDE utilizzando la riga di comando {#reset-the-rde-command-line}

È possibile ripristinare l&#39;RDE e riportarlo allo stato predefinito eseguendo le operazioni seguenti:

`aio aem:rde:reset`

Questo processo in genere richiede alcuni minuti e segnala ```Environment reset.``` in caso di esito positivo o ```Failed to reset the environment.``` in caso di errori. Per un output strutturato, vedere il capitolo sull&#39;output ```--json``` riportato di seguito.

Utilizza il comando [status](#checking-rde-status) per verificare quando l&#39;ambiente è nuovamente pronto.

### Reimpostare l&#39;RDE in Cloud Manager {#reset-the-rde-cloud-manager}

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

Dopo l’avvio del ripristino RDE, in genere sono necessari alcuni minuti per completare e ripristinare lo stato predefinito dell’ambiente. Puoi visualizzare lo stato di ripristino in qualsiasi momento nella colonna **Stato** della scheda o della finestra **Ambienti**.

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

### Eliminare {#delete}

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

#### Fuoco e dimentica, non aspettare {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### Attendere il completamento, reimpostare correttamente {#wait-success}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```

#### Attesa del completamento, ripristino non riuscito {#wait-failed}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset_failed"
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

Gli RDE sono distinti da altri ambienti in quanto il contenuto può essere installato in una cartella `install.rde` (o `install.author.rde` o `install.publish.rde`) in `/apps`. Questa funzionalità consente di eseguire il commit del contenuto in Git e distribuirlo all’RDE utilizzando gli strumenti della riga di comando.

## Popola con contenuto {#populating-content}

Quando un RDE viene reimpostato, tutto il contenuto viene rimosso e quindi, se desiderato, è necessario eseguire un’azione esplicita per aggiungere contenuto. Come best practice, è consigliabile assemblare un set di contenuti da utilizzare come contenuti di prova per convalidare o eseguire il debug delle funzioni nell’RDE. Esistono diverse strategie possibili per popolare l’RDE con tale contenuto:

1. Sincronizzare esplicitamente il pacchetto di contenuti con l&#39;RDE utilizzando gli strumenti della riga di comando

1. Inserire e confermare il contenuto di esempio in Git all&#39;interno di una cartella `install.rde` in `/apps`, quindi sincronizzare il pacchetto di contenuto generale con RDE utilizzando gli strumenti della riga di comando.

1. Utilizzare lo strumento [copia contenuto](/help/implementing/developing/tools/content-copy.md) per copiare un set di contenuti definito da ambienti di produzione, stage o sviluppo o da un altro RDE.

1. Utilizzare Gestione pacchetti

Il limite è di 1 GB per la sincronizzazione dei pacchetti di contenuti.


## Quali sono le differenze tra gli RDE e gli ambienti di sviluppo cloud? {#how-are-rds-different-from-cloud-development-environments}

Sebbene l’RDE sia per molti aspetti simile a un ambiente di sviluppo cloud, esistono alcune lievi differenze a livello di architettura per consentire una rapida sincronizzazione del codice. Il meccanismo per ottenere il codice da RDE è diverso: per gli RDE, si sincronizza il codice da un ambiente di sviluppo locale, mentre per gli ambienti di sviluppo cloud, si distribuisce il codice tramite Cloud Manager.

Per questi motivi, si consiglia di distribuire il codice in un ambiente di sviluppo cloud utilizzando la pipeline non di produzione dopo aver convalidato il codice in un ambiente RDE. Infine, verifica il codice prima di distribuirlo con la pipeline di produzione.

Inoltre, tieni presente le seguenti considerazioni:

* Gli RDE non includono un livello di anteprima
* Attualmente gli RDE non supportano il canale prerelease.


## Di quante RDE ho bisogno? {#how-many-rds-do-i-need}

È disponibile un RDE per ogni soluzione concessa in licenza e Adobe offre anche RDE aggiuntivi che possono essere concessi in licenza per programmi di produzione (non sandbox).

Il numero di RDE necessari dipende dalla composizione e dai processi di un’organizzazione. Il modello più flessibile è quello in cui un’organizzazione acquista un RDE dedicato per ciascuno dei propri sviluppatori AEM Cloud Service. In questo modello, ogni sviluppatore può testare il proprio codice sull’RDE senza coordinarsi con gli altri membri del gruppo sulla disponibilità di un ambiente RDE.

All’altro estremo, un team con un solo RDE può fare affidamento sul coordinamento interno per decidere quale sviluppatore utilizza l’ambiente in un dato momento. Questo approccio funziona bene quando uno sviluppatore raggiunge una feature milestone e deve convalidare il proprio lavoro in un ambiente Cloud con la flessibilità di apportare modifiche rapide.

Un modello intermedio è un modello in cui un’organizzazione acquista diversi RDE, pertanto vi è una maggiore probabilità che sia disponibile un RDE inutilizzato. Una strategia potrebbe essere quella di allocare un RDE per team di scrum o per una funzione importante. I processi interni possono essere utilizzati per coordinare l’utilizzo degli ambienti.

## Quali sono le differenze tra AEM Forms Cloud Service RDE e altri ambienti? {#how-are-forms-rds-different-from-cloud-development-environments}

Gli sviluppatori Forms possono utilizzare AEM Forms Cloud Service Rapid Development Environment per sviluppare rapidamente Forms adattivo, flussi di lavoro e personalizzazioni quali la personalizzazione di componenti core, integrazioni con sistemi di terze parti e altro ancora. AEM Forms Cloud Service Rapid Development Environment (RDE) non supporta le API di comunicazione. Inoltre, non supporta funzioni e funzionalità che richiedono documenti di record, come la generazione di un documento di record all’invio di un modulo adattivo. Le seguenti funzioni di AEM Forms non sono disponibili in un ambiente di sviluppo rapido (RDE):

* Configurazione di un documento record per un modulo adattivo
* Generazione di un documento record all’invio di un modulo adattivo o con un passaggio del flusso di lavoro
* Inviare un documento record come allegato con l’azione Invia e-mail o con il passaggio E-mail in un flusso di lavoro
* Utilizzo di Adobe Accedi a un modulo adattivo o in un passaggio del flusso di lavoro
* API di comunicazione

>[!NOTE]
>
> Non vi è alcuna differenza tra l’interfaccia utente di Rapid Development Environment (RDE) e altri ambienti Cloud Service per Forms. Tutte le opzioni relative al documento record, come la selezione di un modello di documento record per un modulo adattivo, continuano a essere visualizzate nell’interfaccia utente. Questi ambienti non dispongono di API di comunicazione e funzionalità per documenti di record per testare tali opzioni. Pertanto, se scegli un’opzione che richiede le API di comunicazione o le funzionalità del documento di record, il sistema non esegue l’azione. Viene invece visualizzato un messaggio di errore.

## Esercitazione RDE

Per informazioni su RDE in AEM as a Cloud Service, consulta l&#39;esercitazione video che illustra [come configurarlo, come utilizzarlo e il ciclo di vita dello sviluppo (01:25)](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/rde/overview).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione dei problemi relativi a RDE (#rde-troublehooting)

#### Come ottenere la versione più recente di AEM per un RDE esistente {#get-latest-aem-version}

Al momento della creazione, gli RDE sono impostati sulla versione di Adobe Experience Manager (AEM) più recente disponibile. Un [ripristino RDE](#reset-rde), che può essere eseguito utilizzando Cloud Manager o il comando `aio aem:rde:reset`, esegue un ciclo RDE e lo imposta sulla versione di AEM più recente disponibile.

### Risolvere i problemi relativi al plug-in di aio RDE {#aio-rde-plugin-troubleshooting}

#### Errori relativi ad autorizzazioni insufficienti {#insufficient-permissions}

Per utilizzare il plug-in RDE, è necessario essere membri del profilo di prodotto Cloud Manager **Developer - Cloud Service**. Per ulteriori dettagli, vedere [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager - Assegnazione del profilo di prodotto sviluppatore](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer).

In alternativa, puoi confermare di disporre di questo ruolo di sviluppatore se accedi alla console per sviluppatori eseguendo il seguente comando:

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>Se viene visualizzato l&#39;errore `Warning: cloudmanager:* is not a aio command.`, è necessario installare [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) eseguendo il comando seguente:
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

Verifica che l’accesso sia stato completato correttamente eseguendo quanto segue:

`aio cloudmanager:list-programs`

Questo processo elenca tutti i programmi dell’organizzazione configurata e conferma che il ruolo assegnato è corretto.

#### Usa contesto obsoleto `aio-cli-plugin-cloudmanager` {#aio-rde-plugin-troubleshooting-deprecatedcontext}

A causa della cronologia di `aio-cli-plugin-aem-rde`, il nome di contesto `aio-cli-plugin-cloudmanager` è stato utilizzato per qualche tempo. Il plug-in RDE ora utilizza il metodo IMS per gestire le informazioni di contesto, consentendo di memorizzare il contesto a livello globale o locale. È inoltre possibile configurare un contesto predefinito da applicare automaticamente a tutte le chiamate AIO. Il contesto predefinito configurato viene memorizzato localmente e consente agli sviluppatori di tenere traccia e utilizzare singoli contesti e le relative informazioni all&#39;interno di una cartella. Per ulteriori dettagli, leggere [l&#39;esempio per impostare un contesto locale](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) sopra.

Gli sviluppatori che utilizzano entrambi i plug-in, `aio-cli-plugin-cloudmanager` e `aio-cli-plugin-aem-rde` e desiderano conservare tutte le informazioni nello stesso contesto devono ora scegliere tra le seguenti opzioni:

##### Continua a utilizzare il contesto `aio-cli-plugin-cloudmanager`

Il contesto può ancora essere utilizzato. Nel plug-in RDE viene visualizzato un avviso di elementi obsoleti. Questo avviso può essere omesso utilizzando la modalità ```--quiet```. Versioni più recenti del plug-in RDE non offrono più il fallback per la lettura del contesto `aio-cli-plugin-cloudmanager`. Per continuare a utilizzarlo, configurare il contesto predefinito su `aio-cli-plugin-cloudmanager`. Vedi [l&#39;esempio per configurare un contesto locale](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) sopra.

##### Usa qualsiasi altro nome di contesto anche per il plug-in Cloud Manager

I plug-in di Cloud Manager offrono un parametro per definire un contesto da utilizzare. Al momento non supporta la configurazione del contesto predefinita di IMS. Per eseguire questa operazione, configurare il plug-in RDE utilizzando [l&#39;esempio per impostare un contesto locale](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) e indicare al plug-in Cloud Manager di utilizzare `myContext` come ```--imsContextName=myContext``` in ogni chiamata.
