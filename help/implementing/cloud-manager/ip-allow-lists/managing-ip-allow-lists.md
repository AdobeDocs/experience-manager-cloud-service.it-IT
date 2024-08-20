---
title: Gestione degli elenchi IP consentiti
description: Scopri come visualizzare, modificare, eliminare e controllare lo stato degli Elenchi consentiti IP in Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 44%

---

# Gestione degli elenchi IP consentiti {#manage-ip-allow-lists}

Scopri come visualizzare, modificare, eliminare e controllare lo stato degli Elenchi consentiti IP in Cloud Manager.

## Visualizzare e aggiornare Elenchi consentiti IP {#update-ip-allow-lists}

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può visualizzare e aggiornare un Elenco consentiti IP seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.
1. Identifica la riga degli Elenchi consentiti IP che desideri visualizzare o aggiornare.
1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.
1. Seleziona l’opzione **Visualizza e aggiorna**.
1. La procedura guidata **Visualizza e aggiorna** visualizza il nome, gli indirizzi IP (o intervalli) che definiscono la regola insieme agli ambienti e ai servizi a cui la regola viene applicata.
1. Modifica il nome o gli indirizzi IP, a seconda delle esigenze, e conferma quanto inserito.

L’aggiunta o la rimozione di un nuovo intervallo IP da un Elenco consentiti IP ne determina l’applicazione o la rimozione automatica da tutti gli ambienti/servizi corrispondenti a cui era precedentemente applicato.

Non è possibile aggiornare un Elenco consentiti IP mentre è in corso un aggiornamento precedente che non è stato completato.

## Controllare lo stato degli Elenchi consentiti IP {#check-allow-list-status}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla tabella della schermata **Ambienti**, fai clic sull&#39;icona **Stato** dell&#39;Elenco consentiti IP, quindi seleziona la pagina **Elenchi consentiti IP**.

1. Cloud Manager visualizza lo stato dell&#39;Elenco consentiti come descritto [nella seguente sezione](#status).

### Stato di un elenco IP consentiti {#status}

[Il controllo dello stato degli Elenchi consentiti IP](#check-allow-list-status) può avere uno dei valori seguenti.

* **Applicato** - Elenco consentiti IP applicato correttamente a uno o più ambienti.

* **Aggiornamento in corso** - È in corso l&#39;aggiornamento dell&#39;Elenco consentiti IP, che può includere una o più applicazioni o la rimozione dell&#39;elenco.

   * Ogni applicazione o rimozione viene elencata con il relativo stat: **Non avviato**, **In corso**, **Completato** o **Non riuscito**.

* **Non riuscito**: uno o più processi di applicazione o rimozione di un aggiornamento non sono riusciti.
   * Ogni applicazione e rimozione viene elencata insieme al relativo stato.
      * Lo stato **Non riuscito** viene visualizzato nel caso in cui un’applicazione o rimozione dell’aggiornamento risulti non riuscita.
      * Lo stato rimane **Non riuscito** fino alla risoluzione di tutti gli errori.
         * Per poter risolvere l&#39;errore, seleziona l&#39;icona **Riprova** accanto allo stato.
      * Impossibile aggiornare o eliminare un Elenco consentiti IP con stato **Non riuscito**.

* **Eliminazione in corso** - È in corso l&#39;eliminazione di un Elenco consentiti IP.
   * L’eliminazione comporta la rimozione dell’elenco da tutti i servizi.
   * Ogni rimozione viene elencata con il relativo stato: **Non avviato**, **In corso**, **Completato** o **Non riuscito**.
   * Al termine dell’operazione di eliminazione:
      * L&#39;Elenco consentiti IP non viene visualizzato nella tabella Elenco consentiti IP.
      * L’Elenco consentiti IP non viene applicato ad alcun servizio del programma in Cloud Manager.

* **Eliminazione non riuscita**: durante un’operazione di eliminazione, una o più rimozioni non sono andate a buon fine.

   * Ogni rimozione viene elencata con il relativo stato: **Completato** o **Non riuscito**.
   * Se una rimozione non va a buon fine, lo stato diventa **Eliminazione non riuscita.** 
   * Lo stato rimane **Eliminazione non riuscita** fino alla risoluzione di tutti gli errori. All&#39;estrema destra della riga della tabella, fai clic sul menu con i puntini di sospensione, quindi fai clic su **Elimina** per cancellare eventuali errori.
   * Impossibile aggiornare un Elenco consentiti IP con stato **Non riuscito**.

## Eliminare un Elenco consentiti IP {#delete-allow-list}

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può visualizzare e aggiornare un Elenco consentiti IP seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.
1. Identifica la riga dell’Elenco consentiti IP da eliminare.
1. Seleziona il menu con i puntini di sospensione all’estrema destra della riga.
1. Fai clic su **Elimina**.
1. Conferma quanto inserito.

L’eliminazione di un Elenco consentiti IP ne determina la rimozione automatica da tutti i servizi e l’eliminazione dalla tabella.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN (Content Delivery Network) preesistente per gli Elenchi consentiti IP, viene visualizzato un messaggio informativo sulla pagina **Elenco consentiti IP**. Il messaggio ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio non viene più visualizzato dopo aver eseguito la migrazione di tutte le configurazioni dell’ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Per ulteriori dettagli, consulta [Aggiungere un Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).

Un messaggio simile viene visualizzato anche nelle pagine **Certificati SSL** e **Ambienti** degli ambienti che presentano configurazioni CDN preesistenti per i certificati SSL o nomi di dominio personalizzati.
