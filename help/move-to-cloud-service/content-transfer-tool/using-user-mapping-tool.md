---
title: Utilizzo dello strumento di mappatura utente
description: Utilizzo dello strumento di mappatura utente
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
translation-type: tm+mt
source-git-commit: 7bdf8f1e6d8ef1f37663434e7b14798aeb8883f4
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 3%

---

# Utilizzo dello strumento di mappatura utente {#user-mapping-tool}

## Panoramica {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Strumento di mappatura utente"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) consente di spostare gli utenti e i gruppi dal sistema AEM esistente a AEM come Cloud Service. Gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare utenti e gruppi duplicati nell’istanza di authoring del Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerazioni importanti sull’utilizzo dello strumento di mappatura utente"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Utilizzo dello strumento di mappatura utente"


Come parte del percorso di transizione verso Adobe Experience Manager (AEM) come Cloud Service, devi spostare utenti e gruppi dal sistema di AEM esistente a AEM come Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Un cambiamento importante nell’AEM come Cloud Service è l’utilizzo completamente integrato degli ID Adobe per accedere al livello di authoring.  Questo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce il single sign-on in tutte le applicazioni cloud di Adobe. Per ulteriori informazioni, consulta [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). A causa di questa modifica, gli utenti e i gruppi esistenti devono essere mappati ai loro ID IMS per evitare di duplicare utenti e gruppi nell’istanza di authoring del Cloud Service.

## Considerazioni importanti {#important-considerations}

### Casi eccezionali {#exceptional-cases}

Verranno registrati i seguenti casi specifici:

1. Se un utente non ha un indirizzo e-mail nel campo `profile/email` del proprio nodo *jcr*, l&#39;utente o il gruppo in questione verrà migrato ma non mappato.

1. Se una data e-mail non viene trovata nel sistema Adobe Identity Management System (IMS) per l’ID organizzazione utilizzato (o se l’ID IMS non può essere recuperato per un altro motivo), l’utente o il gruppo in questione verrà migrato ma non mappato.

1. Se l’utente è attualmente disattivato, viene trattato come se non fosse disabilitato. Sarà mappato e migrato normalmente e rimarrà disattivato nell’istanza cloud.

1. Se un utente esiste nell&#39;istanza del Cloud Service AEM di destinazione con lo stesso nome utente (rep:principalName) di uno degli utenti nell&#39;istanza AEM di origine, l&#39;utente o il gruppo in questione non verrà migrato.

### Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella il contenuto esistente sull&#39;istanza Cloud prima dell&#39;acquisizione** è impostata, gli utenti già trasferiti sull&#39;istanza del Cloud Service verranno eliminati insieme all&#39;intero archivio esistente e verrà creato un nuovo archivio per l&#39;acquisizione del contenuto in. Questo ripristina anche tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione ed è true per un utente amministratore aggiunto al gruppo **administrators** . L’utente amministratore dovrà essere aggiunto nuovamente al gruppo **administrators** per recuperare il token di accesso per CTT.

* Si consiglia di rimuovere qualsiasi utente esistente dal Cloud Service di destinazione AEM&#39;istanza prima di eseguire CTT con User Mapping. In questo modo si evita qualsiasi conflitto tra la migrazione degli utenti dall’istanza AEM di origine all’istanza AEM di destinazione. I conflitti si verificheranno durante l’acquisizione se lo stesso utente esiste nell’istanza AEM di origine e nell’istanza AEM di destinazione.

* Quando vengono eseguiti gli integratori di contenuto, se il contenuto non viene trasferito perché non è cambiato dal trasferimento precedente, gli utenti e i gruppi associati a tale contenuto non verranno trasferiti, anche se nel frattempo gli utenti e i gruppi sono cambiati. Questo perché gli utenti e i gruppi vengono migrati insieme al contenuto a cui sono associati.

* L’acquisizione avrà esito negativo nei seguenti scenari:

1. Se l&#39;istanza del Cloud Service AEM di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell&#39;istanza AEM di origine.

