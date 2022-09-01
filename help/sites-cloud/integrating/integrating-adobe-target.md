---
title: Integrazione con Adobe Target
description: 'Integrazione con Adobe Target '
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 99%

---

# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte di Adobe Marketing Cloud, Adobe Target ti consente di aumentare la rilevanza dei contenuti attraverso il targeting e la misurazione su tutti i canali. L’integrazione di Adobe Target e AEM as a Cloud Service richiede:

* utilizzo dell’interfaccia utente touch per creare una configurazione Target in AEM as a Cloud Service (è richiesta la configurazione IMS).
* aggiunta e configurazione di Adobe Target come estensione in [Adobe Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=it).

Adobe Launch è necessario per gestire le proprietà lato client sia per Analytics sia per Target nelle pagine AEM (librerie/tag JS). Detto questo, l’integrazione con Launch è necessaria per il &quot;targeting dell&#39;esperienza&quot;. Per l’esportazione dei frammenti di esperienza in Target, sono necessarie solo la configurazione Adobe Target e IMS.

>[!NOTE]
>
>I clienti Adobe Experience Manager as a Cloud Service che non dispongono di un account Target esistente possono richiedere l’accesso a Target Foundation Pack per Experience Cloud. Foundation Pack fornisce un uso limitato del volume di Target.

## Creazione della configurazione di Adobe Target {#create-configuration}

1. Passa a **Strumenti** → **Cloud Services**.
   ![Navigazione](assets/cloudservice1.png "Navigazione")
2. Seleziona **Adobe Target**.
3. Seleziona il pulsante **Crea**.
   ![Crea](assets/tenant1.png "Crea")
4. Compila i dettagli (vedi sotto) e seleziona **Connetti**.
   ![Connetti](assets/open_screen1.png "Connetti")

### Configurazione IMS {#ims-configuration}

Per integrare correttamente Target con AEM e Launch è necessaria una configurazione IMS sia per Launch che per Target. Anche se la configurazione IMS per Launch è preconfigurata in AEM as a Cloud Service, è necessario creare la configurazione IMS di Target (dopo il provisioning di Target). Fai riferimento a [questo video](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) e [questa pagina](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html?lang=it) per scoprire come creare la configurazione IMS di Target.

### ID tenant e codice client di Adobe Target {#tenant-client}

Durante la configurazione dei campi ID tenant e Codice client di Adobe Target, tieni presente quanto segue:

1. Per la maggior parte dei clienti, l’ID tenant e il codice client sono gli stessi. Ciò significa che entrambi i campi contengono le stesse informazioni e sono identici. Assicurati di inserire l’ID tenant in entrambi i campi.
2. Per motivi di legacy, puoi anche immettere valori diversi nei campi ID tenant e Codice client.

In entrambi i casi, tieni presente che:

* Per impostazione predefinita, anche il codice client (se aggiunto per primo) viene copiato automaticamente nel campo ID tenant.
* Hai la possibilità di modificare il set di ID tenant predefinito.
* Di conseguenza, le chiamate di backend a Target saranno basate sull’ID tenant e le chiamate lato client a Target saranno basate sul codice client.

Come indicato in precedenza, il primo caso è il più comune per AEM as a Cloud Service. In entrambi i casi, assicurati che **entrambi** i campi contengano le informazioni corrette a seconda dei requisiti.

>[!NOTE]
>
> Per modificare una configurazione target esistente:
>
> 1. Immetti nuovamente l&#39;ID tenant.
> 2. Riconnetti a Target.
> 3. Salva la configurazione.


### Modifica la configurazione di Target {#edit-target-configuration}

Per modificare la configurazione di Target, segui questi passaggi:

1. Seleziona una configurazione esistente e fai clic su **Proprietà**.
2. Modifica le proprietà.
3. Seleziona **Riconnetti ad Adobe Target**.
4. Seleziona **Salva e chiudi**.

### Aggiunta di una configurazione a un sito {#add-configuration}

Per applicare una configurazione dell&#39;interfaccia utente touch a un sito, vai a: **Sites** → **Seleziona una pagina del sito** → **Proprietà** → **Avanzate** → **Configurazione** → Seleziona il tenant di configurazione.

## Integrazione di Adobe Target sui siti AEM utilizzando Adobe Launch {#integrate-target-launch}

AEM offre un’integrazione standard con Experience Platform Launch. Aggiungendo l’estensione Adobe Target a Experience Platform Launch, puoi utilizzare le funzioni di Adobe Target sulle pagine web AEM. Il rendering delle librerie di Target verrà eseguito solo utilizzando Launch.

>[!NOTE]
>
>I framework esistenti (legacy) continuano a funzionare, ma non possono essere configurati nell’interfaccia utente touch. È consigliabile ricreare le configurazioni di mappatura delle variabili in Launch.

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

**Estensioni** è il contenitore che gestisce le impostazioni della libreria principale. L&#39;estensione Adobe Target supporta implementazioni lato client tramite Target JavaScript SDK per web, at.js moderno. È necessario aggiungere entrambe le estensioni **Adobe Target** e **Adobe ContextHub**.

1. Seleziona l’opzione Catalogo estensioni e cerca Target nel filtro.
2. Seleziona **Adobe Target** at.js e fai clic sull’opzione Installa.
   ![Ricerca Target](assets/search_ext1.png "Ricerca Target")
3. Seleziona il pulsante **Configura**. Osserva la finestra di configurazione con le credenziali dell’account Target importate e la versione at.js per questa estensione.
4. Seleziona **Salva** per aggiungere l’estensione Target alla proprietà Launch. Dovresti essere in grado di visualizzare l’estensione Target elencata nell’elenco **Estensioni installate**.
   ![Salva estensione](assets/configure_extension1.png "Salva estensione")
5. Ripeti i passaggi precedenti per cercare l’estensione **Adobe ContextHub** e installarla (è necessaria per l’integrazione con i parametri contexthub, in base al target da eseguire).

### Creare un elemento dati {#data-element}

Gli **elementi dati** sono i segnaposto con cui puoi mappare i parametri context hub.

1. Seleziona **Elementi dati**.
2. Seleziona **Aggiungi elemento dati**.
3. Fornisci il nome dell’elemento dati e mappalo rispetto a un parametro context hub.
4. Seleziona **Salva**.
   ![Elemento dati](assets/data_elem1.png "Elemento dati")

### Creare una regola di pagina {#page-rule}

In **Regola** viene definita e ordinata una sequenza di azioni, che vengono eseguite sul sito, per ottenere un target.

1. Aggiungi una serie di azioni come esemplificato nella schermata acquisita.
   ![Azioni](assets/rules1.png "Azioni")
2. In Aggiungi parametri a tutte le Mbox aggiungi l’elemento dati configurato in precedenza (vedi l’elemento dati sopra) al parametro che verrà inviato nella chiamata mbox.
   ![Azioni](assets/map_data1.png "Mbox")

### Costruire e pubblicare {#build-publish}

Per informazioni su come costruire e pubblicare, consulta questa [pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html?lang=it).

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
    <td>/conf/tenant/settings/cloudservices/target/</td>
    <td> In precedenza erano presenti più configurazioni presso /etc/cloudservices/testandtarget, ma ora è presente una singola configurazione con un tenant.</td>
  </tr>
</table>

>[!NOTE]
>
>Le configurazioni legacy sono ancora supportate per i clienti esistenti (senza la possibilità di modificarle o crearne di nuove). Le configurazioni legacy faranno parte di pacchetti di contenuti caricati dai clienti che utilizzano VSTS.
