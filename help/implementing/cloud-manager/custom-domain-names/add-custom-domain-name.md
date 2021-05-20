---
title: Aggiunta di un nome di dominio personalizzato
description: Aggiunta di un nome di dominio personalizzato
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: e8848a006a28e87a622779ae62bc43c159b2b20c
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

Per aggiungere un nome di dominio personalizzato in Cloud Manager, un utente deve essere un proprietario business o un gestore distribuzione.

## Considerazioni importanti {#important-considerations}

* Prima di aggiungere un nome di dominio personalizzato, è necessario installare nel programma un certificato SSL valido contenente il nome di dominio personalizzato. Per ulteriori informazioni, consulta [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) .

* Impossibile aggiungere i nomi di dominio agli ambienti mentre è presente una pipeline in esecuzione corrente collegata a tali ambienti.

* È possibile aggiungere un solo nome di dominio alla volta. Tuttavia, i domini non possono contenere caratteri jolly. I domini personalizzati lato autore non sono supportati.

* AEM come Cloud Service non supporta i domini con caratteri jolly.

* Ogni ambiente Cloud Manager può ospitare fino a un massimo di 100 domini personalizzati per ambiente.

* Lo stesso nome di dominio non può essere utilizzato in più di un ambiente.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio, effettua le seguenti operazioni:

1. Passa alla schermata **Ambienti** dalla pagina **Panoramica** .

1. Fai clic su **Impostazioni dominio** dal menu di navigazione a sinistra.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Fare clic sul pulsante **Aggiungi dominio** per aprire la finestra di dialogo **Aggiungi nome di dominio**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. Immetti il nome di dominio personalizzato in **Nome di dominio**.

   >[!NOTE]
   >Non includere `http://`, `https://` o spazi quando si accede al dominio.

1. Seleziona il **Ambiente** il cui servizio di pubblicazione sarà associato al nome di dominio.

1. Seleziona il **Certificato SSL di dominio** dal menu a discesa e seleziona **Continua**.

1. **Viene visualizzata la finestra di dialogo Aggiungi** nome di dominio. Verrà visualizzata la finestra Verifica nome di dominio per la schermata Ambiente. Per ulteriori informazioni, consulta [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) .

   Segui le istruzioni fornite per provare la proprietà del dominio per il tuo ambiente:

1. Fai clic su **Crea**.
1. La distribuzione CDN richiede un certificato SSL valido e una verifica TXT corretta. Questo è indicato dallo stato **Verified and Deployed**.
Passa a [Controllo dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori informazioni sui vari stati e su come risolvere il problema.

   >[!NOTE]
   >La bozza DNS può richiedere fino a poche ore per il riconoscimento, a causa di ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visualizzato nella tabella delle impostazioni del dominio. Per ulteriori informazioni, consulta Controllo dello stato del nome di dominio .

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

1. Passa alla pagina Dettagli ambienti per l’ambiente di interesse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilizza i campi di input nella parte superiore della tabella Nomi di dominio per inviare il nome di dominio personalizzato e seleziona il certificato SSL dall’elenco a discesa. Fai clic su **+ Aggiungi**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Controlla i campi dalla finestra di dialogo **Aggiungi nome di dominio** e fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Non includere `http://`, `https://` o spazi quando si accede al dominio.

1. Viene visualizzata la schermata Verifica del nome di dominio per l’ambiente.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Per ulteriori informazioni, consulta [Verifica del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) . Segui le istruzioni fornite per provare la proprietà del dominio per il tuo ambiente.

1. Fai clic su **Crea**.

1. La distribuzione del nome di dominio personalizzato richiede un certificato SSL valido e una verifica TXT corretta. Questo è indicato dallo stato **Verified and Deployed**.

A questo punto, il nome di dominio personalizzato è pronto per il test e un `CNAME` per puntare a esso. Per ulteriori informazioni sui vari stati e su come risolvere, consulta [Stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) .

>[!NOTE]
>La bozza DNS può richiedere fino a poche ore per il riconoscimento, a causa di ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visualizzato nella tabella delle impostazioni del dominio. Per ulteriori informazioni, consulta Controllo dello stato del nome di dominio .
