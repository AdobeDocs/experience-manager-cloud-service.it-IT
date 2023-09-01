---
title: Frammenti di contenuto - Considerazioni sull’eliminazione
description: Esamina queste considerazioni importanti prima di definire i criteri di eliminazione dei frammenti di contenuto in AEM. I frammenti di contenuto sono uno strumento potente per la distribuzione di contenuti headless e occorre considerare attentamente le implicazioni relative all’eliminazione di tali contenuti.
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: f6698dd8-3e2a-44ac-b00f-df578aa85ffe
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 100%

---

# Frammenti di contenuto - Considerazioni sull’eliminazione {#content-fragments-delete-considerations}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

Esamina queste considerazioni importanti prima di definire i criteri di eliminazione dei frammenti di contenuto in AEM. I frammenti di contenuto sono uno strumento potente per la distribuzione di contenuti headless e occorre considerare attentamente le implicazioni relative all’eliminazione di tali contenuti.

## Autorizzazioni - Elimina o Non Eliminare {#permissions-delete-or-not-delete}

La possibilità di eliminare i contenuti è straordinaria, ma potenzialmente delicata, e in molti settori è necessario limitare e controllare come questi privilegi vengono distribuiti.

In relazione alle autorizzazioni di eliminazione, i frammenti di contenuto devono essere considerati a due livelli:

1. **Il frammento di contenuto come singola entità.**

   * **Caso d’uso**: utente che deve modificare o aggiornare un frammento di contenuto **ed eliminare un intero frammento**.
   * **Autorizzazioni**: l’autorizzazione Elimina può essere assegnata tramite la gestione degli utenti e/o dei gruppi. <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **Le numerose sottoentità che compongono un frammento di contenuto, come varianti e sotto-nodi.**

   Il funzionamento di base dell’editor di frammenti di contenuto prevede che tali elementi secondari transitori possano essere eliminati. Ad esempio, quando si manipolano le varianti, ma anche durante la modifica dei metadati o la gestione dei contenuti associati.

   * **Caso d’uso**: utente che deve modificare o aggiornare un frammento di contenuto **senza la possibilità di eliminare un intero frammento**.
   * **Autorizzazioni**: vedi [Autorizzazioni necessarie solo per la funzionalità dell’editor](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Se un utente non dispone di autorizzazioni Elimina, l’editor di frammenti di contenuto funziona in modalità di *sola lettura*. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>Vedi anche Come controllare le operazioni di gestione degli utenti in AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Autorizzazioni necessarie solo per la funzionalità dell’editor {#permissions-required-for-editor-functionality-only}

Dovrai assegnare autorizzazioni specifiche agli utenti che necessitano di modificare/aggiornare un frammento di contenuto, **ma a cui non vuoi consentire di eliminare un intero frammento**, poiché il funzionamento di base dell’Editor frammento di contenuto richiede l’eliminazione di elementi secondari transitori.

Ad esempio, quando si manipolano le varianti, ma anche durante la modifica dei metadati o la gestione dei contenuti associati.

>[!NOTE]
>
>Le autorizzazioni di eliminazione, necessarie per modificare o aggiornare un frammento di contenuto, sono incluse nell’autorizzazione Elimina assegnata tramite la gestione degli utenti e/o dei gruppi. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

Le autorizzazioni necessarie per modificare o aggiornare un frammento devono essere applicate al nodo contenente il frammento di contenuto o a un nodo principale appropriato (a qualsiasi livello in `/content/dam`). Le autorizzazioni assegnate a un nodo principale vengono applicate a tutti i nodi al suo interno.

Ad esempio, una cartella contenente tutti i frammenti di contenuto, come:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>È anche possibile impostare le autorizzazioni su `/content/dam`, in quanto tutti i frammenti di contenuto sono memorizzati qui.
>
>Tuttavia, questa azione applica le stesse autorizzazioni di eliminazione anche a *tutti* gli altri tipi di risorse.

I prerequisiti di autorizzazione per consentire a un utente e/o gruppo specifico di modificare/aggiornare un frammento di contenuto sono:

>[!NOTE]
>
>Questo elenco mostra tutti i privilegi richiesti, non solo quelli di eliminazione.

* Per i nodi o le cartelle dei frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Per il `jcr:content` nodo di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`

* Per tutti i nodi sottostanti `jcr:content` di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
