---
title: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
description: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
source-git-commit: bec7e01a6f192a9b65a038b2e990c2c285743793
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 29%

---

# Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti) {#getting-started-content-transfer-tool}


## Disponibilità {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Scarica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Note sulla versione"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portale di distribuzione software"

The Content Transfer Tool can be downloaded as a zip file from the Software Distribution Portal. Puoi installare il pacchetto tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) sull’istanza Adobe Experience Manager (AEM) sorgente. Assicurati di scaricare la versione più recente. For more details on the latest version, refer to [Release Notes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

>[!NOTE]
>Scarica lo strumento Content Transfer (Trasferimento contenuti) dal portale di [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Connettività ambiente sorgente {#source-environment-connectivity}

L’istanza di origine AEM può essere in esecuzione dietro un firewall in cui può raggiungere solo alcuni host aggiunti a un Elenco consentiti. In order to successfully run an extraction, the following endpoints will need to be accessible from the instance that is running AEM:

* Il target AEM ambiente as a Cloud Service: `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Servizio di archiviazione BLOB di Azure: `*.blob.core.windows.net`
* Endpoint I/O di mappatura utente: `usermanagement.adobe.io`

Per testare la connettività all&#39;ambiente di destinazione AEM as a Cloud Service, esegui il seguente comando cURL dalla shell dell&#39;istanza di origine (sostituisci `program_id`, `environment_id`e `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>Se `HTTP/2 200` è stata ricevuta una connessione a AEM as a Cloud Service.

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti)  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Running Content Transfer Tool"
>abstract="Learn how to use Content Transfer Tool to migrate the content to AEM as a Cloud Service (Author/Publish)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Vedere Demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial - using Content Transfer Tool"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Segui le indicazioni contenute in questa sezione per apprendere come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti in AEM as a Cloud Service (authoring/pubblicazione):

1. Select the Adobe Experience Manager and navigate to tools -> **Operations** -> **Content Migration**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. Seleziona la **Trasferimento dei contenuti** opzione da **Migrazione dei contenuti** procedura guidata.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. La console seguente viene visualizzata quando crei il primo set di migrazione. Fai clic su **Create Migration Set** (Crea set di migrazione) per creare un nuovo set di migrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >If you have existing migration sets, the console will display the list of existing migration sets with their current status.


1. Compila i campi in **Crea set di migrazione** come descritto di seguito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Name** (Nome): inserisci il nome del set di migrazione.
      >[!NOTE]
      >Il nome del set di migrazione non può contenere caratteri speciali.

   1. **Cloud Service Configuration** (Configurazione Cloud Service): inserisci l’URL dell’istanza di authoring di AEM as a Cloud Service di destinazione.

      >[!NOTE]
      >Puoi creare e mantenere un massimo di dieci set di migrazione alla volta durante l’attività di trasferimento dei contenuti.
      >Inoltre, è necessario creare separatamente una migrazione per ciascun ambiente: *Stage*, *Sviluppo* o *Produzione*.

   1. **Access Token** (Token di accesso): inserisci il token di accesso.

      >[!NOTE]
      >Puoi recuperare il token di accesso utilizzando il **Token di accesso aperto** pulsante . You need to ensure that you belong to the &#39;Administrators&#39; group in the target Cloud Service instance.

   1. **Parameters** (Parametri): seleziona i seguenti parametri per creare il set di migrazione:

      1. **Include Version** (Includi versione): seleziona in base alle esigenze. Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per la migrazione degli eventi di controllo.

         ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >If you intend to include versions as part of a migration set, and are performing top-ups with `wipe=false`, then you must disable version purging due to a current limitation in the Content Transfer Tool. Se preferisci mantenere abilitata l’eliminazione della versione e stai eseguendo i top-up in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.


      1. **Paths to be included** (Percorsi da includere): utilizza il browser percorsi per selezionare i percorsi interessati dalla migrazione. Il selettore del percorso accetta l’input digitando o selezionando.

         >[!IMPORTANT]
         >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (alcuni) `/etc` i percorsi possono essere selezionati in CTT)


1. Fai clic su **Salva** dopo aver compilato tutti i campi nel **Crea set di migrazione** schermata dei dettagli.

1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. Puoi vedere alcune di queste icone descritte di seguito.

   * Una *nuvola rossa* indica che non puoi completare il processo di estrazione.
   * A *nuvola verde* indica che puoi completare il processo di estrazione.
   * Un’*icona gialla* indica che non hai creato il set di migrazione esistente e che quello specifico è stato creato da un altro utente nella stessa istanza.

1. Seleziona un set di migrazione e fai clic su **Proprietà** per visualizzare o modificare le proprietà del set di migrazione. Durante la modifica delle proprietà, non è possibile modificare il **Nome set di migrazione** o **URL servizio**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)


## Novità {#whats-next}

Dopo aver imparato a creare un set di migrazione, ora puoi imparare a usare i processi di estrazione e acquisizione nello strumento Content Transfer (Trasferimento contenuti). Prima di apprendere questi processi, è necessario rivedere [Gestione di archivi di contenuti di grandi dimensioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service.
