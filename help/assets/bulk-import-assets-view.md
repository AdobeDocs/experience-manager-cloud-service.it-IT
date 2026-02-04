---
title: Importazione in blocco delle risorse utilizzando la vista Assets
description: Scopri come importare in blocco le risorse utilizzando la nuova interfaccia utente di Assets (vista Assets). Consente agli amministratori di importare un numero elevato di risorse da un’origine dati ad AEM Assets.
exl-id: 10f9d679-7579-4650-9379-bc8287cb2ff1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User
source-git-commit: 655f84593adb1199bcfc21cb54071feb3c8523c5
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 88%

---

# Importazione in blocco delle risorse utilizzando la vista Assets  {#bulk-import-assets-view}

L’importazione in blocco nella vista AEM Assets consente agli amministratori di importare in AEM Assets un numero elevato di risorse da un’origine dati. Gli amministratori non devono più caricare singole risorse o cartelle in AEM Assets.

>[!NOTE]
>
>L’importazione in blocco delle visualizzazioni di Assets utilizza lo stesso back-end dell’importazione in blocco delle visualizzazioni di amministrazione. Tuttavia, offre più origini dati da cui importare e un’esperienza utente più semplice.

Puoi importare le risorse dalle seguenti origini dati:

* Azure
* AWS
* Google Cloud
* Dropbox
* OneDrive

