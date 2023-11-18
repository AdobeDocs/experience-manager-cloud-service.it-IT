---
title: Integrazione con Adobe Target
description: Scopri come integrare Adobe Target con AEM as a Cloud Service utilizzando l’interfaccia utente touch e Adobe Launch.
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 96%

---

# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte di Adobe Experience Cloud, Adobe Target consente di aumentare la rilevanza dei contenuti mediante il targeting e la valutazione su tutti i canali. L’integrazione di Adobe Target e AEM as a Cloud Service richiede:

* utilizzo dell’interfaccia utente touch per creare una configurazione Target in AEM as a Cloud Service (è richiesta la configurazione IMS).
* aggiunta e configurazione di Adobe Target come estensione in [Adobe Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=it).

Adobe Launch è necessario per gestire le proprietà lato client sia per Analytics sia per Target nelle pagine AEM (librerie/tag JS). Detto questo, l’integrazione con Launch è necessaria per il “targeting dell’esperienza”.

Per l’esportazione di frammenti di esperienza e/o frammenti di contenuto in Target, è sufficiente la [Configurazione Adobe Target e IMS](/help/sites-cloud/integrating/integration-adobe-target-ims.md).

>[!NOTE]
>
>I clienti che non dispongono di un account Target esistente possono richiedere l’accesso a Target Foundation Pack per Experience Cloud. Foundation Pack fornisce un uso limitato del volume di Target.

## Creazione della configurazione di Adobe Target {#create-configuration}

1. Passa a **Strumenti** → **Servizi cloud**.
   ![Navigazione](assets/cloudservice1.png "Navigazione")
2. Seleziona **Adobe Target**.
3. Seleziona il pulsante **Crea**.
   ![Crea](assets/tenant1.png "Crea")
4. Compila i dettagli (vedi sotto) e seleziona **Connetti**.
   ![Connetti](assets/open_screen1.png "Connetti")

### Configurazione IMS {#ims-configuration}

Per integrare correttamente Target con AEM e Launch è necessaria una configurazione IMS sia per Launch che per Target. Anche se la configurazione IMS per Launch è preconfigurata in AEM as a Cloud Service, è necessario creare la configurazione IMS di Target (dopo il provisioning di Target). Consulta [Configurazione IMS da utilizzare per l’integrazione con Adobe Target](/help/sites-cloud/integrating/integration-adobe-target-ims.md) e il video [Integrazione di Experience Platform Launch e AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=it) per scoprire come creare la configurazione IMS di Target.

### ID tenant e codice client di Adobe Target {#tenant-client}

Durante la configurazione dei campi ID tenant e Codice client di Adobe Target, tieni presente quanto segue:

1. Per la maggior parte dei clienti, l’ID tenant e il codice client sono gli stessi. Ovvero, entrambi i campi contengono le stesse informazioni e sono identici. Assicurati di inserire l’ID tenant in entrambi i campi.
2. Per motivi di legacy, puoi anche immettere valori diversi nei campi ID tenant e Codice client.

In entrambi i casi:

* Per impostazione predefinita, anche il codice client (se aggiunto per primo) viene copiato automaticamente nel campo ID tenant.
* Se necessario, puoi modificare il set di ID tenant predefinito.
* Le chiamate di back-end a Target sono basate sull’ID tenant e le chiamate lato client a Target sono basate sul Codice client.

Come indicato in precedenza, il primo caso è il più comune per AEM as a Cloud Service. In entrambi i casi, assicurati che **entrambi** i campi contengano le informazioni corrette a seconda dei requisiti.

>[!NOTE]
>
> Per modificare una configurazione target esistente:
>
> 1. Immetti nuovamente l’ID tenant.
> 2. Riconnettiti a Target.
> 3. Salva la configurazione.

### Modifica la configurazione di Target {#edit-target-configuration}

Per modificare la configurazione di Target, segui questi passaggi:

1. Seleziona una configurazione esistente e fai clic su **Proprietà**.
2. Modifica le proprietà.
3. Seleziona **Riconnetti ad Adobe Target**.
4. Seleziona **Salva e chiudi**.

### Aggiunta di una configurazione a un sito {#add-configuration}

Per applicare una configurazione dell’interfaccia utente touch a un sito, vai a: **Sites** → **Seleziona una pagina del sito** → **Proprietà** → **Avanzate** → **Configurazione** → Seleziona il tenant di configurazione.