1. Se nell’istanza di AEM di origine sono presenti due utenti con nomi utente diversi ma con lo stesso indirizzo e-mail. AEM come Cloud Service non consente a due utenti di avere lo stesso indirizzo e-mail.

## Utilizzo dello strumento di mappatura utente {#using-user-mapping-tool}

Lo strumento di mappatura utenti utilizza un’API che consente di cercare gli utenti di Adobe Identity Management System (IMS) tramite e-mail e restituire i loro ID IMS. Questa API richiede all’utente di creare un ID client per la propria organizzazione, un segreto client e un token di accesso o portatore.

Segui i passaggi riportati di seguito per configurare questa impostazione:

1. Passa a [Adobe Developer Console](https://console.adobe.io) utilizzando il tuo Adobe ID.
1. Crea un nuovo progetto o apri un progetto esistente.
1. Aggiungi un’API .
1. Scegli API User Management.
1. Crea una credenziale JWT.
1. Genera una coppia di chiavi o carica una chiave pubblica (rsa non è buona).
1. Genera un token di accesso (o un token JWT o un token portatore).
1. Salva in sicurezza tutte queste informazioni come **ID client**, **Segreto client**, **ID account tecnico**, **E-mail account tecnico**, **ID organizzazione** e **Access Token**.

## Interfaccia utente {#user-interface}

Lo strumento di mappatura utente è integrato nello strumento Content Transfer (Trasferimento contenuti). Puoi scaricare lo strumento Content Transfer (Trasferimento contenuti) da [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Per ulteriori dettagli sull&#39;ultima versione, consulta le [Note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Content Transfer** (Trasferimento contenuti).
1. Fai clic su **Crea configurazione di mappatura utente**.

   >[!NOTE]
   >Se salti questo passaggio, la mappatura di utenti e gruppi verrà ignorata durante la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   Compila i campi nella configurazione dell’API di gestione utente come descritto di seguito:

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **ID** organizzazione: Immetti l’ID organizzazione Adobe Identity Management System (IMS) per l’organizzazione di migrazione degli utenti.

      >[!NOTE]
      >Per ottenere l&#39;ID organizzazione, accedi all&#39; [Admin Console](https://adminconsole.adobe.com/) e scegli la tua organizzazione (nell&#39;area in alto a destra) se appartieni a più di una. L’ID organizzazione sarà nell’URL della pagina, nel formato `xx@AdobeOrg`, dove xx è l’ID organizzazione IMS.  In alternativa, puoi trovare l’ID organizzazione nella pagina [Adobe Developer Console](https://console.adobe.io) in cui generi il token di accesso.

   * **ID** client: Immetti l’ID client salvato dal passaggio Configurazione.

   * **Token** di accesso: Immetti il token di accesso salvato dal passaggio Configurazione.

      >[!NOTE]
      >Il token di accesso scade ogni 24 ore ed è necessario crearne uno nuovo. Per creare un nuovo token, torna a [Adobe Developer Console](https://console.adobe.io), scegli il progetto, fai clic su **User Management API** e incolla la stessa chiave privata nella casella.

1. Dopo aver inserito le informazioni di cui sopra, fai clic su **Salva**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. Crea un set di migrazione facendo clic su **Crea set di migrazione** e compilando i campi, quindi facendo clic su **Salva**. Per ulteriori informazioni, consulta [Esecuzione dello strumento Content Transfer (Trasferimento contenuti)](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool).

   >[!NOTE]
   >L’opzione di attivazione per includere la mappatura degli utenti da utenti e gruppi IMS è attivata per impostazione predefinita. Con questa impostazione, quando si esegue l’estrazione su questo set di migrazione, lo strumento di mappatura utente viene eseguito come parte della fase di estrazione. Questo è il modo consigliato per eseguire la fase di estrazione dello strumento Content Transfer (Trasferimento contenuti). Se questa opzione è disattivata e/o la configurazione di mappatura utente non viene creata, la mappatura di utenti e gruppi verrà ignorata durante la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. Per eseguire la fase di estrazione, fai riferimento a [Esecuzione dello strumento Content Transfer (Trasferimento contenuti)](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool).
