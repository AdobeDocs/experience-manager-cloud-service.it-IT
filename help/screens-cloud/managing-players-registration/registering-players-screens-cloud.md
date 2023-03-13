---
title: Registrazione dei lettori in Screens as a Cloud Service
description: Questa pagina descrive come registrare i lettori in Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: fb82970154fa37e3b3d1591a2e25989853ec6b90
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Registrazione dei lettori in Screens as a Cloud Service {#registering-players-screens-cloud}

Dopo aver installato e configurato i lettori per Screens as a Cloud Service, è necessario registrarli.

## Obiettivo {#objective}

Questo documento spiega come registrare i lettori nel provider di servizi Screens. Dopo aver letto dovresti essere in grado di:

* come registrare i lettori
* come completare il processo di registrazione dal provider di servizi Screens

## Passaggi per registrare un lettore Screens {#register-players}

Dopo aver installato il lettore su Screens as a Cloud Service, è possibile registrarlo dal provider di Screens Services.

Per registrare il lettore, segui i passaggi seguenti:

1. Accedi al provider Screens Services.

1. Accedi a **Codici di registrazione** in **Gestione dei giocatori** dal pannello di navigazione a sinistra e fai clic su **Crea codice**.

   >[!NOTE]
   >Se non esistono codici validi/non scaduti, fai clic su Crea codice, immetti un nome per il codice e scegli le impostazioni di scadenza in base alle tue esigenze.

   ![immagine](/help/screens-cloud/assets/player/register-player1.png)

1. Compila i campi seguenti in **Creare un codice di registrazione** finestra di dialogo:

   ![immagine](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome codice di registrazione**: nome del codice di registrazione
   1. **Scadenza codice di registrazione**: data di scadenza del codice di registrazione
   1. **Limita utilizzo**: attiva il pulsante per disattivare il limite di utilizzo del codice di registrazione. Per impostazione predefinita, l’opzione Limita utilizzo è disattivata.
   1. **Limite di utilizzo**: scegli il numero per il limite di utilizzo

1. Fai clic su **Crea** per creare il codice di registrazione. Visualizzerai il lettore con il codice di registrazione nell’elenco.

   ![immagine](/help/screens-cloud/assets/player/register-player3.png)

1. Fai clic sul valore sotto la colonna **CODICE DI REGISTRAZIONE**  per copiare il valore negli Appunti.

1. Incolla questo valore in **Immetti il codice** campo in **Registrazione lettore** nell’interfaccia utente di amministrazione del lettore AEM Screens, quindi fai clic su **Registrati**.

   ![immagine](/help/screens-cloud/assets/player/register-player4.png)


1. Dopo aver aggiunto il codice, vedrai che il lettore è ora registrato dall’interfaccia utente di amministrazione del lettore.

   ![immagine](/help/screens-cloud/assets/player/register-player5.png)

1. Dovresti vedere questo lettore ora comparire in **Lettori** dal pannello di navigazione a sinistra. Il codice visualizzato nel provider di servizi Screens corrisponde al **Informazioni di sistema** nell’interfaccia utente di amministrazione, in Codice del lettore.

   ![immagine](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Consigli sulle best practice per la sicurezza durante l’utilizzo del codice di registrazione**
   >Come best practice, puoi limitare l’utilizzo del codice di registrazione. Se un codice di registrazione è compromesso, ma ha un limite di 100 registrazioni, l&#39;autore dell&#39;attacco può registrare solo fino a quel numero, ma non di più. Puoi sempre aggiornare il limite di utilizzo dopo aver creato il codice di registrazione e aver già registrato alcuni lettori del cliente. Se il cliente osserva un’attività di registrazione insolita per un codice di registrazione specifico, può abbassare il limite in tempo reale mentre indaga e può aumentare il numero indietro se si è trattato di un falso allarme, senza influire sui giocatori già registrati.


## Passaggio successivo {#whats-next}

Ora che hai installato e configurato il lettore in modalità Cloud, devi continuare il percorso Screens as a Cloud Service esaminando il documento, [Assegnazione del lettore a un display in Schermi as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) da Screens Services Provider.
