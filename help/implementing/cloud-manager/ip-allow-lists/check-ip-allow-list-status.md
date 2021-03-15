---
title: Verifica dello stato dell’Elenco consentiti IP
description: Verifica dello stato dell’Elenco consentiti IP
translation-type: tm+mt
source-git-commit: ddee11fdfa8cadfcd63472fd3c94cd8af555c856
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Verifica dello stato dell&#39;Elenco consentiti IP {#check-allow-list-status}

Per determinare lo stato degli aggiornamenti dell’Elenco consentiti IP, effettua le seguenti operazioni:

1. Fai clic sull&#39;icona di stato per l&#39;Elenco consentiti IP dalla tabella nella schermata **Ambienti** e seleziona **Elenchi consentiti IP** .

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
   * Lo stato rimarrà Elimina non riuscito finché tutti gli errori non verranno cancellati. L&#39;utente deve selezionare Elimina da **...Menu** all&#39;estrema destra della riga nella tabella per cancellare qualsiasi errore.
   * L&#39;utente non potrà aggiornare l&#39;Elenco consentiti IP quando lo stato non è riuscito.

## Configurazioni CDN preesistenti per Inserire nell&#39;elenco Consentiti IP {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nella pagina dei dettagli **Elenco consentiti IP** e **Ambiente** .

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente, come illustrato nella figura riportata di seguito.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)

