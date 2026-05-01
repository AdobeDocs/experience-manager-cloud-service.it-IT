---
title: Come si inviano i dati a un archivio dell’elenco SharePoint all’invio di un modulo adattivo?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: Come collegare un elenco SharePoint per un modulo adattivo?, Invia a SharePoint, Crea una configurazione elenco SharePoint, Utilizza l’azione Invia a SharePoint in un modulo adattivo, Connetti un modulo adattivo a Microsoft&reg; Elenco SharePoint.
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 0e5045b87719781301d91874c7355eda9426beef
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 4%

---

# Collegare un modulo adattivo all’elenco di Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span> Questo video è applicabile solo ai Componenti core. Per i componenti UE/Foundation, fare riferimento all&#39;articolo.</span>

Per utilizzare l&#39;azione di invio [!UICONTROL Invia a elenco SharePoint] in un modulo adattivo:

1. [Crea una configurazione elenco SharePoint](#1-create-a-sharepoint-list-configuration): connette AEM Forms all&#39;archiviazione elenco Microsoft® Sharepoint.
1. [Utilizzare l&#39;invio utilizzando il modello dati del modulo (FDM) in un modulo adattivo](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm): collega il modulo adattivo a Microsoft® SharePoint configurato.

## &#x200B;1. Creare una configurazione dell’elenco SharePoint

Per collegare AEM Forms all’elenco di Microsoft® Sharepoint:

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Elenco SharePoint]** dall&#39;elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.
1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l&#39;ID client, il segreto client e l&#39;ID tenant per l&#39;URL OAuth, consulta la [documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Puoi recuperare `Client ID` e `Client Secret` dell&#39;app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungi l&#39;URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l&#39;URL dell&#39;istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` nella scheda **Microsoft® Graph** per fornire le autorizzazioni di lettura/scrittura. Aggiungere l&#39;autorizzazione `AllSites.Manage` nella scheda **Sharepoint** per interagire in remoto con i dati di SharePoint.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale Microsoft® Azure.

     >[!NOTE]
     >
     > Il campo **segreto client** è obbligatorio o facoltativo a seconda della configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Fai clic su **[!UICONTROL Connetti]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.
1. Selezionare **[!UICONTROL Sito SharePoint]** e **[!UICONTROL Elenco SharePoint]** dall&#39;elenco a discesa.
1. Selezionare **[!UICONTROL Crea]** per creare la configurazione cloud per Microsoft® SharePointList.

### Autenticazione basata su certificato {#certificate-based-authentication}

L&#39;autenticazione basata su certificato <span class="preview"> per la configurazione dell&#39;elenco di SharePoint si trova nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Nella procedura guidata di configurazione dell’elenco di SharePoint:

1. Imposta **[!UICONTROL Tipo di autenticazione]** su **Autenticazione basata su certificato**.
1. Specificare **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Alias certificato]**, **[!UICONTROL ID tenant]** e **[!UICONTROL Nome tenant]**.
1. Immetti l&#39;**[!UICONTROL URL sito SharePoint]**, verifica la connessione del sito se necessario e seleziona il **[!UICONTROL elenco SharePoint]**.
1. Fai clic su **[!UICONTROL Connetti]** per verificare la connessione, quindi su **[!UICONTROL Salva e chiudi]** per salvare la configurazione.

Nella schermata seguente viene visualizzata la configurazione dell&#39;elenco di SharePoint con **autenticazione basata su certificato**:

![Configurazione elenco SharePoint con autenticazione basata su certificato](/help/forms/assets/sharepoint-list-certificate-auth-configuration.png){width=50%, height=50%, align=center}

Per preparare il certificato per AEM e Microsoft Azure, esegui i seguenti passaggi in AEM, quindi registra il certificato pubblico in Microsoft Azure.

**In AEM**

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
1. Cerca **[!UICONTROL fd-cloudservice]**, seleziona l&#39;utente e fai clic su **[!UICONTROL Proprietà]**.
1. Apri la scheda **[!UICONTROL Registro chiavi]**. Se un keystore non è ancora stato creato, fare clic su **[!UICONTROL Crea keystore]** e completare le richieste per impostare la password del keystore.
1. Aggiungi la chiave privata al keystore: espandi **[!UICONTROL Aggiungi chiave privata dal file keystore]** e carica il file **.jks**.
1. Immetti un **[!UICONTROL Alias]** che corrisponda all&#39;**[!UICONTROL Alias certificato]** nella configurazione dell&#39;elenco di SharePoint, invia il materiale chiave, quindi fai clic su **[!UICONTROL Salva e chiudi]**.

La schermata mostra il keystore dopo l’aggiunta del certificato. L&#39;**[!UICONTROL alias]** deve corrispondere all&#39;**[!UICONTROL alias certificato]** nella configurazione cloud di SharePoint List:

Archivio chiavi utente ![fd-cloudservice con alias certificato](/help/forms/assets/fd-cloudservice-keystore-certificate.png){width=50%, height=50%, align=center}

**In Microsoft Azure**

1. Apri la registrazione dell&#39;applicazione e vai a **Certificati e segreti** > **Certificati**.
1. Selezionare **Carica certificato** e caricare il file del certificato (chiave pubblica) che Azure deve considerare attendibile per l&#39;applicazione.

La schermata mostra la scheda **Certificati** nel portale Azure, dove puoi caricare il certificato per la registrazione all&#39;app:

![Certificati e segreti di registrazione per app Azure](/help/forms/assets/azure-app-registration-sharepoint-certificates.png){width=50%, height=50%, align=center}

## &#x200B;2. Utilizzare l’invio utilizzando il modello dati modulo (FDM) in un modulo adattivo {#use-submit-using-fdm}

È possibile utilizzare la configurazione dell’elenco SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in un elenco SharePoint. Per utilizzare un elenco SharePoint in un modulo adattivo come, effettua le seguenti operazioni:

1. [Creare un modello dati modulo (FDM) utilizzando la configurazione di Microsoft® SharePoint List](/help/forms/create-form-data-models.md)
1. [Configurare il modello dati modulo (FDM) per recuperare e inviare dati](/help/forms/work-with-form-data-model.md#configure-services)
1. [Creare un modulo adattivo](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurare l’azione di invio utilizzando un modello di dati del modulo (FDM)](/help/forms/using-form-data-model.md)

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio elenco di Microsoft® Sharepoint specificato.

>[!NOTE]
>
> In Microsoft® SharePoint List non sono supportati i seguenti tipi di colonna:
>
> * colonna immagine
> * colonna metadati
> * colonna persona
> * colonna di dati esterni

## Articoli correlati

{{af-submit-action}}
