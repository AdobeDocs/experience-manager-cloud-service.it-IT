---
title: Frammenti di contenuto - Elimina considerazioni
description: Frammenti di contenuto - Elimina considerazioni
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Frammenti di contenuto - Elimina considerazioni{#content-fragments-delete-considerations}

## Autorizzazioni - Elimina o Non Elimina {#permissions-delete-or-not-delete}

La possibilità di eliminare contenuti è potente, ma potenzialmente sensibile, e molti settori devono limitare e controllare la modalità di distribuzione di tali privilegi.

In relazione alle autorizzazioni di eliminazione, i frammenti di contenuto devono essere considerati a due livelli:

1. **Il frammento di contenuto come entità singola.**

   * **Caso** di utilizzo: Utente che deve modificare/aggiornare un frammento di contenuto **ed eliminare un intero frammento**.
   * **Autorizzazioni**: L&#39;autorizzazione Elimina può essere assegnata tramite Gestione utente e/o gruppo.

2. **Più sottoentità che costituiscono un frammento di contenuto; ad esempio, varianti, nodi secondari.**

   Il funzionamento di base dell’editor dei frammenti di contenuto richiede che tali sottoelementi transitori possano essere eliminati. Ad esempio, durante la manipolazione delle variazioni; anche durante la modifica dei metadati o la gestione del contenuto associato.

   * **Caso** di utilizzo: Un utente che deve modificare/aggiornare un frammento di contenuto, **senza la possibilità di eliminare un intero frammento**.
   * **Autorizzazioni**: Consultate Autorizzazioni necessarie solo per la funzionalità Editor. <!-- See [Permissions Required for Editor Functionality Only](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only). -->

>[!NOTE]
>
>Se un utente non dispone di autorizzazioni Elimina, l&#39;editor frammenti di contenuto funziona in modalità di sola ** lettura.

>[!NOTE]
>
>Consultate anche Controllo delle operazioni di gestione utenti in AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Autorizzazioni necessarie solo per la funzionalità Editor {#permissions-required-for-editor-functionality-only}

Per gli utenti che necessitano di modificare/aggiornare un frammento di contenuto, **senza consentire loro di eliminare un intero frammento**, è necessario assegnare autorizzazioni specifiche, in quanto il funzionamento di base dell&#39;editor dei frammenti di contenuto richiede l&#39;eliminazione di sottoelementi transitori.

Ad esempio, durante la manipolazione delle variazioni; anche durante la modifica dei metadati o la gestione del contenuto associato.

>[!NOTE]
>
>Le autorizzazioni di eliminazione, necessarie per modificare/aggiornare un frammento di contenuto, sono incluse nell&#39;autorizzazione di eliminazione assegnata tramite Gestione utente e/o gruppo. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

Le autorizzazioni necessarie per modificare/aggiornare un frammento devono essere applicate al nodo contenente il frammento di contenuto o a un nodo principale appropriato (a qualsiasi livello in `/content/dam`). Se assegnate a tale nodo padre, le autorizzazioni verranno applicate a tutti i nodi all&#39;interno di tale ramo.

Ad esempio, una cartella contenente tutti i frammenti di contenuto, come:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>È `/content/dam` inoltre possibile impostare le autorizzazioni in quanto tutti i frammenti di contenuto sono memorizzati in questa cartella.
>
>Tuttavia, questa azione applica le stesse autorizzazioni di eliminazione anche a *tutti* gli altri tipi di risorse.

I prerequisiti per consentire a un utente e/o gruppo specifico di modificare/aggiornare un frammento di contenuto sono:

>[!NOTE]
>
>Questo elenco mostra tutti i privilegi richiesti, non solo quelli di eliminazione.

* Per i nodi o le cartelle dei frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Per il `jcr:content`nodo di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`

* Per tutti i nodi sotto `jcr:content` di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
