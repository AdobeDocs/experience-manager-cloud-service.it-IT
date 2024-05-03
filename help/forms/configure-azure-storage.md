---
title: Come si configura l’archiviazione Azure?
description: Scopri come integrare i moduli con il server di archiviazione Azure.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# Configura [!DNL Azure] archiviazione {#configure-azure-storage}


![integrazione dei dati](assets/data-integeration.png)

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce un [!DNL Azure] configurazione di archiviazione per integrare forms con [!DNL Azure] servizi di storage. Il Modello dati modulo (FDM) può essere utilizzato per creare Forms adattivi che interagiscono con [!DNL Azure] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivi dati in [!DNL Azure] all’invio di un modulo adattivo.
* Scrivi dati in [!DNL Azure] tramite entità personalizzate definite in Form Data Model (FDM) e viceversa.
* Query [!DNL Azure] server per dati e precompilazione di Adaptive Forms.
* Leggi dati da [!DNL Azure] server.

## Crea [!DNL Azure] configurazione di archiviazione {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, assicurati di disporre di un [!DNL Azure] e una chiave di accesso per autorizzare l&#39;accesso al [!DNL Azure] account di archiviazione.

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.
1. Seleziona una cartella per creare la configurazione e seleziona **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo.
1. Specifica il nome del [!DNL Azure] account di archiviazione in **[!UICONTROL Account di archiviazione Azure]** campo.
1. Specifica la chiave per accedere all’account di archiviazione Azure in **[!UICONTROL Chiave di accesso Azure]** e seleziona **[!UICONTROL Salva]**.

## Crea modello dati modulo {#create-azure-form-data-model}

Dopo aver creato [!DNL Azure] configurazione di storage, è possibile [creare il modello dati del modulo](create-form-data-models.md). Specifica la cartella che contiene [!DNL Azure] configurazione in **[!UICONTROL Configurazione origine dati]** durante la creazione del modello dati del modulo (FDM). Puoi quindi selezionare la configurazione dall’elenco di configurazioni esistenti nel nome della cartella specificato.

### Aggiungi [!DNL Azure] servizi al modello dati del modulo {#add-azure-services}

Dopo aver creato il modello dati modulo (FDM) e gli oggetti modello dati, è possibile aggiungere [!DNL Azure] servizi al modello di dati del modulo (FDM).

Da aggiungere [!DNL Azure] servizi:

1. In modalità Modifica, seleziona i servizi da **[!UICONTROL Servizi]** nel riquadro a sinistra e selezionare **[!UICONTROL Aggiungi selezionati]**. I servizi selezionati vengono visualizzati nel **[!UICONTROL Servizi]** del modello dati del modulo (FDM).

   ![Aggiungi servizi selezionati](assets/select-services.png)

1. In **[!UICONTROL Servizi]** , selezionare il servizio e **[!UICONTROL Modifica proprietà]**. In base al servizio, definisci gli oggetti modello di input o output per il servizio.

1. Seleziona **[!UICONTROL Salva]** per salvare il modello dati del modulo (FDM).

   Nella tabella seguente sono descritti i [!DNL Azure] servizi:

   <table>
    <tbody>
     <tr>
      <th><strong>Nome servizio</strong></th>
      <th><strong>Descrizione</strong></th>
     </tr>
     <tr>
      <td>Ottieni BLOB da Azure</td>
      <td>Recupera i dati memorizzati come BLOB nell’archiviazione di Azure utilizzando un ID o un nome</td>
     </tr>
     <tr>
      <td>Ottieni BLOB con URL binari da Azure</td>
      <td>Recupera i dati memorizzati come BLOB con URL per i file binari nell’archiviazione di Azure utilizzando un ID o un nome</td>
     </tr>
     <tr>
      <td>Salva BLOB in Azure</td>
      <td>Utilizza un ID BLOB per salvare i dati nell’archiviazione di Azure</td>
     </tr>
     <tr>
      <td>Aggiorna BLOB in Azure</td>
      <td>Utilizza un ID BLOB per aggiornare i dati nell’archiviazione di Azure</td>
     </tr>
     <tr>
      <td>Recuperare l’elenco degli ID BLOB da Azure</td>
      <td>Recupera un elenco di ID BLOB da Azure in base al numero definito nella richiesta di input.</td>
     </tr>
     <tr>
      <td>Recupera URL SAS per BLOB da Azure</td>
      <td>Recupera gli URL SAS per i BLOB da Azure in base agli ID BLOB nella richiesta di input.</td>
     </tr>
     <tr>
      <td>Elimina BLOB da Azure</td>
      <td>Utilizza un ID BLOB per eliminare i dati dall’archiviazione di Azure</td>
     </tr>
    </tbody>
   </table>

### Definire una proprietà oggetto modello dati come chiave di ricerca {#define-data-model-object-as-metadata}

Per definire una proprietà dell’oggetto modello dati come chiave di ricerca:

1. In **[!UICONTROL Modello]** , selezionare la proprietà dell&#39;oggetto modello dati e selezionare **[!UICONTROL Modifica proprietà]**.
1. Cambia il **[!UICONTROL Chiave di ricerca]** imposta l&#39;opzione sullo stato ON. Questa opzione è disponibile solo per i tipi di dati primari.
1. Seleziona **[!UICONTROL Fine]** e quindi seleziona **[!UICONTROL Salva]** per salvare il modello dati del modulo (FDM).

Dopo aver definito le proprietà dell’oggetto modello dati come chiavi di ricerca, i valori hash vengono memorizzati nei tag di indice di Azure e i valori con codifica Base64 vengono memorizzati nei metadati di Azure.

>[!NOTE]
>
>Sono consentite solo 10 chiavi di ricerca per entità Azure, poiché Azure consente solo 10 tag per BLOB e il valore delle proprietà contrassegnato come chiavi di ricerca viene memorizzato nei tag di indice di Azure dopo l’hashing.

<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->