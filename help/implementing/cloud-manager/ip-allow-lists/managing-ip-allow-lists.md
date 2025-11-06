---
title: Gestire gli elenchi IP consentiti
description: Scopri come visualizzare, modificare, eliminare e controllare lo stato degli Elenchi consentiti IP in Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 19%

---

# Gestire gli elenchi IP consentiti {#manage-ip-allow-lists}

Scopri come visualizzare, modificare, eliminare e controllare lo stato degli Elenchi consentiti IP in Cloud Manager.

## Visualizzare e aggiornare Elenchi consentiti IP {#update-ip-allow-lists}

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può visualizzare e aggiornare un Elenco consentiti IP seguendo la procedura riportata di seguito.

**Per visualizzare e aggiornare gli Elenchi consentiti IP:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Elenco attività](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Elenchi consentiti IP**.
1. Identifica la riga degli Elenchi consentiti IP che desideri visualizzare o aggiornare.
1. Fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) a destra della riga.
1. Dal menu a discesa, fare clic su **Visualizza e aggiorna**.
La finestra di dialogo **Visualizza e aggiorna Elenco consentiti IP** mostra il nome, gli indirizzi IP (o intervalli) che definiscono la regola insieme agli ambienti e ai servizi a cui la regola viene applicata.
1. Modifica il nome o gli indirizzi IP, a seconda delle esigenze.

   L’aggiunta o la rimozione di un nuovo intervallo IP da un Elenco consentiti IP ne determina l’applicazione o la rimozione automatica da tutti gli ambienti/servizi corrispondenti a cui era precedentemente applicato.

   Non è possibile aggiornare un Elenco consentiti IP mentre è in corso un aggiornamento precedente che non è stato completato.

1. Fai clic su **Aggiorna**.

## Controllare lo stato degli Elenchi consentiti IP {#check-allow-list-status}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Elenco attività](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Elenchi consentiti IP**.

1. Nella colonna **Stato** della tabella Elenchi consentiti IP, passa il puntatore del mouse su un Elenco consentiti IP verde (in uso) per visualizzare uno o più servizi applicati.

   I valori di stato mostrati nella tabella hanno i seguenti significati:

   | Stato dell&#39;Elenco consentiti IP | Descrizione |
   | --- | --- |
   | Applicato | L’Elenco consentiti IP è stato applicato correttamente a uno o più ambienti. |
   | Aggiornamento | È in corso l’aggiornamento dell’Elenco consentiti IP, che può includere una o più applicazioni o la rimozione dell’elenco. Ogni applicazione o rimozione viene elencata con il relativo stat: **Non avviato**, **In corso**, **Completato** o **Non riuscito**. |
   | Non riuscito | Uno o più processi di applicazione o rimozione di un aggiornamento non sono riusciti.<br>· Ogni applicazione e rimozione viene elencata insieme al relativo stato.<br>· Lo stato è **Non riuscito** se un&#39;applicazione/rimozione dell&#39;aggiornamento non riesce. Lo stato rimane **Non riuscito** fino alla risoluzione di tutti gli errori.<br>· Fai clic sull&#39;icona **Riprova** accanto allo stato per cancellare l&#39;errore.<br>· Impossibile aggiornare o eliminare un Elenco consentiti IP con stato **Non riuscito**. |
   | Eliminazione | Eliminazione di un Elenco consentiti IP in corso.<br>· L&#39;eliminazione comporta la rimozione dell&#39;elenco da tutti i servizi.<br>· Ogni rimozione viene elencata con il relativo stato **Non avviato**, **In corso**, **Completo** o **Non riuscito**.<br>· Al termine dell&#39;operazione di eliminazione, l&#39;Elenco consentiti IP non viene visualizzato nella tabella dell&#39;Elenco consentiti IP. Inoltre, l’Elenco consentiti IP non viene applicato ad alcun servizio del programma in Cloud Manager. |
   | Eliminazione non riuscita | Una o più rimozioni non sono riuscite durante un&#39;operazione di eliminazione.<br>· Ogni rimozione viene elencata con lo stato **Completo** o **Non riuscito**.<br>· Se una rimozione non riesce, lo stato diventa **Eliminazione non riuscita**. Lo stato rimane **Eliminazione non riuscita** fino alla risoluzione di tutti gli errori. All&#39;estrema destra della riga della tabella, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi fai clic su **Elimina** nel menu a discesa per risolvere l&#39;errore.<br>· Impossibile aggiornare un Elenco consentiti IP con stato **Non riuscito**. |

## Eliminare un Elenco consentiti IP {#delete-allow-list}

Quando elimini un Elenco consentiti IP, questo annulla automaticamente l’applicazione dell’elenco da tutti i servizi e lo elimina dalla tabella dell’Elenco consentiti IP.

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può visualizzare e aggiornare un Elenco consentiti IP seguendo la procedura riportata di seguito.

**Per eliminare un Elenco consentiti IP:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Elenco attività](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Elenchi consentiti IP**.
1. Identifica la riga dell&#39;Elenco consentiti IP che desideri eliminare, quindi fai clic su ![Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) a destra della riga, quindi fai clic su **Elimina**.
1. Nella finestra di dialogo **Elimina Elenco consentiti IP** fare clic su **Elimina**.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi di una configurazione CDN (Content Delivery Network) preesistente per gli Elenchi consentiti IP, viene visualizzato un messaggio informativo sulla pagina **Elenco consentiti IP**. Il messaggio ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio non viene più visualizzato dopo aver eseguito la migrazione di tutte le configurazioni dell’ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Per ulteriori dettagli, consulta [Aggiungere un Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).

Un messaggio simile viene visualizzato anche nelle pagine **Certificati SSL** e **Ambienti** degli ambienti che presentano configurazioni CDN preesistenti per i certificati SSL o nomi di dominio personalizzati.
