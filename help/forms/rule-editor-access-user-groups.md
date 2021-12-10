---
title: Come concedere l'accesso all'Editor regole a Seleziona gruppi di utenti?
description: Ci sono diversi tipi di utenti con competenze diverse che funzionano con Adaptive Forms. Scopri come limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---


# Concedere l’accesso all’editor di regole a specifici gruppi di utenti {#grant-rule-editor-access-to-select-user-groups}

## Panoramica {#overview}

Ci sono diversi tipi di utenti con competenze diverse che funzionano con Adaptive Forms. Anche se gli utenti esperti possono avere le conoscenze necessarie per lavorare con script e regole complesse, potrebbero esserci utenti di livello base che devono lavorare solo con il layout e le proprietà di base di Adaptive Forms.

[!DNL Experience Manager Forms] consente di limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione. Nelle impostazioni del servizio di configurazione di Forms adattivo, puoi specificare il [gruppi di utenti](forms-groups-privileges-tasks.md) che può visualizzare e accedere all’editor di regole.

## Specificare i gruppi di utenti che possono accedere all&#39;editor di regole {#specify-user-groups-that-can-access-rule-editor}

1. Accedi a [!DNL Experience Manager Forms] come amministratore.
1. Nell’istanza di authoring, fai clic su ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![martello](assets/hammer-icon.svg) > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**. La console Web viene visualizzata in una nuova finestra.

   ![1-2](assets/1-2.png)

1. In [!UICONTROL Console web] Finestra, individuare e fare clic **[!UICONTROL Servizio di configurazione dei moduli adattivi]**. **[!UICONTROL Servizio di configurazione dei moduli adattivi]** viene visualizzata la finestra di dialogo . Non modificare alcun valore e fai clic su **[!UICONTROL Salva]**.

   Crea un file `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` in CRX-repository.

1. Accedi a CRXDE come amministratore. Apri file `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` per la modifica.
1. Utilizzare la seguente proprietà per specificare il nome di un gruppo che può accedere all&#39;editor di regole (ad esempio, RuleEditorsUserGroup) e fare clic su **[!UICONTROL Salva tutto]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Per abilitare l&#39;accesso per più gruppi, specifica un elenco di valori separati da virgola:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crea utente](assets/create_user_new.png)

   Ora, quando un utente che non fa parte del gruppo di utenti specificato (qui    `RuleEditorsUserGroup`) tocca un campo e l’icona Modifica regola ( ![edit-rules1](assets/edit-rules1.png)) non è disponibile nella barra degli strumenti Componenti :

   ![componentstoolbarwith](assets/componentstoolbarwithre.png)

   Barra degli strumenti Componenti visibile a un utente con accesso all’editor di regole:

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra degli strumenti dei componenti visibile per un utente senza accesso all’editor di regole

   Per istruzioni su come aggiungere utenti ai gruppi, consulta [Amministrazione degli utenti e sicurezza](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

