---
title: Configurazioni e browser di configurazione
description: Comprendi le configurazioni AEM e come gestiscono le impostazioni dell’area di lavoro in AEM.
source-git-commit: 4892f644929bc308762ca4fb8a2ebfb85e5fb5e2
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 2%

---


# Configurazioni e browser di configurazione {#configuration-browser}

Le configurazioni AEM servono a gestire le impostazioni in AEM e fungono da aree di lavoro.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Una configurazione può essere considerata da due diversi punti di vista.

* [Un ](#configurations-administrator) amministratore utilizza le configurazioni come aree di lavoro all’interno di AEM per definire e gestire gruppi di impostazioni.
* [Uno ](#configurations-developer) sviluppatore utilizza il meccanismo di configurazione sottostante che implementa le configurazioni per mantenere e cercare le impostazioni in AEM.

In sintesi: dal punto di vista di un amministratore, le configurazioni sono il modo in cui si creano le aree di lavoro per gestire le impostazioni in AEM, mentre lo sviluppatore deve comprendere come AEM utilizza e gestisce queste configurazioni all&#39;interno dell&#39;archivio.

Indipendentemente dal tuo punto di vista, le configurazioni hanno due scopi principali in AEM:

* Le configurazioni abilitano alcune funzioni per determinati gruppi di utenti.
* Le configurazioni definiscono i diritti di accesso per tali funzionalità.

## Configurazioni come amministratore {#configurations-administrator}

L’amministratore AEM e gli autori possono considerare le configurazioni come aree di lavoro. Queste aree di lavoro possono essere utilizzate per raccogliere insieme gruppi di impostazioni e il relativo contenuto associato a scopo organizzativo, implementando i diritti di accesso per tali funzioni.

È possibile creare configurazioni per molte funzioni diverse all’interno di AEM.

* [Segmenti Context Hub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Modelli modificabili](/help/sites-cloud/authoring/features/templates.md)
* varie configurazioni cloud

### Esempio {#administrator-example}

Ad esempio, un amministratore può creare due configurazioni per Modelli modificabili.

* WKND Generale
* WKND-Magazine

L’amministratore può quindi creare modelli di pagina generali utilizzando la configurazione WKND-General e quindi modelli specifici per la rivista sotto WKND-Magazine.

L’amministratore può quindi associare il WKND-General a tutti i contenuti del sito WKND. Tuttavia, la configurazione WKND-Magazine verrebbe associata solo al sito della rivista.

Facendo questo:

* Quando un autore crea una nuova pagina per la rivista, può scegliere tra modelli generali (WKND-General) o modelli di rivista (WKND-Magazine).
* Quando un autore crea una nuova pagina per un’altra parte del sito che non è la rivista, l’autore può scegliere solo tra i modelli generali (WKND-General).

Impostazioni simili sono possibili non solo per i modelli modificabili, ma anche per le configurazioni cloud, i segmenti ContextHub e i modelli di frammenti di contenuto.

### Utilizzo del browser di configurazione {#using-configuration-browser}

Il Browser configurazioni consente a un amministratore di creare, gestire e configurare facilmente i diritti di accesso alle configurazioni in AEM.

>[!NOTE]
>
>È possibile creare configurazioni utilizzando il Browser configurazioni solo se l&#39;utente dispone di diritti `admin`. `admin` sono inoltre necessari diritti per assegnare diritti di accesso alla configurazione o modificare in altro modo una configurazione.

#### Creazione di una configurazione {#creating-a-configuration}

È molto semplice creare una nuova configurazione in AEM utilizzando il Browser configurazioni.

1. Accedi a AEM come Cloud Service e dal menu principale seleziona **Strumenti** -> **Generale** -> **Browser configurazioni**.
1. Tocca o fai clic su **Crea**.
1. Specifica un **titolo** e un **nome** per la configurazione.

   ![Creare la configurazione](assets/configuration-create.png)

   * Il **Titolo** deve essere descrittivo.
   * Il **Nome** diventerà il nome del nodo nel repository.
      * Verrà generato automaticamente in base al titolo e verrà regolato in base alle convenzioni di denominazione [AEM.](naming-conventions.md)
      * Può essere regolato se necessario.
1. Controlla il tipo di configurazioni che desideri consentire.
   * [Segmenti Context Hub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
   * [Modelli modificabili](/help/sites-cloud/authoring/features/templates.md)
   * varie configurazioni cloud
1. Tocca o fai clic su **Crea**.

>[!TIP]
>
>Le configurazioni possono essere nidificate.

#### Modifica delle configurazioni e relativi diritti di accesso {#access-rights}

Se si considerano le configurazioni come aree di lavoro, è possibile impostare i diritti di accesso a tali configurazioni in modo da imporre a chi può accedere o meno a tali aree di lavoro.

1. Accedi a AEM come Cloud Service e dal menu principale seleziona **Strumenti** -> **Generale** -> **Browser configurazioni**.
1. Seleziona la configurazione da modificare, quindi tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Seleziona le funzionalità aggiuntive da aggiungere alla configurazione
   >[!NOTE]
   >
   >Non è possibile deselezionare una funzione una volta creata la configurazione.
1. Utilizza il pulsante **Autorizzazioni effettive** per visualizzare una matrice di ruoli e quali autorizzazioni sono attualmente concesse alle configurazioni.
   ![Finestra delle autorizzazioni valide](assets/configuration-effective-permissions.png)
1. Per assegnare nuove autorizzazioni, immetti il nome utente o del gruppo nel campo **Seleziona utente o gruppo** nella sezione **Aggiungi nuove autorizzazioni**.
   * Il campo **Seleziona utente o gruppo** offre il completamento automatico in base agli utenti e ai ruoli esistenti.
1. Seleziona l’utente o il ruolo appropriato dai risultati di completamento automatico.
   * È possibile selezionare più utenti o ruoli.
1. Controlla le opzioni di accesso che gli utenti o i ruoli selezionati devono avere e fai clic su **Aggiungi**.
   ![Aggiungere diritti di accesso a una configurazione](assets/configuration-edit.png)
1. Ripeti i passaggi per selezionare utenti o ruoli e assegnare eventuali diritti di accesso aggiuntivi.
1. Al termine, tocca o fai clic su **Salva e chiudi** .

## Configurazioni come sviluppatore {#configurations-developer}

In qualità di sviluppatore, è importante sapere come AEM un Cloud Service funziona con le configurazioni e come elabora la risoluzione della configurazione.

### Separazione della configurazione e del contenuto {#separation-of-config-and-content}

Anche se l’ [amministratore e gli utenti possono considerare le configurazioni come luoghi di lavoro](#configurations-administrator) per gestire diverse impostazioni e contenuti, è importante comprendere che le configurazioni e il contenuto sono memorizzati e gestiti separatamente da AEM nell’archivio.

* `/content` è la sede di tutti i contenuti.
* `/conf` è la pagina principale di tutte le configurazioni.

Il contenuto fa riferimento alla configurazione associata tramite una proprietà `cq:conf` . AEM esegue una ricerca in base al contenuto ed è una proprietà contestuale `cq:conf` per trovare la configurazione appropriata.

### Esempio {#developer-example}

Per questo esempio, supponiamo che tu disponga di un codice applicazione interessato alle impostazioni DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

Il punto di partenza di tutte le ricerche di configurazione è una risorsa di contenuto, in genere compresa in `/content`. Può trattarsi di una pagina, di un componente all’interno di una pagina, di una risorsa o di una cartella DAM. Questo è il contenuto effettivo per il quale stiamo cercando la configurazione corretta che si applica in questo contesto.

Ora con l&#39;oggetto `Conf` in mano, possiamo recuperare l&#39;elemento di configurazione specifico a cui siamo interessati. In questo caso è `dam/imageserver`, che è una raccolta di impostazioni relative al `imageserver`. La chiamata `getItem` restituisce un valore `ValueMap`. Quindi leggiamo una proprietà stringa `bgkcolor` e forniamo un valore predefinito di &quot;FFFF&quot; nel caso in cui la proprietà (o l&#39;intero elemento di configurazione) non sia presente.

Ora diamo un&#39;occhiata al contenuto JCR corrispondente:

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

In questo esempio, si presuppone una cartella DAM specifica WKND qui e una configurazione corrispondente. A partire da tale cartella `/content/dam/wknd`, viene visualizzata una proprietà stringa denominata `cq:conf` che fa riferimento alla configurazione da applicare alla sottostruttura. La proprietà viene in genere impostata su `jcr:content` di una cartella di risorse o di una pagina. Questi collegamenti `conf` sono espliciti, quindi è facile seguirli semplicemente guardando il contenuto in CRXDE.

Saltando all&#39;interno di `/conf`, seguiamo il riferimento e vediamo che c&#39;è un nodo `/conf/wknd`. Questa è una configurazione. Tieni presente che la ricerca è completamente trasparente per il codice dell’applicazione. Il codice di esempio non ha mai un riferimento dedicato ad esso, è nascosto dietro l&#39;oggetto `Conf` . La configurazione applicata è completamente controllata attraverso il contenuto JCR.

Vediamo che la configurazione contiene un nodo `settings` con nome fisso che contiene gli elementi effettivi, incluso il `dam/imageserver` di cui abbiamo bisogno nel nostro caso. Tale elemento può essere considerato come un &quot;documento delle impostazioni&quot; ed è solitamente rappresentato da un `cq:Page` che include un `jcr:content` contenente il contenuto effettivo.

Infine, vediamo la proprietà `bgkcolor` necessaria per il nostro codice di esempio. Il `ValueMap` che recuperiamo da `getItem` è basato sul nodo `jcr:content` della pagina.

### Risoluzione della configurazione {#configuration-resolution}

L&#39;esempio di base sopra mostrava una singola configurazione. Ma ci sono molti casi in cui vuoi avere configurazioni diverse, come una configurazione globale predefinita, una diversa per ogni marchio e forse una specifica per i tuoi sottoprogetti.

Per supportare questo, la ricerca di configurazione in AEM dispone di un meccanismo di ereditarietà e fallback nell’ordine di preferenza seguente:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configurazione specifica a cui si fa riferimento da `cq:conf` in un punto qualsiasi di `/content`
   * La gerarchia è arbitraria e può essere progettata proprio come la struttura del sito, non è compito del codice dell&#39;applicazione sapere questo
   * Modificabile in fase di esecuzione da parte degli utenti con privilegi di configurazione
1. `/conf/<siteconfig>/<parentconfig>`
   * Genitori ambulanti per configurazioni di fallback
   * Modificabile in fase di esecuzione da parte degli utenti con privilegi di configurazione
1. `/conf/<siteconfig>`
   * Genitori ambulanti per configurazioni di fallback
   * Modificabile in fase di esecuzione da parte degli utenti con privilegi di configurazione
1. `/conf/global`
   * Impostazioni globali del sistema
   * Valori predefiniti globali di solito per l&#39;installazione
   * Impostato da un ruolo `admin`
   * Modificabile in fase di esecuzione da parte degli utenti con privilegi di configurazione
1. `/apps`
   * Valori predefiniti dell&#39;applicazione
   * Risolto con l’implementazione dell’applicazione
   * Sola lettura in fase di runtime
1. `/libs`
   * Valori predefiniti del prodotto AEM
   * Solo modificabile dall’Adobe, accesso al progetto non consentito
   * Risolto con l’implementazione dell’applicazione
   * Sola lettura in fase di runtime

### Utilizzo delle configurazioni {#using-configurations}

Le configurazioni in AEM si basano su configurazioni in base al contesto Sling. I bundle Sling forniscono un&#39;API di servizio che può essere utilizzata per ottenere configurazioni basate sul contesto. Le configurazioni in base al contesto sono configurazioni correlate a una risorsa di contenuto o a una struttura di risorse come descritto in [nell&#39;esempio precedente.](#developer-example)

Per ulteriori dettagli sulle configurazioni in base al contesto, sugli esempi e su come utilizzarle, [consulta la documentazione Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### Console Web ConfMgr {#confmgr-web-console}

A scopo di debug e test, esiste una console Web **ConfMgr** in `https://<host>:<port>/system/console/conf` che può mostrare le configurazioni per un determinato percorso/elemento.

![ConfMgr](assets/configuration-confmgr.png)

Fornisci semplicemente:

* **Percorso contenuto**
* **Elemento**
* **User**

Fai clic su **Risolvi** per vedere quali configurazioni vengono risolte e ricevere il codice di esempio che risolverà tali configurazioni.

### Console Web di configurazione in base al contesto {#context-aware-web-console}

A scopo di debug e test, è disponibile una console Web **Configurazione in base al contesto** all&#39;indirizzo `https://<host>:<port>/system/console/slingcaconfig` che consente di eseguire query sulle configurazioni in base al contesto nell&#39;archivio e di visualizzarne le proprietà.

![Console web di configurazione in base al contesto](assets/configuration-context-aware-console.png)

Fornisci semplicemente:

* **Percorso contenuto**
* **Nome configurazione**

Fai clic su **Risolvi** per recuperare i percorsi e le proprietà contestuali associati alla configurazione selezionata.
