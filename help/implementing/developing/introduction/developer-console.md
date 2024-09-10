---
title: AEM as a Cloud Service Developer Console (Beta)
description: Scopri CRX/DE Lite e AEM as a Cloud Service Developer Console
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ea631743af99879d2a76d3a4a78ecf5883f39c69
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>Questo articolo descrive un’esperienza rinnovata per AEM Cloud Service Developer Console, ora in versione beta, e disponibile per alcuni clienti facendo clic su un pulsante nella parte superiore dell’interfaccia classica. Apprezziamo i commenti che puoi inviare a `aemcs-new-devconsole-ui-beta@adobe.com`. Per informazioni sul Developer Console AEM classico, vedere [questo articolo](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

## Strumenti di sviluppo in AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>Il Developer Console di AEM as a Cloud Service non deve essere confuso con il nome simile [*Adobe Developer Console*](https://developer.adobe.com/developer-console/).
>

I clienti possono accedere a CRXDE lite nell’ambiente di sviluppo del livello di authoring, ma non in quello di stage o produzione. Impossibile scrivere nell&#39;archivio immutabile (`/libs`, `/apps`) in fase di esecuzione. Se si tenta di eseguire questa operazione, verranno generati errori.

È invece possibile avviare il Browser dell’archivio da AEM as a Cloud Service Developer Console, fornendo una vista in sola lettura nell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima. Per ulteriori informazioni, vedere [Browser repository](/help/implementing/developing/tools/repository-browser.md).

In AEM as a Cloud Service Developer Console sono disponibili una serie di strumenti per il debug degli ambienti di sviluppo AEM as a Cloud Service per gli ambienti RDE, di sviluppo, di stage e di produzione. L’URL può essere determinato regolando gli URL del servizio Author o Publish nel modo seguente:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Per avviare AEM as a Cloud Service Developer Console in base a un parametro di ambiente descritto di seguito, è possibile utilizzare il seguente comando CLI di Cloud Manager:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Per ulteriori informazioni, vedere [Informazioni sulla versione](/help/release-notes/home.md).

Gli sviluppatori possono generare informazioni sullo stato e risolvere varie risorse.

Come illustrato di seguito, le informazioni sugli stati disponibili includono lo stato di bundle, componenti, configurazioni OSGI, indici Oak, servizi OSGI e processi Sling.

### Bundle OSGi {#osgi-bundles}

![Schermata Nuovi bundle OSGi nella Console per sviluppatori](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* Viene visualizzata una panoramica dei bundle OSGI distribuiti sul tipo di ambiente selezionato. Consente una ricerca full-text.
* È utile ottenere informazioni sullo stato effettivo dei bundle nell’ambiente. Puoi ottenere informazioni quali pacchetti esportati, pacchetti importati, servizi utilizzati e altro ancora.
* Gli sviluppatori desiderano verificare l’ambiente effettivo e verificare se il bundle esegue le operazioni previste.
* **Caso d&#39;uso di esempio:** Nel pacchetto è specificato un intervallo di versioni di una dipendenza. Qualcosa sta andando storto nella dipendenza. Desideri verificare quale versione della dipendenza viene collegata al bundle. Per verificare questo aspetto, vai ai dettagli del bundle e utilizza l’importazione di bundle/pacchetti per controllare quale versione del bundle o del pacchetto viene utilizzata in fase di esecuzione per scoprirlo. Con queste informazioni puoi regolare l’intervallo di versioni della dipendenza Maven o adattare il codice.

### Pacchetti Java {#java-packages}

![Scheda Pacchetti Java nell&#39;interfaccia utente della Console di sviluppo](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Viene visualizzato un prompt di ricerca che consente di cercare i pacchetti attivi nel sistema OSGI dell’ambiente. In questa posizione puoi vedere quale bundle esporta (o fornisce) il pacchetto e quale importa (o utilizza) il pacchetto. Puoi anche verificare la presenza di pacchetti duplicati (stesso pacchetto, versioni diverse), che in alcuni casi possono causare problemi.
* **Caso d&#39;uso di esempio:** un servizio personalizzato che utilizza il [caricatore di classe dinamico](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) sta caricando una classe senza specificare una versione, che viene esportata da più bundle con versioni diverse, causando un cambiamento dell&#39;implementazione e del comportamento. Lo sviluppatore vuole vedere quali pacchetti sono presenti nell’ambiente senza analizzare il modello di funzione, quindi cerca questo pacchetto e visualizza tutte le versioni esportate. Questo offre loro le informazioni per inserire un intervallo di versioni migliore.

### Servlet {#servlets}

![Scheda Servlet nell&#39;interfaccia utente della Console di sviluppo](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* Viene visualizzato un prompt di ricerca in cui è possibile specificare un percorso con i selettori e un&#39;estensione con GET o POST. Fornisce quindi i risultati dei servlet in ordine di preferenza che gestiranno la richiesta in Sling.
* **Caso d&#39;uso di esempio:** disponi di un servlet OSGI che deve essere attivato su una richiesta e stampato qualcosa nella risposta, ma ottieni una risposta vuota. È necessario verificare se un altro servlet ha la precedenza sul servlet a causa di selettori, `resourceType`, estensioni o classificazione più specifici. Cerchi il percorso previsto e scopri che è attivo un altro servlet con una classificazione più alta. Quindi decidi se puoi ottenere il tuo servlet sopra in classifica aggiungendo selettori, ad esempio.

### Servizi {#services}

![Scheda Servizi nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Simile alla visualizzazione Componenti OSGI, ma basata sui servizi. Puoi cercare rapidamente quali servizi vengono forniti con determinate proprietà.

### Componenti OSGi {#osgi-components}

![Scheda Componenti OSGi nell&#39;interfaccia utente della Console per sviluppatori](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* Viene visualizzata una panoramica dei componenti OSGI presenti nel tipo di ambiente selezionato. Consente una ricerca full-text.
* Puoi ottenere lo stato live dei componenti OSGI nell’ambiente. Puoi vedere quali servizi soddisfa, il bundle che lo fornisce e il tipo di attivazione (immediata o ritardata).
* **Caso d&#39;uso di esempio 1:** In qualità di sviluppatore, devi verificare se un componente attivato con una configurazione è attivo o meno in un particolare ambiente, perché non ottieni il comportamento previsto. È sufficiente cercare il componente nella ricerca e verificare se è attivo o meno.
* **Caso d&#39;uso di esempio 2:** Per ulteriori informazioni su Adobe Experience Manager as a Cloud Service, sei interessato a vedere quali componenti pronti all&#39;uso sono presenti nell&#39;ambiente e quali servizi soddisfano. È possibile estrarli nell&#39;elenco dei componenti.

### Integrazioni {#integrations}

![Scheda Integrazioni nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Consente agli amministratori di generare, rinominare ed eliminare credenziali del servizio e token per sviluppatori.

### Archivio {#repository}

* Apre il [Browser dell&#39;archivio](/help/implementing/developing/tools/repository-browser.md).

### Dump/query stato {#status-dumps-queries}

![Scheda Dump di stato/Query nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* Fornisce un’immagine full text o JSON dello stato corrente di bundle, pacchetti, configurazioni, servizi, componenti, processi sling o definizioni oak.
* Questo può essere utile soprattutto se lo sviluppatore ha rilevato uno stato imprevisto e desidera comunicare o documentare questo per altri sviluppatori. Il download dell’immagine fornisce un’istantanea dello stato per riferimento successivo.

### Configurazioni {#configurations}

![Scheda Configurazioni nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* Questo offre un elenco ricercabile delle configurazioni attive nell’ambiente. Puoi vedere quali proprietà vengono fornite dalle configurazioni estraendo la pagina dei dettagli.
* **Caso d&#39;uso di esempio:** uno sviluppatore vuole assicurarsi che le configurazioni specificate siano effettivamente presenti nell&#39;ambiente. Se la configurazione non è presente, è possibile controllare il modello di feature, la modalità di esecuzione della configurazione o la cartella.

Per i programmi di produzione, l’accesso a AEM as a Cloud Service Developer Console è definito dal &quot;Cloud Manager - Ruolo Sviluppatore&quot; in Adobe Admin Console, mentre per i programmi sandbox, AEM as a Cloud Service Developer Console è disponibile per qualsiasi utente con un profilo di prodotto che gli consente di accedere a AEM as a Cloud Service. Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo Sviluppatore&quot; per le immagini di stato e il browser dell’archivio e gli utenti devono essere definiti anche nel profilo di prodotto Utenti AEM o Amministratori AEM sui servizi di authoring e pubblicazione per visualizzare i dati di entrambi i servizi. Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, vedere [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).