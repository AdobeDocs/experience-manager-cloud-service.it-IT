---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Integrazione dell’archiviazione Azure Blob con AEM Forms, invio dei dati all’archiviazione Azure, creazione della configurazione dell’archiviazione Azure in AEM Forms, utilizzo dell’archiviazione Azure Blob nell’azione di invio di Forms adattivo
feature: Adaptive Forms, Core Components
source-git-commit: a22ecddf7c97c5894cb03eb44296e0562ac46ddb
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# Inviare un modulo adattivo all’archiviazione BLOB di Azure

Il **[!UICONTROL Invia ad Azure Blob Storage]**  L’azione di invio collega un modulo adattivo a un portale Microsoft® Azure. È possibile inviare i dati del modulo, i file, gli allegati o il documento record ai contenitori di archiviazione di Azure connessi.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione delle richieste di moduli. Per ulteriori informazioni su queste opzioni, consulta [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md) articolo.

## Vantaggi

Alcuni dei vantaggi dell’integrazione dell’archiviazione Azure Blob con AEM Forms sono:

* Consente di semplificare il processo di invio di dati, file, allegati e documenti del modulo adattivo ai contenitori di archiviazione di Azure.
* Utilizza Azure Blob Storage per l’archiviazione centralizzata e organizzata degli invii di moduli adattivi.

## Connettere AEM Forms con l’archiviazione BLOB di Microsoft® Azure

Per utilizzare l’archiviazione BLOB di Azure nell’azione di invio di Forms adattivo:

1. [Creare un contenitore di archiviazione BLOB di Azure](#create-a-azure-blob-storage-container-create-azure-configuration): connette AEM Forms ai contenitori di archiviazione Azure.
2. [Utilizzare la configurazione di archiviazione Azure in un modulo adattivo](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): collega il modulo adattivo ai contenitori di archiviazione Azure configurati.

### Creare un contenitore di archiviazione BLOB di Azure {#create-azure-configuration}

Per connettere AEM Forms ai contenitori di archiviazione Azure:
1. Vai al tuo **Autore AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Archiviazione Azure]**.
1. Dopo aver selezionato **[!UICONTROL Archiviazione Azure]**, viene reindirizzato a **[!UICONTROL Browser archiviazione Azure]**.
1. Seleziona un **Contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la procedura guidata Crea configurazione di archiviazione Azure.

   ![Configurazione archiviazione Azure](/help/forms/assets/azure-storage-configuration.png)

1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]**.

   * Puoi recuperare `Azure Storage Account` nome e `Azure Access key` dagli account di archiviazione nel portale Microsoft® Azure.
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. Fai clic su **[!UICONTROL Salva]**.

Ora puoi utilizzare questa configurazione del contenitore di archiviazione Azure per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione di archiviazione Azure in un modulo adattivo {#use-azure-storage-configuartion-in-af}

Puoi utilizzare la configurazione del contenitore di archiviazione Azure creata in un modulo adattivo per salvare dati o documenti di record generati nel contenitore di archiviazione Azure. Per utilizzare la configurazione del contenitore di archiviazione Azure in un modulo adattivo, effettua le seguenti operazioni:
1. Creare un [Modulo adattivo](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stato creato lo storage OneDrive.
   > * In caso negativo [!UICONTROL Contenitore configurazione] è selezionato, quindi il [!UICONTROL Configurazione archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell&#39;azione di invio.

1. Seleziona **Azione di invio** as **[!UICONTROL Invia ad Azure Blob Storage]**.
   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

1. Seleziona la **[!UICONTROL Configurazione archiviazione]**, dove desideri salvare i dati.
1. Clic **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nella configurazione del contenitore di archiviazione Azure specificata.
La struttura di cartelle per il salvataggio dei dati è `/configuration_container/form_name/year/month/date/submission_id/data`.

## Articoli correlati

{{af-submit-action}}