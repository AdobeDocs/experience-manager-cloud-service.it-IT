---
title: Invio di una conferma per l’invio di un modulo tramite e-mail
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms consente di configurare l’azione di invio e-mail che invia una conferma a un utente all’invio del modulo.
seo-description: AEM Forms allows you to configure the email Submit Action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Invio di una conferma per l’invio di un modulo tramite e-mail {#sending-a-form-submission-acknowledgement-via-email}

## Invio di dati per modulo adattivo {#adaptive-form-data-submission}

Forms adattivo offre diversi [Invia azioni](configuring-submit-actions.md) flussi di lavoro per l’invio dei dati del modulo a endpoint diversi.

Ad esempio, il **[!UICONTROL Invia e-mail]** Azione di invio invia un’e-mail in caso di invio corretto di un modulo adattivo. Può anche essere configurato per inviare i dati del modulo e il PDF nell’e-mail.

Questo articolo descrive i passaggi per abilitare l’azione E-mail su un modulo adattivo e le diverse configurazioni fornite.

>[!NOTE]
>
>È inoltre possibile utilizzare **[!UICONTROL Invia PDF tramite e-mail]** opzione per inviare il modulo compilato tramite e-mail come allegato PDF. Le opzioni di configurazione disponibili per questa azione sono le stesse disponibili per **[!UICONTROL Invia e-mail]** azione. L’azione E-mail PDF è disponibile solo per Adaptive Forms basato su XFA

## Azione Invia e-mail {#email-action}

L’azione Invia e-mail consente all’autore di inviare automaticamente e-mail a uno o più destinatari in caso di invio corretto di un modulo adattivo.

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, tap **[!UICONTROL Form Container]** and tap ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an end user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### Utilizzo dei nomi dei campi del modulo adattivo per creare in modo dinamico contenuti e-mail {#using-adaptive-form-field-names-to-dynamically-create-email-content}

I nomi dei campi in un modulo adattivo sono denominati segnaposto e vengono sostituiti con il valore del campo dopo che un utente ha inviato il modulo.

In **[!UICONTROL Invia e-mail]** , è possibile utilizzare segnaposto che vengono elaborati durante l&#39;esecuzione dell&#39;azione. Ciò implica che le intestazioni dell’e-mail (come **[!UICONTROL A]**, **[!UICONTROL CC]**, **[!UICONTROL CCN]**, **[!UICONTROL Oggetto]**) vengono generate quando l&#39;utente invia il modulo.

Per definire un segnaposto, specificare `${<field name>}` in un campo dopo aver selezionato **[!UICONTROL Invia e-mail]** come azione di invio.

Ad esempio, se il modulo contiene **[!UICONTROL Indirizzo e-mail]** campo, denominato `email_addr`, per acquisire l’ID e-mail di un utente, puoi specificare quanto segue nel **[!UICONTROL A]**, **[!UICONTROL CC]**, o **[!UICONTROL CCN]** campi.

`${email_addr}`

Quando un utente invia il modulo, viene inviata un’e-mail all’ID e-mail inserito nel `email_addr` del modulo.

>[!NOTE]
>
>È possibile trovare il nome di un campo nel **[!UICONTROL Modifica]** per il campo.

I segnaposto variabili possono essere utilizzati anche nel **[!UICONTROL Oggetto]** e **[!UICONTROL Modello e-mail]** campi.

Esempio:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>I campi nei pannelli ripetibili non possono essere utilizzati come segnaposto per le variabili.

