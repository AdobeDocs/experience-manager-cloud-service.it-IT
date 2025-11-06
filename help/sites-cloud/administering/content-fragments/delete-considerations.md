---
title: Frammenti di contenuto - Considerazioni sull’eliminazione
description: Esamina queste considerazioni importanti prima di definire i criteri di eliminazione dei frammenti di contenuto in AEM. I frammenti di contenuto sono uno strumento potente per la distribuzione di contenuti headless e occorre considerare attentamente le implicazioni relative all’eliminazione di tali contenuti.
feature: Content Fragments
role: User, Developer
exl-id: d1726bff-3aa8-4758-bee7-0cacea1f660a
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 46%

---

# Considerazioni sull’eliminazione dei frammenti di contenuto {#delete-considerations-content-fragments}

Esamina queste considerazioni importanti prima di definire i criteri di eliminazione per i frammenti di contenuto in AEM. I frammenti di contenuto sono uno strumento potente per la distribuzione di contenuti headless e occorre considerare attentamente le implicazioni relative all’eliminazione di tali contenuti.

## Autorizzazioni - Elimina o Non Eliminare {#permissions-delete-or-not-delete}

La possibilità di eliminare i contenuti è straordinaria, ma potenzialmente delicata, e in molti settori è necessario limitare e controllare come questi privilegi vengono distribuiti.

In relazione alle autorizzazioni di eliminazione, i frammenti di contenuto devono essere considerati a due livelli:

1. **Il frammento di contenuto come singola entità.**

   * **Caso d&#39;uso**: utente che deve modificare o aggiornare un frammento di contenuto - **ed eliminare un intero frammento**.
   * **Autorizzazioni**: l&#39;autorizzazione Elimina può essere assegnata tramite Gestione utenti e/o gruppi.

2. **Le numerose sottoentità che compongono un frammento di contenuto, ad esempio varianti e sottonodi.**

   Il funzionamento di base dell’editor dei frammenti di contenuto richiede che tali elementi secondari transitori possano essere eliminati. Ad esempio, quando si manipolano le varianti, ma anche durante la modifica dei metadati o la gestione dei contenuti associati.

   * **Caso d&#39;uso**: utente che deve modificare o aggiornare un frammento di contenuto - **senza poter eliminare un intero frammento**.
   * **Autorizzazioni**: vedi [Autorizzazioni necessarie solo per la funzionalità dell’editor](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Consulta anche Come controllare le operazioni di gestione degli utenti in AEM.

## Autorizzazioni necessarie solo per la funzionalità dell’editor {#permissions-required-for-editor-functionality-only}

Agli utenti che devono modificare o aggiornare un frammento di contenuto, **senza consentire loro di eliminare un intero frammento**, devono essere assegnate autorizzazioni specifiche, in quanto il funzionamento di base dell&#39;editor frammento di contenuto richiede l&#39;eliminazione di elementi secondari transitori.

Ad esempio, quando si manipolano le varianti, ma anche durante la modifica dei metadati o la gestione dei contenuti associati.

>[!NOTE]
>
>Le autorizzazioni di eliminazione, necessarie per modificare o aggiornare un frammento di contenuto, sono incluse nell’autorizzazione Elimina assegnata tramite la gestione degli utenti e/o dei gruppi.

Le autorizzazioni necessarie per modificare o aggiornare un frammento devono essere applicate al nodo contenente il frammento di contenuto o a un nodo padre appropriato (a qualsiasi livello in `/content/dam`). Le autorizzazioni assegnate a un nodo principale vengono applicate a tutti i nodi al suo interno.

Ad esempio, una cartella contenente tutti i frammenti di contenuto, come:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>È anche possibile impostare le autorizzazioni su `/content/dam`, in quanto tutti i frammenti di contenuto sono archiviati qui.
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

   * `jcr:addChildNodes`, `jcr:modifyProperties`, e `jcr:removeChildNodes`, `jcr:removeNode`
