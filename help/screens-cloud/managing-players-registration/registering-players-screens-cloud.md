---
title: Registrazione dei lettori in Screens as a Cloud Service
description: Questa pagina descrive come registrare i lettori in Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 13%

---

# Registrazione dei lettori in Screens as a Cloud Service {#registering-players-screens-cloud}

Dopo aver installato e configurato i lettori per Screens as a Cloud Service, è necessario registrarli.

## Obiettivo {#objective}

Questo documento consente di comprendere la registrazione dei lettori nel provider di servizi Screens. Dopo aver letto dovresti essere in grado di:

* come registrare i lettori
* come completare il processo di registrazione dal provider di servizi Screens

## Procedura per la registrazione di un lettore Screens {#register-players}

Dopo aver installato il lettore in Screens as a Cloud Service, è possibile registrarlo dal provider di servizi Screens.

Per registrare il lettore, segui i passaggi seguenti:

1. Accedere al provider di servizi Screens.

1. Passa a **Codici di registrazione** in **Gestione dei lettori** dal pannello di navigazione a sinistra e fai clic su **Crea codice**.

   >[!NOTE]
   >Se non esistono codici validi/non scaduti, fai clic su Crea codice, immetti un nome per il codice e scegli le impostazioni di scadenza in base alle tue esigenze.

   ![immagine](/help/screens-cloud/assets/player/register-player1.png)

1. Compila i campi seguenti nella finestra di dialogo **Crea codice di registrazione**:

   ![immagine](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome codice di registrazione**: nome del codice di registrazione
   1. **Scadenza codice di registrazione**: data di scadenza del codice di registrazione
   1. **Limita utilizzo**: attiva il pulsante per disattivare il limite di utilizzo del codice di registrazione. Per impostazione predefinita, l’opzione Limita utilizzo è disattivata.
   1. **Limite di utilizzo**: scegli il numero per il limite di utilizzo

1. Fai clic su **Crea** per creare il codice di registrazione. Puoi visualizzare il lettore con il codice di registrazione nell’elenco.

   ![immagine](/help/screens-cloud/assets/player/register-player3.png)

1. Fare clic sul valore nella colonna **CODICE DI REGISTRAZIONE** per copiare il valore negli Appunti.

1. Incolla questo valore nel campo **Inserisci il codice** nella scheda **Registrazione lettore** dall&#39;interfaccia utente di amministrazione del lettore AEM Screens e fai clic su **Registra**.

   ![immagine](/help/screens-cloud/assets/player/register-player4.png)


1. Dopo aver aggiunto il codice, puoi vedere che il lettore è ora registrato dall’interfaccia utente di amministrazione del lettore.

   ![immagine](/help/screens-cloud/assets/player/register-player5.png)

1. Dovresti vedere il lettore ora visualizzato in **Lettori** dal pannello di navigazione a sinistra. Il codice visualizzato nel provider di servizi Screens corrisponde al pannello **Informazioni di sistema** dell&#39;interfaccia utente di amministrazione in Codice lettore.

   ![immagine](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Consigli sulle best practice per la sicurezza durante l&#39;utilizzo del codice di registrazione**
   >Come best practice, è possibile limitare l’utilizzo del codice di registrazione. Se un codice di registrazione è compromesso, ma ha un limite di 100 registrazioni, un hacker può registrare solo fino a quel numero, ma non di più. Puoi sempre aggiornare il limite di utilizzo dopo aver creato il codice di registrazione e aver già registrato alcuni lettori del cliente. Se il cliente osserva un’attività di registrazione insolita per un codice di registrazione specifico, può abbassare il limite in tempo reale mentre indaga e può aumentare il numero indietro se si è trattato di un falso allarme, senza influire sui giocatori già registrati.


## Passaggio successivo {#whats-next}

Dopo aver installato e configurato il lettore in modalità cloud, è necessario continuare con l&#39;percorso Screens as a Cloud Service esaminando il documento [Assegnazione del lettore a una visualizzazione in Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) dal provider di servizi Screens.
