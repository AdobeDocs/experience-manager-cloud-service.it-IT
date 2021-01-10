---
title: Aggiunta di un nome di dominio personalizzato
description: Aggiunta di un nome di dominio personalizzato
translation-type: tm+mt
source-git-commit: b336f361b496b672d26a5316952ee52ce828e201
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

Per aggiungere un nome di dominio personalizzato in Cloud Manager, un utente deve essere un proprietario aziendale o un gestore distribuzione.

## Considerazioni importanti {#important-considerations}

* Prima di aggiungere un nome di dominio personalizzato, al programma deve essere installato un certificato SSL valido contenente il nome di dominio personalizzato. Per ulteriori informazioni, fare riferimento a [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

* Non è possibile aggiungere i nomi di dominio agli ambienti se è presente una pipeline in esecuzione corrente collegata a tali ambienti.

* È possibile aggiungere un solo nome di dominio alla volta. Tuttavia, i domini non possono contenere caratteri jolly. I domini personalizzati sul lato dell&#39;autore non sono supportati.

* Ogni ambiente Cloud Manager può ospitare fino a un massimo di 100 domini personalizzati per ambiente.

* Lo stesso nome di dominio non può essere utilizzato in più di un ambiente.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio, effettuate le seguenti operazioni:

1. Passare alla schermata **Ambienti** dalla pagina **Panoramica**.

1. Fare clic su **Impostazioni dominio** dal menu di navigazione a sinistra.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Fare clic sul pulsante **Aggiungi dominio** per aprire la finestra di dialogo **Aggiungi nome dominio**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. Immettere il nome di dominio personalizzato in **Nome dominio**.

   >[!NOTE]
   >Non includere `http://`, `https://` o spazi durante l&#39;accesso al dominio.

1. Selezionare l&#39; **Ambiente** il cui servizio Pubblica sarà associato al nome del dominio.

1. Selezionare il **Certificato SSL di dominio** dall&#39;elenco a discesa e selezionare **Continue**.

1. **Viene visualizzata** la finestra di dialogo Aggiungi nome di dominio. Viene visualizzata la schermata Verifica nome dominio per l’ambiente. Per ulteriori informazioni, fare riferimento a [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
Seguite le istruzioni fornite per dimostrare la proprietà del dominio per l’ambiente in uso.

1. Fare clic su **Crea**.
1. La distribuzione CDN richiede un certificato SSL valido e la verifica TXT completata. Questo è indicato dallo stato **Verified and Deployed**.
Per ulteriori informazioni sui vari stati e su come risolvere, passare a [Controllo dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

   >[!NOTE]
   >La prova DNS può richiedere fino a poche ore per il riconoscimento, a causa dei ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visibile nella tabella Impostazioni dominio. Per ulteriori informazioni, fare riferimento a Controllo dello stato del nome di dominio.

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

1. Passate alla pagina Dettagli ambiente per l’ambiente di interesse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilizzate i campi di input nella parte superiore della tabella Nomi di dominio per inviare il nome di dominio personalizzato e selezionate il certificato SSL dall&#39;elenco a discesa. Fare clic su **+ Aggiungi**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Controllare i campi dalla finestra di dialogo **Aggiungi nome dominio** e fare clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Non includete `http://`, `https://` o spazi quando entrate nel vostro dominio.

1. Viene visualizzata la schermata Verifica del nome del dominio per l’ambiente.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Per ulteriori informazioni, fare riferimento a [Verifica del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md). Seguite le istruzioni fornite per dimostrare la proprietà del dominio per l’ambiente in uso.

1. Fare clic su **Crea**.

1. La distribuzione del nome di dominio personalizzato richiede un certificato SSL valido e la verifica TXT completata. Questo è indicato dallo stato **Verified and Deployed**.

A questo punto, il vostro nome di dominio personalizzato è pronto per essere testato e un `CNAME` per indicarlo. Fare riferimento a [Stato nome dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori informazioni sui vari stati e su come risolvere il problema.

>[!NOTE]
>La prova DNS può richiedere fino a poche ore per il riconoscimento, a causa dei ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visibile nella tabella Impostazioni dominio. Per ulteriori informazioni, fare riferimento a Controllo dello stato del nome di dominio.
