---
title: Estensione di Multi Site Manager
description: Scopri come estendere le funzionalità di Multi Site Manager.
exl-id: 4b7a23c3-65d1-4784-9dea-32fcceca37d1
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2337'
ht-degree: 0%

---

# Estensione di Multi Site Manager {#extending-the-multi-site-manager}

Questo documento spiega come estendere le funzionalità di Multi Site Manager e tratta i seguenti argomenti.

* Scopri i membri principali dell’API Java MSM
* Crea una nuova azione di sincronizzazione che può essere utilizzata in una configurazione di rollout
* Modificare la lingua e i codici paese predefiniti

>[!TIP]
>
>Questa pagina è più facilmente compresa nel contesto del documento [Riutilizzo del contenuto: Multi Site Manager](/help/sites-cloud/administering/msm/overview.md).

>[!CAUTION]
>
>Multi Site Manager e le relative API vengono utilizzati per la creazione di un sito Web e, come tali, sono destinati solo all’utilizzo in un ambiente di authoring.

## Panoramica dell’API Java {#overview-of-the-java-api}

La gestione multisito è costituita dai seguenti pacchetti:

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

I principali oggetti API MSM interagiscono come segue (vedi anche la sezione [Termini utilizzati](/help/sites-cloud/administering/msm/overview.md#terms-used)):

![Oggetti API MSM principali](assets/msm-api-interaction.png)

* **`Blueprint`** - Un `Blueprint` (come nella [configurazione blueprint](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations)) specifica le pagine da cui una Live Copy può ereditare il contenuto.

  ![Blueprint](assets/msm-blueprint-interaction.png)

   * L&#39;utilizzo di una configurazione blueprint ( `Blueprint`) è facoltativo, ma:

      * Consente all&#39;autore di utilizzare l&#39;opzione **Rollout** nell&#39;origine per inviare in modo esplicito le modifiche alle Live Copy che ereditano da questa origine.
      * Consente all&#39;autore di utilizzare **Crea sito**, che consente all&#39;utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
      * Definisce la configurazione di rollout predefinita per tutte le Live Copy risultanti.

* **`LiveRelationship`** - `LiveRelationship` specifica la connessione (relazione) tra una risorsa nel ramo Live Copy e la relativa risorsa di origine/blueprint equivalente.

   * Le relazioni vengono utilizzate per la realizzazione dell’ereditarietà e del rollout.
   * `LiveRelationship` oggetti forniscono accesso (riferimenti) alle configurazioni di rollout ( `RolloutConfig`), `LiveCopy` e `LiveStatus` oggetti correlati alla relazione.

   * Ad esempio, in `/content/copy/us` viene creata una Live Copy dall&#39;origine/blueprint in `/content/wknd/language-masters`. Le risorse `/content/wknd/language-masters/en/jcr:content` e `/content/copy/us/en/jcr:content` formano una relazione.

* **`LiveCopy`** - Un `LiveCopy` contiene i dettagli di configurazione per le relazioni (`LiveRelationship`) tra le risorse Live Copy e le relative risorse di origine/blueprint.

   * Utilizza la classe `LiveCopy` per accedere al percorso della pagina, al percorso della pagina sorgente/blueprint, alle configurazioni di rollout e per sapere se le pagine figlie sono incluse anche in `LiveCopy`.

   * Viene creato un nodo `LiveCopy` ogni volta che si utilizza **Crea sito** o **Crea Live Copy**.

* **`LiveStatus`** - `LiveStatus` oggetti forniscono accesso allo stato di runtime di un `LiveRelationship`. Utilizza per eseguire una query sullo stato di sincronizzazione di una Live Copy.

* **`LiveAction`** - Un `LiveAction` è un&#39;azione eseguita su ogni risorsa coinvolta nel rollout.

   * `LiveAction` vengono generati solo da `RolloutConfig`.

* **`LiveActionFactory`** - Un `LiveActionFactory` crea `LiveAction` oggetti con una configurazione `LiveAction`. Le configurazioni vengono memorizzate come risorse nell’archivio.

* **`RolloutConfig`** - `RolloutConfig` contiene un elenco di `LiveActions`, da utilizzare quando attivato. `LiveCopy` eredita `RolloutConfig` e il risultato è presente in `LiveRelationship`.

   * Per impostare una Live Copy per la prima volta viene utilizzato anche un `RolloutConfig` (che attiva `LiveAction`).

## Creazione di una nuova azione di sincronizzazione {#creating-a-new-synchronization-action}

Puoi creare azioni di sincronizzazione personalizzate da utilizzare con le configurazioni di rollout. Questo può essere utile quando le [azioni installate](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) non soddisfano i requisiti specifici dell&#39;applicazione.

A tale scopo, crea due classi:

* Implementazione dell&#39;interfaccia [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) che esegue l&#39;azione.
* Componente OSGi che implementa l&#39;interfaccia [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) e crea istanze della classe `LiveAction`

`LiveActionFactory` crea istanze della classe `LiveAction` per una determinata configurazione:

* `LiveAction` classi includono i seguenti metodi:

   * `getName` - Restituisce il nome dell&#39;azione

      * Il nome viene utilizzato per fare riferimento all&#39;azione, ad esempio, nelle configurazioni di rollout.

   * `execute` - Esegue le attività dell&#39;azione

* `LiveActionFactory` classi includono i seguenti membri:

   * `LIVE_ACTION_NAME` - Campo contenente il nome dell&#39;elemento `LiveAction` associato

      * Questo nome deve coincidere con il valore restituito dal metodo `getName` della classe `LiveAction`.

   * `createAction` - Crea un&#39;istanza di `LiveAction`

      * Il parametro facoltativo `Resource` può essere utilizzato per fornire informazioni di configurazione.

   * `createsAction` - Restituisce il nome del `LiveAction` associato

### Accesso al nodo di configurazione LiveAction {#accessing-the-liveaction-configuration-node}

Utilizzare il nodo di configurazione `LiveAction` nell&#39;archivio per memorizzare informazioni che influiscono sul comportamento in fase di esecuzione dell&#39;istanza `LiveAction`. Il nodo nell&#39;archivio che memorizza la configurazione `LiveAction` è disponibile per l&#39;oggetto `LiveActionFactory` in fase di esecuzione. È quindi possibile aggiungere proprietà al nodo di configurazione a e utilizzarle nell&#39;implementazione `LiveActionFactory` in base alle esigenze.

Ad esempio, un `LiveAction` deve memorizzare il nome dell&#39;autore blueprint. Una proprietà del nodo di configurazione include il nome della proprietà della pagina blueprint in cui sono memorizzate le informazioni. In fase di esecuzione, `LiveAction` recupera il nome della proprietà dalla configurazione, quindi ottiene il valore della proprietà.

Il parametro del metodo [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) è un oggetto `Resource`. Questo oggetto `Resource` rappresenta il nodo `cq:LiveSyncAction` per questa azione live nella configurazione di rollout.

Per ulteriori informazioni, vedere [Creazione di una configurazione di rollout](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration).

Come di consueto quando si utilizza un nodo di configurazione, è necessario adattarlo a un oggetto `ValueMap`:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Accesso ai nodi di Target, ai nodi Source e alla LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

I seguenti oggetti vengono forniti come parametri del metodo `execute` dell&#39;oggetto `LiveAction`:

* Oggetto [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) che rappresenta l&#39;origine della Live Copy
* Oggetto `Resource` che rappresenta la destinazione della Live Copy.
* L&#39;oggetto [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) per la Live Copy
   * Il valore `autoSave` indica se `LiveAction` deve salvare le modifiche apportate all&#39;archivio
   * Il valore `reset` indica la modalità di ripristino del rollout.

Da questi oggetti è possibile ottenere informazioni su `LiveCopy`. È inoltre possibile utilizzare gli oggetti `Resource` per ottenere `ResourceResolver`, `Session` e `Node` oggetti. Questi oggetti sono utili per la manipolazione del contenuto del repository:

Nella prima riga del codice seguente, l&#39;origine è l&#39;oggetto `Resource` della pagina di origine:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Gli argomenti `Resource` possono essere `null` o `Resources` oggetti che non si adattano a `Node` oggetti, ad esempio [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) oggetti.

## Creazione di una nuova configurazione di rollout {#creating-a-new-rollout-configuration}

Puoi creare una configurazione di rollout quando le configurazioni di rollout installate non soddisfano i requisiti dell’applicazione, segui questi due passaggi:

* [Creare la configurazione di rollout](#create-the-rollout-configuration)
* [Aggiungere azioni di sincronizzazione alla configurazione di rollout](#add-synchronization-actions-to-the-rollout-configuration)

La nuova configurazione di rollout è quindi disponibile quando imposti le configurazioni di rollout su una pagina blueprint o Live Copy.

>[!TIP]
>
>Consulta anche le [best practice per personalizzare i rollout](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts).

### Creare la configurazione di rollout {#create-the-rollout-configuration}

Per creare una configurazione di rollout:

1. Apri CRXDE Lite in `https://<host>:<port>/crx/de`.

1. Passa a `/apps/msm/<your-project>/rolloutconfigs`, la versione personalizzata di `/libs/msm/wcm/rolloutconfigs` del progetto.

   * Se si tratta della prima configurazione, questo ramo `/libs` deve essere utilizzato come modello per creare il nuovo ramo in `/apps`.

1. In questa posizione, crea un nodo con le seguenti proprietà:

   * **Nome**: nome del nodo della configurazione di rollout, ad esempio `contentCopy` o `workflow`
   * **Tipo**: `cq:RolloutConfig`

1. Aggiungi le seguenti proprietà a questo nodo:

   * **Nome**: `jcr:title`

     **Tipo**: `String`
     **Valore**: titolo di identificazione che verrà visualizzato nell&#39;interfaccia utente

   * **Nome**: `jcr:description`

     **Tipo**: `String`
     **Valore**: descrizione facoltativa.

   * **Nome**: `cq:trigger`

     **Tipo**: `String`
     **Valore**: [Attivatore rollout](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers) da utilizzare
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Fare clic su **Salva tutto**.

### Aggiungere azioni di sincronizzazione alla configurazione di rollout {#add-synchronization-actions-to-the-rollout-configuration}

Le configurazioni di rollout sono archiviate sotto il [nodo di configurazione rollout](#create-the-rollout-configuration) creato sotto il nodo `/apps/msm/<your-project>/rolloutconfigs`.

Aggiungi nodi secondari di tipo `cq:LiveSyncAction` per aggiungere azioni di sincronizzazione alla configurazione di rollout. L&#39;ordine dei nodi delle azioni di sincronizzazione determina l&#39;ordine in cui si verificano le azioni.

1. In CRXDE Lite, seleziona il nodo [Configurazione rollout](#create-the-rollout-configuration), ad esempio `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`.

1. Crea un nodo con le seguenti proprietà:

   * **Nome**: nome del nodo dell&#39;azione di sincronizzazione
      * Il nome deve essere uguale a **Nome azione** nella tabella in [Azioni di sincronizzazione](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions), ad esempio `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Aggiungere e configurare tutti i nodi delle azioni di sincronizzazione necessari.

1. Ridisponi i nodi delle azioni in modo che il loro ordine corrisponda all’ordine in cui desideri che si verifichino.
   * Il nodo di azione più in alto si verifica per primo.

## Creazione e utilizzo di una classe LiveActionFactory semplice {#creating-and-using-a-simple-liveactionfactory-class}

Segui le procedure descritte in questa sezione per sviluppare un `LiveActionFactory` e utilizzarlo in una configurazione di rollout. Le procedure utilizzano Maven ed Eclipse per sviluppare e distribuire `LiveActionFactory`:

1. [Crea il progetto Maven](#create-the-maven-project) e importalo in Eclipse.
1. [Aggiungi dipendenze](#add-dependencies-to-the-pom-file) al file POM.
1. [Implementa l&#39;interfaccia `LiveActionFactory`](#implement-liveactionfactory) e distribuisci il bundle OSGi.
1. [Crea la configurazione rollout](#create-the-example-rollout-configuration).
1. [Crea la Live Copy](#create-the-live-copy).

[Il progetto Maven e il codice sorgente della classe Java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout) sono disponibili nell&#39;archivio Git pubblico.

### Creare il progetto Maven {#create-the-maven-project}

La procedura seguente richiede l&#39;aggiunta del profilo `adobe-public` al file delle impostazioni Maven.

* Per informazioni sul profilo pubblico di adobe, consulta [Ottenere il plug-in Maven del pacchetto di contenuti](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* Per informazioni sul file delle impostazioni Maven, consulta la [Guida di riferimento delle impostazioni](https://maven.apache.org/settings.html) di Maven.

1. Apri un terminale o una sessione della riga di comando e cambia la directory in modo che punti alla posizione in cui creare il progetto.
1. Immetti il comando seguente:

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Specifica i seguenti valori al prompt interattivo:

   * **`groupId`**: `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. Avvia Eclipse e [importa il progetto Maven](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse).

### Aggiungi dipendenze al file POM {#add-dependencies-to-the-pom-file}

Aggiungere le dipendenze in modo che il compilatore Eclipse possa fare riferimento alle classi utilizzate nel codice `LiveActionFactory`.

1. Da Esplora progetti Eclipse aprire il file `MyLiveActionFactory/pom.xml`.

1. Nell&#39;editor, fare clic sulla scheda `pom.xml` e individuare la sezione `project/dependencyManagement/dependencies`.

1. Aggiungere il codice XML seguente nell&#39;elemento `dependencyManagement`, quindi salvare il file.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Apri il file POM per il bundle da **Project Explorer** in `MyLiveActionFactory-bundle/pom.xml`.

1. Nell&#39;editor, fare clic sulla scheda `pom.xml` e individuare la sezione progetto/dipendenze. Aggiungi il seguente XML all’interno dell’elemento dependencies, quindi salva il file:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementare LiveActionFactory {#implement-liveactionfactory}

La classe `LiveActionFactory` seguente implementa una classe `LiveAction` che registra i messaggi relativi alle pagine di origine e di destinazione e copia la proprietà `cq:lastModifiedBy` dal nodo di origine al nodo di destinazione. Il nome dell&#39;azione live è `exampleLiveAction`.

1. In Esplora progetti Eclipse fare clic con il pulsante destro del mouse sul pacchetto `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` e scegliere **Nuovo** > **Classe**.

1. Per il **Nome**, immettere `ExampleLiveActionFactory` e quindi fare clic su **Fine**.

1. Aprire il file `ExampleLiveActionFactory.java`, sostituire il contenuto con il codice seguente e salvare il file.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Utilizzando il terminale o la sessione di comando, modificare la directory nella directory `MyLiveActionFactory` (la directory di progetto Maven). Quindi, immetti il seguente comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. Il file AEM `error.log` deve indicare che il bundle è avviato, visibile nei registri in `https://<host>:<port>/system/console/status-slinglogs`.

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Creare la configurazione di rollout di esempio {#create-the-example-rollout-configuration}

Crea la configurazione di rollout MSM che utilizza `LiveActionFactory` creata:

1. Crea e configura una configurazione di rollout [con la procedura standard](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) utilizzando le proprietà:

   * **Titolo**: Esempio Di Configurazione Di Rollout
   * **Nome**: examplerolloutconfig
   * **cq:trigger**: `publish`

### Aggiungi l’azione live alla configurazione di rollout di esempio {#add-the-live-action-to-the-example-rollout-configuration}

Configurare la configurazione di rollout creata nella procedura precedente in modo che utilizzi la classe `ExampleLiveActionFactory`.

1. Apri CRXDE Lite.

1. Crea il seguente nodo in `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nome**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Fare clic su **Salva tutto**.

1. Selezionare il nodo `exampleLiveAction` e aggiungere una proprietà per indicare alla classe `ExampleLiveAction` che la proprietà `cq:LastModifiedBy` deve essere replicata dal nodo di origine a quello di destinazione.

   * **Nome**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

1. Fare clic su **Salva tutto**.

### Creare la Live Copy {#create-the-live-copy}

[Crea una Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) del ramo Inglese/Prodotti del sito di riferimento WKND utilizzando la configurazione di rollout:

* **Source**: `/content/wknd/language-masters/en/products`

* **Configurazione rollout**: Esempio Di Configurazione Rollout

Attiva la pagina **Prodotti** (inglese) del ramo di origine e osserva i messaggi di registro generati dalla classe `LiveAction`:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## Modifica dei nomi delle lingue e dei paesi predefiniti {#changing-language-names-and-default-countries}

L’AEM utilizza un set predefinito di codici per lingua e paese.

* Il codice lingua predefinito è il codice a due lettere minuscole, come definito dallo standard ISO-639-1.
* Il codice predefinito del paese è il codice a due lettere minuscole o maiuscole, come definito dallo standard ISO 3166.

MSM utilizza un elenco memorizzato di codici di lingua e paese per determinare il nome del paese associato al nome della versione della lingua della pagina. Se necessario, puoi modificare i seguenti aspetti dell’elenco:

* Titoli delle lingue
* Nomi paesi
* Paesi predefiniti per le lingue (tra cui `en`, `de`)

L&#39;elenco delle lingue è archiviato sotto il nodo `/libs/wcm/core/resources/languages`. Ogni nodo figlio rappresenta una lingua o un paese della lingua:

* Il nome del nodo è il codice della lingua (ad esempio `en` o `de`) o il codice del paese_lingua (ad esempio `en_us` o `de_ch`).

* La proprietà `language` del nodo memorizza il nome completo della lingua per il codice.
* La proprietà `country` del nodo memorizza il nome completo del paese per il codice.
* Quando il nome del nodo è costituito solo da un codice della lingua (ad esempio `en`), la proprietà del paese è `*` e un&#39;ulteriore proprietà `defaultCountry` memorizza il codice del paese-lingua per indicare il paese da utilizzare.

![Definizione lingua](assets/msm-language-manager.png)

Per modificare le lingue:

1. Apri CRXDE Lite.
1. Seleziona la cartella `/apps` e fai clic su **Crea**, quindi su **Crea cartella.**

1. Denomina la nuova cartella `wcm`.

1. Ripetere il passaggio precedente per creare la struttura di cartelle `/apps/wcm/core`. Creare un nodo di tipo `sling:Folder` in `core` denominato `resources`.

1. Fare clic con il pulsante destro del mouse sul nodo `/libs/wcm/core/resources/languages` e scegliere **Copia**.
1. Fare clic con il pulsante destro del mouse sulla cartella `/apps/wcm/core/resources` e scegliere **Incolla**. Modificare i nodi figlio come richiesto.
1. Fare clic su **Salva tutto**.
1. Fare clic su **Strumenti**, **Operazioni** e quindi su **Console Web**. Da questa console fare clic su **OSGi**, quindi su **Configurazione**.
1. Individua e fai clic su **Day CQ WCM Language Manager** e modifica il valore di **Language List** in `/apps/wcm/core/resources/languages`, quindi fai clic su **Save**.

   ![&#x200B; giorno CQ WCM Language Manager](assets/msm-language-manager.png)

## Configurazione dei blocchi MSM nelle proprietà della pagina {#configuring-msm-locks-on-page-properties}

Quando crei una proprietà di pagina personalizzata, potrebbe essere necessario considerare se la nuova proprietà può essere idonea per il rollout in qualsiasi Live Copy.

Ad esempio, se vengono aggiunte due nuove proprietà di pagina:

* E-mail di contatto:

   * Non è necessario implementare questa proprietà, in quanto sarà diversa in ciascun paese (o marchio, ecc.).

* Stile visivo chiave:

   * Il requisito del progetto è che questa proprietà venga implementata in quanto è (di solito) comune a tutti i paesi (o marchi, e così via).

Quindi è necessario assicurarsi che:

* E-mail di contatto:

   * È escluso dalle proprietà di rollout.
   * Per ulteriori informazioni, vedere [Configurazione della sincronizzazione Live Copy](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization).

* Stile visivo chiave:

   * Assicurati di non poter modificare questa proprietà a meno che l’ereditarietà non venga annullata.
   * Assicurati inoltre di poter ripristinare l’ereditarietà. Questa operazione viene controllata facendo clic sui collegamenti a catena o a catena interrotta che vengono attivati per indicare lo stato della connessione.

Se una proprietà di pagina è soggetta a rollout e quindi, in caso di annullamento/ripristino dell’ereditarietà durante la modifica, è controllata dalla proprietà della finestra di dialogo:

* `cq-msm-lockable`

   * Questo creerà il simbolo del collegamento a catena nella finestra di dialogo.
   * Questo consente la modifica solo se l’ereditarietà viene annullata (il collegamento a catena è interrotto).
   * Questo si applica solo al primo livello figlio della risorsa
      * **Tipo**: `String`
      * **Valore**: contiene il nome della proprietà in esame ed è paragonabile al valore della proprietà `name`
         * Ad esempio, consulta

           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Una volta definito `cq-msm-lockable`, l&#39;interruzione/chiusura della catena interagirà con MSM nel modo seguente:

* Se il valore di `cq-msm-lockable` è:

   * **Relativo** (ad esempio, `myProperty` o `./myProperty`)

      * Interrompendo la catena, la proprietà verrà aggiunta e rimossa da `cq:propertyInheritanceCancelled`.

   * **Assoluto** (ad esempio, `/image`)

      * Se si interrompe la catena, l&#39;ereditarietà verrà annullata aggiungendo il mixin `cq:LiveSyncCancelled` a `./image` e impostando `cq:isCancelledForChildren` a `true`.

      * La chiusura della catena ripristina l’ereditarietà.

>[!NOTE]
>
>`cq-msm-lockable` si applica al primo livello figlio della risorsa da modificare e non funziona su nessun livello precedente più profondo, a prescindere dal fatto che il valore sia definito come assoluto o relativo.

>[!NOTE]
>
>Quando riabiliti l’ereditarietà, la proprietà della pagina Live Copy non viene sincronizzata automaticamente con la proprietà sorgente. Se necessario, è possibile richiedere manualmente una sincronizzazione.
