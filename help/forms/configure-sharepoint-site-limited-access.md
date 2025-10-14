---
title: Come si configura un sito SharePoint con accesso limitato utilizzando l’ambito di autorizzazione?
description: Scopri come configurare il sito SharePoint con accesso limitato utilizzando l’ambito di autorizzazione.
keywords: Come configurare il sito SharePoint con accesso limitato?, Configurare SharePoint con accesso limitato, Utilizzare l'ambito di autorizzazione per limitare l'accesso al sito SharePoint.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 3230bab2-c1aa-409d-9f01-c42cf88b1135
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 3%

---

# Configurare il sito SharePoint con accesso limitato utilizzando l’ambito di autorizzazione

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Lo scopo dell&#39;accesso limitato o limitato è migliorare la gestione della sicurezza consentendo agli amministratori di controllare l&#39;accesso degli utenti a un particolare sito SharePoint o a un gruppo di siti SharePoint. Il livello di autorizzazione è utile quando devi concedere a un utente o a un gruppo l’accesso a un sito specifico senza consentire loro di visualizzare altri siti di SharePoint non consentiti.

## Vantaggi della configurazione del sito SharePoint con accesso limitato

Vantaggi per fornire accesso limitato al sito SharePoint:

* **Protezione avanzata**: limitando l&#39;accesso, è possibile garantire che solo il personale autorizzato possa visualizzare o manipolare informazioni riservate, riducendo il rischio di accesso non autorizzato.

* **Principio del privilegio minimo**: fornisce agli utenti i livelli minimi di accesso, o autorizzazioni, necessari per eseguire le loro funzioni lavorative. Questo riduce al minimo l&#39;esposizione di ogni utente a parti sensibili della rete, che possono essere protette da potenziali minacce interne.

* **Protezione dei dati**: l&#39;accesso limitato consente di proteggere i dati critici dall&#39;esposizione. Garantisce che solo gli utenti che devono vedere i dati possano accedervi, aspetto essenziale per rispettare le normative sulla protezione dei dati.

* **Prevenzione della perdita accidentale di dati**: con un numero inferiore di persone in grado di modificare il contenuto, le possibilità di eliminare o alterare accidentalmente dati importanti si riducono notevolmente.

* **Flusso di dati controllato**: consente di controllare il flusso di informazioni all&#39;interno e all&#39;esterno dell&#39;organizzazione, garantendo che i dati non finiscano nelle mani sbagliate.

## Configurare SharePoint con accesso limitato utilizzando l’ambito di autorizzazione

Per configurare SharePoint Sites con accesso limitato utilizzando gli ambiti di autorizzazione, effettua le seguenti operazioni:

1. [Creare un’applicazione con &#x200B;](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [Imposta l’ambito di autorizzazione nell’istanza di AEM](#set-the-authorization-scope-at-aem-instance)

### Creare un’applicazione con l’autorizzazione limitata nel portale di Azure

Creare un&#39;applicazione nel [portale di Microsoft Azure](https://portal.azure.com/#home) con l&#39;ambito di autorizzazione `Sites.Selected` nell&#39;API Graph di Microsoft.

![Sito SharePoint selezionato](/help/forms/assets/sharepoint-selected-site.png)

Per informazioni su come recuperare `Client ID`, `Client Secret` e `Tenant ID` per `OAuth URL`, consulta [Documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
* Nel portale Microsoft® Azure, aggiungere l&#39;URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l&#39;URL dell&#39;istanza di authoring.
* Aggiungi l&#39;ambito delle autorizzazioni `offline_access` e `Sites.Selected` nell&#39;API Graph di Microsoft per fornire accesso limitato ai siti.
* Per URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale di Microsoft® Azure.

Per utilizzare l&#39;autorizzazione API `Sites.Selected` è necessaria un&#39;applicazione registrata nel portale di Azure con le autorizzazioni appropriate impostate per i siti SharePoint Online. Questa configurazione garantisce che l’applicazione disponga dell’autorizzazione necessaria per interagire con il sito SharePoint all’interno dell’ambito definito, fornendo in tal modo l’accesso limitato richiesto.

Per istruzioni sullo sviluppo di applicazioni che utilizzano le autorizzazioni [&#x200B; per Sites SharePoint Online, consulta l&#39;](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476)articolo del blog - Sviluppo di applicazioni che utilizzano le autorizzazioni Sites.Selected per i siti SPO`Sites.Selected`.

### Imposta l’ambito di autorizzazione nell’istanza di AEM

Per fornire un accesso limitato a un sito SharePoint di Microsoft, è essenziale impostare correttamente l’ambito di autorizzazione. Per impostare l’ambito di autorizzazione e collegare AEM Forms allo storage Microsoft® SharePoint:

1. Vai alla tua istanza di **AEM Forms Author** > **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Dopo aver selezionato **[!UICONTROL Microsoft® SharePoint]**, sei reindirizzato a **[!UICONTROL SharePoint Browser]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Libreria documenti di SharePoint]** dall&#39;elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.

   ![Accesso sito limitato SharePoint](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]**. Per informazioni su come recuperare l&#39;ID client e il segreto client, consulta la [documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).

1. Utilizza URL OAuth come `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale di Microsoft® Azure.

   >[!NOTE]
   >
   > Il campo **segreto client** è obbligatorio oppure facoltativo in base alla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Aggiungi `offline_access Sites.Selected` nel campo `Authorization Scope`. Quando si aggiunge l&#39;ambito `offline_access Sites.Selected` nel campo della casella di testo `Authorization Scope`, la casella di testo `SharePoint Site ID` diventa visibile sullo schermo.

1. Specifica l&#39;ID del sito SharePoint. Per informazioni su come recuperare l&#39;ID sito di SharePoint, consulta la sezione [Byte aggiuntivi](#extra-bytes).

1. Fare clic su **[!UICONTROL Controlla connessione sito]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.

1. Selezionare **Sito SharePoint** > **Raccolta documenti** > **Cartella SharePoint** per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel sito SharePoint selezionato.
   >* Creare una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente nella raccolta `Documents` del sito SharePoint selezionato facendo clic su **Crea cartella**.

Ora puoi utilizzare questa configurazione di [SharePoint Sites per l&#39;azione di invio in un modulo adattivo](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af).

## Byte aggiuntivi

Per recuperare il valore di `SharePoint Site ID`:
1. Passa alle [API Esplora grafico di Microsoft](https://developer.microsoft.com/en-us/graph/graph-explorer).
1. Nel riquadro a sinistra, sotto le API `SharePoint Sites`, fare clic su `Search for a SharePoint site by keyword`.
1. Sostituire il segnaposto `contoso` con il nome effettivo del sito SharePoint per recuperare l&#39;ID sito corrispondente.

   ![ID raccolta documenti di SharePoint](/help/forms/assets/sharepoint-site-id.png)

Facendo clic sul pulsante `Run Query`, l&#39;ID sito viene visualizzato sullo schermo.
