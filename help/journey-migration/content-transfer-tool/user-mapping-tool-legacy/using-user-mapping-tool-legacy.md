---
title: Utilizzo dello strumento di mappatura utente (legacy)
description: Utilizzo dello strumento di mappatura utente (legacy)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 154c3eb3dbee07e830f489212777540a18c952b3
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 3%

---

# Utilizzo dello strumento di mappatura utente (legacy) {#using-user-mapping-tool}

>[!INFO]
>
>Questa documentazione fa riferimento a una versione obsoleta di questo strumento. Per ulteriori informazioni sull’ultima versione, consulta [Mappatura utente e migrazione principale](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

Lo strumento di mappatura utenti utilizza un’API che consente di cercare gli utenti di Adobe Identity Management System (IMS) tramite e-mail e restituire i loro ID IMS. Questa API richiede all’utente di creare un ID client per la propria organizzazione, un segreto client e un token di accesso o portatore.

## Impostazione dello strumento di mappatura utente {#setting-up-user-mapping}

**Prerequisito:** La mappatura utente richiede che ogni utente sia mappato al suo ID IMS abbia un indirizzo e-mail nel suo profilo in AEM e in IMS.  Tieni presente che anche se l’utente utilizza un indirizzo e-mail come ID utente per l’accesso, la mappatura non funzionerà per tale utente, a meno che l’indirizzo e-mail non sia anche nel profilo e anche in IMS.

Segui i passaggi riportati di seguito per configurare questa impostazione:

1. Passa a [Console Adobe Developer](https://console.adobe.io) utilizzando il tuo Adobe ID.
1. Crea un nuovo progetto o apri un progetto esistente.
1. Aggiungi un’API - Fai clic su **Aggiungi a progetto** e seleziona **API**
1. Scegli API User Management.  Per rendere disponibile questa opzione, è necessario disporre delle autorizzazioni di amministratore di sistema.
1. Crea una credenziale JWT.
1. Genera una coppia di chiavi o carica una chiave pubblica (rsa non è buona).  C&#39;è un pulsante, **Generare una coppia di chiavi pubblica/privata**, che farà questo per te.  Assicurati di salvare le chiavi pubblica e privata.
1. Passa all’API User Management.
1. Genera un token di accesso (o un token portatore) incollando il contenuto della chiave privata nella casella di testo e facendo clic su **Genera token**.
1. Salva tutte queste informazioni, ad esempio **ID client**, **Segreto client**, **ID account tecnico**, **E-mail account tecnico**, **ID organizzazione** e **Token di accesso** sicuro.

## Accesso all’interfaccia utente per lo strumento di mappatura degli utenti {#user-interface}

Lo strumento di mappatura utente è integrato nello strumento Content Transfer (Trasferimento contenuti). Puoi scaricare lo strumento Content Transfer (Trasferimento contenuti) da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Per ulteriori informazioni sull’ultima versione, consulta la [Note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Migrazione dei contenuti**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Fai clic su **Mappatura utente** il Card.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Fai clic su **Creare una configurazione di mappatura utente**.

   >[!NOTE]
   >Se salti questo passaggio, la mappatura di utenti e gruppi verrà ignorata durante la fase di estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Compila i campi in **Configurazione API di gestione utenti**, come descritto di seguito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID organizzazione**: Immetti l’ID organizzazione Adobe Identity Management System (IMS) per l’organizzazione di migrazione degli utenti.

      >[!NOTE]
      >Per ottenere l&#39;ID organizzazione, accedi al [Admin Console](https://adminconsole.adobe.com/) e scegli la tua organizzazione (in alto a destra) se appartieni a più di una. L&#39;ID organizzazione sarà nell&#39;URL della pagina, nel formato come `xx@AdobeOrg`, dove xx è l’ID organizzazione IMS.  In alternativa, puoi trovare l’ID organizzazione nel [Console Adobe Developer](https://console.adobe.io) pagina in cui viene generato il token di accesso.

   * **ID client**: Immetti l’ID client salvato dal passaggio Configurazione.

   * **Token di accesso**: Immetti il token di accesso salvato dal passaggio Configurazione.

      >[!NOTE]
      >Il token di accesso scade ogni 24 ore ed è necessario crearne uno nuovo. Per creare un nuovo token, torna a [Console Adobe Developer](https://console.adobe.io), scegli il progetto e fai clic su **API di gestione utenti** e incolla la stessa chiave privata nella casella.

1. Dopo aver compilato i campi, fai clic su **Configurazione del test** per verificare la connessione al servizio API User Management. Se la connessione ha esito positivo, potrai fare clic su **Salva** per salvare la configurazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Dopo aver salvato la configurazione, seleziona la configurazione e fai clic su **Avvia mappatura utente**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Fai clic su **Inizio** dalla finestra di dialogo per avviare il processo di mappatura utente.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Visualizza la **Stato** come **IN ESECUZIONE**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Una volta completata la mappatura utente, fai clic su **Risultati** per visualizzare il riepilogo.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* Una volta completata la mappatura utente, puoi tornare alla pagina di migrazione dei contenuti utilizzando la breadcrumb. La scheda User Mapping (Mappatura utente) visualizza lo stato e la marca temporale. Fai clic su **Trasferimento dei contenuti** per creare un set di migrazione per eseguire l’estrazione. Fai riferimento a [Esecuzione dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) per ulteriori dettagli.


### Ripresa del processo di mappatura utente {#resume-user-mapping-process}

Se il processo di mappatura utente viene interrotto a causa di uno dei motivi seguenti:

* Utente selezionato **Interrompi mappatura utente**
* il token di accesso è scaduto durante il processo o,
* qualche altra ragione

   >[!NOTE]
   >L&#39;avanzamento viene salvato dal punto in cui il processo si è interrotto.

Segui i passaggi riportati di seguito per riprendere il processo di mappatura utente:

1. Fai clic su **Visualizza registro** per controllare l&#39;avanzamento salvato, controlla il registro di mappatura utente.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Fai clic sul pulsante **Avvia mappatura utente** per riprendere da dove è stato disattivato.

   >[!NOTE]
   >Prima di riavviare, verificare che il token di accesso sia ancora valido o sia stato aggiornato.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Fai clic su **Inizio** dalla finestra di dialogo per riprendere il processo di mappatura utente.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Una volta completato il processo di mappatura utente, visualizzerai il **Stato** come **COMPLETATO** per la configurazione specifica.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
