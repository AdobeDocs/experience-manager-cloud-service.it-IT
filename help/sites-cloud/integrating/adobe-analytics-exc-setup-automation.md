---
title: Integrare Adobe Analytics con Experience Cloud Setup Automation
description: Experience Cloud Setup Automation fornisce un modo semplice e automatizzato di integrare e dotare Experience Manager Sites di Experience Platform Launch e Adobe Analytics di una semplice procedura guidata dell’interfaccia utente. Scopri come utilizzare la configurazione automatica con il tuo sito.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '639'
ht-degree: 100%

---

# Integrare Adobe Analytics con Experience Cloud Setup Automation {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> Questa funzionalità è attualmente in versione beta interna. La versione di Target è prevista nel primo trimestre del 2022.

Experience Cloud Setup Automation fornisce un modo semplice e automatizzato di integrare e dotare Experience Manager Sites di Experience Platform Launch e Adobe Analytics con una semplice procedura guidata dell’interfaccia utente.

L’integrazione di Adobe Analytics con AEM Sites non è mai stata così semplice. Con Experience Cloud Setup Automation, l’installazione, l’integrazione e la strumentazione del sito per acquisire analisi delle prestazioni per comprendere il coinvolgimento e la conversione dei clienti è tutto gestito con pochi clic.

Questo video illustra come un sito AEM viene integrato con Experience Platform Launch e Analytics utilizzando Experience Cloud Setup Automation:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Requisiti 

La configurazione dell’automazione è progettata per funzionare con un sito AEM costruito utilizzando [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) con il [Livello dati client di Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=it) abilitato. È possibile generare un nuovo sito con queste funzioni abilitate automaticamente utilizzando [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) o creando un sito utilizzando un [Modello di sito](/help/journey-sites/quick-site/create-site.md).

## Come impostare

1. Passa a **Sites** e seleziona la pagina principale del sito da integrare con Adobe Analytics.
1. Espandi il menu della barra laterale e tocca **Configurazione di Analytics**.

   Questa è una nuova opzione nella barra laterale che aprirà un pannello che fornirà i controlli e lo stato di Experience Cloud Setup Automation.
1. Tocca il pulsante **Integra Analytics**.
1. Nella finestra di dialogo risultante, fornisci un nome per **ID suite di rapporti**.

   Questa stringa verrà utilizzata per creare una nuova [ID suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=it) in Adobe Analytics come archivio dati per i dati di analisi del sito AEM selezionato. Alla stringa fornita verranno aggiunti l’ambiente e gli identificatori di livello per garantire l’univocità.

1. Aggiorna la pagina e il pannello e tocca **Verifica stato integrazione** per controllare lo stato dell’automazione.

   La configurazione dell’automazione avviene in modo asincrono. **Verifica stato integrazione** mostrerà lo stato corrente dell’integrazione.

   * **In corso**: indica che il processo è in esecuzione.
   * **Integrazione completa**: indica che il processo ha completato l’integrazione di Analytics e Launch, la configurazione delle estensioni e delle regole di lancio e la creazione della nuova suite di rapporti in Adobe Analytics.
   * **Errore**: indica che il processo automatizzato non è stato completato correttamente. Controlla i file di registro per questo processo facendo clic sul collegamento Registri.

## Convalidare la configurazione AEM

Una volta completata l’automazione, verifica che il tuo sito stia attivando gli eventi di Analytics.

1. Apri una pagina del sito utilizzando **Editor siti**.
1. Utilizza l’opzione **Visualizza come pubblicato** per caricare una versione pubblicata della pagina.
1. Utilizza gli strumenti di sviluppo del browser per controllare il traffico di rete e che **Launch** e i file `AppMeasurement.js` vengano ora caricati.
1. Inspect è la console del browser per visualizzare che gli eventi a livello di pagina e componente vengano attivati e raccolti dal livello dati del client Adobe.

## Convalidare la configurazione di Analytics

Quindi, passa ad Adobe Analytics per visualizzare i dati che fluiscono dagli eventi del sito AEM.

1. Passa ad Adobe Analytics nella stessa organizzazione IMS del sito AEM.
1. Crea un nuovo rapporto di panoramica per spostarsi da AEM Sites a **Rapporti** > **Coinvolgimento** > **Adobe Experience Manager** > **Panoramica delle prestazioni del sito**.
1. Tocca **Apri rapporto**.
1. Seleziona la **ID suite di rapporti** che corrisponde al nome della suite di rapporti utilizzato nell’esercizio precedente.
1. Nel tempo puoi visualizzare il flusso di dati di analisi nel nuovo modello.

   >[!NOTE]
   >
   > Con una nuova integrazione, potrebbero essere necessarie alcune ore prima che il rapporto venga compilato con i dati.
