---
title: Gestione dei certificati SSL
description: Scopri come controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli con Cloud Manager.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 70f99cfb2cd00278d9ebbb7972ef455af7a87a1b
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 17%

---


# Gestire i certificati SSL {#managing-ssl-certificates}

Scopri come utilizzare Cloud Manager per verificare lo stato e come eliminare i certificati SSL gestiti dal cliente e gestiti dall’Adobe. Per i certificati gestiti dal cliente, è inoltre possibile modificarli e aggiornarli (sostituirli).

## Controllare lo stato dei certificati SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere visualizzato dalla pagina **Certificati SSL**.

| Stato del certificato SSL | Descrizione |
| --- | --- |
| Verde | Il certificato è valido per almeno 14 giorni dalla data corrente. |
| Arancione | La scadenza del certificato è tra meno di 14 giorni.<br>· Assicurarsi di disporre di un piano per rinnovare il certificato e sostituirlo tramite l&#39;interfaccia utente di Cloud Manager per evitare possibili accessi o interruzioni del sito.<br>· Cloud Manager invia notifiche regolari nell&#39;interfaccia utente per avvisarti della scadenza imminente del certificato. |
| Rosso | Il certificato SSL è scaduto.<br>Consulta [Aggiornare un certificato SSL gestito dal cliente scaduto](#update-ssl-certificate) o [Eliminare un certificato SSL](#deleting-an-ssl-certificate). |

## Aggiornare un certificato SSL gestito dal cliente scaduto {#update-ssl-certificate}

Quando un certificato gestito dal cliente scade, i domini in uso con il certificato scaduto non funzionano più. L’aggiornamento dei certificati garantisce che il dominio continui a funzionare come desiderato.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per aggiornare un certificato SSL gestito dal cliente scaduto:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Dalla pagina **Panoramica**, passa alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, passa alla schermata **Certificati SSL**.
1. Nella riga del certificato gestito del cliente scaduto che desideri aggiornare, fai clic sul pulsante con i puntini di sospensione all&#39;estrema destra, quindi seleziona **Visualizza e aggiorna**.

   ![Aggiorna una certificazione SSL gestita dal cliente scaduta](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. Nella finestra di dialogo **Visualizza e aggiorna certificato SSL** eseguire le operazioni seguenti:

   * (Facoltativo) Nel campo **Nome certificato** digitare un nuovo nome.
   * Nel campo **Certificato**, incolla la nuova chiave del contenuto del certificato.
   * Nel campo **Chiave privata**, aggiorna questo campo solo se hai apportato modifiche al certificato.
   * Nel campo **Catena di certificati** (o catena di attendibilità), incollare la catena di certificati.

1. Fai clic su **Aggiorna** per salvare le modifiche e farle applicare automaticamente.

## Sostituire un certificato SSL gestito dal cliente scaduto {#replace-ssl-certificate}

Segui gli stessi passaggi descritti in [Aggiornare un certificato SSL scaduto](#update-ssl-certificate) per sostituire un certificato SSL scaduto gestito dal cliente.

## Eliminare un certificato SSL {#deleting-an-ssl-certificate}

L’eliminazione di Adobi di certificati SSL gestiti o gestiti dal cliente da Cloud Manager è un’azione permanente che non può essere annullata. Come best practice, Adobe consiglia di salvare i file SSL localmente prima di eliminarli in Cloud Manager.

>[!NOTE]
>
>Non puoi eliminare un certificato SSL gestito di Adobe a cui sono associati uno o più domini attivi. Prima di eliminare il certificato SSL è necessario eliminare tutti i domini attivi associati. Per ulteriori informazioni, consulta [Gestire i nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per eliminare un certificato SSL:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, passa alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, passa alla schermata **Certificati SSL**.
1. Nella riga del certificato che desideri eliminare, fai clic sul pulsante con i puntini di sospensione all&#39;estrema destra, quindi seleziona **Elimina**.
Se il pulsante Elimina contiene un&#39;icona di informazioni come nell&#39;immagine seguente, vedere la nota precedente.

   ![Pulsante Elimina con icona Informazioni](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. Nella finestra di dialogo **Elimina certificato SSL**, fai clic su **Elimina** per confermare l&#39;eliminazione.
1. Esegui la pipeline per annullare la distribuzione del certificato eliminato.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi già di una configurazione CDN per il certificato SSL, nella pagina **Certificati SSL** viene visualizzato un messaggio informativo. Ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e gestibili in Cloud Manager.

Il messaggio scompare dopo che tutte le configurazioni dell’ambiente preesistenti sono state migrate utilizzando l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Per ulteriori dettagli, vedere [Aggiungere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

Un messaggio simile viene visualizzato anche nelle pagine **Elenco IP consentiti** e **Ambienti** degli ambienti che presentano configurazioni CDN preesistenti per gli elenchi IP consentiti o i nomi di dominio personalizzati.
