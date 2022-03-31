---
title: Gestione dei certificati SSL
description: Scopri come utilizzare Cloud Manager per controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# Gestione dei certificati SSL {#managing-ssl-certificates}

Scopri come utilizzare Cloud Manager per controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli.

## Controllo dello stato dei certificati SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere compreso immediatamente dalla pagina del certificato SSL.

* **Verde** - Questo stato indica che il certificato è valido per almeno 60 giorni dalla data corrente.

* **Arancio** - Questo stato indica che il certificato scade dopo meno di 60 giorni.
   * È ora di verificare di avere un piano per rinnovare il certificato e sostituirlo tramite l’interfaccia utente di Cloud Manager al fine di evitare possibili accessi o interruzioni del sito.
   * Cloud Manager invia notifiche regolari nell’interfaccia utente per avvisarti della scadenza imminente del certificato.

* **Rosso** - Questo stato indica che il certificato SSL è scaduto.

## Aggiornamento di un certificato SSL {#update-ssl-certificate}

Quando un certificato scade, i domini in uso con il certificato scaduto non funzioneranno più. L’aggiornamento dei certificati tramite i passaggi seguenti assicura che il dominio continui a funzionare come desiderato.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.
1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.
1. Passa a **Certificati SSL** dalla schermata **Ambienti** schermo.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL installato correttamente nel programma. Fai clic sul pulsante dei puntini di sospensione all&#39;estrema destra nella riga del certificato che desideri aggiornare e seleziona **Visualizza e aggiorna**.
1. I dettagli del certificato vengono visualizzati e possono essere aggiornati.

>[!NOTE]
>
>Un utente deve essere membro del **Proprietario business** o **Gestione distribuzione** per aggiornare un certificato SSL in Cloud Manager.

## Sostituzione di un certificato SSL {#replace-ssl-certificate}

È possibile sostituire un certificato SSL seguendo gli stessi passaggi descritti nella sezione . [Aggiornamento di un certificato SSL.](#update-ssl-certificate)

## Eliminazione di un certificato SSL {#deleting-an-ssl-certificate}

La rimozione dei certificati da Cloud Manager è un’azione permanente che non può essere annullata. Come best practice, Adobe consiglia di salvare localmente i file SSL prima di eliminarli in Cloud Manager.

Cloud Manager non ti consente di eliminare un certificato SSL associato a uno o più domini. Tutti i domini associati devono essere eliminati prima di eliminare il certificato SSL. Fare riferimento al documento [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) per saperne di più.

Per eliminare un certificato SSL, effettua le seguenti operazioni.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.
1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.
1. Passa a **Certificati SSL** dalla schermata **Ambienti** schermo.
1. Verrà visualizzata una tabella con una riga per ogni certificato SSL installato correttamente nel programma. Fai clic sul pulsante dei puntini di sospensione all’estrema destra nella riga del certificato da eliminare e seleziona **Elimina**.
1. Conferma l’eliminazione in **Elimina certificato SSL** finestra di dialogo.

>[!NOTE]
>
>Un utente deve essere membro del **Proprietario business** o **Gestione distribuzione** per eliminare un certificato SSL in Cloud Manager.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per il certificato SSL, verrà visualizzato un messaggio informativo sul **Certificati SSL** , incoraggiandoti ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio scompare dopo la migrazione di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

Fare riferimento al documento [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) per ulteriori dettagli.

Un messaggio simile è fornito anche sul **ELENCO CONSENTITI IP** e **Ambienti** pagine per ambienti con configurazioni CDN preesistenti per elenchi consentiti IP o nomi di dominio personalizzati.
