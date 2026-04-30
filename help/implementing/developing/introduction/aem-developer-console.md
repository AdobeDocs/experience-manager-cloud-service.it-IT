---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Scopri AEM as a Cloud Service Developer Console e il suo set di strumenti di sola lettura per il debug degli ambienti cloud.
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 51c14ba3c15e0136911003752253d21ed673a0eb
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---


# Developer Console (Beta) di AEM as a Cloud Service {#developer-console}

AEM as a Cloud Service Developer Console include un set di strumenti di sola lettura per il debug degli ambienti cloud. È accessibile tramite un collegamento per ambiente in Cloud Manager e offre funzioni per visualizzare bundle, impostazioni OSGi, servizi e servlet e altro ancora.

>[!NOTE]
>
>Questo articolo descrive un’esperienza rinnovata per AEM Cloud Service Developer Console, attualmente in versione beta.
>
>* Un gruppo limitato di utenti può accedere alla nuova console tramite un pulsante nella parte superiore dell’attuale Developer Console.
>* Adobe è lieta di ricevere qualsiasi feedback che puoi inviare a `aemcs-new-devconsole-ui-beta@adobe.com`.
>* Per la documentazione sul Developer Console AEM corrente, consulta [questo articolo.](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)
>* Il Developer Console di AEM as a Cloud Service non deve essere confuso con il nome simile [*Adobe Developer Console*.](https://developer.adobe.com/developer-console/)

>[!TIP]
>
>Developer Console è di sola lettura. Se stai lavorando allo sviluppo locale utilizzando SDK e hai bisogno di modificare le impostazioni OSGi o il contenuto dell’archivio, puoi utilizzare:
>
>* [CRXDE Lite](/help/implementing/developing/tools/crxde.md)

<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

## Prerequisiti {#prerequisites}

Developer Console è accessibile solo agli utenti con determinati ruoli in determinati programmi.

* Per i programmi di produzione, il &quot;Cloud Manager - Ruolo Sviluppatore&quot; nel Adobe Admin Console controlla l’accesso a Developer Console.
* Per i programmi sandbox, qualsiasi utente con un profilo di prodotto che concede l’accesso ad AEM può utilizzare Developer Console.
* Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo sviluppatore&quot; per le immagini di stato e l’accesso al browser dell’archivio.

Per visualizzare i dati dei servizi di authoring e pubblicazione, gli utenti devono essere assegnati anche al &quot;Profilo di prodotto Utenti AEM&quot; o &quot;Amministratori AEM&quot; in entrambi i servizi.

Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, vedere la [documentazione di Cloud Manager.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## Scheda Bundle OSGi {#osgi-bundles}

La scheda **Bundle OSGi** fornisce una panoramica dei bundle OSGi distribuiti nell&#39;ambiente selezionato e offre una ricerca full-text.

![Nuova schermata dei bundle OSGi in Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* La scheda fornisce informazioni sullo stato effettivo dei bundle nell’ambiente, ad esempio pacchetti esportati, pacchetti importati, servizi utilizzati e altro ancora.
* È ideale controllare lo stato dei bundle per verificare se eseguono le operazioni previste.

**Caso d&#39;uso di esempio:** Supponiamo che tu specifichi un intervallo di versioni per una dipendenza nel bundle. Ma qualcosa non va nella dipendenza e devi controllare quale versione della dipendenza è effettivamente utilizzata dal bundle. Per verificare, apri Developer Console e fai clic sul nome di un bundle nella scheda **Bundle OSGi** per accedere ai dettagli del bundle, quindi utilizza il pannello a soffietto **Importazione dei bundle** per verificare quale versione del bundle o del pacchetto viene utilizzata in fase di esecuzione. Con queste informazioni, puoi regolare l’intervallo di versioni della dipendenza Maven o adattare il codice.

## Scheda Pacchetti Java {#java-packages}

La scheda **Pacchetti Java** offre un campo di ricerca per cercare i pacchetti attivi nel sistema OSGi dell&#39;ambiente.

![Scheda Pacchetti Java nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Puoi vedere quale bundle esporta (o fornisce) il pacchetto e quali bundle importano (o utilizzano) il pacchetto.
* Puoi anche verificare la presenza di pacchetti duplicati (stesso pacchetto, versioni diverse), che in alcuni casi possono causare problemi.

**Caso d&#39;uso di esempio:** Supponiamo che un servizio personalizzato che utilizza il [caricatore di classe dinamico](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) carichi una classe senza specificare una versione. Poiché più bundle esportano versioni diverse, l’implementazione varia, causando modifiche nel comportamento. Si desidera verificare quali pacchetti sono presenti nell&#39;ambiente senza analizzare il modello di feature. Utilizzando questa scheda è possibile cercare il pacchetto e visualizzare tutte le versioni esportate e quindi utilizzare un intervallo di versioni migliore.

## Scheda Configurazioni {#configurations}

La scheda **Configurazioni** offre un elenco ricercabile delle configurazioni attive nell&#39;ambiente. Per vedere quali proprietà vengono fornite da ciascuna configurazione, fai clic su di essa e visualizza la pagina dei dettagli.

![Scheda Configurazioni nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* **Caso d&#39;uso di esempio:** Supponiamo che si desideri verificare che le configurazioni specificate siano effettivamente presenti nell&#39;ambiente. Se si cerca nella scheda **Configurations** della console e la configurazione non è presente, è possibile controllare il modello di funzionalità, la modalità di esecuzione della configurazione o la cartella.

## Scheda Servlet {#servlets}

La scheda **Servlet** offre un campo di ricerca in cui è possibile specificare un percorso con i selettori e un&#39;estensione con GET o POST. Fornisce quindi un elenco di servlet in ordine di preferenza che gestisce la richiesta in Sling.

![Scheda Servlet nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

**Caso d&#39;uso di esempio:** supponiamo che tu disponga di un servlet OSGi che deve essere attivato su richiesta e stampare l&#39;output nella risposta. Tuttavia, invece dell’output previsto, si ottiene una risposta vuota. È necessario verificare se un altro servlet ha la precedenza sul servlet a causa di selettori, `resourceType`, estensioni o classificazione più specifici. Cerchi il percorso previsto e scopri che è attivo un altro servlet con una classificazione più alta. Puoi quindi decidere se aumentare la classificazione del servlet aggiungendo, ad esempio, selettori.

## Scheda Servizi {#services}

La scheda **Servizi** fornisce una panoramica dei servizi presenti nell&#39;ambiente selezionato e offre una ricerca full-text.

![Scheda Servizi nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/services-dev-console.png)

Fai clic su un servizio per visualizzarne i dettagli.

## Scheda Componenti OSGi {#osgi-components}

La scheda **Componenti OSGi** fornisce una panoramica dei componenti OSGi presenti nel tipo di ambiente selezionato e offre una ricerca full-text. Puoi visualizzare lo stato live dei componenti OSGi nell’ambiente e quali servizi soddisfa, il bundle che lo fornisce e il tipo di attivazione (immediata o ritardata).

![Scheda Componenti OSGi nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* **Caso d&#39;uso di esempio 1:** Supponiamo che sia necessario verificare se un componente attivato con una configurazione è attivo in un ambiente specifico poiché si sta verificando un comportamento imprevisto. È sufficiente cercare il componente nella ricerca e verificare se è attivo o meno.
* **Caso d&#39;uso di esempio 2:** Supponiamo che tu voglia vedere quali componenti pronti all&#39;uso sono disponibili nell&#39;ambiente e identificare i servizi che supportano per saperne di più su Adobe Experience Manager as a Cloud Service. Puoi controllare i componenti nell’elenco dei componenti.

## Scheda Integrazioni {#integrations}

La scheda **Integrazioni** consente agli amministratori di generare, rinominare ed eliminare le credenziali del servizio e i token per sviluppatori.

![Scheda Integrazioni nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

## Scheda Archivio {#repository}

La scheda **Archivio** apre il browser dell&#39;archivio [.](/help/implementing/developing/tools/repository-browser.md)

## Scheda Dump/Query di stato {#status-dumps-queries}

La scheda **Duplicazioni di stato/query** ti consente di scaricare un’immagine full-text o JSON dello stato corrente di bundle, pacchetti, configurazioni, servizi, componenti, processi sling o definizioni di Oak.

![Scheda Dump di stato/Query nell&#39;interfaccia utente di Developer Console](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

È inoltre possibile aprire lo strumento Prestazioni query [.](/help/operations/query-and-indexing-best-practices.md#query-performance-tool)

* **Caso d&#39;uso di esempio:** Questa scheda è particolarmente utile se si verifica uno stato imprevisto e si desidera comunicare o documentare tale stato per altri sviluppatori. Il download dell’immagine fornisce un’istantanea dello stato per riferimento successivo.
