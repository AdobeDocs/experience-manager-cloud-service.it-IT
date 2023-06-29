---
title: Utilizzo dello strumento di mappatura utenti (legacy)
description: Utilizzo dello strumento di mappatura utenti (legacy)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# Utilizzo dello strumento di mappatura utenti (legacy) {#using-user-mapping-tool}

>[!INFO]
>
>Questa documentazione fa riferimento a una versione obsoleta dello strumento. Per ulteriori informazioni sull’ultima versione, consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

Lo strumento di mappatura utenti utilizza un’API che consente di cercare gli utenti Adobe Identity Management System (IMS) tramite e-mail e restituire i loro ID IMS. Questa API richiede che l’utente crei un ID client per la propria organizzazione, un segreto client e un token di accesso o Bearer.

## Impostazione dello strumento di mappatura utenti {#setting-up-user-mapping}

**Prerequisito:** La mappatura utente richiede che ogni utente da mappare sul suo ID IMS abbia un indirizzo e-mail nel suo profilo in AEM e in IMS. Anche se l’utente utilizza un indirizzo e-mail come ID utente per l’accesso, la mappatura non funziona per tale utente a meno che l’indirizzo e-mail non sia presente anche nel profilo e in IMS.

Per configurare questa configurazione, segui i passaggi seguenti:

1. Accedi a [Console Adobe Developer](https://developer.adobe.com/console/) utilizzando il tuo Adobe ID.
1. Crea un progetto o apri un progetto esistente.
1. Aggiungi un’API - Fai clic su **Aggiungi al progetto** e seleziona **API**
1. Scegli API User Management. Per rendere disponibile questa opzione è necessario disporre delle autorizzazioni di amministratore di sistema.
1. Crea una credenziale JWT.
1. Genera una coppia di chiavi o carica una chiave pubblica (rsa non è un buon metodo). C&#39;è un pulsante, **Genera una coppia di chiavi pubblica/privata** che crea questa coppia di chiavi. Assicurati di salvare sia le chiavi pubbliche che quelle private.
1. Passa all’API User Management.
1. Generare un token di accesso (o token Bearer) incollando il contenuto della chiave privata nella casella di testo e facendo clic su **Genera token**.
1. Salva tutte queste informazioni come **ID client**, **Segreto client**, **ID account tecnico**, **E-mail account tecnico**, **ID organizzazione**, e **Token di accesso** in modo sicuro.

## Accesso all&#39;interfaccia utente per lo strumento di mappatura utenti {#user-interface}

Lo strumento di mappatura utenti è integrato nello strumento Content Transfer (Trasferimento contenuti). Puoi scaricare lo strumento Content Transfer (Trasferimento contenuti) da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Per maggiori dettagli sull’ultima versione, consulta [Note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Migrazione dei contenuti**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Fai clic su **Mappatura utenti** Card.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Clic **Crea configurazione mappatura utenti**.

   >[!NOTE]
   >Se salti questo passaggio, la mappatura di utenti e gruppi viene ignorata durante la fase di estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Compila i campi in **Configurazione API gestione utenti**, come descritto di seguito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID organizzazione**: immetti l’ID dell’organizzazione Adobe Identity Management System (IMS) per l’organizzazione di cui vengono migrati gli utenti.

     >[!NOTE]
     >Per ottenere l’ID organizzazione, accedi a [Admin Console](https://adminconsole.adobe.com/) e scegli la tua organizzazione (in alto a destra) se appartieni a più di una. L’ID organizzazione si trova nell’URL della pagina, in un formato simile a `xx@AdobeOrg`, dove xx è l’ID dell’organizzazione IMS. In alternativa, puoi trovare l’ID organizzazione nel [Console Adobe Developer](https://developer.adobe.com/console/) in cui viene generato il token di accesso.

   * **ID client**: immetti l’ID client salvato dal passaggio Configurazione.

   * **Token di accesso**: immetti il token di accesso salvato dal passaggio Configurazione.

     >[!NOTE]
     >Il token di accesso scade ogni 24 ore ed è necessario crearne uno nuovo. Per creare un token, torna a [Console Adobe Developer](https://developer.adobe.com/console/), scegli il progetto, fai clic su **API User Management** e incolla la stessa chiave privata nella casella.

1. Dopo aver popolato i campi, fai clic su **Prova configurazione** per verificare la connessione al servizio API User Management. Se la connessione ha esito positivo, puoi fare clic su **Salva** per salvare la configurazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Dopo aver salvato la configurazione, selezionala e fai clic su **Avvia mappatura utenti**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Clic **Inizio** dalla finestra di dialogo, in modo da avviare il processo di mappatura utente.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Viene visualizzato il **Stato** as **IN ESECUZIONE**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Una volta completata la mappatura utente, fai clic su **Risultati** per visualizzare il riepilogo.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* Una volta completata la mappatura utente, puoi tornare alla pagina di migrazione dei contenuti utilizzando la breadcrumb. La scheda Mappatura utente visualizza lo stato e la marca temporale. Clic **Trasferimento dei contenuti** in modo da poter creare un set di migrazione per eseguire l’estrazione. Consulta [Esecuzione dello strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) per ulteriori dettagli.

### Ripresa del processo di mappatura utenti {#resume-user-mapping-process}

Se il processo di mappatura utenti viene interrotto per uno dei motivi seguenti:

* Opzione **Interrompi mappatura utenti** selezionato dall&#39;utente.
* Il token di accesso è scaduto durante il processo.
* O per qualche altra ragione.

  >[!NOTE]
  >L’avanzamento viene salvato dal punto in cui è stato interrotto il processo.

Per riprendere il processo di mappatura utenti, effettua le seguenti operazioni:

1. Clic **Visualizza registro** per rivedere il registro di mappatura utenti in modo da poter controllare l’avanzamento salvato.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Clic **Avvia mappatura utenti** per riprendere dal punto in cui era stato interrotto.

   >[!NOTE]
   >Prima di riavviare il computer, verifica che il token di accesso sia ancora valido o che sia stato aggiornato.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Clic **Inizio** dalla finestra di dialogo, in modo da riprendere il processo di mappatura utente.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Al termine del processo di mappatura utenti, puoi visualizzare **Stato** as **COMPLETATO** per quella specifica configurazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
