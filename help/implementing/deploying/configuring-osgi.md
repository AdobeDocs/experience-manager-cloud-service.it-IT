---
title: Configurazione di OSGi per Adobe Experience Manager as a Cloud Service
description: Configurazione OSGi con valori segreti e valori specifici dell’ambiente
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '3317'
ht-degree: 1%

---

# Configurazione di OSGi per Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Con la versione 2021.12.0, l’AEM ha introdotto la possibilità di utilizzare l’interfaccia utente di Cloud Manager per configurare le variabili di ambiente standard. Per ulteriori informazioni, consulta la documentazione [qui](/help/implementing/cloud-manager/environment-variables.md).

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi dell&#39;AEM e le sue configurazioni.

OSGi fornisce le primitive standardizzate che consentono di creare applicazioni partendo da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un’applicazione e distribuiti. Questo consente di gestire facilmente i bundle OSGi che possono essere arrestati, installati e avviati singolarmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi è contenuto in uno dei vari bundle. Per ulteriori informazioni, vedere [Specifiche OSGi](https://help.eclipse.org/latest/index.jsp).

Puoi gestire le impostazioni di configurazione per i componenti OSGi tramite i file di configurazione che fanno parte di un progetto di codice AEM.

## File di configurazione OSGi {#osgi-configuration-files}

Le modifiche alla configurazione sono definite nei pacchetti di codice del progetto AEM (`ui.apps`) come file di configurazione (`.cfg.json`) in cartelle di configurazione specifiche per la modalità di esecuzione:

`/apps/example/config.<runmode>`

Il formato dei file di configurazione OSGi è basato su JSON utilizzando `.cfg.json` formato definito dal progetto Apache Sling.

Le configurazioni OSGi eseguono il targeting dei componenti OSGi tramite il PID (Persistent Identity), che per impostazione predefinita corrisponde al nome della classe Java™ del componente OSGi. Ad esempio, per fornire la configurazione OSGi per un servizio OSGi implementato da:

`com.example.workflow.impl.ApprovalWorkflow.java`

un file di configurazione OSGi è definito in:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

dopo il `cfg.json` Formato di configurazione OSGi.

>[!NOTE]
>
>Versioni precedenti dei file di configurazione OSGi supportati da AEM che utilizzano diversi formati di file, ad esempio `.cfg`, `.config` e come XML `sling:OsgiConfig` definizioni delle risorse. Questi formati sono sostituiti da `.cfg.json` Formato di configurazione OSGi.

## Risoluzione runmode {#runmode-resolution}

>[!TIP]
>
>AEM 6.x supporta modalità di esecuzione personalizzate, ma AEM as a Cloud Service no. Supporto as a Cloud Service AEM e [set esatto di modalità di esecuzione](./overview.md#runmodes). Qualsiasi variazione nelle configurazioni OSGi tra ambienti AEM as a Cloud Service deve essere gestita utilizzando [Variabili di ambiente di configurazione OSGi](#environment-specific-configuration-values).

Configurazioni OSGi specifiche possono essere indirizzate a istanze AEM specifiche utilizzando modalità di esecuzione. Per utilizzare runmode, crea cartelle di configurazione in `/apps/example` (dove esempio è il nome del progetto), nel formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Tutte le configurazioni OSGi in tali cartelle vengono utilizzate se le modalità di esecuzione definite nel nome della cartella di configurazione corrispondono a quelle utilizzate dall’AEM.

Ad esempio, se l’AEM utilizza le modalità di esecuzione author e dev, i nodi di configurazione in `/apps/example/config.author/` e `/apps/example/config.author.dev/` , mentre i nodi di configurazione in `/apps/example/config.publish/` e `/apps/example/config.author.stage/` non vengono applicati.

Se sono applicabili più configurazioni per lo stesso PID, viene applicata la configurazione con il maggior numero di modalità di esecuzione corrispondenti.

La granularità di questa regola è a livello PID. Ciò significa che non è possibile definire alcune proprietà per lo stesso PID in `/apps/example/config.author/` e più specifici in `/apps/example/config.author.dev/` per lo stesso PID. La configurazione con il maggior numero di modalità di esecuzione corrispondenti è efficace per l’intero PID.

>[!NOTE]
>
>A `config.preview` Cartella di configurazione OSGi **non può** essere dichiarata allo stesso modo `config.publish` può essere dichiarata cartella. Il livello di anteprima eredita invece la configurazione OSGi dai valori del livello di pubblicazione.

Quando si sviluppa localmente, un parametro di avvio in modalità di esecuzione, `-r`, viene utilizzato per specificare la configurazione OSGI in modalità di esecuzione.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### Verifica delle modalità di esecuzione

Le modalità di esecuzione dell’AEM as a Cloud Service sono ben definite in base al tipo di ambiente e al servizio. Rivedi [elenco completo delle modalità di esecuzione AEM as a Cloud Service disponibili](./overview.md#runmodes).

I valori di configurazione OSGi specificati dalla modalità di esecuzione possono essere verificati da:

1. Aprire l&#39;AEM come Cloud Service [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it)
1. Selezione dei livelli di servizio da controllare, utilizzando __Pod__ elenco a discesa
1. Selezione del __Stato__ scheda
1. Selezione __Configurazioni__ dal __Immagine stato__ elenco a discesa
1. Selezione del __Ottieni stato__ pulsante

La vista risultante mostra tutte le configurazioni dei componenti OSGi per i livelli selezionati con i relativi valori di configurazione OSGi applicabili. Questi valori possono essere confrontati con i valori di configurazione OSGi nel codice sorgente del progetto AEM in `/apps/example/osgiconfig/config.<runmode(s)>`.


Per verificare che vengano applicati i valori di configurazione OSGi appropriati:

1. Nell’output di configurazione della Console per sviluppatori
1. Individua il `pid` che rappresenta la configurazione OSGi da verificare; questo è il nome del file di configurazione OSGi nel codice sorgente del progetto AEM.
1. Inspect `properties` elenco per `pid` e verifica che la chiave e i valori corrispondano al file di configurazione OSGi nel codice sorgente del progetto AEM per la modalità di esecuzione da verificare.=


## Tipi di valori di configurazione OSGi {#types-of-osgi-configuration-values}

Esistono tre varietà di valori di configurazione OSGi che possono essere utilizzati con Adobe Experience Manager as a Cloud Service.

1. **Valori in linea**, valori inseriti a livello di codice nella configurazione OSGi e memorizzati in Git. Ad esempio:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valori segreti**, valori che non devono essere memorizzati in Git per motivi di sicurezza. Ad esempio:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Valori specifici dell’ambiente**, valori che variano tra ambienti di sviluppo e che pertanto non possono essere oggetto di targeting accurato tramite la modalità di esecuzione (poiché esiste un singolo `dev` in Adobe Experience Manager as a Cloud Service). Ad esempio:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Un singolo file di configurazione OSGi può utilizzare insieme qualsiasi combinazione di questi tipi di valori di configurazione. Ad esempio:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Come scegliere il tipo di valore di configurazione OSGi appropriato {#how-to-choose-the-appropriate-osgi-configuration-value-type}

Nel caso comune di OSGi, vengono utilizzati i valori di configurazione OSGi in linea. Le configurazioni specifiche dell’ambiente vengono utilizzate solo per casi d’uso specifici in cui un valore differisce tra ambienti di sviluppo.

![Struttura decisionale per l’utilizzo del tipo di valore di configurazione appropriato](assets/choose-configuration-value-type_res1.png)

Le configurazioni specifiche dell’ambiente estendono le configurazioni OSGi tradizionali definite in modo statico che contengono valori in linea, consentendo di gestire i valori di configurazione OSGi esternamente tramite l’API di Cloud Manager. È importante capire quando deve essere utilizzato l’approccio comune e tradizionale per definire i valori in linea e memorizzarli in Git, anziché astrarre i valori in configurazioni specifiche per l’ambiente.

Le seguenti indicazioni spiegano quando utilizzare configurazioni non segrete e segrete specifiche per l’ambiente:

### Quando utilizzare i valori di configurazione in linea {#when-to-use-inline-configuration-values}

I valori delle configurazioni in linea sono considerati l’approccio standard e devono essere utilizzati quando possibile. Le configurazioni in linea offrono i vantaggi di:

* Vengono mantenuti, con governance e cronologia delle versioni in Git
* I valori sono implicitamente associati alle distribuzioni del codice
* Non richiedono ulteriori considerazioni sulla distribuzione o sul coordinamento

Quando definisci un valore di configurazione OSGi, inizia con valori in linea e seleziona solo configurazioni segrete o specifiche dell’ambiente, se necessario per il caso d’uso.

### Quando utilizzare valori di configurazione non segreti specifici dell’ambiente {#when-to-use-non-secret-environment-specific-configuration-values}

Utilizza solo configurazioni specifiche dell’ambiente (`$[env:ENV_VAR_NAME]`) per i valori di configurazione non segreti quando i valori variano per il livello di anteprima o variano tra gli ambienti di sviluppo. Ciò include le istanze di sviluppo locali e qualsiasi ambiente di sviluppo Adobe Experience Manager as a Cloud Service. A parte l’impostazione di valori univoci per il livello di anteprima, evita di utilizzare configurazioni non segrete specifiche dell’ambiente per gli ambienti Adobe Experience Manager as a Cloud Service Stage o Production.

* Utilizza solo configurazioni non segrete specifiche dell’ambiente per valori di configurazione diversi tra il livello di pubblicazione e quello di anteprima o per valori diversi tra ambienti di sviluppo, incluse le istanze di sviluppo locali.
* A parte lo scenario in cui il livello di anteprima deve variare rispetto al livello di pubblicazione, utilizza i valori in linea standard nelle configurazioni OSGi per i valori non segreti di Stage e Production. In relazione a ciò, non è consigliabile utilizzare configurazioni specifiche per l’ambiente per facilitare l’apporto di modifiche alla configurazione in fase di esecuzione degli ambienti di staging e produzione; tali modifiche devono essere introdotte tramite la gestione del codice sorgente.

### Quando utilizzare i valori di configurazione segreti specifici dell’ambiente {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service richiede l’utilizzo di configurazioni specifiche per l’ambiente (`$[secret:SECRET_VAR_NAME]`) per eventuali valori di configurazione OSGi segreti, ad esempio password, chiavi API private o qualsiasi altro valore che non può essere memorizzato in Git per motivi di sicurezza.

Utilizza configurazioni segrete specifiche per l’ambiente per archiviare il valore dei segreti in tutti gli ambienti Adobe Experience Manager as a Cloud Service, inclusi Stage e Produzione.

## Creazione di configurazioni OSGi {#creating-osgi-configurations}

Esistono due modi per creare configurazioni OSGi, come descritto di seguito. Il primo approccio è in genere utilizzato per configurare componenti OSGi personalizzati con proprietà e valori OSGi noti da parte dello sviluppatore e il secondo per i componenti OSGi forniti dall’AEM.

### Scrittura delle configurazioni OSGi {#writing-osgi-configurations}

I file di configurazione OSGi in formato JSON possono essere scritti manualmente nel progetto AEM. Questo è spesso il modo più rapido per creare configurazioni OSGi per componenti OSGi noti, in particolare componenti OSGi personalizzati progettati e sviluppati dallo stesso sviluppatore che definisce le configurazioni. Questo approccio può essere utilizzato anche per copiare/incollare e aggiornare configurazioni per lo stesso componente OSGi in varie cartelle in modalità di esecuzione.

1. Nell’IDE, apri il file `ui.apps` , individuare o creare la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue il targeting delle modalità di esecuzione che la nuova configurazione OSGi deve eseguire
1. In questa cartella di configurazione, crea un `<PID>.cfg.json` file. Il PID è l’identità persistente del componente OSGi. In genere è il nome completo della classe dell’implementazione del componente OSGi. Ad esempio:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
I nomi dei file di factory della configurazione OSGi utilizzano `<factoryPID>-<name>.cfg.json` convenzione di denominazione
1. Apri il nuovo `.cfg.json` e definiscono le combinazioni chiave/valore per le coppie proprietà e valore OSGi, seguendo la [Formato di configurazione JSON OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Salva le modifiche nel nuovo `.cfg.json` file
1. Aggiungi e conferma il nuovo file di configurazione OSGi su Git

### Generazione di configurazioni OSGi tramite QuickStart per SDK AEM {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

La console web AEM di Quickstart Jar per AEM SDK può essere utilizzata per configurare i componenti OSGi ed esportare le configurazioni OSGi come JSON. Questo è utile per configurare i componenti OSGi forniti dall’AEM le cui proprietà OSGi e i relativi formati di valore potrebbero non essere ben compresi dallo sviluppatore che definisce le configurazioni OSGi nel progetto AEM.

>[!NOTE]
>
>L’interfaccia utente di configurazione della console web dell’AEM scrive `.cfg.json` file nel repository. Pertanto, tieni presente questo flusso di lavoro per evitare potenziali comportamenti imprevisti durante lo sviluppo locale, quando le configurazioni OSGi definite dal progetto AEM possono differire dalle configurazioni generate.

1. Accedi alla console web AEM di Quickstart Jar per l’SDK dell’AEM all’indirizzo `https://<host>:<port>/system/console` come utente amministratore
1. Accedi a **OSGi** > **Configurazione**
1. Per configurare, individua il componente OSGi e tocca il suo titolo per modificarlo
   ![Configurazione OSGi](./assets/configuring-osgi/configuration.png)
1. Modifica i valori delle proprietà di configurazione OSGi tramite l’interfaccia web, in base alle esigenze
1. Registra il PID (Persistent Identity) in un luogo sicuro. Viene utilizzato in seguito per generare il JSON di configurazione OSGi
1. Tocca Salva
1. Passa a OSGi > Stampante di configurazione del programma di installazione OSGi
1. Incolla il PID copiato nel passaggio 5, assicurati che il formato di serializzazione sia impostato su &quot;OSGi Configurator JSON&quot;
1. Tocca Stampa
1. La configurazione OSGi in formato JSON verrà visualizzata nella sezione Proprietà di configurazione serializzata
   ![Stampante di configurazione OSGi Installer](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. Nell’IDE, apri il file `ui.apps` , individuare o creare la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue il targeting delle modalità di esecuzione che la nuova configurazione OSGi deve applicare.
1. In questa cartella di configurazione, crea un `<PID>.cfg.json` file. Il PID è lo stesso valore del passaggio 5.
1. Incolla le proprietà di configurazione serializzate dal passaggio 10 nel `.cfg.json` file.
1. Salva le modifiche nel nuovo `.cfg.json` file.
1. Aggiungi e conferma il nuovo file di configurazione OSGi su Git.


## Formati delle proprietà di configurazione OSGi {#osgi-configuration-property-formats}

### Valori in linea {#inline-values}

I valori in linea sono formattati come coppie nome-valore standard, seguendo la sintassi JSON standard. Ad esempio:

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### Valori di configurazione specifici per l’ambiente {#environment-specific-configuration-values}

La configurazione OSGi deve assegnare un segnaposto per la variabile da definire in base all’ambiente:

```
use $[env:ENV_VAR_NAME]
```

I clienti devono utilizzare questa tecnica solo per le proprietà di configurazione OSGi relative al proprio codice personalizzato; non deve essere utilizzata per sostituire la configurazione OSGi definita da Adobe.

>[!NOTE]
>
>I segnaposto non possono essere utilizzati in [istruzioni repoinit](/help/implementing/deploying/overview.md#repoinit).

### Valori di configurazione segreti {#secret-configuration-values}

La configurazione OSGi deve assegnare un segnaposto per il segreto da definire in base all’ambiente:

```
use $[secret:SECRET_VAR_NAME]
```

### Denominazione variabile {#variable-naming}

Quanto segue si applica sia ai valori di configurazione specifici dell’ambiente che a quelli segreti.

I nomi delle variabili devono rispettare le seguenti regole:

* Lunghezza minima: 2
* Lunghezza massima: 100
* Deve corrispondere a regex: `[a-zA-Z_][a-zA-Z_0-9]*`

I valori per le variabili non devono superare i 2048 caratteri.

>[!CAUTION]
>
>Esistono regole relative all’utilizzo di alcuni prefissi per i nomi delle variabili:
>
>1. Nomi di variabili con prefisso `INTERNAL_`, `ADOBE_`, o `CONST_` sono riservati per Adobe. Tutte le variabili impostate dal cliente che iniziano con questi prefissi vengono ignorate.
>
>1. I clienti non devono fare riferimento a variabili con prefisso `INTERNAL_` o `ADOBE_` o.
>
>1. Variabili di ambiente con prefisso `AEM_` sono definite dal prodotto come API pubbliche che devono essere utilizzate e impostate dai clienti.
>   I clienti possono utilizzare e impostare le variabili di ambiente a partire dal prefisso `AEM_` con questo prefisso non devono definire le proprie variabili.

### Valori predefiniti {#default-values}

Quanto segue si applica sia ai valori di configurazione specifici dell’ambiente che a quelli segreti.

Se non viene impostato alcun valore per ambiente, in fase di runtime il segnaposto non viene sostituito e viene lasciato sul posto poiché non si è verificata alcuna interpolazione. Per evitare questo problema, è possibile fornire un valore predefinito come parte del segnaposto con la seguente sintassi:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Con un valore predefinito fornito, il segnaposto viene sostituito con il valore per ambiente, se fornito, o con il valore predefinito fornito.

### Sviluppo locale {#local-development}

Quanto segue si applica sia ai valori di configurazione specifici dell’ambiente che a quelli segreti.

Le variabili possono essere definite nell’ambiente locale in modo che vengano rilevate dall’AEM locale in fase di runtime. Ad esempio, su Linux®:

```bash
export ENV_VAR_NAME=my_value
```

Si consiglia di scrivere un semplice script bash che imposti le variabili di ambiente utilizzate nelle configurazioni e di eseguirlo prima di avviare l’AEM. Strumenti come [https://direnv.net/](https://direnv.net/) semplificare questo approccio. A seconda del tipo di valori, potrebbero essere archiviati nella gestione del codice sorgente, se possono essere condivisi tra tutti.

I valori per i segreti vengono letti dai file. Pertanto, per ogni segnaposto che utilizza un segreto, è necessario creare un file di testo contenente il valore segreto.

Ad esempio, se `$[secret:server_password]` viene utilizzato, un file di testo denominato **server_password** deve essere creato. Tutti questi file segreti devono essere archiviati nella stessa directory e nella proprietà framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` deve essere configurato con quella directory locale.

>[!CAUTION]
>
>Le estensioni di file non sono consentite per il file di testo.
>
>Per questo esempio, il file di testo deve essere denominato **server_password** - senza estensione file.

Il `org.apache.felix.configadmin.plugin.interpolation.secretsdir` è una proprietà del framework Sling; pertanto questa proprietà non viene impostata nella console felix (/system/console), ma nel file sling.properties utilizzato all’avvio del sistema. Questo file si trova nel sottodir /conf della cartella Jar/install estratta (crx-quickstart/conf).

esempio: aggiungi questa riga alla fine del file &#39;crx-quickstart/conf/sling.properties&#39; per configurare &#39;crx-quickstart/secretsdir&#39; come cartella segreta:

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### Configurazione Author e Publish {#author-vs-publish-configuration}

Se una proprietà OSGi richiede valori diversi per Author e Publish:

* Separa `config.author` e `config.publish` Utilizza le cartelle OSGi come descritto in [Sezione Risoluzione runmode](#runmode-resolution).
* Sono disponibili due opzioni per la creazione dei nomi di variabili indipendenti da utilizzare:
   * la prima opzione, consigliata: in tutte le cartelle OSGi (come `config.author` e `config.publish`) dichiarata per definire valori diversi, utilizza lo stesso nome di variabile. Per esempio
     `$[env:ENV_VAR_NAME;default=<value>]`, dove il valore predefinito corrisponde al valore predefinito per quel livello (di authoring o pubblicazione). Quando si imposta la variabile di ambiente tramite [API di Cloud Manager](#cloud-manager-api-format-for-setting-properties) o tramite un client, differenziare tra i livelli utilizzando il parametro &quot;service&quot; come descritto in questo [Documentazione di riferimento API](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/). Il parametro &quot;service&quot; associa il valore della variabile al livello OSGi appropriato. Può essere &quot;author&quot; o &quot;publish&quot; o &quot;preview&quot;.
   * la seconda opzione, che consiste nel dichiarare variabili distinte utilizzando un prefisso come `author_<samevariablename>` e `publish_<samevariablename>`

### Esempi di configurazione {#configuration-examples}

Negli esempi seguenti, supponiamo che ci siano tre ambienti di sviluppo, oltre agli ambienti di stage e di produzione.

**Esempio 1**

L’intento è il valore della proprietà OSGi `my_var1` per essere lo stesso per stage e prod, ma differire per ciascuno dei tre ambienti di sviluppo.

<table>
<tr>
<td>
<b>Cartella</b>
</td>
<td>
<b>Contenuto di myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

**Esempio 2**

L’intento è il valore della proprietà OSGi `my_var1` differire per stage, prod e per ciascuno dei tre ambienti di sviluppo. Pertanto, è necessario chiamare l’API di Cloud Manager per impostare il valore per `my_var1` per ogni ambiente di sviluppo

<table>
<tr>
<td>
<b>Cartella</b>
</td>
<td>
<b>Contenuto di myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

**Esempio 3**

L’intento è il valore della proprietà OSGi `my_var1` per essere lo stesso per gli ambienti di staging, produzione e solo per uno degli ambienti di sviluppo, ma per differenziarlo per gli altri due ambienti di sviluppo. In questo caso, è necessario chiamare l’API di Cloud Manager per impostare il valore di `my_var1` per ciascuno degli ambienti di sviluppo, incluso l’ambiente di sviluppo che deve avere lo stesso valore di stage e produzione. Non erediterà il valore impostato nella cartella **config**.

<table>
<tr>
<td>
<b>Cartella</b>
</td>
<td>
<b>Contenuto di myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

Un altro modo per eseguire questa operazione consiste nell’impostare un valore predefinito per il token di sostituzione nella cartella config.dev in modo che sia lo stesso valore presente nella cartella **config** cartella.

<table>
<tr>
<td>
<b>Cartella</b>
</td>
<td>
<b>Contenuto di myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

## Formato API di Cloud Manager per l’impostazione delle proprietà {#cloud-manager-api-format-for-setting-properties}

Consulta [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) informazioni sulla configurazione dell’API.
>[!NOTE]
>
>Assicurati che l’API di Cloud Manager utilizzata abbia assegnato il ruolo &quot;Responsabile dell’implementazione - Cloud Service&quot;. Gli altri ruoli non sono in grado di eseguire tutti i comandi seguenti.

### Impostazione dei valori tramite API {#setting-values-via-api}

Una chiamata all’API distribuisce le nuove variabili e i nuovi valori in un ambiente Cloud, in modo simile a una tipica pipeline di distribuzione del codice del cliente. I servizi di authoring e pubblicazione vengono riavviati e fanno riferimento ai nuovi valori, in genere dopo alcuni minuti.

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>Le variabili predefinite non vengono impostate tramite API, ma nella proprietà OSGi stessa.
>
>Consulta [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) per ulteriori informazioni.

### Recupero valori tramite API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Consulta [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) per ulteriori informazioni.

### Eliminazione dei valori tramite API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Per eliminare una variabile, includerla con un valore vuoto.

Consulta [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) per ulteriori informazioni.

### Recupero valori tramite la riga di comando {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### Impostazione dei valori tramite la riga di comando {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### Eliminazione dei valori tramite la riga di comando {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Consulta [questa pagina](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) per ulteriori informazioni su come configurare i valori utilizzando il plugin Cloud Manager, ad Adobe I/O CLI.

### Numero di variabili {#number-of-variables}

È possibile dichiarare fino a 200 variabili per ambiente.

## Considerazioni sull’implementazione per valori di configurazione segreti e specifici dell’ambiente {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Poiché i valori di configurazione segreti e specifici dell’ambiente si trovano al di fuori di Git e pertanto non fanno parte dei meccanismi formali di distribuzione di Adobe Experience Manager as a Cloud Service, il cliente deve gestire, gestire e integrare nel processo di distribuzione di Adobe Experience Manager as a Cloud Service.

Come accennato in precedenza, la chiamata all’API distribuisce le nuove variabili e i nuovi valori negli ambienti Cloud, in modo simile a una tipica pipeline di distribuzione del codice del cliente. I servizi di authoring e pubblicazione vengono riavviati e fanno riferimento ai nuovi valori, in genere dopo alcuni minuti. I gate e i test di qualità eseguiti da Cloud Manager durante una distribuzione regolare del codice non vengono eseguiti durante questo processo.

In genere, i clienti chiamano l’API per impostare le variabili di ambiente prima di distribuire il codice che si basa su di esse in Cloud Manager. In alcune situazioni, potrebbe essere utile modificare una variabile esistente dopo la distribuzione del codice.

>[!NOTE]
>
>L’API potrebbe non riuscire quando una pipeline è in uso, o con un aggiornamento AEM o con la distribuzione da parte del cliente, a seconda della parte della pipeline end-to-end che viene eseguita in quel momento. La risposta di errore indica che la richiesta non è stata eseguita correttamente, anche se non ne indica il motivo specifico.

In alcuni casi, la distribuzione pianificata del codice del cliente si basa su variabili esistenti per l’immissione di nuovi valori, il che non sarebbe appropriato per il codice corrente. Se questo è un problema, si raccomanda di apportare modifiche variabili in modo additivo. Per farlo, crea nuovi nomi di variabili invece di modificare solo il valore delle variabili precedenti in modo che il codice precedente non faccia mai riferimento al nuovo valore. Quindi, quando la nuova versione del cliente appare stabile, è possibile scegliere di rimuovere i valori precedenti.

Analogamente, poiché i valori di una variabile non sono sottoposti a controllo delle versioni, un rollback del codice potrebbe causarne il riferimento a valori più recenti che causano problemi. Anche la strategia sulle variabili aggiuntive menzionata in precedenza può essere d&#39;aiuto in questo contesto.

Questa strategia aggiuntiva per le variabili è utile anche per gli scenari di disaster recovery in cui se il codice di diversi giorni prima deve essere ridistribuito, i nomi e i valori delle variabili a cui fa riferimento rimarranno intatti. Questo si basa su una strategia in cui un cliente attende alcuni giorni prima di rimuovere tali variabili meno recenti, altrimenti il codice precedente non avrebbe variabili appropriate a cui fare riferimento.
