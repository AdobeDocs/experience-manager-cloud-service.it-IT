---
title: Creazione e gestione delle revisioni nei moduli
seo-title: Creating and managing reviews in forms
description: La funzione Revisione è un meccanismo che consente a uno o più revisori di commentare una risorsa disponibile in un modulo.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
topic-tags: forms-manager
source-git-commit: 400e9fa0263b3e9bdae10dc80d524b291f99496d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Creazione e gestione di revisioni per le risorse nei moduli{#creating-and-managing-reviews-for-assets-in-forms}

## Recensione {#review}

Una revisione è un meccanismo che consente a uno o più revisori di commentare una risorsa disponibile in un modulo.

## Impostazione di una revisione {#setting-up-a-review}

1. Passare alla scheda Forms e selezionare un modulo.
1. Se il modulo non dispone di una revisione in corso, avviare una revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni. Fai clic sul pulsante Start Review ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) icona.
1. Inserite le seguenti informazioni:

   * Titolo: Obbligatorio, può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura.
   * Descrizione: Facoltativo, descrizione dello scopo/contenuto da rivedere.
   * Termine: Facoltativo, la data in cui termina la revisione. Al termine della scadenza l&#39;attività viene visualizzata come &quot;Scaduto&quot;.
   * Revisori: Un minimo di uno è obbligatorio. Digitando un nome di gruppo o un nome utente vengono elencati tutti i nomi corrispondenti, ad eccezione del gruppo di utenti del servizio. selezionare un nome e fare clic su Aggiungi.

1. Fai clic su Start per avviare una revisione.

>[!NOTE]
>
>* L’amministratore può accedere a qualsiasi gruppo associato agli utenti del modulo.
>* Il gruppo Utenti del servizio non è disponibile per la selezione per la revisione.


### Azioni che si verificano quando viene impostata una revisione {#actions-that-occur-when-a-review-is-set-up}

Questa sezione descrive cosa accade quando viene creata o impostata una revisione.

1. Viene creata e assegnata una nuova attività di revisione al revisore selezionato.
1. A tutti i revisori viene assegnata un&#39;attività di revisione. L’attività viene visualizzata nella relativa sezione Notifiche. Un revisore può fare clic su una notifica oppure passare alla casella in entrata per visualizzare l’attività. Un revisore può fare clic per aprire l&#39;attività di revisione, visualizzare il modulo e iniziare ad aggiungere commenti.

   ![Avviso notifica revisore](assets/review-notification-img.png)

   Avviso notifica revisore

1. La casella dei commenti è disponibile per i revisori del modulo. Altri possono visualizzare i commenti, ma non possono scrivere commenti.

## Gestione di una revisione {#managing-a-review}

>[!NOTE]
>
>È possibile modificare solo le revisioni in corso. Impossibile modificare le revisioni completate.

1. Passare alla scheda Forms e selezionare un modulo.

1. Se una risorsa è in corso di revisione e sei l’iniziatore della revisione, consulta Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni vengono visualizzate le icone. Solo l’iniziatore della revisione può gestire (Aggiorna/Termina) la revisione.

   Fai clic su Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)icona.

   Per gli utenti diversi dall&#39;iniziatore, l&#39;icona Gestisci revisione è disabilitata.

1. Viene visualizzata una schermata con le informazioni seguenti:

   * **Titolo**: Impossibile modificare.

   * **Descrizione**: Disponibile per la modifica.

   * **Termine**: Disponibile per la modifica. È possibile modificare la scadenza in qualsiasi data e ora successive alla data e all’ora correnti.

   * **Nome revisore**: Disponibile per la modifica. È possibile aggiungere o rimuovere revisori. Se un&#39;attività è scaduta, è possibile aggiungere revisori solo dopo aver esteso la scadenza oltre la data corrente.

1. Modificare i campi necessari e fare clic su Fine.

   ![Rivedere lo stato aggiornato in Gestione attività](assets/manage-review-img.png)

   Rivedere lo stato aggiornato in Gestione attività

1. Per terminare la revisione, fare clic su Termina revisione.

### Azioni che si verificano quando una revisione viene modificata {#actions-that-occur-when-a-review-is-modified}

Questa sezione descrive cosa succede in Aggiornamento/Fine revisione:

1. Se la descrizione Revisione viene modificata, viene aggiornata l&#39;attività corrispondente dei revisori e dell&#39;iniziatore.
1. Se la scadenza di revisione viene modificata, l&#39;attività corrispondente per i revisori viene aggiornata con la nuova data.

1. Se un revisore viene rimosso:

   ![Rimozione di un revisore](assets/removeduser.png)

   Rimozione di un revisore

   1. Se incompleta, l&#39;attività assegnata viene terminata.
   1. Il revisore non può più commentare il modulo.

1. Se viene aggiunto un revisore:

   ![Aggiunta di un revisore](assets/addedreviewer.png)

   Aggiunta di un revisore

   1. Viene creata e assegnata un&#39;attività di revisione al revisore appena aggiunto.
   1. Il revisore appena aggiunto può aggiungere commenti sul modulo.

1. Al termine di una revisione:

   1. **Revisori**: Per ogni revisore, l&#39;attività incompleta relativa alla revisione viene terminata. L&#39;attività non viene più visualizzata come &quot;In sospeso&quot; nella sezione Notifiche del revisore.
   1. **Iniziatore**: L&#39;attività assegnata all&#39;iniziatore Revisione è contrassegnata come completata. L&#39;attività viene rimossa dalla sezione Notifica dell&#39;iniziatore della revisione.
   1. **Tutto**: La revisione viene visualizzata nella sezione Recensioni precedenti . Non è possibile aggiungere ulteriori osservazioni.
      ![revisione completa](assets/review-complete-imgg.png)


