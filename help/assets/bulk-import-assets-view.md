---
title: Importazione in blocco delle risorse utilizzando la vista Assets
description: Scopri come importare in blocco le risorse utilizzando la nuova interfaccia utente di Assets (vista Assets). Consente agli amministratori di importare un numero elevato di risorse da un’origine dati ad AEM Assets.
exl-id: 10f9d679-7579-4650-9379-bc8287cb2ff1
source-git-commit: 88198e9333a7f706fc99e487d8cde84647fa111f
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 46%

---

# Importazione in blocco delle risorse utilizzando la vista Assets  {#bulk-import-assets-view}

L’importazione in blocco nella vista AEM Assets consente agli amministratori di importare in AEM Assets un numero elevato di risorse da un’origine dati. Gli amministratori non devono più caricare singole risorse o cartelle in AEM Assets.

>[!NOTE]
>
>L’importazione in blocco della vista Risorse utilizza lo stesso backend dell’importazione in blocco della vista Amministratore. Tuttavia, offre più origini dati da cui importare e un’esperienza utente più semplice.

Puoi importare le risorse dalle seguenti origini dati:

* Azure
* AWS
* Google Cloud
* Dropbox
* OneDrive

## Prerequisiti {#prerequisites}

| Origine dati | Prerequisiti |
|-----|------|
| Azure | <ul> <li>Account archiviazione Azure </li> <li> Contenitore BLOB di Azure <li> Chiave di accesso Azure o token SAS in base alla modalità di autenticazione </li></ul> |
| AWS | <ul> <li>Area geografica AWS </li> <li> Bucket AWS <li> Chiave di accesso AWS </li><li> Segreto di accesso AWS </li></ul> |
| Google Cloud | <ul> <li>Bucket GCP </li> <li> E-mail account servizio GCP <li> Chiave privata account servizio GCP</li></ul> |
| Dropbox | <ul> <li>ID client Dropbox (Chiave app) </li> <li> Segreto client Dropbox (segreto app)</li></ul> |
| OneDrive | <ul> <li>ID tenant di OneDrive  </li> <li> ID client OneDrive</li><li> Segreto client OneDrive</li></ul> |

Oltre a questi prerequisiti basati sull’origine dati, è necessario conoscere il nome della cartella di origine disponibile nell’origine dati che contiene tutte le risorse che devono essere importate in AEM Assets.

## Configurare l’applicazione per sviluppatori di Dropbox {#dropbox-developer-application}

Prima di importare le risorse dall’account di Dropbox ad AEM Assets, crea e configura l’applicazione per sviluppatori di Dropbox.

Esegui i passaggi seguenti:

1. Accedi al tuo [Account Dropbox](https://www.dropbox.com/developers) e fai clic su **[!UICONTROL Creare le app]**.

1. In **[!UICONTROL Scegli un’API]** , selezionare l&#39;unico pulsante di opzione disponibile.

1. In **[!UICONTROL Scegli il tipo di accesso necessario]** , selezionare una delle opzioni seguenti:

   * Seleziona **[!UICONTROL Cartella app]**, se hai bisogno di accedere a una singola cartella creata all’interno dell’applicazione nel tuo account di Dropbox.

   * Seleziona **[!UICONTROL Dropbox completo]**, se hai bisogno di accedere a tutti i file e le cartelle all’interno del tuo account di Dropbox.

1. Specifica un nome per l’applicazione e fai clic su **[!UICONTROL Crea app]**.

1. In **[!UICONTROL Impostazioni]** nell&#39;applicazione, aggiungi quanto segue alla scheda **[!UICONTROL URI di reindirizzamento]** sezione:

   * https://exc-unifiedcontent.experience.adobe.net

   * https://exc-unifiedcontent.experience-stage.adobe.net (valido solo per gli ambienti Stage)

1. Copia i valori per **[!UICONTROL Chiave app]** e **[!UICONTROL Segreto app]** campi. I valori sono necessari durante la configurazione dello strumento di importazione in blocco in AEM Assets.

1. Il giorno **[!UICONTROL Autorizzazioni]** , aggiungi le seguenti autorizzazioni all&#39;interno della scheda **[!UICONTROL Singoli ambiti]** sezione.

   * account_info.read

   * files.metadata.read

   * files.content.read

   * files.content.write

1. Clic **[!UICONTROL Invia]** per salvare le modifiche.

## Configurare l&#39;applicazione per sviluppatori OneDrive {#onedrive-developer-application}

Prima di importare risorse dall&#39;account OneDrive in AEM Assets, crea e configura l&#39;applicazione per sviluppatori OneDrive.

Esegui i passaggi seguenti:

1. Accedi al tuo [Account OneDrive](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) e fai clic su **[!UICONTROL Nuova registrazione]**.

1. Specifica un nome per l’applicazione, seleziona **[!UICONTROL Solo account in questa directory organizzativa (solo Adobe: singolo tenant)]** da **[!UICONTROL Tipi di account supportati]** e fai clic su **[!UICONTROL Registrati]**. Creazione dell&#39;applicazione completata.

1. Copia i valori per i campi ID client applicazione e ID tenant. I valori sono necessari durante la configurazione dello strumento di importazione in blocco in AEM Assets.

1. Per aggiungere un certificato, effettua le seguenti operazioni:
   1. Nella pagina di panoramica dell’applicazione, fai clic su **[!UICONTROL Aggiungi un certificato o un segreto]** e quindi fare clic su **[!UICONTROL Nuovo segreto client]**.
   1. Specifica la descrizione e la scadenza del segreto client e fai clic su **[!UICONTROL Aggiungi]**.
   1. Dopo aver creato il segreto client, copia il **[!UICONTROL Valore]** (non copiare il campo ID segreto). È necessario per configurare l’importazione in blocco in AEM Assets.

1. Per aggiungere URI di reindirizzamento, effettua le seguenti operazioni:
   1. Nella pagina di panoramica dell’applicazione, fai clic su **[!UICONTROL Aggiungere un URI di reindirizzamento]** > **[!UICONTROL Aggiungi una piattaforma]** > **[!UICONTROL Web]**.
   1. Aggiungi quanto segue a **[!UICONTROL URI di reindirizzamento]** sezione:

      * https://exc-unifiedcontent.experience.adobe.net

      * https://exc-unifiedcontent.experience-stage.adobe.net (valido solo per gli ambienti Stage)

      Aggiungi il primo URI e fai clic su **[!UICONTROL Configura]** per aggiungerlo. Puoi aggiungerne altre facendo clic su **[!UICONTROL Aggiungi URI]** opzione disponibile in **[!UICONTROL Web]** sezione sul **[!UICONTROL Autenticazione]** pagina.

1. Per aggiungere le autorizzazioni API per l’applicazione, effettua le seguenti operazioni:
   1. Clic **[!UICONTROL Autorizzazioni API]** nel riquadro a sinistra e fare clic su **[!UICONTROL Aggiungere un’autorizzazione]**.
   1. Clic **[!UICONTROL Grafico Microsoft]** > **[!UICONTROL Autorizzazioni delegate]**. Il **[!UICONTROL Seleziona autorizzazione]** mostra le autorizzazioni disponibili.
   1. Seleziona `offline_access` autorizzazione da `OpenId permissions` e `Files.ReadWrite.All` autorizzazione da `Files`.
   1. Clic **[!UICONTROL Aggiungere autorizzazioni]** per salvare gli aggiornamenti.




## Creare una configurazione di importazione in blocco {#create-bulk-import-configuration}

Per creare una configurazione di importazione in blocco, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Impostazioni]** > **[!UICONTROL Importazione in blocco]** e fai clic su **[!UICONTROL Crea importazione]**.
1. Seleziona l’origine dati. Le opzioni disponibili includono Azure, AWS, Google Cloud e Dropbox.
1. Specifica un nome per la configurazione dell’importazione in blocco nel campo **[!UICONTROL Nome]**.
1. Specifica le credenziali specifiche dell’origine dati, come indicato nei [Prerequisiti](#prerequisites).
1. Immetti il nome della cartella che contiene le risorse nell’origine dati in **[!UICONTROL Cartella di origine]** campo.

   >[!NOTE]
   >
   >Se si utilizza Dropbox come origine dati, specificare il percorso della cartella di origine in base alle regole seguenti:
   >* Se si seleziona **Dropbox completo** durante la creazione dell’applicazione di Dropbox, la cartella che contiene le risorse è già presente in `https://www.dropbox.com/home/bulkimport-assets`, quindi specifica `bulkimport-assets` nel **[!UICONTROL Cartella di origine]** campo.
   >* Se si seleziona **Cartella app** durante la creazione dell’applicazione di Dropbox, la cartella che contiene le risorse è già presente in `https://www.dropbox.com/home/Apps/BulkImportAppFolderScope/bulkimport-assets`, quindi specifica `bulkimport-assets` nel **[!UICONTROL Cartella di origine]** campo, dove `BulkImportAppFolderScope` fa riferimento al nome dell’applicazione. `Apps` viene aggiunto automaticamente dopo `home` in questo caso.

1. (Facoltativo) Seleziona l’opzione **[!UICONTROL Elimina il file di origine dopo l’importazione]** per eliminare i file originali dall’archivio dati di origine dopo l’importazione in Experience Manager Assets.
1. Seleziona la **[!UICONTROL Modalità di importazione]**. Seleziona **[!UICONTROL Ignora]**, **[!UICONTROL Sostituisci]** o **[!UICONTROL Crea versione]**. La modalità Ignora è l’impostazione predefinita e, in questa modalità, l’importazione di una risorsa viene ignorata se esiste già.
   ![Importa dettagli origine](/help/assets/assets/bulk-import-source-details.png)

1. (Facoltativo) Specifica il file di metadati da importare, fornito in formato CSV, nel campo File di metadati e fai clic su **[!UICONTROL Successivo]** per passare a **[!UICONTROL Posizione e filtri]**.
1. Per definire una posizione in DAM in cui importare le risorse utilizzando il campo **[!UICONTROL Cartella risorse di destinazione]**, specifica un percorso. Esempio: `/content/dam/imported_assets`.
1. (Facoltativo) Nella sezione **[!UICONTROL Scegli filtri]**, specifica la dimensione minima in MB del file delle risorse da includere nel processo di acquisizione nel campo **[!UICONTROL Filtra per dimensione min]**.
1. (Facoltativo) Specifica la dimensione massima in MB del file delle risorse da includere nel processo di acquisizione del campo **[!UICONTROL Filtra per dimensione max]**.
1. (Facoltativo) Seleziona i tipi MIME da includere nel processo di acquisizione utilizzando il campo **[!UICONTROL Includi tipo MIME]**. In questo campo è possibile selezionare più tipi MIME. Se non definisci un valore, tutti i tipi MIME vengono inclusi nel processo di acquisizione.

1. (Facoltativo) Seleziona i tipi MIME da escludere dal processo di acquisizione utilizzando il campo **[!UICONTROL Escludi tipo MIME]**. In questo campo è possibile selezionare più tipi MIME. Se non definisci un valore, tutti i tipi MIME vengono inclusi nel processo di acquisizione.

   ![Filtri di importazione in blocco](assets/bulk-import-location.png)

1. Fai clic su **[!UICONTROL Avanti]**. Seleziona **[!UICONTROL Salva ed esegui importazione]** per salvare la configurazione ed eseguire l’importazione in blocco. Seleziona **[!UICONTROL Salva importazione]** per salvare la configurazione in modo da poterla eseguire in un secondo momento.

   ![Esegui importazione in blocco](assets/bulk-import-run.png)

1. Fai clic su **[!UICONTROL Salva]** per eseguire l’opzione selezionata.

### Gestione dei nomi dei file durante l’importazione in blocco {#filename-handling-bulkimport-assets-view}

Quando importi risorse o cartelle in blocco, [!DNL Experience Manager Assets] importa l&#39;intera struttura di ciò che esiste nell&#39;origine di importazione. [!DNL Experience Manager] segue le regole predefinite per i caratteri speciali nei nomi delle risorse e delle cartelle; pertanto, questi nomi di file devono essere bonificati. Sia per il nome della cartella che per quello della risorsa, il titolo definito dall’utente rimane invariato e viene memorizzato in `jcr:title`.

Durante l’importazione in blocco, [!DNL Experience Manager] cerca le cartelle esistenti per evitare di reimportare le risorse e le cartelle e verifica inoltre le regole di bonifica applicate nella cartella principale in cui avviene l’importazione. Se le regole di bonifica vengono applicate nella cartella padre, le stesse regole vengono applicate all&#39;origine di importazione. Per le nuove importazioni, per gestire i nomi file di risorse e cartelle vengono applicate le seguenti regole di bonifica.

Per ulteriori informazioni sui nomi non consentiti, sulla gestione dei nomi delle risorse e sulla gestione dei nomi delle cartelle durante l’importazione in blocco, consulta [Gestione dei nomi dei file durante l’importazione in blocco nella vista Amministrazione](add-assets.md##filename-handling-bulkimport).

## Visualizzare le configurazioni di importazione in blocco esistenti {#view-import-configuration}

Se selezioni di salvare la configurazione dopo averla creata, questa viene visualizzata nella scheda **[!UICONTROL Importazioni salvate]**.

![Salvare la configurazione dell’importazione in blocco](assets/bulk-import-save.png)

Se selezioni di salvare ed eseguire l’importazione, la configurazione di importazione viene visualizzata nella scheda **[!UICONTROL Importazioni eseguite]**.

![Salvare la configurazione dell’importazione in blocco](assets/bulk-import-executed.png)

Se pianifichi un’importazione, questa viene visualizzata nella scheda **[!UICONTROL Importazioni pianificate]**.

## Modificare la configurazione dell’importazione in blocco {#edit-import-configuration}

Per modificare i dettagli della configurazione, fai clic su Altre opzioni (...) corrispondenti al nome della configurazione, quindi fai clic su **[!UICONTROL Modifica]**. Durante l’operazione di modifica non è possibile modificare il titolo della configurazione e l’origine dati di importazione. Puoi modificare la configurazione dalle schede Importazioni eseguite, Importazioni pianificate e Importazioni salvate.

![Modificare la configurazione dell’importazione in blocco](assets/bulk-import-edit.png)

## Pianificare importazioni una tantum o ricorrenti {#schedule-imports}

Per pianificare un’importazione in blocco una tantum o ricorrente, effettua le seguenti operazioni:

1. fare clic su Altre opzioni (...) corrispondenti al nome di configurazione disponibile nella **[!UICONTROL Importazioni eseguite]** o **[!UICONTROL Importazioni salvate]** e fai clic su **[!UICONTROL Pianificazione]**. Puoi anche riprogrammare un’importazione pianificata esistente: passa alla scheda **[!UICONTROL Importazioni pianificate]** e fai clic su **[!UICONTROL Pianifica]**.

1. Imposta un’acquisizione una tantum o una pianificazione oraria, giornaliera o settimanale. Fai clic su **[!UICONTROL Invia]**.

   ![Pianificare la configurazione dell’importazione in blocco](assets/bulk-import-schedule.png)

## Verificare lo stato dell’importazione {#import-health-check}

Per convalidare la connessione all&#39;origine dati, fare clic su Altre opzioni (...) corrispondenti al nome della configurazione e quindi fare clic su **[!UICONTROL Verifica]**. Se la connessione ha esito positivo, Experience Manager Assets presenta il seguente messaggio:

![Verifica dello stato dell’importazione in blocco](assets/bulk-import-health-check.png)

## Eseguire un’esecuzione di prova prima di eseguire un’importazione {#dry-run-bulk-import}

Fai clic su Altre opzioni (...) corrispondenti al nome della configurazione e fai clic su **[!UICONTROL Dry Run]** per richiamare un’esecuzione dei test per il processo di importazione in blocco. In Experience Manager Assets vengono visualizzati i dettagli seguenti sul processo di importazione in blocco:

![Verifica dello stato dell’importazione in blocco](assets/bulk-import-dry-run.png)

## Eseguire un’importazione in blocco {#run-bulk-import}

Se hai salvato l’importazione durante la creazione della configurazione, puoi passare alla scheda Importazioni salvate, fare clic su Altre opzioni (...) corrispondenti alla configurazione e fare clic su **[!UICONTROL Esegui]**.

Analogamente, se è necessario eseguire un&#39;importazione già eseguita, passare alla scheda Importazioni eseguite, fare clic su Altre opzioni (...) corrispondenti al nome della configurazione e fare clic su **[!UICONTROL Esegui]**.

## Interrompere o pianificare un’importazione in corso {#schedule-stop-ongoing-report}

Per pianificare o interrompere un’importazione in blocco in corso, puoi usare la finestra di dialogo sullo stato dell’importazione in blocco che viene visualizzata nella pagina home di Importazione in blocco durante un’importazione.

![Importazione in corso](assets/bulk-import-progress.png)

Puoi anche visualizzare le risorse importate nella cartella di destinazione, facendo clic su **[!UICONTROL Visualizza risorse]**.


## Eliminare una configurazione di importazione in blocco {#delete-bulk-import-configuration}

Fai clic su Altre opzioni (...) corrispondenti al nome della configurazione esistente in **[!UICONTROL Importazioni eseguite]**, **[!UICONTROL Importazioni pianificate]**, o **[!UICONTROL Importazioni salvate]** e fai clic su **[!UICONTROL Elimina]** per eliminare la configurazione Importazione in blocco.

## Passare alle risorse dopo l’importazione in blocco {#view-assets-after-bulk-import}

Per visualizzare il percorso di destinazione delle risorse in cui vengono importate dopo l&#39;esecuzione del processo Importazione in blocco, fare clic su Altre opzioni (...) corrispondenti al nome della configurazione e quindi fare clic su **[!UICONTROL Visualizza risorse]**.
