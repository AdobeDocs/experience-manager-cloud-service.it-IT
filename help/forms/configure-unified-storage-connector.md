---
title: Come si configura Unified Storage Connector per AEM Forms?
description: Scopri come gestire Unified Storage Connector per AEM Forms. Utilizzare il connettore di archiviazione unificata per collegare AEM Forms a archivi dati esterni.
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Gestire il connettore di storage unificato per AEM Forms {#manage-unified-storage-connector}

È possibile utilizzare Unified Storage Connector per collegare AEM Forms a archivi dati esterni.

Ad esempio, è possibile compilare i valori per i campi di un modulo adattivo e inviarlo a un flusso di lavoro AEM. È inoltre possibile configurare flussi di lavoro AEM per memorizzare i dati in un archivio esterno, ad esempio il server di archiviazione Microsoft Azure. Utilizzare Unified Storage Connector per creare una connessione tra flussi di lavoro AEM e lo storage esterno.

## Collegare flussi di lavoro AEM con un server di archiviazione Microsoft Azure {#connect-workflows-with-azure}

Crea una configurazione di archiviazione di Azure e fai riferimento a tale configurazione utilizzando Unified Storage Connector. È quindi possibile configurare AEM modelli di flusso di lavoro per esternalizzare l’archiviazione dei dati per collegarli a un server di archiviazione di Azure.

### Crea [!DNL Azure] configurazione dello storage {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, assicurati di disporre di un [!DNL Azure] l&#39;account di archiviazione e una chiave di accesso per autorizzare l&#39;accesso al [!DNL Azure] account di archiviazione.

Esegui i seguenti passaggi per creare un [!DNL Azure] configurazione di archiviazione:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Archiviazione di Azure]**.
1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo .
1. Specifica il nome della [!DNL Azure] account di archiviazione nel **[!UICONTROL Account di archiviazione di Azure]** campo .
1. Specifica la chiave per accedere all’account di archiviazione di Azure nel **[!UICONTROL Chiave di accesso di Azure]** campo e tocco **[!UICONTROL Salva]**.

### Configurare il connettore di archiviazione unificato per i flussi di lavoro AEM {#configure-unified-storage-connector-workflows}

Esegui i seguenti passaggi per configurare Unified Storage Connector per i flussi di lavoro AEM:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.

1. In **[!UICONTROL Flusso di lavoro]** sezione, Seleziona **[!UICONTROL Azure]** dall&#39;elenco a discesa Archiviazione.
1. Specifica la [percorso di configurazione per la configurazione di archiviazione di Azure](#create-azure-storage-configuration) in **[!UICONTROL Percorso di configurazione dell&#39;archiviazione]** campo .
1. Tocca **[!UICONTROL Pubblica]** quindi tocca **[!UICONTROL Salva]** per salvare la configurazione.

### Configurare un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni {#configure-workflow-external-data-storage}

Esegui i seguenti passaggi per configurare un modello di flusso di lavoro AEM per un archivio dati esterno:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Seleziona un nome di modello e tocca **[!UICONTROL Modifica]**.
1. Tocca l’icona Informazioni pagina e tocca **[!UICONTROL Apri proprietà]**.
1. Seleziona **[!UICONTROL Esternalizzare l’archiviazione dei dati del flusso di lavoro]**.
1. Tocca **[!UICONTROL Salva e chiudi]** per salvare le proprietà.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e recuperare la cronologia del passaggio Assegna attività sono disabilitate quando si configura un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni.

### Linee guida per i flussi di lavoro AEM per l’archiviazione dei dati esterni {#guidelines-workflows-external-data-storage}

Di seguito sono riportate le linee guida per l’utilizzo dei flussi di lavoro AEM e la memorizzazione dei dati in archivi di dati esterni, ad esempio il server di archiviazione Microsoft Azure:

* Utilizza le variabili per memorizzare i dati durante la definizione dei file di dati di input e output e degli allegati nei passaggi del modello di flusso di lavoro. Non selezionare **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** opzioni. La **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** le opzioni non vengono visualizzate automaticamente una volta [configurare un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni](#configure-workflow-external-data-storage).

* Utilizza le variabili per memorizzare file di dati e allegati durante l’invio di un modulo adattivo a un flusso di lavoro AEM. Non selezionare **[!UICONTROL Relativo al payload]** durante l’invio di un modulo adattivo a un flusso di lavoro AEM. La **[!UICONTROL Relativo al payload]** l&#39;opzione non viene visualizzata automaticamente una volta [configurare un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni](#configure-workflow-external-data-storage).

* Non utilizzare un passaggio personalizzato AEM Workflow in un modello di flusso di lavoro per memorizzare i dati nell&#39;archivio CRX DE.

* Quando [configurare un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni](#configure-workflow-external-data-storage), non creare colonne personalizzate per AEM casella in entrata, poiché i valori delle colonne personalizzate non vengono recuperati se l’elemento di lavoro nella casella in entrata AEM appartiene a un flusso di lavoro contrassegnato per l’archiviazione esterna.
