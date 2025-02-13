---
title: Come si configura il connettore di archiviazione unificata (USC) per AEM Forms?
description: Scopri come gestire il connettore di archiviazione unificata (USC) per AEM Forms. Utilizza il connettore di archiviazione unificata (USC) per collegare AEM Forms alle archiviazioni dati esterne.
role: Admin, Developer, User
feature: Adaptive Forms, Workflow
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: c17e4e70fa8cec176c908983230b03f2899bc1ca
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Gestire il connettore di archiviazione unificata (USC) per AEM Forms {#manage-unified-storage-connector}

È possibile utilizzare il connettore di archiviazione unificata (USC) per collegare AEM Forms a archivi di dati esterni.

Ad esempio, puoi compilare i valori dei campi in un modulo adattivo e inviarlo a un flusso di lavoro AEM. Puoi configurare ulteriormente i flussi di lavoro di AEM per archiviare i dati in un archivio esterno, ad esempio il server di archiviazione di Microsoft Azure. Utilizza il connettore di archiviazione unificata (USC) per creare una connessione tra i flussi di lavoro di AEM e l’archiviazione esterna.

## Collegare i flussi di lavoro di AEM a un server di archiviazione Microsoft Azure {#connect-workflows-with-azure}

Crea una configurazione di archiviazione Azure e fai riferimento a tale configurazione utilizzando il connettore di archiviazione unificata (USC). Puoi quindi configurare i modelli di flusso di lavoro di AEM per esternalizzare l’archiviazione dati in modo da collegarli a un server di archiviazione Azure.

### Crea configurazione archiviazione [!DNL Azure] {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, verificare di disporre di un account di archiviazione [!DNL Azure] e di una chiave di accesso per autorizzare l&#39;accesso all&#39;account di archiviazione [!DNL Azure].

Per creare una configurazione di archiviazione [!DNL Azure], effettuare le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Archiviazione Azure]**.
1. Selezionare una cartella per creare la configurazione e selezionare **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nel campo **[!UICONTROL Titolo]**.
1. Specificare il nome dell&#39;account di archiviazione [!DNL Azure] nel campo **[!UICONTROL Account di archiviazione Azure]**.
1. Specifica la chiave per accedere all&#39;account di archiviazione Azure nel campo **[!UICONTROL Chiave di accesso Azure]** e seleziona **[!UICONTROL Salva]**.

### Configurare il connettore di archiviazione unificata (USC) per i flussi di lavoro di AEM {#configure-unified-storage-connector-workflows}

Per configurare il connettore di archiviazione unificata (USC) per i flussi di lavoro di AEM, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.

1. Nella sezione **[!UICONTROL Flusso di lavoro]**, seleziona **[!UICONTROL Azure]** dall&#39;elenco a discesa Archiviazione.
1. Specificare il [percorso di configurazione per la configurazione di archiviazione Azure](#create-azure-storage-configuration) nel campo **[!UICONTROL Percorso configurazione di archiviazione]**.
1. Seleziona **[!UICONTROL Pubblica]**, quindi seleziona **[!UICONTROL Salva]** per salvare la configurazione.

### Configurare un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni {#configure-workflow-external-data-storage}

Per configurare un modello di flusso di lavoro AEM per un’archiviazione dati esterna, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Selezionare un nome di modello e selezionare **[!UICONTROL Modifica]**.
1. Selezionare l&#39;icona Informazioni pagina e selezionare **[!UICONTROL Apri proprietà]**.
1. Selezionare **[!UICONTROL Esternalizzare l&#39;archiviazione dei dati del flusso di lavoro]**.
1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare le proprietà.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e per recuperare la cronologia del passaggio Assegna attività sono disabilitate quando configuri un modello di flusso di lavoro AEM per l’archiviazione di dati esterni.

### Linee guida per i flussi di lavoro di AEM per l’archiviazione di dati esterni {#guidelines-workflows-external-data-storage}

Di seguito sono riportate le linee guida per l’utilizzo dei flussi di lavoro di AEM e l’archiviazione dei dati in archivi di dati esterni, come il server di archiviazione di Microsoft Azure:

* Utilizza le variabili per memorizzare i dati durante la definizione dei file di dati di input e output e degli allegati nei passaggi del modello di flusso di lavoro. Non selezionare **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** opzioni. Le opzioni **[!UICONTROL Relative al payload]** e **[!UICONTROL Disponibili in un percorso assoluto]** non vengono visualizzate automaticamente dopo aver [configurato un modello di flusso di lavoro AEM per l&#39;archiviazione dati esterna](#configure-workflow-external-data-storage).

* Utilizza le variabili per memorizzare file di dati e allegati durante l’invio di un modulo adattivo a un flusso di lavoro di AEM. Non selezionare l&#39;opzione **[!UICONTROL Relativo al payload]** durante l&#39;invio di un modulo adattivo a un flusso di lavoro AEM. L&#39;opzione **[!UICONTROL Relativo al payload]** non viene visualizzata automaticamente dopo aver [configurato un modello di flusso di lavoro AEM per l&#39;archiviazione dati esterna](#configure-workflow-external-data-storage).

* Non utilizzare un passaggio del flusso di lavoro AEM personalizzato in un modello di flusso di lavoro per memorizzare i dati nell’archivio CRX DE.

* Quando [configuri un modello di flusso di lavoro AEM per l&#39;archiviazione dati esterna](#configure-workflow-external-data-storage), non creare colonne personalizzate per la casella in entrata AEM, poiché i valori delle colonne personalizzate non vengono recuperati se l&#39;elemento di lavoro nella casella in entrata AEM appartiene a un flusso di lavoro contrassegnato per l&#39;archiviazione esterna.

>[!MORELIKETHIS]
>
>* [Configura origini dati per AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurare l&#39;archiviazione Azure per AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrare Microsoft Dynamics 365](/help/forms/configure-msdynamics.md)
>  [Aggiungi Forms Portal a una pagina AEM Sites](/help/forms/configure-forms-portal.md)
