---
title: Come si configura il connettore di archiviazione unificata per AEM Forms?
description: Scopri come gestire il connettore di archiviazione unificata per AEM Forms. Utilizza il connettore di archiviazione unificata per collegare AEM Forms a archivi di dati esterni.
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Gestione del connettore di archiviazione unificata per AEM Forms {#manage-unified-storage-connector}

Puoi utilizzare il connettore di archiviazione unificata per collegare AEM Forms a archivi di dati esterni.

Ad esempio, puoi compilare i valori dei campi in un modulo adattivo e inviarlo a un flusso di lavoro AEM. Puoi configurare ulteriormente i flussi di lavoro AEM per archiviare i dati in un archivio esterno, ad esempio il server di archiviazione Microsoft Azure. Utilizza il connettore di archiviazione unificata per creare una connessione tra i flussi di lavoro AEM e l’archiviazione esterna.

## Collegare i flussi di lavoro AEM con un server di archiviazione Microsoft Azure {#connect-workflows-with-azure}

Crea una configurazione di archiviazione Azure e fai riferimento a tale configurazione utilizzando il connettore di archiviazione unificata. È quindi possibile configurare i modelli di flusso di lavoro AEM per esternalizzare l’archiviazione dati per collegarli a un server di archiviazione Azure.

### Crea [!DNL Azure] configurazione di archiviazione {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, assicurati di disporre di un [!DNL Azure] e una chiave di accesso per autorizzare l&#39;accesso al [!DNL Azure] account di archiviazione.

Per creare un’ [!DNL Azure] configurazione archiviazione:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.
1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo.
1. Specifica il nome del [!DNL Azure] account di archiviazione in **[!UICONTROL Account di archiviazione Azure]** campo.
1. Specifica la chiave per accedere all’account di archiviazione Azure in **[!UICONTROL Chiave di accesso Azure]** campo e tocco **[!UICONTROL Salva]**.

### Configurare il connettore di archiviazione unificata per i flussi di lavoro AEM {#configure-unified-storage-connector-workflows}

Per configurare il connettore di archiviazione unificata per i flussi di lavoro AEM, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.

1. In **[!UICONTROL Flusso di lavoro]** sezione, Seleziona **[!UICONTROL Azure]** dall&#39;elenco a discesa Archiviazione.
1. Specifica la [percorso di configurazione per la configurazione dell’archiviazione Azure](#create-azure-storage-configuration) nel **[!UICONTROL Percorso configurazione archiviazione]** campo.
1. Tocca **[!UICONTROL Pubblica]** e quindi tocca **[!UICONTROL Salva]** per salvare la configurazione.

### Configurare un modello di flusso di lavoro AEM per l’archiviazione di dati esterni {#configure-workflow-external-data-storage}

Per configurare un modello di flusso di lavoro AEM per un’archiviazione dati esterna, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Seleziona un nome di modello e tocca **[!UICONTROL Modifica]**.
1. Tocca l’icona Informazioni pagina e tocca **[!UICONTROL Apri proprietà]**.
1. Seleziona **[!UICONTROL Esternalizzare l’archiviazione dei dati del flusso di lavoro]**.
1. Tocca **[!UICONTROL Salva e chiudi]** per salvare le proprietà.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e per recuperare la cronologia del passaggio Assegna attività sono disabilitate quando si configura un modello di flusso di lavoro AEM per l’archiviazione di dati esterni.

### Linee guida per i flussi di lavoro AEM per l’archiviazione di dati esterni {#guidelines-workflows-external-data-storage}

Di seguito sono riportate le linee guida per l&#39;utilizzo dei flussi di lavoro AEM e l&#39;archiviazione dei dati in archivi dati esterni, ad esempio il server di archiviazione Microsoft Azure:

* Utilizza le variabili per memorizzare i dati durante la definizione dei file di dati di input e output e degli allegati nei passaggi del modello di flusso di lavoro. Non selezionare **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** opzioni. Il **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** le opzioni non vengono visualizzate automaticamente una volta [configurare un modello di flusso di lavoro AEM per l’archiviazione di dati esterni](#configure-workflow-external-data-storage).

* Utilizza le variabili per memorizzare file di dati e allegati durante l’invio di un modulo adattivo a un flusso di lavoro AEM. Non selezionare **[!UICONTROL Relativo al payload]** durante l’invio di un modulo adattivo a un flusso di lavoro AEM. Il **[!UICONTROL Relativo al payload]** opzione non viene visualizzata automaticamente una volta [configurare un modello di flusso di lavoro AEM per l’archiviazione di dati esterni](#configure-workflow-external-data-storage).

* Non utilizzare un passaggio del flusso di lavoro AEM personalizzato in un modello di flusso di lavoro per memorizzare i dati nell’archivio CRX DE.

* Quando [configurare un modello di flusso di lavoro AEM per l’archiviazione di dati esterni](#configure-workflow-external-data-storage), non creare colonne personalizzate per la casella in entrata AEM poiché i valori delle colonne personalizzate non vengono recuperati se l’elemento di lavoro nella casella in entrata AEM appartiene a un flusso di lavoro contrassegnato per l’archiviazione esterna.

>[!MORELIKETHIS]
>
>* [Configurare le origini dati per AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurare l’archiviazione Azure per AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrare Microsoft Dynamics 365 e Salesforce con Forms adattivo](/help/forms/configure-msdynamics-salesforce.md)
>  [Aggiungere Forms Portal a una pagina di AEM Sites](/help/forms/configure-forms-portal.md)
