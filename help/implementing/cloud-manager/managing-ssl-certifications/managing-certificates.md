---
title: Gestione dei certificati SSL
description: Scopri come controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli con Cloud Manager.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 7143ea8d36e26aa1674608ff7bd8ba22e2030b3c
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 73%

---


# Gestione dei certificati SSL {#managing-ssl-certificates}

Scopri come controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli con Cloud Manager.

## Controllo dello stato dei certificati SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere visualizzato dalla pagina del certificato SSL.

* **Verde**: indica che il certificato è valido per almeno 14 giorni dalla data corrente.

* **Arancione**: indica che la scadenza del certificato è tra meno di 14 giorni.
   * In questo momento è necessario verificare di disporre di un piano per il rinnovo del certificato e sostituirlo tramite l’interfaccia utente di Cloud Manager, per evitare possibili accessi o interruzioni del sito.
   * Cloud Manager invia notifiche regolari nell’interfaccia utente per avvisarti della scadenza imminente del certificato.

* **Rosso**: indica che la scadenza del certificato SSL è trascorsa.

## Aggiornamento di un certificato SSL {#update-ssl-certificate}

Quando un certificato scade, i domini in uso con il certificato scaduto smetteranno di funzionare. Aggiornare i certificati seguendo la procedura riportata di seguito garantisce che il dominio continui a funzionare come desiderato.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata
1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** , selezionare il programma.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla schermata **Certificati SSL**.
1. Puoi visualizzare una tabella con una riga per ogni certificato SSL installato correttamente nel programma. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga del certificato che desideri aggiornare e seleziona **Visualizza e aggiorna**.
1. Vengono visualizzati i dettagli del certificato, che possono essere aggiornati.
1. Esegui la pipeline per distribuire il certificato aggiornato.

>[!NOTE]
>
>Per aggiornare un certificato SSL in Cloud Manager, l’utente deve avere il ruolo **Proprietario business** o **Responsabile della distribuzione**.

## Sostituzione di un certificato SSL {#replace-ssl-certificate}

È possibile sostituire un certificato SSL seguendo gli stessi passaggi descritti nella sezione [Aggiornamento di un certificato SSL.](#update-ssl-certificate)

## Eliminazione di un certificato SSL {#deleting-an-ssl-certificate}

La rimozione dei certificati da Cloud Manager è un’azione permanente che non può essere annullata. Come best practice, Adobe consiglia di salvare localmente i file SSL prima di eliminarli in Cloud Manager.

Cloud Manager non consente di eliminare un certificato SSL associato a uno o più domini. Prima dell’eliminazione del certificato SSL è necessario eliminare tutti i domini associati. Per ulteriori informazioni, consulta [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

Per eliminare un certificato SSL, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla schermata **Certificati SSL**.
1. Puoi visualizzare una tabella con una riga per ogni certificato SSL installato correttamente nel programma. Fai clic sui puntini di sospensione all’estrema destra della riga del certificato che desideri eliminare e seleziona. **Elimina**.
1. Conferma l’eliminazione nella finestra di dialogo **Elimina certificato SSL**.
1. Esegui la pipeline per annullare la distribuzione del certificato eliminato.

>[!NOTE]
>
>Per eliminare un certificato SSL in Cloud Manager, l’utente deve avere il ruolo **Proprietario business** o **Responsabile della distribuzione**.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per il certificato SSL, viene visualizzato un messaggio informativo sulla **Certificati SSL** , per invitarti ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio non viene più visualizzato dopo aver eseguito la migrazione di tutte le configurazioni dell’ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Consulta [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) per ulteriori dettagli.

Un messaggio simile viene visualizzato anche nelle pagine **Elenco IP consentiti** e **Ambienti** degli ambienti che presentano configurazioni CDN preesistenti per gli elenchi IP consentiti o i nomi di dominio personalizzati.
