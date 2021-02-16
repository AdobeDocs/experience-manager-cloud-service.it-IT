---
title: Integrazione con Adobe Target
description: 'Integrazione con Adobe Target '
translation-type: tm+mt
source-git-commit: 79cdc4f453efe5b251891c09934e2dcb823f645c
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---


# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte dell&#39;Adobe Marketing Cloud,  Adobe Target consente di aumentare la pertinenza dei contenuti attraverso il targeting e la misurazione su tutti i canali. L&#39;integrazione  Adobe Target e AEM come Cloud Service richiede:

* utilizzo dell&#39;interfaccia utente touch per creare una configurazione Target in AEM come Cloud Service (è richiesta la configurazione IMS).
* aggiunta e configurazione  Adobe Target come estensione in [ Adobe Launch](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html).

 Adobe Launch è necessario per la gestione delle proprietà lato client sia per Analytics che per Target nelle pagine AEM (librerie/tag JS). Tuttavia, l&#39;integrazione con Launch è necessaria per il &quot;targeting delle esperienze&quot;. Per l’esportazione di frammenti esperienza in Target è necessario solo disporre della configurazione Adobe Target  e di IMS.

>[!NOTE]
>
>Adobe Experience Manager, come clienti di Cloud Service che non dispongono di un account Target esistente, può richiedere l&#39;accesso a Target Foundation Pack per  Experience Cloud. Foundation Pack fornisce un utilizzo limitato del volume di Target.

## Creazione della  configurazione Adobe Target {#create-configuration}

1. Passare a **Strumenti** → **Cloud Services**.
   ![](assets/cloudservice1.png "NavigationNavigation")
2. Selezionare **Adobe Target**.
3. Selezionare il pulsante **Crea**.
   ![](assets/tenant1.png "CreateCreate")
4. Compila i dettagli (vedi sotto) e seleziona **Connect**.
   ![](assets/open_screen1.png "Connect")

### Configurazione IMS {#ims-configuration}

Per integrare correttamente Target con AEM e Launch è necessaria una configurazione IMS sia per Launch che per Target. Mentre la configurazione IMS per Launch è preconfigurata in AEM come Cloud Service, è necessario creare la configurazione IMS di Target (dopo il provisioning di Target). Fate riferimento a [questo video](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) e [questa pagina](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html) per informazioni su come creare la configurazione IMS di Target.

###  ID tenant Adobe Target e  codice client Adobe Target {#tenant-client}

Durante la configurazione dei  campi ID tenant Adobe Target e  Codice client Adobe Target, tenete presente quanto segue:

1. Per la maggior parte dei clienti, l&#39;ID tenant e il codice cliente sono gli stessi. Ciò significa che entrambi i campi contengono le stesse informazioni e sono identici. Accertatevi di inserire l’ID tenant in entrambi i campi.
2. A fini legacy, è inoltre possibile immettere valori diversi nei campi ID tenant e Codice cliente.

In entrambi i casi, tenete presente che:

* Per impostazione predefinita, anche il Codice client (se aggiunto per primo) viene automaticamente copiato nel campo ID tenant.
* È possibile modificare l&#39;ID tenant predefinito impostato.
* Di conseguenza, le chiamate back-end a Target saranno basate sull&#39;ID tenant e le chiamate client-side a Target saranno basate sul codice client.

Come già detto, il primo caso è il più comune per AEM come Cloud Service. In entrambi i casi, accertatevi che i campi **sia** contengano le informazioni corrette a seconda dei requisiti.

>[!NOTE]
>
> Per modificare una configurazione di Target esistente:
>
> 1. Reinserite l&#39;ID tenant.
> 2. Connettetevi di nuovo a Target.
> 3. Salva la configurazione.


### Modifica della configurazione di destinazione {#edit-target-configuration}

Per modificare la configurazione di Target, attenetevi alla seguente procedura:

1. Selezionate una configurazione esistente e fate clic su **Proprietà**.
2. Modificare le proprietà.
3. Selezionare **Connetti di nuovo a  Adobe Target**.
4. Seleziona **Salva e chiudi**.

### Aggiunta di una configurazione a un sito {#add-configuration}

Per applicare una configurazione dell&#39;interfaccia utente touch a un sito, passare a: **Siti** → **Selezionare una pagina del sito** → **Proprietà** → **Avanzate** → **Configurazione** → Selezionare il tenant di configurazione.

## Integrazione  Adobe Target su AEM siti utilizzando  lancio Adobe {#integrate-target-launch}

