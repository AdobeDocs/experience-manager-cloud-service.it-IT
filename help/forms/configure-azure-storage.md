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

# Configura archiviazione [!DNL Azure] {#configure-azure-storage}


![integrazione dei dati](assets/data-integeration.png)

[[!DNL Experience Manager Forms] Integrazione dati](data-integration.md) fornisce una configurazione di archiviazione [!DNL Azure] per integrare i moduli con i servizi di archiviazione [!DNL Azure]. Il modello di dati del modulo (FDM) può essere utilizzato per creare Forms adattivo che interagisce con il server [!DNL Azure] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivere i dati in [!DNL Azure] all&#39;invio del modulo adattivo.
* Scrivere i dati in [!DNL Azure] tramite entità personalizzate definite in Form Data Model (FDM) e viceversa.
* Eseguire una query sul server [!DNL Azure] per i dati e precompilare Adaptive Forms.
* Lettura dei dati dal server [!DNL Azure].

## Crea configurazione archiviazione [!DNL Azure] {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, verificare di disporre di un account di archiviazione [!DNL Azure] e di una chiave di accesso per autorizzare l&#39;accesso all&#39;account di archiviazione [!DNL Azure].

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.
1. Selezionare una cartella per creare la configurazione e selezionare **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nel campo **[!UICONTROL Titolo]**.
1. Specificare il nome dell&#39;account di archiviazione [!DNL Azure] nel campo **[!UICONTROL Account di archiviazione Azure]**.
1. Specifica la chiave per accedere all&#39;account di archiviazione Azure nel campo **[!UICONTROL Chiave di accesso Azure]** e seleziona **[!UICONTROL Salva]**.

## Crea modello dati modulo {#create-azure-form-data-model}

Dopo aver creato la configurazione dell&#39;archiviazione [!DNL Azure], puoi [creare il modello dati del modulo](create-form-data-models.md). Specificare la cartella contenente la configurazione [!DNL Azure] nel campo **[!UICONTROL Configurazione Source dati]** durante la creazione del modello dati del modulo. Puoi quindi selezionare la configurazione dall’elenco di configurazioni esistenti nel nome della cartella specificato.

### Aggiungi servizi [!DNL Azure] al modello dati del modulo {#add-azure-services}

Dopo aver creato il modello dati del modulo (FDM) e gli oggetti del modello dati, è possibile aggiungere [!DNL Azure] servizi al modello dati del modulo (FDM).

Per aggiungere [!DNL Azure] servizi:

1. In modalità Modifica, seleziona i servizi dalla sezione **[!UICONTROL Servizi]** nel riquadro a sinistra, quindi seleziona **[!UICONTROL Aggiungi selezionati]**. I servizi selezionati vengono visualizzati nella scheda **[!UICONTROL Servizi]** del modello dati modulo (FDM).

   ![Aggiungi servizi selezionati](assets/select-services.png)

1. Nella scheda **[!UICONTROL Servizi]**, selezionare il servizio e **[!UICONTROL Modifica proprietà]**. In base al servizio, definisci gli oggetti modello di input o output per il servizio.

1. Seleziona **[!UICONTROL Salva]** per salvare il modello dati del modulo (FDM).

   Nella tabella seguente sono descritti i servizi [!DNL Azure] disponibili:

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

1. Nella scheda **[!UICONTROL Modello]**, selezionare la proprietà dell&#39;oggetto modello dati e selezionare **[!UICONTROL Modifica proprietà]**.
1. Imposta l&#39;opzione di attivazione per **[!UICONTROL Chiave di ricerca]**. Questa opzione è disponibile solo per i tipi di dati primari.
1. Seleziona **[!UICONTROL Fine]**, quindi seleziona **[!UICONTROL Salva]** per salvare il modello dati del modulo (FDM).

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