---
title: Sviluppo di un componente personalizzato per Screens as a Cloud Service
description: Il seguente tutorial illustra i passaggi necessari per creare un componente personalizzato per AEM Screens. AEM Screens riutilizza molti modelli di progettazione e tecnologie esistenti di altri prodotti AEM. Il tutorial evidenzia differenze e considerazioni speciali durante lo sviluppo per AEM Screens.
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: 1179e45f6e75a8a4f5e5e76903243f64d9f406ae
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 2%

---

# Sviluppo di un componente personalizzato per AEM Screens as a Cloud Service{#developing-a-custom-component-for-aem-screens}

Il seguente tutorial illustra i passaggi necessari per creare un componente personalizzato per AEM Screens. AEM Screens riutilizza molti modelli di progettazione e tecnologie esistenti di altri prodotti AEM. Il tutorial evidenzia differenze e considerazioni speciali durante lo sviluppo per AEM Screens.

## Panoramica {#overview}

Questo tutorial è destinato agli sviluppatori che hanno poca esperienza con AEM Screens. In questo tutorial, viene creato un semplice componente &quot;Hello World&quot; per un canale Sequence in AEM Screens. Una finestra di dialogo consente agli autori di aggiornare il testo visualizzato.


## Prerequisiti {#prerequisites}

Per completare questa esercitazione, sono necessari i seguenti elementi:

1. Feature Pack di Screens più recente

1. Lettore AEM Screens

1. Ambiente di sviluppo locale

I passaggi del tutorial e le schermate vengono eseguiti utilizzando **CRXDE Lite**. È inoltre possibile utilizzare gli IDE per completare l&#39;esercitazione. Ulteriori informazioni sull&#39;utilizzo di un IDE per sviluppare [con AEM sono disponibili qui](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html).


## Configurazione del progetto {#project-setup}

Il codice sorgente di un progetto Screens viene in genere gestito come progetto Maven con più moduli. Per accelerare l&#39;esercitazione, è stato pregenerato un progetto utilizzando [Archetipo progetto AEM 13](https://github.com/adobe/aem-project-archetype). Consulta [Configurazione del progetto](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html) per ulteriori dettagli sulla creazione di un progetto con Archetipo progetto Maven AEM.

