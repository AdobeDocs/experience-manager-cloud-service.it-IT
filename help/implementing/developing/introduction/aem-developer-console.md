---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Scopri CRXDE Lite e AEM as a Cloud Service Developer Console.
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# Developer Console (Beta) di AEM as a Cloud Service {#developer-console}

>[!NOTE]
>
>Questo articolo descrive un’esperienza rinnovata per AEM Cloud Service Developer Console, attualmente in versione beta. Alcuni clienti possono accedervi facendo clic su un pulsante nella parte superiore dell’interfaccia classica. Adobe ti invita a inviare qualsiasi feedback a `aemcs-new-devconsole-ui-beta@adobe.com`. Per informazioni sul Developer Console classico di AEM, consulta [questo articolo](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

AEM as a Cloud Service Developer Console include una serie di strumenti per il debug in ambienti Cloud. È accessibile tramite un collegamento per ambiente in Cloud Manager.

>[!NOTE]
>Il Developer Console di AEM as a Cloud Service non deve essere confuso con il nome simile [*Adobe Developer Console*](https://developer.adobe.com/developer-console/).
>


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

Gli sviluppatori possono accedere alle funzioni descritte di seguito:

## Bundle OSGi {#osgi-bundles}

![Schermata Nuovi bundle OSGi nella Console per sviluppatori](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* Panoramica dei bundle OSGI distribuiti nel tipo di ambiente selezionato. Consente una ricerca full-text.
* È utile ottenere informazioni sullo stato effettivo dei bundle nell’ambiente. Puoi ottenere informazioni quali pacchetti esportati, pacchetti importati, servizi utilizzati e altro ancora.
* Gli sviluppatori desiderano verificare l’ambiente effettivo e verificare se il bundle esegue le operazioni previste.
* **Caso d&#39;uso di esempio:** Nel pacchetto è specificato un intervallo di versioni di una dipendenza. Qualcosa sta andando storto nella dipendenza. Desideri verificare quale versione della dipendenza viene collegata al bundle. Per verificare, vai ai dettagli del bundle e utilizza l’importazione di bundle/pacchetti per verificare quale versione del bundle o del pacchetto viene utilizzata in fase di esecuzione. Con queste informazioni, puoi regolare l’intervallo di versioni della dipendenza Maven o adattare il codice.

## Pacchetti Java {#java-packages}

![Scheda Pacchetti Java nell&#39;interfaccia utente della Console di sviluppo](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Un prompt di ricerca che puoi utilizzare per cercare i pacchetti attivi nel sistema OSGI dell’ambiente. In questa posizione puoi vedere quale bundle esporta (o fornisce) il pacchetto e quale importa (o utilizza) il pacchetto. Puoi anche verificare la presenza di pacchetti duplicati (stesso pacchetto, versioni diverse), che in alcuni casi possono causare problemi.
* **Caso d&#39;uso di esempio:** un servizio personalizzato che utilizza il [caricatore di classe dinamico](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) carica una classe senza specificare una versione. Poiché più bundle esportano versioni diverse, l’implementazione varia, causando modifiche nel comportamento. Lo sviluppatore vuole verificare quali pacchetti sono presenti nell’ambiente senza analizzare il modello di funzione. Cercano il pacchetto e visualizzano tutte le versioni esportate. Questa funzionalità consente di immettere informazioni per un intervallo di versioni migliore.

## Servlet {#servlets}

![Scheda Servlet nell&#39;interfaccia utente della Console di sviluppo](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* Un prompt di ricerca in cui è possibile specificare un percorso con i selettori e un&#39;estensione con GET o POST. Fornisce quindi i risultati dei servlet in ordine di preferenza, che gestisce la richiesta in Sling.
* **Caso d&#39;uso di esempio:** disponi di un servlet OSGI che deve essere attivato su richiesta e stampare l&#39;output nella risposta. Tuttavia, invece dell’output previsto, la risposta restituisce vuoto. È necessario verificare se un altro servlet ha la precedenza sul servlet a causa di selettori, `resourceType`, estensioni o classificazione più specifici. Cerchi il percorso previsto e scopri che è attivo un altro servlet con una classificazione più alta. Quindi decidi se puoi ottenere il tuo servlet sopra in classifica aggiungendo selettori, ad esempio.

## Servizi {#services}

![Scheda Servizi nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Simile alla visualizzazione Componenti OSGI, ma basata sui servizi. Puoi cercare rapidamente quali servizi vengono forniti con determinate proprietà.

## Componenti OSGi {#osgi-components}

![Scheda Componenti OSGi nell&#39;interfaccia utente della Console per sviluppatori](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* Panoramica dei componenti OSGI presenti nel tipo di ambiente selezionato. Consente una ricerca full-text.
* Puoi ottenere lo stato live dei componenti OSGI nell’ambiente. Puoi vedere quali servizi soddisfa, il bundle che lo fornisce e il tipo di attivazione (immediata o ritardata).
* **Caso d&#39;uso di esempio 1:** In qualità di sviluppatore, è necessario verificare se un componente attivato con una configurazione è attivo in un ambiente specifico. Il motivo è che il comportamento previsto non si verifica. È sufficiente cercare il componente nella ricerca e verificare se è attivo o meno.
* **Caso d&#39;uso di esempio 2:** Vuoi vedere quali componenti predefiniti sono disponibili nell&#39;ambiente e identificare i servizi che supportano. Questa funzionalità consente di saperne di più su Adobe Experience Manager as a Cloud Service. È possibile estrarli nell&#39;elenco dei componenti.

## Integrazioni {#integrations}

![Scheda Integrazioni nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Gli amministratori possono generare, rinominare ed eliminare le credenziali del servizio e i token per sviluppatori.

## Archivio {#repository}

* Apre il [Browser dell&#39;archivio](/help/implementing/developing/tools/repository-browser.md).

## Dump/query stato {#status-dumps-queries}

![Scheda Dump di stato/Query nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* Un’immagine full text o JSON dello stato corrente di bundle, pacchetti, configurazioni, servizi, componenti, processi sling o definizioni di Oak.
* Utile soprattutto se lo sviluppatore ha rilevato uno stato imprevisto e desidera comunicare o documentare questo stato per altri sviluppatori. Il download dell’immagine fornisce un’istantanea dello stato per riferimento successivo.

## Configurazioni {#configurations}

![Scheda Configurazioni nell&#39;interfaccia utente di Console sviluppatori](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* Un elenco ricercabile di configurazioni attive nell’ambiente. Puoi vedere quali proprietà vengono fornite dalle configurazioni estraendo la pagina dei dettagli.
* **Caso d&#39;uso di esempio:** uno sviluppatore vuole assicurarsi che le configurazioni specificate siano effettivamente presenti nell&#39;ambiente. Se la configurazione non è presente, è possibile controllare il modello di feature, la modalità di esecuzione della configurazione o la cartella.

Per i programmi di produzione, il &quot;Cloud Manager - Ruolo Sviluppatore&quot; in Adobe Admin Console controlla l’accesso ad AEM as a Cloud Service Developer Console. Per i programmi sandbox, qualsiasi utente con un profilo di prodotto che concede l’accesso ad AEM può utilizzare Developer Console. Per tutti i programmi, è necessario &quot;Cloud Manager - Ruolo sviluppatore&quot; per le immagini di stato e l’accesso al browser dell’archivio. Per visualizzare i dati dei servizi Author e Publish, gli utenti devono essere assegnati anche al profilo di prodotto Utenti AEM o Amministratori AEM per entrambi i servizi.

Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, vedere [Documentazione di Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

