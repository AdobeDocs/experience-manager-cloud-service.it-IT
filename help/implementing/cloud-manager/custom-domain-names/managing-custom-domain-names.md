---
title: Gestione dei nomi di dominio personalizzati
description: Scopri come utilizzare Cloud Manager per visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# Gestione dei nomi di dominio personalizzati {#managing-custom-domain-names}

Cloud Manager consente di visualizzare, aggiornare, sostituire ed eliminare nomi di dominio personalizzati.

## Visualizza e aggiorna {#view-and-update}

Utilizza la **Visualizza e aggiorna** per visualizzare i dettagli di uno dei nomi di dominio personalizzati.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Identifica la riga del nome di dominio personalizzato che desideri visualizzare o aggiornare.

1. Fai clic sul pulsante con i puntini di sospensione all’estremità destra della riga.

1. Seleziona la **Visualizza e aggiorna** opzione .

## Aggiornamento del certificato SSL del nome di dominio personalizzato {#update-cert}

Puoi seguire [gli stessi passaggi per visualizzare e aggiornare un nome di dominio personalizzato](#view-and-update) per aggiornare il certificato SSL di un nome di dominio personalizzato.

>[!NOTE]
>
>Il certificato SSL deve essere valido, [già configurato,](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e contengono il nome di dominio personalizzato che si sta aggiornando.

##  Eliminazione di un nome di dominio personalizzato {#deleting}

Un utente con **Proprietario business** o **Gestione distribuzione** Il ruolo può utilizzare Cloud Manager per eliminare un nome di dominio personalizzato.

### Eliminazione di un nome di dominio personalizzato da tutti gli ambienti associati {#delete-cdn-all}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Passa a **Impostazioni di dominio** dalla pagina **Ambienti** schermo.

1. Identifica la riga del nome di dominio personalizzato che desideri eliminare.

1. Fai clic sul pulsante con i puntini di sospensione all’estremità destra della riga.

1. Seleziona **Elimina**.

   ![Eliminazione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. Conferma l’invio.

### Eliminazione di un nome di dominio personalizzato da un ambiente specifico {#delete-cdn-specific}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.
1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.
1. Da **Ambienti** , passa alla schermata dei dettagli dell’ambiente di interesse.
1. Nella tabella dei nomi di dominio, identificare la riga del nome di dominio personalizzato che si desidera eliminare.
1. Fai clic sul pulsante con i puntini di sospensione all’estremità destra della riga.
1. Seleziona **Elimina**.
1. Conferma l’invio.