1. Scarica e installa i seguenti pacchetti utilizzando [Gestione pacchetti CRX](http://localhost:4502/crx/packmgr/index.jsp):

[Ottieni file](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [Ottieni file](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **Facoltativamente** se si lavora con Eclipse o un altro IDE, scaricare il pacchetto di origine seguente. Distribuisci il progetto in un’istanza AEM locale utilizzando il comando Maven:

   **`mvn -PautoInstallPackage clean install`**

   Avvia progetto di esecuzione We.Retail di HelloWorld SRC Screens

[Ottieni file](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. In [Gestione pacchetti CRX](http://localhost:4502/crx/packmgr/index.jsp), verificare che siano installati i due pacchetti seguenti:

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Screens We.Retail Esegui pacchetti Ui.Apps e Ui.Content installati tramite Gestione pacchetti CRX](assets/crx-packages.png)

   Screens We.Retail Esegui pacchetti Ui.Apps e Ui.Content installati tramite CRX Package Manager

1. Il pacchetto **screens-weretail-run.ui.apps** installa il codice sotto `/apps/weretail-run`.

   Questo pacchetto contiene il codice responsabile del rendering dei componenti personalizzati per il progetto. Questo pacchetto include il codice del componente ed eventuali JavaScript o CSS necessari. Questo pacchetto incorpora anche **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** che contiene il codice Java™ necessario per il progetto.

   >[!NOTE]
   >
   >In questa esercitazione non viene scritto alcun codice Java™. Se è necessaria una logica di business più complessa, è possibile creare e distribuire Java™ di back-end utilizzando il bundle Java™ di base.

   ![Rappresentazione del codice ui.apps in CRXDE Lite](/help/screens-cloud/developing/assets/uipps-contents.png)

   Rappresentazione del codice ui.apps in CRXDE Lite

   Il componente **`helloworld`** è solo un segnaposto. Nel corso dell’esercitazione, viene aggiunta una funzionalità che consente all’autore di aggiornare il messaggio visualizzato dal componente.

1. Il pacchetto **screens-weretail-run.ui.content** installa il codice sotto:

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   Questo pacchetto contiene il contenuto iniziale e la struttura di configurazione necessaria per il progetto. **`/conf/we-retail-run`** contiene tutte le configurazioni per il progetto di esecuzione We.Retail. **`/content/dam/we-retail-run`** include l&#39;avvio delle risorse digitali per il progetto. **`/content/screens/we-retail-run`** contiene la struttura del contenuto di Screens. Il contenuto sotto questi percorsi viene aggiornato principalmente in AEM. Per promuovere la coerenza tra gli ambienti (locale, di sviluppo, di staging, di produzione) spesso nel controllo del codice sorgente viene salvata una struttura di contenuto di base.

1. **Passa al progetto AEM Screens > Esecuzione We.Retail:**

   Dalla navigazione globale in AEM > fai clic sull’icona Screens. Verifica che sia visibile il progetto di esecuzione We.Retail.

   ![we-retaiul-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## Creare il componente Hello World {#hello-world-cmp}

Il componente Hello World è un componente semplice che consente a un utente di inserire un messaggio da visualizzare sullo schermo. Il componente è basato sul [modello di componente AEM Screens: https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template).

AEM Screens presenta alcuni vincoli interessanti che non sono necessariamente validi per i componenti WCM Sites tradizionali.

* La maggior parte dei componenti Screens deve essere eseguita a schermo intero sui dispositivi di digital signage di destinazione
* La maggior parte dei componenti Screens deve essere incorporata nei canali di sequenza per generare presentazioni
* L’authoring deve consentire di modificare singoli componenti in un canale di sequenza, pertanto il loro rendering a schermo intero non è necessario

1. In **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` (o IDE scelto), passa a `/apps/weretail-run/components/content/helloworld.`

   Aggiungi le seguenti proprietà al componente `helloworld`:

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![Proprietà per /apps/weretail-run/components/content/helloworld](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   Proprietà per /apps/weretail-run/components/content/helloworld

   Il componente **`helloworld`** estende il componente **foundation/components/parbase** in modo che possa essere utilizzato correttamente in un canale di sequenza.

1. Crea un file sotto `/apps/weretail-run/components/content/helloworld` denominato `helloworld.html.`

   Compila il file con quanto segue:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (that is, on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, that is, edit, design, scaffolding, and so on. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   I componenti Screens richiedono due rendering diversi a seconda della [modalità di authoring](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/authoring/author-environment-tools.html#page-modes) utilizzata:

   1. **Produzione**: modalità Anteprima o Pubblicazione (wcmmode=disabled)
   1. **Modifica**: utilizzato per tutte le altre modalità di creazione, ovvero modifica, progettazione, scaffolding, sviluppatore...

   `helloworld.html`funge da commutatore, controllando quale modalità di authoring è attiva e reindirizzando a un altro script HTL. Una convenzione comune utilizzata dai componenti Screens consiste nell&#39;avere uno script `edit.html` per la modalità di modifica e uno script `production.html` per la modalità di produzione.

1. Crea un file sotto `/apps/weretail-run/components/content/helloworld` denominato `production.html.`

   Compila il file con quanto segue:

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   Il markup di produzione riportato sopra si riferisce al componente Hello World. Poiché il componente viene utilizzato su un canale Sequenza, è incluso un attributo `data-duration`. L&#39;attributo `data-duration` viene utilizzato dal canale della sequenza per sapere per quanto tempo deve essere visualizzato un elemento della sequenza.

   Il componente esegue il rendering di un tag `div` e `h1` con testo. `${properties.message}` è una parte dello script HTL che restituisce il contenuto di una proprietà JCR denominata `message`. In seguito viene creata una finestra di dialogo che consente all&#39;utente di immettere un valore per il testo della proprietà `message`.

   Si noti inoltre che con il componente viene utilizzata la notazione BEM (Block Element Modifier). BEM è una convenzione di codifica CSS che semplifica la creazione di componenti riutilizzabili. BEM è la notazione utilizzata da [Componenti core di AEM](https://github.com/adobe/aem-core-wcm-components/wiki/CSS-coding-conventions). <!-- WEBSITE WAS NOT ACCESSIBLE AS OF SEPTEMBER 1, 2022 More info can be found at: [https://getbem.com/](https://getbem.com/) -->

1. Crea un file sotto `/apps/weretail-run/components/content/helloworld` denominato `edit.html.`

   Compila il file con quanto segue:

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/edit.html
   
   */-->
   
   <!--/* if message populated */-->
   <div
    data-sly-test.message="${properties.message}"
    class="aem-Screens-editWrapper cmp-hello-world">
    <p class="cmp-hello-world__message">${message}</p>
   </div>
   
   <!--/* empty place holder */-->
   <div data-sly-test="${!message}"
        class="aem-Screens-editWrapper cq-placeholder cmp-hello-world"
        data-emptytext="${'Hello World' @ i18n, locale=request.locale}">
   </div>
   ```

   Il markup di modifica qui sopra si riferisce al componente Hello World. Nel primo blocco viene visualizzata una versione di modifica del componente, se il messaggio della finestra di dialogo è stato popolato.

   Se non è stato immesso alcun messaggio di dialogo, viene eseguito il rendering del secondo blocco. `cq-placeholder` e `data-emptytext` eseguono il rendering dell&#39;etichetta ***Hello World*** come segnaposto in questo caso. La stringa per l’etichetta può essere internazionalizzata utilizzando i18n per supportare l’authoring in più lingue.

1. **Copia finestra di dialogo immagine Screens da utilizzare per il componente Hello World.**

   È più semplice iniziare da una finestra di dialogo esistente e quindi apportare modifiche.

   1. Copia la finestra di dialogo da: `/libs/screens/core/components/content/image/cq:dialog`
   1. Incolla la finestra di dialogo sotto `/apps/weretail-run/components/content/helloworld`

   ![copia-immagine-finestra di dialogo](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **Aggiorna finestra di dialogo Hello World per includere una scheda per il messaggio.**

   Aggiorna la finestra di dialogo in modo che corrisponda a quanto segue. La struttura dei nodi JCR della finestra di dialogo finale è presentata di seguito in XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       jcr:title="Hello World"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content
           jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/coral/foundation/tabs"
           size="L">
           <items jcr:primaryType="nt:unstructured">
               <message
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Message"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <message
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                   fieldDescription="Message for component to display"
                                   fieldLabel="Message"
                                   name="./message"/>
                           </items>
                       </column>
                   </items>
               </message>
               <sequence
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Sequence"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <duration
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
                                   defaultValue=""
                                   fieldDescription="Amount of time the image is shown in the sequence, in milliseconds"
                                   fieldLabel="Duration (ms)"
                                   min="0"
                                   name="./duration"/>
                           </items>
                       </column>
                   </items>
               </sequence>
           </items>
       </content>
   </jcr:root>
   ```

   `textfield` per il messaggio viene salvato in una proprietà denominata `message` e `numberfield` per la durata viene salvato in una proprietà denominata `duration`. In `/apps/weretail-run/components/content/helloworld/production.html` HTL fa riferimento a entrambe queste proprietà come `${properties.message}` e `${properties.duration}`.

   ![Hello World - finestra di dialogo completata](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Finestra di dialogo Hello World - completato

## Creare librerie lato client {#clientlibs}

Le librerie lato client forniscono un meccanismo per organizzare e gestire i file CSS e JavaScript necessari per un’implementazione AEM.

I componenti AEM Screens vengono riprodotti in modo diverso nelle modalità Modifica e Anteprima/Produzione. Vengono create due librerie client: una per la modalità di modifica e una per l’anteprima/produzione.

1. Crea una cartella per le librerie lato client per il componente Hello World.

   Sotto `/apps/weretail-run/components/content/helloworld`, creare una cartella denominata `clientlibs`.

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. Nella cartella `clientlibs` creare un nodo denominato `shared` di tipo `cq:ClientLibraryFolder.`

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. Aggiungi le seguenti proprietà alla libreria client condivisa:

   * `allowProxy` | Booleano | `true`

   * `categories`| Stringa[] | `cq.screens.components`

   ![Proprietà per /apps/weretail-run/components/content/helloworld/clientlibs/shared](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   Proprietà per /apps/weretail-run/components/content/helloworld/clientlibs/shared

   La proprietà Categories è una stringa che identifica la libreria client. La categoria cq.screens.component viene utilizzata sia in modalità Modifica che Anteprima/Produzione. Di conseguenza, qualsiasi CSS/JS definito nella libreria client condivisa viene caricato in tutte le modalità.

   È consigliabile non esporre mai percorsi direttamente a /apps in un ambiente di produzione. La proprietà allowProxy garantisce che venga fatto riferimento alla libreria client CSS e JS tramite un prefisso of/etc.clientlibs.

1. Crea il file denominato `css.txt` sotto la cartella condivisa.

   Compila il file con quanto segue:

   ```
   #base=css
   
   styles.less
   ```

1. Creare una cartella denominata `css` sotto la cartella `shared`. Aggiungere un file denominato `style.less` sotto la cartella `css`. La struttura delle librerie client ora dovrebbe essere simile alla seguente:

   ![2018-04-30_at_3_11pm](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   Invece di scrivere direttamente CSS, questa esercitazione utilizza MENO. [LESS](https://lesscss.org/) è un popolare precompilatore CSS che supporta variabili, mixin e funzioni CSS. Le librerie client di AEM supportano in modo nativo la compilazione LESS. È possibile utilizzare Sass o altri precompilatori, che tuttavia devono essere compilati al di fuori di AEM.

1. Popolare `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` con quanto segue:

   ```css
   /**
       Shared Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less
   
   **/
   
   .cmp-hello-world {
       background-color: #fff;
   
    &__message {
     color: #000;
     font-family: Helvetica;
     text-align:center;
    }
   }
   ```

1. Copiare e incollare la cartella della libreria client `shared` per creare una libreria client denominata `production`.

   ![Copia la libreria client condivisa per creare una libreria client di produzione](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   Copia la libreria client condivisa per creare una libreria client di produzione.

1. Aggiorna la proprietà `categories` della libreria client di produzione in modo che sia `cq.screens.components.production.`

   In questo modo gli stili vengono caricati solo in modalità Anteprima/Produzione.

   ![Proprietà per /apps/weretail-run/components/content/helloworld/clientlibs/production](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   Proprietà per /apps/weretail-run/components/content/helloworld/clientlibs/production

1. Popolare `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` con quanto segue:

   ```css
   /**
       Production Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less
   
   **/
   .cmp-hello-world {
   
       height: 100%;
       width: 100%;
       position: fixed;
   
    &__message {
   
     position: relative;
     font-size: 5rem;
     top:25%;
    }
   }
   ```

   Gli stili di cui sopra visualizzano il messaggio centrato al centro dello schermo, ma solo in modalità di produzione.

È possibile utilizzare una terza categoria di libreria client: `cq.screens.components.edit` per aggiungere al componente stili specifici di sola modifica.

| Categoria Clientlib | Utilizzo |
|---|---|
| `cq.screens.components` | Stili e script condivisi tra le modalità di modifica e di produzione |
| `cq.screens.components.edit` | Stili e script utilizzati solo in modalità di modifica |
| `cq.screens.components.production` | Stili e script utilizzati solo in modalità di produzione |

## Creare una pagina di progettazione {#design-page}

AEM Screens utilizza [modelli di pagina statici](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-static.html) e [configurazioni di progettazione](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/siteandpage/default-components-designmode.html) per le modifiche globali. Le configurazioni di progettazione vengono spesso utilizzate per configurare i componenti consentiti per Parsys su un canale. Una best practice consiste nell’archiviare queste configurazioni in un modo specifico per l’app.

Di seguito viene creata una pagina Progettazione dell&#39;esecuzione di We.Retail in cui sono memorizzate tutte le configurazioni specifiche del progetto.

1. In **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs`, passa a `/apps/settings/wcm/designs`
1. Creare un nodo sotto la cartella delle progettazioni, denominato `we-retail-run` con un tipo di `cq:Page`.
1. Nella pagina `we-retail-run` aggiungere un altro nodo denominato `jcr:content` di tipo `nt:unstructured`. Aggiungi le seguenti proprietà al nodo `jcr:content`:

   | Nome | Tipo | Valore |
   |---|---|---|
   | jcr:title | Stringa | Esecuzione We.Retail |
   | sling:resourceType | Stringa | wcm/core/components/designer |
   | cq:doctype | Stringa | html_5 |

   ![Pagina progettazione in /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   Pagina di progettazione in /apps/settings/wcm/designs/we-retail-run

## Creare un canale sequenza {#create-sequence-channel}

Il componente Hello World deve essere utilizzato su un canale di sequenza. Per testare il componente, viene creato un nuovo canale di sequenza.

1. Dalla navigazione globale AEM, passa a **Screens** > **We.Retail Ru** n > e seleziona **Canali**.

1. Fai clic sul pulsante **Crea**

   1. Scegli **Crea entità**

   ![2018-04-30_at_5_18pm](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. Nella procedura guidata Crea:

1. Passaggio modello - scegli **Canale sequenza**

   1. Passaggio proprietà

   * Scheda Base > Titolo = **Canale Inattivo**
   * Scheda Canale > seleziona **Rendi canale online**

   ![canale inattivo](/help/screens-cloud/developing/assets/idle-channel.gif)

1. Apri le proprietà della pagina per il canale inattivo. Aggiornare il campo Struttura in modo che punti a `/apps/settings/wcm/designs/we-retail-run,` la pagina di progettazione creata nella sezione precedente.

   ![Configurazione progettazione /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   Configurazione di progettazione che punta a /apps/settings/wcm/designs/we-retail-run

1. Modifica il canale inattivo creato per aprirlo.

1. Passa alla modalità pagina **Progettazione**.

   1. Fai clic sull&#39;icona **chiave inglese** in Parsys per configurare i componenti consentiti.

   1. Selezionare il gruppo **Screens** e il gruppo **Esecuzione We.Retail - Contenuto**.

   ![2018-04-30_at_5_43pm](assets/2018-04-30_at_5_43pm.png)

1. Passa alla modalità pagina **Modifica**. Il componente Hello World può ora essere aggiunto alla pagina e combinato con altri componenti del canale di sequenza.

   ![2018-04-30_at_5_53pm](assets/2018-04-30_at_5_53pm.png)

1. In **CRXDE Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par`, passa a `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`. La proprietà `components` ora include `group:Screens`, `group:We.Retail Run - Content`.

   ![Configurazione progettazione in /apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   Configurazione del progetto in /apps/settings/wcm/designs/we-retail-run

## Modello per gestori personalizzati {#custom-handlers}

Se il componente personalizzato utilizza risorse esterne, come risorse (immagini, video, font e icone), rappresentazioni di risorse specifiche o librerie lato client (css e js), queste risorse non vengono aggiunte automaticamente alla configurazione offline. Il motivo è che Adobe raggruppa solo il markup HTML per impostazione predefinita.

Per personalizzare e ottimizzare le risorse esatte scaricate sul lettore, Adobe offre un meccanismo di estensione per i componenti personalizzati, in modo da esporre le loro dipendenze alla logica di caching offline in Screens.

La sezione seguente mostra il modello per i gestori di risorse offline personalizzati e i requisiti minimi in `pom.xml` per quel progetto specifico.

```java
package …;

import javax.annotation.Nonnull;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceUtil;
import org.apache.sling.api.resource.ValueMap;

import com.adobe.cq.screens.visitor.OfflineResourceHandler;

@Service(value = OfflineResourceHandler.class)
@Component(immediate = true)
public class MyCustomHandler extends AbstractResourceHandler {

 @Reference
 private …; // OSGi services injection

 /**
  * The resource types that are handled by the handler.
  * @return the handled resource types
  */
 @Nonnull
 @Override
 public String[] getSupportedResourceTypes() {
     return new String[] { … };
 }

 /**
  * Accept the provided resource, visit and traverse it as needed.
  * @param resource The resource to accept
  */
 @Override
 public void accept(@Nonnull Resource resource) {
     ValueMap properties = ResourceUtil.getValueMap(resource);
     
     /* You can directly add explicit paths for offline caching using the `visit`
        method of the visitor. */
     
     // retrieve a custom property from the component
     String myCustomRenditionUrl = properties.get("myCustomRenditionUrl", String.class);
     // adding that exact asset/rendition/path to the offline manifest
     this.visitor.visit(myCustomRenditionUrl);
     
     
     /* You can delegate handling for dependent resources so they are also added to
        the offline cache using the `accept` method of the visitor. */
     
     // retrieve a referenced dependent resource
     String referencedResourcePath = properties.get("myOtherResource", String.class);
     ResourceResolver resolver = resource.getResourceResolver();
     Resource referencedResource = resolver.getResource(referencedResourcePath);
     // let the handler for that resource handle it
     if (referencedResource != null) {
         this.visitor.accept(referencedResource);
     }
   }
}
```

Il codice seguente fornisce i requisiti minimi in `pom.xml` per quel progetto specifico:

```css
   <dependencies>
        …
        <!-- Felix annotations -->
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.9.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Screens core bundle with OfflineResourceHandler/AbstractResourceHandler -->
        <dependency>
            <groupId>com.adobe.cq.screens</groupId>
            <artifactId>com.adobe.cq.screens</artifactId>
            <version>1.5.90</version>
            <scope>provided</scope>
        </dependency>
        …
      </dependencies>
```

## Tutti gli elementi insieme {#putting-it-all-together}

Il video seguente mostra il componente finito e come può essere aggiunto a un canale Sequenza. Il canale viene quindi aggiunto a una visualizzazione Posizione e infine assegnato a un lettore Screens.

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## Codice finito {#finished-code}

Di seguito è riportato il codice finito dell&#39;esercitazione. I pacchetti AEM compilati sono **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** e **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**. **SRC-screens-weretail-run-0.0.1.zip &#x200B;** è il codice sorgente non compilato che può essere distribuito utilizzando Maven.

[Ottieni file](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[Ottieni file](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[Ottieni file](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
