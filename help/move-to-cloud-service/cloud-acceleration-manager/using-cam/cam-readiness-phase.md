---
title: Fase di preparazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica della fase di preparazione di Cloud Acceleration Manager.
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: 3063a9d3a28e974300afa1b91c2b6a344b3361b8
workflow-type: tm+mt
source-wordcount: '1057'
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

1. Passa a **Preparazione** come illustrato nella figura riportata di seguito.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Per ulteriori informazioni, consulta Creazione e gestione di un progetto in Cloud Acceleration Manager .

## Utilizzo della scheda di analisi delle best practice {#best-practices-analysis}

Segui i passaggi riportati di seguito per utilizzare la scheda Analisi delle best practice :

1. Fai clic sul pulsante **Revisione** dal pulsante **Analisi delle best practice** il Card.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Segui questi passaggi per scaricare Best Practices Analyzer (BPA).

   >[!NOTE]
   >Per evitare un impatto sulle istanze aziendali critiche, si consiglia di eseguire BPA in un ambiente di authoring il più simile possibile all’ambiente di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di authoring di produzione.

   1. Passa a [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) e scarica Best Practices Analyzer come file zip.

      >[!NOTE]
      >Revisione [Utilizzo di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) per scoprire come eseguire BPA.

   1. Esportare il rapporto in formato CSV

1. Fai clic su **Carica nuovo rapporto** per caricare il rapporto BPA in CAM.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >Non è possibile caricare il rapporto se ti trovi in modalità in incognito del browser.

1. Dopo aver caricato un nuovo rapporto, verrà visualizzato il rapporto di analisi delle best practice .

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Rivedi ed esplora il dashboard Analisi delle best practice in CAM. Consulta la sezione seguente [Analisi del rapporto sulle best practice](#analysis-report) per ulteriori dettagli.

   >[!NOTE]
   >Il caricamento di un nuovo rapporto ripristina tutte le valutazioni.

### Utilizzo dell&#39;anteprima di stampa {#print-preview-cam}

È possibile selezionare l’opzione di anteprima di stampa in Cloud Acceleration Manager per un’anteprima stampabile dei rapporti o per stampare il rapporto in un formato PDF per facilitarne la condivisione.

Effettua le seguenti operazioni:

1. Fai clic su **Anteprima di stampa** , come illustrato di seguito.

   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Clic su **Anteprima di stampa** apre una nuova scheda con il rapporto visualizzato in un’anteprima stampabile. Fai clic su **Stampa** per stampare il rapporto in un formato PDF.

   >[!IMPORTANT]
   >* Opzione **Salva come PDF** è consigliato e supportato per la funzionalità di cui sopra.
   >* Se si utilizza il pulsante di stampa del browser, verrà stampata una sola pagina.


   ![immagine](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview2.png)

### Utilizzo della linea di tendenza della vista {#trendline-view-cam}

Quando carichi più rapporti di Best Practices Analyzer (BPA) in un progetto, puoi selezionare la **Visualizza linea di tendenza** per visualizzare e confrontare i risultati dei rapporti BPA storici.

Per visualizzare i rapporti dall’opzione della linea di tendenza, effettua le seguenti operazioni:

>[!NOTE]
>Quando carichi più di un rapporto BPA in un progetto, visualizzerai l’ **...** icona.

1. Passa al progetto e fai clic su **Revisione** dal **Analisi delle best practice** nella scheda **Preparazione** fase.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Fai clic sul pulsante **...** per visualizzare il menu a discesa.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >Il rapporto visualizzato è sempre il rapporto con la data più recente del rapporto.

1. Fai clic su **Visualizza linea di tendenza**, come illustrato nella figura seguente.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clic su **Visualizza linea di tendenza** apre la vista della linea di tendenza del rapporto, come illustrato nella figura riportata di seguito.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >Il rapporto Linee di tendenza visualizza i risultati dei rapporti BPA storici in una rappresentazione grafica.
   >
   >Vedrete due grafici che mostrano la tendenza di:
   >1. **Tendenza dei risultati dei report**
   >1. **Componenti personalizzati e tendenze dei modelli**

   >
   >Puoi aggiungere o modificare la visualizzazione grafica tramite il menu a discesa, come illustrato nella figura seguente:
   >![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view4.png)


### Analisi del rapporto sulle best practice {#analysis-report}

Esplora le seguenti schede disponibili nella pagina Rapporto di analisi delle best practice :

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con ogni scheda, è possibile:
>* fai clic su ogni scheda per aprire la relativa scheda associata
>* segnalibro di tutte le schede del rapporto (incluso il filtro) per la condivisione o il recupero futuro
>* utilizza l’icona dei dettagli per visualizzare i dettagli di ogni risultato del rapporto


#### Proprietà rapporto {#report-properties}

La **Proprietà rapporto** La scheda fornisce informazioni sulle proprietà del rapporto, ad esempio data del rapporto, durata, filtri, data di caricamento e dettagli di Adobe Experience Manager (AEM).

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Panoramica dei rapporti {#report-overview}

Questo **Panoramica dei rapporti** la scheda fornisce i risultati del rapporto e i livelli di gravità che si applicano quando si valuta la disponibilità a passare a AEM as a Cloud Service, come illustrato nella figura riportata di seguito.

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Fai clic su questo rapporto per aprire la **Rapporto** scheda .

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Puoi filtrare il rapporto in base a importanza, sottotipo o conteggio.

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Fai riferimento a [Interpretazione del rapporto di Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) per informazioni sulle categorie dei risultati e sui livelli di importanza.

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

1. Fai clic sul pulsante **Visualizza** dal pulsante **Pianificazione E Configurazione** il Card. Questa scheda fornisce tutti i contenuti pertinenti che consentono di pianificare e impostare la migrazione AEM.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carosello di contenuti visualizza tutte le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Eliminazione di un rapporto di analisi delle best practice {#delete-trendline}

Per eliminare un rapporto dalla vista Linea di tendenza, effettua le seguenti operazioni:

>[!IMPORTANT]
>È possibile eliminare un rapporto solo quando sono stati caricati più rapporti in un progetto.

1. Passa al progetto e fai clic su **Revisione** dal **Analisi delle best practice** nella scheda **Preparazione** fase.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Fai clic sul pulsante **...** per visualizzare il menu a discesa.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

1. Fai clic su **Visualizza linea di tendenza**, come illustrato nella figura seguente.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. Fai clic sull’icona Elimina dal **Rapporto Trendline** schermo.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Fai clic su **Elimina** per confermare l’eliminazione.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view6a.png)

## Novità {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come creare un progetto, ora puoi passare alla revisione del passaggio successivo nel [Fase di implementazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
