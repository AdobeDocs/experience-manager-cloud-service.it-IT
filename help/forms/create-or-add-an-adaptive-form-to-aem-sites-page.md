---
title: Creare o aggiungere un modulo adattivo alla pagina di AEM Sites
description: Scopri come creare o aggiungere facilmente un modulo adattivo alla pagina AEM Sites. Scopri le tecniche e le best practice passo passo per integrare moduli dinamici e personalizzabili nel tuo sito web, ottimizzando le tue esperienze digitali per il massimo impatto.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---


# Creare o aggiungere un modulo adattivo alla pagina di AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

Con AEM Forms puoi incorporare facilmente i moduli adattivi nelle pagine web. Questo consente ai visitatori di compilare e inviare i moduli in modo comodo, senza mai uscire dalla pagina in cui si trovano. In questo modo, possono rimanere coinvolti senza difficoltà con altri elementi del sito web interagendo attivamente con il modulo.

Puoi sfruttare appieno questa funzione utilizzando le seguenti opzioni:

* **Aggiungere un modulo personalizzato:** Crea un nuovo modulo da zero, adattandolo in modo specifico alle tue esigenze e preferenze di progettazione.

* **Migliora frammenti esperienza:** Estendi la portata dei moduli aggiungendoli ai frammenti esperienza AEM per consentirne il riutilizzo su più pagine o siti.

* **Utilizzare modelli approvati:** Utilizza modelli preapprovati per creare rapidamente moduli in linea con le linee guida di branding e gli standard di progettazione della tua organizzazione.

* **Aggiungi moduli esistenti:** È possibile integrare facilmente i moduli già creati nei siti Web, consentendo ai visitatori di interagire direttamente con essi.

* **Aggiungi più moduli:**  Aggiungere più moduli a una pagina per fornire più scelte agli utenti in base alle loro preferenze e requisiti. Questi possono essere una combinazione di forme nuove di zecca da zero e moduli esistenti.

Puoi utilizzare l’editor di AEM Sites per creare e aggiungere rapidamente più moduli alle pagine di AEM Sites. L’utilizzo dell’editor di AEM Sites consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites, sfruttando la potenza dei componenti dei moduli adattivi, tra cui comportamento dinamico, convalide, integrazione dei dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

## Obiettivo

* Scopri come creare un modulo adattivo utilizzando l’editor di AEM Sites e il frammento di esperienza
* Scopri come impostare layout e tema per un modulo adattivo aggiunto a una pagina AEM Sites e
* Creare un modulo adattivo utilizzando l’editor di AEM Sites e un frammento di esperienza


## Considerazioni {#consideration}

AEM Forms fornisce i componenti Contenitore modulo adattivo e Forms adattivo - Incorpora. È possibile utilizzare il Contenitore di moduli adattivi per creare e aggiungere un nuovo modulo in un frammento di esperienza o in una pagina AEM Sites, mentre il componente Forms adattivo - Incorpora consente di aggiungere un modulo adattivo esistente o crearne uno nuovo tramite l’editor di Forms adattivo.

Quando utilizzi il Contenitore di moduli adattivi per creare o aggiungere un modulo, i moduli vengono tradotti e localizzati attraverso il flusso di traduzione AEM Sites. Per ogni lingua viene generata una copia separata (copia per lingua) della pagina del sito e dei moduli corrispondenti e, quando un autore di contenuti modifica una regola in un modulo nella pagina padre, le stesse modifiche devono essere apportate in tutte le copie per lingua del modulo. Il Contenitore di moduli adattivi consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

Quando crei o aggiungi un modulo utilizzando il componente di incorporamento modulo adattivo, i moduli vengono tradotti e localizzati utilizzando il flusso di traduzione AEM Forms. In questo caso, viene mantenuto un singolo modulo a cui viene fatto riferimento in tutte le copie in lingua delle pagine di Sites. Il componente per l’incorporamento di moduli adattivi non fornisce l’accesso a varie funzioni delle pagine AEM Sites come, controllo delle versioni, targeting, traduzione e gestione multisito.


## Prima di iniziare {#before-you-start}

+++  Abilitare i componenti core Forms adattivi per il tuo ambiente

Assicurati che [I componenti core Forms adattivi sono abilitati per l’ambiente AEM Forms as a Cloud Service](enable-adaptive-forms-core-components.md).

+++

+++ Abilita **[!UICONTROL Contenitore Forms adattivo]

