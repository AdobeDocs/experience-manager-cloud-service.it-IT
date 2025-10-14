---
title: Modelli modificabili
description: Scopri come vengono utilizzati i modelli modificabili durante la creazione di una pagina, definendone il contenuto iniziale, il contenuto strutturato, le policy di authoring e il layout.
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 4%

---

# Modelli modificabili {#editable-templates}

Scopri come vengono utilizzati i modelli modificabili durante la creazione di una pagina, definendone il contenuto iniziale, il contenuto strutturato, le policy di authoring e il layout.

## Panoramica {#overview}

Durante la creazione di una pagina è necessario selezionare un modello. Il modello di pagina viene utilizzato come base per la nuova pagina. Il modello può definire la struttura della pagina risultante, tutto il contenuto iniziale e i componenti che possono essere utilizzati (proprietà di progettazione).

* I modelli modificabili consentono agli autori di creare e utilizzare i modelli.
* I modelli modificabili possono essere utilizzati per creare pagine modificabili sia con
   * [Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md) e
   * [Editor universale](/help/sites-cloud/authoring/universal-editor/templates.md)

I modelli di pagine utilizzati per creare pagine modificabili con Universal Editor utilizzano un sottoinsieme limitato di funzionalità di modelli modificabili. Pertanto, il resto di questo documento si concentra sui modelli modificabili utilizzati per creare pagine modificabili con l’Editor pagina.

## Modelli e pagine modificabili modificati con Editor pagina {#page-editor}

Durante la creazione di modelli per la creazione di pagine modificabili con Editor pagina, vengono normalmente identificati gli autori specializzati.

* Tali autori specializzati sono denominati **autori di modelli**
* Gli autori dei modelli devono essere membri del gruppo `template-authors`.
* I modelli modificabili mantengono una connessione dinamica a qualsiasi pagina creata da essi. In questo modo, eventuali modifiche al modello verranno applicate anche alle pagine.
* I modelli modificabili rendono il componente Pagina più generico, pertanto il componente Pagina principale può essere utilizzato senza personalizzazione.

Con i modelli modificabili, le parti che compongono una pagina vengono isolate all’interno dei componenti. Puoi configurare le combinazioni necessarie di componenti in un’interfaccia utente, eliminando in tal modo la necessità di sviluppare un nuovo componente pagina per ogni variante di pagina.

Questo documento:

* Panoramica sulla creazione di un modello modificabile
* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili
* Descrive come AEM valuta la disponibilità di un modello

>[!NOTE]
>
>In questo documento si presuppone che tu abbia già familiarità con la creazione e la modifica di modelli. Vedere il documento di creazione [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md), che descrive le funzionalità dei modelli modificabili esposti all&#39;autore del modello.

