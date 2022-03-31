---
title: Gestione degli Elenchi IP consentiti
description: Scopri come visualizzare, modificare, eliminare e controllare lo stato degli elenchi consentiti IP in Cloud Manager.
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---


# Gestione degli Elenchi IP consentiti {#manage-ip-allow-lists}

Scopri come visualizzare, modificare, eliminare e controllare lo stato degli elenchi consentiti IP in Cloud Manager.

## Visualizzazione e aggiornamento di Elenchi consentiti IP {#update-ip-allow-lists}

Un utente nel **Proprietario business** o **Gestione distribuzione** per visualizzare e aggiornare un elenco consentiti IP, puoi seguire questi passaggi.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.
1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.
1. Passa a **ELENCHI CONSENTITI IP** dalla pagina **Ambienti** schermo.
1. Identifica la riga per gli elenchi consentiti IP che desideri visualizzare o aggiornare.
1. Fai clic sul pulsante con i puntini di sospensione all’estremità destra della riga.
1. Seleziona la **Visualizza e aggiorna** opzione .
1. La **Visualizza e aggiorna** verranno visualizzati il nome, gli indirizzi IP (o intervalli) che definiscono la regola insieme agli ambienti e al servizio a cui viene applicata la regola.
1. Apporta modifiche al nome o agli indirizzi IP e conferma l’invio.

L’aggiunta o la rimozione di un nuovo intervallo IP a un elenco consentiti IP lo applicherà/annullerà automaticamente l’applicazione a tutti gli ambienti/servizi corrispondenti a cui era stato applicato in precedenza.

Impossibile eseguire aggiornamenti a un elenco consentiti IP mentre è in corso un aggiornamento precedente e non è stato completato.

## Controllo dello stato degli Elenchi consentiti IP {#check-allow-list-status}

Segui questi passaggi per controllare lo stato degli elenchi consentiti IP.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Fai clic sul pulsante **Stato** icona per l’elenco consentiti IP dalla tabella **Ambienti** e seleziona la **ELENCHI CONSENTITI IP** pagina.

1. Cloud Manager visualizza lo stato dell’elenco consentiti come descritto [nella sezione seguente.](#status)

### Stato di un Elenco consentiti IP {#status}

[Quando controlli lo stato degli elenchi consentiti IP,](#check-allow-list-status) possono avere uno dei seguenti valori.

* **Applicato** - L&#39;elenco consentiti IP viene applicato correttamente a uno o più ambienti.

* **Aggiornamento** - È in corso un aggiornamento dell’elenco consentiti IP, che può includere una o più applicazioni o l’annullamento dell’applicazione dell’elenco.

   * Ogni applicazione/annullamento dell&#39;applicazione è elencata insieme al proprio stato di **Non avviato**, **In corso**, **Completa** oppure **Non riuscito**.

* **Non riuscito** - Impossibile eseguire uno o più processi di applicazione o di annullamento dell&#39;applicazione di un aggiornamento.
   * Ogni applicazione e applicazione viene elencata insieme al relativo stato.
      * Lo stato è **Non riuscito** se un&#39;applicazione o un&#39;applicazione nell&#39;aggiornamento non riesce.
      * Lo stato rimarrà come **Non riuscito** finché tutti gli errori non vengono cancellati.
         * È necessario selezionare la **Riprova** accanto allo stato per cancellare l’errore.
      * Non è possibile aggiornare o eliminare un elenco consentiti IP con un **Non riuscito** stato.

* **Eliminazione** - È in corso l’eliminazione di un elenco consentiti IP.
   * L’eliminazione comporta l’annullamento dell’applicazione dell’elenco da tutti i servizi.
   * Ogni applicazione non è elencata insieme al proprio stato di **Non avviato**, **In corso**, **Completa** oppure **Non riuscito**.
   * Una volta completata l’operazione di eliminazione, l’elenco consentiti IP eseguirà le seguenti operazioni:
      * Non viene più visualizzato nella tabella dell’elenco consentiti IP.
      * Non viene più applicato ad alcun servizio del programma in Cloud Manager.

* **Eliminazione non riuscita** - Errore di una o più applicazioni durante un&#39;operazione di eliminazione.

   * Ogni applicazione viene elencata insieme allo stato **Completa** o **Non riuscito**.
   * Lo stato sarà **Eliminazione non riuscita** se un&#39;applicazione non riesce.
   * Lo stato rimarrà come **Eliminazione non riuscita** finché tutti gli errori non vengono cancellati.
      * Selezionare **Elimina** dal menu dei puntini di sospensione all’estrema destra della riga nella tabella per cancellare qualsiasi errore.
   * Impossibile aggiornare un elenco consentiti IP mentre lo stato è **Non riuscito**.

## Eliminazione di un elenco IP consentiti {#delete-allow-list}

Un utente nel **Proprietario business** o **Gestione distribuzione** per visualizzare e aggiornare un elenco consentiti IP, puoi seguire questi passaggi.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.
1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.
1. Passa a **ELENCHI CONSENTITI IP** dalla pagina **Ambienti** schermo.
1. Identifica la riga dell’elenco consentiti IP che desideri eliminare.
1. Selezionare il menu dei puntini di sospensione all&#39;estremità destra della riga.
1. Fai clic su **Elimina**.
1. Conferma l’invio.

Se si elimina un elenco consentiti IP, questo viene automaticamente rimosso da tutti i servizi e eliminato dalla tabella.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per i tuoi elenchi consentiti IP, verrà visualizzato un messaggio informativo sul **ELENCO CONSENTITI IP** , incoraggiandoti ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio scompare dopo la migrazione di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

Fare riferimento al documento [Aggiunta di un elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) per ulteriori dettagli.

Un messaggio simile è fornito anche sul **Certificati SSL** e **Ambienti** pagine per ambienti con configurazioni CDN preesistenti per certificati SSL o nomi di dominio personalizzati.
