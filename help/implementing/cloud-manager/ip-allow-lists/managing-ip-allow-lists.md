---
title: Gestione degli elenchi IP consentiti
description: Scopri come visualizzare, modificare, eliminare e controllare lo stato dei inserisce nell'elenco Consentiti di IP in Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 52%

---

# Gestione degli elenchi IP consentiti {#manage-ip-allow-lists}

Scopri come visualizzare, modificare, eliminare e controllare lo stato dei inserisce nell&#39;elenco Consentiti di IP in Cloud Manager.

## Visualizzazione e aggiornamento degli elenchi IP consentiti {#update-ip-allow-lists}

Un utente in **Proprietario business** o **Responsabile dell’implementazione** Per visualizzare e aggiornare un elenco Consentiti di IP di un, il ruolo può seguire la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.
1. Identificare la riga per i inserisce nell&#39;elenco Consentiti di IP che si desidera visualizzare o aggiornare.
1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.
1. Seleziona l’opzione **Visualizza e aggiorna**.
1. Il **Visualizza e aggiorna** procedura guidata visualizza il nome, gli indirizzi IP (o intervalli) che definiscono la regola insieme agli ambienti e ai servizi a cui la regola viene applicata.
1. Modifica il nome o gli indirizzi IP, a seconda delle esigenze, e conferma quanto inserito.

L’aggiunta o la rimozione di un nuovo intervallo IP da un elenco Consentiti di IP lo applica/annulla automaticamente a tutti gli ambienti/servizi corrispondenti a cui era precedentemente applicato.

Non è possibile aggiornare un elenco Consentiti IP durante un aggiornamento precedente che non è stato completato.

## Controllo dello stato degli elenchi di IP consentiti {#check-allow-list-status}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Stato** per l&#39;IP inserire nell&#39;elenco Consentiti dalla tabella **Ambienti** e seleziona la **ELENCHI CONSENTITI IP** pagina.

1. Cloud Manager visualizza lo stato del inserisco nell&#39;elenco Consentiti di come descritto [nella sezione seguente.](#status)

### Stato di un elenco IP consentiti {#status}

[Durante il controllo dello stato dei elenchi Consentiti IP, è possibile:](#check-allow-list-status) possono avere uno dei seguenti valori.

* **Applicato** - Il inserisco nell&#39;elenco Consentiti di IP è stato applicato correttamente a uno o più ambienti.

* **Aggiornamento** - È in corso un aggiornamento del inserisco nell&#39;elenco Consentiti di IP, che può includere una o più applicazioni o la rimozione dell&#39;elenco.

   * Ogni applicazione o rimozione viene elencata con il relativo stat: **Non avviato**, **In corso**, **Completato** o **Non riuscito**.

* **Non riuscito**: uno o più processi di applicazione o rimozione di un aggiornamento non sono riusciti.
   * Ogni applicazione e rimozione viene elencata insieme al relativo stato.
      * Lo stato **Non riuscito** viene visualizzato nel caso in cui un’applicazione o rimozione dell’aggiornamento risulti non riuscita.
      * Lo stato rimane **Non riuscito** fino alla risoluzione di tutti gli errori.
         * Per poter risolvere l&#39;errore, seleziona l&#39;icona **Riprova** accanto allo stato.
      * Non è possibile aggiornare o eliminare un elenco Consentiti IP con un **Non riuscito** stato.

* **Eliminazione** - È in corso l&#39;eliminazione di un elenco Consentiti IP da parte di un utente con nome di dominio (IP).
   * L’eliminazione comporta la rimozione dell’elenco da tutti i servizi.
   * Ogni rimozione viene elencata con il relativo stato: **Non avviato**, **In corso**, **Completato** o **Non riuscito**.
   * Al termine dell’operazione di eliminazione:
      * Il inserisco nell&#39;elenco Consentiti di IP non viene visualizzato nella tabella di inserisce nell&#39;elenco Consentiti dell’IP.
      * Il inserisco nell&#39;elenco Consentiti di IP non viene applicato ad alcun servizio del programma in Cloud Manager.

* **Eliminazione non riuscita**: durante un’operazione di eliminazione, una o più rimozioni non sono andate a buon fine.

   * Ogni rimozione viene elencata con il relativo stato: **Completato** o **Non riuscito**.
   * Se una rimozione non va a buon fine, lo stato diventa **Eliminazione non riuscita.** 
   * Lo stato rimane **Eliminazione non riuscita** fino alla risoluzione di tutti gli errori.
      * Per risolvere gli errori, seleziona **Elimina** dal menu con i puntini di sospensione all’estrema destra della riga della tabella.
   * Non è possibile aggiornare un elenco Consentiti IP durante il quale è stato impostato il valore **Non riuscito**.

## Eliminazione di un elenco IP consentiti {#delete-allow-list}

Un utente in **Proprietario business** o **Responsabile dell’implementazione** Per visualizzare e aggiornare un elenco Consentiti di IP di un, il ruolo può seguire la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.
1. Identificare la riga dell&#39;elenco Consentiti IP che si desidera eliminare.
1. Seleziona il menu con i puntini di sospensione all’estrema destra della riga.
1. Fai clic su **Elimina**.
1. Conferma quanto inserito.

Se si elimina un elenco Consentiti IP, questo viene rimosso automaticamente da tutti i servizi e viene eliminato dalla tabella.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per i inserisce nell&#39;elenco Consentiti di IP, viene visualizzato un messaggio informativo sulla **ELENCO CONSENTITI IP** pagina. Il messaggio ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio non viene più visualizzato dopo aver eseguito la migrazione di tutte le configurazioni dell’ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Consulta [Aggiunta di un Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) per ulteriori dettagli.

Un messaggio simile viene visualizzato anche nelle pagine **Certificati SSL** e **Ambienti** degli ambienti che presentano configurazioni CDN preesistenti per i certificati SSL o nomi di dominio personalizzati.
