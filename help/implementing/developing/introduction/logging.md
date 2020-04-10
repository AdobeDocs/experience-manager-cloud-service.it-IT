---
title: Registrazione
description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
translation-type: tm+mt
source-git-commit: 1b10561af9349059aaee97e4f42d2e339f629700

---


# Registrazione{#logging}

AEM come servizio cloud ti offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni di richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di registro e un formato per i messaggi di registro

Per lo sviluppo locale, le voci di registro sono scritte in file locali nella `/crx-quickstart/logs` cartella.

Negli ambienti Cloud, gli sviluppatori possono scaricare i registri tramite Cloud Manager o utilizzare uno strumento della riga di comando per localizzare i registri.

>[!NOTE]
>
>L&#39;accesso a AEM come servizio cloud si basa sui principi Sling. Per ulteriori informazioni, consulta Registrazione [Sling](https://sling.apache.org/site/logging.html) .

<!-- ## Global Logging {#global-logging}

[Apache Sling Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) is used to configure the root logger. This defines the global settings for logging in AEM as a Cloud Service:

* the logging level
* the location of the central log file
* the number of versions to be kept
* version rotation; either maximum size or a time interval
* the format to be used when writing the log messages
-->

## Loggers e scrittori per servizi individuali {#loggers-and-writers-for-individual-services}

Oltre alle impostazioni di accesso globali, AEM come servizio cloud consente di configurare impostazioni specifiche per un singolo servizio:

* il livello di registrazione specifico
* logger (il servizio OSGi che fornisce i messaggi di registro)

Questo consente di incanalare i messaggi di registro per un singolo servizio in un file separato. Ciò può essere particolarmente utile durante lo sviluppo o i test; ad esempio, quando è necessario un livello di registro maggiore per un servizio specifico.

AEM come servizio Cloud utilizza i seguenti strumenti per scrivere messaggi di registro nel file:

1. Un servizio **** OSGi (logger) scrive un messaggio di registro.
1. Un **Registratore** di registrazione riceve questo messaggio e lo formatta in base alle specifiche dell’utente.
1. Un **utente che esegue la registrazione** scrive tutti questi messaggi nel file fisico definito.

Questi elementi sono collegati dai seguenti parametri per gli elementi appropriati:

* **Logger (Logging)**

   Definite i servizi che generano i messaggi.

* **File di registro (Logging Logger)**

   Definire il file fisico per la memorizzazione dei messaggi di registro.

   Viene utilizzato per collegare un Registratore di registrazione a un Registratore di registrazione. Per stabilire la connessione, il valore deve essere identico allo stesso parametro nella configurazione di Log Writer.

* **File di registro (Registratore Di Registrazione)**

   Definire il file fisico in cui verranno scritti i messaggi di registro.

   Deve essere identico allo stesso parametro nella configurazione di Logging Writer, altrimenti la corrispondenza non verrà effettuata. Se non esiste alcuna corrispondenza, verrà creato un Writer implicito con configurazione predefinita (rotazione del registro giornaliera).

### Registratori e scrittori standard {#standard-loggers-and-writers}

Alcuni logger e scrittori sono inclusi in un’installazione standard di AEM come servizio cloud.

Il primo è un caso speciale in quanto controlla sia i `request.log` file che i `access.log` file:

* Il Logger:

   * Apache Sling Custom Request Data Logger

      (org.apache.sling.Engine.impl.log.RequestLoggerService)

   * Scrivete messaggi sul contenuto della richiesta a `request.log`.

* Collegamenti a:

   * Registratore di richieste Apache Sling

      (org.apache.sling.Engine.impl.log.RequestLogger)

   * Scrive i messaggi in `request.log` o `access.log`.

Questi possono essere personalizzati se necessario, anche se la configurazione standard è adatta per la maggior parte delle installazioni.

Le altre coppie seguono la configurazione standard:

* Il Logger:

   * Configurazione Del Registratore Di Registrazione Apache Sling

      (org.apache.sling.commons.log.LogManager.factory.config)

   * Scrive `Information` i messaggi in `logs/error.log`.

* Collegamenti allo scrittore:

   * Configurazione dello scrittore di registrazione Apache Sling

      (org.apache.sling.commons.log.LogManager.factory.writer)

