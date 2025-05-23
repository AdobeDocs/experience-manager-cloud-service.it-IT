---
title: Integrare Adobe Analytics con Experience Cloud Setup Automation
description: Experience Cloud Setup Automation fornisce un modo semplice e automatizzato di integrare e dotare Experience Manager Sites di Experience Platform Tags e Adobe Analytics con una semplice procedura guidata dell’interfaccia utente. Scopri come utilizzare la configurazione automatica con il tuo sito.
feature: Integration
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
solution: Experience Manager Sites
source-git-commit: 4a3e65ef6a8aa08c8bc78db31f94272334994ac5
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 86%

---

# Integrare Adobe Analytics con Experience Cloud Setup Automation {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
>La funzionalità Experience Cloud Setup Automation è obsoleta.

Experience Cloud Setup Automation fornisce un modo semplice e automatizzato di integrare e dotare Experience Manager Sites di Experience Platform Tags e Adobe Analytics con una semplice procedura guidata dell’interfaccia utente.

L’integrazione di Adobe Analytics con AEM Sites non è mai stata così semplice. Con Experience Cloud Setup Automation, l’installazione, l’integrazione e la strumentazione del sito per acquisire analisi delle prestazioni per comprendere il coinvolgimento e la conversione dei clienti è tutto gestito con pochi clic.

Questo video illustra come un sito AEM viene integrato con Experience Platform Tags e Analytics utilizzando Experience Cloud Setup Automation:

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## Requisiti 

La configurazione dell’automazione è progettata per funzionare con un sito AEM costruito utilizzando [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) con il [Livello dati client di Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=it) abilitato. È possibile generare un nuovo sito con queste funzioni abilitate automaticamente utilizzando [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) o creando un sito utilizzando un [Modello di sito](/help/journey-sites/quick-site/create-site.md).

## Prerequisiti {#prerequisites}

Prima di utilizzare questa funzione, è importante seguire queste istruzioni per garantire che i servizi necessari come prerequisiti siano stati configurati correttamente nell’ambiente:

1. Accedi ad Adobe Admin Console (https://adminconsole.adobe.com/).
1. Verifica che nell’angolo in alto a destra sia selezionato l’ID organizzazione IMS corretto.
1. Fai clic sull’opzione di navigazione Prodotti.
1. Verifica che sia stato effettuato il provisioning di “Adobe Experience Manager as a Cloud Service” per l’organizzazione IMS.
1. Verifica che sia stato effettuato il provisioning di “Adobe Analytics” per l’organizzazione IMS.
1. Passa a Cloud Manager (https://experience.adobe.com/cloud-manager).
1. Seleziona il Programma desiderato.
1. Controlla che nell’ambiente sia installata l’ultima versione di Cloud Service (in caso contrario, seleziona Aggiorna nelle opzioni del menu).
1. Esegui una pipeline full-stack in Cloud Manager.

L’ambiente ora dovrebbe essere pronto per la configurazione dell’automazione di Experience Cloud.

## Come impostare

1. Passa a **Sites** e seleziona la pagina principale del sito da integrare con Adobe Analytics.
1. Espandere il menu della barra laterale e selezionare **Imposta Analytics**.

   Questa è una nuova opzione nella barra laterale che apre un pannello che fornisce i controlli e lo stato per Experience Cloud Setup Automation.
1. Selezionare il pulsante **Integra Analytics**.
1. Nella finestra di dialogo risultante, fornisci un nome per **ID suite di rapporti**.

   Questa stringa viene utilizzata per creare un [ID suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=it) in Adobe Analytics come archivio dati per i dati di analisi del sito AEM selezionato. Alla stringa fornita verranno aggiunti l’ambiente e gli identificatori di livello per garantirne l’univocità.

1. Aggiorna la pagina e il pannello e seleziona **Verifica stato integrazione** per controllare lo stato dell&#39;automazione.

   La configurazione dell’automazione avviene in modo asincrono. **Verifica stato integrazione** mostrerà lo stato corrente dell’integrazione.

   * **In corso**: indica che il processo è in esecuzione.
   * **Integrazione completa**: indica che il processo ha completato l’integrazione di Analytics e Tags, la configurazione delle estensioni e delle regole di Tags e la creazione della nuova suite di rapporti in Adobe Analytics.
   * **Errore**: indica che il processo automatizzato non è stato completato correttamente. Controlla i file di registro per questo processo facendo clic sul collegamento Registri.

## Convalidare la configurazione AEM

Una volta completata l’automazione, verifica che il tuo sito stia attivando gli eventi di Analytics.

1. Apri una pagina del sito utilizzando **Editor siti**.
1. Utilizza l’opzione **Visualizza come pubblicato** per caricare una versione pubblicata della pagina.
1. Utilizza gli strumenti per gli sviluppatori del browser per controllare il traffico di rete e che **Tags** e i file `AppMeasurement.js` vengano ora caricati.
1. Inspect è la console del browser per visualizzare che gli eventi a livello di pagina e componente vengano attivati e raccolti dal livello dati del client Adobe.

## Convalidare la configurazione di Analytics

Quindi, passa ad Adobe Analytics per visualizzare i dati che fluiscono dagli eventi del sito AEM.

1. Passa ad Adobe Analytics nella stessa organizzazione IMS del sito AEM.
1. Crea un nuovo rapporto di panoramica per spostarsi da AEM Sites a **Rapporti** > **Coinvolgimento** > **Adobe Experience Manager** > **Panoramica delle prestazioni del sito**.
1. Seleziona **Apri report**.
1. Seleziona la **ID suite di rapporti** che corrisponde al nome della suite di rapporti utilizzato nell’esercizio precedente.
1. Nel tempo puoi visualizzare il flusso di dati di analisi nel nuovo modello.

   >[!NOTE]
   >
   > Con una nuova integrazione, potrebbero essere necessarie alcune ore prima che il rapporto venga compilato con i dati.
