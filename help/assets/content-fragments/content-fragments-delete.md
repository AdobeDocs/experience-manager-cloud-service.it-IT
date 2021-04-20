---
title: Frammenti di contenuto - Considerazioni sull’eliminazione
description: Esamina queste considerazioni importanti prima di definire i criteri di eliminazione dei frammenti di contenuto in AEM. I frammenti di contenuto sono uno strumento potente per la distribuzione di contenuti headless e occorre considerare attentamente le implicazioni relative all’eliminazione di tali contenuti.
feature: Content Fragments
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 10%

---


# Frammenti di contenuto - Considerazioni sull’eliminazione {#content-fragments-delete-considerations}

Esamina queste considerazioni importanti prima di definire i criteri di eliminazione dei frammenti di contenuto in AEM. I frammenti di contenuto sono uno strumento potente per la distribuzione di contenuti headless e occorre considerare attentamente le implicazioni relative all’eliminazione di tali contenuti.

## Autorizzazioni - Elimina o non elimina {#permissions-delete-or-not-delete}

La possibilità di eliminare i contenuti è potente, ma potenzialmente sensibile, e molti settori devono limitare e controllare come questi privilegi vengono distribuiti.

In relazione alle autorizzazioni di eliminazione, i frammenti di contenuto devono essere considerati a due livelli:

1. **Il frammento di contenuto come singola entità.**

   * **Caso** di utilizzo: Utente che deve modificare/aggiornare un frammento di contenuto  **ed eliminare un intero frammento**.
   * **Autorizzazioni**: L’autorizzazione Elimina può essere assegnata tramite Gestione utenti e/o gruppi.  <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **Le più sottoentità che compongono un frammento di contenuto; ad esempio, varianti, sotto-nodi.**

   Il funzionamento di base dell’editor dei frammenti di contenuto richiede che tali elementi secondari transitori possano essere eliminati. Ad esempio, quando si manipolano le variazioni; anche durante la modifica dei metadati o la gestione dei contenuti associati.

   * **Caso** di utilizzo: Utente che deve modificare/aggiornare un frammento di contenuto  **senza poter eliminare un intero frammento**.
   * **Autorizzazioni**: Consulta  [Autorizzazioni necessarie solo per la funzionalità dell’editor](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Se un utente non dispone di autorizzazioni Elimina, l’editor Frammento di contenuto funziona in modalità *sola lettura* . <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>Vedere anche Come controllare le operazioni di gestione degli utenti in AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Autorizzazioni necessarie solo per la funzionalità dell&#39;editor {#permissions-required-for-editor-functionality-only}

Dovrai assegnare autorizzazioni specifiche agli utenti che necessitano di modificare/aggiornare un frammento di contenuto, **ma a cui non vuoi consentire di eliminare un intero frammento**, poiché il funzionamento di base dell’Editor frammento di contenuto richiede l’eliminazione di elementi secondari transitori.

Ad esempio, quando si manipolano le variazioni; anche durante la modifica dei metadati o la gestione dei contenuti associati.

>[!NOTE]
>
>Le autorizzazioni di eliminazione, necessarie per modificare/aggiornare un frammento di contenuto, sono incluse nell’autorizzazione Elimina assegnata tramite Gestione utente e/o gruppo. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

Le autorizzazioni necessarie per modificare/aggiornare un frammento devono essere applicate al nodo contenente il frammento di contenuto o a un nodo principale appropriato (a qualsiasi livello in `/content/dam`). Quando vengono assegnate a tale nodo padre, le autorizzazioni vengono applicate a tutti i nodi all&#39;interno di tale ramo.

Ad esempio, una cartella contenente tutti i frammenti di contenuto, ad esempio:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>È inoltre possibile impostare le autorizzazioni su `/content/dam`, in quanto tutti i frammenti di contenuto sono memorizzati qui.
>
>Tuttavia, questa azione applica le stesse autorizzazioni di eliminazione anche ad *tutti* altri tipi di risorse.

I prerequisiti per le autorizzazioni per consentire a un utente e/o gruppo specifico di modificare/aggiornare un frammento di contenuto sono:

>[!NOTE]
>
>Questo elenco mostra tutti i privilegi richiesti, non solo quelli di eliminazione.

* Per i nodi o le cartelle dei frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Per il nodo `jcr:content`di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` e  `jcr:removeChildNodes`

* Per tutti i nodi sotto `jcr:content` di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` e  `jcr:removeChildNodes`,  `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
