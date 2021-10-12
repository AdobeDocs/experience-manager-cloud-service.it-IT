---
title: Utilizzo dello strumento di mappatura utente
description: Utilizzo dello strumento di mappatura utente
source-git-commit: 6ab32a952a53eed612192ee8359373087e6cf624
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---


# Utilizzo dello strumento di mappatura utente {#using-user-mapping-tool}

Lo strumento di mappatura utenti utilizza un’API che consente di cercare gli utenti di Adobe Identity Management System (IMS) tramite e-mail e restituire i loro ID IMS. Questa API richiede all’utente di creare un ID client per la propria organizzazione, un segreto client e un token di accesso o portatore.

## Impostazione dello strumento di mappatura utente {#setting-up-user-mapping}

Segui i passaggi riportati di seguito per configurare questa impostazione:

1. Passa a [Adobe Developer Console](https://console.adobe.io) utilizzando il tuo Adobe ID.
1. Crea un nuovo progetto o apri un progetto esistente.
1. Aggiungi un&#39;API - Fai clic su **Aggiungi al progetto** e seleziona **API**
1. Scegli API User Management.  Potrebbe essere necessario ottenere le autorizzazioni per avere questa opzione.
1. Crea una credenziale JWT.
1. Genera una coppia di chiavi o carica una chiave pubblica (rsa non è buona).  È presente un pulsante, **Genera una coppia di chiavi pubblica/privata**, che farà questo per te.  Assicurati di salvare le chiavi pubblica e privata.
1. Passa all’API User Management.
1. Genera un token di accesso (o un token portatore) incollando il contenuto della chiave privata nella casella di testo e facendo clic su **Genera token**.
1. Salva in sicurezza tutte queste informazioni come **ID client**, **Segreto client**, **ID account tecnico**, **E-mail account tecnico**, **ID organizzazione** e **Access Token**.

## Accesso all’interfaccia utente per lo strumento di mappatura degli utenti {#user-interface}

Lo strumento di mappatura utente è integrato nello strumento Content Transfer (Trasferimento contenuti). Puoi scaricare lo strumento Content Transfer (Trasferimento contenuti) da [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Per ulteriori dettagli sull&#39;ultima versione, consulta le [Note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Migrazione dei contenuti**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Fai clic sulla scheda **Mappatura utente** .

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Fai clic su **Crea configurazione di mappatura utente**.

   >[!NOTE]
   >Se salti questo passaggio, la mappatura di utenti e gruppi verrà ignorata durante la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Compila i campi in **Configurazione API di gestione utente**, come descritto di seguito.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID** organizzazione: Immetti l’ID organizzazione Adobe Identity Management System (IMS) per l’organizzazione di migrazione degli utenti.

      >[!NOTE]
      >Per ottenere l&#39;ID organizzazione, accedi all&#39; [Admin Console](https://adminconsole.adobe.com/) e scegli la tua organizzazione (nell&#39;area in alto a destra) se appartieni a più di una. L’ID organizzazione sarà nell’URL della pagina, nel formato `xx@AdobeOrg`, dove xx è l’ID organizzazione IMS.  In alternativa, puoi trovare l’ID organizzazione nella pagina [Adobe Developer Console](https://console.adobe.io) in cui generi il token di accesso.

   * **ID** client: Immetti l’ID client salvato dal passaggio Configurazione.

   * **Token** di accesso: Immetti il token di accesso salvato dal passaggio Configurazione.

      >[!NOTE]
      >Il token di accesso scade ogni 24 ore ed è necessario crearne uno nuovo. Per creare un nuovo token, torna a [Adobe Developer Console](https://console.adobe.io), scegli il progetto, fai clic su **User Management API** e incolla la stessa chiave privata nella casella.

1. Dopo aver compilato i campi, fai clic su **Prova configurazione** per verificare la connessione al servizio API User Management. Se la connessione ha esito positivo, potrai fare clic su **Salva** per salvare la configurazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Dopo aver salvato la configurazione, seleziona la configurazione e fai clic su **Avvia mappatura utente**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Una volta completata la mappatura utente, fai clic su **Risultati** per visualizzare il riepilogo.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* Una volta completata la mappatura utente, puoi tornare alla pagina di migrazione dei contenuti utilizzando la breadcrumb. La scheda User Mapping (Mappatura utente) visualizza lo stato e la marca temporale. Fai clic su **Content Transfer** per creare un set di migrazione per eseguire l’estrazione. Per ulteriori informazioni, consulta [Esecuzione dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) .


### Ripresa del processo di mappatura utente {#resume-user-mapping}

Se il processo di mappatura utente viene interrotto a causa di uno dei motivi seguenti:

* L&#39;utente ha selezionato **Interrompi mappatura utente**
* il token di accesso è scaduto durante il processo o,
* un&#39;altra ragione.

L&#39;avanzamento viene salvato dal punto in cui il processo si è interrotto. Rivedi il registro di mappatura utente per controllare l’avanzamento salvato. Fai di nuovo clic sul pulsante **Avvia mappatura utente** per riprendere da dove è stato disattivato. Prima di riavviare, verificare che il token di accesso sia ancora valido o sia stato aggiornato.
