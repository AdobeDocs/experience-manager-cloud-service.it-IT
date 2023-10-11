---
title: Come fornire l’accesso all’editor di regole per moduli adattivi di AEM per selezionare i gruppi di utenti?
description: Esistono diversi tipi di utenti con diverse competenze che lavorano con Adaptive Forms. Scopri come limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---


# Concedere l’accesso all’editor di regole a specifici gruppi di utenti {#grant-rule-editor-access-to-select-user-groups}

## Panoramica {#overview}

Esistono diversi tipi di utenti con diverse competenze che lavorano con Adaptive Forms. Anche se gli utenti esperti possono avere le giuste conoscenze per lavorare con script e regole complesse, ci possono essere utenti di livello base che devono lavorare solo con il layout e le proprietà di base di Adaptive Forms.

[!DNL Experience Manager Forms] consente di limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione. Nelle impostazioni del servizio di configurazione di Adaptive Forms puoi specificare [gruppi di utenti](forms-groups-privileges-tasks.md) che possono visualizzare e accedere all’editor di regole.

## Specificare i gruppi di utenti che possono accedere all’editor di regole {#specify-user-groups-that-can-access-rule-editor}

1. Accedi a [!DNL Experience Manager Forms] come amministratore.
1. Nell’istanza di authoring, fai clic su ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![martello](assets/hammer-icon.svg) > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**. La console Web si apre in una nuova finestra.

   ![1-2](assets/1-2.png)

1. In entrata [!UICONTROL Console web] Finestra, individua e fai clic su **[!UICONTROL Servizio configurazione modulo adattivo]**. **[!UICONTROL Servizio configurazione modulo adattivo]** viene visualizzata. Non modificare alcun valore e fai clic su **[!UICONTROL Salva]**.

   Crea un file `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` in CRX-repository.

1. Accedi a CRXDE come amministratore. Apri file `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` per la modifica.
1. Utilizzare la proprietà seguente per specificare il nome di un gruppo che può accedere all&#39;editor di regole (ad esempio, RuleEditorsUserGroup) e fare clic su **[!UICONTROL Salva tutto]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Per abilitare l’accesso per più gruppi, specifica un elenco di valori separati da virgola:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crea utente](assets/create_user_new.png)

   Ora, quando un utente che non fa parte del gruppo di utenti specificato (qui    `RuleEditorsUserGroup`) tocca un campo, l’icona Modifica regola ( ![edit-rules1](assets/edit-rules1.png)) non è disponibile nella barra degli strumenti Componenti:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra degli strumenti Componenti visibile a un utente con accesso all’editor di regole:

   ![componentstoolbarwithout outre](assets/componentstoolbarwithoutre.png)

   Barra degli strumenti Componenti visibile a un utente senza accesso all’editor di regole

   Per istruzioni sull’aggiunta di utenti ai gruppi, consulta [Amministrazione utenti e sicurezza](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=it).

