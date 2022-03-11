---
title: 'Visualizzazione dell’aggiornamento e della sostituzione di un certificato SSL - Gestione di SSL '
description: Visualizzazione dell’aggiornamento e della sostituzione di un certificato SSL - Gestione dei certificati SSL
exl-id: 662494b1-a710-4822-97ef-057043ef89ba
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Visualizzazione e aggiornamento e sostituzione di un certificato SSL  {#view-update-replace-ssl-certificate}

## Visualizzazione e aggiornamento di un certificato SSL {#view-update}

Quando utilizzare queste opzioni nell’interfaccia utente di Cloud Manager:

* Un certificato esistente sta per scadere. L&#39;utente ha rinnovato il certificato con il fornitore del certificato e desidera sostituire quello esistente che sta per scadere. Nota Solo gli utenti con le autorizzazioni appropriate possono effettuare aggiornamenti.
* Utilizza la **Visualizza e aggiorna** per visualizzare semplicemente i dettagli del certificato SSL.
* In alternativa, è possibile modificare il nome utilizzato per fare riferimento a un certificato da questa schermata.
* Solo gli utenti con le autorizzazioni appropriate possono effettuare aggiornamenti.


## Aggiornamento di un certificato SSL in scadenza {#update-ssl-certificate}

Quando un certificato scade, i domini in uso con il certificato scaduto non funzioneranno più. Per aggiornare un certificato scaduto, è necessario seguire i passaggi elencati di seguito. In questo modo il dominio continuerà a funzionare come desiderato. L’aggiunta di un nuovo certificato richiederà l’aggiornamento del nome di dominio personalizzato con il nuovo certificato prima che i domini funzionino come desiderato. Fai riferimento a [Visualizzazione e aggiornamento e sostituzione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md) per ulteriori dettagli.

Per aggiornare un certificato SSL, effettua le seguenti operazioni:

>[!NOTE]
>Per aggiornare un certificato SSL in Cloud Manager, un utente deve essere in ruolo Proprietario business o Gestore distribuzione.

1. Passa alla schermata Certificati SSL dal **Ambienti** pagina.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL installato correttamente nel programma.
1. È possibile accedere alle opzioni del menu per ogni riga selezionando i tre pulsanti all’estremità destra della riga di interesse.
1. Seleziona **Visualizza e aggiorna**. I dettagli del certificato possono essere visualizzati qui.

## Sostituzione di un certificato SSL {#replace-ssl-certificate}

Per sostituire un certificato SSL, effettua le seguenti operazioni:

1. Passa alla schermata Certificati SSL dal **Ambienti** pagina.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL installato correttamente nel programma.
1. È possibile accedere alle opzioni del menu per ogni riga selezionando i tre pulsanti all’estremità destra della riga di interesse.
1. Seleziona **Visualizza e aggiorna**.
1. Per sostituire il certificato, incolla il nuovo contenuto nei campi di input appropriati e fai clic su **Salva**. Dovrai risolvere eventuali errori.

   Fai riferimento a [Errori di certificato](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) per risolvere i problemi più comuni.
