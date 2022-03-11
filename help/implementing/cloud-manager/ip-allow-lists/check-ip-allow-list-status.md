---
title: Verifica dello stato dell’Elenco consentiti IP
description: Verifica dello stato dell’Elenco consentiti IP
exl-id: 5ddea04f-3720-4663-90a8-9399019bfcbe
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Verifica dello stato dell’Elenco consentiti IP {#check-allow-list-status}

Per determinare lo stato degli aggiornamenti dell’Elenco consentiti IP, effettua le seguenti operazioni:

1. Fai clic sull’icona di stato per l’Elenco consentiti IP dalla tabella **Ambienti** schermata e seleziona **ELENCHI CONSENTITI IP** pagina.

1. Cloud Manager visualizza uno dei seguenti stati, come indicato nella sezione seguente.

## Stato di un Elenco consentiti IP {#status}

Di seguito sono riportate le definizioni di stato che verranno visualizzate in un Elenco consentiti IP:

* **Applicato**: L’Elenco consentiti IP viene applicato correttamente negli ambienti.  Gli ambienti e il servizio possono essere visualizzati come mostrato nell&#39;immagine seguente.

* **Aggiornamento**: È in corso un aggiornamento dell’Elenco consentiti IP che può includere una o più applicazioni o non applicate. Le opzioni Applica e Annulla applicazione verranno elencate insieme a Non avviato/In corso/Completato o Non riuscito.

* **Non riuscito**: Impossibile applicare o annullare l&#39;applicazione di uno o più processi in un aggiornamento. Verranno elencati tutti i campi Applica e Annulla applicazione insieme a Completato o Non riuscito.
   * Lo stato sarà Non riuscito, anche se l’applicazione o l’annullamento dell’applicazione nell’aggiornamento non riesce.
   * Lo stato rimarrà Non riuscito finché tutti gli errori non verranno cancellati. Per cancellare l’errore, l’utente deve selezionare l’icona di esecuzione di un nuovo tentativo accanto allo stato .
   * L&#39;utente non sarà in grado di aggiornare o eliminare l&#39;Elenco consentiti IP mentre lo stato è Non riuscito.

* **Eliminazione**: Richiesta di eliminazione in corso. Ciò comporta l&#39;annullamento dell&#39;applicazione di tutti i servizi. Ogni applicazione non applicata verrà elencata insieme a Non avviata/In corso/Completata o Non riuscita.
Una volta completata l’operazione di eliminazione, l’Elenco consentiti IP eseguirà le seguenti operazioni:
   * Non viene più visualizzato nella tabella dell’Elenco consentiti IP.
   * Non viene più applicato ad alcun servizio del programma in Cloud Manager.

* **Eliminazione non riuscita**: Impossibile eseguire uno o più processi non applicati in un&#39;operazione di eliminazione. Ogni applicazione non applicata verrà elencata insieme a Completato o Non riuscito.

   * Lo stato verrà Elimina non riuscito, anche se una non applicazione non riesce.
   * Lo stato rimarrà Elimina non riuscito finché tutti gli errori non verranno cancellati. L&#39;utente deve selezionare Elimina dal **...** menu all&#39;estrema destra della riga nella tabella per cancellare qualsiasi errore.
   * L&#39;utente non potrà aggiornare l&#39;Elenco consentiti IP quando lo stato non è riuscito.

## Configurazioni CDN preesistenti per Elenchi consentiti IP {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nel **ELENCO CONSENTITI IP** e **Ambiente** pagina dei dettagli. Il messaggio visualizzato nell’interfaccia utente scompare dopo la migrazione completa da parte del cliente di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente e potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente. Fai riferimento a [Aggiunta di un Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) per ulteriori dettagli.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
