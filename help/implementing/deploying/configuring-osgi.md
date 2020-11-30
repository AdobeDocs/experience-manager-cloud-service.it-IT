---
title: Configurazione di OSGi per AEM as a Cloud Service
description: 'Configurazione OSGi con valori segreti e valori specifici per l’ambiente '
translation-type: tm+mt
source-git-commit: 0a2d44a63c3d26460c0836ab6b28989a0aad72da
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 1%

---


# Configurazione di OSGi per AEM as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e le sue configurazioni.

OSGi fornisce le primitive standardizzate che consentono di creare applicazioni da componenti di piccole dimensioni, riutilizzabili e collaborativi. Questi componenti possono essere composti in un’applicazione e distribuiti. Questo consente di gestire facilmente i bundle OSGi quando possono essere arrestati, installati e avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ciascun componente OSGi è contenuto in uno dei vari bundle. Per ulteriori informazioni, consultate la specifica [](https://www.osgi.org/Specifications/HomePage)OSGi.

Potete gestire le impostazioni di configurazione per i componenti OSGi tramite file di configurazione che fanno parte di un progetto di codice AEM.

## File di configurazione OSGi {#osgi-configuration-files}

Le modifiche alla configurazione sono definite nei pacchetti di codice del progetto AEM (`ui.apps`) come file di configurazione (`.cfg.json`) in cartelle di configurazione specifiche della modalità di esecuzione:

`/apps/example/config.<runmode>`

Il formato dei file di configurazione OSGi è basato su JSON utilizzando il `.cfg.json` formato definito dal progetto Apache Sling.

Le configurazioni OSGi sono destinate ai componenti OSGi tramite il relativo PID (Persistent Idenity), che per impostazione predefinita corrisponde al nome della classe Java del componente OSGi. Ad esempio, per fornire la configurazione OSGi per un servizio OSGi implementato da:

`com.example.workflow.impl.ApprovalWorkflow.java`

un file di configurazione OSGi è definito in:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

seguendo il formato di configurazione cfg.json OSGi.

>[!NOTE]
>
>Versioni precedenti di AEM file di configurazione OSGi supportati utilizzando formati di file diversi come .cfg., .config e come definizioni di risorse sling:OsgiConfig XML. Questi formati vengono sostituiti dal formato di configurazione cfg.json OSGi.

## Risoluzione in modalità di esecuzione {#runmode-resolution}

Configurazioni OSGi specifiche possono essere indirizzate a istanze AEM specifiche utilizzando le modalità di esecuzione. Per utilizzare la modalità di esecuzione, create le cartelle di configurazione in `/apps/example` (dove ad esempio è il nome del progetto), nel formato seguente:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Eventuali configurazioni OSGi in tali cartelle saranno utilizzate se le modalità di esecuzione definite nel nome della cartella di configurazione corrispondono alle modalità di esecuzione utilizzate da AEM.

Ad esempio, se AEM utilizza le modalità di esecuzione, i nodi di configurazione in `/apps/example/config.author/` e `/apps/example/config.author.dev/` verranno applicati, mentre i nodi di configurazione in `/apps/example/config.publish/` e `/apps/example/config.author.stage/` non saranno applicati.

Se si applicano più configurazioni per lo stesso PID, viene applicata la configurazione con il numero più elevato di modalità di esecuzione corrispondenti.

La granularità di questa regola è a livello PID. Ciò significa che non è possibile definire alcune proprietà per lo stesso PID in `/apps/example/config.author/` e più specifiche in `/apps/example/config.author.dev/` per lo stesso PID.  La configurazione con il maggior numero di modalità di esecuzione corrispondenti sarà efficace per l&#39;intero PID.

Quando si sviluppa localmente, è possibile passare un parametro di avvio in modalità di esecuzione per stabilire quale configurazione OSGI in modalità di esecuzione verrà utilizzata.

## Tipi di valori di configurazione OSGi {#types-of-osgi-configuration-values}

Esistono tre varietà di valori di configurazione OSGi che possono essere utilizzati con AEM come Cloud Service.

1. **Valori** in linea, ossia valori hardcoded nella configurazione OSGi e memorizzati in Git. Esempio:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valori** segreti, che sono valori che non devono essere memorizzati in Git per motivi di sicurezza. Esempio:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **I valori** specifici dell&#39;ambiente, che sono valori che variano da un ambiente di sviluppo all&#39;altro, e quindi non possono essere mirati in modo accurato dalla modalità di esecuzione (poiché esiste un&#39;unica `dev` modalità di esecuzione in AEM come Cloud Service). Esempio:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Tenere presente che un singolo file di configurazione OSGi può utilizzare insieme qualsiasi combinazione di questi tipi di valori di configurazione. Esempio:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Come scegliere il tipo di valore di configurazione OSGi appropriato {#how-to-choose-the-appropriate-osgi-configuration-value-type}

Il caso comune per OSGi utilizza valori di configurazione OSGi in linea. Le configurazioni specifiche per l&#39;ambiente sono utilizzate solo per casi d&#39;uso specifici in cui un valore varia in base agli ambienti di sviluppo.

![](assets/choose-configuration-value-type_res1.png)

Le configurazioni specifiche per l’ambiente estendono le configurazioni OSGi tradizionali e statiche che contengono valori in linea, consentendo di gestire i valori di configurazione OSGi esternamente tramite l’API di Cloud Manager. È importante capire quando utilizzare l&#39;approccio comune e tradizionale di definire i valori in linea e memorizzarli in Git, anziché astrarre i valori in configurazioni specifiche per l&#39;ambiente.

Le seguenti linee guida riguardano i casi in cui utilizzare configurazioni non segrete e specifiche dell&#39;ambiente segreto:

### Quando utilizzare i valori di configurazione in linea {#when-to-use-inline-configuration-values}

I valori delle configurazioni in linea sono considerati l&#39;approccio standard e devono essere utilizzati quando possibile. Le configurazioni in linea offrono i seguenti vantaggi:

* Sono mantenuti, con governance e storia della versione in Git
* I valori sono implicitamente legati alle distribuzioni del codice
* Non richiedono ulteriori considerazioni di implementazione o di coordinamento

Quando definite un valore di configurazione OSGi, iniziate con i valori in linea, tutte le configurazioni specifiche per il segreto o l&#39;ambiente selezionate solo se necessarie per il caso d&#39;uso.

### Quando utilizzare valori di configurazione non segreti per l&#39;ambiente {#when-to-use-non-secret-environment-specific-configuration-values}

Utilizzate configurazioni specifiche dell&#39;ambiente (`$[env:ENV_VAR_NAME]`) solo per i valori di configurazione non segreti quando i valori variano in base agli ambienti di sviluppo. Ciò include le istanze di sviluppo locale e qualsiasi AEM come ambienti di sviluppo Cloud Service. Evitare di utilizzare configurazioni non segrete specifiche per l&#39;ambiente per AEM come ambienti di fase o produzione Cloud Service.

* Utilizzate solo configurazioni non segrete specifiche per l&#39;ambiente per i valori di configurazione che differiscono tra gli ambienti di sviluppo, incluse le istanze di sviluppo locale.
* Utilizzate invece i valori inline standard nelle configurazioni OSGi per i valori non segreti di Stage e Produzione.  A tale proposito, non è consigliabile utilizzare configurazioni specifiche per l&#39;ambiente per facilitare l&#39;esecuzione delle modifiche di configurazione in fase di esecuzione agli ambienti di fase e produzione; queste modifiche dovrebbero essere introdotte tramite la gestione del codice sorgente.

### Quando utilizzare i valori di configurazione specifici dell&#39;ambiente segreto {#when-to-use-secret-environment-specific-configuration-values}

AEM come Cloud Service richiede l’uso di configurazioni specifiche dell’ambiente (`$[secret:SECRET_VAR_NAME]`) per qualsiasi valore di configurazione OSGi segreto, come password, chiavi API private o qualsiasi altro valore che non può essere memorizzato in Git per motivi di sicurezza.

Utilizzate configurazioni specifiche per l&#39;ambiente segreto per memorizzare il valore per i segreti su tutte le AEM come ambienti di Cloud Service, inclusi Stage e Produzione.

<!-- ### Adding a New Configuration to the Repository {#adding-a-new-configuration-to-the-repository}

#### What You Need to Know {#what-you-need-to-know}

To add a new configuration to the repository you need to know the following:

1. The **Persistent Identity** (PID) of the service.

   Reference the **Configurations** field in the Web console. The name is shown in brackets after the bundle name (or in the **Configuration Information** towards the bottom of the page).

   For example, create a node `com.day.cq.wcm.core.impl.VersionManagerImpl.` to configure **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Whether a specific runmode is required. Create the folder:

    * `config` - for all run modes
    * `config.author` - for the author environment
    * `config.publish` - for the publish environment
    * `config.<run-mode>` - as appropriate

1. Whether a **Configuration** or **Factory Configuration** is necessary.
1. The individual parameters to be configured; including any existing parameter definitions that will need to be recreated.

   Reference the individual parameter field in the Web console. The name is shown in brackets for each parameter.

   For example, create a property
   `versionmanager.createVersionOnActivation` to configure **Create Version on Activation**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Does a configuration already exist in `/libs`? To list all configurations in your instance, use the **Query** tool in CRXDE Lite to submit the following SQL query:

   `select * from sling:OsgiConfig`

   If so, this configuration can be copied to ` /apps/<yourProject>/`, then customized in the new location. -->

## Creazione di configurazioni OSGi

Esistono due modi per creare nuove configurazioni OSGi, come descritto di seguito. Il primo approccio è in genere utilizzato per configurare componenti OSGi personalizzati con proprietà e valori OSGi ben noti dallo sviluppatore, e il secondo per i componenti OSGi AEM forniti.

### Scrittura di configurazioni OSGi

I file di configurazione OSGi formattati JSON possono essere scritti manualmente direttamente nel progetto AEM. Questo è spesso il modo più veloce per creare configurazioni OSGi per componenti OSGi noti, e in particolare componenti OSGi personalizzati che sono stati progettati e sviluppati dallo stesso sviluppatore che definisce le configurazioni. Questo approccio può essere utilizzato anche per copiare/incollare e aggiornare le configurazioni per lo stesso componente OSGi in diverse cartelle in modalità di esecuzione.

1. Nell’IDE, apri il `ui.apps` progetto, individua o crea la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue le modalità di esecuzione della nuova configurazione OSGi
1. In questa cartella di configurazione, create un nuovo `<PID>.cfg.json` file. Il PID è l’Identità persistente del componente OSGi, in genere è il nome completo della classe dell’implementazione del componente OSGi. Esempio:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
Tenete presente che i nomi dei file factory di configurazione OSGi utilizzano la convenzione di `<PID>-<factory-name>.cfg.json` denominazione
1. Aprite il nuovo `.cfg.json` file e definite le combinazioni chiave/valore per le coppie di proprietà e valori OSGi, seguendo il formato [di configurazione](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)JSON OSGi.
1. Salvare le modifiche apportate al nuovo `.cfg.json` file
1. Aggiungete e inviate il nuovo file di configurazione OSGi a Git

### Generazione di configurazioni OSGi tramite l’SDK AEM Quickstart

La console AEM Web AEM SDK Quickstart Jar può essere utilizzata per configurare componenti OSGi ed esportare configurazioni OSGi come JSON. Questo è utile per configurare componenti OSGi forniti AEM le cui proprietà OSGi e i relativi formati di valore potrebbero non essere ben compresi dallo sviluppatore che definisce le configurazioni OSGi nel progetto AEM. Tenere presente che utilizzando l&#39;interfaccia utente Configurazione della console Web AEM è possibile scrivere `.cfg.json` i file nell&#39;archivio, per evitare possibili comportamenti imprevisti durante lo sviluppo locale, quando le configurazioni OSGi definite AEM progetto possono essere diverse dalle configurazioni generate.

1. Accedi alla console Web AEM Jar dell&#39;SDK AEM come utente amministratore
1. Passa a OSGi > Configurazione
1. Individuate il componente OSGi da configurare e toccate il titolo per modificarlo
   ![Configurazione OSGi](./assets/configuring-osgi/configuration.png)
1. Modificare i valori delle proprietà di configurazione OSGi tramite l&#39;interfaccia utente Web in base alle esigenze
1. Registra l’identità persistente (PID) in un luogo sicuro, verrà utilizzato in seguito per generare il JSON di configurazione OSGi
1. Tocca Salva
1. Passare a OSGi > Stampante di configurazione OSGi Installer
1. Incolla nel PID copiato al passaggio 5, verifica che il formato di serializzazione sia impostato su &quot;OSGi Configurator JSON&quot;
1. Toccate Stampa,
1. La configurazione OSGi in formato JSON verrà visualizzata nella sezione Proprietà di configurazione serializzate
   ![Stampante di configurazione OSGi](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. Nell’IDE, aprite il `ui.apps` progetto, individuate o create la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue le modalità di esecuzione a cui deve essere applicata la nuova configurazione OSGi.
1. In questa cartella di configurazione, create un nuovo `<PID>.cfg.json` file. Il PID è lo stesso valore del Passaggio 5.
1. Incollate le proprietà di configurazione serializzata dal passaggio 10 al `.cfg.json` file.
1. Salvare le modifiche apportate al nuovo `.cfg.json` file.
1. Aggiungete e inviate il nuovo file di configurazione OSGi a Git.


## Formati delle proprietà di configurazione OSGi

### Valori in linea {#inline-values}

Come ci si può aspettare, i valori in linea sono formattati come coppie nome-valore standard, seguendo la sintassi JSON standard. Esempio:

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### Valori di configurazione specifici per l&#39;ambiente {#environment-specific-configuration-values}

Nella configurazione OSGi deve essere assegnato un segnaposto per la variabile che deve essere definita per ambiente:

```
use $[env:ENV_VAR_NAME]
```

I clienti devono utilizzare questa tecnica solo per le proprietà di configurazione OSGI relative al loro codice personalizzato; non deve essere utilizzato per ignorare  configurazione OSGI definita dal Adobe.

### Valori di configurazione segreti {#secret-configuration-values}

Nella configurazione OSGi deve essere assegnato un segnaposto per il segreto che deve essere definito in base all’ambiente:

```
use $[secret:SECRET_VAR_NAME]
```

### Denominazione delle variabili {#variable-naming}

Quanto segue si applica sia ai valori di configurazione specifici dell&#39;ambiente che ai valori segreti.

I nomi delle variabili devono seguire le regole seguenti:

* lunghezza minima: 2
* lunghezza massima: 100
* deve corrispondere a regex: `[a-zA-Z_][a-zA-Z_0-9]*`

I valori per le variabili non devono superare i 2048 caratteri.

### Valori predefiniti {#default-values}

Quanto segue si applica sia ai valori di configurazione specifici dell&#39;ambiente che ai valori segreti.

Se non viene impostato alcun valore per ambiente, in fase di esecuzione il segnaposto non verrà sostituito e lasciato in posizione poiché non è stata eseguita l&#39;interpolazione. Per evitare questo problema, è possibile fornire un valore predefinito all&#39;interno del segnaposto con la sintassi seguente:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Se viene fornito un valore predefinito, il segnaposto verrà sostituito con il valore per ambiente specificato oppure con il valore predefinito fornito.

### Sviluppo locale {#local-development}

Quanto segue si applica sia ai valori di configurazione specifici dell&#39;ambiente che ai valori segreti.

Le variabili possono essere definite nell&#39;ambiente locale in modo che vengano rilevate dal AEM locale in fase di esecuzione. Ad esempio, in Linux:

```bash
export ENV_VAR_NAME=my_value
```

Si consiglia di scrivere uno script di base semplice che imposti le variabili di ambiente utilizzate nelle configurazioni ed esegua tale script prima di avviare AEM. Strumenti come [https://direnv.net/](https://direnv.net/) semplificano questo approccio. A seconda del tipo di valori, possono essere sottoposti a check-in nella gestione del codice sorgente, se possono essere condivisi tra tutti.

I valori per i segreti vengono letti dai file. Pertanto, per ogni segnaposto che utilizza un segreto è necessario creare un file di testo contenente il valore segreto.

Ad esempio, se `$[secret:server_password]` viene utilizzato, è necessario creare un file di testo denominato **server_password** . Tutti questi file segreti devono essere memorizzati nella stessa directory e la proprietà framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` deve essere configurata con quella directory locale.

### Configurazione autore e pubblicazione {#author-vs-publish-configuration}

Se una proprietà OSGI richiede valori diversi per autore e pubblicazione:

* utilizzare cartelle separate `config.author` e `config.publish` OSGi, come descritto nella sezione Risoluzione [in modalità di esecuzione](#runmode-resolution).
* è necessario utilizzare nomi di variabili indipendenti. Si consiglia di utilizzare un prefisso, ad esempio `author_<variablename>` e `publish_<variablename>` dove i nomi delle variabili sono identici

### Esempi di configurazione {#configuration-examples}

Negli esempi riportati di seguito, si supponga che siano presenti 3 ambienti di sviluppo, oltre agli ambienti stage e prod.

**Esempio 1**

L&#39;intento è che il valore della proprietà OSGI sia lo stesso per stage e prod, ma differisca `my_var1` per ciascuno degli ambienti di sviluppo 3.

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
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Esempio 2**

L&#39;intento è che il valore della proprietà OSGI `my_var1` differisca per lo stage, il prod e per ciascuno degli ambienti di sviluppo 3. Pertanto, l&#39;API di Cloud Manager dovrà essere chiamata per impostare il valore per `my_var1` ogni env di dev.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Esempio 3**

L&#39;intento è che il valore della proprietà OSGi `my_var1` sia lo stesso per il palco, la produzione, e solo uno degli ambienti di sviluppo, ma che sia diverso per gli altri due ambienti di sviluppo. In questo caso, l&#39;API di Cloud Manager dovrà essere chiamata per impostare il valore di `my_var1` per ciascuno degli ambienti di sviluppo, anche per l&#39;ambiente di sviluppo che dovrebbe avere lo stesso valore di fase e produzione. Non erediterà il valore impostato nella **configurazione** della cartella.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

Un altro modo per farlo sarebbe impostare un valore predefinito per il token di sostituzione nella cartella config.dev in modo che sia lo stesso valore della cartella **config** .

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

## Formato API di Cloud Manager per l&#39;impostazione delle proprietà {#cloud-manager-api-format-for-setting-properties}

Consultate [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) sulla configurazione dell&#39;API.
>[!NOTE]
>
>Verifica che l&#39;API di Cloud Manager utilizzata abbia assegnato il ruolo &quot;Gestione distribuzione - Cloud Service&quot;. Altri ruoli non sono in grado di eseguire tutti i comandi sottostanti.

### Impostazione dei valori tramite API {#setting-values-via-api}

La chiamata dell&#39;API implementerà le nuove variabili e i nuovi valori in un ambiente Cloud, simile a una tipica pipeline di distribuzione del codice cliente. I servizi di creazione e pubblicazione verranno riavviati e faranno riferimento ai nuovi valori, in genere impiegando alcuni minuti.

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

Le variabili predefinite non sono impostate tramite API, ma nella proprietà OSGi stessa.

Per ulteriori informazioni, consulta [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) .

### Ottenimento di valori tramite API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Per ulteriori informazioni, consulta [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) .

### Eliminazione di valori tramite API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Per eliminare una variabile, includetela con un valore vuoto.

Per ulteriori informazioni, consulta [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) .

### Ottenimento dei valori tramite la riga di comando {#getting-values-via-cli}

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

### Eliminazione di valori tramite la riga di comando {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Consulta [questa pagina](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) per ulteriori informazioni su come configurare i valori tramite il plug-in Cloud Manager per  CLI di Adobe I/O.

### Numero di variabili {#number-of-variables}

È possibile dichiarare fino a 200 variabili per ambiente.

## Considerazioni sulla distribuzione per i valori di configurazione specifici per l&#39;ambiente e il segreto {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Poiché i valori di configurazione segreti e specifici dell&#39;ambiente non rientrano in Git e, pertanto, non fanno parte del AEM formale come meccanismi di implementazione del Cloud Service, il cliente deve gestire, governare e integrare nel AEM come processo di implementazione del Cloud Service.

Come già detto, chiamando l&#39;API i nuovi valori e variabili verranno distribuiti negli ambienti Cloud, in modo simile a un tipico pipeline di distribuzione del codice cliente. I servizi di creazione e pubblicazione verranno riavviati e faranno riferimento ai nuovi valori, in genere impiegando alcuni minuti. I cancelli di qualità e i test eseguiti da Cloud Manager durante una distribuzione regolare del codice non vengono eseguiti durante questo processo.

In genere, i clienti richiamano l&#39;API per impostare le variabili di ambiente prima di distribuire il codice che si basa su di esse in Cloud Manager. In alcuni casi, è possibile modificare una variabile esistente dopo che il codice è già stato distribuito.

L&#39;API potrebbe non riuscire quando è in uso una pipeline, un aggiornamento AEM o una distribuzione cliente, a seconda di quale parte della pipeline end-to-end viene eseguita in quel momento. La risposta di errore indica che la richiesta non è riuscita, anche se non indicherà il motivo specifico.

Potrebbero verificarsi situazioni in cui una distribuzione programmata del codice cliente si basa su variabili esistenti per avere nuovi valori, il che non sarebbe appropriato per il codice corrente. Se questo è un problema, si consiglia di apportare modifiche variabili in modo additivo. A tal fine, create nuovi nomi di variabili invece di modificare semplicemente il valore di vecchie variabili in modo che il codice non faccia mai riferimento al nuovo valore. Quindi, quando il nuovo rilascio del cliente appare stabile, è possibile scegliere di rimuovere i valori precedenti.

Analogamente, poiché i valori di una variabile non dispongono di una versione, un rollback del codice potrebbe fare riferimento a valori più recenti che causano problemi. Anche in questo caso la suddetta strategia di variabile additiva sarebbe d&#39;aiuto.

Questa strategia di variabile additiva è utile anche per gli scenari di disaster recovery in cui, se si desidera ridistribuire il codice da diversi giorni, i nomi e i valori delle variabili a cui fa riferimento rimarranno intatti. Questo si basa su una strategia in cui il cliente attende alcuni giorni prima di rimuovere le vecchie variabili, altrimenti il codice meno recente non avrebbe variabili appropriate a cui fare riferimento.
