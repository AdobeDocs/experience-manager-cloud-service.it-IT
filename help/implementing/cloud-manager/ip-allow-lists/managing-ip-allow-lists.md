---
title: Gestione degli elenchi IP consentiti
description: Scopri come visualizzare, modificare, eliminare e controllare lo stato degli elenchi IP consentiti in Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: 5311ba7f001201fc94c73fa52bc7033716c1ba78
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 57%

---

# Gestione degli elenchi IP consentiti {#manage-ip-allow-lists}

Scopri come visualizzare, modificare, eliminare e controllare lo stato degli elenchi IP consentiti in Cloud Manager.

## Visualizzazione e aggiornamento degli elenchi IP consentiti {#update-ip-allow-lists}

L’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può visualizzare e aggiornare l’elenco IP consentiti seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.
1. Individua la riga degli elenchi IP consentiti che desideri visualizzare o aggiornare.
1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.
1. Seleziona l’opzione **Visualizza e aggiorna**.
1. Il **Visualizza e aggiorna** procedura guidata visualizza il nome, gli indirizzi IP (o intervalli) che definiscono la regola insieme agli ambienti e al servizio a cui la regola viene applicata.
1. Modifica il nome o gli indirizzi IP, a seconda delle esigenze, e conferma quanto inserito.

L’aggiunta o la rimozione di un nuovo intervallo IP dall’elenco IP consentiti comporta l’applicazione o la rimozione automatica di tutti gli ambienti/servizi corrispondenti ai quali era precedentemente applicato.

Non è possibile aggiornare un elenco consentiti IP mentre è in corso un aggiornamento precedente che non è stato completato.

## Controllo dello stato degli elenchi IP consentiti {#check-allow-list-status}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla tabella riportata nella schermata **Ambienti**, fai clic sull’icona **Stato** dell’elenco IP consentiti, quindi seleziona la pagina **Elenchi IP consentiti**.

1. Cloud Manager mostra lo stato dell’elenco consentiti come descritto [nella sezione seguente.](#status)

### Stato di un elenco IP consentiti {#status}

[Il controllo dello stato degli elenchi IP consentiti](#check-allow-list-status) può riportare uno dei seguenti valori.

* **Applicato**: l’elenco IP consentiti è stato applicato correttamente a uno o più ambienti.

* **Aggiornamento** - È in corso l’aggiornamento dell’elenco consentiti IP, che può includere una o più applicazioni o la rimozione dell’elenco.

   * Ogni applicazione/rimozione viene elencata con il relativo stato tra **Non avviato**, **In corso**, **Completo** o **Non riuscito**.

* **Non riuscito** - Uno o più processi di applicazione o rimozione di un aggiornamento non sono riusciti.
   * Ogni applicazione e rimozione viene elencata insieme al relativo stato.
      * Lo stato **Non riuscito** viene visualizzato nel caso in cui un’applicazione/rimozione dell’aggiornamento risulti non riuscita.
      * Lo stato rimane come **Non riuscito** fino alla risoluzione di tutti gli errori.
         * Seleziona la **Riprova** accanto allo stato, in modo da poter risolvere l’errore.
      * Non è possibile aggiornare o eliminare un elenco consentiti IP con **Non riuscito** stato.

* **Eliminazione in corso**: è in corso l’eliminazione di un elenco IP consentiti.
   * L’eliminazione comporta la rimozione dell’elenco da tutti i servizi.
   * Ogni rimozione viene elencata con il relativo stato di **Non avviato**, **In corso**, **Completa**, o **Non riuscito**.
   * Una volta completata l’operazione di eliminazione, l’elenco IP consentiti:
      * Non viene più visualizzato nella tabella dell’elenco IP consentiti.
      * Non viene più applicato ad alcun servizio del programma in Cloud Manager.

* **Eliminazione non riuscita** - Una o più rimozioni non sono riuscite durante un&#39;operazione di eliminazione.

   * Ogni rimozione viene elencata con il relativo stato **Completa** o **Non riuscito**.
   * Lo stato diventa **Eliminazione non riuscita** se una rimozione non riesce.
   * Lo stato rimane come **Eliminazione non riuscita** fino alla risoluzione di tutti gli errori.
      * Seleziona **Elimina** dal menu con i puntini di sospensione all’estrema destra della riga della tabella, in modo da poter eliminare eventuali errori.
   * Impossibile aggiornare un elenco consentiti IP con lo stato **Non riuscito**.

## Eliminazione di un elenco IP consentiti {#delete-allow-list}

L’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può visualizzare e aggiornare l’elenco IP consentiti seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.
1. Individua la riga dell’elenco IP consentiti che desideri eliminare.
1. Seleziona il menu con i puntini di sospensione all’estrema destra della riga.
1. Fai clic su **Elimina**.
1. Conferma quanto inserito.

L’eliminazione di un elenco consentiti IP ne determina la rimozione automatica da tutti i servizi e l’eliminazione dalla tabella.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per gli elenchi consentiti IP, viene visualizzato un messaggio informativo sulla **ELENCO CONSENTITI IP** pagina. Il messaggio ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio non viene più visualizzato dopo aver eseguito la migrazione di tutte le configurazioni dell’ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Consulta [Aggiunta di un elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) per ulteriori dettagli.

Un messaggio simile viene visualizzato anche nelle pagine **Certificati SSL** e **Ambienti** degli ambienti che presentano configurazioni CDN preesistenti per i certificati SSL o i nomi di dominio personalizzati.
