---
title: Creazione e gestione delle revisioni nei moduli
seo-title: Creating and managing reviews in forms
description: Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti su una risorsa disponibile in un modulo.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
topic-tags: forms-manager
source-git-commit: 659484f80d1f31794512af5e4d190b04a9f3e4e8
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Creazione e gestione delle revisioni delle risorse nei moduli{#creating-and-managing-reviews-for-assets-in-forms}

## Recensione {#review}

Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti su una risorsa disponibile in un modulo.

## Impostazione di una revisione {#setting-up-a-review}

1. Passa alla scheda Forms e seleziona un modulo.
1. Se per il modulo non è in corso una revisione, viene avviata una revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni. Fai clic sull’icona Start Review (Avvia revisione) ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) icona.
1. Inserite le seguenti informazioni:

   * Titolo: obbligatorio, può contenere caratteri alfanumerici, trattini o trattini bassi.
   * Descrizione: facoltativo, descrizione dello scopo/contenuto da rivedere.
   * Scadenza: facoltativo, la data in cui termina la revisione. Se la scadenza è stata superata, l’attività viene visualizzata come &quot;Scaduto&quot;.
   * Revisori: almeno uno è obbligatorio. Digitando un nome di gruppo o un nome utente vengono elencati tutti i nomi corrispondenti ad eccezione del gruppo utenti del servizio. selezionare un nome e fare clic su Aggiungi.

1. Per avviare una revisione, fai clic su Avvia.

>[!NOTE]
>
>* L’amministratore può accedere a tutti i gruppi associati agli utenti del modulo.
>* Il gruppo Utenti del servizio non è disponibile per la selezione per la revisione.


### Azioni che si verificano quando viene impostata una revisione {#actions-that-occur-when-a-review-is-set-up}

Questa sezione descrive cosa accade quando si crea o si configura una revisione.

1. Viene creata una nuova attività di revisione assegnata al revisore selezionato.
1. A tutti i revisori viene assegnata un&#39;attività di revisione. L’attività viene visualizzata nella sezione Notifiche. Un revisore può fare clic su una notifica o passare alla casella in entrata per visualizzare l&#39;attività. Un revisore può fare clic per aprire l&#39;attività di revisione, visualizzare il modulo e iniziare ad aggiungere commenti.

   ![Avviso di notifica revisore](assets/review-notification-img.png)

   Avviso di notifica revisore

1. La casella dei commenti è disponibile per i revisori del modulo. Altri possono visualizzare i commenti, ma non possono scriverli.

## Gestione di una revisione {#managing-a-review}

>[!NOTE]
>
>È possibile modificare solo le revisioni in corso. Le recensioni completate non possono essere modificate.

1. Passa alla scheda Forms e seleziona un modulo.

1. Se per una risorsa è in corso una revisione e l’utente è l’iniziatore della revisione, viene visualizzata l’opzione Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni. Solo l&#39;iniziatore di revisione può gestire (aggiornare/terminare) la revisione.

   Fai clic sul pulsante Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)icona.

   Per gli utenti diversi dall&#39;iniziatore, l&#39;icona Gestisci revisione è disabilitata.

1. Viene visualizzata una schermata con le seguenti informazioni:

   * **Titolo**: impossibile modificarlo.

   * **Descrizione**: disponibile per la modifica.

   * **Scadenza**: disponibile per la modifica. È possibile modificare la scadenza in qualsiasi data e ora oltre la data e l&#39;ora correnti.

   * **Nome revisore**: disponibile per la modifica. È possibile aggiungere o rimuovere revisori. Se un&#39;attività è scaduta, è possibile aggiungere revisori solo dopo aver esteso la scadenza oltre la data corrente.

1. Modificare i campi necessari e quindi fare clic su Fine.

   ![Verifica stato aggiornato in Gestione attività](assets/manage-review-img.png)

   Verifica stato aggiornato in Gestione attività

1. Per terminare la revisione, fare clic su Termina revisione.

### Azioni che si verificano quando viene modificata una revisione {#actions-that-occur-when-a-review-is-modified}

Questa sezione descrive cosa accade in Review Update/End (Aggiornamento/Fine revisione):

1. Se la descrizione Revisione viene modificata, l&#39;attività corrispondente dei revisori e dell&#39;iniziatore viene aggiornata.
1. Se la scadenza della revisione viene modificata, l&#39;attività corrispondente per i revisori viene aggiornata con la nuova data.

1. Se un revisore viene rimosso:

   ![Rimozione di un revisore](assets/removeduser.png)

   Rimozione di un revisore

   1. Se incompleta, l&#39;attività assegnata viene terminata.
   1. Il revisore non può più aggiungere commenti al modulo.

1. Se viene aggiunto un revisore:

   ![Aggiunta di un revisore](assets/addedreviewer.png)

   Aggiunta di un revisore

   1. Viene creata un&#39;attività di revisione assegnata al revisore appena aggiunto.
   1. Il revisore appena aggiunto può aggiungere commenti sul modulo.

1. Al termine di una revisione:

   1. **Revisori**: per ogni revisore, l’attività incompleta correlata alla revisione viene terminata. L’attività non viene più visualizzata come &quot;In sospeso&quot; nella sezione Notifiche del revisore.
   1. **Iniziatore**: l&#39;attività assegnata all&#39;iniziatore di revisione è contrassegnata come completata. L&#39;attività viene rimossa dalla sezione Notifica dell&#39;iniziatore di revisione.
   1. **Tutti**: la revisione viene visualizzata nella sezione Revisioni precedenti. Non è possibile aggiungere altri commenti.
      ![revisione completata](assets/review-complete-imgg.png)