## Integrazione di Adobe Target in AEM Sites utilizzando Adobe Launch {#integrate-target-launch}

AEM offre un’integrazione standard con Experience Platform Launch. Aggiungendo l’estensione Adobe Target a Experience Platform Launch, puoi utilizzare le funzioni di Adobe Target sulle pagine web AEM. Il rendering delle librerie di Target viene eseguito solo utilizzando Launch.

>[!NOTE]
>
>I framework esistenti (legacy) continuano a funzionare, ma non possono essere configurati nell’interfaccia utente touch. Adobe consiglia di ricreare le configurazioni di mappatura delle variabili in Launch.

In generale, i passaggi di integrazione sono i seguenti:

1. Creare una proprietà Launch
2. Aggiungi le estensioni richieste
3. Crea un elemento dati (per acquisire i parametri dell’hub contestuale)
4. Crea una regola di pagina
5. Costruire e pubblicare

### Creazione di una proprietà Launch {#create-property}

Una proprietà è un contenitore con estensioni, regole ed elementi dati.

1. Seleziona il pulsante **Nuova proprietà**.
2. Specifica un nome per la proprietà.
3. Come dominio, immetti l’IP/host sul quale desideri caricare la libreria launch.
4. Seleziona il pulsante **Salva**.
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### Aggiunta delle estensioni richieste {#add-extension}

Le **Estensioni** sono il contenitore che gestisce le impostazioni della libreria principale. L’estensione Adobe Target supporta implementazioni lato client tramite l’SDK JavaScript di Target per web morderno, at.js. Aggiungi entrambe le estensioni **Adobe Target** e **Adobe ContextHub**.

1. Seleziona l’opzione Catalogo estensioni e cerca Target nel filtro.
2. Seleziona **Adobe Target** at.js e fai clic sull’opzione Installa.
   ![Ricerca Target](assets/search_ext1.png "Ricerca Target")
3. Seleziona il pulsante **Configura**. Osserva la finestra di configurazione con le credenziali dell’account Target importate e la versione at.js per questa estensione.
4. Seleziona **Salva** per aggiungere l’estensione Target alla proprietà Launch. Dovresti essere in grado di visualizzare l’estensione Target elencata nell’elenco **Estensioni installate**.
   ![Salva estensione](assets/configure_extension1.png "Salva estensione")
5. Ripeti i passaggi precedenti per cercare l’estensione **Adobe ContextHub** e installarla (è necessaria per l’integrazione con i parametri contexthub, in base al targeting da eseguire).

### Creare un elemento dati {#data-element}

Gli **elementi dati** sono i segnaposto con cui puoi mappare i parametri context hub.

1. Seleziona **Elementi dati**.
2. Seleziona **Aggiungi elemento dati**.
3. Fornisci il nome dell’elemento dati e mappalo rispetto a un parametro context hub.
4. Seleziona **Salva**.
   ![Elemento dati](assets/data_elem1.png "Elemento dati")

### Creare una regola di pagina {#page-rule}

In **Regola** viene definita e ordinata una sequenza di azioni, che vengono eseguite sul sito, per ottenere il targeting.

1. Aggiungi una serie di azioni come esemplificato nella schermata acquisita.
   ![Azioni](assets/rules1.png "Azioni")
2. In Aggiungi parametri a tutte le MBox, aggiungi l’elemento dati configurato in precedenza (vedi l’elemento dati precedente) al parametro che verrà inviato nella chiamata mBox.
   ![Azioni](assets/map_data1.png "Mbox")

### Costruire e pubblicare {#build-publish}

Per informazioni su come creare e pubblicare, consulta questa [pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html?lang=it).

## Modifiche alla struttura del contenuto tra le configurazioni di interfaccia utente classica e touch {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>Cambia</th>
    <th>Configurazione interfaccia utente classica</th>
    <th>Configurazione interfaccia utente touch</th>
    <th>Conseguenze</th>
  </tr>
  <tr>
    <td>Posizione della configurazione Target.</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>//conf/tenant/settings/cloudconfigs/target/</td>
    <td> In precedenza erano presenti più configurazioni in /etc/cloudservices/testandtarget, ma ora è presente una singola configurazione in un tenant.</td>
  </tr>
</table>

>[!NOTE]
>
>Le configurazioni legacy sono ancora supportate per la clientela esistente (senza la possibilità di modificarle o crearne di nuove). Le configurazioni legacy fanno parte di pacchetti di contenuti caricati da clienti che utilizzano VSTS.
