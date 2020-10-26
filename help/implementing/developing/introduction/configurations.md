---
title: Configurazioni e browser di configurazione
description: Comprendere AEM configurazioni e come gestiscono le impostazioni dell'area di lavoro in AEM.
translation-type: tm+mt
source-git-commit: 47d2ff211b5c00457793dc7bd321df1139cfc327
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# Configurazioni e browser di configurazione {#configuration-browser}

AEM configurazioni servono a gestire le impostazioni in AEM e fungono da aree di lavoro.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Una configurazione può essere considerata da due diversi punti di vista.

* [Un amministratore](#configurations-administrator) utilizza le configurazioni come aree di lavoro all’interno AEM per definire e gestire i gruppi di impostazioni.
* [Uno sviluppatore](#configurations-developer) utilizza il meccanismo di configurazione sottostante che implementa le configurazioni per mantenere e cercare le impostazioni in AEM.

In sintesi: dal punto di vista dell&#39;amministratore, le configurazioni sono il modo in cui si creano le aree di lavoro per gestire le impostazioni in AEM, mentre lo sviluppatore deve comprendere come AEM utilizza e gestisce tali configurazioni all&#39;interno del repository.

Indipendentemente dal vostro punto di vista, le configurazioni servono a due scopi principali in AEM:

* Le configurazioni attivano alcune funzioni per alcuni gruppi di utenti.
* Le configurazioni definiscono i diritti di accesso per tali funzioni.

## Configurazioni come amministratore {#configurations-administrator}

Sia l’amministratore AEM che gli autori possono considerare le configurazioni come aree di lavoro. Tali aree di lavoro possono essere utilizzate per raccogliere insieme gruppi di impostazioni e il relativo contenuto a scopo organizzativo, implementando i diritti di accesso per tali funzioni.

Le configurazioni possono essere create per molte funzioni diverse all&#39;interno di AEM.

* [Configurazioni cloud](/help/implementing/developing/introduction/configurations.md)
* [Segmenti di Context Hub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Modelli modificabili](/help/sites-cloud/authoring/features/templates.md)

### Esempio {#administrator-example}

Ad esempio, un amministratore può creare due configurazioni per Modelli modificabili.

* WKND - Generale
* WKND-Magazine

L’amministratore può quindi creare modelli di pagina generali utilizzando la configurazione WKND-General e quindi modelli specifici per la rivista sotto WKND-Magazine.

L’amministratore può quindi associare il WKND-General a tutto il contenuto del sito WKND. Tuttavia, la configurazione WKND-Magazine sarebbe associata solo al sito della rivista.

In questo modo:

* Quando un autore crea una nuova pagina per la rivista, può scegliere tra modelli generali (WKND-General) o modelli di rivista (WKND-Magazine).
* Quando un autore crea una nuova pagina per un’altra parte del sito che non è la rivista, può scegliere solo tra i modelli generali (WKND-General).

Impostazioni simili sono possibili non solo per i modelli modificabili, ma anche per le configurazioni cloud, i segmenti ContextHub e i modelli di frammenti di contenuto.

### Utilizzo del browser di configurazione {#using-configuration-browser}

Il Browser di configurazione consente agli amministratori di creare, gestire e configurare facilmente i diritti di accesso alle configurazioni in AEM.

>[!NOTE]
>
>È possibile creare configurazioni utilizzando il browser di configurazione solo se l&#39;utente dispone di `admin` diritti. `admin` sono inoltre necessari per assegnare diritti di accesso alla configurazione o per modificare in altro modo una configurazione.

#### Creating a Configuration {#creating-a-configuration}

È molto semplice creare una nuova configurazione in AEM utilizzando il browser di configurazione.

1. Accedete AEM come Cloud Service e dal menu principale selezionate **Strumenti** -> **Generali** -> **Browser** di configurazione.
1. Tocca o fai clic su **Crea**.
1. Specificate un **Titolo** e un **Nome** per la configurazione.

   ![Creare la configurazione](assets/configuration-create.png)

   * Il **Titolo** deve essere descrittivo.
   * Il **Nome** diventerà il nome del nodo nella directory archivio.
      * Verrà generato automaticamente in base al titolo e verrà modificato in base alle convenzioni di denominazione [AEM.](naming-conventions.md)
      * Può essere regolato se necessario.
1. Verificare il tipo di configurazioni che si desidera consentire.
   * [Configurazioni cloud](/help/implementing/developing/introduction/configurations.md)
   * [Segmenti di Context Hub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
   * [Modelli modificabili](/help/sites-cloud/authoring/features/templates.md)
1. Tocca o fai clic su **Crea**.

>[!TIP]
>
>Le configurazioni possono essere nidificate.

#### Modifica delle configurazioni e relativi diritti di accesso {#access-rights}

Se si considerano le configurazioni come aree di lavoro, è possibile impostare i diritti di accesso su tali configurazioni per applicare a chi potrebbero accedere o meno tali aree di lavoro.

1. Accedete AEM come Cloud Service e dal menu principale selezionate **Strumenti** -> **Generali** -> **Browser** di configurazione.
1. Selezionate la configurazione da modificare, quindi toccate o fate clic su **Proprietà** nella barra degli strumenti.
1. Selezionare le funzioni aggiuntive da aggiungere alla configurazione
   >[!NOTE]
   >
   >Non è possibile deselezionare una funzione dopo la creazione della configurazione.
1. Utilizzate il pulsante Autorizzazioni **** effettive per visualizzare una matrice di ruoli e le autorizzazioni che sono attualmente concesse alle configurazioni.
   ![Finestra delle autorizzazioni effettive](assets/configuration-effective-permissions.png)
1. Per assegnare nuove autorizzazioni, immettete il nome utente o del gruppo nel campo **Seleziona utente o gruppo** nella sezione **Aggiungi nuove autorizzazioni** .
   * Il campo **Seleziona utente o gruppo** offre il completamento automatico in base agli utenti e ai ruoli esistenti.
1. Selezionate l’utente o il ruolo appropriato dai risultati di completamento automatico.
   * Potete selezionare più utenti o ruoli.
1. Verificare le opzioni di accesso che devono avere gli utenti o i ruoli selezionati e fare clic su **Aggiungi**.
   ![Aggiunta di diritti di accesso a una configurazione](assets/configuration-edit.png)
1. Ripetete i passaggi per selezionare utenti o ruoli e assegnare diritti di accesso aggiuntivi, a seconda delle necessità.
1. Toccate o fate clic su **Salva e chiudi** al termine.

## Configurazioni come sviluppatore {#configurations-developer}

In qualità di sviluppatore, è importante sapere come AEM come Cloud Service funziona con le configurazioni e come elabora la risoluzione della configurazione.

### Separazione di configurazione e contenuto {#separation-of-config-and-content}

Sebbene l&#39; [amministratore e gli utenti possano considerare le configurazioni come luoghi](#configurations-administrator) di lavoro per gestire diverse impostazioni e contenuti, è importante comprendere che le configurazioni e i contenuti sono memorizzati e gestiti separatamente da AEM nella directory archivio.

* `/content` è la pagina principale di tutti i contenuti.
* `/conf` è la casa di tutte le configurazioni.

Il contenuto fa riferimento alla configurazione associata tramite una `cq:conf` proprietà. AEM eseguire una ricerca in base al contenuto ed è una `cq:conf` proprietà contestuale per trovare la configurazione appropriata.

### Esempio {#developer-example}

Per questo esempio, supponiamo che tu abbia del codice applicativo interessato alle impostazioni DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

Il punto di partenza di tutte le ricerche di configurazione è una risorsa di contenuto, in genere da qualche parte sotto `/content`. Può trattarsi di una pagina, di un componente all’interno di una pagina, di una risorsa o di una cartella DAM. Questo è il contenuto effettivo per il quale stiamo cercando la configurazione giusta che si applica in questo contesto.

Ora con l&#39; `Conf` oggetto in mano, possiamo recuperare l&#39;elemento di configurazione specifico a cui siamo interessati. In questo caso è `dam/imageserver`, ovvero una raccolta di impostazioni relative al `imageserver`. La `getItem` chiamata restituisce un `ValueMap`. Quindi si legge una proprietà `bgkcolor` stringa e si fornisce il valore predefinito &quot;FFFFFF&quot; nel caso in cui la proprietà (o l&#39;intero elemento di configurazione) non sia presente.

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

In questo esempio, si presuppone una cartella DAM specifica per WKND e una configurazione corrispondente. A partire da tale cartella `/content/dam/wknd`, verrà visualizzata una proprietà stringa denominata `cq:conf` che fa riferimento alla configurazione da applicare alla struttura secondaria. La proprietà viene in genere impostata sulla `jcr:content` cartella di una risorsa o pagina. Questi `conf` collegamenti sono espliciti, quindi è facile seguirli semplicemente guardando il contenuto in CRXDE.

Saltando dentro `/conf`, seguiamo il riferimento e vediamo che c&#39;è un `/conf/wknd` nodo. Questa è una configurazione. La ricerca è completamente trasparente per il codice dell&#39;applicazione. Il codice di esempio non ha mai un riferimento dedicato ad esso, è nascosto dietro l&#39; `Conf` oggetto. La configurazione applicata è completamente controllata attraverso il contenuto JCR.

Vediamo che la configurazione contiene un nodo con nome fisso `settings` che contiene gli elementi effettivi, incluso il `dam/imageserver` nostro caso. Tale elemento può essere considerato come un &quot;documento delle impostazioni&quot; ed è in genere rappresentato da un `cq:Page` incluso un `jcr:content` contenuto effettivo.

Infine, vediamo la proprietà `bgkcolor` che il nostro codice di esempio ha bisogno. Il `ValueMap` ritorno da `getItem` è basato sul `jcr:content` nodo della pagina.

### Risoluzione della configurazione {#configuration-resolution}

L&#39;esempio di base sopra mostrava una singola configurazione. Ma ci sono molti casi in cui si desidera avere configurazioni diverse, come una configurazione globale predefinita, una diversa per ogni marchio e forse una specifica per i sottoprogetti.

Per supportare questo, la ricerca di configurazione in AEM ha meccanismi di ereditarietà e fallback nell&#39;ordine di preferenza seguente:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configurazione specifica a cui si fa riferimento da `cq:conf` qualche parte in `/content`
   * La gerarchia è arbitraria e può essere progettata proprio come la struttura del sito, non è compito del codice applicazione sapere questo
   * Modificabile in fase di esecuzione dagli utenti con privilegi di configurazione
1. `/conf/<siteconfig>/<parentconfig>`
   * Traversare i genitori per le configurazioni di fallback
   * Modificabile in fase di esecuzione dagli utenti con privilegi di configurazione
1. `/conf/<siteconfig>`
   * Traversare i genitori per le configurazioni di fallback
   * Modificabile in fase di esecuzione dagli utenti con privilegi di configurazione
1. `/conf/global`
   * Impostazioni globali del sistema
   * Generalmente, impostazioni predefinite globali per l’installazione
   * Impostato da un `admin` ruolo
   * Modificabile in fase di esecuzione dagli utenti con privilegi di configurazione
1. `/apps`
   * Impostazioni predefinite applicazione
   * Problema risolto con la distribuzione dell’applicazione
   * Sola lettura in fase di esecuzione
1. `/libs`
   * AEM predefiniti del prodotto
   * Modificabile solo da  Adobe, accesso al progetto non consentito
   * Problema risolto con la distribuzione dell’applicazione
   * Sola lettura in fase di esecuzione

### Utilizzo delle configurazioni {#using-configurations}

Le configurazioni in AEM si basano sulle configurazioni Sling Context-Aware. I bundle Sling forniscono un&#39;API di servizio che può essere utilizzata per ottenere configurazioni basate sul contesto. Le configurazioni basate sul contesto sono configurazioni correlate a una risorsa di contenuto o a una struttura di risorse, come [descritto nell’esempio precedente.](#developer-example)

Per ulteriori dettagli sulle configurazioni, gli esempi e le modalità di utilizzo in base al contesto, [consulta la documentazione Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### Console Web ConfMgr {#confmgr-web-console}

A scopo di debug e test, è disponibile una console Web **ConfMgr** in `https://<host>:<port>/system/console/conf`, che può mostrare le configurazioni per un determinato percorso/elemento.

![ConfMgr](assets/configuration-confmgr.png)

È sufficiente fornire:

* **Percorso contenuto**
* **Elemento**
* **User**

Fate clic su **Risolvi** per vedere quali configurazioni vengono risolte e ricevere il codice di esempio che risolverà tali configurazioni.

### Console Web di configurazione in base al contesto {#context-aware-web-console}

A scopo di debug e test, è disponibile una console Web di configurazione **in base al** contesto all&#39;indirizzo `https://<host>:<port>/system/console/slingcaconfig`, che consente di eseguire query sulle configurazioni in base al contesto nell&#39;archivio e di visualizzarne le proprietà.

![Console Web di configurazione in base al contesto](assets/configuration-context-aware-console.png)

È sufficiente fornire:

* **Percorso contenuto**
* **Nome configurazione**

Fate clic su **Risolvi** per recuperare i percorsi contestuali e le proprietà associati per la configurazione selezionata.
