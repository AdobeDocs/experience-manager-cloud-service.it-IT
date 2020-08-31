---
title: Modelli di pagina
description: I modelli di pagina vengono utilizzati per creare una pagina che verrà utilizzata come base per la nuova pagina
translation-type: tm+mt
source-git-commit: 0508311b997789ada07856a73d29e38d1b735979
workflow-type: tm+mt
source-wordcount: '3244'
ht-degree: 8%

---


# Modelli di pagina {#page-templates}

Per creare una pagina è necessario selezionare un modello. Il modello di pagina viene utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina risultante, eventuali contenuti iniziali e i componenti che possono essere utilizzati (proprietà di progettazione). Ciò presenta numerosi vantaggi:

* I modelli di pagina consentono agli autori specializzati di [creare e modificare i modelli](/help/sites-cloud/authoring/features/templates.md).
   * Tali autori specializzati sono denominati autori di **modelli**
   * Gli autori dei modelli devono essere membri del `template-authors` gruppo.
* I modelli di pagina mantengono una connessione dinamica a tutte le pagine da essi create. In questo modo tutte le modifiche apportate al modello verranno applicate alle pagine stesse.
* I modelli di pagina rendono il componente pagina più generico, in modo che possa essere utilizzato senza personalizzazione.

Con Modelli pagina, i pezzi che creano una pagina sono isolati all’interno dei componenti. È possibile configurare le combinazioni di componenti necessarie in un’interfaccia utente, eliminando così la necessità di sviluppare un nuovo componente di pagina per ogni variazione di pagina.

Questo documento:

* Fornisce una panoramica sulla creazione di un modello di pagina
* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili
* Descrive come AEM valuta la disponibilità di un modello

>[!NOTE]
>
>Questo documento presuppone che si abbia già familiarità con la creazione e la modifica di modelli. Consultate il documento di authoring [Creazione di modelli](/help/sites-cloud/authoring/features/templates.md)di pagina, che descrive in dettaglio le capacità dei modelli modificabili come esposti all’autore del modello.

