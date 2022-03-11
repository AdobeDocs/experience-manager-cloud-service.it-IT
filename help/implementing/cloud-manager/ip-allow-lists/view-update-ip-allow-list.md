---
title: Visualizzazione e aggiornamento - Elenchi consentiti IP in Cloud Manager
description: Visualizzazione e aggiornamento - Elenchi consentiti IP in Cloud Manager
exl-id: 9f9aebcd-b6d0-497a-b262-0a24b4938b45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---

# Visualizzazione e aggiornamento di un elenco IP consentiti {#view-update}

Puoi visualizzare e aggiornare gli Elenchi consentiti IP nei seguenti scenari:

* Per visualizzare e aggiornare il menu, è sufficiente visualizzare i dettagli di uno o più Elenchi consentiti IP.
* Per modificare uno o più dei seguenti elementi:
   * Intervalli IP nella definizione del nome della regola
   * Nome descrittivo della regola dell’Elenco consentiti IP

## Aggiorna Elenco consentiti IP {#update-ip-allow-lists}


Per poter aggiornare un Elenco consentiti IP, è necessario che un utente con il ruolo Proprietario business o Gestore distribuzione sia connesso.

>[!NOTE]
>La procedura guidata Visualizza e aggiorna visualizzerà il nome, gli intervalli IP o IP che definiscono la regola. Inoltre, visualizzerà gli ambienti e il servizio in cui viene applicata la regola.

Per aggiornare un Elenco consentiti IP, effettua le seguenti operazioni:

1. Passa a **ELENCHI CONSENTITI IP** dalla pagina **Ambienti** schermo.
1. Identifica la riga in cui è elencata la regola dell’Elenco consentiti IP che desideri visualizzare/aggiornare.
1. Seleziona la **...** dall&#39;estremità destra della riga.
1. Seleziona la **Visualizza e aggiorna** opzione .
1. Apporta modifiche al nome o agli IP e conferma l’invio.

## Considerazioni importanti sull’aggiunta, l’aggiornamento o la rimozione di Elenchi consentiti IP {#considerations}

* Aggiungendo un nuovo intervallo IP all&#39;Elenco consentiti IP, questo verrà automaticamente applicato a tutti i servizi ambientali corrispondenti.
* Se si rimuove un intervallo IP dall’Elenco consentiti IP, questo verrà automaticamente rimosso da tutti i servizi relativi all’ambiente.
* Impossibile eseguire aggiornamenti a un Elenco consentiti IP mentre è in corso un aggiornamento precedente e non è stato completato.
* Gli aggiornamenti non possono essere effettuati a un Elenco consentiti IP se sono presenti errori da un aggiornamento precedente. Gli eventuali errori devono essere cancellati tentando di ritentare l&#39;aggiornamento.
Fai riferimento a [Verifica dello stato dell’Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md) per saperne di più.
