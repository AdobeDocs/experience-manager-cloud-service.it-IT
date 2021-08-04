---
title: Configurazione di OSGi per Adobe Experience Manager as a Cloud Service
description: 'Configurazione OSGi con valori segreti e valori specifici per l’ambiente '
feature: Distribuzione
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: 2555e5e1545f198a235d44f8cb07e25d7490d1d5
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 0%

---

# Configurazione di OSGi per Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[](https://www.osgi.org/) OSGiè un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e le sue configurazioni.

OSGi fornisce le primitive standardizzate che consentono di costruire applicazioni da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un’applicazione e distribuiti. Questo consente una facile gestione dei bundle OSGi in quanto possono essere arrestati, installati, avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi è contenuto in uno dei vari bundle. Per ulteriori informazioni, consulta la [specifica OSGi](https://www.osgi.org/Specifications/HomePage).

Puoi gestire le impostazioni di configurazione per i componenti OSGi tramite file di configurazione che fanno parte di un progetto di codice AEM.

## File di configurazione OSGi {#osgi-configuration-files}

Le modifiche alla configurazione sono definite nei pacchetti di codice del progetto AEM (`ui.apps`) come file di configurazione (`.cfg.json`) in cartelle di configurazione specifiche della modalità di esecuzione:

`/apps/example/config.<runmode>`

Il formato dei file di configurazione OSGi è basato su JSON utilizzando il formato `.cfg.json` definito dal progetto Apache Sling.

Le configurazioni OSGi sono destinate ai componenti OSGi tramite la loro identità persistente (PID), che per impostazione predefinita corrisponde al nome della classe Java™ del componente OSGi. Ad esempio, per fornire la configurazione OSGi per un servizio OSGi implementato da:

`com.example.workflow.impl.ApprovalWorkflow.java`

un file di configurazione OSGi è definito in:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

seguendo il formato di configurazione cfg.json OSGi .

>[!NOTE]
>
>Versioni precedenti di file di configurazione OSGi supportati utilizzando formati di file diversi come .cfg., .config e come definizioni di risorse XML sling:OsgiConfig. Questi formati vengono sostituiti dal formato di configurazione cfg.json OSGi.

## Risoluzione in modalità di esecuzione {#runmode-resolution}

Configurazioni OSGi specifiche possono essere indirizzate a istanze AEM specifiche utilizzando le modalità di esecuzione. Per utilizzare la modalità runmode, crea le cartelle di configurazione in `/apps/example` (dove esempio è il nome del progetto), nel formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Tutte le configurazioni OSGi in tali cartelle vengono utilizzate se le modalità di esecuzione definite nel nome della cartella di configurazione corrispondono alle modalità di esecuzione utilizzate da AEM.

Ad esempio, se AEM utilizza le modalità di esecuzione author e dev, vengono applicati i nodi di configurazione in `/apps/example/config.author/` e `/apps/example/config.author.dev/`, mentre i nodi di configurazione in `/apps/example/config.publish/` e `/apps/example/config.author.stage/` non vengono applicati.

Se sono applicabili più configurazioni per lo stesso PID, viene applicata la configurazione con il numero più alto di modalità di esecuzione corrispondenti.

La granularità di questa regola è a livello di PID. Ciò significa che non è possibile definire alcune proprietà per lo stesso PID in `/apps/example/config.author/` e altre specifiche in `/apps/example/config.author.dev/` per lo stesso PID. La configurazione con il maggior numero di modalità di esecuzione corrispondenti sarà efficace per l&#39;intero PID.

>[!NOTE]
>
>Una cartella di configurazione `config.preview` OSGI **non può** essere dichiarata nello stesso modo in cui una cartella `config.publish` può essere dichiarata. Al contrario, il livello di anteprima eredita la propria configurazione OSGI dai valori del livello di pubblicazione.

Quando si sviluppa localmente, è possibile trasmettere un parametro di avvio in modalità runmode per determinare quale configurazione OSGI in modalità runmode viene utilizzata.

## Tipi di valori di configurazione OSGi {#types-of-osgi-configuration-values}

Esistono tre varietà di valori di configurazione OSGi che possono essere utilizzati con Adobe Experience Manager as a Cloud Service.

1. **Valori** in linea, che sono valori hardcoded nella configurazione OSGi e memorizzati in Git. Esempio:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valori** segreti, ovvero valori che non devono essere memorizzati in Git per motivi di sicurezza. Esempio:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Valori** specifici per l’ambiente, ovvero valori che variano da un ambiente di sviluppo all’altro e che pertanto non possono essere oggetto di targeting accurato in modalità di esecuzione (poiché in Adobe Experience Manager as a Cloud Service è presente una sola modalità  `dev` di esecuzione). Esempio:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Tieni presente che un singolo file di configurazione OSGi può utilizzare qualsiasi combinazione di questi tipi di valori di configurazione in combinazione. Esempio:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Come scegliere il tipo di valore di configurazione OSGi appropriato {#how-to-choose-the-appropriate-osgi-configuration-value-type}

Il caso comune per OSGi utilizza valori di configurazione OSGi in linea. Le configurazioni specifiche per l’ambiente vengono utilizzate solo per casi d’uso specifici in cui un valore differisce tra gli ambienti di sviluppo.

![](assets/choose-configuration-value-type_res1.png)

Le configurazioni specifiche per l’ambiente estendono le configurazioni OSGi tradizionali e definite statisticamente che contengono valori in linea, consentendo di gestire i valori di configurazione OSGi esternamente tramite l’API di Cloud Manager. È importante capire quando utilizzare l’approccio comune e tradizionale di definire i valori in linea e memorizzarli in Git, anziché astrarre i valori in configurazioni specifiche per l’ambiente.

Le seguenti linee guida riguardano quando utilizzare configurazioni non segrete e specifiche per l’ambiente:

### Quando utilizzare i valori di configurazione in linea {#when-to-use-inline-configuration-values}

I valori delle configurazioni in linea sono considerati l’approccio standard e devono essere utilizzati quando possibile. Le configurazioni in linea forniscono i vantaggi di:

* Vengono mantenuti, con governance e cronologia delle versioni in Git
* I valori sono implicitamente associati alle distribuzioni del codice
* Non richiedono ulteriori considerazioni sulla distribuzione o sul coordinamento

Quando definisci un valore di configurazione OSGi, inizia con i valori in linea e seleziona solo le configurazioni segrete o specifiche per l’ambiente, se necessario per il caso d’uso.

### Quando utilizzare valori di configurazione specifici dell’ambiente non segreti {#when-to-use-non-secret-environment-specific-configuration-values}

Utilizza solo configurazioni specifiche per l’ambiente (`$[env:ENV_VAR_NAME]`) per valori di configurazione non segreti quando i valori variano per il livello di anteprima o variano in ambienti di sviluppo. Ciò include le istanze di sviluppo locali e qualsiasi ambiente di sviluppo Adobe Experience Manager as a Cloud Service. A parte l’impostazione di valori univoci per il livello di anteprima, evita di utilizzare configurazioni non segrete specifiche per l’ambiente per Adobe Experience Manager as a Cloud Service Stage o gli ambienti di produzione.

* Utilizza solo configurazioni non segrete specifiche per l’ambiente per i valori di configurazione che differiscono tra il livello di pubblicazione e di anteprima o per i valori che differiscono tra gli ambienti di sviluppo, incluse le istanze di sviluppo locali.
* Oltre allo scenario in cui il livello di anteprima deve variare dal livello di pubblicazione, utilizza i valori inline standard nelle configurazioni OSGi per i valori non segreti Stage e Produzione. In relazione, si sconsiglia di utilizzare configurazioni specifiche per l&#39;ambiente per facilitare l&#39;esecuzione di modifiche di configurazione in fase di runtime agli ambienti di stage e produzione; queste modifiche devono essere introdotte tramite la gestione del codice sorgente.

### Quando utilizzare valori di configurazione specifici dell’ambiente segreto {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service richiede l&#39;uso di configurazioni specifiche per l&#39;ambiente (`$[secret:SECRET_VAR_NAME]`) per qualsiasi valore di configurazione OSGi segreto, come password, chiavi API private o qualsiasi altro valore che non può essere memorizzato in Git per motivi di sicurezza.

Utilizza configurazioni specifiche per l’ambiente segreto per memorizzare il valore per i segreti su tutti gli ambienti Adobe Experience Manager as a Cloud Service, inclusi Stage e Produzione.

## Creazione di configurazioni OSGi {#creating-sogi-configurations}

Esistono due modi per creare configurazioni OSGi, come descritto di seguito. L’approccio precedente viene generalmente utilizzato per configurare componenti OSGi personalizzati che hanno proprietà e valori OSGi ben noti dallo sviluppatore e quest’ultimo per i componenti OSGi forniti da AEM.

### Scrittura delle configurazioni OSGi {#writing-osgi-configurations}

I file di configurazione OSGi formattati JSON possono essere scritti manualmente direttamente nel progetto AEM. Questo è spesso il modo più rapido per creare configurazioni OSGi per componenti OSGi ben noti, e in particolare per componenti OSGi personalizzati che sono stati progettati e sviluppati dallo stesso sviluppatore che definisce le configurazioni. Questo approccio può anche essere utilizzato per copiare/incollare e aggiornare le configurazioni per lo stesso componente OSGi in varie cartelle in modalità runmode.

1. Nell’IDE, apri il progetto `ui.apps`, individua o crea la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue le modalità di esecuzione necessarie per eseguire la nuova configurazione OSGi
1. In questa cartella di configurazione, crea un nuovo file `<PID>.cfg.json`. Il PID è l’identità persistente del componente OSGi di solito è il nome completo della classe dell’implementazione del componente OSGi. Esempio:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
I nomi dei file di fabbrica della configurazione OSGi utilizzano la convenzione di  `<PID>-<factory-name>.cfg.json` denominazione
1. Apri il nuovo file `.cfg.json` e definisci le combinazioni chiave/valore per le coppie di proprietà e valori OSGi, seguendo il [formato di configurazione OSGi JSON](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Salva le modifiche apportate al nuovo file `.cfg.json`
1. Aggiungi e esegui il commit del nuovo file di configurazione OSGi su Git

### Generazione di configurazioni OSGi tramite l’SDK Quickstart AEM {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

La console Web AEM di Jar dell’SDK AEM Quickstart può essere utilizzata per configurare i componenti OSGi ed esportare le configurazioni OSGi come JSON. Questo è utile per configurare componenti OSGi forniti da AEM le cui proprietà OSGi e i relativi formati di valore potrebbero non essere ben compresi dallo sviluppatore che definisce le configurazioni OSGi nel progetto AEM.

>[!NOTE]
>
>L&#39;interfaccia utente di configurazione della console Web AEM scrive `.cfg.json` file nell&#39;archivio. Tieni presente questo aspetto per evitare potenziali comportamenti inaspettati durante lo sviluppo locale, quando le configurazioni OSGi AEM definite dal progetto possono differire dalle configurazioni generate.

1. Accedi alla console Web AEM di Jar dell&#39;SDK AEM Quickstart come utente amministratore
1. Passa a OSGi > Configurazione
1. Per configurare, individua il componente OSGi e tocca il relativo titolo da modificare
   ![Configurazione OSGi](./assets/configuring-osgi/configuration.png)
1. Modifica i valori delle proprietà di configurazione OSGi tramite l’interfaccia utente Web in base alle esigenze
1. Registra il PID (Persistent Identity) in un luogo sicuro. Viene utilizzato in seguito per generare la configurazione OSGi JSON
1. Tocca Salva
1. Passa a OSGi > Stampante di configurazione del programma di installazione OSGi
1. Incolla nel PID copiato al passaggio 5, assicurati che il formato di serializzazione sia impostato su &quot;OSGi Configurator JSON&quot;
1. Tocca Stampa
1. La configurazione OSGi in formato JSON verrà visualizzata nella sezione Proprietà di configurazione serializzate .
   ![Stampante di configurazione del programma di installazione OSGi](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. Nell’IDE, apri il progetto `ui.apps`, individua o crea la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue le modalità di esecuzione necessarie per la nuova configurazione OSGi.
1. In questa cartella di configurazione, crea un nuovo file `<PID>.cfg.json`. Il PID è lo stesso valore del passaggio 5.
1. Incolla le proprietà di configurazione serializzata dal passaggio 10 nel file `.cfg.json` .
1. Salva le modifiche apportate al nuovo file `.cfg.json`.
1. Aggiungi e conferma il tuo nuovo file di configurazione OSGi a Git.


## Formati delle proprietà di configurazione OSGi {#osgi-configuration-property-formats}

### Valori in linea {#inline-values}

I valori in linea vengono formattati come coppie nome-valore standard, seguendo la sintassi JSON standard. Esempio:

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### Valori di configurazione specifici per l’ambiente {#environment-specific-configuration-values}

La configurazione OSGi deve assegnare un segnaposto per la variabile che deve essere definita per ambiente:

```
use $[env:ENV_VAR_NAME]
```

I clienti devono utilizzare questa tecnica solo per le proprietà di configurazione OSGI correlate al loro codice personalizzato; non deve essere utilizzato per sostituire la configurazione OSGI definita da Adobe.

>[!NOTE]
>
>I segnaposto non possono essere utilizzati in [istruzioni di reindirizzamento](/help/implementing/deploying/overview.md#repoinit).

### Valori di configurazione segreti {#secret-configuration-values}

La configurazione OSGi deve assegnare un segnaposto per il segreto che deve essere definito per ambiente:

```
use $[secret:SECRET_VAR_NAME]
```

### Denominazione delle variabili {#variable-naming}

Quanto segue si applica sia ai valori di configurazione specifici dell’ambiente che a quelli segreti.

I nomi delle variabili devono seguire le regole seguenti:

* Lunghezza minima: 2
* Lunghezza massima: 100
* Deve corrispondere a regex: `[a-zA-Z_][a-zA-Z_0-9]*`

I valori per le variabili non devono superare i 2048 caratteri.

>[!NOTE]
>
>I nomi delle variabili con prefisso `INTERNAL_` sono riservati per Adobe. Tutte le variabili del set di clienti che iniziano con questo prefisso verranno ignorate. I clienti non devono fare riferimento a queste variabili.

### Valori predefiniti {#default-values}

Quanto segue si applica sia ai valori di configurazione specifici dell’ambiente che a quelli segreti.

Se non viene impostato alcun valore per ambiente, in fase di runtime il segnaposto non viene sostituito e viene lasciato in posizione poiché non si è verificata alcuna interpolazione. Per evitare questo problema, è possibile fornire un valore predefinito come parte del segnaposto con la seguente sintassi:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Se viene fornito un valore predefinito, il segnaposto viene sostituito con il valore per ambiente, se fornito, o con il valore predefinito fornito.

### Sviluppo locale {#local-development}

Quanto segue si applica sia ai valori di configurazione specifici dell’ambiente che a quelli segreti.

Le variabili possono essere definite nell’ambiente locale in modo che vengano raccolte dall’AEM locale in fase di runtime. Ad esempio, su Linux®:

```bash
export ENV_VAR_NAME=my_value
```

Si consiglia di scrivere un semplice script bash che imposti le variabili di ambiente utilizzate nelle configurazioni ed eseguirle prima di avviare AEM. Strumenti come [https://direnv.net/](https://direnv.net/) aiutano a semplificare questo approccio. A seconda del tipo di valori, possono essere sottoposti a Check-In nella gestione del codice sorgente, se possono essere condivisi tra tutti.

I valori per i segreti vengono letti dai file. Pertanto, per ogni segnaposto che utilizza un segreto, deve essere creato un file di testo contenente il valore segreto.

Ad esempio, se si utilizza `$[secret:server_password]`, è necessario creare un file di testo denominato **server_password**. Tutti questi file segreti devono essere memorizzati nella stessa directory e la proprietà del framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` deve essere configurata con tale directory locale.

### Configurazione autore e pubblicazione {#author-vs-publish-configuration}

Se una proprietà OSGI richiede valori diversi per l&#39;autore rispetto alla pubblicazione:

* È necessario utilizzare cartelle separate `config.author` e `config.publish` OSGi, come descritto nella sezione [Risoluzione in modalità di esecuzione](#runmode-resolution).
* Esistono due opzioni per creare nomi di variabili indipendenti che devono essere utilizzati:
   * la prima opzione, consigliata: in tutte le cartelle OSGI (come `config.author` e `config.publish`) dichiarate per definire valori diversi, utilizza lo stesso nome di variabile. Esempio
      `$[env:ENV_VAR_NAME;default=<value>]`, dove il valore predefinito corrisponde al valore predefinito per quel livello (authoring o pubblicazione). Quando imposti la variabile di ambiente tramite [API di Cloud Manager](#cloud-manager-api-format-for-setting-properties) o tramite un client, distingue tra i livelli utilizzando il parametro &quot;service&quot; come descritto in questa [documentazione di riferimento API](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables). Il parametro &quot;service&quot; associa il valore della variabile al livello OSGI appropriato. Può essere &quot;autore&quot; o &quot;pubblicazione&quot; o &quot;anteprima&quot;.
   * la seconda opzione, ovvero dichiarare variabili distinte utilizzando un prefisso come `author_<samevariablename>` e `publish_<samevariablename>`

### Esempi di configurazione {#configuration-examples}

Negli esempi seguenti, si supponga che siano presenti tre ambienti di sviluppo, oltre agli ambienti stage e prod.

**Esempio 1**

L’intento è che il valore della proprietà OSGI `my_var1` sia lo stesso per stage e prod, ma differisca per ciascuno dei tre ambienti di sviluppo.

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
{ 
 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**Esempio 2**

L&#39;intento è che il valore della proprietà OSGI `my_var1` differisca per stage, prod e per ciascuno dei tre ambienti di sviluppo. Pertanto, è necessario chiamare l’API di Cloud Manager per impostare il valore per `my_var1` per ogni env di sviluppo.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1": "val2",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**Esempio 3**

L’intento è che il valore della proprietà OSGi `my_var1` sia lo stesso per gli ambienti di stage, produzione e solo per uno degli ambienti di sviluppo, ma sia diverso per gli altri due ambienti di sviluppo. In questo caso, è necessario chiamare l’API di Cloud Manager per impostare il valore di `my_var1` per ciascuno degli ambienti di sviluppo, anche per l’ambiente di sviluppo che deve avere lo stesso valore di stage e produzione. Non erediterà il valore impostato nella cartella **config**.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

Un altro modo per farlo sarebbe quello di impostare un valore predefinito per il token di sostituzione nella cartella config.dev in modo che sia lo stesso valore della cartella **config**.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1;default=val1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

## Formato API di Cloud Manager per l’impostazione delle proprietà {#cloud-manager-api-format-for-setting-properties}

Consulta [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) su come configurare l&#39;API.
>[!NOTE]
>
>Assicurati che l’API di Cloud Manager utilizzata abbia assegnato il ruolo &quot;Deployment Manager - Cloud Service&quot;. Altri ruoli non sono in grado di eseguire tutti i comandi sottostanti.

### Impostazione dei valori tramite API {#setting-values-via-api}

Una chiamata all&#39;API distribuisce le nuove variabili e i nuovi valori in un ambiente Cloud, simile a una tipica pipeline di distribuzione del codice cliente. I servizi di authoring e pubblicazione verranno riavviati e faranno riferimento ai nuovi valori, in genere impiegando alcuni minuti.

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
>Le variabili predefinite non sono impostate tramite API, ma nella proprietà OSGi stessa.
>
>Per ulteriori informazioni, consulta [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) .

### Ottenimento dei valori tramite API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Per ulteriori informazioni, consulta [questa pagina](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) .

### Eliminazione di valori tramite API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Per eliminare una variabile, includerla con un valore vuoto.

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

### Eliminazione dei valori tramite la riga di comando {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Per ulteriori informazioni su come configurare i valori utilizzando il plug-in Cloud Manager per Adobe I/O CLI, consulta [questa pagina](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) .

### Numero di variabili {#number-of-variables}

È possibile dichiarare fino a 200 variabili per ambiente.

## Considerazioni sulla distribuzione per valori di configurazione segreti e specifici per l’ambiente {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Poiché i valori di configurazione segreti e specifici per l’ambiente sono al di fuori di Git e, di conseguenza, non fanno parte dei meccanismi formali di implementazione di Adobe Experience Manager as a Cloud Service, il cliente deve gestire, governare e integrare in Adobe Experience Manager come processo di distribuzione di Cloud Service.

Come accennato in precedenza, la chiamata dell’API distribuisce le nuove variabili e i nuovi valori agli ambienti Cloud, in modo simile a una tipica pipeline di distribuzione del codice cliente. I servizi di authoring e pubblicazione verranno riavviati e faranno riferimento ai nuovi valori, in genere impiegando alcuni minuti. Tieni presente che i gate e i test di qualità eseguiti da Cloud Manager durante una distribuzione regolare del codice non vengono eseguiti durante questo processo.

In genere, i clienti chiamano l’API per impostare le variabili di ambiente prima di distribuire il codice che si basa su di esse in Cloud Manager. In alcune situazioni, potrebbe essere utile modificare una variabile esistente dopo che il codice è già stato distribuito.

>[!NOTE]
>
>L’API potrebbe non riuscire quando è in uso una pipeline, un aggiornamento AEM o un’implementazione cliente, a seconda della parte della pipeline da fine a fine che viene eseguita in quel momento. La risposta di errore indicherà che la richiesta non è riuscita, anche se non indicherà il motivo specifico.

In alcuni casi, la distribuzione del codice cliente pianificato si basa su variabili esistenti per disporre di nuovi valori, il che non sarebbe appropriato per il codice corrente. Se si tratta di un problema, si raccomanda di apportare modifiche variabili in modo additivo. A questo scopo, crea nuovi nomi di variabili invece di semplicemente modificare il valore di vecchie variabili, il cui codice così vecchio non fa mai riferimento al nuovo valore. Quindi, quando il nuovo rilascio del cliente appare stabile, si può scegliere di rimuovere i valori precedenti.

Allo stesso modo, poiché ai valori di una variabile non viene applicata una versione, un rollback del codice potrebbe causare un riferimento a valori più recenti che causano problemi. Anche in questo caso sarebbe utile la strategia per la variabile additiva precedentemente menzionata.

Questa strategia di variabile additiva è utile anche per gli scenari di disaster recovery in cui, se si desidera ridistribuire il codice da diversi giorni, i nomi e i valori delle variabili a cui fa riferimento rimarranno intatti. Questo si basa su una strategia in cui un cliente attende alcuni giorni prima di rimuovere le variabili meno recenti, altrimenti il codice meno recente non disporrebbe di variabili appropriate a cui fare riferimento.
