---
title: Integrare Adobe Analytics con Experience Cloud Setup Automation
description: Experience Cloud Setup Automation fornisce un modo semplice e automatizzato di integrare e dotare Experience Manager Sites di Experience Platform Launch e Adobe Analytics di una semplice interfaccia guidata dell’interfaccia utente. Scopri come utilizzare la configurazione automatica con il tuo sito.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
source-git-commit: 6c84c0eff6392f1f86c18c9daf15c402c4d9e778
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Integrare Adobe Analytics con Experience Cloud Setup Automation {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> Questa funzionalità è attualmente in versione beta interna. La versione di Target è nel primo trimestre del 2022.

Experience Cloud Setup Automation fornisce un modo semplice e automatizzato di integrare e dotare Experience Manager Sites di Experience Platform Launch e Adobe Analytics di una semplice interfaccia guidata dell’interfaccia utente.

L’integrazione di Adobe Analytics con AEM Sites non è mai stata così semplice. Con Experience Cloud Setup Automation, l&#39;installazione, l&#39;integrazione e la strumentazione del sito per acquisire analisi delle prestazioni per comprendere il coinvolgimento e la conversione dei clienti è tutto gestito con pochi clic.

Questo video illustra come un sito AEM viene integrato con Experience Platform Launch e Analytics utilizzando l’automazione dell’installazione di Experienci Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Requisiti

La configurazione di automazione è progettata per funzionare con un sito AEM costruito utilizzando [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) con [Livello dati client di Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) abilitato. È possibile generare un nuovo sito con queste funzioni abilitate automaticamente utilizzando [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) o creando un sito utilizzando un [Modello del sito](/help/journey-sites/quick-site/create-site.md).

## Come impostare

1. Passa a **Sites** e seleziona la directory principale del sito da integrare con Adobe Analytics.
1. Espandi il menu della barra laterale e tocca **Configurazione di Analytics**.

   Questa è una nuova opzione nella barra laterale che aprirà un pannello che fornirà i controlli e lo stato per Experience Cloud Setup Automation.
1. Tocca **Integrare Analytics** pulsante .
1. Nella finestra di dialogo risultante, fornisci un nome per **ID suite di rapporti**.

   Questa stringa verrà utilizzata per creare una nuova [ID suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) in Adobe Analytics come archivio dati per i dati di analisi per il sito AEM selezionato. Alla stringa fornita verrà aggiunto l&#39;ambiente e gli identificatori di livello per garantire l&#39;univocità.

1. Aggiorna la pagina e il pannello e tocca **Verifica stato integrazione** per controllare lo stato dell&#39;automazione.

   La configurazione dell&#39;automazione avviene in modo asincrono. La **Verifica stato integrazione** mostrerà lo stato corrente dell&#39;integrazione.

   * **In corso** - indica che il processo è in esecuzione.
   * **Integrazione completa** - indica che il processo ha completato l’integrazione di Analytics e Launch, la configurazione delle estensioni Launch e delle regole Launch e la creazione della nuova suite di rapporti in Adobe Analytics.
   * **Errore** - indica che il processo automatizzato non è stato completato correttamente. Controlla i file di registro per questo lavoro facendo clic sul collegamento Registri .

## Convalida AEM configurazione

Una volta completata l&#39;automazione, verifica che il tuo sito stia attivando gli eventi di Analytics.

1. Apri una pagina del sito utilizzando **Editor siti**.
1. Utilizza la **Visualizza come pubblicato** per caricare una versione pubblicata della pagina.
1. Utilizzare gli strumenti di sviluppo del browser per controllare il traffico di rete e che **Launch** e `AppMeasurement.js` I file vengono ora caricati.
1. Inspect è la console del browser per visualizzare che gli eventi a livello di pagina e componente vengono attivati e raccolti da Adobe Client Data Layer.

## Convalida la configurazione di Analytics

Quindi, passa ad Adobe Analytics per visualizzare i dati che scorrono dagli eventi del sito AEM.

1. Passa ad Adobe Analytics nella stessa organizzazione IMS del sito AEM.
1. Creare un nuovo rapporto di panoramica per AEM Sites che consente di spostarsi a **Rapporti** > **Coinvolgimento** > **Adobe Experience Manager** > **Panoramica delle prestazioni del sito**.
1. Tocca **Apri rapporto**.
1. Seleziona la **ID suite di rapporti** che corrisponde al nome della suite di rapporti utilizzato nell’esercizio precedente.
1. Nel tempo puoi visualizzare il flusso di dati analitici nel nuovo modello.

   >[!NOTE]
   >
   > Con una nuova integrazione, potrebbero essere necessarie alcune ore prima che il rapporto venga compilato con i dati.
