---
title: Fase di preparazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica della fase di preparazione di Cloud Acceleration Manager.
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: 3fea3da263216c8250fd1ba3e3b1edd73b5c8940
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 5%

---

# Fase di preparazione in Cloud Acceleration Manager {#readiness-phase-cam}

Dopo aver creato un progetto in Cloud Acceleration Manager, ora puoi avviare la valutazione dell’implementazione AEM corrente nella fase di preparazione.

La fase di preparazione include:

* [Analisi delle best practice](#best-practices-analysis)
* [Pianificazione e configurazione](#planning-setup)

Segui i passaggi seguenti per passare alla fase di preparazione:

1. Fai clic sulla scheda del progetto per aprire la pagina di destinazione del progetto.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. Passa alla sezione **Preparazione** , come illustrato nella figura riportata di seguito.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Per ulteriori informazioni, consulta Creazione e gestione di un progetto in Cloud Acceleration Manager .

## Utilizzo della scheda di analisi delle best practice {#best-practices-analysis}

Segui i passaggi riportati di seguito per utilizzare la scheda Analisi delle best practice :

1. Fai clic sul pulsante **Rivedi** dalla scheda **Analisi delle best practice** .

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Segui questi passaggi per scaricare Best Practices Analyzer (BPA).

   >[!NOTE]
   >Per evitare un impatto sulle istanze aziendali critiche, si consiglia di eseguire BPA in un ambiente di authoring il più simile possibile all’ambiente di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di authoring di produzione.

   1. Passa al portale [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) e scarica Best Practices Analyzer come file zip.

      >[!NOTE]
      >Per informazioni su come eseguire BPA, consulta [Utilizzo di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) .

   1. Esportare il rapporto in formato CSV

1. Fai clic su **Carica nuovo report** per caricare il report BPA in CAM.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >Non è possibile caricare il rapporto se ti trovi in modalità in incognito del browser.

1. Dopo aver caricato un nuovo rapporto, verrà visualizzato il rapporto di analisi delle best practice .

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Rivedi ed esplora il dashboard Analisi delle best practice in CAM. Per ulteriori informazioni, fai riferimento alla sezione seguente [Rapporto sull&#39;analisi delle best practice](#analysis-report) .

   >[!NOTE]
   >Il caricamento di un nuovo rapporto ripristina tutte le valutazioni.

1. Fai clic sull&#39;icona **Anteprima di stampa**, come mostrato di seguito.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Facendo clic su **Anteprima di stampa** si apre una nuova scheda con il rapporto visualizzato in un&#39;anteprima stampabile. Fai clic su **Stampa** per stampare il rapporto in un formato PDF per facilitarne la condivisione.

   >[!IMPORTANT]
   >* L&#39;opzione **Salva come PDF** è consigliata e supportata per la funzionalità di cui sopra.
   >* Se si utilizza il pulsante di stampa del browser, verrà stampata una sola pagina.


   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview2.png)

### Analisi del rapporto sulle best practice {#analysis-report}

Esplora le seguenti schede disponibili nella pagina Rapporto di analisi delle best practice :

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con ogni scheda, è possibile:
>* fai clic su ogni scheda per aprire la relativa scheda associata
>* segnalibro di tutte le schede del rapporto (incluso il filtro) per la condivisione o il recupero futuro
>* utilizza l’icona dei dettagli per visualizzare i dettagli di ogni risultato del rapporto


#### Proprietà rapporto {#report-properties}

La scheda **Proprietà report** fornisce informazioni sulle proprietà del report quali data del report, durata, filtri, data di caricamento e dettagli di Adobe Experience Manager (AEM).

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Panoramica dei rapporti {#report-overview}

Questa scheda **Panoramica rapporto** fornisce i risultati del rapporto e i livelli di gravità da applicare durante la valutazione della preparazione al passaggio a AEM as a Cloud Service, come illustrato nella figura riportata di seguito.

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Facendo clic su questo rapporto si apre la scheda **Report** .

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Puoi filtrare il rapporto in base a importanza, sottotipo o conteggio.

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Per informazioni sulle categorie dei risultati e i livelli di importanza, fai riferimento a [Interpretazione del rapporto di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) .

#### Valutazione delle best practice {#best-practices-assessment}

L’opzione Valutazione delle best practice fornisce una valutazione dell’istanza AEM corrente e fornisce indicazioni sui passaggi successivi per adottare AEM best practice. Da questa scheda puoi esaminare le seguenti informazioni:

* Panoramica dell’istanza AEM
* Componenti e modelli personalizzati
* Risultati aggiuntivi
* Query lente
* Attività di manutenzione

#### Valutazione della complessità della migrazione {#migration-complexity-assessment}

L’opzione Valutazione della complessità della migrazione fornisce una valutazione della complessità necessaria per migrare l’implementazione AEM esistente a AEM as a Cloud Service.

Da questa scheda puoi esaminare le seguenti informazioni:

* Panoramica dell’istanza AEM
* Valutazione
* Considerazioni sulla migrazione dei contenuti

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Utilizzo della scheda Planning e Setup {#planning-setup}

Segui questa sezione per esplorare la scheda delle attività Pianificazione e Configurazione .

1. Fai clic sul pulsante **Visualizza** dalla scheda **Pianificazione e configurazione**. Questa scheda fornisce tutti i contenuti pertinenti che consentono di pianificare e impostare la migrazione AEM.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carosello di contenuti visualizza tutte le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## Novità {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come creare un progetto, ora puoi passare alla revisione del passaggio successivo nella [fase di implementazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
