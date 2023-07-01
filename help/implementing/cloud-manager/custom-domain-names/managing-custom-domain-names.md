---
title: Gestione dei nomi di dominio personalizzati
description: Scopri come visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati con Cloud Manager.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 96%

---

# Gestione dei nomi di dominio personalizzati {#managing-custom-domain-names}

Cloud Manager consente di visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati.

## Menu Visualizza e aggiorna {#view-and-update}

Visualizza i dettagli di qualsiasi nome di dominio personalizzato tramite il menu **Visualizza e aggiorna**.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Individua la riga del nome di dominio personalizzato che desideri visualizzare o aggiornare.

1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.

1. Seleziona l’opzione **Visualizza e aggiorna**.

## Aggiornamento del certificato SSL di un nome di dominio personalizzato {#update-cert}

Per aggiornare il certificato SSL di un nome di dominio personalizzato, segui la [stessa procedura indicata per visualizzare e aggiornare un nome di dominio personalizzato](#view-and-update).

>[!NOTE]
>
>Il certificato SSL deve essere valido, [precedentemente configurato](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e contenere il nome di dominio personalizzato che desideri aggiornare.

## Eliminazione di un nome di dominio personalizzato {#deleting}

L’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può eliminare un nome di dominio personalizzato con Cloud Manager.

### Eliminazione di un nome di dominio personalizzato da tutti gli ambienti associati {#delete-cdn-all}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla schermata **Ambienti**, accedi alla pagina **Impostazioni dominio**.

1. Individua la riga del nome di dominio personalizzato che desideri eliminare.

1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.

1. Seleziona **Elimina**.

   ![Eliminazione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. Conferma quanto inserito.

### Eliminazione di un nome di dominio personalizzato da un ambiente specifico {#delete-cdn-specific}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla pagina **Ambienti**, accedi alla schermata dei dettagli dell’ambiente di tuo interesse.
1. Nella tabella dei nomi di dominio, individua la riga del nome di dominio personalizzato che desideri eliminare.
1. Fai clic sul pulsante con i puntini di sospensione all’estrema destra della riga.
1. Seleziona **Elimina**.
1. Conferma quanto inserito.
