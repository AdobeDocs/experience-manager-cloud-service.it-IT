---
title: Ambienti di sviluppo rapidi
description: Scopri come sfruttare gli ambienti di sviluppo rapido per iterazioni di sviluppo rapide in un ambiente cloud.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: 5bfa5a1df940b8903acd08f4c3cb7443adb897d8
workflow-type: tm+mt
source-wordcount: '3325'
ht-degree: 5%

---

# Ambienti di sviluppo rapidi {#rapid-development-environments}

Per implementare le modifiche, gli ambienti di Cloud Development correnti richiedono l’utilizzo di un processo che utilizzi un’ampia protezione del codice e regole di qualità denominate pipeline CI/CD. Per le situazioni in cui sono necessari cambiamenti rapidi e iterativi, Adobe ha introdotto gli RDE (Rapid Development Environments, RDE in breve).

Gli RDE consentono agli sviluppatori di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che è dimostrato funzionare in un ambiente di sviluppo locale.

Una volta testate le modifiche in un RDE, possono essere distribuite in un ambiente di sviluppo cloud regolare tramite la pipeline di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Puoi fare riferimento a video aggiuntivi che mostrano [come configurarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [come usarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)e [ciclo di vita dello sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) utilizzando RDE.

## Introduzione {#introduction}

Gli RDE possono essere utilizzati per le configurazioni di codice, contenuto e Apache o Dispatcher. A differenza dei normali ambienti di sviluppo cloud, gli sviluppatori possono utilizzare strumenti a riga di comando locali per sincronizzare il codice generato localmente con un RDE.

Ogni programma è fornito con un RDE. In caso di account Sandbox, saranno ibernati dopo alcune ore di utilizzo non autorizzato.

Al momento della creazione, gli RDE sono impostati sulla versione AEM più recente disponibile. Una reimpostazione RDE, che può essere eseguita utilizzando Cloud Manager, esegue il ciclo RDE e la imposta sulla versione AEM più recente disponibile.

In genere, un RDE viene utilizzato da un singolo sviluppatore alla volta per testare e eseguire il debug di una funzione specifica. Al termine della sessione di sviluppo, l’RDE può essere reimpostato in uno stato predefinito per l’utilizzo successivo.

Ulteriori RDE possono essere concessi in licenza per i programmi Produzione (non sandbox).

## Abilitazione dell’RDE in un programma {#enabling-rde-in-a-program}

Segui questi passaggi per utilizzare Cloud Manager per creare un RDE per il tuo programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma a cui desideri aggiungere un RDE per visualizzare i relativi dettagli.

   * Gli RDE possono essere aggiunti a entrambi [programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) e [programmi di produzione.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. Per aggiungere un programma, dalla pagina **Panoramica del programma**, accedi alla scheda **Ambienti** e fai clic su **Aggiungi ambiente**.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

      ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente** che viene visualizzata:

   * Seleziona **Sviluppo rapido** in **Seleziona tipo di ambiente** intestazione.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dietro il tipo di ambiente.
   * Fornisci un **Nome** per l&#39;ambiente.
   * Fornire un **Descrizione** per l&#39;ambiente.
   * Seleziona un’**Area geografica cloud**.

   ![Finestra di dialogo Aggiungi ambiente](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Ora il nuovo ambiente viene visualizzato nella schermata **Panoramica** della scheda **Ambienti.**

Al momento della creazione, gli RDE sono impostati sulla versione AEM più recente disponibile. Una reimpostazione RDE, che può essere eseguita anche utilizzando Cloud Manager, esegue il ciclo RDE e la imposta sulla versione AEM più recente disponibile.

Per ulteriori informazioni sull’utilizzo di Cloud Manager per creare ambienti, gestire gli utenti con accesso e assegnare domini personalizzati, consulta [la documentazione di Cloud Manager.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Installazione degli strumenti della riga di comando RDE {#installing-the-rde-command-line-tools}

Dopo aver aggiunto un RDE per il programma utilizzando Cloud Manager, puoi interagire con esso impostando gli strumenti della riga di comando come descritto nei passaggi seguenti:

>[!IMPORTANT]
>
>Assicurati di disporre della versione più recente di [Nodo e NPM installati](https://nodejs.org/it/download/) ad Adobe I/O CLI e i plug-in correlati per funzionare correttamente.


1. Installare gli strumenti CLI di Adobe I/O seguendo la procedura descritta [qui](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Installa il plug-in Adobe I/O CLI tools cloud manager e configurali come descritto [qui](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. Installa gli strumenti CLI di Adobe I/O AEM plugin RDE eseguendo questi comandi:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Configura il plug-in cloud manager per l’ID organizzazione:

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   e sostituisci la stringa alfanumerica con il tuo ID organizzazione, che può essere cercato utilizzando la strategia [qui](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Quindi, configura l&#39;ID programma:

   `aio config:set cloudmanager_programid 12345`

1. Quindi, configura l’ID ambiente a cui verrà allegato l’RDE:

   `aio config:set cloudmanager_environmentid 123456`

1. Dopo aver configurato il plug-in, effettua l’accesso

   `aio login`

   La risposta in caso di accesso riuscito dovrebbe essere simile all&#39;output sottostante, ma puoi ignorare i valori visualizzati.

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

   Tieni presente che questo passaggio ti richiede di essere membro di Cloud Manager **Sviluppatore - Cloud Service** Profilo prodotto. Vedi [questa pagina](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) per ulteriori dettagli.

   In alternativa, puoi confermare di disporre di questo ruolo di sviluppatore se puoi accedere alla console di sviluppo eseguendo questo comando:

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >Se vedi la `Warning: cloudmanager:list-programs is not a aio command.` errore, è necessario installare [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) eseguendo il comando seguente:
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

1. Verifica che l&#39;accesso sia stato completato correttamente eseguendo

   `aio cloudmanager:list-programs`

   Questo dovrebbe elencare tutti i programmi nell&#39;organizzazione configurata.


Per ulteriori informazioni e dimostrazioni, consulta la sezione [come impostare un RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) esercitazione video.

## Utilizzo di RDE durante lo sviluppo di una nuova funzione {#using-rde-while-developing-a-new-feature}

L’Adobe consiglia il seguente flusso di lavoro per lo sviluppo di una nuova funzione:

* Quando viene raggiunta una fase cardine intermedia e convalidata localmente con l’SDK as a Cloud Service AEM, il codice deve essere impegnato in un ramo di funzionalità Git che non fa ancora parte della riga principale, anche se il commit in Git è facoltativo. Ciò che costituisce una &quot;pietra miliare intermedia&quot; varia in base alle abitudini dei team. Alcuni esempi includono alcune nuove righe di codice, mezza giornata di lavoro o il completamento di una funzionalità secondaria.

* Reimpostare l’RDE se è stato utilizzato da un’altra feature e si desidera [reimpostarlo su uno stato predefinito](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->Il ripristino richiederà alcuni minuti e tutti i contenuti e il codice esistenti verranno eliminati. Puoi usare il comando Stato RDE per confermare che l’RDE è pronto. L’RDE verrà riprodotto con la versione di AEM più recente.

   >[!IMPORTANT]
   >
   > Se gli ambienti di staging e produzione non ricevono aggiornamenti automatici AEM versione e sono molto indietro rispetto alla versione più recente AEM, ricorda che il codice in esecuzione sull’RDE potrebbe non corrispondere a come funzionerà il codice in fase di staging e produzione. In tal caso, è particolarmente importante eseguire un test approfondito del codice durante la gestione temporanea prima di distribuirlo in produzione.


* Utilizzando l’interfaccia della riga di comando RDE, sincronizza il codice locale con l’RDE. Le opzioni includono l’installazione di un pacchetto di contenuti, un bundle specifico, un file di configurazione OSGI, un file di contenuto e un file zip di una configurazione Apache/Dispatcher. È inoltre possibile fare riferimento a un pacchetto di contenuti remoti. Consulta la sezione [Strumenti della riga di comando RDE](#rde-cli-commands) per ulteriori informazioni. È possibile utilizzare il comando di stato per verificare che la distribuzione abbia avuto esito positivo. Facoltativamente, utilizza Gestione pacchetti per installare i pacchetti di contenuto.

* Verifica il codice nell’RDE. Gli URL di authoring e pubblicazione sono disponibili in Cloud Manager.

* Se il codice non si comporta come previsto, utilizza tecniche di debug standard per comprendere il problema e apportare le modifiche appropriate. Senza apportare modifiche al codice a git (poiché non sono state convalidate), utilizza la CLI locale per sincronizzare il codice all’RDE. Continua a ripetere fino a quando il problema non viene risolto.

* Una volta che il codice si comporta come previsto, esegui il commit del codice nel ramo della funzione git.

* Il codice sincronizzato in RDE non utilizza una pipeline di Cloud Manager, pertanto ora devi utilizzare una pipeline di non produzione di Cloud Manager per distribuire il ramo di funzionalità Git nell’ambiente di Cloud Development. Questo verifica che il codice superi i gate di qualità di Cloud Manager e ti consente di essere sicuro che in seguito il codice verrà distribuito correttamente utilizzando la pipeline di produzione di Cloud Manager.

* Ripeti i passaggi indicati sopra per ogni cardine intermedia fino a quando tutto il codice per la funzione non è pronto ed è eseguito correttamente sia nell’ambiente RDE che nell’ambiente di sviluppo cloud.

* Distribuisci il codice in produzione tramite la pipeline di produzione di Cloud Manager.

## Utilizzo di RDE per eseguire il debug di una funzione esistente {#use-rde-to-debug-an-existing-feature}

Il flusso di lavoro è simile allo sviluppo di una nuova funzione. La differenza è che il codice sincronizzato in RDE riflette l’etichetta git di qualsiasi elemento inviato all’ambiente in cui è stato trovato il problema. Inoltre, può essere utile distribuire contenuti che corrispondano all’ambiente a monte. Ciò può essere ottenuto esportando e importando pacchetti di contenuti.

## Più sviluppatori che collaborano allo stesso RDE {#multiple-developers-collaborating-on-the-same-rde}

Un RDE supporta un singolo progetto alla volta. Poiché il codice viene sincronizzato da un ambiente di sviluppo locale all’ambiente RDE, è più naturale che uno sviluppatore lo utilizzi da solo in un dato momento.

Tuttavia, con un’attenta coordinazione, è possibile che più di uno sviluppatore convalidino una funzione specifica o eseguano il debug di un problema specifico. La chiave è che ogni sviluppatore mantiene sincronizzati i propri progetti locali, in modo che le modifiche al codice apportate da un particolare sviluppatore vengano assorbite dagli altri sviluppatori, altrimenti uno sviluppatore potrebbe sovrascrivere inavvertitamente il codice dell’altro. La strategia consigliata è che ogni sviluppatore esegua il commit delle modifiche in un ramo git condiviso prima di sincronizzarlo con l’RDE, in modo che gli altri sviluppatori eseguano il pull delle modifiche prima di apportare le proprie modifiche.

## Comandi degli strumenti della riga di comando RDE {#rde-cli-commands}

### Guida/Informazioni generali {#help}

* Per un elenco di comandi, digitare:

   `aio aem:rde`

* Per informazioni dettagliate su un comando, digitare:

   `aio aem rde <command> --help`

### Distribuzione in RDE {#deploying-to-rde}

Questa sezione descrive l’utilizzo di RDE CLI per distribuire, installare o aggiornare bundle, configurazioni OSGI, pacchetti di contenuto, file di contenuto individuali e configurazioni di Apache o Dispatcher.

Il modello di utilizzo generale è `aio aem:rde:install <artifact>`.

Di seguito sono riportati alcuni esempi:

<u>Distribuzione di un pacchetto di contenuti</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

La risposta per una distribuzione di successo è simile alla seguente:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Facoltativamente, puoi fare riferimento a un archivio remoto:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Per impostazione predefinita, gli artefatti vengono distribuiti sia sui livelli di authoring che di pubblicazione, ma il flag &quot;-s&quot; può essere utilizzato per eseguire il targeting di un livello specifico.

Qualsiasi pacchetto AEM può essere distribuito, ad esempio pacchetti con codice, contenuto o un [pacchetto contenitore](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (chiamato anche il pacchetto &quot;all&quot;).

>[!IMPORTANT]
>
>La configurazione del dispatcher per il progetto WKND non viene distribuita tramite l’installazione del pacchetto di contenuti di cui sopra. Sarà necessario distribuirlo separatamente seguendo i passaggi &quot;Implementazione di una configurazione Apache/Dispatcher&quot;.

<u>Distribuzione di una configurazione OSGI</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

dove la risposta per una distribuzione di successo è simile alla seguente:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Distribuzione di un bundle</u>

Per distribuire un bundle, utilizza:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

dove la risposta per una distribuzione di successo è simile alla seguente:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Distribuzione di un file di contenuto</u>

Per distribuire un file di contenuto, utilizza:

`aio aem:rde:install world.txt -p /apps/hello.txt`

dove la risposta per una distribuzione di successo è simile alla seguente:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Distribuzione di una configurazione Apache/Dispatcher</u>

L’intera struttura delle cartelle deve essere sotto forma di file zip per questo tipo di configurazione.

Da `dispatcher` modulo di un progetto AEM, puoi comprimere la configurazione del dispatcher eseguendo il seguente comando maven:

`mvn clean package`

o utilizzando il seguente comando zip dal `src` directory `dispatcher` modulo:

`zip -y -r dispatcher.zip .`

quindi distribuisci la configurazione con questo comando:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>Il comando precedente presuppone che si stia distribuendo il [WKND](https://github.com/adobe/aem-guides-wknd) configurazioni del dispatcher del progetto. Assicurati di sostituire il `X.X.X` con il numero di versione del progetto WKND corrispondente o il numero di versione specifico del progetto durante la distribuzione della configurazione del dispatcher del progetto.

>[!NOTE]
>
>RDE supporta la configurazione del dispatcher &quot;in modalità flessibile&quot;, ma non la configurazione del dispatcher &quot;in modalità legacy&quot;. Vedi [documentazione del dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per informazioni sulle due modalità. Puoi anche consultare la documentazione su [migrazione alla modalità flessibile](/help/implementing/dispatcher/validation-debug.md#migrating), se non lo hai già fatto.

Una distribuzione corretta genererà una risposta simile alla seguente:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

Il codice distribuito in RDE non è sottoposto a una pipeline di Cloud Manager e ai relativi gate di qualità associati, tuttavia il codice passa attraverso un’analisi, che segnalerà gli errori, come illustrato nell’esempio di codice seguente:

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

L&#39;esempio di codice riportato sopra illustra il comportamento se un bundle non risolve, nel qual caso è &quot;impilato&quot; e sarà installato solo se i suoi requisiti (importazioni mancanti, in questo caso) sono soddisfatti tramite l&#39;installazione di un altro codice.

### Controllo dello stato dell’RDE {#checking-rde-status}

Puoi utilizzare RDE CLI per verificare se l’ambiente è pronto per essere distribuito in, in quanto le distribuzioni sono state effettuate tramite il plug-in RDE.

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

Se il comando restituisce una nota sulla distribuzione delle istanze, è comunque possibile procedere ed eseguire l&#39;aggiornamento successivo, ma l&#39;ultimo potrebbe non essere ancora visibile sull&#39;istanza.

### Mostra cronologia distribuzione {#show-deployment-history}

Puoi controllare la cronologia delle distribuzioni effettuate all’RDE eseguendo:

`aio aem:rde:history`

che restituisce una risposta sotto forma di:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Eliminazione da RDE {#deleting-from-rde}

È possibile eliminare configurazioni e bundle precedentemente distribuiti in RDE tramite gli strumenti CLI. Utilizza la `status` per un elenco di ciò che può essere eliminato, che include `bsn` per i bundle e `pid` per le configurazioni a cui fare riferimento nel comando delete.

Ad esempio, se `com.adobe.granite.demo.MyServlet.cfg.json` è stato installato, `bsn` è `com.adobe.granite.demo.MyServlet`, senza **cfg.json** suffisso

L&#39;eliminazione di pacchetti di contenuto o file di contenuto non è supportata. Per rimuoverli, è necessario reimpostare l’RDE, che lo restituirà a uno stato predefinito.

Per ulteriori informazioni, consulta l’esempio seguente:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Per ulteriori informazioni e dimostrazioni, consulta la sezione [come utilizzare i comandi RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) esercitazione video.

## Ripristina {#reset-rde}

Reimpostando l’RDE vengono rimossi tutti i codici, le configurazioni e i contenuti personalizzati dalle istanze di authoring e pubblicazione. Questo può essere utile, ad esempio, se l’RDE è stato utilizzato per testare una funzione specifica e si desidera reimpostarla su uno stato predefinito per testare una funzione diversa.

Una reimpostazione imposta l’RDE sulla versione AEM più recente disponibile.

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

Puoi utilizzare Cloud Manager per reimpostare l’RDE seguendo i passaggi seguenti:

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera reimpostare l&#39;RDE.

1. Dalla pagina **Panoramica**, fai clic sulla scheda **Ambienti** nella parte superiore della schermata.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * In alternativa, per passare direttamente alla scheda **Ambienti**, fai clic sul pulsante **Mostra tutto** nella scheda **Ambienti**.

      ![Opzione Mostra tutto](/help/implementing/cloud-manager/assets/environment-showall.png)

1. La **Ambienti** viene visualizzata la finestra in cui sono elencati tutti gli ambienti del programma.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Fare clic sul pulsante dei puntini di sospensione dell&#39;RDE che si desidera reimpostare e quindi selezionare **Reimposta**.

   ![Visualizza dettagli ambiente](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Conferma di voler reimpostare l’RDE facendo clic su **Reimposta** nella finestra di dialogo.

   ![Conferma reimpostazione](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager conferma tramite una notifica del banner che il processo di ripristino è stato avviato.

   ![Reimposta notifica banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Una volta avviato il processo di reimpostazione dell’RDE, in genere sono necessari alcuni minuti per completare e ripristinare lo stato predefinito dell’ambiente. Lo stato del processo di ripristino può essere visualizzato in qualsiasi momento nel **Stato** della colonna **Ambienti** o nella **Ambienti** finestra.

![Stato di reimpostazione RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

È inoltre possibile reimpostare l’RDE utilizzando il pulsante dei puntini di sospensione direttamente dal **Ambienti** scheda **Panoramica** pagina.

![Ripristina RDE dalla scheda Ambienti](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Per ulteriori informazioni su come utilizzare Cloud Manager per gestire gli ambienti, consulta [la documentazione di Cloud Manager.](/help/implementing/cloud-manager/manage-environments.md)

## Modalità di esecuzione {#runmodes}

La configurazione OSGI specifica RDE può essere applicata utilizzando suffissi sul nome della cartella, come negli esempi seguenti:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Consulta la sezione [documentazione in modalità runmode](/help/implementing/deploying/overview.md#runmodes) per informazioni generali sulle modalità di esecuzione.

>[!NOTE]
>
>La configurazione OSGI RDE è univoca in quanto eredita i valori di qualsiasi proprietà OSGI dichiarata dal bundle `dev` modalità di esecuzione.

Gli RDE sono diversi dagli altri ambienti in quanto il contenuto può essere installato in una cartella install.rde (o install.author.rde o install.publish.rde) in /apps. Questo consente di eseguire il commit del contenuto in git e di consegnarlo all’RDE utilizzando gli strumenti della riga di comando.

## Popolamento con il contenuto {#populating-content}

Quando un RDE viene reimpostato, tutti i contenuti vengono rimossi e quindi, se lo si desidera, è necessario intervenire in modo esplicito per aggiungere contenuto. Come best practice, considera l’assemblaggio di un set di contenuti da utilizzare come contenuto di prova per la convalida o il debug delle funzioni nell’RDE. Esistono diverse strategie possibili per popolare l’RDE con tale contenuto:

1. Sincronizza esplicitamente il pacchetto di contenuti con l’RDE utilizzando gli strumenti della riga di comando

1. Posiziona e esegui il commit del contenuto di esempio in git all’interno di una cartella install.rde in /apps, quindi sincronizza il pacchetto di contenuto complessivo con l’RDE utilizzando gli strumenti della riga di comando.

1. Utilizza la [strumento copia contenuto](/help/implementing/developing/tools/content-copy.md) per copiare un set di contenuti definito da ambienti prod, stage o dev o da un altro RDE.

1. Utilizzo di Gestione pacchetti

Tieni presente che la sincronizzazione dei pacchetti di contenuti è limitata a 1 GB.

## Registrazione {#logging}

I livelli di registro possono essere impostati modificando le configurazioni OSGi. Controlla la [documentazione](/help/implementing/developing/introduction/logging.md) per ulteriori informazioni.

## Quali sono le differenze tra gli RDE e gli ambienti di sviluppo cloud? {#how-are-rds-different-from-cloud-development-environments}

Sebbene l’RDE sia in molti modi simile a un ambiente di sviluppo cloud, esistono alcune differenze architettoniche minori per consentire una sincronizzazione rapida del codice. Il meccanismo per ottenere il codice all’RDE è diverso: per gli RDE, un codice sincronizzato da un ambiente di sviluppo locale, mentre per gli ambienti di sviluppo cloud, uno distribuisce il codice tramite Cloud Manager.

Per questi motivi, dopo aver convalidato il codice in un ambiente RDE, devi distribuire il codice in un ambiente di sviluppo Cloud utilizzando la pipeline non di produzione. Infine, testa il codice prima di distribuirlo con la pipeline di produzione.

Considera anche le seguenti considerazioni:

* Gli RDE non includono un livello di anteprima
* Gli RDE non supportano attualmente la visualizzazione e il debug del codice front-end distribuito utilizzando la pipeline front-end di Cloud Manager.
* Attualmente gli RDE non supportano il canale prerelease.


## Di quanti RDE ho bisogno? {#how-many-rds-do-i-need}

È disponibile un RDE per ogni soluzione con licenza e Adobe offre anche altri RDE, che possono essere concessi in licenza per i programmi di produzione (non sandbox).

Il numero di RDE necessari dipende dalla composizione e dai processi di un&#39;organizzazione. Il modello più flessibile è quello in cui un’organizzazione acquista un RDE dedicato per ciascuno dei propri sviluppatori AEM Cloud Service. In questo modello, ogni sviluppatore può testare il proprio codice sull’RDE senza coordinarsi con altri membri del team riguardo alla disponibilità di un ambiente RDE.

All’altro estremo, un team con un singolo RDE può utilizzare processi interni per coordinare quali sviluppatori possono utilizzare l’ambiente in un dato momento. Questo può accadere ogni volta che uno sviluppatore raggiunge una fase cardine di una funzione intermedia ed è pronto per la convalida in un ambiente Cloud in cui può apportare rapidamente le modifiche necessarie.

Un modello intermedio è quello in cui un’organizzazione acquista un numero di RDE, quindi c’è una maggiore probabilità che un RDE non utilizzato sia disponibile. Una strategia potrebbe essere quella di allocare un RDE per team di script o funzionalità principali. I processi interni possono essere utilizzati per coordinare l’utilizzo degli ambienti.

## In che modo un ambiente AEM Forms Cloud Service Rapid Development Environment (RDE) è diverso da altri ambienti? {#how-are-forms-rds-different-from-cloud-development-environments}

Gli sviluppatori Forms possono utilizzare AEM Forms Cloud Service Rapid Development Environment per sviluppare rapidamente Forms adattivo, flussi di lavoro e personalizzazioni come la personalizzazione di componenti core, integrazioni con sistemi di terze parti e altro ancora. L’ambiente AEM Forms Cloud Service Rapid Development Environment (RDE) non supporta le API di comunicazione e le funzioni e le funzionalità che richiedono Document of Record, come la generazione di un documento di record all’invio di un modulo adattivo. Le seguenti funzioni di AEM Forms elencate non sono disponibili in un ambiente di sviluppo rapido (RDE):

* Configurazione di un documento di record per un modulo adattivo
* Generazione di un documento di record all’invio di un modulo adattivo o con un passaggio del flusso di lavoro
* Invia documento come allegato con azione Invia per e-mail o con passaggio E-mail in un flusso di lavoro
* Utilizzo di Adobe Sign in un modulo adattivo o in un passaggio del flusso di lavoro
* API di comunicazione

>[!NOTE]
>
> Non vi è alcuna differenza tra l’interfaccia utente di Rapid Development Environment (RDE) e altri ambienti di Cloud Service per Forms. Tutte le opzioni relative al documento di record, come la selezione di un modello di documento per un modulo adattivo, continuano a essere visualizzate nell’interfaccia utente. Questi ambienti non dispongono di API di comunicazione e funzionalità di documentazione per testare tali opzioni. Quindi, quando scegli un’opzione che richiede le funzionalità API di comunicazione o Documento di record, non viene eseguita alcuna azione e viene visualizzato o restituito un messaggio di errore.

## Esercitazione RDE

Per informazioni sull’RDE in AEM as a Cloud Service, consulta [tutorial video che illustra come configurarlo, come utilizzarlo e il ciclo di vita dello sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)
