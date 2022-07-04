---
title: Integrare un modulo adattivo con Microsoft® Power Automate
description: Integrare un modulo adattivo con Microsoft® Power Automate.
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# Collegare un modulo adattivo con Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

È possibile configurare un modulo adattivo per eseguire un flusso cloud Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record a Power Automate Cloud Flow per l&#39;elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche aziendali intorno ai dati acquisiti e automatizzare i flussi di lavoro dei clienti. Di seguito sono riportati alcuni esempi delle operazioni che è possibile eseguire dopo l&#39;integrazione di un modulo adattivo con Microsoft® Power Automate:

* Utilizzare i dati di Forms adattivi in un processo aziendale Power Automation
* Utilizza Power Automate per inviare dati acquisiti a più di 500 origini dati o a qualsiasi API disponibile pubblicamente
* Eseguire calcoli complessi sui dati acquisiti
* Salvataggio dei dati Forms adattivi nei sistemi di storage a una pianificazione predefinita

L&#39;editor Forms adattivo fornisce **Richiamare un flusso Microsoft® Power Automate** l’azione di invio per l’invio di dati di moduli adattivi, allegati e documenti di record viene inviata a Flusso cloud di Power Automate. Per utilizzare l&#39;azione Invia per inviare i dati acquisiti a Microsoft® Power Automate, [Collega la tua istanza as a Cloud Service Forms con Microsoft® Power Automate](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## Prerequisiti

Per collegare un modulo adattivo con Microsoft® Power Automate sono necessari i seguenti requisiti:

* Licenza Microsoft® Power Automate Premium.
* Microsoft® [Flusso automatizzato dell&#39;alimentazione](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) con `When an HTTP request is received` per accettare i dati di invio del modulo adattivo.


* Un utente di Experience Manager con privilegi di amministratore di Forms Author e Forms.
* Verificare che l&#39;account utilizzato per la connessione a Power Automate sia il proprietario del flusso di Power Automate.


## Collega la tua istanza as a Cloud Service Forms con Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Esegui le seguenti operazioni per collegare l&#39;istanza as a Cloud Service di Forms con Microsoft® Power Automate:

1. Creare un&#39;applicazione Microsoft® Azure Active Directory
1. Creare la configurazione Microsoft® Power Automate Dataverse Cloud.
1. Crea configurazione cloud del servizio di flusso automatizzato Microsoft® Power
1. Pubblicare la configurazione Microsoft® Power Automate Dataverse Cloud.

### Crea applicazione Microsoft® Azure Active Directory {#ms-power-automate-application}

1. Accedi a [Portale di Azure](https://portal.azure.com/).
1. Seleziona [!UICONTROL Azure Active Directory] dalla navigazione a sinistra.
1. Nella pagina Directory predefinita, seleziona [!UICONTROL Registrazioni di app] dal pannello a sinistra.
1. Nella pagina Registrazioni app , fai clic su Nuove registrazioni .
1. Specifica il nome, i tipi di account supportati e l’URI di reindirizzamento nella pagina. Nell’URI di reindirizzamento, specifica quanto segue e fai clic su Salva.
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registra un&#39;applicazione Azure Active Directory](assets/power-automate-application.png)

   >[!NOTE]
   >Puoi anche specificare URI di reindirizzamento aggiuntivi, se necessario, dalla pagina Autenticazione .
   > Per i tipi di account supportati, seleziona un tenant singolo, più tenant o account Microsoft personale a seconda del caso d’uso


1. Nella pagina Autenticazione, abilita le seguenti opzioni e fai clic su Salva.


   * Token di accesso (utilizzati per flussi impliciti)
   * Token ID (utilizzati per flussi impliciti e ibridi)

1. Nella pagina Autorizzazioni API, fai clic su Aggiungi un’autorizzazione.
1. In API Microsoft®, seleziona Servizio flusso e seleziona le seguenti autorizzazioni.
   * Flows.Manage.All
   * Flows.Read.All

   Fai clic su Aggiungi autorizzazioni per salvare le autorizzazioni.
1. Nella pagina Autorizzazioni API, fai clic su Aggiungi un’autorizzazione. Seleziona le API utilizzate dalla mia organizzazione e cerca `DataVerse`.
1. Abilita user_impersonation e fai clic su Aggiungi autorizzazioni.
1. (Facoltativo) Nella pagina Certificati e segreti fare clic su Nuovo segreto client. Nella schermata Aggiungi un segreto client, fornisci una descrizione e un periodo di tempo per la scadenza del segreto e fai clic su Aggiungi. Viene generata una stringa segreta.
1. Tieni una nota specifica dell’organizzazione [URL dell’ambiente Dynamics](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### Creare la configurazione Microsoft® Power Automate Dataverse Cloud {#microsoft-power-automate-dataverse-cloud-configuration}

1. Nell’istanza di authoring di AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser di configurazione]**.
1. Sulla **[!UICONTROL Browser di configurazione]** pagina, tocca **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** specifica una finestra di dialogo **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e tocca **[!UICONTROL Crea]**. Crea un contenitore di configurazione per l’archiviazione dei Cloud Services. Assicurati che il nome della cartella non contenga spazio.
1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e apri il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore nel **[!UICONTROL Contenitore di configurazione]** campo .
1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare [!DNL Microsoft® Power Automate Flow Service] configurazione in AEM Forms.
1. Sulla **[!UICONTROL Configura il servizio Dataverse per Microsoft® Power Automate]** , specifica la **[!UICONTROL ID client]** (indicato anche come ID applicazione), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]** e **[!UICONTROL URL ambiente dinamico]**. Utilizza l’ID client, il segreto client, l’URL OAuth e l’URL dell’ambiente dinamico di [Applicazione Microsoft® Azure Active Directory](#ms-power-automate-application) creato nella sezione precedente. Utilizza l’opzione Endpoint nell’interfaccia utente dell’applicazione Microsoft® Azure Active Directory per trovare l’URL OAuth

![Utilizza l’opzione Endpoint nell’interfaccia utente dell’applicazione Microsoft Power Automate per trovare l’URL OAuth](assets/endpoints.png)
Utilizza l’opzione Endpoint nell’interfaccia utente dell’applicazione Microsoft® Power Automate per trovare l’URL OAuth

1. Tocca **[!UICONTROL Connetti]** . Se richiesto, accedi al tuo account Microsoft® Azure. Tocca **[!UICONTROL Salva]**.

### Creare la configurazione cloud del servizio di flusso automatico Microsoft® Power.

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizio di flusso automatico dell&#39;alimentazione Microsoft®]** e apri il contenitore di configurazione creato nella sezione precedente.

   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore nel **[!UICONTROL Contenitore di configurazione]** campo .
1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare [!DNL Microsoft® Power Automate Flow Service] configurazione in AEM Forms.
1. Sulla **[!UICONTROL Configurare Dataverse per Microsoft® Power Automate]** , specifica la **[!UICONTROL ID client]** (indicato anche come ID applicazione), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]** e **[!UICONTROL URL ambiente dinamico]**. Utilizza l’ID client, il segreto client, l’URL OAuth e l’ID ambiente di Dynamics. Utilizza l’opzione Endpoint nell’interfaccia utente dell’applicazione Microsoft® Azure Active Directory per trovare l’URL OAuth. Apri [Flussi personali](https://us.flow.microsoft.com) tocca e collega I miei flussi utilizzano l’ID elencato in URL come ID di Dynamics Environment.
1. Tocca **[!UICONTROL Connetti]**. Se richiesto, accedi al tuo account Microsoft® Azure. Tocca **[!UICONTROL Salva]**.

### Pubblicare sia Microsoft® Power Automate Dataverse che Microsoft® Power Automate Flow Service Configurazioni Cloud {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e apri il contenitore di configurazione creato in [Creare la configurazione Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) sezione .
1. Seleziona la `dataverse` configurazione e tocca **[!UICONTROL Pubblica]**.
1. Nella pagina Pubblica , seleziona **[!UICONTROL Tutte le configurazioni]** e toccare **[!UICONTROL Pubblica]**. Pubblicare sia Power Automate Dataverse che Power Automate Flow Service Configurazioni Cloud.

L&#39;istanza as a Cloud Service di Forms è ora connessa con Microsoft® Power Automate. È ora possibile inviare dati di Forms adattivi a un flusso di automazione del consumo.

## Utilizzare l&#39;azione di invio Invoke a Microsoft® Power Automate per inviare i dati a un flusso di automazione di alimentazione {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Dopo [Collega la tua istanza as a Cloud Service Forms con Microsoft® Power Automate](#connect-forms-server-with-power-automate), esegui le seguenti operazioni per configurare il modulo adattivo per inviare i dati acquisiti a un flusso Microsoft® al momento dell’invio del modulo.

1. Accedi all’istanza di authoring, seleziona il modulo adattivo e fai clic su **[!UICONTROL Proprietà]**.
1. Nel contenitore di configurazione, sfoglia e seleziona il contenitore creato nella sezione . [Creare la configurazione Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration), e tocca **[!UICONTROL Salva e chiudi]**.
1. Apri il modulo adattivo per la modifica e passa a **[!UICONTROL Invio]** della sezione delle proprietà del contenitore del modulo adattivo.
1. Nel contenitore delle proprietà, per **[!UICONTROL Inviare azioni]** seleziona la **[!UICONTROL Richiamare un flusso di automazione dell&#39;alimentazione]** opzione . Diventa disponibile un elenco dei flussi di corrente disponibili **[!UICONTROL Flusso automatizzato dell&#39;alimentazione]** opzione . Selezionare il flusso richiesto e inviare i dati di Forms adattivi al momento dell’invio.

![Configurare l’azione Invia](assets/submission.png)

>[!NOTE]
>
> Prima di inviare il modulo adattivo, assicurati che `When an HTTP Request is received` viene aggiunto lo schema JSON al flusso di automazione di Power.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

