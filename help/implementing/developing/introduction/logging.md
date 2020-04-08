---
title: Registrazione
description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

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

## Registrazione globale {#global-logging}

[La configurazione](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) Apache Sling Logging viene utilizzata per configurare il logger radice. Definisce le impostazioni globali per l’accesso ad AEM come servizio cloud:

* livello di registrazione
* posizione del file di registro centrale
* il numero di versioni da conservare
* rotazione della versione; dimensione massima o intervallo di tempo
* il formato da utilizzare per la scrittura dei messaggi di registro

## Loggers e scrittori per servizi individuali {#loggers-and-writers-for-individual-services}

Oltre alle impostazioni di accesso globali, AEM come servizio cloud consente di configurare impostazioni specifiche per un singolo servizio:

* il livello di registrazione specifico
* il percorso del singolo file di registro
* il numero di versioni da conservare
* rotazione della versione; dimensione massima o intervallo di tempo
* il formato da utilizzare per la scrittura dei messaggi di registro
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
   1. Configurate gli altri parametri come necessario.

1. Create una nuova istanza della configurazione [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Specificare il file di registro. Deve corrispondere a quello specificato per il logger.
   1. Configurate gli altri parametri come necessario.

### Creare un file di registro personalizzato {#create-a-custom-log-file}

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

1. Imposta le seguenti proprietà su questo nodo:

   * Nome: `org.apache.sling.commons.log.file`

      Tipo: Stringa

      Valore: specifica il file di registro; ad esempio, `logs/myLogFile.log`

   * Nome: `org.apache.sling.commons.log.names`

      Tipo: Stringa[] (String + Multi)

      Valore: specificare i servizi OSGi per i quali il logger deve registrare i messaggi; ad esempio, tutti i seguenti elementi:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * Nome: `org.apache.sling.commons.log.level`

      Tipo: Stringa

      Valore: specificare il livello di registro richiesto ( `debug`, `info`, `warn` o `error`); ad esempio `debug`

   * Configurate gli altri parametri come richiesto:

      * Nome: `org.apache.sling.commons.log.pattern`

         Tipo: `String`

         Valore: specificare il pattern del messaggio di registro come richiesto; ad esempio,

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supporta fino a sei argomenti.

   >{0} Il timestamp del tipo `java.util.Date`
   >
   >{1} l&#39;indicatore di registro{2} il nome del thread corrente{3} il nome del logger{4} il livello di registro{5} il messaggio di registro

   >Se la chiamata di registro include una traccia `Throwable` di stack, questa viene aggiunta al messaggio.

   >[!CAUTION]
   org.apache.sling.commons.log.names deve avere un valore.

   >[!NOTE]
   I percorsi di scrittura del registro sono relativi alla `crx-quickstart` posizione.
   Pertanto, un file di registro specificato come:
   `logs/thelog.log`

   >scrive in:
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   E un file di registro specificato come:
   `../logs/thelog.log`

   >scrive in una directory:
   ` <*cq-installation-dir*>/logs/`
&quot;(ovvero accanto a ` `&lt;*cq-installing-dir*>/`crx-quickstart/`)

1. Questo passaggio è necessario solo quando è necessario un nuovo Writer (ad es. con una configurazione diversa da quella del Writer predefinito).

   >[!CAUTION]
   È necessaria una nuova configurazione per l&#39;utente che esegue l&#39;accesso solo se l&#39;impostazione predefinita esistente non è adatta.

   >Se non è configurato alcun Writer esplicito, il sistema genererà automaticamente un Writer implicito in base all&#39;impostazione predefinita.

   In `/apps/<*project-name*>/config`, create un nodo per la nuova `Apache Sling Logging Writer` configurazione:

   * Nome: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (in quanto si tratta di uno scrittore)

      Come con il Logger, `<*identifier*>` viene sostituito da testo libero che è necessario immettere per identificare l’istanza (non è possibile omettere tali informazioni). Esempio, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   Anche se non è un requisito tecnico, è consigliabile rendere `<*identifier*>` unico.

   Imposta le seguenti proprietà su questo nodo:

   * Nome: `org.apache.sling.commons.log.file`

      Tipo: `String`

      Valore: specificare il file di registro in modo che corrisponda al file specificato nel logger;

      in questo esempio, `../logs/myLogFile.log`.

   * Configurate gli altri parametri come richiesto:

      * Nome: `org.apache.sling.commons.log.file.number`

         Tipo: `Long`

         Valore: specificare il numero di file di registro da conservare; ad esempio, `5`

      * Nome: `org.apache.sling.commons.log.file.size`

         Tipo: `String`

         Valore: specificare come necessario per controllare la rotazione del file per dimensione/data; ad esempio, `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` controlla la rotazione del file di registro impostando:
   * una dimensione massima del file
   * una pianificazione di ora/data
   per indicare quando verrà creato un nuovo file (e il file esistente verrà rinominato in base al pattern del nome).
   * È possibile specificare un limite di dimensioni con un numero. Se non viene fornito alcun indicatore di dimensione, questo viene considerato come il numero di byte, oppure è possibile aggiungere uno degli indicatori di dimensione - `KB`, `MB`o `GB` (il caso viene ignorato).
   * È possibile specificare come `java.util.SimpleDateFormat` pattern una pianificazione di ora/data. Definisce il periodo di tempo dopo il quale il file verrà ruotato; inoltre il suffisso aggiunto al file ruotato (per l’identificazione).
   Il valore predefinito è &#39;.&#39;yyyy-MM-dd (per la rotazione giornaliera del registro).
   Ad esempio, a mezzanotte del 20 gennaio 2010 (o quando il primo messaggio di registro dopo tale data sarà preciso), ../logs/error.log verrà rinominato in ../logs/error.log.2010-01-20. La registrazione per il 21 gennaio verrà restituita a (un nuovo e vuoto) ../logs/error.log finché non viene eseguito il rollback al cambio di giorno successivo.
       | `&#39;.&#39;yyyy-MM`|Rotazione all&#39;inizio di ogni mese|
    |—|—|
    | `&#39;.&quot;yyyy-ww`|Rotazione al primo giorno di ogni settimana (a seconda delle impostazioni internazionali). |
       | `&#39;.&#39;yyyy-MM-dd`|Rotazione a mezzanotte ogni giorno. |
       | `&#39;.&#39;yyyy-MM-dd-a`|Rotazione a mezzanotte e a mezzogiorno di ogni giorno. |
       | `&#39;.&#39;yyyy-MM-dd-HH`|Rotazione nella parte superiore di ogni ora. |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm&quot;|Rotazione all&#39;inizio di ogni minuto. |
     
     Nota: Quando si specifica un&#39;ora/data:
       1. È necessario &quot;escape&quot; testo letterale all&#39;interno di una coppia di virgolette singole (&#39; &#39;);
   per     evitare che alcuni caratteri vengano interpretati come lettere del pattern.
       1. Utilizzate solo i caratteri consentiti per un nome di file valido in qualsiasi punto dell&#39;opzione.
   

1. Leggere il nuovo file di registro con lo strumento scelto.

   Il file di registro creato da questo esempio sarà `../crx-quickstart/logs/myLogFile.log`.

La console Felix fornisce inoltre informazioni sul supporto dei log Sling in `../system/console/slinglog`; ad esempio `https://localhost:4502/system/console/slinglog`.draf