>[!TIP]
>
>[L&#39;esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) approfondisce le modalità di utilizzo dei modelli modificabili implementando un esempio ed è molto utile per comprendere come impostare un modello in un nuovo progetto

## Creazione di un nuovo modello modificabile {#creating-a-new-template}

La creazione di modelli modificabili viene eseguita principalmente con la console [modelli e l&#39;editor modelli](/help/sites-cloud/authoring/page-editor/templates.md) da un autore di modelli. Questa sezione offre una panoramica di questo processo e segue con una descrizione di ciò che accade a livello tecnico.

Quando crei un modello modificabile:

1. Crea una cartella [&#x200B; per i modelli](#template-folders). Questo non è obbligatorio, ma è una best practice consigliata.
1. Seleziona un tipo di [modello](#template-type). Viene copiato per creare la [definizione modello](#template-definitions).

   >[!NOTE]
   >
   >È disponibile una selezione di tipi di modello pronti all’uso. Se necessario, puoi anche [creare tipi di modello specifici per il sito](#creating-template-types).

1. Configura la struttura, i criteri per i contenuti, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura ti consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati in una pagina risultante né eliminati dalle pagine risultanti.
   * Se desideri che gli autori delle pagine possano aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sulla struttura, vedere [Struttura](#structure) in questo documento.

   **Criteri**

   * I criteri per contenuto definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minima/massima.

   * Sono applicabili al modello (e alle pagine create con il modello).

   Per informazioni dettagliate su come un autore di modelli definisce i criteri, vedere [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sui criteri, vedi [Criteri di contenuto](#content-policies) in questo documento.

   **Contenuto iniziale**

   * Il contenuto iniziale definisce il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può quindi essere modificato dagli autori di pagine.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-initial-content-author).

   Per informazioni tecniche sul contenuto iniziale, vedere [Contenuto iniziale](#initial-content) in questo documento.

   **Layout**

   * Puoi definire il layout del modello per una serie di dispositivi.
   * Il layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate su come un autore di modelli definisce il layout del modello, vedere [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-layout-template-author).

   Per informazioni tecniche sul layout del modello, vedere [Layout](#layout) in questo documento.

1. Abilita il modello, quindi consenti la creazione di strutture di contenuto specifiche.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile agli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate su come un autore di modelli abilita un modello, vedere [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author).

   Per informazioni tecniche sull&#39;abilitazione di un modello, vedere [Abilitazione e autorizzazione di un modello](#enabling-and-allowing-a-template-for-use)e in questo documento

1. Utilizzala per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una pagina, non vi è alcuna differenza visibile né indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate su come un autore di pagine utilizza i modelli per creare una pagina, vedere [Creazione e organizzazione delle pagine](/help/sites-cloud/authoring/sites-console/organizing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, vedere [Pagine di contenuto risultanti](#resultant-content-pages) in questo documento.

>[!TIP]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. Ai fini dell&#39;internalizzazione, si consiglia di utilizzare le [funzionalità di localizzazione dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it).

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione della pagina. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>La libreria client dell&#39;editor presuppone la presenza dello spazio dei nomi `cq.shared` nelle pagine di contenuto e, in caso contrario, si verificherà l&#39;errore di JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di esse include automaticamente `cq.shared`. Tuttavia, se decidi di creare pagine di contenuto personalizzate da zero senza basarle su contenuto di esempio, devi assicurarti di includere lo spazio dei nomi `cq.shared`.
>
>Per ulteriori informazioni, vedere [Utilizzo delle librerie lato client](/help/implementing/developing/introduction/clientlibs.md).

## Cartelle modelli {#template-folders}

Per organizzare i modelli è possibile utilizzare le cartelle seguenti:

* `global`
* Specifico del sito

>[!NOTE]
>
>Anche se è possibile nidificare le cartelle, quando l&#39;utente le visualizza nella console **Modelli**, vengono presentate come una struttura semplice.

In un&#39;istanza AEM standard la cartella `global` esiste già nella console modelli. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. Puoi aggiungere i modelli predefiniti a questa cartella o crearne una (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una cartella contenente i modelli personalizzati e non utilizzare la cartella `global`.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con diritti `admin`.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente
1. Elementi padre della cartella corrente
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se le configurazioni si sovrappongono ( `path`/ `label`), verrà presentata all&#39;utente solo l&#39;istanza più vicina alla cartella corrente.

Per creare una cartella, puoi effettuare le seguenti operazioni:

* A livello di programmazione o con CRXDE Lite
* Utilizzo di [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

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

1. Puoi quindi definire le seguenti proprietà sul nodo principale della cartella:

   `<your-folder-name> [sling:Folder]`

   * Nome: `jcr:title`
   * Tipo: `String`
   * Valore: il titolo (per la cartella) che si desidera visualizzare nella console **Modelli**.

1. Oltre alle autorizzazioni e ai privilegi di authoring standard (ad esempio, `content-authors`), ora è necessario assegnare i gruppi e definire i diritti di accesso (ACL) necessari affinché gli autori possano creare modelli nella nuova cartella.

   Il gruppo `template-authors` è il gruppo predefinito che deve essere assegnato. Per informazioni dettagliate, consulta la sezione [ACL e gruppi](#acls-and-groups).

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Utilizzo del browser configurazioni {#using-the-configuration-browser}

1. Vai a **Navigazione globale** > **Strumenti** > [**Browser configurazioni**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   Le cartelle esistenti sono elencate a sinistra, inclusa la cartella `global`.

1. Fai clic su **Crea**.
1. Nella finestra di dialogo **Crea configurazione** è necessario configurare i campi seguenti:

   * **Titolo**: specifica un titolo per la cartella di configurazione
   * **Modelli modificabili**: selezionare per consentire modelli modificabili in questa cartella

1. Fai clic su **Crea**.

>[!NOTE]
>
>Nel [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser), è possibile modificare la cartella globale e attivare l&#39;opzione **Modelli modificabili** se si desidera creare modelli in questa cartella, tuttavia questa non è la best practice consigliata.

### ACL e gruppi {#acls-and-groups}

Una volta create le cartelle di modelli (tramite CRXDE o con il Browser configurazioni), per garantire la corretta protezione è necessario definire gli ACL per i gruppi appropriati per le cartelle di modelli.

È possibile utilizzare come esempio le cartelle dei modelli per l&#39;[esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

#### Gruppo di autori di modelli {#the-template-authors-group}

Il gruppo `template-authors` è il gruppo utilizzato per gestire l&#39;accesso ai modelli e viene fornito come standard con AEM, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>Il gruppo `template-authors` è solo per gli utenti che devono essere in grado di creare nuovi modelli.
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
   <td>Autori modelli<br /> </td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> specifico del sito</td>
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
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> specifico del sito</td>
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

Questo gruppo `template-authors` predefinito copre solo le impostazioni del progetto, in cui tutti i membri `template-authors` possono accedere e creare tutti i modelli. Per impostazioni più complesse, in cui sono necessari più gruppi di autori di modelli per separare l’accesso ai modelli, è necessario creare più gruppi di autori di modelli personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori di modelli continuerebbero a essere le stesse.

## Tipo di modello {#template-type}

Durante la creazione di un modello è necessario specificare un tipo di modello:

* I tipi di modello forniscono in modo efficace i modelli per un modello. Durante la creazione di un modello, per creare il nuovo modello vengono utilizzati la struttura e il contenuto iniziale del tipo di modello selezionato.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta eseguita la copia, l&#39;unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Tipo di risorsa del componente Pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell’editor di modelli.
   * È consigliabile definire i punti di interruzione per la griglia reattiva e la configurazione dell’emulatore mobile in sul tipo di modello.

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina di HTML5 e Pagina modulo adattivo.

   * Esempi aggiuntivi vengono forniti come parte dell&#39;esercitazione [WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* I tipi di modello vengono in genere definiti dagli sviluppatori.

I tipi di modello preconfigurati sono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non è necessario modificare nulla nel percorso `/libs`. Questo perché il contenuto di `/libs` può essere sovrascritto in qualsiasi momento da un aggiornamento dell&#39;AEM.

I tipi di modello specifici per il sito devono essere memorizzati nella posizione simile di:

* `/apps/settings/wcm/template-types`

Le definizioni per i tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (scelta consigliata) o in alternativa in `global`. Ad esempio:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>I tipi di modello devono rispettare la struttura di cartelle corretta (ovvero `/settings/wcm/...`), altrimenti i tipi di modello non verranno trovati.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating an editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

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

1. Crea un modello come faresti con qualsiasi modello pagina. Consulta [Modelli per creare pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md#creating-a-new-template-template-author). Questo fungerà da base per il tipo di modello.
1. Utilizzando CRXDE Lite, copiare il modello creato dal nodo `templates` al nodo `template-types` nella [cartella modelli](#template-folders).
1. Elimina il modello dal nodo `templates` nella [cartella modelli](#template-folders).
1. Nella copia del modello presente nel nodo `template-types`, eliminare tutte le proprietà `cq:template` e `cq:templateType` da tutti i nodi `jcr:content`.

Puoi anche sviluppare un tipo di modello personalizzato utilizzando come base un modello modificabile di esempio, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-sites-example-custom-template-type su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definizioni dei modelli {#template-definitions}

Le definizioni per i modelli modificabili sono archiviate [cartelle definite dall&#39;utente](#template-folders) (consigliato) o in alternativa in `global`. Ad esempio:

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

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una pagina.
* Le modifiche apportate alla struttura vengono applicate a tutte le pagine create con il modello.
* Il nodo `root` ( `structure/jcr:content/root`) definisce l&#39;elenco dei componenti disponibili nella pagina risultante.
   * I componenti definiti nella struttura del modello non possono essere spostati o eliminati dalle pagine risultanti.
   * Dopo lo sblocco di un componente, la proprietà `editable` è impostata su `true`.
   * Dopo lo sblocco di un componente che contiene già contenuto, questo contenuto viene spostato nel ramo `initial`.

* Il nodo `cq:responsive` contiene le definizioni per il layout reattivo.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un nodo `jcr:content` copiato in qualsiasi nuova pagina.
* Viene unito alla struttura ( `/structure`) durante la creazione di una pagina.
* Le pagine esistenti non verranno aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* Il nodo `root` contiene un elenco di componenti per definire ciò che è disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e successivamente viene sbloccato (o viceversa), tale contenuto viene utilizzato come contenuto iniziale.

### Layout {#layout}

Quando [modifichi un modello puoi definire il layout](/help/sites-cloud/authoring/page-editor/templates.md), questo utilizza il [layout responsive standard](/help/sites-cloud/administering/responsive-layout.md), che può essere [configurato nella pagina dall&#39;autore di contenuto](/help/sites-cloud/authoring/page-editor/responsive-layout.md).

### Criteri per contenuto {#content-policies}

I criteri per contenuto definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minime/massime. Sono applicabili al modello (e alle pagine create con il modello). I criteri per i contenuti possono essere creati e selezionati nell’editor modelli.

* La proprietà `cq:policy` nel nodo `root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, nei nodi espliciti del componente in `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

### Criteri di pagina {#page-policies}

I criteri di pagina consentono di definire il [criterio contenuto](#content-policies) per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e autorizzazione di un modello per l’utilizzo {#enabling-and-allowing-a-template-for-use}

1. **Abilita il modello**

   Prima di poter utilizzare un modello, è necessario abilitarlo in uno dei modi seguenti:

   * [Abilitazione del modello](/help/sites-cloud/authoring/page-editor/templates.md) dalla console **Modelli**.

   * Impostazione della proprietà di stato nel nodo `jcr:content`.

      * Ad esempio, su:

        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definisci la proprietà:

         * Nome: stato
         * Tipo: String
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definisci i percorsi dei modelli consentiti nelle **Proprietà pagina**](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) della pagina appropriata o della pagina principale di un ramo secondario.
   * Imposta la proprietà:

     `cq:allowedTemplates`
Nel nodo `jcr:content` del ramo richiesto.

   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine di contenuto risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Sono state create con una sottostruttura unita da `structure` e `initial` nel modello

* Includere riferimenti alle informazioni contenute nel modello e nel tipo di modello. Ciò si ottiene con un nodo `jcr:content` con le proprietà:

   * `cq:template` - Fornisce il riferimento dinamico al modello effettivo; consente di riflettere le modifiche al modello sulle pagine effettive.

   * `cq:templateType` - Fornisce un riferimento al tipo di modello.

![Relazione tra modelli, contenuti e componenti](assets/templates-content-components.png)

Il diagramma precedente mostra l’interrelazione tra modelli, contenuto e componenti:

* Controller - `/content/<my-site>/<my-page>` - Pagina risultante che fa riferimento al modello. Il contenuto controlla l&#39;intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.
* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - Il [modello e i criteri dei contenuti correlati](#template-definitions) definiscono la configurazione della pagina.
* Modello - Bundle OSGi - [Bundle OSGi](/help/implementing/deploying/configuring-osgi.md) implementano la funzionalità.
* Visualizzazione - `/apps/<my-site>/components` - Negli ambienti di authoring e di pubblicazione il contenuto viene riprodotto dai componenti.

Durante il rendering di una pagina:

* **Modelli**:

   * Per accedere al modello corrispondente alla pagina, viene fatto riferimento alla proprietà `cq:template` del nodo `jcr:content`.

* **Componenti**:

   * Il componente page unirà la struttura `structure/jcr:content` del modello alla struttura `jcr:content` della pagina.
      * Il componente Pagina consente all’autore di modificare solo i nodi della struttura del modello contrassegnati come modificabili (e gli eventuali elementi secondari).
      * Durante il rendering di un componente su una pagina, il percorso relativo di tale componente viene preso dal nodo `jcr:content`; verrà quindi cercato lo stesso percorso nel nodo `policies/jcr:content` del modello.
         * La proprietà `cq:policy` di questo nodo punta al criterio del contenuto effettivo, ovvero contiene la configurazione di progettazione per quel componente.
            * In questo modo è possibile disporre di più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.

### Disponibilità dei modelli {#template-availability}

Durante la creazione di una pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni sul posizionamento specificate in ciascun modello.

Le seguenti proprietà determinano se è consentito utilizzare un modello `T` per inserire una nuova pagina come elemento figlio della pagina `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* Proprietà `cq:allowedTemplates` del sottonodo `jcr:content` di `P` o predecessore di `P`.

* La proprietà `allowedPaths` di `T`.

* La proprietà `allowedParents` di `T`.

* La proprietà `allowedChildren` del modello di `P`.

La valutazione funziona come segue:

* La prima proprietà `cq:allowedTemplates` non vuota trovata durante l&#39;ascesa della gerarchia di pagine a partire da `P` viene confrontata con il percorso di `T`. Se nessuno dei valori corrisponde, `T` viene rifiutato.

* Se `T` ha una proprietà `allowedPaths` non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` verrà rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` verrà rifiutato a meno che non appartenga alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione di `P` se e solo se il nome del secondo livello del percorso di `T` è uguale al nome del secondo livello del percorso di `P`. Ad esempio, il modello `/apps/wknd/templates/foo` appartiene alla stessa applicazione della pagina `/content/wknd`.

* Se `T` ha una proprietà `allowedParents` non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` verrà rifiutato.

* Se il modello di `P` ha una proprietà `allowedChildren` non vuota, ma nessuno dei valori corrisponde al percorso di `T`, `T` verrà rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione del modello:

![Processo di valutazione modello](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, la loro combinazione può portare a regole molto complesse e difficili da tracciare e gestire.
>
>Pertanto, Adobe consiglia di iniziare da semplice, definendo:
>
>* solo la proprietà `cq:allowedTemplates`
>
>* solo nella directory principale del sito
>
>Ad esempio, consulta l&#39;[esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) contenuto: `/content/wknd/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents` e `allowedChildren` possono anche essere posizionate nei modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice definire ulteriori `cq:allowedTemplates` proprietà nelle sottosezioni del sito se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio consiste nel fatto che le proprietà `cq:allowedTemplates` possono essere aggiornate da un autore nella scheda **Avanzate** delle **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l’interfaccia utente (standard), pertanto avrebbe bisogno di uno sviluppatore per mantenere le regole e una distribuzione del codice per ogni modifica.

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli utilizzabili per creare pagine figlie in una determinata pagina, utilizzare la proprietà `cq:allowedTemplates` di `jcr:content` nodo della pagina per specificare l&#39;elenco di modelli consentiti come pagine figlie. Ogni valore nell&#39;elenco deve essere il percorso assoluto di un modello per una pagina figlio consentita, ad esempio `/apps/wknd/templates/page-content`.

È possibile utilizzare la proprietà `cq:allowedTemplates` nel nodo `jcr:content` del modello per applicare questa configurazione a tutte le pagine create che utilizzano questo modello.

Per aggiungere altri vincoli, ad esempio relativi alla gerarchia dei modelli, è possibile utilizzare le proprietà `allowedParents/allowedChildren` nel modello. È quindi possibile specificare esplicitamente che le pagine create da un modello devono essere padri/figli di pagine create da un modello T.
