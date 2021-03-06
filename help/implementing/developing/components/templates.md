---
title: Modelli di pagina
description: I modelli di pagina vengono utilizzati per creare una pagina che verrà utilizzata come base per la nuova pagina
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '3296'
ht-degree: 8%

---

# Modelli di pagina {#page-templates}

Quando crei una pagina devi selezionare un modello. Il modello di pagina viene utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina risultante, eventuali contenuti iniziali e i componenti che possono essere utilizzati (proprietà di progettazione). Questo offre diversi vantaggi:

* I modelli di pagina consentono agli autori specializzati di: [creare e modificare modelli](/help/sites-cloud/authoring/features/templates.md).
   * Questi autori specializzati sono chiamati **autori di modelli**
   * Gli autori dei modelli devono essere membri del gruppo `template-authors` gruppo.
* I modelli di pagina mantengono una connessione dinamica a tutte le pagine create da essi. In questo modo tutte le modifiche apportate al modello verranno applicate alle pagine stesse.
* I modelli di pagina rendono il componente pagina più generico, in modo che possa essere utilizzato senza personalizzazione.

Con Modelli di pagina, le parti che compongono una pagina vengono isolate all’interno dei componenti. È possibile configurare le combinazioni di componenti necessarie in un’interfaccia utente, eliminando in tal modo la necessità di sviluppare un nuovo componente di pagina per ogni variante di pagina.

Questo documento:

* Offre una panoramica della creazione di un modello di pagina
* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili
* Descrive come AEM valuta la disponibilità di un modello

>[!NOTE]
>
>Questo documento presuppone che tu abbia già familiarità con la creazione e la modifica dei modelli. Vedere il documento di authoring [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md), che descrive le funzionalità dei modelli modificabili esposte all’autore del modello.

>[!TIP]
>
>[Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) illustra in dettaglio l’utilizzo dei modelli di pagina mediante l’implementazione di un esempio ed è utile per comprendere come impostare un modello in un nuovo progetto

## Creazione di un nuovo modello {#creating-a-new-template}

La creazione di modelli di pagina viene eseguita principalmente con [console e editor modelli](/help/sites-cloud/authoring/features/templates.md) da un autore di modelli. Questa sezione fornisce una panoramica di questo processo e ne segue una descrizione a livello tecnico.

Durante la creazione di un nuovo modello modificabile:

