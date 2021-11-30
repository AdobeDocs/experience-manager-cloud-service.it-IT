---
title: Registrazione dei lettori in Screens as a Cloud Service
description: Questa pagina descrive come registrare i lettori in Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Registrazione dei lettori in Screens as a Cloud Service {#registering-players-screens-cloud}

Una volta installati e configurati i lettori per Screens as a Cloud Service, è necessario registrare i lettori.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come registrare i lettori nel provider di servizi Screens. Dopo aver letto dovrebbe essere in grado di:

* scopri come registrare i giocatori
* come completare il processo di registrazione da Screens Services Provider

## Passaggi per registrare un lettore Screens {#register-players}

Dopo aver installato il lettore su Screens as a Cloud Service, è possibile registrare il lettore da Screens Services Provider.

Per registrare il lettore, effettua le seguenti operazioni:

1. Accedi al provider di servizi Screens.

1. Passa a **Codici di registrazione** sotto **Gestione dei giocatori** dal pannello di navigazione a sinistra e fai clic su **Crea codice**.

   >[!NOTE]
   >Se non esistono codici validi/non scaduti, fai clic su crea codice e inserisci un nome per il codice, quindi scegli le impostazioni di scadenza in base alle tue esigenze.

   ![immagine](/help/screens-cloud/assets/player/register-player1.png)

1. Compila i campi seguenti in **Crea un codice di registrazione** finestra di dialogo:

   ![immagine](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome del codice di registrazione**: Nome del codice di registrazione
   1. **Scadenza codice registrazione**: Data di scadenza del codice di registrazione
   1. **Utilizzo limite**: Attiva il pulsante per disattivare il limite di utilizzo del codice di registrazione. Per impostazione predefinita, l’opzione Limita utilizzo è disattivata.
   1. **Limite di utilizzo**: Scegliere il numero per il limite di utilizzo

1. Fai clic su **Crea** per creare il codice di registrazione. Vedrai il tuo giocatore con il codice di registrazione nell&#39;elenco.

   ![immagine](/help/screens-cloud/assets/player/register-player3.png)

1. Fai clic sul valore sotto la colonna **CODICE DI REGISTRAZIONE**  per copiare il valore negli Appunti.

1. Incolla questo valore nel **Immetti il codice** nel campo **Registrazione lettore** scheda dall’interfaccia utente amministratore di AEM Screens Player e fai clic su **Registro**.

   ![immagine](/help/screens-cloud/assets/player/register-player4.png)


1. Dopo aver aggiunto il codice, vedrai che il lettore è ora registrato dall’interfaccia utente amministratore del lettore.

   ![immagine](/help/screens-cloud/assets/player/register-player5.png)

1. Dovresti vedere questo giocatore ora apparire in **Giocatori** dal pannello di navigazione a sinistra. Il codice visualizzato in Screens Services Provider corrisponde al **Informazioni di sistema** pannello dall&#39;interfaccia utente amministratore in Codice lettore.

   ![immagine](/help/screens-cloud/assets/player/register-player6.png)

>[!IMPORTANT]
>**Raccomandazione sulle best practice per la sicurezza durante l&#39;utilizzo del codice di registrazione
>Come best practice, puoi limitare l’utilizzo del codice di registrazione. Se un codice di registrazione è compromesso, ma ha un limite di 100 registrazioni, l&#39;autore dell&#39;attacco può registrare solo fino a quel numero, ma non di più. È sempre possibile aggiornare il limite di utilizzo dopo la creazione del codice di registrazione e dopo la registrazione di alcuni giocatori del cliente. Se il cliente osserva un&#39;attività di registrazione insolita per un codice di registrazione specifico, può abbassare il limite in tempo reale mentre indaga e può aumentare il numero se si tratta di un falso allarme, senza influire sui giocatori già registrati.


## Novità {#whats-next}

Ora, dopo aver installato e configurato il lettore in modalità Cloud, dovresti continuare il tuo percorso as a Cloud Service Screens esaminando il documento, [Assegnazione del lettore a una visualizzazione in Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) da Screens Services Provider.