AEM offre un&#39;integrazione out-of-the-box con il Experience Platform Launch. Aggiungendo l&#39;estensione Adobe Target  al Experience Platform Launch è possibile utilizzare le funzionalità di  Adobe Target su AEM pagina Web. Per il rendering delle librerie di Target è possibile utilizzare solo Launch.

>[!NOTE]
>
>I framework esistenti (legacy) funzionano ancora, ma non possono essere configurati nell&#39;interfaccia utente touch. È consigliabile rigenerare le configurazioni di mappatura delle variabili in Launch.

Come panoramica generale, i passaggi di integrazione sono:

1. Creare una proprietà Launch
2. Aggiungere le estensioni richieste
3. Crea un elemento dati (per acquisire i parametri dell&#39;hub di contesto)
4. Creare una regola di pagina
5. Creazione e pubblicazione

### Creazione di una proprietà di avvio {#create-property}

Una proprietà è un contenitore che verrà compilato con estensioni, regole, elementi di dati.

1. Selezionare il pulsante **Nuova proprietà**.
2. Specificare un nome per la proprietà.
3. Mentre il dominio immette l&#39;IP/host su cui si desidera caricare la libreria del lancio.
4. Selezionare il pulsante **Salva**.
   ![](assets/properties_newproperty1.png "LaunchpropertyLaunchproperty")

### Aggiunta delle estensioni necessarie {#add-extension}

**** Estensionsis il contenitore che gestisce le impostazioni della libreria di base. L&#39;estensione Adobe Target  supporta implementazioni lato client utilizzando l&#39;SDK JavaScript di Target per il Web moderno, at.js. È necessario aggiungere le estensioni **Adobe Target** e **ContextHub** di Adobe.

1. Selezionate l’opzione Catalogo estensioni e cercate Target nel filtro.
2. Selezionare **Adobe Target** at.js e fare clic sull&#39;opzione di installazione.
   ![Target ](assets/search_ext1.png "SearchTarget")
3. Selezionare il pulsante **Configura**. Osservate la finestra di configurazione con le credenziali dell&#39;account Target importate e la versione at.js per questa estensione.
4. Selezionare **Save** per aggiungere l&#39;estensione Target alla proprietà Launch. Dovrebbe essere possibile visualizzare l&#39;estensione Target elencata nell&#39;elenco **Estensioni installate**.
   ![Salva estensione ](assets/configure_extension1.png "ExtensionSave")
5. Ripetete i passaggi indicati sopra per cercare l&#39;estensione **ContextHub** del Adobe e installarla (richiesta per l&#39;integrazione con i parametri contestualizzatori, in base alla quale verrà eseguito il targeting).

### Creazione di un elemento dati {#data-element}

**Gli** elementi di dati sono i segnaposto ai quali è possibile mappare i parametri dell&#39;hub di contesto.

1. Selezionare **Elementi dati**.
2. Selezionare **Aggiungi elemento dati**.
3. Immettete il nome dell’elemento dati e associatelo a un parametro context hub.
4. selezionare **Save**.
   ![Elemento Data ](assets/data_elem1.png "ElementData")

### Creazione di una regola di pagina {#page-rule}

In **Rule** definiamo e ordiniamo una sequenza di azioni, che verranno eseguite sul sito, per raggiungere il targeting.

1. Aggiungete un set di azioni come esemplificato nello screenshot.
   ![](assets/rules1.png "ActionsActions")
2. In Aggiungi parametri a tutte le mbox aggiungete l’elemento dati configurato in precedenza (vedete l’elemento dati sopra) al parametro che verrà inviato nella chiamata mbox.
   ![](assets/map_data1.png "MboxActions")

### Creazione e pubblicazione di {#build-publish}

Per informazioni su come creare e pubblicare, fare riferimento a questa [pagina](https://docs.adobe.com/content/help/en/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html).

## Modifiche alla struttura del contenuto tra le configurazioni dell&#39;interfaccia classica e touch {#changes-content-structure}

| **Cambia** | **Configurazione interfaccia utente classica** | **Configurazione interfaccia touch** | **Conseguenze** |
|---|---|---|---|
| Posizione della configurazione di Target. | /etc/cloudservices/testandtarget/ | /conf/tenant/settings/cloud/target | Precedenti configurazioni multiple erano presenti in /etc/cloudservices/testandtarget, ma ora una singola configurazione sarà presente sotto un tenant. |

>[!NOTE]
>
>Le configurazioni precedenti sono ancora supportate per i clienti esistenti (senza la possibilità di modificarle o crearne di nuove). Le configurazioni precedenti faranno parte di pacchetti di contenuti caricati dal cliente tramite VSTS.
