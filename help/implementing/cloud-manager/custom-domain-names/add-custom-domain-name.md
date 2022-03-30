---
title: Aggiunta di un nome di dominio personalizzato
description: Scopri come aggiungere un nome di dominio personalizzato utilizzando Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

In Cloud Manager puoi aggiungere un nome di dominio personalizzato da due posizioni:

* [Dalla pagina Impostazioni dominio](#adding-cdn-settings)
* [Dalla pagina Ambienti](#adding-cdn-environments)

>[!NOTE]
>
>Un utente deve avere **Proprietario business** o **Gestione distribuzione** per aggiungere un nome di dominio personalizzato in Cloud Manager

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Segui questi passaggi per aggiungere un nome di dominio personalizzato dal **Impostazioni di dominio** pagina.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Fai clic su **Impostazioni di dominio** nel pannello di navigazione a sinistra.

   ![Finestra Impostazioni dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Fai clic sul pulsante **Aggiungi dominio** in alto a destra per aprire **Aggiungi nome di dominio** finestra di dialogo.

   ![Finestra di dialogo Aggiungi dominio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Immetti il nome di dominio personalizzato nella **Nome di dominio** campo .

   >[!NOTE]
   >
   >Non includere `http://`, `https://`o spazi quando si accede al dominio.

1. Seleziona la **Ambiente** il cui servizio sarà associato al nome di dominio.

1. Seleziona la **Pubblica** o **Anteprima** servizio.

1. Seleziona la **Certificato SSL del dominio** associato al nome di dominio dal menu a discesa e seleziona **Continua**.

1. La **Aggiungi nome di dominio** viene visualizzata una finestra di dialogo che consente di passare al processo di verifica del nome di dominio. Segui le istruzioni fornite per provare la proprietà del dominio per il tuo ambiente. Fai clic su **Crea**.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La distribuzione CDN richiede un certificato SSL valido e una verifica TXT corretta. Questo è indicato dallo stato **Verificato e distribuito**.

Consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori informazioni sui vari stati e su come affrontare i potenziali problemi.

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore a causa di ritardi di propagazione DNS.
>
>Cloud Manager verificherà la proprietà e aggiornerà lo stato visualizzato nella tabella delle impostazioni del dominio. Consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori dettagli.

>[!TIP]
>
>Fai riferimento a [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) per ulteriori informazioni sui record TXT.

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

Segui questi passaggi per aggiungere un nome di dominio personalizzato dal **Ambienti** pagina.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Dettagli ambienti** per l’ambiente di interesse.

   ![Inserimento del nome di dominio nella pagina Dettagli ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilizza la **Nomi di dominio** per inviare il nome di dominio personalizzato.

   1. Immetti il nome di dominio personalizzato.
   1. Seleziona il certificato SSL associato a questo nome dall’elenco a discesa.
   1. Fai clic su **+Aggiungi**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Controlla i valori selezionati nella **Aggiungi nome di dominio** e fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Non includere `http://`, `https://`o spazi quando si immette nel nome di dominio.

1. La **Aggiungi nome di dominio** viene visualizzata una finestra di dialogo che consente di passare al processo di verifica del nome di dominio. Segui le istruzioni fornite per provare la proprietà del dominio per il tuo ambiente. Fai clic su **Crea**.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La distribuzione CDN richiede un certificato SSL valido e una verifica TXT corretta. Questo è indicato dallo stato **Verificato e distribuito**.

Consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori informazioni sui vari stati e su come affrontare i potenziali problemi.

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore a causa di ritardi di propagazione DNS.
>
>Cloud Manager verificherà la proprietà e aggiornerà lo stato visualizzato nella tabella delle impostazioni del dominio. Consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori dettagli.

>[!TIP]
>
>Fai riferimento a [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) per ulteriori informazioni sui record TXT.
