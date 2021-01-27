---
title: Utilizzo dello strumento di mappatura utente
description: Utilizzo dello strumento di mappatura utente
translation-type: tm+mt
source-git-commit: a5129eac9f8032de5931b75c83eea62e480c1847
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 1%

---


# Utilizzo dello strumento di mappatura utente {#user-mapping-tool}

## Panoramica {#overview}

Come parte del percorso di transizione da AEM come Cloud Service, è necessario spostare utenti e gruppi dal sistema AEM esistente a AEM come Cloud Service. Questo viene fatto dallo strumento di trasferimento dei contenuti.

Un cambiamento importante nell’AEM come Cloud Service è l’uso completamente integrato di  ID Adobe per accedere al livello di authoring.  Ciò richiede l’utilizzo di Adobe Admin Console per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate nel Adobe   Identity Management System (IMS) che fornisce il single sign-on in tutte  applicazioni cloud Adobe. Per ulteriori dettagli, vedere  Identity Management. A causa di questa modifica, gli utenti e i gruppi esistenti devono essere mappati sui loro ID IMS per evitare la duplicazione di utenti e gruppi nell’istanza di creazione del Cloud Service.

## Considerazioni importanti {#important-considerations}

Vi sono alcuni casi eccezionali da prendere in considerazione. Verranno registrati i seguenti casi specifici e l&#39;utente o il gruppo in questione non verrà mappato:

1. Se un utente non dispone di un indirizzo e-mail nel campo `profile/email` del proprio nodo jcr.

1. Se un&#39;e-mail specificata non viene trovata nel sistema IMS per l&#39;ID organizzazione utilizzato (o se l&#39;ID IMS non può essere recuperato per un altro motivo).

1. Se l&#39;utente è attualmente disattivato, verrà trattato come se non fosse disabilitato.  Sarà mappato e migrato come normale e rimarrà disabilitato nell&#39;istanza cloud.

## Utilizzo dello strumento di mappatura utenti {#using-user-mapping-tool}

Lo strumento di mappatura utenti utilizza un’API che consente di effettuare ricerche per gli utenti IMS tramite e-mail e di restituire i loro ID IMS. Questa API richiede che l&#39;utente crei un ID client per la propria organizzazione, un Segreto cliente e un Token di accesso/Portatore.

Per impostare questa impostazione, effettuate le seguenti operazioni:

1. Andate a [ Adobe Developer Console](https://console.adobe.io) utilizzando l&#39;Adobe ID .
1. Creazione di un nuovo progetto o apertura di un progetto esistente
1. Aggiunta di un&#39;API
1. Scegli API di gestione utente
1. Creare una credenziale JWT
1. Generare una coppia di chiavi o caricare una chiave pubblica (rsa non è buona)
1. Generare un token di accesso (o un token JWT o un token del portatore).
1. Salvate tutte queste informazioni (ID client, Segreto cliente, ID account tecnico, E-mail account tecnico, ID organizzazione, Token di accesso) in un luogo sicuro.

## Interfaccia utente {#user-interface}

Lo strumento di mappatura utenti è integrato nello strumento di trasferimento dei contenuti. Potete scaricare lo strumento di trasferimento dei contenuti dal portale di distribuzione del software. Per ulteriori dettagli sull’ultima versione, consulta Note sulla versione.

1. Selezionare l&#39;Adobe Experience Manager e passare agli strumenti -> **Operazioni** -> **Trasferimento dei contenuti**.
1. Fare clic su **Crea configurazione mappatura utente**.

   >[!NOTE]
   >Se saltate questo passaggio, la mappatura di utenti e gruppi verrà ignorata durante la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   Compilate i campi nella configurazione API di gestione utente come descritto di seguito:

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **ID** organizzazione: Immettete l’ID organizzazione IMS per l’organizzazione per la quale gli utenti vengono migrati.

      >[!NOTE]
      >Per ottenere l&#39;ID organizzazione, accedete al Admin Console [](https://adminconsole.adobe.com/) e scegliete l&#39;organizzazione (nell&#39;area in alto a destra) se appartenete a più di uno. L’ID organizzazione sarà nell’URL della pagina, nel formato `xx@AdobeOrg`, dove xx è l’ID organizzazione IMS.  In alternativa, puoi trovare l&#39;ID organizzazione nella pagina [ Developer Console](https://console.adobe.io) del Adobe in cui crei il Token di accesso.

   * **ID** client: Immettere l&#39;ID client salvato dal passaggio Configurazione

   * **Token** di accesso: Immettere il token di accesso salvato dal passaggio Configurazione

      >[!NOTE]
      >Il token di accesso scade ogni 24 ore e occorre crearne uno nuovo. Per creare un nuovo token, tornate in [ Adobe Developer Console](https://console.adobe.io), scegliete il progetto, fate clic su User Management API e incollate la stessa chiave privata nella casella.

1. Dopo aver immesso le informazioni di cui sopra, fare clic su **Salva**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. Per creare un set di migrazione, fare clic su **Crea set di migrazione** e compilare i campi, quindi fare clic su **Salva**. Per ulteriori dettagli, vedere Esecuzione di Content Transfer Tool.

   >[!NOTE]
   >Per impostazione predefinita, l’interruttore di attivazione/disattivazione per includere la mappatura degli utenti da utenti e gruppi IMS è attivato. Con questa impostazione, quando Estrazione viene eseguita su questo set di migrazione, lo strumento di mappatura utente viene eseguito come parte della fase di estrazione. Questo è il metodo consigliato per eseguire la fase di estrazione dello strumento di trasferimento dei contenuti. Se questa opzione è disattivata e/o la configurazione Mappatura utente non viene creata, la mappatura di utenti e gruppi verrà ignorata durante la fase Estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. Per eseguire la fase di estrazione, fare riferimento a [Esecuzione di Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool).



