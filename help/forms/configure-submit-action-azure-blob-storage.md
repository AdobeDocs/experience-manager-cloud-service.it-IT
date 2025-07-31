---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Integrazione dell’archiviazione Azure Blob con AEM Forms, invio dei dati all’archiviazione Azure, creazione della configurazione dell’archiviazione Azure in AEM Forms, utilizzo dell’archiviazione Azure Blob nell’azione di invio di Forms adattivo
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---

# Inviare un modulo adattivo all’archiviazione BLOB di Azure

L&#39;azione di invio **[!UICONTROL Invia ad Azure Blob Storage]** collega un modulo adattivo a un portale Microsoft® Azure. È possibile inviare i dati del modulo, i file, gli allegati o il documento record ai contenitori di archiviazione di Azure connessi.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/aem-forms-submit-action.md).

## Vantaggi

Alcuni dei vantaggi dell’integrazione dell’archiviazione Azure Blob con AEM Forms sono:

* Consente di semplificare il processo di invio di dati, file, allegati e documenti del modulo adattivo ai contenitori di archiviazione di Azure.
* Utilizza Azure Blob Storage per l’archiviazione centralizzata e organizzata degli invii di moduli adattivi.

## Connettere AEM Forms con l’archiviazione BLOB di Microsoft® Azure

Per utilizzare l’archiviazione BLOB di Azure nell’azione di invio di Forms adattivo:

1. [Creare un contenitore di archiviazione BLOB di Azure](#create-a-azure-blob-storage-container-create-azure-configuration): connette AEM Forms ai contenitori di archiviazione di Azure.
2. [Usa la configurazione di archiviazione Azure in un modulo adattivo](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): connette il modulo adattivo ai contenitori di archiviazione Azure configurati.

### Creare un contenitore di archiviazione BLOB di Azure {#create-azure-configuration}

Per connettere AEM Forms ai contenitori di archiviazione Azure:

1. Vai all&#39;**istanza Autore AEM Forms** > **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Archiviazione Azure]**.
1. Dopo aver selezionato **[!UICONTROL Archiviazione Azure]**, si verrà reindirizzati a **[!UICONTROL Browser archiviazione Azure]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la procedura guidata Crea configurazione di archiviazione Azure.

   ![Configurazione archiviazione Azure](/help/forms/assets/azure-storage-configuration.png)

1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]**.

   * È possibile recuperare il nome `Azure Storage Account` e `Azure Access key` dagli account di archiviazione nel portale Microsoft® Azure.
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=it)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=it)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. Fai clic su **[!UICONTROL Salva]**.

Ora puoi utilizzare questa configurazione del contenitore di archiviazione Azure per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione di archiviazione Azure in un modulo adattivo {#use-azure-storage-configuartion-in-af}

Puoi utilizzare la configurazione del contenitore di archiviazione Azure creata in un modulo adattivo per salvare dati o documenti di record generati nel contenitore di archiviazione Azure.

>[!NOTE]
>
> * Selezionare lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stato creato lo spazio di archiviazione di OneDrive.
> * Se non è selezionato alcun contenitore di configurazione [!UICONTROL Contenitore di configurazione], nella finestra delle proprietà dell&#39;azione di invio vengono visualizzate le cartelle globali [!UICONTROL Configurazione archiviazione].

>[!BEGINTABS]

>[!TAB Componente di base]

Per utilizzare la configurazione del contenitore di archiviazione Azure in un modulo adattivo basato su componenti di base, effettua le seguenti operazioni:

1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Invio]** delle proprietà Contenitore modulo adattivo.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Invia ad Azure Blob Storage]**.

   ![Archiviazione BLOB di Azure GIF](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%,height=50%}

   Puoi anche salvare il documento di record (DoR) nell’archiviazione BLOB di Azure.

1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nella configurazione del contenitore di archiviazione Azure specificata.
La struttura di cartelle per il salvataggio dei dati è `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Componente core]

Per utilizzare la configurazione del contenitore di archiviazione Azure in un modulo adattivo basato su componenti core, effettua le seguenti operazioni:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Invia ad Azure Blob Storage]**.

   ![Archiviazione BLOB di Azure GIF](/help/forms/assets/azure-submit-video.gif)

   Puoi anche salvare il documento di record (DoR) nell’archiviazione BLOB di Azure.

1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nella configurazione del contenitore di archiviazione Azure specificata.
La struttura di cartelle per il salvataggio dei dati è `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Editor universale]

Per utilizzare la configurazione del contenitore di archiviazione Azure in un modulo adattivo creato in Universal Editor, effettua le seguenti operazioni:

1. Apri il modulo adattivo per la modifica.
1. Fai clic sull&#39;estensione **Modifica proprietà modulo** nell&#39;editor.
Viene visualizzata la finestra di dialogo **Proprietà modulo**.

   >[!NOTE]
   >
   > * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
   > * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

1. Fai clic sulla scheda **Invio** e seleziona **[!UICONTROL Invia ad Azure Blob Storage]** azione di invio.
   ![Archiviazione BLOB di Azure](/help/forms/assets/azure-blob-storage-ue.png)

   Se si seleziona **Salva allegati con nome originale**, gli allegati vengono archiviati nella cartella utilizzando i nomi di file originali. Puoi anche salvare il documento di record (DoR) nell’archiviazione BLOB di Azure.

1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva&amp;Chiudi]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nella configurazione del contenitore di archiviazione Azure specificata.
La struttura di cartelle per il salvataggio dei dati è `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!ENDTABS]

## Articoli correlati

{{af-submit-action}}
