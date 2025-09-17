---
title: Fase di preparazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica sulla fase di preparazione in Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 3a0576e62518240b89290a75752386128b1ab082
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 7%

---

# Fase di preparazione in Cloud Acceleration Manager {#readiness-phase-cam}

Dopo aver creato un progetto in Cloud Acceleration Manager (CAM), ora puoi avviare la valutazione dell’implementazione Adobe Experience Manager (AEM) corrente nella fase di preparazione.

La fase di preparazione include:

* [Analisi delle best practice](#best-practices-analysis)
* [Pianificazione e installazione](#planning-setup)

Per passare alla fase di preparazione, segui la procedura riportata di seguito:

1. Fai clic sulla scheda del progetto.

   ![Scheda Progetto](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Nella pagina di destinazione del progetto, passa alla sezione **Preparazione**, come illustrato nella figura seguente.

   ![Preparazione](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Per ulteriori informazioni, consulta Creazione e gestione di un progetto in Cloud Acceleration Manager.

## Utilizzo della scheda di analisi di Best Practice {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="Rapporto di analisi di Best Practices"
>abstract="Il rapporto di Best Practices Analyzer può essere caricato su CAM per fornire un’analisi sulla migrazione ad AEM as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="Utilizzo di Best Practices Analyzer"

1. Fai clic su **Rivedi** dalla scheda **Analisi delle best practice**.

   ![Analisi delle best practice - Revisione](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Scarica Best Practices Analyzer (BPA).

   >[!NOTE]
   >Per evitare un impatto sulle istanze aziendali critiche, Adobe consiglia di eseguire BPA in un ambiente di authoring. L’ambiente deve essere il più simile possibile all’ambiente di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di authoring di produzione.

   1. Passa al portale [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*) e scarica Best Practices Analyzer come file zip.

      >[!NOTE]
      >Rivedi [Utilizzo di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html#imp-considerations) per scoprire come eseguire BPA.

1. In CAM, fai clic su **Ottieni chiave di caricamento**, in modo da ottenere la chiave utilizzata per configurare il sistema per caricare automaticamente i rapporti BPA direttamente in CAM.

   ![Ottieni chiave di caricamento](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >Il rapporto può ancora essere caricato manualmente, ma l’utilizzo della Chiave di caricamento semplifica l’operazione. Nota che il rapporto non può essere caricato manualmente se la sua dimensione è pari o superiore a circa 200 MB. Inoltre, il rapporto non può essere caricato utilizzando la modalità di navigazione in incognito del browser.

1. Dopo aver caricato un nuovo rapporto, puoi vedere il rapporto Analisi delle best practice in CAM.

   ![Rapporto sull&#39;analisi delle best practice](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >Se vengono caricati più rapporti diversi, il rapporto visualizzato in dettaglio è sempre quello con la data di creazione più recente (non la data di caricamento).

1. Rivedi ed esplora la dashboard Analisi delle best practice in CAM. Per ulteriori dettagli, consulta [Analisi delle best practice](#analysis-report).

   >[!NOTE]
   >Il caricamento di un nuovo rapporto ripristina tutte le valutazioni se questo è più recente del rapporto caricato in precedenza.

### Utilizzo dell&#39;anteprima di stampa {#print-preview-cam}

Puoi selezionare l’opzione Anteprima di stampa in Cloud Acceleration Manager per un’anteprima stampabile dei rapporti o per stampare il rapporto in formato PDF per facilitarne la condivisione.

Effettua le seguenti operazioni:

1. Fare clic sull&#39;azione **Anteprima di stampa**.

   ![Anteprima di stampa](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. Nella nuova scheda con il report visualizzato in un&#39;anteprima stampabile, fare clic su **Stampa** per stampare il report in formato PDF.

   >[!IMPORTANT]
   >
   >* L&#39;opzione **Salva come PDF** è consigliata e supportata per la funzionalità precedente.
   >* Se si utilizza il pulsante Stampa del browser, verrà stampata una sola pagina.

   ![Stampa](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Utilizzo della linea di tendenza della vista {#trendline-view-cam}

Quando carichi più di un report BPA (Best Practices Analyzer) distinto in un progetto, puoi selezionare l&#39;opzione **Visualizza linea di tendenza** per visualizzare e confrontare i risultati dei report BPA storici.

Per visualizzare i rapporti dall’opzione della linea di tendenza, segui i passaggi seguenti:

>[!NOTE]
>Quando carichi più di un report BPA distinto in un progetto, viene visualizzata l&#39;icona **...**. I rapporti vengono considerati uguali (non distinti) se l’host e il tempo di creazione sono gli stessi.

1. Passa al progetto e fai clic su **Rivedi** dalla scheda **Analisi delle best practice** nella fase **Preparazione**.

   ![Analisi delle best practice - Revisione](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Dall&#39;elenco a discesa **Visualizza**, fare clic su **Rapporto linea di tendenza**, come illustrato nella figura seguente.

   ![Rapporto linea di tendenza](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Facendo clic su **Report linea di tendenza** viene aperta la visualizzazione della linea di tendenza del report.

   ![Visualizzazione linea di tendenza](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >Il rapporto Linea di tendenza visualizza i risultati dei rapporti BPA cronologici in una rappresentazione grafica.
   >
   >Sono presenti due grafici che mostrano la tendenza del:
   > 
   >1. **Tendenza risultati report**
   >1. **Tendenza modelli e componenti personalizzati**
   >
   >Potete aggiungere o modificare la vista grafica mediante il menu a discesa, come illustrato nella figura riportata di seguito.
   >![Selezionare la visualizzazione grafica](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Analisi del rapporto di Best Practices Analyzer {#analysis-report}

Esplora le seguenti schede disponibili nella pagina Report di analisi delle best practice:

![Rapporto di analisi delle best practice](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con ogni scheda, puoi:
>
>* apri la scheda associata
>* applica un segnalibro a tutte le schede dei rapporti (incluso il filtro) per la condivisione o il recupero futuro
>* utilizza l’icona dettagli per visualizzare i dettagli di ciascun risultato del rapporto

#### Proprietà rapporto {#report-properties}

La scheda **Proprietà report** fornisce informazioni sulle proprietà del report come la data, la durata, i filtri, la data di caricamento e i dettagli di Adobe Experience Manager (AEM).

![Proprietà report](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Panoramica del rapporto {#report-overview}

Questa scheda **Panoramica report** fornisce i risultati del report e i livelli di gravità che si applicano quando si valuta la fattibilità del passaggio ad AEM as a Cloud Service, come illustrato nella figura seguente.

![Panoramica report](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Facendo clic su questo report si apre la scheda **Report**.

![Scheda Report](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Puoi filtrare il rapporto in base alla rilevanza, al sottotipo o al conteggio.

![Filtri per report](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulta [Interpretazione del rapporto di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html) per informazioni sulle categorie di risultati e sui livelli di importanza.

#### Valutazione delle best practice {#best-practices-assessment}

L’opzione di valutazione delle best practice fornisce una valutazione dell’istanza AEM corrente e indicazioni sui passaggi successivi per adottare le best practice di AEM. Da questa scheda è possibile esaminare le informazioni riportate di seguito.

* Panoramica dell’istanza AEM
* Componenti e modelli personalizzati
* Ulteriori risultati
* Query lente
* Attività di manutenzione

#### Valutazione della complessità della migrazione {#migration-complexity-assessment}

L’opzione Valutazione della complessità della migrazione fornisce una valutazione della complessità della migrazione dell’implementazione AEM esistente ad AEM as a Cloud Service.

Da questa scheda è possibile esaminare le informazioni riportate di seguito.

* Panoramica dell’istanza AEM
* Valutazione
* Considerazioni sulla migrazione dei contenuti

  ![Valutazione complessità migrazione](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Utilizzo della scheda Pianificazione e configurazione {#planning-setup}

1. Fare clic su **Visualizza** dalla scheda **Pianificazione e installazione**. Questa scheda fornisce tutti i contenuti utili per pianificare e configurare la migrazione AEM.

   ![Pianificazione E Installazione - Vista](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carosello di contenuti mostra tutte le informazioni rilevanti per questa fase del percorso di migrazione.

   ![Pianificazione E Installazione Del Carosello](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Eliminazione di un rapporto di analisi delle best practice dalla vista Linea di tendenza {#delete-trendline}

>[!IMPORTANT]
>Un rapporto può essere eliminato solo quando in un progetto è stato caricato più di un rapporto.

1. Passa al progetto e fai clic su **Rivedi** dalla scheda **Analisi delle best practice** nella fase **Preparazione**.

   ![Analisi delle best practice - Revisione](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Fare clic su **...**.

   ![Ellisse](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Nell&#39;elenco a discesa fare clic su **Visualizza linea di tendenza**, come illustrato nella figura seguente.

   ![Visualizza linea di tendenza](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Fare clic sull&#39;icona Elimina nella schermata **Report linea di tendenza**.

   ![Rapporto linea di tendenza - Elimina](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Fai clic su **Elimina** per confermare l&#39;eliminazione.

   ![Elimina](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## Passaggio successivo {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come creare un progetto, puoi passare alla revisione del passaggio successivo nella [fase di implementazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html).
