---
title: Verifica dello stato del Elenco consentiti  IP
description: Verifica dello stato del Elenco consentiti  IP
translation-type: tm+mt
source-git-commit: e6a8d69ea87ac56a51cde2f131c4accff1bea527
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Verifica dello stato del Elenco consentiti  IP {#check-allow-list-status}

Per determinare lo stato degli aggiornamenti al Elenco consentiti di  IP, effettuate le seguenti operazioni:

1. Fare clic sull&#39;icona Stato per il Elenco consentiti di  IP dalla tabella nella schermata **Ambienti** e selezionare la pagina **Elenchi consentiti di  IP**.

1. Cloud Manager visualizzerà uno dei seguenti stati, come indicato nella sezione seguente.

## Stato di un Elenco consentiti di  IP {#status}

Di seguito sono riportate le definizioni di stato che verranno visualizzate in un Elenco consentiti di  IP:

* **Applicato**: L&#39;Elenco consentiti IP  viene applicato correttamente agli ambienti.  Gli ambienti e il servizio sono visualizzati come illustrato nell&#39;immagine seguente.

* **Aggiornamento**: È in corso un aggiornamento al Elenco consentiti di  IP che può includere una o più applicazioni o l&#39;annullamento dell&#39;applicazione. Ogni applicazione e applicazione verrà elencata insieme a Non avviata/In corso/Completata o Non valida.

* **Non riuscito**: Uno o più processi di applicazione o non applicazione in un aggiornamento non sono riusciti. Ogni applicazione e applicazione verrà elencata insieme a Completato o Non valido.
   * Lo stato avrà esito negativo, anche se una applicazione/non applicazione nell&#39;aggiornamento non riesce.
   * Lo stato resterà Non riuscito fino a quando tutti gli errori non verranno cancellati. L&#39;utente deve selezionare l&#39;icona dei tentativi accanto allo stato per cancellare l&#39;errore.
   * L&#39;utente non sarà in grado di aggiornare o eliminare il Elenco consentiti di  IP mentre lo stato non è riuscito.

* **Eliminazione**: Richiesta di eliminazione in corso. Ciò comporta l&#39;annullamento dell&#39;applicazione di tutti i servizi. Ogni applicazione non applicata verrà elencata insieme a Non avviata/In corso/Completata o Non riuscita.
Una volta completata l&#39;operazione di eliminazione, il Elenco consentiti di  IP:
   * Non viene più visualizzato nella tabella del Elenco consentiti di  IP.
   * Non verrà più applicato ad alcun servizio nel programma in Cloud Manager.

* **Eliminazione non riuscita**: Uno o più processi non applicabili in un&#39;operazione di eliminazione non riusciti. Ogni applicazione non applicata verrà elencata insieme a Completato o Non valido.

   * Lo stato sarà Elimina non riuscito, anche se uno non applicato non riesce.
   * Lo stato resterà Elimina non riuscito fino a quando tutti gli errori non verranno cancellati. L&#39;utente deve selezionare Elimina dal **...** menu all&#39;estrema destra della riga nella tabella per cancellare qualsiasi errore.
   * L&#39;utente non sarà autorizzato ad aggiornare  Elenco consentiti IP mentre lo stato non è riuscito.

