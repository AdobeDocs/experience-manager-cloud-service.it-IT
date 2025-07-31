---
title: Come integrare un modulo adattivo con Microsoft&reg; Power Automate?
description: Integrare un modulo adattivo con Microsoft&reg; Power Automate.
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
keywords: collegare i moduli AEM per l'automazione dell'alimentazione, l'automazione dell'alimentazione AEM Forms, integrare l'automazione dell'alimentazione in Adaptive Forms, inviare dati da Adaptive Forms a Power Automate
feature: Adaptive Forms, Foundation Components, Core Components, Edge Delivery Services
role: Admin, User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 4%

---


# Collegare un modulo adattivo con Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

<span class="preview"> Se sei su GovCloud e devi connetterti a un tenant GCC (Government Cloud Computing), invia un&#39;e-mail dal tuo indirizzo ufficiale a aem-forms-ea@adobe.com per richiedere l&#39;accesso tramite il programma Early Adopter. </span>

È possibile configurare un modulo adattivo per eseguire un flusso cloud di Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record al flusso cloud Power Automate per l’elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche di business sulla base dei dati acquisiti e automatizzare i flussi di lavoro dei clienti.

L&#39;editor di Forms adattivo fornisce l&#39;azione di invio **Richiama un flusso Microsoft® Power Automate** per inviare i dati dei moduli adattivi, gli allegati e il documento di record al flusso cloud di Power Automate.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/aem-forms-submit-action.md).


## Vantaggi

Di seguito sono riportati alcuni esempi di cosa è possibile fare dopo l’integrazione di un modulo adattivo con Microsoft® Power Automate:

* Utilizzare dati Forms adattivi in processi aziendali Power Automate
* Utilizza Power Automate per inviare i dati acquisiti a più di 500 origini dati o a qualsiasi API disponibile pubblicamente
* Eseguire calcoli complessi sui dati acquisiti
* Salvataggio dei dati Adaptive Forms sui sistemi di storage secondo una pianificazione predefinita

## Prerequisiti

Per collegare un modulo adattivo con Microsoft® Power Automate sono necessari i seguenti elementi:

* Licenza Microsoft® Power Automate Premium.
* Flusso di Microsoft® [Power Automate](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) con trigger `When an HTTP request is received` per accettare i dati di invio del modulo adattivo.
* Un utente Experience Manager con [privilegi di Forms Author](/help/forms/forms-groups-privileges-tasks.md) e [di Forms Admin](/help/forms/forms-groups-privileges-tasks.md)
* L’account utilizzato per connettersi a Microsoft® Power Automate è il proprietario del flusso Power Automate configurato per ricevere i dati dal modulo adattivo

## Collegare l&#39;istanza Forms as a Cloud Service con Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Per collegare l’istanza Forms as a Cloud Service a Microsoft® Power Automate, effettua le seguenti operazioni:

1. [Creazione di un Microsoft](#ms-power-automate-application)
1. [Crea Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Crea Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Pubblica Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Crea applicazione Microsoft® Azure Active Directory {#ms-power-automate-application}

1. Accedi a [portale di Azure](https://portal.azure.com/).
1. Selezionare [!UICONTROL Azure Active Directory] dal menu di navigazione a sinistra.
1. Nella pagina Directory predefinita, seleziona [!UICONTROL Registrazioni app] dal pannello a sinistra.
1. Nella pagina Registrazioni app, fai clic su Nuove registrazioni.
1. Specifica il nome, i tipi di account supportati e l’URI di reindirizzamento nella pagina. Nell’URI di reindirizzamento, specifica quanto segue e fai clic su Salva.
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrare un&#39;applicazione Azure Active Directory](assets/power-automate-application.png)

   >[!NOTE]
   >Se necessario, puoi anche specificare URI di reindirizzamento aggiuntivi dalla pagina Autenticazione.
   > Per i tipi di account supportati, seleziona singolo tenant, più tenant o account Microsoft® personale a seconda del caso d’uso


1. Nella pagina Autenticazione, abilita le opzioni seguenti e fai clic su Salva.


   * Token di accesso (utilizzati per i flussi impliciti)
   * Token ID (utilizzati per flussi impliciti e ibridi)

1. Nella pagina Autorizzazioni API, fare clic su `Add a permission`.

1. In API Microsoft®, selezionare `Power Automate` e selezionare le autorizzazioni seguenti.
   * Flows.Manage.All
   * Flows.Read.All
   * Autorizzazione GCC (opzionale se desideri connetterti a un tenant GCC (Government Cloud Computing))
Fare clic su `Add permissions` per salvare le autorizzazioni.
1. Nella pagina Autorizzazioni API, fare clic su `Add a permission`. Selezionare le API utilizzate dalla mia organizzazione, cercare `DataVerse` e abilitare `user_impersonation` Fare clic su `Add` autorizzazioni.
1. (Facoltativo) Nella pagina Certificati e segreti, fai clic su Nuovo segreto client. Nella schermata Aggiungi segreto client, fornisci una descrizione e un periodo di tempo per la scadenza del segreto, quindi fai clic su Aggiungi. Viene generata una stringa segreta.
1. Tieni presente l&#39;URL dell&#39;ambiente [Dynamics](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests) specifico per la tua organizzazione.

### Crea configurazione cloud Microsoft® Power Automate Dataverse {#microsoft-power-automate-dataverse-cloud-configuration}

1. Nell&#39;istanza Autore AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Nella pagina **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]** e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione per archiviare Cloud Services. Verificare che il nome della cartella non contenga spazio.
1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e apri il contenitore di configurazione creato nel passaggio precedente.


   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore nel campo **[!UICONTROL Contenitore configurazione]**.

1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare la configurazione [!DNL Microsoft® Power Automate Flow Service] in AEM Forms.
1. Nella pagina **[!UICONTROL Configura servizio Dataverse per Microsoft® Power Automate]**, specificare **[!UICONTROL ID client]** (denominato anche ID applicazione), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]** e **[!UICONTROL URL ambiente dinamico]**. Utilizzare l&#39;ID client, il segreto client, l&#39;URL OAuth e l&#39;URL dell&#39;ambiente dinamico dell&#39;[applicazione Microsoft® Azure Active Directory](#ms-power-automate-application) creata nella sezione precedente. Utilizza l’opzione Endpoints nell’interfaccia utente dell’applicazione Microsoft® Azure Active Directory per trovare l’URL OAuth

   ![Utilizza l&#39;opzione Endpoints nell&#39;interfaccia utente dell&#39;applicazione Microsoft Power Automate per trovare l&#39;URL OAuth](assets/endpoints.png)

1. Seleziona **[!UICONTROL Connetti]**. Se richiesto, accedere all&#39;account Microsoft® Azure. Seleziona **[!UICONTROL Salva]**.

### Crea configurazione cloud del servizio Flow di Microsoft® Power Automate {#create-microsoft-power-automate-flow-cloud-configuration}

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Servizio flusso Microsoft® Power Automate]** e apri il contenitore di configurazione creato nella sezione precedente.


   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore nel campo **[!UICONTROL Contenitore configurazione]**.

1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare la configurazione [!DNL Microsoft® Power Automate Flow Service] in AEM Forms.

1. (Facoltativo) Selezionare la casella di controllo `Connect to Microsoft GCC` per connettersi al tenant GCC.

   >[!NOTE]
   >
   > Se desideri connetterti a un tenant GCC (Government Cloud Computing), seleziona l’autorizzazione GCC nel portale di Microsoft Azure.


   ![Configurazione cloud Power Automate](/help/forms/assets/power-automate.png)

1. Nella pagina **[!UICONTROL Configura Dataverse per Microsoft® Power Automate]**, specificare **[!UICONTROL ID client]** (denominato anche ID applicazione), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]** e **[!UICONTROL URL ambiente dinamico]**. Utilizza l’ID client, il segreto client, l’URL OAuth e l’ID ambiente Dynamics. Utilizza l’opzione Endpoints nell’interfaccia utente dell’applicazione Microsoft® Azure Active Directory per trovare l’URL OAuth. Apri il collegamento [Flussi personali](https://us.flow.microsoft.com) e seleziona I miei flussi utilizzano l&#39;ID elencato nell&#39;URL come ID ambiente Dynamics.

1. Seleziona **[!UICONTROL Connetti]**. Se richiesto, accedere all&#39;account Microsoft® Azure. Seleziona **[!UICONTROL Salva]**.

### Pubblicare le configurazioni cloud di Microsoft® Power Automate Dataverse e Microsoft® Power Automate Flow Service {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e apri il contenitore di configurazione creato nella precedente sezione [Crea configurazione cloud Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration).
1. Selezionare la configurazione `dataverse` e selezionare **[!UICONTROL Pubblica]**.
1. Nella pagina Pubblica, seleziona **[!UICONTROL Tutte le configurazioni]** e **[!UICONTROL Pubblica]**. Pubblicare configurazioni cloud Power Automate Dataverse e Power Automate Flow Service.

L&#39;istanza Forms as a Cloud Service è ora collegata a Microsoft® Power Automate. È ora possibile inviare dati Adaptive Forms a un flusso Power Automate.

## Utilizzare l&#39;azione di invio Richiama un flusso Microsoft® Power Automate per inviare i dati a un flusso Power Automate {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Dopo aver [connesso l&#39;istanza di Forms as a Cloud Service con Microsoft® Power Automate](#connect-forms-server-with-power-automate), eseguire l&#39;azione seguente per configurare il modulo adattivo in modo da inviare i dati acquisiti a un flusso Microsoft® all&#39;invio del modulo.

>[!BEGINTABS]

>[!TAB Componente di base]

1. Accedi all&#39;istanza Autore, seleziona il modulo adattivo e fai clic su **[!UICONTROL Proprietà]**.
1. Nel Contenitore configurazione, sfogliare e selezionare il contenitore creato nella sezione [Crea configurazione cloud Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration), quindi selezionare **[!UICONTROL Salva e chiudi]**.
1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Invio]** delle proprietà Contenitore modulo adattivo.
1. Nel contenitore delle proprietà, per **[!UICONTROL Azioni di invio]** selezionare l&#39;opzione **[!UICONTROL Richiama un flusso Power Automate]** e selezionare un flusso **[!UICONTROL Power Automate]**. Seleziona il flusso richiesto e i dati di Adaptive Forms vengono inviati al momento dell’invio.

   ![Configura azione di invio](assets/submission.png)
1. Fai clic su **[!UICONTROL Fine]**.

>[!NOTE]
>
> Prima di inviare il modulo adattivo, accertati che il trigger `When an HTTP Request is received` con lo schema JSON sottostante sia aggiunto al flusso Power Automate.

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

>[!TAB Componente core]

1. Accedi all&#39;istanza Autore, seleziona il modulo adattivo e fai clic su **[!UICONTROL Proprietà]**.
1. Nel Contenitore configurazione, sfogliare e selezionare il contenitore creato nella sezione [Crea configurazione cloud Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration), quindi selezionare **[!UICONTROL Salva e chiudi]**.
1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Selezionare l&#39;opzione **[!UICONTROL Richiama un flusso Power Automate]** dall&#39;elenco a discesa Azione di invio e selezionare un **[!UICONTROL flusso Power Automate]**. Seleziona il flusso richiesto e i dati di Adaptive Forms vengono inviati al momento dell’invio.

   ![Configura azione di invio](/help/forms/assets/power-automate-cc.png)
1. Fai clic su **[!UICONTROL Fine]**.

>[!NOTE]
>
> Prima di inviare il modulo adattivo, accertati che il trigger `When an HTTP Request is received` con lo schema JSON sottostante sia aggiunto al flusso Power Automate.

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

>[!TAB Editor universale]

1. Accedi all’istanza di authoring e seleziona il modulo adattivo.
1. Nel Contenitore configurazione, sfogliare e selezionare il contenitore creato nella sezione [Crea configurazione cloud Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration), quindi selezionare **[!UICONTROL Salva e chiudi]**.
1. Apri il modulo adattivo per la modifica.
1. Fai clic sull&#39;estensione **Modifica proprietà modulo** nell&#39;editor.
Viene visualizzata la finestra di dialogo **Proprietà modulo**.

   >[!NOTE]
   >
   > * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
   > * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).


1. Fai clic sulla scheda **Invio** e seleziona **[!UICONTROL Richiama un flusso Power Automate]**. Invia azione. Seleziona il flusso richiesto e i dati di Adaptive Forms vengono inviati al momento dell’invio.

   ![Configura azione di invio](/help/forms/assets/power-automate-ue.png)
1. Fai clic su **[!UICONTROL Salva&amp;Chiudi]**.

>[!NOTE]
>
> Prima di inviare il modulo adattivo, accertati che il trigger `When an HTTP Request is received` con lo schema JSON sottostante sia aggiunto al flusso Power Automate.

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

>[!ENDTABS]

<!--
## See also

* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
* [Configure a Submit Action](configure-submit-actions-core-components.md)
* [Adobe Experience Manager Connector for Microsoft&reg; Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
* [Connect Adaptive Form to Microsoft&reg; Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)
-->


## Articoli correlati

{{af-submit-action}}

<!--

>[!MORELIKETHIS]
>
>* [Connect Adaptive Form to Microsoft Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)

-->