>[!TIP]
>
>[L&#39;esercitazione](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND approfondisce l&#39;uso dei modelli di pagina mediante l&#39;implementazione di un esempio ed è molto utile per comprendere come impostare un modello in un nuovo progetto

## Creating a New Template {#creating-a-new-template}

La creazione di modelli di pagina viene realizzata principalmente con la console [modelli e l’editor](/help/sites-cloud/authoring/features/templates.md) modelli da un autore di modelli. Questa sezione fornisce una panoramica di questo processo e una descrizione di quanto avviene a livello tecnico.

Durante la creazione di un nuovo modello modificabile:

1. Create una [cartella per i modelli](#template-folders). Questa operazione non è obbligatoria, ma è consigliata.
1. Selezionate un tipo [di](#template-type)modello. Viene copiata per creare la definizione [del](#template-definitions)modello.

   >[!NOTE]
   >
   >Sono disponibili una selezione di tipi di modelli out-of-the-box. Potete anche [creare modelli](#creating-template-types) personalizzati per il sito, se necessario.

1. Configurate la struttura, i criteri di contenuto, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati su una pagina risultante, né eliminati da alcuna pagina risultante.
   * Se desideri che gli autori delle pagine siano in grado di aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate sulla modalità in cui un autore del modello definisce la struttura, consultate [Creazione di modelli](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)di pagina.

   Per i dettagli tecnici della struttura, vedere [Struttura](#structure) in questo documento.

   **Criteri**

   * I criteri di contenuto definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minime e massime.
   * Questi sono applicabili al modello (e alle pagine create con tale modello).

   Per informazioni dettagliate sulla definizione dei criteri da parte dell&#39;autore di un modello, consultate [Creazione di modelli](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)di pagina.

   Per informazioni tecniche sulle politiche, consultate [Criteri](#content-policies) di contenuto in questo documento.

   **Contenuto iniziale**

   * Contenuto iniziale definisce il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può essere modificato dagli autori della pagina.

   Per informazioni dettagliate sulla modalità in cui un autore del modello definisce la struttura, consultate [Creazione di modelli](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)di pagina.

   Per informazioni tecniche sui contenuti iniziali, consultate Contenuto [](#initial-content) iniziale in questo documento.

   **Layout**

   * È possibile definire il layout del modello per una serie di dispositivi.
   * Il Layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate sulla modalità in cui un autore del modello definisce il layout del modello, consultate [Creazione di modelli](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author)di pagina.

   Per informazioni tecniche sul layout del modello, consultate [Layout](#layout) in questo documento.

1. Attivate il modello, quindi consentitelo per specifiche strutture ad albero del contenuto.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile per gli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate sull’abilitazione di un modello da parte dell’autore di un modello, consultate [Creazione di modelli](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)di pagina.

   Per informazioni tecniche sull&#39;abilitazione di un modello, consultate Abilitazione e [abilitazione di un modello per l&#39;](#enabling-and-allowing-a-template-for-use)utilizzo in questo documento

1. Utilizzatelo per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una nuova pagina, non vi è alcuna differenza visibile e nessuna indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate sull’utilizzo dei modelli da parte dell’autore di una pagina per creare una pagina, consultate [Creazione e organizzazione di pagine](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, consultate Pagine [di contenuti](#resultant-content-pages) risultanti in questo documento.

>[!NOTE]
>
>La libreria client dell&#39;editor presuppone la presenza dello `cq.shared` spazio dei nomi nelle pagine di contenuto, e se è assente, `Uncaught TypeError: Cannot read property 'shared' of undefined` si verificherà l&#39;errore JavaScript.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di esse viene incluso automaticamente `cq.shared`. Tuttavia, se decidete di creare da zero pagine di contenuto personalizzate senza basarle su contenuti di esempio, dovete includere lo `cq.shared` spazio nomi.

<!--See [Using Client-Side Libraries](/help/sites-developing/clientlibs.md) for further information.-->

>[!CAUTION]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello.

## Cartelle modello {#template-folders}

Per organizzare i modelli potete utilizzare le cartelle seguenti:

* `global`
* Specifico per il sito

>[!NOTE]
>
>Anche se potete nidificare le cartelle, quando l’utente le visualizza nella console **Modelli** vengono presentate come una struttura semplice.

In a standard AEM instance the `global` folder already exists in the template console. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. Potete aggiungere i modelli predefiniti a questa cartella o creare una nuova cartella (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una nuova cartella in cui memorizzare i modelli personalizzati e non utilizzare la `global` cartella.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con `admin` diritti.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente
1. Elemento padre/i della cartella corrente
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se una configurazione si sovrappone ( `path`/ `label`), all&#39;utente viene presentata solo l&#39;istanza più vicina alla cartella corrente.

Per creare una nuova cartella, potete effettuare le seguenti operazioni:

* Programmaticamente o con CRXDE Lite
* Utilizzo del browser di configurazione

## Utilizzo di CRXDE Lite {#using-crxde-lite}

1. È possibile creare una nuova cartella (in /conf) per l’istanza a livello di programmazione o con CRXDE Lite.

   Deve essere utilizzata la seguente struttura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. È quindi possibile definire le seguenti proprietà sul nodo principale della cartella:

   `<your-folder-name> [sling:Folder]`

   * Nome: `jcr:title`
   * Tipo: `String`
   * Valore: Titolo (per la cartella) che desiderate visualizzare nella console **Modelli** .

1. Oltre alle autorizzazioni e ai privilegi di authoring standard (ad esempio `content-authors`) è ora necessario assegnare i gruppi e definire i diritti di accesso (ACL, Access Rights) necessari agli autori per poter creare i modelli nella nuova cartella.

   Il `template-authors` gruppo è il gruppo predefinito che deve essere assegnato. Per informazioni dettagliate, vedere la sezione [ACL e gruppi](#acls-and-groups) .

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Utilizzo del browser di configurazione {#using-the-configuration-browser}

1. Andate a Navigazione **** globale > **Strumenti** > **Browser** di configurazione.

   Le cartelle esistenti sono elencate a sinistra, inclusa la `global` cartella.

1. Fai clic su **Crea**.
1. Nella finestra di dialogo **Crea configurazione** è necessario configurare i seguenti campi:

   * **Titolo**: Fornire un titolo per la cartella di configurazione
   * **Modelli** modificabili: Fare clic per consentire la modifica dei modelli all&#39;interno di questa cartella

1. Fai clic su **Crea**

>[!NOTE]
>
>Nel browser di configurazione, potete modificare la cartella globale e attivare l’opzione Modelli **** modificabili se desiderate creare dei modelli all’interno di questa cartella, ma questa non è la procedura consigliata.

### ACL e gruppi {#acls-and-groups}

Una volta create le cartelle dei modelli (tramite CRXDE o con il browser di configurazione), gli ACL devono essere definiti per i gruppi appropriati per le cartelle dei modelli per garantire la protezione adeguata.

Le cartelle dei modelli per l’esercitazione [](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND possono essere utilizzate come esempio.

#### Il gruppo di autori dei modelli {#the-template-authors-group}

Il `template-authors` gruppo è il gruppo utilizzato per gestire l&#39;accesso ai modelli ed è dotato di AEM standard, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>Il `template-authors` gruppo è destinato solo agli utenti che devono essere in grado di creare nuovi modelli.
>
>La modifica dei modelli è molto efficace e, se non viene eseguita correttamente, i modelli esistenti possono essere interrotti. Questo ruolo dovrebbe pertanto essere mirato e includere solo utenti qualificati.

Nella tabella seguente sono elencate le autorizzazioni necessarie per la modifica dei modelli.

<table>
 <tbody>
  <tr>
   <th>Percorso</th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni <br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autori modello<br /> </td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> del sito specifico</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>read</td>
   <td>Utente Web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori contenuto</td>
   <td>replica</td>
   <td>Gli autori di replicheContent devono attivare i modelli di una pagina durante l’attivazione di una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> del sito specifico</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>read</td>
   <td>Utente Web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori contenuto</td>
   <td>replica</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i criteri di un modello di pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autore del modello</td>
   <td>read</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti.</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

Questo `template-authors` gruppo predefinito copre solo le impostazioni di progetto, dove tutti `template-authors` i membri possono accedere e creare tutti i modelli. Per le impostazioni più complesse, in cui sono necessari gruppi di autori di modelli multipli per l&#39;accesso separato ai modelli, è necessario creare un numero maggiore di gruppi di autori di modelli personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori dei modelli rimarrebbero invariate.

## Template Type {#template-type}

Quando create un nuovo modello, dovete specificare un tipo di modello:

* I tipi di modello forniscono efficacemente i modelli per un modello. Quando create un nuovo modello, la struttura e il contenuto iniziale del tipo di modello selezionato vengono usati per creare il nuovo modello.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta eseguita la copia, l&#39;unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Il tipo di risorsa del componente pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell&#39;editor modelli.
   * È consigliabile definire i punti di interruzione per la griglia reattiva e l&#39;impostazione dell&#39;emulatore mobile sul tipo di modello. Questo è facoltativo, perché la configurazione può essere definita anche sul singolo modello (consultate la sezione Tipo di [modello e Gruppi](#p-template-type-and-mobile-device-groups-br-p)di dispositivi mobili).

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina HTML5 e Pagina modulo adattiva.

   * Altri esempi sono forniti nell’ambito dell’esercitazione [WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* I tipi di modelli sono generalmente definiti dagli sviluppatori.

I tipi di modelli forniti vengono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non è necessario modificare nulla nel `/libs` percorso. Questo perché il contenuto di `/libs` può essere sovrascritto in qualsiasi momento da un aggiornamento a AEM.

I tipi di modello specifici per il sito devono essere memorizzati nella posizione comparabile di:

* `/apps/settings/wcm/template-types`

Le definizioni per i tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (consigliato) o in alternativa in `global`. Esempio:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>I tipi di modello devono rispettare la struttura corretta delle cartelle (ovvero `/settings/wcm/...`), in caso contrario i tipi di modello non verranno trovati.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### Creazione di tipi di modelli {#creating-template-types}

Se avete creato un modello che può fungere da base per altri modelli, potete copiare il modello come tipo di modello.

1. Create un modello come fareste con qualsiasi Modello pagina [come illustrato qui](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), che fungerà da base per il tipo di modello.
1. Utilizzando CRXDE Lite, copiate il modello appena creato dal `templates` nodo al `template-types` nodo sotto la cartella [del](#template-folders)modello.
1. Eliminate il modello dal `templates` nodo sotto la cartella [del](#template-folders)modello.
1. Nella copia del modello che si trova sotto il `template-types` nodo, eliminare tutte `cq:template` e `cq:templateType` le `jcr:content` proprietà.

Potete anche sviluppare un tipo di modello personalizzato utilizzando un modello modificabile di esempio come base, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto di tipo &quot;aem-sites-example-custom-template-type&quot; su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definizioni dei modelli {#template-definitions}

Le definizioni per i modelli modificabili sono memorizzate nelle cartelle [definite dall&#39;](#template-folders) utente (consigliato) o in alternativa in `global`. Esempio:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Il nodo principale del modello è di tipo `cq:Template` con una struttura di ossatura di:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Gli elementi principali sono:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

Questo nodo contiene le proprietà per il modello:

* **Nome**: `jcr:title`
* **Nome**: `status`
   * ``**Tipo**: `String`
   * **Valore**: `draft`, `enabled` or `disabled`

### Struttura {#structure}

Definisce la struttura della pagina risultante:

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una nuova pagina.
* Le modifiche apportate alla struttura si rifletteranno sulle pagine create con il modello.
* Il nodo `root` ( `structure/jcr:content/root`) definisce l’elenco dei componenti che saranno disponibili nella pagina risultante.
   * I componenti definiti nella struttura del modello non possono essere spostati né eliminati dalle pagine risultanti.
   * Quando un componente viene sbloccato, la `editable` proprietà viene impostata su `true`.
   * Quando un componente che contiene già del contenuto viene sbloccato, il contenuto viene spostato nel `initial` ramo.

* Il `cq:responsive` nodo contiene le definizioni per il layout reattivo.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un `jcr:content` nodo che viene copiato in qualsiasi nuova pagina.
* Viene unito alla struttura ( `/structure`) durante la creazione di una nuova pagina.
* Eventuali pagine esistenti non verranno aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* Il `root` nodo contiene un elenco di componenti per definire ciò che sarà disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e tale componente viene successivamente sbloccato (o viceversa), tale contenuto viene utilizzato come contenuto iniziale.

### Layout {#layout}

Quando [modificate un modello potete definire il layout](/help/sites-cloud/authoring/features/templates.md), questo utilizza il layout [reattivo](/help/sites-cloud/authoring/features/responsive-layout.md)standard.

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Content Policies {#content-policies}

I criteri di contenuto definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello). I criteri di contenuto possono essere creati e selezionati nell&#39;editor modelli.

* La proprietà `cq:policy`, sul `root` nodo
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, nei nodi espliciti dei componenti in `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

### Criteri di pagina {#page-policies}

I criteri di pagina consentono di definire i criteri [di](#content-policies) contenuto per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e abilitazione di un modello per l&#39;uso {#enabling-and-allowing-a-template-for-use}

1. **Abilita modello**

   Per poter utilizzare un modello, è necessario che sia attivato:

   * [Abilitazione del modello](/help/sites-cloud/authoring/features/templates.md#enablingatemplateauthor) dalla console **Modelli** .

   * Impostazione della proprietà status sul `jcr:content` nodo.

      * Ad esempio, on:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definire la proprietà:

         * Nome: status
         * Tipo: Stringa
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definire i percorsi dei modelli consentiti nelle proprietà **di**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) pagina della pagina o della pagina principale appropriata di un ramo secondario.
   * Impostare la proprietà:
      `cq:allowedTemplates`
In 
`jcr:content` del ramo richiesto.
   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine di contenuti risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Vengono creati con una sottostruttura ad albero che viene unita da `structure` e `initial` nel modello

* Contiene riferimenti alle informazioni contenute nel modello e nel tipo di modello. Questo si ottiene con un `jcr:content` nodo con le proprietà:

   * `cq:template` - Fornisce il riferimento dinamico al modello effettivo; consente di riflettere le modifiche apportate al modello sulle pagine effettive.

   * `cq:templateType` - Fornisce un riferimento al tipo di modello.

![Modalità di interazione tra modelli, contenuti e componenti](/help/implementing/developing/introduction/assets/templates-content-components.png)

Il diagramma precedente mostra come i modelli, i contenuti e i componenti si interfacciano:

* Controller - `/content/<my-site>/<my-page>` - La pagina risultante che fa riferimento al modello. Il contenuto controlla l’intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.
* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - Il [modello e i relativi criteri](#template-definitions) di contenuto definiscono la configurazione della pagina.
* Modello - Pacchetti OSGi - I bundle [OSGI](/help/implementing/deploying/configuring-osgi.md) implementano la funzionalità.
* Visualizzazione - `/apps/<my-site>/components` - Sia nell’ambiente di creazione che nell’ambiente di pubblicazione, il rendering del contenuto viene eseguito dai componenti.

Durante il rendering di una pagina:

* **Modelli**:

   * Viene fatto riferimento alla `cq:template` proprietà del relativo `jcr:content` nodo per accedere al modello corrispondente alla pagina.

* **Componenti**:

   * Il componente Pagina unisce la `structure/jcr:content` struttura ad albero del modello alla `jcr:content` struttura ad albero della pagina.
      * Il componente Pagina consente solo all’autore di modificare i nodi della struttura del modello contrassegnati come modificabili (così come altri elementi secondari).
      * Quando si esegue il rendering di un componente su una pagina, il percorso relativo di tale componente viene ricavato dal `jcr:content` nodo; viene quindi ricercato lo stesso percorso sotto il `policies/jcr:content` nodo del modello.
         * La `cq:policy` proprietà di questo nodo fa riferimento al criterio del contenuto effettivo (ovvero contiene la configurazione di progettazione per quel componente).
            * Questo consente di avere più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.

### Disponibilità del modello {#template-availability}

Quando si crea una nuova pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle limitazioni alla posizione specificate in ciascun modello.

Le proprietà seguenti determinano se un modello `T` può essere utilizzato per inserire una nuova pagina come figlio di una pagina `P`. Ciascuna di queste proprietà è una stringa con più valori che contiene zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* La `cq:allowedTemplates` proprietà del `jcr:content` nodo secondario di `P` o di un predecessore di `P`.

* La `allowedPaths` proprietà di `T`.

* La `allowedParents` proprietà di `T`.

* La `allowedChildren` proprietà del modello di `P`.

La valutazione funziona come segue:

* La prima `cq:allowedTemplates` proprietà non vuota trovata durante l&#39;ascendente della gerarchia di pagina che inizia con `P` viene confrontata con il percorso di `T`. Se nessuno dei valori corrisponde, `T` viene rifiutato.

* Se `T` esiste una `allowedPaths` proprietà non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` viene rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` viene rifiutato a meno che non appartengano alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione come `P` if e solo se il nome del secondo livello del percorso `T` è uguale al nome del secondo livello del percorso di `P`. Ad esempio, il modello `/apps/geometrixx/templates/foo` appartiene alla stessa applicazione della pagina `/content/geometrixx`.

* Se `T` è presente una `allowedParents` proprietà non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` viene rifiutato.

* Se il modello di `P` dispone di una `allowedChildren` proprietà non vuota, ma nessuno dei valori corrisponde al percorso di `T`, `T` viene rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione dei modelli:

![Processo di valutazione dei modelli](/help/implementing/developing/introduction/assets/template-evaluation.png)

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Siti**. Tuttavia, combinarle può portare a regole molto complesse che sono difficili da monitorare e gestire.
>
>Pertanto,  Adobe consiglia di iniziare in modo semplice, definendo:
>
>* solo la `cq:allowedTemplates` proprietà
   >
   >
* solo nella directory principale del sito
>
>
Per un esempio, consultate il contenuto dell&#39;esercitazione [](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND: `/content/wknd/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents`e `allowedChildren` possono essere inserite anche nei modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice definire ulteriori `cq:allowedTemplates` proprietà nelle sottosezioni del sito, se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio è rappresentato dal fatto che le `cq:allowedTemplates` proprietà possono essere aggiornate da un autore nella scheda **Avanzate** delle Proprietà **di** pagina. Le altre proprietà del modello non possono essere aggiornate utilizzando l&#39;interfaccia (standard), pertanto per ogni modifica è necessario che uno sviluppatore mantenga le regole e implementi il codice.

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli che possono essere utilizzati per creare pagine figlie in una determinata pagina, utilizzate la `cq:allowedTemplates` proprietà del `jcr:content` nodo della pagina per specificare l&#39;elenco di modelli da consentire come pagine figlie. Ogni valore nell&#39;elenco deve essere un percorso assoluto a un modello per una pagina figlia consentita, ad esempio `/apps/wknd/templates/page-content`.

È possibile utilizzare la `cq:allowedTemplates` proprietà sul nodo del modello `jcr:content` per applicare questa configurazione a tutte le pagine create di recente che utilizzano questo modello.

Se desiderate aggiungere altri vincoli, ad esempio per quanto riguarda la gerarchia del modello, potete utilizzare le `allowedParents/allowedChildren` proprietà del modello. Potete quindi specificare esplicitamente che le pagine create da un modello T devono essere pagine padre/figlio di pagine create da un modello T.