>[!VIDEO](https://video.tv.adobe.com/v/3451967/?captions=ita&learn=on){transcript=true}

## Prerequisiti {#prerequisites}

| Origine dati | Prerequisiti |
|-----|------|
| Azure | <ul> <li>Account archiviazione Azure </li> <li> Contenitore BLOB di Azure <li> Chiave di accesso Azure o token SAS in base alla modalità di autenticazione </li></ul> |
| AWS | <ul> <li>Area geografica AWS </li> <li> Bucket AWS <li> Chiave di accesso AWS </li><li> Segreto di accesso AWS </li></ul> |
| Google Cloud | <ul> <li>Bucket GCP </li> <li> E-mail account servizio GCP <li> Chiave privata account servizio GCP</li></ul> |
| Dropbox | <ul> <li>ID client Dropbox (chiave app) </li> <li> Segreto client Dropbox (segreto app)</li></ul> |
| OneDrive | <ul> <li>ID tenant OneDrive  </li> <li> ID client OneDrive</li><li> Segreto client OneDrive</li></ul> |

Oltre a questi prerequisiti basati sull’origine dati, è necessario conoscere il nome della cartella di origine disponibile nell’origine dati che contiene tutte le risorse da importare in AEM Assets.

## Configurare l’applicazione per sviluppatori di Dropbox {#dropbox-developer-application}

Prima di importare le risorse dall’account di Dropbox ad AEM Assets, crea e configura l’applicazione per sviluppatori di Dropbox.

Esegui i passaggi seguenti:

1. Accedi al tuo [Account Dropbox](https://www.dropbox.com/developers) e fai clic su **[!UICONTROL Create apps]** (Crea app). <br>Se utilizzi un account Dropbox Enterprise, devi avere accesso al ruolo di amministratore dei contenuti.

1. Nella sezione **[!UICONTROL Choose an API]** (Scegli un API), seleziona l’unico pulsante di scelta disponibile.

1. Nella sezione **[!UICONTROL Choose the type of access you need]** (Scegli il tipo di accesso necessario), seleziona una delle opzioni seguenti:

   * Seleziona **[!UICONTROL App folder]** (Cartella app), se hai bisogno di accedere a una singola cartella creata all’interno dell’applicazione nel tuo account Dropbox.

   * Seleziona **[!UICONTROL Full Dropbox]** (Dropbox completo), se hai bisogno di accedere a tutti i file e le cartelle all’interno del tuo account Dropbox.

1. Specifica un nome per l’applicazione e fai clic su **[!UICONTROL Create app]** (Crea app).

1. Nella scheda **[!UICONTROL Settings]** (Impostazioni) dell’applicazione creata, aggiungi https://experience.adobe.com alla sezione **[!UICONTROL Redirect URIs]** (URI di reindirizzamento).

1. Copia i valori per i campi **[!UICONTROL App key]** (Chiave app) e **[!UICONTROL App secret]** (Segreto app). I valori sono necessari durante la configurazione dello strumento di importazione in blocco in AEM Assets.

1. Nella scheda **[!UICONTROL Permissions]** (Autorizzazioni), aggiungi le seguenti autorizzazioni all’interno della sezione **[!UICONTROL Individual scopes]** (Singoli ambiti).

   * account_info.read

   * files.metadata.read

   * files.content.read

   * files.content.write

1. Per salvare le modifiche, fai clic su **[!UICONTROL Submit]** (Invia).

## Configurare l’applicazione per sviluppatori OneDrive {#onedrive-developer-application}

Prima di importare risorse dall’account OneDrive in AEM Assets, crea e configura l’applicazione per sviluppatori OneDrive.

### Creare un’applicazione

1. Accedi al tuo [Account OneDrive](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) e fai clic su **[!UICONTROL New registration]** (Nuova registrazione).

1. Specifica un nome per l’applicazione, seleziona **[!UICONTROL Accounts in this organizational directory only (Adobe only - Single tenant)]** (Solo account in questa directory organizzativa (solo Adobe: tenant singolo)) da **[!UICONTROL Supported account types]** (Tipi di account supportati).

1. Per aggiungere degli URI di reindirizzamento, effettua le seguenti operazioni:

   1. Nel menu a discesa **[!UICONTROL Select a platform]** (Seleziona una piattaforma), seleziona **[!UICONTROL Web]**.

   1. Alla sezione **[!UICONTROL Redirect URIs]** (URI di reindirizzamento) aggiungi https://experience.adobe.
   <!-- Add the first URI and click **[!UICONTROL Configure]** to add it. You can add more by clicking **[!UICONTROL Add URI]** option available in the **[!UICONTROL Web]** section on the **[!UICONTROL Authentication]** page. -->

1. Fai clic su **[!UICONTROL Registra]**. L’applicazione viene creata con successo.

1. Copia i valori per i campi **[!UICONTROL Application (client) ID]** (ID applicazione (client)) e **[!UICONTROL Directory (tenant) ID]** (ID directory (tenant)). I valori sono necessari durante la configurazione dello strumento di importazione in blocco in AEM Assets.

1. Fai clic su **[!UICONTROL Add a certificate or secret]** (Aggiungi un certificato o un segreto) in corrispondenza dell’opzione **[!UICONTROL Client credentials]** (Credenziali client).

1. Fai clic su **[!UICONTROL New client secret]** (Nuovo segreto client), fornisci la descrizione del segreto client, la scadenza e fai clic su **[!UICONTROL Add]** (Aggiungi).

1. Dopo aver creato il segreto client, copia il campo **[!UICONTROL Value]** (Valore) (non copiare il campo ID segreto). Verrà richiesto per configurare l’importazione in blocco in AEM Assets.

### Aggiungere le autorizzazioni API

Per aggiungere le autorizzazioni API per l’applicazione, effettua le seguenti operazioni:

1. Fai clic su **[!UICONTROL API permissions]** (Autorizzazioni API) nel riquadro a sinistra e fai clic su **[!UICONTROL Add a permission]** (Aggiungi un’autorizzazione).
1. Fai clic su **[!UICONTROL Microsoft Graph]** > **[!UICONTROL Delegated permissions]** (Grafico Microsoft > Autorizzazioni delegate). La sezione **[!UICONTROL Select Permission]** (Seleziona autorizzazione) mostra le autorizzazioni disponibili.
1. Seleziona l’autorizzazione `offline_access` da `OpenId permissions` e l’autorizzazione `Files.ReadWrite.All` da `Files`.
1. Fai clic su **[!UICONTROL Add permissions]** (Aggiungi autorizzazioni) per salvare gli aggiornamenti.

## Creare una configurazione di importazione in blocco {#create-bulk-import-configuration}

Per creare una configurazione di importazione in blocco in [!DNL Experience Manager Assets], effettua le seguenti operazioni:

1. Fai clic nel riquadro a sinistra su **[!UICONTROL Bulk Import]** (Importazione in blocco) e quindi su **[!UICONTROL Create Import]** (Crea importazione).
1. Seleziona l’origine dati. Le opzioni disponibili includono **[!UICONTROL Azure]**, **[!UICONTROL AWS]**, **[!UICONTROL Google Cloud]**, **[!UICONTROL Dropbox]** e **[!UICONTROL OneDrive]**.
1. Specifica un nome per la configurazione dell’importazione in blocco nel campo **[!UICONTROL Nome]**.
1. Specifica le credenziali specifiche dell’origine dati, come indicato nei [Prerequisiti](#prerequisites).
1. Immetti il nome della cartella principale che contiene le risorse nell’origine dati nel campo **[!UICONTROL Cartella di origine]**.

   >[!NOTE]
   >
   >Se utilizzi Dropbox come origine dati, specifica il percorso della cartella di origine in base alle regole seguenti:
   >* Se durante la creazione dell’applicazione di Dropbox hai selezionato **Full Dropbox** (Dropbox completo), la cartella che contiene le risorse è già presente in `https://www.dropbox.com/home/bulkimport-assets`, quindi specifica `bulkimport-assets` nel campo **[!UICONTROL Cartella di origine]**.
   >* Se durante la creazione dell’applicazione di Dropbox hai selezionato **App folder** (Cartella app), la cartella che contiene le risorse è già presente in `https://www.dropbox.com/home/Apps/BulkImportAppFolderScope/bulkimport-assets`, quindi specifica `bulkimport-assets` nel campo **[!UICONTROL Cartella di origine]**, dove `BulkImportAppFolderScope` fa riferimento al nome dell’applicazione. In questo caso, `Apps` viene aggiunto automaticamente dopo `home`.

   >[!NOTE]
   >
   >Se si utilizza OneDrive come origine dati, specificare il percorso della cartella di origine in base alle regole seguenti:
   >* Specifica solo il nome della cartella principale, senza il dominio. Se il percorso URL completo della cartella è `https://my.sharepoint.com/my?id=/personal/user/Documents/Importfolder/`, specificare `/Importfolder/` nel campo **[!UICONTROL Cartella Source]**.
   >* Se il nome della cartella contiene più parole separate da spazi, specificalo con gli spazi nella configurazione dell’importazione in blocco.
   >* La cartella di origine deve trovarsi nella directory principale. I percorsi delle cartelle non sono supportati.

1. (Facoltativo) Seleziona l’opzione **[!UICONTROL Elimina il file di origine dopo l’importazione]** per eliminare i file originali dall’archivio dati di origine dopo l’importazione in Experience Manager Assets.
1. Seleziona la **[!UICONTROL Modalità di importazione]**. Seleziona **[!UICONTROL Ignora]**, **[!UICONTROL Sostituisci]** o **[!UICONTROL Crea versione]**. La modalità Ignora è l’impostazione predefinita e, in questa modalità, l’importazione di una risorsa viene ignorata se esiste già.
   ![Importa dettagli origine](/help/assets/assets/bulk-import-source-details.png)

1. (Facoltativo) Specifica il file di metadati da importare, fornito in formato CSV, nel campo **[!UICONTROL File di metadati]**. Il file di origine dei metadati deve trovarsi nella cartella di origine. Fai clic su **[!UICONTROL Avanti]** per passare a **[!UICONTROL Posizione e filtri]**.

   >[!NOTE]
   >
   >A seconda delle regole di sicurezza dell&#39;organizzazione, è possibile che sia necessario il consenso dell&#39;amministratore per la connessione dell&#39;applicazione allo strumento Importazione in blocco. Se necessario, l’amministratore deve fornire il consenso prima di salvare la configurazione dell’importazione in blocco.

1. Per definire una posizione in DAM in cui importare le risorse utilizzando il campo **[!UICONTROL Cartella risorse di destinazione]**, specifica un percorso. Esempio: `/content/dam/imported_assets`.
1. (Facoltativo) Nella sezione **[!UICONTROL Scegli filtri]**, specifica la dimensione minima in MB del file delle risorse da includere nel processo di acquisizione nel campo **[!UICONTROL Filtra per dimensione min]**.
1. (Facoltativo) Specifica la dimensione massima in MB del file delle risorse da includere nel processo di acquisizione del campo **[!UICONTROL Filtra per dimensione max]**.
1. (Facoltativo) Seleziona i tipi MIME da includere nel processo di acquisizione utilizzando il campo **[!UICONTROL Includi tipo MIME]**. In questo campo è possibile selezionare più tipi MIME. Se non definisci un valore, tutti i tipi MIME vengono inclusi nel processo di acquisizione.

1. (Facoltativo) Seleziona i tipi MIME da escludere dal processo di acquisizione utilizzando il campo **[!UICONTROL Escludi tipo MIME]**. In questo campo è possibile selezionare più tipi MIME. Se non definisci un valore, tutti i tipi MIME vengono inclusi nel processo di acquisizione.

   ![Filtri di importazione in blocco](assets/bulk-import-location.png)

1. Fai clic su **[!UICONTROL Avanti]**. Seleziona una delle opzioni seguenti in base alle tue preferenze:

   * Seleziona **[!UICONTROL Salva importazione]** per salvare la configurazione in modo da poterla eseguire in un secondo momento.
   * **[!UICONTROL Salva ed esegui importazione]** per salvare la configurazione ed eseguire l’importazione in blocco.
   * **[!UICONTROL Salva e pianifica l’importazione]** per salvare la configurazione e pianificare l’importazione in blocco per un momento successivo. Puoi scegliere la frequenza dell’importazione in blocco e impostare la data e l’ora dell’importazione. L’importazione in blocco viene eseguita alla data e all’ora impostate nella frequenza selezionata.

   ![Esegui importazione in blocco](assets/save-run.png)

1. Fai clic su **[!UICONTROL Salva]** per eseguire l’opzione selezionata.

### Gestione dei nomi dei file durante l’importazione in blocco {#filename-handling-bulkimport-assets-view}

Quando importi risorse o cartelle in blocco, [!DNL Experience Manager Assets] importa l’intera struttura di ciò che esiste nell’origine di importazione. [!DNL Experience Manager] segue le regole predefinite per i caratteri speciali nei nomi delle risorse e delle cartelle; pertanto, questi nomi di file devono essere bonificati. Sia per il nome della cartella che per quello della risorsa, il titolo definito dall’utente rimane invariato e viene memorizzato in `jcr:title`.

Durante l’importazione in blocco, [!DNL Experience Manager] cerca le cartelle esistenti per evitare di reimportare le risorse e le cartelle e verifica inoltre le regole di bonifica applicate nella cartella principale in cui avviene l’importazione. Se le regole di bonifica vengono applicate nella cartella principale, le stesse regole vengono applicate all’origine di importazione. Per le nuove importazioni, per gestire i nomi file di risorse e cartelle vengono applicate le seguenti regole di bonifica.

Per ulteriori informazioni sui nomi non consentiti, sulla gestione dei nomi delle risorse e sulla gestione dei nomi delle cartelle durante l&#39;importazione in blocco, vedere [Gestione dei nomi dei file durante l&#39;importazione in blocco in Admin View](add-assets.md##filename-handling-bulkimport).

## Visualizzare le configurazioni di importazione in blocco esistenti {#view-import-configuration}

Per visualizzare le importazioni in blocco esistenti, seleziona l’opzione **[!UICONTROL Importazioni in blocco]** nel riquadro a sinistra. Viene visualizzata la pagina Importazioni in blocco con l’elenco di **[!UICONTROL Importazioni eseguite]**. <br>È inoltre possibile visualizzare le **[!UICONTROL Importazioni salvate]** e le **[!UICONTROL Importazioni pianificate]** dall’opzione a discesa.

![Salvare la configurazione dell’importazione in blocco](assets/bulk-import-options.png)

## Modificare la configurazione dell’importazione in blocco {#edit-import-configuration}

Per modificare i dettagli della configurazione, fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione, quindi fai clic su **[!UICONTROL Modifica]**. Durante l’operazione di modifica non è possibile modificare il titolo della configurazione e l’origine dati di importazione. Puoi modificare la configurazione dalle schede Importazioni eseguite, Importazioni pianificate e Importazioni salvate.

![Modificare la configurazione dell’importazione in blocco](assets/edit-bulk-import.png)

## Pianificare importazioni una tantum o ricorrenti {#schedule-imports}

Per pianificare un’importazione in blocco una tantum o ricorrente, effettua le seguenti operazioni:

1. Fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione nella scheda **[!UICONTROL Importazioni eseguite]** o **[!UICONTROL Importazioni salvate]**, quindi fai clic su **[!UICONTROL Pianifica]**. Puoi anche riprogrammare un’importazione pianificata esistente: passa alla scheda **[!UICONTROL Importazioni pianificate]** e fai clic su **[!UICONTROL Pianifica]**.

1. Imposta un’acquisizione una tantum o una pianificazione oraria, giornaliera o settimanale. Fai clic su **[!UICONTROL Invia]**.

   ![Pianificare la configurazione dell’importazione in blocco](assets/bulk-import-schedule.png)

## Verificare lo stato dell’importazione {#import-health-check}

Per convalidare la connessione all’origine dati, fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione, quindi fai clic su **[!UICONTROL Verifica]**. Se la connessione ha esito positivo, Experience Manager Assets presenta il seguente messaggio:

![Verifica dello stato dell’importazione in blocco](assets/bulk-import-health-check.png)

## Eseguire un’esecuzione di prova prima di eseguire un’importazione {#dry-run-bulk-import}

Fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione e fai clic su **[!UICONTROL Prova]** per richiamare un’esecuzione di test per il processo di importazione in blocco. In Experience Manager Assets vengono visualizzati i dettagli seguenti sul processo di importazione in blocco:

![Verifica dello stato dell’importazione in blocco](assets/bulk-import-dry-run.png)

## Eseguire un’importazione in blocco {#run-bulk-import}

Se hai salvato l’importazione durante la creazione della configurazione, passa alla scheda Importazioni salvate, fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza della configurazione e fai clic su **[!UICONTROL Esegui]**.

Allo stesso modo, se devi eseguire un’importazione già eseguita, passa alla scheda Importazioni eseguite, fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione e fai clic su **[!UICONTROL Esegui]**.

## Interrompere o pianificare un’importazione in corso {#schedule-stop-ongoing-report}

Per pianificare o interrompere un’importazione in blocco in corso, puoi usare la finestra di dialogo sullo stato dell’importazione in blocco che viene visualizzata nella pagina home di Importazione in blocco durante un’importazione.

![Importazione in corso](assets/bulk-import-progress.png)

Puoi anche visualizzare le risorse importate nella cartella di destinazione, facendo clic su **[!UICONTROL Visualizza risorse]**.

## Eliminare una configurazione di importazione in blocco {#delete-bulk-import-configuration}

Fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione esistente nelle schede **[!UICONTROL Importazioni eseguite]**, **[!UICONTROL Importazioni pianificate]** o **[!UICONTROL Importazioni salvate]** e fai clic su **[!UICONTROL Elimina]** per eliminare la configurazione Importazione in blocco.

## Passare alle risorse dopo l’importazione in blocco {#view-assets-after-bulk-import}

Per visualizzare il percorso di destinazione in cui le risorse vengono importate dopo l’esecuzione del processo di importazione in blocco, fai clic sull’![icona Altro](assets/do-not-localize/more-icon.svg) in corrispondenza del nome della configurazione, quindi fai clic su **[!UICONTROL Visualizza risorse]**.
