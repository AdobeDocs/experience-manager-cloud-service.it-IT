---
title: Guida introduttiva agli strumenti di refactoring
description: Scopri come iniziare a utilizzare gli strumenti di refactoring in AEM as a Cloud Service
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# Guida introduttiva agli strumenti di refactoring {#getting-started-refactoring-tools}

## Disponibilità {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## Esecuzione degli strumenti di refactoring {#running-refactoring-tools}

Utilizza lo strumento Refactoring per migrare il codice e garantirne la compatibilità con AEM as a Cloud Service.

1. Se non hai ancora creato un progetto CAM, consulta [Creazione e gestione di un progetto in CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project).
1. Fai clic sulla scheda **Refactoring del codice** per caricare il codice sorgente.

   ![immagine](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. Quando accedi per la prima volta alla **Visualizzazione codice Source**, verrà visualizzato uno stato vuoto in cui viene richiesto di caricare il codice sorgente.

   ![immagine](/help/journey-migration/refactoring-tools/assets/rscam2.png)

## Caricamento del codice Source {#uploading}

Quando i clienti accedono per la prima volta agli **strumenti di refactoring**, nella **vista Codice Source** viene visualizzato uno stato vuoto. Per caricare il progetto e iniziare il processo di ispezione, segui i passaggi seguenti:

1. **Accedi alla pagina di caricamento del progetto**\
   Per avviare il processo di caricamento, fai clic sul pulsante **Caricamento progetto** nello stato vuoto.

   ![immagine](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **Carica Il Codice Source**
   - Nella finestra di dialogo di caricamento, seleziona il file ZIP del codice sorgente.
   - Fai clic su **Carica** per iniziare.
   - L’avanzamento del caricamento viene visualizzato nella finestra di dialogo. La durata dipende dalla dimensione del progetto.

   ![immagine](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **Processo di ispezione**
   - Dopo il caricamento, il **processo di ispezione** inizia automaticamente in background.
   - **Visualizzazione codice Source** mostrerà il progetto caricato e il relativo stato di ispezione.

1. **Stato ispezione** Il processo di ispezione è progettato per semplificare l&#39;esecuzione degli strumenti di refactoring riducendo il sovraccarico delle configurazioni manuali.

   L&#39;ispezione mostrerà uno dei seguenti stati:
   - **In esecuzione** - Ispezione in corso.
   - **Pronto** - Ispezione completata. È ora possibile eseguire gli strumenti di refactoring.
   - **Non riuscito** - Si è verificato un errore. Fare clic sul progetto per esaminare il rapporto di ispezione e risolvere eventuali problemi.

   ![immagine](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>
>Il caricamento di un nuovo progetto eliminerà quello esistente. Prima di procedere, assicurati di aver salvato tutti i dati necessari.

>[!NOTE]
>
>I processi di refactoring possono essere eseguiti solo se il caricamento del codice sorgente ha esito positivo.

## Processi di refactoring {#refactoring-jobs}

Quando si fa clic sulla scheda **Processo di refactoring**, viene visualizzato un elenco dei processi esistenti. Se non è stato ancora creato alcun processo, verrà visualizzato uno stato vuoto che richiede la creazione del processo.

![immagine](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### &#x200B;1. Creare un nuovo processo di refactoring

- Fare clic sul pulsante **Crea nuovo processo**.
- Selezionare gli strumenti di refactoring desiderati.
- Fare clic su **Inizio** per avviare il processo di refactoring.

![immagine](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>
>Puoi attivare singoli processi di refactoring o eseguire tutti gli strumenti disponibili in un&#39;unica operazione utilizzando l&#39;opzione **Tutti gli strumenti insieme**.

### &#x200B;2. Stato processo

- **In esecuzione** - Il processo è attualmente in corso. Lo stato viene aggiornato automaticamente al completamento o in caso di errore.
- **Completato** - Il processo è stato completato. Ora puoi rivedere i risultati o scaricare il codice rielaborato.
- **Non riuscito** - Errore del processo. Fai clic sul processo per visualizzare i registri dettagliati e risolvere il problema.

![immagine](/help/journey-migration/refactoring-tools/assets/rscam8.png)

Quando il processo viene completato correttamente, il pulsante **Scarica** diventa disponibile e consente di recuperare:

- **Progetto con refactoring**: codice aggiornato dopo l&#39;applicazione della trasformazione. I clienti possono scaricare il codice più recente per il loro progetto.
- **Registri attività**: durante l&#39;esecuzione del processo, tutti i passaggi eseguiti dallo strumento e le modifiche apportate vengono registrati come parte di questo.
- **Rapporto risultati**: questo rapporto contiene elementi che non sono stati eseguiti completamente dallo strumento ma che devono ancora essere risolti. Tutte le modifiche sono registrate qui.

![immagine](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>
>Il completamento di ogni processo può richiedere fino a 1 ora. Se lo stato non viene aggiornato, contatta il supporto Adobe.
