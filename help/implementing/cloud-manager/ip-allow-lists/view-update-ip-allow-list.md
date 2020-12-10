---
title: Visualizzazione e aggiornamento - Elenchi consentiti di  IP in Gestione risorse
description: Visualizzazione e aggiornamento - Elenchi consentiti di  IP in Gestione risorse
translation-type: tm+mt
source-git-commit: 4635cb6360707d12cf512b0ee21f05169a153114
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Visualizzazione e aggiornamento di Elenchi consentiti di  IP {#view-update}

Puoi visualizzare e aggiornare gli Elenchi consentiti di  IP nei seguenti scenari:

* Per visualizzare e aggiornare il menu, è sufficiente visualizzare i dettagli di uno o più Elenchi consentiti di  IP.
* Per modificare uno o più dei seguenti parametri:
   * Intervalli IP nella definizione del nome della regola
   * Nome descrittivo della regola di Elenco consentiti  IP

## Aggiorna Elenco consentiti  IP {#update-ip-allow-lists}


Per poter aggiornare un Elenco consentiti di  IP, è necessario che un utente nel ruolo Proprietario business o Gestione distribuzione abbia eseguito l&#39;accesso.

>[!NOTE]
>Nella procedura guidata Visualizza e aggiorna verranno visualizzati il nome, gli intervalli IP o IP che definiscono la regola. Inoltre, verranno visualizzati gli ambienti e il servizio a cui è applicata la regola.

Per aggiornare un Elenco consentiti di  IP, effettuate le seguenti operazioni:

1. Passare alla pagina **Elenchi consentiti  IP** dalla schermata **Ambienti**.
1. Identificare la riga in cui è elencata la regola del Elenco consentiti  IP che si desidera visualizzare/aggiornare.
1. Selezionare la **...** menu dall&#39;estremità destra della riga.
1. Selezionare l&#39;opzione **Visualizza e aggiorna**.
1. Apportate modifiche al nome o agli IP e confermate l&#39;invio.

## Considerazioni importanti per l&#39;aggiunta, l&#39;aggiornamento o la rimozione di Elenchi consentiti di  IP {#considerations}

* L&#39;aggiunta di un nuovo intervallo IP al Elenco consentiti di  IP lo applicherà automaticamente a tutti i servizi ambientali corrispondenti.
* Se rimuovi un intervallo IP dal Elenco consentiti di  IP, questo verrà automaticamente rimosso da tutti i servizi ambientali corrispondenti.
* Non è possibile eseguire aggiornamenti a un Elenco consentiti di  IP mentre è in corso un aggiornamento precedente e non è stato completato.
* Non è possibile eseguire aggiornamenti a un Elenco consentiti di  IP se sono presenti errori da un aggiornamento precedente. Eventuali errori devono essere cancellati provando a ripetere l&#39;aggiornamento.
Per ulteriori informazioni, fare riferimento alla sezione [Controllo dello stato del Elenco consentiti  IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md).