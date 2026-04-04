---
title: Flusso di lavoro di invio per l'interfaccia utente associata - IC Genera output PDF
description: Scopri come funzionano l’invio e il flusso di lavoro per l’interfaccia utente Associate e segui un flusso di lavoro di esempio che genera PDF da JSON di comunicazione interattiva (IC).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 9d8a33e4-e206-48e6-9daf-b15feb9c67a3
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---

# Flusso di lavoro di invio per l&#39;interfaccia utente associata

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

Questo articolo spiega come funzionano l’invio e il flusso di lavoro quando abiliti un flusso di lavoro per l’interfaccia utente Associa. Viene quindi illustrato come configurare un flusso di lavoro per l’invio. La procedura dettagliata utilizza come esempio la generazione di un PDF dal payload di Comunicazione interattiva (IC); è possibile adattare i passaggi per altri tipi di flusso di lavoro.

<!--
## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).
-->

## Configurare un flusso di lavoro di invio

I passaggi seguenti mostrano come creare un flusso di lavoro che viene eseguito quando gli utenti inviano dall’interfaccia utente Associa. In questo caso viene utilizzato **il rendering dell&#39;IC in PDF** come esempio, con il passaggio predefinito **Output PDF rendering IC**. Quando un utente invia da Associate UI (Interfaccia utente associata), il payload viene inviato al flusso di lavoro; questo passaggio utilizza **communicationDom** (IC-JSON) dal payload per produrre il PDF.

### Struttura del payload

Il flusso di lavoro riceve un payload JSON. Il campo **communicationDom** contiene il codice IC-JSON utilizzato per la generazione di PDF. Il passaggio **Output PDF rendering IC** lo utilizza come input del modello.

| Campo | Descrizione |
|-------|-------------|
| communicationDom | IC-JSON per la generazione di PDF |
| auditMetadata | Informazioni di controllo |
| submitData | Dati modulo inviati (JSON) |
| prefillData | Dati precompilati (JSON) |
| referer, cookies, queryString, clientIP, userAgent, formSubmitter | Richiedi metadati |

### Creare il modello di flusso di lavoro

1. **Base:** Crea un modello di flusso di lavoro (ad esempio, aggiungi un flusso di lavoro come **pdfrenderworkflow**).

   ![Scheda di base del modello di flusso di lavoro](/help/forms/assets/associate-ui-add-workflow.png)

1. **Variabili:** Aggiungi variabili che corrispondono al payload e al passaggio: **communicationDom** (JSON), **auditMetadata** (JSON), **outputDocument** (Documento).

   ![Variabili flusso di lavoro](/help/forms/assets/associate-ui-add-variables.png)

1. **Passaggio:** Aggiungi il passaggio **Output PDF rendering IC**.
   ![Aggiungi passaggio flusso di lavoro](/help/forms/assets/associate-ui-add-step.png)

1. Nella scheda **Input**, impostare **Seleziona modello (JsonObject)** su **Variabile** → **communicationDom**. Salvate il passo e il modello.

   ![Output PDF rendering IC — scheda Input](/help/forms/assets/associate-ui-input-variable.png)

1. Nella scheda **Output**, impostare **Seleziona modello (JsonObject)** su **Variabile** → **communicationDom**. Salvate il passo e il modello.

   ![Variabili del flusso di lavoro e area di lavoro](/help/forms/assets/assocaite-ui-output-variable.png)

### Collega il flusso di lavoro all&#39;interfaccia utente associata

In [Abilita e configura l&#39;interfaccia utente associata](/help/forms/interactive-communication/enable-configure-associate-ui.md), abilita la visualizzazione associata e in **Flusso di lavoro** imposta **Configura flusso di lavoro per l&#39;aggiornamento** su On e seleziona questo modello di flusso di lavoro. Pubblica l&#39;IC e [integra l&#39;interfaccia utente Associate](/help/forms/interactive-communication/invoke-associate-ui.md) in modo che gli invii attivino questo flusso di lavoro.

![Impostazioni comunicazione interattiva - Configurazione del flusso di lavoro per l&#39;interfaccia utente associata](/help/forms/assets/associate-ui-configure-workflow.png)

Quando **Esternalizza archiviazione dati flusso di lavoro** è abilitato, configurare l&#39;esternalizzatore in modo che i dati del flusso di lavoro vengano archiviati nell&#39;archiviazione esterna (ad esempio, Azure). Vedi [Esternalizzare i dati del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html).

## Consulta anche

- [Associate UI in Interactive Communication Editor](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Abilitare e configurare l’interfaccia utente di Associa per le comunicazioni interattive](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integrare l’interfaccia utente di Associa nell’applicazione](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Esternalizzare i dati del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)