* Il Logger:

   * Configurazione del logger di registrazione Apache Sling(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Scrive `Warning` messaggi in `../logs/error.log` per il servizio `org.apache.pdfbox`.

* Non si collega a uno specifico Writer in modo da creare e utilizzare un Writer implicito con configurazione predefinita (rotazione del registro giornaliera).

## Impostazione del livello di registro {#setting-the-log-level}

Per modificare i livelli di registro per gli ambienti Cloud, la configurazione Sling Logging OSGI deve essere modificata, seguita da una ridistribuzione completa. Poiché non è istantaneo, essere cauti nell&#39;attivare log verbosi in ambienti di produzione che ricevono molto traffico. In futuro, è possibile che ci saranno meccanismi per cambiare più rapidamente il livello di registro.

>[!NOTE]
>
> Per eseguire le modifiche di configurazione elencate di seguito, è necessario crearle in un ambiente di sviluppo locale e quindi inviarle a un’istanza AEM come servizio cloud. Per ulteriori informazioni su come eseguire questa operazione, consulta [Implementazione in AEM come servizio](/help/implementing/deploying/overview.md)cloud.

### Attivazione del livello di registro DEBUG {#activating-the-debug-log-level}

>[!WARNING]
>
> Attivando il livello di registro DEBUG a livello globale, si genererà una grande quantità di informazioni che sarà difficile setacciare. È consigliabile attivarla solo per i servizi che richiedono il debug. Per ulteriori informazioni, consulta [Registratori e Scrittori per i servizi](logging.md#loggers-and-writers-for-individual-services)individuali.

Il livello di registro predefinito è INFO, ovvero i messaggi DEBUG non vengono registrati.
Per attivare il livello di registro DEBUG, impostare la variabile

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

da eseguire il debug. Non lasciare il registro a livello di registro DEBUG più a lungo del necessario, in quanto genera molti registri.
Una riga nel file di debug in genere inizia con DEBUG, quindi fornisce il livello di registro, l&#39;azione del programma di installazione e il messaggio di registro. Esempio:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

I livelli di registro sono i seguenti:

| 0 | Errore irreversibile | L&#39;azione non è riuscita e il programma di installazione non può proseguire. |
|---|---|---|
| 1 | Errore | L&#39;azione non è riuscita. L&#39;installazione continua, ma una parte di CRX non è stata installata correttamente e non funzionerà. |
| 2 | Avvertenza | L&#39;azione è riuscita ma ha incontrato dei problemi. CRX può funzionare o meno correttamente. |
| 3 | Informazioni | L&#39;azione è riuscita. |

### Creazione di registri e scrittori personalizzati {#creating-your-own-loggers-and-writers}

Puoi definire la tua coppia Logger/Writer:

1. Create una nuova istanza della configurazione [Apache Sling Logging Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Specificate il file di registro.
   1. Specificate il logger.

<!-- 1. Create a new instance of the Factory Configuration [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

    1. Specify the Log File - this must match that specified for the Logger.
    1. Configure the other parameters as required. -->

### Configurare la registrazione {#configure-logging}

>[!NOTE]
>
>Quando lavori con Adobe Experience Manager, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi.

In alcune circostanze può essere utile creare un file di registro personalizzato con un livello di registro diverso. È possibile eseguire questa operazione nella directory archivio:

1. Se non già esistente, create una nuova cartella di configurazione ( `sling:Folder`) per il progetto `/apps/<*project-name*>/config`.
1. In `/apps/<*project-name*>/config`, create un nodo per la nuova configurazione del logger di registrazione Apache Sling:

   * Nome: `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (in quanto si tratta di un Logger)

      Dove `<*identifier*>` viene sostituito da testo libero che è necessario immettere per identificare l’istanza (non è possibile omettere tali informazioni).

      Esempio, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Anche se non è un requisito tecnico, è consigliabile rendere `<*identifier*>` unico.

<!-- 1. Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: String

      Value: specify the Log File; for example, `logs/myLogFile.log`

    * Name: `org.apache.sling.commons.log.names`

      Type: String[] (String + Multi)

      Value: specify the OSGi services for which the Logger is to log messages; for example, all of the following:

        * `org.apache.sling`
        * `org.apache.felix`
        * `com.day`

    * Name: `org.apache.sling.commons.log.level`

      Type: String

      Value: specify the log level required ( `debug`, `info`, `warn` or `error`); for example `debug`

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.pattern`

          Type: `String`

          Value: specify the pattern of the log message as required; for example,

          `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supports up to six arguments.

   >
   >
   >{0} The timestamp of type `java.util.Date`
   >{1} the log marker
   >{2} the name of the current thread
   >{3} the name of the logger
   >{4} the log level
   >{5} the log message

   >
   >
   >If the log call includes a `Throwable` the stacktrace is appended to the message.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names must have a value.

   >[!NOTE]
   >
   >Log writer paths are relative to the `crx-quickstart` location.
   >
   >
   >Therefore, a log file specified as:
   >
   >
   >`logs/thelog.log`

   >
   >
   >writes to:
   >
   >
   >`` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   >
   >
   >And a log file specified as:
   >
   >
   >`../logs/thelog.log`

   >
   >
   >writes to a directory:
   >
   >
   >` <*cq-installation-dir*>/logs/`
   >``(i.e. next to ` `<*cq-installation-dir*>/`crx-quickstart/`)
 -->

<!-- open question: see if we need to leave the above warning note in place, but adjust it so that it doesn't mention filenames -->

<!-- 1. This step is only necessary when a new Writer is required (i.e. with a configuration that is different to the default Writer).

   >[!CAUTION]
   >
   >A new Logging Writer Configuration is only required when the existing default is not suitable.

   >
   >
   >If no explicit Writer is configured the system will automatically generate an implicit Writer based on the default.

   Under `/apps/<*project-name*>/config`, create a node for the new `Apache Sling Logging Writer` Configuration:

    * Name: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (as this is a Writer)

      As with the Logger, `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

   Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: `String`

      Value: specify the Log File so that it matches the file specified in the Logger;

      for this example, `../logs/myLogFile.log`.

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.file.number`

          Type: `Long`

          Value: specify the number of log files you want kept; for example, `5`

        * Name: `org.apache.sling.commons.log.file.size`

          Type: `String`

          Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controls the rotation of the log file by setting either:
   >
   >* a maximum file size
   >* a time/date schedule
   >
   >to indicate when a new file will be created (and the existing file renamed according to the name pattern).
   >
   >* A size limit can be specified with a number. If no size indicator is given, then this is taken as the number of bytes, or you can add one of the size indicators - `KB`, `MB`, or `GB` (case is ignored).
   >* A time/date schedule can be specified as a `java.util.SimpleDateFormat` pattern. This defines the time period after which the file will be rotated; also the suffix appended to the rotated file (for identification).
   >
   >The default is '.'yyyy-MM-dd (for daily log rotation).
   >
   >So for example, at midnight of January 20th 2010 (or when the first log message after this occurs to be precise), ../logs/error.log will be renamed to ../logs/error.log.2010-01-20. Logging for the 21st of January will be output to (a new and empty) ../logs/error.log until it is rolled over at the next change of day.
   >
   >      | `'.'yyyy-MM` |Rotation at the beginning of each month |
   >      |---|---|
   >      | `'.'yyyy-ww` |Rotation at the first day of each week (depends on the locale). |
   >      | `'.'yyyy-MM-dd` |Rotation at midnight each day. |
   >      | `'.'yyyy-MM-dd-a` |Rotation at midnight and midday of each day. |
   >      | `'.'yyyy-MM-dd-HH` |Rotation at the top of every hour. |
   >      | `'.'yyyy-MM-dd-HH-mm` |Rotation at the beginning of every minute. |
   >
   >      Note: When specifying a time/date:
   >      1. You should "escape" literal text within a pair of single quotes (' ');
   >      this is to avoid certain characters being interpreted as pattern letters.
   >      1. Only use characters allowed for a valid file name anywhere in the option.

1. Read your new log file with your chosen tool.

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`. -->

La console Felix fornisce inoltre informazioni sul supporto dei log Sling in `../system/console/slinglog`; ad esempio `https://localhost:4502/system/console/slinglog`.draf