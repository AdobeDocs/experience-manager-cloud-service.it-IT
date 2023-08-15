---
title: Modelli di pagina
description: I Modelli di pagina vengono utilizzati durante la creazione di una pagina utilizzata come base per la nuova pagina
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 5%

---

# Modelli di pagina {#page-templates}

Durante la creazione di una pagina è necessario selezionare un modello. Il modello di pagina viene utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina risultante, eventuali contenuti iniziali e i componenti che possono essere utilizzati (proprietà di progettazione). Questo offre diversi vantaggi:

* I modelli di pagina consentono agli autori specializzati di [creare e modificare modelli](/help/sites-cloud/authoring/features/templates.md).
   * Tali autori specializzati sono chiamati **autori di modelli**
   * Gli autori dei modelli devono essere membri di `template-authors` gruppo.
* I modelli di pagina mantengono una connessione dinamica a tutte le pagine create da essi. In questo modo, eventuali modifiche al modello verranno applicate anche alle pagine.
* I modelli di pagina rendono il componente Pagina più generico, in modo che il componente Pagina principale possa essere utilizzato senza personalizzazione.

Con Modelli di pagina, i pezzi che compongono una pagina sono isolati all’interno dei componenti. Puoi configurare le combinazioni necessarie di componenti in un’interfaccia utente, eliminando in tal modo la necessità di sviluppare un nuovo componente pagina per ogni variante di pagina.

Questo documento:

* Panoramica sulla creazione di un modello di pagina
* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili
* Descrive come AEM valuta la disponibilità di un modello

>[!NOTE]
>
>In questo documento si presuppone che tu abbia già familiarità con la creazione e la modifica di modelli. Consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md), che descrive le funzionalità dei modelli modificabili come esposti all’autore del modello.

>[!TIP]
>
>[Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) Approfondisce le modalità di utilizzo dei modelli di pagina implementando un esempio ed è molto utile per comprendere come impostare un modello in un nuovo progetto

## Creazione di un nuovo modello {#creating-a-new-template}

La creazione di modelli di pagina viene eseguita principalmente con [console modelli ed editor modelli](/help/sites-cloud/authoring/features/templates.md) da un autore di modelli. Questa sezione offre una panoramica di questo processo e segue con una descrizione di ciò che accade a livello tecnico.

Quando crei un nuovo modello modificabile:

