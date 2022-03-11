---
title: Come si configura l’archiviazione di Azure?
description: Scopri come integrare i moduli con il server di archiviazione Azure.
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 10284b1ac6fbad2e7f6231603c3dd60b6e404299
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# Configura[!DNL Azure]archiviazione {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce un [!DNL Azure] configurazione di archiviazione per integrare i moduli con [!DNL Azure] servizi di storage. Il modello dati modulo può essere utilizzato per creare un Forms adattivo che interagisca con [!DNL Azure] per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivere dati in [!DNL Azure] all’invio di moduli adattivi.
* Scrivi dati in [!DNL Azure] attraverso entità personalizzate definite in Form Data Model e viceversa.
* Query [!DNL Azure] server per i dati e precompilare Adaptive Forms.
* Leggi dati da [!DNL Azure] server.

## Crea [!DNL Azure] configurazione dello storage {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, assicurati di disporre di un [!DNL Azure] l&#39;account di archiviazione e una chiave di accesso per autorizzare l&#39;accesso al [!DNL Azure] account di archiviazione.

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Archiviazione di Azure]**.
1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo .
1. Specifica il nome della [!DNL Azure] account di archiviazione nel **[!UICONTROL Account di archiviazione di Azure]** campo .
1. Specifica la chiave per accedere all’account di archiviazione di Azure nel **[!UICONTROL Chiave di accesso di Azure]** campo e tocco **[!UICONTROL Salva]**.

## Crea modello dati modulo {#create-azure-form-data-model}

Dopo aver creato il [!DNL Azure] configurazione dell&#39;archiviazione, è possibile [creare il modello dati del modulo](create-form-data-models.md). Specifica la cartella contenente la [!DNL Azure] nella configurazione **[!UICONTROL Configurazione origine dati]** durante la creazione del modello dati del modulo. Puoi quindi selezionare la configurazione dall’elenco delle configurazioni esistenti nel nome della cartella specificato.

### Aggiungi [!DNL Azure] servizi al modello dati modulo {#add-azure-services}

Dopo aver creato gli oggetti modello dati modulo e modello dati, è possibile aggiungere [!DNL Azure] servizi per il modello dati del modulo.

Per aggiungere [!DNL Azure] servizi:

1. In modalità Modifica, seleziona i servizi dalla **[!UICONTROL Servizi]** nel riquadro a sinistra e tocca **[!UICONTROL Aggiungi selezionati]**. I servizi selezionati vengono visualizzati nella **[!UICONTROL Servizi]** scheda del modello dati del modulo.

   ![Aggiungi servizi selezionati](assets/select-services.png)

1. In **[!UICONTROL Servizi]** , seleziona il servizio e **[!UICONTROL Modifica proprietà]**. In base al servizio, definisci gli oggetti modello di input o output per il servizio.

1. Tocca **[!UICONTROL Salva]** per salvare il modello dati del modulo.

   La tabella seguente descrive i dati disponibili [!DNL Azure] servizi:

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
      <td>Recupera i dati memorizzati come BLOB con URL per i binari nell’archiviazione di Azure utilizzando un ID o un nome</td>
     </tr>
     <tr>
      <td>Salva BLOB in Azure</td>
      <td>Utilizzare un ID BLOB per salvare i dati nell’archiviazione di Azure</td>
     </tr>
     <tr>
      <td>Aggiorna BLOB in Azure</td>
      <td>Utilizzare un ID BLOB per aggiornare i dati nell’archiviazione di Azure</td>
     </tr>
     <tr>
      <td>Recupera elenco di ID BLOB da Azure</td>
      <td>Recupera un elenco di ID BLOB da Azure in base al numero definito nella richiesta di input.</td>
     </tr>
     <tr>
      <td>Recupera gli URL SAS per i BLOB da Azure</td>
      <td>Recupera gli URL SAS per i BLOB da Azure in base agli ID BLOB nella richiesta di input.</td>
     </tr>
     <tr>
      <td>Elimina BLOB da Azure</td>
      <td>Utilizzare un ID BLOB per eliminare i dati dall’archiviazione di Azure</td>
     </tr>
    </tbody>
   </table>

### Definire una proprietà dell’oggetto modello dati come chiave di ricerca {#define-data-model-object-as-metadata}

Per definire una proprietà dell&#39;oggetto modello dati come chiave di ricerca:

1. In **[!UICONTROL Modello]** , seleziona la proprietà dell’oggetto modello dati e tocca **[!UICONTROL Modifica proprietà]**.
1. Passa alla **[!UICONTROL Chiave di ricerca]** attiva l&#39;opzione. Questa opzione è disponibile solo per i tipi di dati principali.
1. Tocca **[!UICONTROL Fine]** quindi tocca **[!UICONTROL Salva]** per salvare il modello dati del modulo.

Dopo aver definito le proprietà dell&#39;oggetto del modello dati come chiavi di ricerca, i valori hash vengono memorizzati nei tag di indice di Azure e i valori codificati di Base64 sono memorizzati nei metadati di Azure.

>[!NOTE]
>
>Per l’entità Azure sono consentite solo 10 chiavi di ricerca, in quanto Azure consente solo 10 tag per BLOB e il valore delle proprietà contrassegnato come chiavi di ricerca viene memorizzato nei tag di indice di Azure dopo l’hashing.
