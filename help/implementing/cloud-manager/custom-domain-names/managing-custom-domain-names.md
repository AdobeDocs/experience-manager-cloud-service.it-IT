---
title: Gestione dei nomi di dominio personalizzati
description: Scopri come visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati con Cloud Manager.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2d1382c84d872719332986baa5829d1623d9d9a6
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 34%

---


# Gestire i nomi di dominio personalizzati {#managing-custom-domain-names}

Cloud Manager consente di modificare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati.

## Modificare una configurazione del nome di dominio personalizzato {#view-and-update}

Ad Adobe, in Cloud Manager potrebbe essere utile modificare la configurazione di un nome di dominio personalizzato per i seguenti motivi:

* **Cambio degli ambienti**: applicare la configurazione corretta a seconda che il contenuto venga distribuito agli utenti finali (Publish) o agli utenti interni (Author).
* **Aggiornamenti della sicurezza**: per eseguire l&#39;aggiornamento a un certificato SSL più recente per migliorare la sicurezza o la conformità.
* **Modifica della strategia di distribuzione**: assicurarsi che il certificato SSL corretto venga applicato a un ambiente specifico per la crittografia e l&#39;accesso al sito corretti.

**Per modificare la configurazione di un nome di dominio personalizzato:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra.
1. Nell&#39;intestazione **Services**, fare clic su **Configurazioni CDN**.
1. Nella pagina **Configurazioni CDN**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui desideri modificare la CDN.
1. Fai clic su **Modifica**.
1. Nella finestra di dialogo **Modifica configurazione CDN** eseguire le operazioni seguenti:
   * Nell&#39;elenco a discesa **Livello** selezionare il livello (Publish o Anteprima) che si desidera utilizzare.
   * Nell&#39;elenco a discesa **Certificato SSL** selezionare il certificato SSL che si desidera utilizzare.
1. Fai clic su **Aggiorna**.


## Aggiornare il certificato SSL di un nome di dominio personalizzato {#update-cert}

Per aggiornare il certificato SSL di un nome di dominio personalizzato, segui la [stessa procedura indicata per visualizzare e aggiornare un nome di dominio personalizzato](#view-and-update).

>[!NOTE]
>
>Il certificato SSL deve essere valido, [già configurato](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) e contenere il nome di dominio personalizzato che si sta aggiornando.


## Eliminare un nome di dominio personalizzato {#deleting}

L’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può eliminare un nome di dominio personalizzato con Cloud Manager.

### Eliminare un nome di dominio personalizzato da tutti gli ambienti associati {#delete-cdn-all}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla schermata **Panoramica**, accedi alla pagina **Impostazioni dominio**.

1. Identifica la riga del nome di dominio personalizzato che desideri eliminare.

1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.

1. Seleziona **Elimina**.

1. Conferma quanto inserito.


### Eliminare un nome di dominio personalizzato da un ambiente specifico {#delete-cdn-specific}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla pagina **Ambienti**, accedi a una schermata dei dettagli dell&#39;ambiente di tuo interesse.
1. Nella tabella dei nomi di dominio, identifica la riga del nome di dominio personalizzato che desideri eliminare.
1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.
1. Seleziona **Elimina**.
1. Conferma quanto inserito.