Per abilitare [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su Modifica.
1. Apri il modello della pagina Sites. Per aprire il modello, passare alla [!UICONTROL Informazioni pagina] ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Modifica modello]. Apre il modello corrispondente nell’editor modelli.
1. Nella vista Struttura, fare clic sul pulsante **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) nella barra dei menu. In **[!UICONTROL Componenti consentiti]** e seleziona la **[!UICONTROL Contenitore Forms adattivo]**  casella di controllo sotto **[Nome progetto archetipo AEM] - Modulo adattivo**.
1. Clic **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  Aggiungere librerie client Forms adattive alla pagina AEM Sites

Per abilitare la funzionalità completa del componente Contenitore Forms adattivo, aggiungi le librerie client Customheaderlibs e Customfooterlibs alla pagina AEM Sites utilizzando la pipeline di distribuzione. Per aggiungere le librerie:

1. Accedere e clonare [Archivio Git AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Apri la cartella AEM Cloud Service Git Repository in un editor di testo per piani. Ad esempio, Codice visivo Microsoft.
1. Apri `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` per la modifica e annota il valore di `sling:resourceSuperType`. Ad esempio, annota il valore `core/wcm/components/page/v3/page`.


   ![risorsa sling](/help/forms/assets/slingresource.png)

1. Accedi a `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` e creare una struttura di cartelle identica al valore indicato nel passaggio precedente. Ad esempio, se il valore è simile all’esempio del passaggio precedente, la struttura del nodo finale è `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![struttura di sovrapposizione](/help/forms/assets/overlaystructure.png)

1. Crea `customheaderlibs.html` e `customfooterlibs.html` file nella struttura dei nodi creata nel passaggio precedente e aggiungi il seguente contenuto ai file:

   ```
        //Customheaderlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
        </sly> 
   
        //customfooterlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
        </sly> 
   ```

1. [Eseguire la pipeline di distribuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le librerie client nell’ambiente AEM as a Cloud Service.

+++

## Creare un modulo adattivo {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Puoi creare un nuovo modulo da zero, adattandolo in modo specifico alle tue esigenze e preferenze di progettazione, direttamente in una pagina di siti AEM o in Frammento di esperienza. Per i moduli monouso, si consiglia di eseguire l’authoring diretto in una pagina dei siti AEM, mentre i frammenti di esperienza sono ideali per i moduli che devono essere riutilizzati in più pagine del sito web.

* [Creare un modulo in una pagina di AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creare un modulo in un frammento esperienza](#create-an-adaptive-form-in-experience-fragment)

### Creare un modulo in una pagina di AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puoi utilizzare il componente Contenitore modulo adattivo nell’editor di AEM Sites per creare un modulo personalizzato. Il componente consente di creare un modulo trascinandone e rilasciandone i componenti. I componenti del modulo sono basati su Componenti core. Puoi personalizzarli facilmente in base alle esigenze della tua organizzazione.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Per creare un modulo adattivo in una pagina Sites:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Trascina la selezione **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti alla pagina Sites. Crea uno spazio nella pagina per il modulo. Puoi utilizzare la modalità layout per modificare la dimensione dello spazio del contenitore.
1. Trascina i componenti core modulo adattivo nello spazio contenitore per creare il modulo.
1. Aggiungi il pulsante Invia.

Quindi, imposta l’azione Invia e le proprietà avanzate.

### Creare un modulo in un frammento esperienza {#create-an-adaptive-form-in-experience-fragment}

Puoi estendere la portata dei moduli aggiungendoli ai Frammenti esperienza AEM per consentirne il riutilizzo su più pagine o siti. Ad esempio, puoi includere un modulo di iscrizione a una newsletter all’interno di un frammento di esperienza. Questo consente di riutilizzare in modo comodo il frammento su più pagine del sito web, eliminando la necessità di ricreare ripetutamente il modulo. Eventuali aggiornamenti o modifiche apportate al modulo di iscrizione alla newsletter all’interno del frammento di esperienza si propagano automaticamente a tutte le pagine in cui viene utilizzato. Questo semplifica il processo e garantisce un’esperienza utente fluida, semplificando al contempo la gestione dei moduli del sito web.

Per creare un modulo adattivo in un frammento di esperienza:

## Modificare il layout di un modulo adattivo {#change-layout-of-an-adaptive-form}

Nella pagina di AEM Sites, utilizza [Modalità Layout](/help/sites-cloud/authoring/features/responsive-layout.md) per ridimensionare un componente Contenitore modulo adattivo aggiunto a una pagina AEM Sites.