1. Crea un [cartella dei modelli](#template-folders). Questa operazione non è obbligatoria, ma è consigliata la best practice.
1. Seleziona una [tipo di modello](#template-type). Viene copiato per creare il [definizione del modello](#template-definitions).

   >[!NOTE]
   >
   >Viene fornita una selezione di tipi di modelli pronti all’uso. È inoltre possibile [creare tipi di modelli specifici per il sito](#creating-template-types) se necessario.

1. Configura la struttura, i criteri dei contenuti, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura ti consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati su una pagina risultante, né eliminati da alcuna pagina risultante.
   * Se desideri che gli autori delle pagine siano in grado di aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Per i dettagli tecnici della struttura, vedi [Struttura](#structure) in questo documento.

   **Criteri**

   * I criteri dei contenuti definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minime e massime.
   * Questi sono applicabili al modello (e alle pagine create con tale modello).

   Per informazioni dettagliate su come un autore di modelli definisce i criteri, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sulle politiche, consulta [Criteri di contenuto](#content-policies) in questo documento.

   **Contenuto iniziale**

   * Il contenuto iniziale definisce il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può quindi essere modificato dagli autori delle pagine.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   Per informazioni tecniche sul contenuto iniziale, consulta [Contenuto iniziale](#initial-content) in questo documento.

   **Layout**

   * È possibile definire il layout del modello per una serie di dispositivi.
   * Il Layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate sulla definizione del layout del modello da parte dell’autore, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   Per informazioni tecniche sul layout dei modelli, consulta [Layout](#layout) in questo documento.

1. Abilita il modello, quindi lo consenti per strutture di contenuto specifiche.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile agli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate su come un autore di modelli abilita un modello, consulta [Creazione di modelli di pagina](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Per informazioni tecniche sull’abilitazione di un modello, consulta [Abilitazione e autorizzazione di un modello per noi](#enabling-and-allowing-a-template-for-use)e in questo documento

1. Utilizzalo per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una nuova pagina, non vi è alcuna differenza visibile e nessuna indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate su come un autore di pagine utilizza i modelli per creare una pagina, consulta [Creazione e organizzazione delle pagine](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, consulta [Pagine dei contenuti risultanti](#resultant-content-pages) in questo documento.

>[!TIP]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. Ai fini dell&#39;internalizzazione, la [funzioni di localizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it) sono consigliati.

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione delle pagine. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>La libreria client dell&#39;editor presuppone la presenza di `cq.shared` spazio dei nomi nelle pagine di contenuto e se è assente nell&#39;errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` risulterà.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, quindi qualsiasi contenuto basato su di essi include automaticamente `cq.shared`. Tuttavia, se decidi di creare da zero pagine di contenuto personalizzate senza basarle su contenuti di esempio, devi assicurarti di includere il `cq.shared` spazio dei nomi.
>
>Vedi [Utilizzo delle librerie lato client](/help/implementing/developing/introduction/clientlibs.md) per ulteriori informazioni.



## Cartelle dei modelli {#template-folders}

Per organizzare i modelli è possibile utilizzare le cartelle seguenti:

* `global`
* Specifico del sito

>[!NOTE]
>
>Anche se è possibile nidificare le cartelle, quando l’utente le visualizza nel **Modelli** console sono presentate come una struttura piatta.

In un&#39;istanza AEM standard `global` cartella già esistente nella console modelli. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. È possibile aggiungere i modelli predefiniti a questa cartella o creare una nuova cartella (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una nuova cartella contenente i modelli personalizzati e non utilizzare la `global` cartella.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con `admin` diritti.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente
1. Elemento padre/i della cartella corrente
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se una qualsiasi configurazione si sovrappone ( `path`/ `label`), all’utente viene presentata solo l’istanza più vicina alla cartella corrente.

Per creare una nuova cartella è possibile effettuare le seguenti operazioni:

* Programmaticamente o con CRXDE Lite
* Utilizzo della [Browser di configurazione](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

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
   * Valore: Titolo (per la cartella) che si desidera visualizzare nel **Modelli** console.

1. Oltre alle autorizzazioni e ai privilegi standard per l’authoring (ad es. `content-authors`) devi ora assegnare i gruppi e definire i diritti di accesso richiesti (ACL, Access Rights) affinché gli autori possano creare modelli nella nuova cartella.

   La `template-authors` gruppo è il gruppo predefinito che deve essere assegnato. Vedi la sezione [ACL e gruppi](#acls-and-groups) per i dettagli.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Utilizzo del browser di configurazione {#using-the-configuration-browser}

1. Vai a **Navigazione globale** -> **Strumenti** > [**Browser di configurazione**.](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   Le cartelle esistenti sono elencate a sinistra, tra cui `global` cartella.

1. Fai clic su **Crea**.
1. In **Crea configurazione** è necessario configurare i campi seguenti nella finestra di dialogo:

   * **Titolo**: Fornire un titolo per la cartella di configurazione
   * **Modelli modificabili**: Selezione di modelli modificabili all’interno della cartella

1. Fai clic su **Crea**

>[!NOTE]
>
>In [Browser di configurazione,](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) puoi modificare la cartella globale e attivare la **Modelli modificabili** se desideri creare modelli all’interno di questa cartella, tuttavia questa non è la best practice consigliata.

### ACL e gruppi {#acls-and-groups}

Una volta create le cartelle dei modelli (tramite CRXDE o con il browser di configurazione), le ACL devono essere definite per i gruppi appropriati per le cartelle dei modelli per garantire la corretta sicurezza.

Le cartelle di modelli per [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) può essere utilizzato come esempio.

#### Gruppo autori modelli {#the-template-authors-group}

La `template-authors` gruppo è il gruppo utilizzato per gestire l’accesso ai modelli ed è standard con AEM, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>La `template-authors` Il gruppo è destinato solo agli utenti che devono essere in grado di creare nuovi modelli.
>
>La modifica dei modelli è molto potente e, se non viene eseguita correttamente, i modelli esistenti possono essere interrotti. Pertanto questo ruolo dovrebbe essere concentrato e includere solo gli utenti qualificati.

Nella tabella seguente sono descritte le autorizzazioni necessarie per la modifica dei modelli.

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
   <td>leggere, scrivere, replicare</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in siti specifici <code>/conf</code> spazio</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>read</td>
   <td>Utente web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Gli autori replicateContent devono attivare i modelli di una pagina quando si attiva una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leggere, scrivere, replicare</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in siti specifici <code>/conf</code> spazio</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>read</td>
   <td>L'utente web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i criteri di un modello di pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autore del modello</td>
   <td>read</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti.</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

Questa impostazione predefinita `template-authors` il gruppo copre solo le impostazioni del progetto, dove tutte `template-authors` i membri possono accedere e creare tutti i modelli. Per configurazioni più complesse, in cui sono necessari gruppi di autori di modelli multipli per separare l’accesso ai modelli, è necessario creare gruppi di autori di modelli più personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori dei modelli rimarrebbero invariate.

## Tipo di modello {#template-type}

Quando si crea un nuovo modello, è necessario specificare un tipo di modello:

* I tipi di modello forniscono efficacemente i modelli per un modello. Quando si crea un nuovo modello, la struttura e il contenuto iniziale del tipo di modello selezionato vengono utilizzati per creare il nuovo modello.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta effettuata la copia, l’unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Il tipo di risorsa del componente pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell’editor modelli.
   * È consigliabile definire i punti di interruzione per la griglia reattiva e la configurazione dell’emulatore mobile in sul tipo di modello.

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina di HTML5 e Pagina modulo adattivo.

   * Altri esempi sono forniti come parte del [Esercitazione WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* I tipi di modello sono generalmente definiti dagli sviluppatori.

I tipi di modelli predefiniti sono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non devi cambiare nulla nel `/libs` percorso. Questo perché il contenuto di `/libs` può essere sovrascritto in qualsiasi momento da un aggiornamento a AEM.

I tipi di modelli specifici per il sito devono essere memorizzati nel percorso comparabile di:

* `/apps/settings/wcm/template-types`

Le definizioni dei tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (consigliato) o in alternativa in `global`. Ad esempio:

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

Se hai creato un modello che può fungere da base per altri modelli, puoi copiarlo come tipo di modello.

1. Crea un modello come faresti con un modello di pagina [come documentato qui](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), che fungerà da base per il tipo di modello.
1. Utilizzando CRXDE Lite, copia il modello appena creato dal `templates` al nodo `template-types` sotto il nodo [cartella dei modelli](#template-folders).
1. Elimina il modello dal `templates` sotto il nodo [cartella dei modelli](#template-folders).
1. Nella copia del modello che si trova sotto il `template-types` nodo, elimina tutto `cq:template` e `cq:templateType` `jcr:content` proprietà.

Puoi anche sviluppare un tipo di modello personalizzato utilizzando un modello modificabile di esempio come base, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-sites-example-custom-template-type su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definizioni dei modelli {#template-definitions}

Vengono memorizzate le definizioni dei modelli modificabili [cartelle definite dall&#39;utente](#template-folders) (consigliato) o in alternativa in `global`. Ad esempio:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Il nodo principale del modello è di tipo `cq:Template` con struttura ossea di:

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

Questo nodo contiene le proprietà del modello:

* **Nome**: `jcr:title`
* **Nome**: `status`
   * ``**Tipo**: `String`
   * **Valore**: `draft`, `enabled` o `disabled`

### Struttura {#structure}

Definisce la struttura della pagina risultante:

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una nuova pagina.
* Le modifiche apportate alla struttura verranno applicate a tutte le pagine create con il modello.
* La `root` ( `structure/jcr:content/root`Il nodo ) definisce l’elenco dei componenti che saranno disponibili nella pagina risultante.
   * I componenti definiti nella struttura del modello non possono essere spostati o eliminati dalle pagine risultanti.
   * Quando un componente viene sbloccato, la `editable` è impostata su `true`.
   * Quando un componente che contiene già è sbloccato, il contenuto viene spostato in `initial` ramo.

* La `cq:responsive` node contiene le definizioni del layout dinamico.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un `jcr:content` che viene copiato in una nuova pagina.
* È unito alla struttura ( `/structure`) durante la creazione di una nuova pagina.
* Eventuali pagine esistenti non verranno aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* La `root` node contiene un elenco di componenti per definire cosa sarà disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e successivamente viene sbloccato (o viceversa), viene utilizzato come contenuto iniziale.

### Layout {#layout}

Quando [modifica di un modello da definire](/help/sites-cloud/authoring/features/templates.md), utilizza [layout dinamico standard](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Criteri di contenuto {#content-policies}

I criteri dei contenuti definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello). I criteri del contenuto possono essere creati e selezionati nell’editor modelli.

* La proprietà `cq:policy`, sul `root` nodo
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, sui nodi espliciti del componente sotto `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

### Criteri di pagina {#page-policies}

I criteri di pagina consentono di definire [informativa sui contenuti](#content-policies) per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e autorizzazione di un modello per l’uso {#enabling-and-allowing-a-template-for-use}

1. **Attiva il modello**

   Prima di poter utilizzare un modello, è necessario attivarlo tramite:

   * [Abilitazione del modello](/help/sites-cloud/authoring/features/templates.md) dal **Modelli** console.

   * Impostazione della proprietà di stato nel `jcr:content` nodo.

      * Ad esempio, su:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definisci la proprietà:

         * Nome: status
         * Tipo: Stringa
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definisci i percorsi dei modelli consentiti nel **Proprietà pagina**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) della pagina o della pagina principale appropriata di un ramo secondario.
   * Imposta la proprietà:
      `cq:allowedTemplates`
Sulla 
`jcr:content` nodo del ramo richiesto.
   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine dei contenuti risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Sono create con una sottostruttura da cui è stata eseguita l’unione `structure` e `initial` nel modello

* Avere riferimenti alle informazioni contenute nel modello e nel tipo di modello. Ciò è possibile con un `jcr:content` nodo con le proprietà:

   * `cq:template` - Fornisce il riferimento dinamico al modello effettivo; consente di visualizzare le modifiche apportate al modello nelle pagine effettive.

   * `cq:templateType` - Fornisce un riferimento al tipo di modello.

![Interrelazione tra modelli, contenuti e componenti](assets/templates-content-components.png)

Il diagramma precedente mostra come i modelli, i contenuti e i componenti si rapportano:

* Controller - `/content/<my-site>/<my-page>` - La pagina risultante che fa riferimento al modello. Il contenuto controlla l’intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.
* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [criteri di contenuto e modelli correlati](#template-definitions) definisci la configurazione della pagina.
* Modello - Bundle OSGi - Il [Bundle OSGI](/help/implementing/deploying/configuring-osgi.md) implementa la funzionalità .
* Visualizza - `/apps/<my-site>/components` - Negli ambienti di authoring e di pubblicazione il rendering del contenuto viene eseguito dai componenti.

Durante il rendering di una pagina:

* **Modelli**:

   * La `cq:template` proprietà `jcr:content` verrà fatto riferimento al nodo per accedere al modello corrispondente a tale pagina.

* **Componenti**:

   * Il componente pagina unisce il `structure/jcr:content` struttura del modello con `jcr:content` struttura della pagina.
      * Il componente pagina consente solo all’autore di modificare i nodi della struttura del modello che sono stati contrassegnati come modificabili (così come altri elementi secondari).
      * Quando si esegue il rendering di un componente su una pagina, il percorso relativo di tale componente viene ricavato dal `jcr:content` nodo; lo stesso percorso `policies/jcr:content` Viene quindi eseguita la ricerca nel nodo del modello.
         * La `cq:policy` di questo nodo fa riferimento al criterio del contenuto effettivo (ovvero contiene la configurazione di progettazione per quel componente).
            * Questo consente di avere più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.

### Disponibilità dei modelli {#template-availability}

Quando crei una nuova pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni di posizionamento specificate in ciascun modello.

Le proprietà seguenti determinano se un modello `T` può essere utilizzato per inserire una nuova pagina come pagina figlia di `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* La `cq:allowedTemplates` proprietà `jcr:content` sottonodo di `P` o un antenato di `P`.

* La `allowedPaths` proprietà di `T`.

* La `allowedParents` proprietà di `T`.

* La `allowedChildren` proprietà del modello di `P`.

La valutazione funziona come segue:

* Il primo non vuoto `cq:allowedTemplates` trovato durante l&#39;ascesa della gerarchia di pagina che inizia con `P` viene confrontato con il percorso di `T`. Se nessuno dei valori corrisponde, `T` è rifiutato.

* Se `T` non è vuoto `allowedPaths` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` è rifiutato a meno che non appartenga alla stessa domanda `P`. `T` appartiene alla stessa applicazione `P` se e solo se il nome del secondo livello del percorso `T` è lo stesso del nome del secondo livello del percorso `P`. Ad esempio, il modello `/apps/wknd/templates/foo` appartiene alla stessa applicazione della pagina `/content/wknd`.

* Se `T` non è vuoto `allowedParents` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è rifiutato.

* Se il modello di `P` non è vuoto `allowedChildren` , ma nessuno dei valori corrisponde al percorso di `T`, `T` è rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione del modello:

![Processo di valutazione dei modelli](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, combinarle può portare a regole molto complesse che sono difficili da monitorare e gestire.
>
>Pertanto, Adobe consiglia di iniziare con semplicità, definendo:
>
>* solo il `cq:allowedTemplates` property
>
>* solo nella directory principale del sito
>
>Ad esempio, consulta [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) contenuto: `/content/wknd/jcr:content`
>
>Proprietà `allowedPaths`, `allowedParents`e `allowedChildren` può anche essere posizionato sui modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice da definire `cq:allowedTemplates` nelle sottosezioni del sito se è necessario limitare ulteriormente i modelli consentiti.
>
>Un vantaggio aggiuntivo è rappresentato dal `cq:allowedTemplates` le proprietà possono essere aggiornate da un autore nel **Avanzate** della scheda **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l’interfaccia utente (standard), pertanto per ogni modifica sarebbe necessario uno sviluppatore per mantenere le regole e una distribuzione del codice.

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli che possono essere utilizzati per creare pagine figlie sotto una determinata pagina, utilizza la funzione `cq:allowedTemplates` proprietà di `jcr:content` nodo della pagina per specificare l’elenco di modelli da consentire come pagine figlie. Ogni valore nell’elenco deve essere un percorso assoluto a un modello per una pagina figlio consentita, ad esempio `/apps/wknd/templates/page-content`.

È possibile utilizzare `cq:allowedTemplates` nella proprietà del modello  `jcr:content` per applicare questa configurazione a tutte le pagine appena create che utilizzano questo modello.

Se desideri aggiungere altri vincoli, ad esempio per quanto riguarda la gerarchia dei modelli, puoi utilizzare la funzione `allowedParents/allowedChildren` nel modello. È quindi possibile specificare esplicitamente che le pagine create da un modello T devono essere padre/figlio di pagine create da un modello T.