1. Creare un [cartella per i modelli](#template-folders). Questo non è obbligatorio, ma è una best practice consigliata.
1. Seleziona un [tipo di modello](#template-type). Viene copiato per creare [definizione modello](#template-definitions).

   >[!NOTE]
   >
   >È disponibile una selezione di tipi di modello pronti all’uso. È inoltre possibile [creare tipi di modello specifici per il sito](#creating-template-types) se necessario.

1. Configura la struttura, i criteri per i contenuti, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura ti consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati in una pagina risultante né eliminati dalle pagine risultanti.
   * Se desideri che gli autori delle pagine possano aggiungere e rimuovere componenti, aggiungi un sistema paragrafo al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Per i dettagli tecnici della struttura, vedi [Struttura](#structure) in questo documento.

   **Criteri**

   * I criteri per contenuto definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minima/massima.

   * Sono applicabili al modello (e alle pagine create con il modello).

   Per informazioni dettagliate su come un autore di modelli definisce i criteri, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sui criteri, consulta [Criteri per contenuto](#content-policies) in questo documento.

   **Contenuto iniziale**

   * Il contenuto iniziale definisce il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può quindi essere modificato dagli autori di pagine.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   Per informazioni tecniche sul contenuto iniziale, vedi [Contenuto iniziale](#initial-content) in questo documento.

   **Layout**

   * È possibile definire il layout del modello per una serie di dispositivi.
   * Il Layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate su come un autore di modelli definisce il layout di un modello, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   Per informazioni tecniche sul layout dei modelli, consulta [Layout](#layout) in questo documento.

1. Abilita il modello, quindi consenti la creazione di strutture di contenuto specifiche.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile agli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate su come un autore di modelli abilita un modello, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Per informazioni tecniche sull’abilitazione di un modello, consulta [Abilitazione e autorizzazione di un modello per l’utente](#enabling-and-allowing-a-template-for-use)e nel presente documento

1. Utilizzala per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una nuova pagina, non vi è alcuna differenza visibile né indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate su come un autore di pagine utilizza i modelli per creare una pagina, consulta [Creazione e organizzazione delle pagine](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, consulta [Pagine di contenuto risultanti](#resultant-content-pages) in questo documento.

>[!TIP]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. Ai fini dell&#39;internalizzazione, la [funzioni di localizzazione dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it) sono consigliati.

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione della pagina. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>La libreria client dell’editor presuppone la presenza di `cq.shared` nelle pagine di contenuto e, se è assente, l’errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` risulterà.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di essi include automaticamente `cq.shared`. Tuttavia, se decidi di creare pagine di contenuto personalizzate da zero senza basarle su contenuti di esempio, devi assicurarti di includere `cq.shared` spazio dei nomi.
>
>Consulta [Utilizzo delle librerie lato client](/help/implementing/developing/introduction/clientlibs.md) per ulteriori informazioni.



## Cartelle modelli {#template-folders}

Per organizzare i modelli è possibile utilizzare le cartelle seguenti:

* `global`
* Specifico del sito

>[!NOTE]
>
>Anche se è possibile nidificare le cartelle, quando l’utente le visualizza in **Modelli** console sono presentati come una struttura piatta.

In un caso di AEM standard, la `global` La cartella esiste già nella console dei modelli. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. Puoi aggiungere i modelli predefiniti a questa cartella o crearne una nuova (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una nuova cartella in cui inserire i modelli personalizzati e non utilizzare `global` cartella.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con `admin` diritti.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente
1. Elementi padre della cartella corrente
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se le configurazioni si sovrappongono ( `path`/ `label`), viene presentata all’utente solo l’istanza più vicina alla cartella corrente.

Per creare una nuova cartella, puoi effettuare le seguenti operazioni:

* A livello di programmazione o con CRXDE Liti
* Utilizzo di [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## Utilizzo di CRXDE Lite {#using-crxde-lite}

1. È possibile creare una nuova cartella (in /conf) per l’istanza a livello di programmazione o con CRXDE Liti.

   Deve essere utilizzata la seguente struttura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Puoi quindi definire le seguenti proprietà sul nodo principale della cartella:

   `<your-folder-name> [sling:Folder]`

   * Nome: `jcr:title`
   * Tipo: `String`
   * Valore: il titolo (per la cartella) che desideri visualizzare nel **Modelli** console.

1. Oltre alle autorizzazioni e ai privilegi di authoring standard (ad esempio, `content-authors`) ora devi assegnare i gruppi e definire i diritti di accesso (ACL) necessari affinché gli autori possano creare modelli nella nuova cartella.

   Il `template-authors` gruppo è il gruppo predefinito da assegnare. Consulta la sezione [ACL e gruppi](#acls-and-groups) per i dettagli.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Utilizzo del browser configurazioni {#using-the-configuration-browser}

1. Vai a **Navigazione globale** -> **Strumenti** > [**Browser configurazioni**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   Le cartelle esistenti sono elencate a sinistra, incluso `global` cartella.

1. Fai clic su **Crea**.
1. In **Crea configurazione** finestra di dialogo è necessario configurare i seguenti campi:

   * **Titolo**: specifica un titolo per la cartella di configurazione
   * **Modelli modificabili**: seleziona per consentire i modelli modificabili all’interno di questa cartella

1. Fai clic su **Crea**

>[!NOTE]
>
>In [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) puoi modificare la cartella globale e attivare **Modelli modificabili** se desideri creare modelli all’interno di questa cartella, tuttavia questa non è la best practice consigliata.

### ACL e gruppi {#acls-and-groups}

Una volta create le cartelle di modelli (tramite CRXDE o con il Browser configurazioni), per garantire la corretta protezione è necessario definire gli ACL per i gruppi appropriati per le cartelle di modelli.

Le cartelle dei modelli per [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) può essere utilizzato come esempio.

#### Gruppo di autori di modelli {#the-template-authors-group}

Il `template-authors` group è il gruppo utilizzato per gestire l’accesso ai modelli e viene fornito come standard con AEM, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>Il `template-authors` Il gruppo è solo per gli utenti che devono essere in grado di creare nuovi modelli.
>
>La modifica dei modelli è molto potente e, se non eseguita correttamente, i modelli esistenti possono essere interrotti. Pertanto, questo ruolo deve essere mirato e includere solo utenti qualificati.

La tabella seguente descrive le autorizzazioni necessarie per la modifica dei modelli.

<table>
 <tbody>
  <tr>
   <th>Percorso</th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni<br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autori di modelli<br /> </td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in siti specifici <code>/conf</code> spazio</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>letto</td>
   <td>L’utente web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>replicateGli autori di contenuti devono attivare i modelli di una pagina quando attivano una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in siti specifici <code>/conf</code> spazio</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>letto</td>
   <td>L’utente web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Gli autori di contenuti devono attivare i criteri di un modello di una pagina quando attivano una pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autore del modello</td>
   <td>letto</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti.</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

Questa impostazione predefinita `template-authors` il gruppo copre solo le impostazioni del progetto, in cui tutte `template-authors` ai membri è consentito accedere a tutti i modelli e crearli. Per impostazioni più complesse, in cui sono necessari più gruppi di autori di modelli per separare l’accesso ai modelli, è necessario creare più gruppi di autori di modelli personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori di modelli continuerebbero a essere le stesse.

## Tipo di modello {#template-type}

Quando si crea un nuovo modello, è necessario specificare un tipo di modello:

* I tipi di modello forniscono in modo efficace i modelli per un modello. Durante la creazione di un nuovo modello, per creare il nuovo modello vengono utilizzati la struttura e il contenuto iniziale del tipo di modello selezionato.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta eseguita la copia, l&#39;unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Tipo di risorsa del componente Pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell’editor di modelli.
   * È consigliabile definire i punti di interruzione per la griglia reattiva e la configurazione dell’emulatore mobile in sul tipo di modello.

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina di HTML5 e Pagina modulo adattivo.

   * Ulteriori esempi sono forniti come parte del [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* I tipi di modello vengono in genere definiti dagli sviluppatori.

I tipi di modello preconfigurati sono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non è necessario modificare nulla nel `/libs` percorso. Questo perché il contenuto di `/libs` può essere sovrascritto in qualsiasi momento da un aggiornamento dell’AEM.

I tipi di modello specifici per il sito devono essere memorizzati nella posizione simile di:

* `/apps/settings/wcm/template-types`

Le definizioni per i tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (scelta consigliata) o in alternativa in `global`. Ad esempio:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>I tipi di modello devono rispettare la struttura di cartelle corretta, ovvero `/settings/wcm/...`), altrimenti i tipi di modello non vengono trovati.

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

### Creazione di tipi di modello {#creating-template-types}

Se è stato creato un modello che può fungere da base per altri modelli, è possibile copiarlo come tipo di modello.

1. Crea un modello come faresti con un modello pagina [come documentato qui](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), che fungerà da base per il tipo di modello.
1. Utilizzando CRXDE Liti, copia il modello appena creato da `templates` nodo a `template-types` nodo sotto [cartella modelli](#template-folders).
1. Elimina il modello da `templates` nodo sotto [cartella modelli](#template-folders).
1. Nella copia del modello che si trova in `template-types` nodo, elimina tutto `cq:template` e `cq:templateType` proprietà da tutti `jcr:content` nodi.

Puoi anche sviluppare un tipo di modello personalizzato utilizzando come base un modello modificabile di esempio, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-sites-example-custom-template-type su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definizioni dei modelli {#template-definitions}

Vengono memorizzate le definizioni per i modelli modificabili [cartelle definite dall&#39;utente](#template-folders) (consigliato) o in alternativa in `global`. Ad esempio:

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

Gli elementi principali sono i seguenti:

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
   * &quot;**Tipo**: `String`
   * **Valore**: `draft`, `enabled` o `disabled`

### Struttura {#structure}

Definisce la struttura della pagina risultante:

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una nuova pagina.
* Le modifiche apportate alla struttura vengono applicate a tutte le pagine create con il modello.
* Il `root` ( `structure/jcr:content/root`) definisce l’elenco dei componenti disponibili nella pagina risultante.
   * I componenti definiti nella struttura del modello non possono essere spostati o eliminati dalle pagine risultanti.
   * Dopo aver sbloccato un componente, `editable` proprietà impostata su `true`.
   * Dopo aver sbloccato un componente che contiene già contenuto, questo viene spostato nel `initial` filiale.

* Il `cq:responsive` Il nodo contiene le definizioni per il layout reattivo.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un `jcr:content` che viene copiato in qualsiasi nuova pagina.
* Viene unito alla struttura ( `/structure`) durante la creazione di una nuova pagina.
* Le pagine esistenti non verranno aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* Il `root` node contiene un elenco di componenti per definire ciò che è disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e successivamente viene sbloccato (o viceversa), tale contenuto viene utilizzato come contenuto iniziale.

### Layout {#layout}

Quando [modifica di un modello è possibile definire il layout](/help/sites-cloud/authoring/features/templates.md), utilizza [layout responsivo standard](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Criteri per contenuto {#content-policies}

I criteri per contenuto definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minima/massima. Sono applicabili al modello (e alle pagine create con il modello). I criteri per i contenuti possono essere creati e selezionati nell’editor modelli.

* La proprietà `cq:policy`, sulla `root` nodo
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, sui nodi espliciti dei componenti in `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

### Criteri di pagina {#page-policies}

I criteri di pagina ti consentono di definire [criterio contenuto](#content-policies) per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e autorizzazione di un modello per l’utilizzo {#enabling-and-allowing-a-template-for-use}

1. **Abilita il modello**

   Prima di poter utilizzare un modello, è necessario abilitarlo in uno dei modi seguenti:

   * [Abilitazione del modello](/help/sites-cloud/authoring/features/templates.md) dal **Modelli** console.

   * Impostazione della proprietà status su `jcr:content` nodo.

      * Ad esempio, su:
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definisci la proprietà:

         * Nome: stato
         * Tipo: String
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definisci i percorsi dei modelli consentiti in **Proprietà pagina**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) della pagina o della pagina principale appropriata di un ramo secondario.
   * Imposta la proprietà:
     `cq:allowedTemplates`
Il giorno `jcr:content` nodo del ramo richiesto.

   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine di contenuto risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Sono create con una sottostruttura unita da `structure` e `initial` nel modello

* Includere riferimenti alle informazioni contenute nel modello e nel tipo di modello. Ciò si ottiene con una `jcr:content` con le proprietà:

   * `cq:template` - Fornisce il riferimento dinamico al modello effettivo; consente di riflettere le modifiche al modello sulle pagine effettive.

   * `cq:templateType` - Fornisce un riferimento al tipo di modello.

![Correlazione tra modelli, contenuti e componenti](assets/templates-content-components.png)

Il diagramma precedente mostra l’interrelazione tra modelli, contenuto e componenti:

* Controller - `/content/<my-site>/<my-page>` : pagina risultante che fa riferimento al modello. Il contenuto controlla l&#39;intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.
* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - Il [modelli e criteri per contenuti correlati](#template-definitions) definisci la configurazione della pagina.
* Modello - Pacchetti OSGi - La [Bundle OSGi](/help/implementing/deploying/configuring-osgi.md) implementa la funzionalità.
* Visualizza - `/apps/<my-site>/components` : i componenti eseguono il rendering del contenuto negli ambienti di authoring e di pubblicazione.

Durante il rendering di una pagina:

* **Modelli**:

   * Il `cq:template` proprietà del suo `jcr:content` Per accedere al modello corrispondente alla pagina, viene fatto riferimento al nodo.

* **Componenti**:

   * Il componente Pagina unirà il `structure/jcr:content` struttura del modello con `jcr:content` della pagina.
      * Il componente Pagina consente all’autore di modificare solo i nodi della struttura del modello contrassegnati come modificabili (e gli eventuali elementi secondari).
      * Quando si esegue il rendering di un componente su una pagina, il relativo percorso di tale componente viene ricavato da `jcr:content` nodo; lo stesso percorso sotto `policies/jcr:content` Verrà quindi eseguita una ricerca nel nodo del modello.
         * Il `cq:policy` proprietà di questo nodo punta al criterio del contenuto effettivo, ovvero contiene la configurazione di progettazione per quel componente.
            * In questo modo è possibile disporre di più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.

### Disponibilità dei modelli {#template-availability}

Quando si crea una nuova pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni sul posizionamento specificate in ciascun modello.

Le seguenti proprietà determinano se un modello `T` può essere utilizzata per inserire una nuova pagina come pagina figlia di `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* Il `cq:allowedTemplates` proprietà del `jcr:content` sottonodo di `P` o un predecessore di `P`.

* Il `allowedPaths` proprietà di `T`.

* Il `allowedParents` proprietà di `T`.

* Il `allowedChildren` proprietà del modello di `P`.

La valutazione funziona come segue:

* Il primo non vuoto `cq:allowedTemplates` è stata trovata una proprietà durante l’ascensione della gerarchia delle pagine che inizia con `P` corrisponde al percorso di `T`. Se nessuno dei valori corrisponde, `T` è stato rifiutato.

* Se `T` ha un valore non vuoto `allowedPaths` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è stato rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` viene rifiutato a meno che non appartenga alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione di `P` se e solo se il nome del secondo livello del percorso di `T` è uguale al nome del secondo livello del percorso di `P`. Ad esempio, il modello `/apps/wknd/templates/foo` appartiene alla stessa applicazione della pagina `/content/wknd`.

* Se `T` ha un valore non vuoto `allowedParents` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è stato rifiutato.

* Se il modello di `P` ha un valore non vuoto `allowedChildren` , ma nessuno dei valori corrisponde al percorso di `T`, `T` è stato rifiutato.

* In tutti gli altri casi: `T` è consentito.

Il diagramma seguente illustra il processo di valutazione del modello:

![Processo di valutazione del modello](assets/template-evaluation.png)

>[!CAUTION]
>
>L’AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, la loro combinazione può portare a regole molto complesse e difficili da tracciare e gestire.
>
>Pertanto, l’Adobe consiglia di iniziare da semplice, definendo:
>
>* solo il `cq:allowedTemplates` proprietà
>
>* solo nella directory principale del sito
>
>Ad esempio, consulta [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) contenuto: `/content/wknd/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents`, e `allowedChildren` può essere posizionato anche sui modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* definizione più semplice `cq:allowedTemplates` proprietà nelle sottosezioni del sito, se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio è che il `cq:allowedTemplates` Le proprietà possono essere aggiornate da un autore in **Avanzate** scheda di **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l’interfaccia utente (standard), pertanto avrebbe bisogno di uno sviluppatore per mantenere le regole e una distribuzione del codice per ogni modifica.

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli utilizzabili per creare pagine figlie in una determinata pagina, utilizza `cq:allowedTemplates` proprietà di `jcr:content` nodo della pagina per specificare l’elenco di modelli consentiti come pagine figlie. Ogni valore nell’elenco deve essere il percorso assoluto di un modello per una pagina figlia consentita, ad esempio `/apps/wknd/templates/page-content`.

È possibile utilizzare `cq:allowedTemplates` proprietà del modello  `jcr:content` per applicare questa configurazione a tutte le nuove pagine create che utilizzano questo modello.

Per aggiungere altri vincoli, ad esempio relativi alla gerarchia dei modelli, è possibile utilizzare `allowedParents/allowedChildren` proprietà nel modello. È quindi possibile specificare esplicitamente che le pagine create da un modello devono essere padri/figli di pagine create da un modello T.
