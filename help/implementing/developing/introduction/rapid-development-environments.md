---
title: Ambienti di sviluppo rapidi
description: Scopri come utilizzare gli ambienti di sviluppo rapido per le iterazioni di sviluppo rapido in un ambiente cloud.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '3317'
ht-degree: 5%

---

# Ambienti di sviluppo rapidi {#rapid-development-environments}

Per distribuire le modifiche, gli ambienti di sviluppo cloud attuali richiedono l’utilizzo di un processo che utilizza regole estese di qualità e sicurezza del codice, denominate pipeline CI/CD. Per le situazioni in cui sono necessari cambiamenti rapidi e iterativi, Adobe ha introdotto ambienti di sviluppo rapido (RDE, Rapid Development Environments).

Gli RDE consentono agli sviluppatori di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale.

Una volta testate in un RDE, le modifiche possono essere distribuite in un ambiente di sviluppo Cloud regolare tramite la pipeline di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Ulteriori video dimostrativi [come impostarla](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [come utilizzarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)e [ciclo di vita dello sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) utilizzo di RDE.

## Introduzione {#introduction}

Gli RDE possono essere utilizzati per codice, contenuto e configurazioni di Apache o Dispatcher. A differenza dei normali ambienti di sviluppo cloud, gli sviluppatori possono utilizzare strumenti della riga di comando locali per sincronizzare il codice generato localmente con un RDE.

A ogni programma viene fornito un RDE. Nel caso degli account Sandbox, vengono sospesi dopo alcune ore di non utilizzo.

Al momento della creazione, gli RDE sono impostati sulla versione AEM più recente disponibile. Un ripristino RDE, che può essere eseguito utilizzando Cloud Manager, esegue un ciclo dell’RDE e lo imposta sulla versione dell’AEM più recente disponibile.

In genere, un RDE viene utilizzato da un singolo sviluppatore in un determinato momento, per testare e eseguire il debug di una funzione specifica. Al termine della sessione di sviluppo, è possibile ripristinare lo stato predefinito dell’RDE per l’utilizzo successivo.

Ulteriori RDE possono essere concessi in licenza per programmi di produzione (non sandbox).

## Abilitazione di RDE in un programma {#enabling-rde-in-a-program}

Per creare un RDE per il programma, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma al quale si desidera aggiungere un RDE per visualizzarne i dettagli.

   * Gli RDE possono essere aggiunti a entrambi [programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) e [programmi di produzione.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. Per aggiungere un programma, dalla pagina **Panoramica del programma**, accedi alla scheda **Ambienti** e fai clic su **Aggiungi ambiente**.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

     ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente** che viene visualizzata:

   * Seleziona **Sviluppo rapido** sotto **Seleziona tipo di ambiente** intestazione.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dopo il tipo di ambiente.
   * Fornisci un **Nome** per l&#39;ambiente.
   * Fornisci un **Descrizione** per l&#39;ambiente.
   * Seleziona un’**Area geografica cloud**.

   ![Finestra di dialogo Aggiungi ambiente](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Ora il nuovo ambiente viene visualizzato nella schermata **Panoramica** della scheda **Ambienti.**

Al momento della creazione, gli RDE sono impostati sulla versione AEM più recente disponibile. Un ripristino RDE, che può essere eseguito anche utilizzando Cloud Manager, esegue un ciclo dell’RDE e lo imposta sulla versione dell’AEM più recente disponibile.

Per ulteriori informazioni sull’utilizzo di Cloud Manager per creare ambienti, gestire gli utenti che possono accedervi e assegnare domini personalizzati, consulta [la documentazione di Cloud Manager.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Installazione degli strumenti della riga di comando RDE {#installing-the-rde-command-line-tools}

Dopo aver aggiunto un RDE per il programma utilizzando Cloud Manager, puoi interagire con esso configurando gli strumenti della riga di comando come descritto nei passaggi seguenti:

>[!IMPORTANT]
>
>Assicurati di disporre della versione più recente di [Nodo e NPM installati](https://nodejs.org/it/download/) ad Adobe I/O CLI e i relativi plug-in per funzionare correttamente.


1. Installare gli strumenti CLI Adobe I/O seguendo la procedura descritta di seguito. [qui](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Installa il plug-in Adobe I/O CLI tools Cloud Manager e configurali come descritto [qui](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. Installare il plug-in AEM RDE degli strumenti CLI di Adobe I/O eseguendo i seguenti comandi:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Configura il plug-in cloud manager per l’ID organizzazione:

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   e sostituisci la stringa alfanumerica con il tuo ID organizzazione, che può essere cercato utilizzando la strategia [qui](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Quindi, configura l’ID del programma:

   `aio config:set cloudmanager_programid 12345`

1. Quindi, configura l’ID ambiente a cui verrà allegato l’RDE:

   `aio config:set cloudmanager_environmentid 123456`

1. Al termine della configurazione del plug-in, effettua l’accesso eseguendo le seguenti operazioni:

   `aio login`

   La risposta in caso di esito positivo dell’accesso dovrebbe essere simile all’output riportato di seguito, ma puoi ignorare i valori visualizzati.

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

   Nota: questo passaggio richiede l’iscrizione a Cloud Manager **Sviluppatore - Cloud Service** Profilo prodotto. Consulta [questa pagina](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) per ulteriori dettagli.

   In alternativa, puoi confermare di disporre di questo ruolo di sviluppatore se puoi accedere alla console per sviluppatori eseguendo questo comando:

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >Se vedi il `Warning: cloudmanager:list-programs is not a aio command.` errore, è necessario installare [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) eseguendo il comando seguente:
   >
   >```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

1. Verifica che l’accesso sia stato completato correttamente eseguendo

   `aio cloudmanager:list-programs`

   Questo dovrebbe elencare tutti i programmi nell’organizzazione configurata.


Per ulteriori informazioni e dimostrazioni, vedere [come impostare un RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) tutorial video.

## Utilizzo di RDE durante lo sviluppo di una nuova feature {#using-rde-while-developing-a-new-feature}

L’Adobe consiglia il seguente flusso di lavoro per lo sviluppo di una nuova funzione:

* Quando viene raggiunta una fase cardine intermedia e la sua convalida a livello locale con l’SDK as a Cloud Service dell’AEM, il codice deve essere confermato in un ramo della funzione Git che non fa ancora parte della riga principale, anche se il commit in Git è facoltativo. Ciò che costituisce un &quot;traguardo intermedio&quot; varia in base alle abitudini del team. Alcuni esempi includono nuove righe di codice, mezza giornata di lavoro o il completamento di una sottofunzione.

* Reimpostare l&#39;RDE se è stato utilizzato da un&#39;altra feature e si desidera [ripristina lo stato predefinito](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->L’operazione di ripristino richiederà alcuni minuti e tutto il contenuto e il codice esistenti verrà eliminato. È possibile utilizzare il comando RDE status per confermare che RDE è pronto. L’RDE tornerà alla versione più recente dell’AEM.

  >[!IMPORTANT]
  >
  > Se gli ambienti di staging e produzione non ricevono aggiornamenti automatici del rilascio dell’AEM e sono molto in ritardo rispetto alla versione più recente del rilascio dell’AEM, tieni presente che il codice in esecuzione sull’RDE potrebbe non corrispondere al modo in cui il codice funzionerà nell’ambiente di staging e produzione. In questo caso, è particolarmente importante eseguire un test approfondito del codice sulla gestione temporanea prima di distribuirlo alla produzione.


* Utilizzando l&#39;interfaccia della riga di comando RDE, sincronizzare il codice locale con RDE. Le opzioni includono l’installazione di un pacchetto di contenuti, un bundle specifico, un file di configurazione OSGI, un file di contenuti e un file zip di una configurazione Apache/Dispatcher. È inoltre possibile fare riferimento a un pacchetto di contenuti remoto. Consulta la [Strumenti della riga di comando RDE](#rde-cli-commands) per ulteriori informazioni. È possibile utilizzare il comando di stato per verificare che la distribuzione sia stata eseguita correttamente. Facoltativamente, utilizza Gestione pacchetti per installare i pacchetti di contenuti.

* Verifica il codice nell’RDE. Gli URL Author e Publish sono disponibili in Cloud Manager.

* Se il codice non si comporta come previsto, utilizza tecniche di debug standard per comprendere il problema e apportare le modifiche appropriate. Senza eseguire il commit delle modifiche del codice in Git (poiché non sono state convalidate), utilizza la CLI locale per sincronizzare il codice in RDE. Continua a ripetere l’iterazione fino a quando il problema non viene risolto.

* Una volta che il codice si comporta come previsto, esegui il commit del codice nel ramo della funzione Git.

* Il codice sincronizzato con RDE non utilizza una pipeline di Cloud Manager, pertanto ora devi utilizzare una pipeline non di produzione di Cloud Manager per distribuire il ramo della funzione Git nell’ambiente di sviluppo Cloud. In questo modo, potrai verificare che il codice superi i gate di qualità di Cloud Manager e avere la certezza che verrà successivamente distribuito correttamente utilizzando la pipeline di produzione di Cloud Manager.

* Ripeti i passaggi precedenti per ogni fase cardine intermedia fino a quando tutto il codice per la funzione non è pronto ed è eseguito correttamente sia nell’ambiente RDE che in quello di sviluppo cloud.

* Distribuisci il codice in produzione tramite la pipeline di produzione di Cloud Manager.

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

Qualsiasi pacchetto AEM può essere distribuito, ad esempio pacchetti con codice, contenuto o un [pacchetto contenitore](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (chiamato anche pacchetto &quot;all&quot;).

>[!IMPORTANT]
>
>La configurazione del dispatcher per il progetto WKND non viene distribuita tramite l’installazione del pacchetto di contenuti di cui sopra. Sarà necessario distribuirla separatamente seguendo i passaggi &quot;Distribuzione di una configurazione Apache/Dispatcher&quot;.

<u>Distribuzione di una configurazione OSGI</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

dove la risposta per una distribuzione corretta è simile alla seguente:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Distribuzione di un bundle</u>

Per distribuire un bundle, utilizza:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

dove la risposta per una distribuzione corretta è simile alla seguente:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Distribuzione di un file di contenuto</u>

Per distribuire un file di contenuto, utilizza:

`aio aem:rde:install world.txt -p /apps/hello.txt`

dove la risposta per una distribuzione corretta è simile alla seguente:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Distribuzione di una configurazione di Apache/Dispatcher</u>

Per questo tipo di configurazione, l’intera struttura di cartelle deve essere sotto forma di un file zip.

Dalla sezione `dispatcher` di un progetto AEM, puoi comprimere la configurazione dispatcher eseguendo il seguente comando maven:

`mvn clean package`

o utilizzando il comando zip seguente da `src` directory del `dispatcher` modulo:

`zip -y -r dispatcher.zip .`

quindi distribuisci la configurazione con questo comando:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>Il comando precedente presuppone che tu stia distribuendo [WKND](https://github.com/adobe/aem-guides-wknd) configurazioni del dispatcher del progetto. Sostituire il `X.X.X` con il numero di versione del progetto WKND corrispondente o il numero di versione specifico del progetto quando distribuisci la configurazione dispatcher del progetto.

>[!NOTE]
>
>RDE supporta la configurazione del dispatcher in &quot;modalità flessibile&quot;, ma non in &quot;modalità legacy&quot;. Consulta [documentazione di dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per informazioni sulle due modalità. È inoltre possibile consultare la documentazione su [migrazione in modalità flessibile](/help/implementing/dispatcher/validation-debug.md#migrating), se non lo hai già fatto.

Una distribuzione corretta genera una risposta simile alla seguente:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

Il codice distribuito in RDE non viene sottoposto a una pipeline di Cloud Manager e ai relativi gate di qualità associati, tuttavia il codice viene sottoposto ad alcune analisi che segnaleranno gli errori, come illustrato nell’esempio di codice seguente:

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

L’esempio di codice riportato sopra illustra il comportamento se un bundle non si risolve, nel qual caso è &quot;in staging&quot; e verrà installato solo se i suoi requisiti (importazioni mancanti, in questo caso) sono soddisfatti tramite l’installazione di un altro codice.

### Controllo dello stato della RDE {#checking-rde-status}

È possibile utilizzare RDE CLI per verificare se l’ambiente è pronto per essere distribuito in, in quanto le distribuzioni sono state effettuate tramite il plug-in RDE.

In esecuzione:

`aio aem:rde:status`

restituirà:

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

che restituisce una risposta in forma di:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Eliminazione da RDE {#deleting-from-rde}

È possibile eliminare configurazioni e bundle distribuiti in precedenza in RDE tramite gli strumenti CLI. Utilizza il `status` per un elenco di elementi che possono essere eliminati, che include `bsn` per i bundle e `pid` per le configurazioni a cui fare riferimento nel comando delete.

Ad esempio, se `com.adobe.granite.demo.MyServlet.cfg.json` è stato installato, il `bsn` è solo `com.adobe.granite.demo.MyServlet`, senza **cfg.json** suffisso.

L&#39;eliminazione di pacchetti di contenuti o file di contenuti non è supportata. Per rimuoverli, è necessario reimpostare l&#39;RDE, che lo riporterà allo stato predefinito.

Per ulteriori informazioni, consulta l’esempio seguente:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Per ulteriori informazioni e dimostrazioni, vedere [come utilizzare i comandi RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) tutorial video.

## Ripristina {#reset-rde}

Se si ripristina la RDE, verranno rimossi dalle istanze di authoring e di pubblicazione tutto il codice personalizzato, le configurazioni e il contenuto. Questo ripristino è utile, ad esempio, se l&#39;RDE è stato utilizzato per testare una caratteristica specifica e si desidera ripristinarla allo stato predefinito in modo da poter testare una caratteristica diversa.

Una reimpostazione imposta la RDE sulla versione AEM più recente disponibile.

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code is deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role to use the reset feature. If not, a reset action results in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

Per ripristinare l’RDE, puoi utilizzare Cloud Manager seguendo i passaggi seguenti:

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera reimpostare l&#39;RDE.

1. Dalla pagina **Panoramica**, fai clic sulla scheda **Ambienti** nella parte superiore della schermata.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * In alternativa, per passare direttamente alla scheda **Ambienti**, fai clic sul pulsante **Mostra tutto** nella scheda **Ambienti**.

     ![Opzione Mostra tutto](/help/implementing/cloud-manager/assets/environment-showall.png)

1. Il **Ambienti** Viene visualizzata una finestra in cui sono elencati tutti gli ambienti del programma.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Fai clic sul pulsante con i puntini di sospensione dell’RDE da reimpostare, quindi seleziona **Reimposta**.

   ![Visualizza dettagli ambiente](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Conferma di voler reimpostare la RDE facendo clic su **Reimposta** nella finestra di dialogo.

   ![Conferma reimpostazione](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager conferma tramite un banner l’avvio del processo di ripristino.

   ![Reimposta notifica banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Una volta avviato il processo di ripristino RDE, in genere sono necessari alcuni minuti per completarlo e ripristinare lo stato predefinito dell’ambiente. Lo stato del processo di ripristino può essere visualizzato in qualsiasi momento nella **Stato** colonna del **Ambienti** o nella scheda **Ambienti** finestra.

![Stato reimpostazione RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

È inoltre possibile reimpostare l’RDE utilizzando il pulsante con i puntini di sospensione direttamente dal **Ambienti** scheda su **Panoramica** pagina.

![Reimposta RDE dalla scheda Ambienti](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Per ulteriori informazioni su come utilizzare Cloud Manager per gestire gli ambienti, consulta [la documentazione di Cloud Manager.](/help/implementing/cloud-manager/manage-environments.md)

## Modalità di esecuzione {#runmodes}

La configurazione OSGI specifica per RDE può essere applicata utilizzando i suffissi sul nome della cartella, come negli esempi seguenti:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Consulta la [documentazione runmode](/help/implementing/deploying/overview.md#runmodes) per informazioni generali sulle modalità di esecuzione.

>[!NOTE]
>
>La configurazione OSGI RDE è univoca in quanto eredita i valori di tutte le proprietà OSGI dichiarate dal pacchetto `dev` modalità di esecuzione.

Gli RDE sono distinti da altri ambienti in quanto il contenuto può essere installato in una cartella install.rde (o install.author.rde o install.publish.rde) in /apps. Questo consente di eseguire il commit del contenuto in Git e distribuirlo all’RDE utilizzando gli strumenti della riga di comando.

## Popolamento con il contenuto {#populating-content}

Quando un RDE viene reimpostato, tutto il contenuto viene rimosso e quindi, se desiderato, è necessario eseguire un’azione esplicita per aggiungere contenuto. Come best practice, è consigliabile assemblare un set di contenuti da utilizzare come contenuti di prova per convalidare o eseguire il debug delle funzioni nell’RDE. Esistono diverse strategie possibili per popolare l’RDE con tale contenuto:

1. Sincronizza esplicitamente il pacchetto di contenuti con l’RDE utilizzando gli strumenti della riga di comando

1. Inserisci e conferma il contenuto di esempio in Git all’interno di una cartella install.rde in /apps, quindi sincronizza il pacchetto di contenuti generali con RDE utilizzando gli strumenti della riga di comando.

1. Utilizza il [strumento copia contenuto](/help/implementing/developing/tools/content-copy.md) per copiare un set di contenuti definito da ambienti di produzione, stage o sviluppo o da un altro RDE.

1. Utilizzare Gestione pacchetti

Tieni presente che sei limitato a 1 GB durante la sincronizzazione dei pacchetti di contenuti.

## Registrazione {#logging}

I livelli di registro possono essere impostati modificando le configurazioni OSGi. Controlla la [documentazione](/help/implementing/developing/introduction/logging.md) per ulteriori informazioni.

## Quali sono le differenze tra gli RDE e gli ambienti di sviluppo cloud? {#how-are-rds-different-from-cloud-development-environments}

Sebbene l’RDE sia simile per molti aspetti a un ambiente di sviluppo cloud, esistono alcune lievi differenze a livello di architettura per consentire una rapida sincronizzazione del codice. Il meccanismo per ottenere il codice da RDE è diverso: per gli RDE, si sincronizza il codice da un ambiente di sviluppo locale, mentre per gli ambienti di sviluppo cloud, si distribuisce il codice tramite Cloud Manager.

Per questi motivi, dopo aver convalidato il codice in un ambiente RDE, è consigliabile distribuirlo in un ambiente di sviluppo cloud utilizzando la pipeline non di produzione. Infine, verifica il codice prima di distribuirlo con la pipeline di produzione.

Inoltre, tieni presente le seguenti considerazioni:

* Gli RDE non includono un livello di anteprima
* Al momento gli RDE non supportano la visualizzazione e il debug del codice front-end distribuito tramite la pipeline front-end di Cloud Manager.
* Attualmente gli RDE non supportano il canale prerelease.


## Di quante RDE ho bisogno? {#how-many-rds-do-i-need}

È disponibile un RDE per ogni soluzione concessa in licenza e l’Adobe offre anche RDE aggiuntivi, che possono essere concessi in licenza per programmi di produzione (non sandbox).

Il numero di RDE necessari dipende dalla composizione e dai processi di un’organizzazione. Il modello più flessibile è quello in cui un’organizzazione acquista un RDE dedicato per ciascuno dei propri sviluppatori AEM Cloud Service. In questo modello, ogni sviluppatore può testare il proprio codice sull’RDE senza coordinarsi con gli altri membri del gruppo per determinare se è disponibile un ambiente RDE.

All’estremo opposto, un team con un singolo RDE può utilizzare processi interni per coordinare quale sviluppatore può utilizzare l’ambiente in un dato momento. Questo può accadere quando uno sviluppatore ha raggiunto una fase cardine della funzione intermedia ed è pronto per la convalida in un ambiente Cloud in cui può apportare rapidamente le modifiche necessarie.

Un modello intermedio è un modello in cui un’organizzazione acquista un certo numero di RDE, pertanto vi è una maggiore probabilità che sia disponibile un RDE inutilizzato. Una strategia potrebbe essere quella di allocare un RDE per team di scrum o per una funzione importante. I processi interni possono essere utilizzati per coordinare l’utilizzo degli ambienti.

## Quali sono le differenze tra AEM Forms Cloud Service Rapid Development Environment (RDE) e altri ambienti? {#how-are-forms-rds-different-from-cloud-development-environments}

Gli sviluppatori Forms possono utilizzare AEM Forms Cloud Service Rapid Development Environment per sviluppare rapidamente Forms adattivo, flussi di lavoro e personalizzazioni quali la personalizzazione di componenti core, integrazioni con sistemi di terze parti e altro ancora. AEM Forms Cloud Service Rapid Development Environment (RDE) non supporta le API di comunicazione e le funzionalità che richiedono un documento di record, come la generazione di un documento di record all’invio di un modulo adattivo. Le seguenti funzioni di AEM Forms non sono disponibili in un ambiente di sviluppo rapido (RDE):

* Configurazione di un documento record per un modulo adattivo
* Generazione di un documento record all’invio di un modulo adattivo o con un passaggio del flusso di lavoro
* Inviare un documento record come allegato con l’azione Invia e-mail o con il passaggio E-mail in un flusso di lavoro
* Utilizzo di Adobe Sign in un modulo adattivo o in un passaggio del flusso di lavoro
* API di comunicazione

>[!NOTE]
>
> Non c’è differenza tra l’interfaccia utente di Rapid Development Environment (RDE) e altri ambienti di Cloud Service per Forms. Tutte le opzioni relative al documento record, come la selezione di un modello di documento record per un modulo adattivo, continuano a essere visualizzate nell’interfaccia utente. Questi ambienti non dispongono di API di comunicazione e funzionalità per documenti di record per testare tali opzioni. Pertanto, quando scegli un’opzione che richiede API di comunicazione o funzionalità del documento di record, non viene eseguita alcuna azione e viene visualizzato o restituito un messaggio di errore.

## Esercitazione RDE

Per informazioni sulla RDE in AEM as a Cloud Service, consulta [tutorial video che illustra come configurarlo, come utilizzarlo e il ciclo di vita dello sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)
