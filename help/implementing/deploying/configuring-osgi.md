---
title: Configurazione di OSGi per Adobe Experience Manager as a Cloud Service
description: Configurazione OSGi con valori segreti e valori specifici per l’ambiente
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: 26ca2addb14f62588035323ce886ae890919b759
workflow-type: tm+mt
source-wordcount: '3312'
ht-degree: 1%

---

# Configurazione di OSGi per Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

>[!NOTE]
>
>AEM ha introdotto la possibilità di utilizzare l’interfaccia utente di Cloud Manager per configurare le variabili di ambiente standard con la versione 2021.12.0. Per ulteriori informazioni, consulta la documentazione [qui](/help/implementing/cloud-manager/environment-variables.md).

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e le sue configurazioni.

OSGi fornisce le primitive standardizzate che consentono di costruire applicazioni da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un’applicazione e distribuiti. Questo consente una facile gestione dei bundle OSGi in quanto possono essere arrestati, installati, avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi è contenuto in uno dei vari bundle. Per ulteriori informazioni, consulta la sezione [Specifiche OSGi](https://help.eclipse.org/latest/index.jsp).

Puoi gestire le impostazioni di configurazione per i componenti OSGi tramite file di configurazione che fanno parte di un progetto di codice AEM.

## File di configurazione OSGi {#osgi-configuration-files}

Le modifiche di configurazione sono definite nei pacchetti di codice del progetto AEM (`ui.apps`) come file di configurazione (`.cfg.json`) in cartelle di configurazione specifiche della modalità di esecuzione:

`/apps/example/config.<runmode>`

Il formato dei file di configurazione OSGi è basato su JSON utilizzando `.cfg.json` definito dal progetto Apache Sling.

Le configurazioni OSGi sono destinate ai componenti OSGi tramite la loro identità persistente (PID), che per impostazione predefinita corrisponde al nome della classe Java™ del componente OSGi. Ad esempio, per fornire la configurazione OSGi per un servizio OSGi implementato da:

`com.example.workflow.impl.ApprovalWorkflow.java`

un file di configurazione OSGi è definito in:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

che segue `cfg.json` Formato di configurazione OSGi.

>[!NOTE]
>
>Versioni precedenti di file di configurazione OSGi supportati utilizzando formati di file diversi, come `.cfg`, `.config` e come XML `sling:OsgiConfig` definizioni delle risorse. Questi formati vengono sostituiti dal `.cfg.json` Formato di configurazione OSGi.

## Risoluzione in modalità di esecuzione {#runmode-resolution}

>[!TIP]
>
>AEM 6.x supporta le modalità di esecuzione personalizzate, tuttavia AEM as a Cloud Service no. AEM supporto as a Cloud Service e [set esatto di modalità di esecuzione](./overview.md#runmodes). Qualsiasi variazione nelle configurazioni OSGi tra AEM ambienti as a Cloud Service deve essere gestita utilizzando [Variabili dell&#39;ambiente di configurazione OSGi](#environment-specific-configuration-values).

Configurazioni OSGi specifiche possono essere indirizzate a istanze AEM specifiche utilizzando le modalità di esecuzione. Per utilizzare la modalità runmode, creare le cartelle di configurazione in `/apps/example` (dove esempio è il nome del progetto), nel formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Tutte le configurazioni OSGi in tali cartelle vengono utilizzate se le modalità di esecuzione definite nel nome della cartella di configurazione corrispondono alle modalità di esecuzione utilizzate da AEM.

Ad esempio, se AEM utilizza le modalità di esecuzione author e dev, i nodi di configurazione in `/apps/example/config.author/` e `/apps/example/config.author.dev/` vengono applicati, mentre i nodi di configurazione in `/apps/example/config.publish/` e `/apps/example/config.author.stage/` non sono applicati.

Se sono applicabili più configurazioni per lo stesso PID, viene applicata la configurazione con il numero più alto di modalità di esecuzione corrispondenti.

La granularità di questa regola è a livello di PID. Ciò significa che non è possibile definire alcune proprietà per lo stesso PID in `/apps/example/config.author/` e più specifiche in `/apps/example/config.author.dev/` per lo stesso PID. La configurazione con il maggior numero di modalità di esecuzione corrispondenti sarà efficace per l&#39;intero PID.

>[!NOTE]
>
>A `config.preview` Cartella di configurazione OSGi **impossibile** devono essere dichiarati allo stesso modo `config.publish` può essere dichiarata cartella. Al contrario, il livello di anteprima eredita la propria configurazione OSGi dai valori del livello di pubblicazione.

Quando si sviluppa localmente, un parametro di avvio in modalità di esecuzione, `-r`, viene utilizzato per specificare la configurazione OSGI in modalità di esecuzione.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### Verifica delle modalità di esecuzione

AEM modalità di esecuzione as a Cloud Service sono ben definite in base al tipo di ambiente e al servizio. Consulta la sezione [elenco completo delle modalità di esecuzione AEM as a Cloud Service disponibili](./overview.md#runmodes).

I valori di configurazione OSGi specificati dalla modalità runmode possono essere verificati da:

1. Apertura dell’ambiente AEM as a Cloud Services [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it)
1. Selezione dei livelli di servizio da ispezionare, utilizzando __Pod__ menu a discesa
1. Selezione della __Stato__ scheda
1. Selezione __Configurazioni__ dal __Immagine stato__ menu a discesa
1. Selezione della __Ottieni stato__ pulsante

La visualizzazione risultante visualizza tutte le configurazioni dei componenti OSGi per i livelli selezionati con i relativi valori di configurazione OSGi applicabili. Questi valori possono essere incrociati con i valori di configurazione OSGi nel codice sorgente del progetto AEM in `/apps/example/osgiconfig/config.<runmode(s)>`.


Per verificare che siano applicati i valori di configurazione OSGi appropriati:

1. Nell’output Configurazione della Console per sviluppatori
1. Individua il `pid` rappresentare la configurazione OSGi da verificare; questo è il nome del file di configurazione OSGi nel codice sorgente del progetto AEM.
1. Inspect `properties` elenco per `pid` e verifica che la chiave e i valori corrispondano al file di configurazione OSGi nel codice sorgente del progetto AEM per la modalità runmode da verificare.=


## Tipi di valori di configurazione OSGi {#types-of-osgi-configuration-values}

Ci sono tre varietà di valori di configurazione OSGi che possono essere utilizzati con Adobe Experience Manager as a Cloud Service.

1. **Valori in linea**, che sono valori hardcoded nella configurazione OSGi e memorizzati in Git. Esempio:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valori segreti**, valori che non devono essere memorizzati in Git per motivi di sicurezza. Esempio:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Valori specifici per l’ambiente**, valori che variano da un ambiente di sviluppo all&#39;altro e che pertanto non possono essere oggetto di targeting accurato in modalità di esecuzione (poiché è presente un solo `dev` in modalità runmode in Adobe Experience Manager as a Cloud Service). Esempio:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Un singolo file di configurazione OSGi può utilizzare qualsiasi combinazione di questi tipi di valori di configurazione in combinazione. Esempio:

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

Utilizza solo configurazioni specifiche per l’ambiente (`$[env:ENV_VAR_NAME]`) per i valori di configurazione non segreti quando i valori variano per il livello di anteprima o variano tra gli ambienti di sviluppo. Questo include le istanze di sviluppo locali e tutti gli ambienti di sviluppo Adobe Experience Manager as a Cloud Service. A parte l’impostazione di valori univoci per il livello di anteprima, evita di utilizzare configurazioni non segrete specifiche per l’ambiente per gli ambienti Adobe Experience Manager as a Cloud Service Stage o Production.

* Utilizza solo configurazioni non segrete specifiche per l’ambiente per i valori di configurazione che differiscono tra il livello di pubblicazione e di anteprima o per i valori che differiscono tra gli ambienti di sviluppo, incluse le istanze di sviluppo locali.
* Oltre allo scenario in cui il livello di anteprima deve variare dal livello di pubblicazione, utilizza i valori inline standard nelle configurazioni OSGi per i valori non segreti Stage e Produzione. In relazione, si sconsiglia di utilizzare configurazioni specifiche per l&#39;ambiente per facilitare l&#39;esecuzione di modifiche di configurazione in fase di runtime agli ambienti di stage e produzione; queste modifiche devono essere introdotte tramite la gestione del codice sorgente.

### Quando utilizzare valori di configurazione specifici dell’ambiente segreto {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service richiede l’utilizzo di configurazioni specifiche per l’ambiente (`$[secret:SECRET_VAR_NAME]`) per qualsiasi valore di configurazione OSGi segreto, ad esempio password, chiavi API private o qualsiasi altro valore che non può essere memorizzato in Git per motivi di sicurezza.

Utilizza configurazioni specifiche per l’ambiente segreto per memorizzare il valore per i segreti su tutti gli ambienti Adobe Experience Manager as a Cloud Service, inclusi Stage e Produzione.

## Creazione di configurazioni OSGi {#creating-osgi-configurations}

Esistono due modi per creare configurazioni OSGi, come descritto di seguito. L’approccio precedente viene generalmente utilizzato per configurare componenti OSGi personalizzati che hanno proprietà e valori OSGi ben noti dallo sviluppatore e quest’ultimo per i componenti OSGi forniti da AEM.

### Scrittura delle configurazioni OSGi {#writing-osgi-configurations}

I file di configurazione OSGi formattati JSON possono essere scritti manualmente direttamente nel progetto AEM. Questo è spesso il modo più rapido per creare configurazioni OSGi per componenti OSGi ben noti, e in particolare per componenti OSGi personalizzati che sono stati progettati e sviluppati dallo stesso sviluppatore che definisce le configurazioni. Questo approccio può anche essere utilizzato per copiare/incollare e aggiornare le configurazioni per lo stesso componente OSGi in varie cartelle in modalità runmode.

1. Nell’IDE, apri la `ui.apps` , individua o crea la cartella di configurazione (`/apps/.../config.<runmode>`) che esegue il targeting delle modalità di esecuzione della nuova configurazione OSGi
1. In questa cartella di configurazione, crea un `<PID>.cfg.json` file. Il PID è l’identità persistente del componente OSGi. In genere è il nome della classe completa dell’implementazione del componente OSGi. Esempio:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
I nomi dei file di fabbrica della configurazione OSGi utilizzano il `<factoryPID>-<name>.cfg.json` convenzione di denominazione
1. Apri il nuovo `.cfg.json` e definire le combinazioni chiave/valore per le coppie di proprietà e valori OSGi, seguendo la [Formato di configurazione JSON OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Salva le modifiche apportate al nuovo `.cfg.json` file
1. Aggiungi e esegui il commit del nuovo file di configurazione OSGi su Git

### Generazione di configurazioni OSGi tramite l’SDK Quickstart AEM {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

La console Web AEM di Jar dell’SDK AEM Quickstart può essere utilizzata per configurare i componenti OSGi ed esportare le configurazioni OSGi come JSON. Questo è utile per configurare componenti OSGi forniti da AEM le cui proprietà OSGi e i relativi formati di valore potrebbero non essere ben compresi dallo sviluppatore che definisce le configurazioni OSGi nel progetto AEM.

>[!NOTE]
>
>L’interfaccia utente di configurazione della console Web AEM scrive `.cfg.json` file nel repository. Tieni presente questo aspetto per evitare potenziali comportamenti inaspettati durante lo sviluppo locale, quando le configurazioni OSGi AEM definite dal progetto possono differire dalle configurazioni generate.

1. Accedi alla console Web AEM di Jar dell&#39;SDK AEM Quickstart all&#39;indirizzo `https://<host>:<port>/system/console` come utente amministratore
1. Passa a **OSGi** > **Configurazione**
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
1. Nell’IDE, apri la `ui.apps` , individua o crea la cartella di configurazione (`/apps/.../config.<runmode>`), che esegue il targeting delle modalità di esecuzione necessarie per la nuova configurazione OSGi.
1. In questa cartella di configurazione, crea un `<PID>.cfg.json` file. Il PID è lo stesso valore del passaggio 5.
1. Incolla le proprietà di configurazione serializzata dal passaggio 10 nel `.cfg.json` file.
1. Salva le modifiche apportate al nuovo `.cfg.json` file.
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

I clienti devono utilizzare questa tecnica solo per le proprietà di configurazione OSGi correlate al loro codice personalizzato; non deve essere utilizzato per sostituire la configurazione OSGi definita da Adobe.

>[!NOTE]
>
>I segnaposto non possono essere utilizzati in [dichiarazioni repoinit](/help/implementing/deploying/overview.md#repoinit).

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

>[!CAUTION]
>
>Esistono regole relative all&#39;utilizzo di alcuni prefissi per i nomi delle variabili:
>
>1. Nomi di variabile con prefisso `INTERNAL_`, `ADOBE_`oppure `CONST_` sono riservati dall&#39;Adobe. Tutte le variabili impostate dal cliente che iniziano con questi prefissi verranno ignorate.
>
>1. I clienti non devono fare riferimento a variabili con prefisso `INTERNAL_` o `ADOBE_` o.
>
>1. Variabili di ambiente con il prefisso `AEM_` sono definiti dal prodotto come API pubblica da utilizzare e impostare dai clienti.
   >   Mentre i clienti possono utilizzare e impostare le variabili di ambiente che iniziano con il prefisso . `AEM_` non devono definire le proprie variabili con questo prefisso.


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

Si consiglia di scrivere un semplice script bash che imposti le variabili di ambiente utilizzate nelle configurazioni ed eseguirle prima di avviare AEM. Strumenti simili [https://direnv.net/](https://direnv.net/) contribuire a semplificare questo approccio. A seconda del tipo di valori, possono essere sottoposti a Check-In nella gestione del codice sorgente, se possono essere condivisi tra tutti.

I valori per i segreti vengono letti dai file. Pertanto, per ogni segnaposto che utilizza un segreto, deve essere creato un file di testo contenente il valore segreto.

Ad esempio se `$[secret:server_password]` viene utilizzato un file di testo denominato **server_password** deve essere creato. Tutti questi file segreti devono essere archiviati nella stessa directory e nella proprietà framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` deve essere configurato con quella directory locale.

>[!CAUTION]
>
>Estensioni file non consentite per il file di testo.
>
>Pertanto, per l’esempio precedente, il file di testo deve essere denominato **server_password** - senza estensione di file.

La `org.apache.felix.configadmin.plugin.interpolation.secretsdir` è una proprietà del framework Sling; quindi questa proprietà non è impostata nella console felix (/system/console), ma è impostata nel file sling.properties che viene utilizzato all&#39;avvio del sistema. Questo file si trova nella directory secondaria /conf della cartella Jar/install estratta (crx-quickstart/conf).

esempio: aggiungi questa riga alla fine del file &quot;crx-quickstart/conf/sling.properties&quot; per configurare &#39;crx-quickstart/secretsdir&#39; come cartella segreta:

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### Configurazione autore e pubblicazione {#author-vs-publish-configuration}

Se una proprietà OSGi richiede valori diversi per autore e pubblicazione:

* Separato `config.author` e `config.publish` Le cartelle OSGi devono essere utilizzate, come descritto in [Sezione Risoluzione in modalità di esecuzione](#runmode-resolution).
* Esistono due opzioni per creare nomi di variabili indipendenti che devono essere utilizzati:
   * la prima opzione, consigliata: in tutte le cartelle OSGi (come `config.author` e `config.publish`) dichiarata per definire valori diversi, usa lo stesso nome di variabile. Per esempio
      `$[env:ENV_VAR_NAME;default=<value>]`, dove il valore predefinito corrisponde al valore predefinito per quel livello (authoring o pubblicazione). Quando si imposta la variabile di ambiente tramite [API di Cloud Manager](#cloud-manager-api-format-for-setting-properties) o tramite un client, distinguere tra i livelli utilizzando il parametro &quot;service&quot; come descritto in questo [Documentazione di riferimento API](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/). Il parametro &quot;service&quot; associa il valore della variabile al livello OSGi appropriato. Può essere &quot;autore&quot; o &quot;pubblicazione&quot; o &quot;anteprima&quot;.
   * la seconda opzione, ovvero dichiarare variabili distinte utilizzando un prefisso come `author_<samevariablename>` e `publish_<samevariablename>`

### Esempi di configurazione {#configuration-examples}

Negli esempi seguenti, si supponga che siano presenti tre ambienti di sviluppo, oltre agli ambienti stage e prod.

**Esempio 1**

L&#39;intento è il valore della proprietà OSGi `my_var1` essere lo stesso per stage e prod, ma differire per ciascuno dei tre ambienti di sviluppo.

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

L&#39;intento è il valore della proprietà OSGi `my_var1` per diversi ambienti di stage, prod e per ciascuno dei tre ambienti di sviluppo. È pertanto necessario chiamare l’API di Cloud Manager per impostare il valore per `my_var1` per ogni dev env.

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

L&#39;intento è il valore della proprietà OSGi `my_var1` essere lo stesso per gli ambienti stage, produzione e solo per uno degli ambienti di sviluppo, ma differire per gli altri due ambienti di sviluppo. In questo caso, l’API di Cloud Manager deve essere chiamata per impostare il valore di `my_var1` per ciascuno degli ambienti di sviluppo, anche per l’ambiente di sviluppo che deve avere lo stesso valore di stage e produzione. Non erediterà il valore impostato nella cartella **config**.

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

Un altro modo per farlo sarebbe quello di impostare un valore predefinito per il token di sostituzione nella cartella config.dev in modo che sia lo stesso valore di nel **config** cartella.

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

Vedi [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) informazioni sulla configurazione dell’API.
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
>Vedi [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) per ulteriori informazioni.

### Ottenimento dei valori tramite API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Vedi [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) per ulteriori informazioni.

### Eliminazione di valori tramite API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Per eliminare una variabile, includerla con un valore vuoto.

Vedi [questa pagina](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) per ulteriori informazioni.

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
>Vedi [questa pagina](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) per ulteriori informazioni su come configurare i valori utilizzando il plug-in Cloud Manager, ad Adobe I/O CLI.

### Numero di variabili {#number-of-variables}

È possibile dichiarare fino a 200 variabili per ambiente.

## Considerazioni sulla distribuzione per valori di configurazione segreti e specifici per l’ambiente {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Poiché i valori di configurazione segreti e specifici per l’ambiente non rientrano in Git e non fanno quindi parte dei meccanismi formali di implementazione di Adobe Experience Manager as a Cloud Service, il cliente deve gestire, gestire e integrare nel processo di distribuzione di Adobe Experience Manager as a Cloud Service.

Come accennato in precedenza, la chiamata dell’API distribuisce le nuove variabili e i nuovi valori agli ambienti Cloud, in modo simile a una tipica pipeline di distribuzione del codice cliente. I servizi di authoring e pubblicazione verranno riavviati e faranno riferimento ai nuovi valori, in genere impiegando alcuni minuti. Tieni presente che i gate e i test di qualità eseguiti da Cloud Manager durante una distribuzione regolare del codice non vengono eseguiti durante questo processo.

In genere, i clienti chiamano l’API per impostare le variabili di ambiente prima di distribuire il codice che si basa su di esse in Cloud Manager. In alcune situazioni, potrebbe essere utile modificare una variabile esistente dopo che il codice è già stato distribuito.

>[!NOTE]
>
>L’API potrebbe non riuscire quando è in uso una pipeline, un aggiornamento AEM o un’implementazione cliente, a seconda della parte della pipeline da fine a fine che viene eseguita in quel momento. La risposta di errore indicherà che la richiesta non è riuscita, anche se non indicherà il motivo specifico.

In alcuni casi, la distribuzione del codice cliente pianificato si basa su variabili esistenti per disporre di nuovi valori, il che non sarebbe appropriato per il codice corrente. Se si tratta di un problema, si raccomanda di apportare modifiche variabili in modo additivo. A questo scopo, crea nuovi nomi di variabili invece di semplicemente modificare il valore di vecchie variabili, il cui codice così vecchio non fa mai riferimento al nuovo valore. Quindi, quando il nuovo rilascio del cliente appare stabile, si può scegliere di rimuovere i valori precedenti.

Allo stesso modo, poiché ai valori di una variabile non viene applicata una versione, un rollback del codice potrebbe causare un riferimento a valori più recenti che causano problemi. Anche in questo caso sarebbe utile la strategia per la variabile additiva precedentemente menzionata.

Questa strategia di variabile additiva è utile anche per gli scenari di disaster recovery in cui, se si desidera ridistribuire il codice da diversi giorni, i nomi e i valori delle variabili a cui fa riferimento rimarranno intatti. Questo si basa su una strategia in cui un cliente attende alcuni giorni prima di rimuovere le variabili meno recenti, altrimenti il codice meno recente non disporrebbe di variabili appropriate a cui fare riferimento.
