---
title: 'Visualizzazione di un aggiornamento e sostituzione di un certificato SSL - Gestione di SSL '
description: Visualizzazione dell'aggiornamento e sostituzione di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: d1301d4414f87b30f5ab732eacbb61c96f102262
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Visualizzazione e aggiornamento e sostituzione di un certificato SSL {#view-update-replace-ssl-certificate}

## Visualizzazione e aggiornamento di un certificato SSL {#view-update}

Quando utilizzare questa opzione nell&#39;interfaccia utente di Cloud Manager:

* Un certificato esistente sta per scadere. L&#39;utente ha rinnovato il certificato con il fornitore del certificato e desidera sostituire quello esistente che sta per scadere. Nota Solo gli utenti con le autorizzazioni appropriate possono effettuare aggiornamenti.
* Utilizzate il menu Visualizza e aggiorna per visualizzare semplicemente i dettagli del certificato SSL.
* In alternativa, potete modificare il nome utilizzato per fare riferimento a un certificato da questa schermata.
   >[!NOTE]
   >Solo gli utenti con le autorizzazioni appropriate possono effettuare aggiornamenti.


## Aggiornamento di un certificato SSL alla scadenza {#update-ssl-certificate}


>[!NOTE]
>Quando un certificato scade, tutti i domini in uso con il certificato scaduto non funzioneranno più. Per aggiornare un certificato scaduto, è necessario seguire i passaggi elencati di seguito. In questo modo il dominio continuerà a funzionare come desiderato. Per poter aggiungere un nuovo certificato, è necessario aggiornare il nome di dominio personalizzato con il nuovo certificato. Per ulteriori informazioni, consulta Visualizza e aggiorna nome dominio personalizzato

Per aggiornare un certificato SSL, effettuate le seguenti operazioni:

>[!NOTE]
>Per aggiornare un certificato SSL in Cloud Manager, un utente deve essere incluso nel ruolo Proprietario business o Gestione distribuzione.

1. Passare alla schermata Certificati SSL dalla pagina **Ambienti**.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL che è stato installato correttamente nel programma.
1. Per accedere alle opzioni di menu per ogni riga, selezionare i tre pulsanti all&#39;estremità destra della riga di interesse. Da qui, seleziona Visualizza e aggiorna. I dettagli del certificato possono essere visualizzati da qui, come illustrato nell&#39;esempio seguente.
1. Per sostituire il certificato, incollate il nuovo contenuto nei campi di input appropriati e salvate. Dovrete risolvere eventuali errori. Fare riferimento alla sezione Errori certificati per risolvere i problemi più comuni.