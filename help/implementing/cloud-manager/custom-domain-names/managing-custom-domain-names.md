---
title: Gestione dei nomi di dominio personalizzati
description: Scopri come visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati con Cloud Manager.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4e887b753eaf09e104c68484792f00dcb08ee304
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 57%

---


# Gestire i nomi di dominio personalizzati {#managing-custom-domain-names}

Cloud Manager consente di visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati.

## Visualizzare e aggiornare un nome di dominio personalizzato {#view-and-update}

Visualizza i dettagli di qualsiasi nome di dominio personalizzato tramite il menu **Visualizza e aggiorna**.

**Per visualizzare e aggiornare un nome di dominio personalizzato:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Identifica la riga del nome di dominio personalizzato che desideri visualizzare o aggiornare.

1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.

1. Seleziona l’opzione **Visualizza e aggiorna**.

## Aggiornare il certificato SSL di un nome di dominio personalizzato {#update-cert}

Per aggiornare il certificato SSL di un nome di dominio personalizzato, segui la [stessa procedura indicata per visualizzare e aggiornare un nome di dominio personalizzato](#view-and-update).

>[!NOTE]
>
>Il certificato SSL deve essere valido, [già configurato](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e contenere il nome di dominio personalizzato che si sta aggiornando.

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
