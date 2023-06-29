---
title: Fase di preparazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica sulla fase di preparazione in Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 5%

---

# Fase di preparazione in Cloud Acceleration Manager {#readiness-phase-cam}

Dopo aver creato un progetto in Cloud Acceleration Manager, ora puoi avviare la valutazione dell’implementazione AEM corrente nella fase di preparazione.

La fase di preparazione include:

* [Analisi delle best practice](#best-practices-analysis)
* [Pianificazione e configurazione](#planning-setup)

Per passare alla fase di preparazione, segui la procedura riportata di seguito:

1. Fai clic sulla scheda del progetto per aprire la pagina di destinazione del progetto.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Accedi a **Preparazione** come illustrato nella figura riportata di seguito.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Per ulteriori informazioni, consulta Creazione e gestione di un progetto in Cloud Acceleration Manager.

## Utilizzo della scheda Analisi delle best practice {#best-practices-analysis}

Per utilizzare la scheda Analisi delle best practice, effettua le seguenti operazioni:

1. Fai clic sul pulsante **Revisione** dal pulsante **Analisi delle best practice** Card.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Segui questi passaggi per scaricare Best Practices Analyzer (BPA).

   >[!NOTE]
   >Per evitare un impatto sulle istanze aziendali critiche, si consiglia di eseguire BPA in un ambiente di authoring il più simile possibile all’ambiente di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di authoring di produzione.

   1. Accedi a [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) e scarica Best Practices Analyzer come file zip.

      >[!NOTE]
      >Revisione [Utilizzo di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) per informazioni su come eseguire BPA.

   1. Esportare il rapporto in formato CSV

1. Fai clic su **Carica nuovo rapporto** per caricare il rapporto BPA in CAM.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >Il report non può essere caricato se sei in modalità di navigazione in incognito nel browser.

1. Dopo aver caricato un nuovo rapporto, visualizzerai il rapporto Analisi delle best practice.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Rivedi ed esplora la dashboard Analisi delle best practice in CAM. Consulta [Analisi delle best practice](#analysis-report) per ulteriori dettagli.

   >[!NOTE]
   >Il caricamento di un nuovo rapporto reimposta tutte le valutazioni.

### Utilizzo dell&#39;anteprima di stampa {#print-preview-cam}

È possibile selezionare l’opzione Anteprima di stampa in Cloud Acceleration Manager per un’anteprima stampabile dei rapporti o per stampare il rapporto in formato PDF per facilitarne la condivisione.

Effettua le seguenti operazioni:

1. Fai clic su **Anteprima di stampa** come illustrato di seguito.

   ![immagine](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Clic su **Anteprima di stampa** apre una nuova scheda con il report visualizzato in un&#39;anteprima stampabile. Fai clic su **Stampa** per stampare il report in un formato PDF.

   >[!IMPORTANT]
   >* Opzione **Salva come PDF** è consigliato e supportato per la funzionalità precedente.
   >* Se si utilizza il pulsante Stampa del browser, verrà stampata una sola pagina.

   ![immagine](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Utilizzo della linea di tendenza della vista {#trendline-view-cam}

Quando carichi più di un rapporto Best Practices Analyzer (BPA) in un progetto, puoi selezionare **Visualizza linea di tendenza** per visualizzare e confrontare i risultati dei rapporti BPA cronologici.

Per visualizzare i rapporti dall’opzione della linea di tendenza, segui i passaggi seguenti:

>[!NOTE]
>Quando carichi più di un rapporto BPA in un progetto, visualizzerai **...** icona.

1. Passa al progetto e fai clic su **Revisione** dal **Analisi delle best practice** scheda in **Preparazione** fase.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Fai clic sul pulsante **...** per visualizzare il menu a discesa.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >Il rapporto visualizzato è sempre il rapporto con la data più recente.

1. Fai clic su **Visualizza linea di tendenza**, come illustrato nella figura seguente.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clic su **Visualizza linea di tendenza** apre la vista della linea di tendenza del rapporto, come illustrato nella figura riportata di seguito.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >Il rapporto Linea di tendenza visualizza i risultati dei rapporti BPA cronologici in una rappresentazione grafica.
   >
   >Sono disponibili due grafici che mostrano la tendenza del:
   >1. **Tendenza dei risultati del rapporto**
   >1. **Tendenza modelli e componenti personalizzati**
   >
   >È possibile aggiungere o modificare la visualizzazione grafica tramite il menu a discesa, come illustrato nella figura seguente:
   >![immagine](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Analisi del rapporto di Best Practices Analyzer {#analysis-report}

Scopri le seguenti schede disponibili nella pagina Report di analisi delle best practice:

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con ogni scheda, è possibile:
>* fai clic su ogni scheda per aprirne la scheda associata
>* applica un segnalibro a tutte le schede dei rapporti (incluso il filtro) per la condivisione o il recupero futuro
>* utilizza l’icona dettagli per visualizzare i dettagli di ciascun risultato del rapporto

#### Proprietà rapporto {#report-properties}

Il **Proprietà rapporto** fornisce informazioni sulle proprietà del rapporto come data, durata, filtri, data di caricamento e dettagli di Adobe Experience Manager (AEM).

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Panoramica dei rapporti {#report-overview}

Questo **Panoramica dei rapporti** La scheda fornisce i risultati del rapporto e i livelli di gravità che si applicano quando si valuta la prontezza di passare a AEM as a Cloud Service, come mostrato nella figura seguente.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Facendo clic su questo report si apre **Report** scheda.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Puoi filtrare il rapporto in base alla rilevanza, al sottotipo o al conteggio.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulta [Interpretazione del rapporto di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) per informazioni sulle categorie e sui livelli di importanza dei risultati.

#### Valutazione delle best practice {#best-practices-assessment}

L’opzione di valutazione delle best practice fornisce una valutazione dell’istanza AEM corrente e indicazioni sui passaggi successivi per adottare le best practice per l’AEM. Da questa scheda è possibile esaminare le informazioni riportate di seguito.

* Panoramica dell’istanza AEM
* Componenti e modelli personalizzati
* Ulteriori risultati
* Query lente
* Attività di manutenzione

#### Valutazione della complessità della migrazione {#migration-complexity-assessment}

L’opzione Valutazione della complessità della migrazione fornisce una valutazione della complessità della migrazione dell’implementazione AEM esistente a AEM as a Cloud Service.

Da questa scheda è possibile esaminare le informazioni riportate di seguito.

* Panoramica dell’istanza AEM
* Valutazione
* Considerazioni sulla migrazione dei contenuti

  ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Utilizzo della scheda Pianificazione e configurazione {#planning-setup}

Segui questa sezione per esplorare la scheda delle attività Pianificazione e configurazione.

1. Fai clic sul pulsante **Visualizza** dal pulsante **Pianificazione E Configurazione** Card. Questa scheda fornisce tutti i contenuti utili per pianificare e configurare la migrazione dell’AEM.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carosello di contenuti mostra tutte le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Eliminazione di un rapporto di analisi delle best practice {#delete-trendline}

Per eliminare un rapporto dalla vista Linea di tendenza, effettua le seguenti operazioni:

>[!IMPORTANT]
>Un rapporto può essere eliminato solo quando in un progetto è stato caricato più di un rapporto.

1. Passa al progetto e fai clic su **Revisione** dal **Analisi delle best practice** scheda in **Preparazione** fase.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Fai clic sul pulsante **...** per visualizzare il menu a discesa.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Fai clic su **Visualizza linea di tendenza**, come illustrato nella figura seguente.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Fai clic sull’icona Elimina da **Rapporto linea di tendenza** schermo.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Fai clic su **Elimina** per confermare l’eliminazione.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## Passaggio successivo {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come creare un progetto, puoi passare alla revisione del passaggio successivo nella [Fase di implementazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
