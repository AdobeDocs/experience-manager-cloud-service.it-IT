---
title: Gestire i token di accesso degli archivi esterni in Cloud Manager
description: Scopri come visualizzare, modificare ed eliminare i token di accesso utilizzati per Bring Your Own Git in AEM Cloud Manager.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: bc9f392c-61f5-4d39-972b-4c6c8f9bab4a
source-git-commit: 19fd6713e083826bd9aa621d86805bcd55a6743a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# Gestire i token di accesso per gli archivi esterni {#manage-access-tokens}

<!-- badge: label="Private beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#manage-access-tokens" -->

Cloud Manager utilizza i token di accesso per gestire archivi ospitati su piattaforme Git esterne. In precedenza, se un token scadeva, era necessario ripetere l’onboarding dell’archivio associato per rimanere operativo.

Ora la funzionalità **Gestisci token di accesso** consente di gestire i token in modo più efficiente. Puoi visualizzare, rinominare o rimuovere i token collegati ai provider Git esterni supportati, inclusi GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Vedi anche [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

<!--
>[!NOTE]
>
>The features described in this article are only available through the private beta program. For more details and to sign up for the private beta, see [Bring Your Own Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket).
-->

## Visualizza token di accesso {#view-access-tokens}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma di cui desideri gestire il token di accesso Git personalizzato.
1. Nel menu laterale, in **Programma**, fare clic su ![Icona struttura cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Archivi**.
1. Fai clic su **Gestisci token di accesso** nell&#39;angolo superiore destro della pagina.

   Il pulsante **Gestisci token di accesso** è visibile solo se il programma utilizza la funzione Bring Your Own Git.

   ![Finestra di dialogo Gestisci token di accesso contenente un token attivo e un token inattivo](/help/implementing/cloud-manager/managing-code/assets/access-tokens-manage.png)

1. Nella finestra di dialogo **Gestisci token di accesso**:
   * Sono elencati tutti i token di accesso.
   * Puoi **modificare** qualsiasi token di accesso.
   * È possibile **eliminare** solo i token di accesso *non attualmente in uso*. Se un token è in uso, il pulsante ![Elimina icona struttura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) è disabilitato.

## Modificare un token di accesso {#edit-access-tokens}

1. Nella finestra di dialogo **Gestisci token di accesso**, a destra del nome di un token, fai clic sull&#39;icona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).
1. Nella finestra di dialogo **Modifica token di accesso**, aggiorna **Nome token**, il valore **Token di accesso** o entrambi.

   ![Finestra di dialogo Modifica token di accesso](/help/implementing/cloud-manager/managing-code/assets/access-tokens-edit.png)

1. Se il **token di accesso** è attualmente in uso, viene visualizzata una notifica che avvisa che tutti gli archivi associati verranno automaticamente riconvalidati dopo l&#39;aggiornamento.

1. Fai clic su **Aggiorna** per salvare le modifiche.

## Eliminare un token di accesso {#delete-access-token}

1. Nella finestra di dialogo **Gestisci token di accesso**, a destra del nome di un token, fai clic sull&#39;icona ![Elimina](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)

   L&#39;icona è disabilitata (![Icona Elimina struttura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)) per i token attualmente in uso.

1. Nella finestra di dialogo **Elimina token di accesso**, fai clic su **Elimina** per rimuovere definitivamente il token.
