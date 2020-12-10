---
title: 'Visualizzazione di un aggiornamento e sostituzione di un certificato SSL - Gestione di SSL '
description: Visualizzazione dell'aggiornamento e sostituzione di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: d5a119921a06ea06cbf2b95353083aa987869629
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Visualizzazione e aggiornamento e sostituzione di un certificato SSL {#view-update-replace-ssl-certificate}

## Visualizzazione e aggiornamento di un certificato SSL {#view-update}

Quando utilizzare queste opzioni nell&#39;interfaccia utente di Cloud Manager:

* Un certificato esistente sta per scadere. L&#39;utente ha rinnovato il certificato con il fornitore del certificato e desidera sostituire quello esistente che sta per scadere. Nota Solo gli utenti con le autorizzazioni appropriate possono effettuare aggiornamenti.
* Utilizzate il menu **Visualizza e aggiorna** per visualizzare semplicemente i dettagli del certificato SSL.
* In alternativa, potete modificare il nome utilizzato per fare riferimento a un certificato da questa schermata.
* Solo gli utenti con le autorizzazioni appropriate possono effettuare aggiornamenti.


## Aggiornamento di un certificato SSL alla scadenza {#update-ssl-certificate}

Quando un certificato scade, tutti i domini in uso con il certificato scaduto non funzioneranno più. Per aggiornare un certificato scaduto, è necessario seguire i passaggi elencati di seguito. In questo modo il dominio continuerà a funzionare come desiderato. Per poter aggiungere un nuovo certificato, è necessario aggiornare il nome di dominio personalizzato con il nuovo certificato. Per ulteriori informazioni, fare riferimento a [Visualizzazione e aggiornamento e sostituzione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

Per aggiornare un certificato SSL, effettuate le seguenti operazioni:

>[!NOTE]
>Per aggiornare un certificato SSL in Cloud Manager, un utente deve essere incluso nel ruolo Proprietario business o Gestione distribuzione.

1. Passare alla schermata Certificati SSL dalla pagina **Ambienti**.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL che è stato installato correttamente nel programma.
1. Per accedere alle opzioni di menu per ogni riga, selezionare i tre pulsanti all&#39;estremità destra della riga di interesse.
1. Selezionare **Visualizza e aggiorna**. I dettagli del certificato possono essere visualizzati da qui.

## Sostituzione di un certificato SSL {#replace-ssl-certificate}

Per sostituire un certificato SSL, effettuate le seguenti operazioni:

1. Passare alla schermata Certificati SSL dalla pagina **Ambienti**.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL che è stato installato correttamente nel programma.
1. Per accedere alle opzioni di menu per ogni riga, selezionare i tre pulsanti all&#39;estremità destra della riga di interesse.
1. Selezionare **Visualizza e aggiorna**.
1. Per sostituire il certificato, incollate il nuovo contenuto nei campi di input appropriati e fate clic su **Salva**. Dovrete risolvere eventuali errori.

   Fare riferimento a [Errori certificati](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) per risolvere i problemi più comuni.