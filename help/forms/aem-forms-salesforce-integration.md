---
title: Come integrare Salesforce utilizzando il flusso delle credenziali client OAuth 2.0 con AEM Forms?
description: Scopri come integrare Salesforce con AEM Forms utilizzando il flusso delle credenziali client OAuth 2.0. Vengono visualizzati i passaggi per l’integrazione con AEM Forms Salesforce.
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration, AEM Forms Salesforce integration
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: 9eb15dda5f56938d686d0b863cb1ffa841f8228b
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# Integrare il modulo adattivo con Salesforce {#configure-salesforce-with-ouath-2.0-client-credential}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

L’integrazione di Adobe Experience Manager (AEM) Forms con Salesforce consente alle organizzazioni di semplificare i processi collegando le funzionalità di creazione e gestione dei moduli alla piattaforma Salesforce. La connessione di un modulo adattivo con Salesforce consente uno scambio di dati fluido tra le due piattaforme. Quando gli utenti inviano i moduli, i dati vengono sincronizzati automaticamente con Salesforce. Garantisce che tutte le informazioni del cliente siano aggiornate e centralizzate all&#39;interno del sistema.

Puoi utilizzare le credenziali client OAuth 2.0 per integrare AEM Forms con l’applicazione Salesforce. Le credenziali client OAuth 2.0 sono un metodo standard e sicuro per la comunicazione diretta senza il coinvolgimento dell’utente.

![Flusso di lavoro durante l&#39;impostazione della comunicazione tra l&#39;applicazione AEM Forms e Salesforce](/help/forms/assets/salesforce-workflow.png)

AEM Forms scambia le credenziali del client (chiave consumer e segreto consumer), definite nell’applicazione connessa Salesforce, per ottenere un token di accesso.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

L’utilizzo delle credenziali del client OAuth 2.0 per l’autenticazione rispetto all’autenticazione del flusso del codice di autorizzazione offre diversi vantaggi:

* L&#39;autenticazione delle credenziali client OAuth 2.0 consente più di cinque connessioni per utente.
* La configurazione dell’origine dati dell’AEM continua a funzionare su disattivazione, modifiche di accesso, aggiornamento della password per un utente AEM.

## Prerequisiti {#prerequisites}

Prima di impostare la comunicazione tra un’applicazione Salesforce e un ambiente AEM:

* Crea un&#39;app connessa a [Salesforce con flusso di credenziali client OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5) e un utente solo API per la tua organizzazione e ottieni la chiave consumer e il segreto consumer per l&#39;app.

* Assicurati che il file Swagger sia configurato in modo appropriato per corrispondere alle API della tua organizzazione. In alternativa, puoi scegliere di [creare un file Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=it) da zero, adatto all&#39;utilizzo nell&#39;ambiente AEM.


## Configurare l’applicazione Salesforce utilizzando il flusso delle credenziali client OAuth 2.0 {#steps-to-create-aem-datasource-configuration}

Per collegare il modulo adattivo all’applicazione Salesforce utilizzando le impostazioni di autenticazione delle credenziali client OAuth 2.0, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**.
1. Seleziona la cartella di configurazione.
1. Fai clic su **[!UICONTROL Crea]** per visualizzare **[!UICONTROL Crea configurazione Data Source]**.
1. Specifica il **[!UICONTROL Titolo]** e seleziona il **[!UICONTROL Tipo di servizio]** come **[!UICONTROL Servizio RESTful]**.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona **[!UICONTROL Swagger Source]** come **[!UICONTROL File].**

   >[!NOTE]
   >
   > Quando il file Swagger è selezionato, lo schema, il nome host e il percorso di base vengono popolati automaticamente.

1. Carica il file Swagger creato dal computer locale facendo clic su **[!UICONTROL Sfoglia]**.
1. Selezionare **[!UICONTROL Tipo di autenticazione]** come **[!UICONTROL OAuth 2.0]** e viene visualizzato il pannello **[!UICONTROL Impostazioni autenticazione]**.
1. Selezionare **[!UICONTROL Tipo di concessione]** come **[!UICONTROL Credenziali client]**.
1. Specifica l&#39;**[!UICONTROL ID client]** e il **[!UICONTROL Segreto client]** ottenuti dall&#39;app connessa Salesforce.
1. Specifica l&#39;**[!UICONTROL URL token di accesso]** in formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Ogni organizzazione ha il proprio nome di dominio specifico.

1. Fare clic su **[!UICONTROL Verifica connessione]**.
1. Se la connessione riesce, fare clic sul pulsante **[!UICONTROL Crea]**.


Dopo aver configurato l’applicazione Salesforce, puoi utilizzare la configurazione durante la creazione del modello dati del modulo (FDM). Per ulteriori informazioni, vedere [Creare un modello dati modulo (FDM)](create-form-data-models.md). [Configura l&#39;azione di invio Modello dati modulo](/help/forms/using-form-data-model.md) per un modulo adattivo per inviare dati alle applicazioni Salesforce.

Per ulteriori informazioni sulla creazione e l&#39;utilizzo di Form Data Model (FDM) nei flussi di lavoro aziendali, vedere [Integrazione dei dati](data-integration.md).

## Articoli correlati

{{af-submit-action}}


