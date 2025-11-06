---
title: Gestire i certificati SSL
description: Scopri come controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli con Cloud Manager.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 13%

---


# Gestire i certificati SSL {#managing-ssl-certificates}

Scopri come controllare lo stato dei certificati SSL e come modificarli, sostituirli, aggiornarli ed eliminarli con Cloud Manager.

## Controllare lo stato dei certificati SSL {#checking-status-an-ssl-certificate}

Cloud Manager offre una panoramica dello stato di tutti i certificati del programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.
1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.

La pagina **Certificati SSL** fornisce lo stato dei certificati SSL.

| Stato del certificato SSL | Descrizione |
| --- | --- |
| Verde | Il certificato è valido per almeno 14 giorni dalla data corrente. |
| Arancione | La scadenza del certificato è tra meno di 14 giorni.<br>· Assicurarsi di disporre di un piano per rinnovare il certificato e sostituirlo tramite l&#39;interfaccia utente di Cloud Manager per evitare possibili accessi o interruzioni del sito.<br>· Cloud Manager invia notifiche regolari nell&#39;interfaccia utente per avvisarti della scadenza imminente del certificato. |
| Rosso | Il certificato SSL è scaduto.<br>Consulta [Aggiornare un certificato SSL gestito dal cliente scaduto](#update-ssl-certificate) o [Eliminare un certificato SSL](#deleting-an-ssl-certificate). |

## Aggiornare un certificato SSL gestito dal cliente scaduto {#update-ssl-certificate}

Quando un certificato gestito dal cliente scade, i domini in uso con il certificato scaduto non funzionano più. L’aggiornamento dei certificati garantisce che il dominio continui a funzionare come desiderato.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

>[!IMPORTANT]
>
>Quando aggiungi o aggiorni un certificato SSL, non includere il nuovo certificato nella catena di certificati. L’inclusione di impedisce il completamento del caricamento.

**Per aggiornare un certificato SSL gestito dal cliente scaduto:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.
1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.
1. Nella riga del certificato gestito del cliente scaduto che desideri aggiornare, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) all&#39;estrema destra, quindi fai clic su **Visualizza e aggiorna**.

   ![Aggiorna una certificazione SSL gestita dal cliente scaduta](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. Nella finestra di dialogo **Visualizza e aggiorna certificato SSL** eseguire le operazioni seguenti:

   * (Facoltativo) Nel campo **Nome certificato** digitare un nuovo nome.
   * Nel campo **Certificato**, incolla la nuova chiave del contenuto del certificato.
   * Nel campo **Chiave privata**, aggiorna questo campo solo se hai apportato modifiche al certificato.
   * Nel campo **Catena di certificati** (o catena di attendibilità), incollare la catena di certificati.

1. Fai clic su **Aggiorna** per salvare le modifiche e farle applicare automaticamente.


>[!NOTE]
>
>Se due o più certificati SAN coprono la stessa voce di dominio SAN e uno di essi viene aggiornato, il sistema installa il certificato aggiornato per il dominio.
>
>Per ulteriori informazioni, vedere [Risoluzione dei problemi relativi ai certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert).

## Sostituire un certificato SSL gestito dal cliente scaduto {#replace-ssl-certificate}

Segui gli stessi passaggi descritti in [Aggiornare un certificato SSL scaduto](#update-ssl-certificate) per sostituire un certificato SSL scaduto gestito dal cliente.

## Rinominare un certificato SSL gestito di Adobe (#rename-an-ssl-certificate)

Di seguito sono riportati alcuni motivi per cui potrebbe essere utile rinominare un certificato SSL:

* **Organizzazione migliorata**: la ridenominazione del certificato può aiutare a chiarirne lo scopo, ad esempio a identificare l&#39;ambiente (ad esempio gestione temporanea, produzione) o il dominio a cui è destinato.
* **Evitare confusione**: se gestisci più certificati, un nome chiaro e descrittivo può aiutare a evitare errori, ad esempio l&#39;applicazione del certificato errato al dominio errato.
* **Conformità e controllo**: i certificati con nomi corretti possono essere più facili da tracciare a scopo di sicurezza e controllo.

**Per rinominare un certificato SSL gestito di Adobe:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.

1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.

1. Nella pagina **Certificati SSL**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga il cui **certificato SSL gestito da Adobe** desideri rinominare.

1. Scegliere **Rinomina** dal menu a discesa.

1. Nella finestra di dialogo **Rinomina certificato DV** immettere il nuovo nome del certificato nel campo di testo **Nome certificato**.

1. Fai clic su **Rinomina**.


## Eliminare un certificato SSL {#deleting-an-ssl-certificate}

L’eliminazione di certificati SSL gestiti da Adobe o dal cliente da Cloud Manager è un’azione permanente che non può essere annullata. Come best practice, Adobe consiglia di salvare i file SSL localmente prima di eliminarli in Cloud Manager.

>[!NOTE]
>
>Non puoi eliminare un certificato SSL gestito da Adobe a cui sono associati uno o più domini attivi. Prima di eliminare il certificato SSL è necessario eliminare tutti i domini attivi associati. Per ulteriori informazioni, consulta [Gestire i nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per eliminare un certificato SSL:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.

1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.

1. Nella pagina Certificati SSL, nella riga di tabella del certificato che si desidera eliminare, fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) all&#39;estrema destra, quindi su **Elimina**.

   Se **Elimina** ha un&#39;icona di informazioni come nell&#39;immagine seguente, vedere la nota precedente.

   ![Pulsante Elimina con icona Informazioni](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. Nella finestra di dialogo **Elimina certificato SSL**, fai clic su **Elimina** per confermare l&#39;eliminazione.

1. Esegui la pipeline per annullare la distribuzione del certificato eliminato.


## Configurazioni CDN preesistenti {#pre-existing-cdn}

Se disponi già di una configurazione CDN per il certificato SSL, nella pagina **Certificati SSL** viene visualizzato un messaggio informativo. Ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e gestibili in Cloud Manager.

Il messaggio scompare dopo che tutte le configurazioni dell’ambiente preesistenti sono state migrate utilizzando l’interfaccia utente. Potrebbero essere necessari da uno a due giorni lavorativi prima che il messaggio scompaia.

Per ulteriori dettagli, vedere [Aggiungere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

Un messaggio simile viene visualizzato anche nelle pagine **Elenco consentiti IP** e **Ambienti** per gli ambienti che dispongono di configurazioni CDN preesistenti per Elenchi consentiti IP o nomi di dominio personalizzati.
