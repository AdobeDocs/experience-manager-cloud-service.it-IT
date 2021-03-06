---
title: Guida introduttiva allo strumento Content Transfer (legacy)
description: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 22%

---

# Guida introduttiva allo strumento Content Transfer (legacy) {#getting-started-content-transfer-tool}


## Disponibilità {#availability}

Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) sull’istanza Adobe Experience Manager (AEM) sorgente. Assicurati di scaricare la versione più recente. Per ulteriori dettagli sull’ultima versione, consulta [Note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

>[!NOTE]
>Scarica lo strumento Content Transfer (Trasferimento contenuti) dal portale di [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Connettività ambiente sorgente {#source-environment-connectivity}

L’istanza di origine AEM può essere in esecuzione dietro un firewall in cui può raggiungere solo alcuni host aggiunti a un Elenco consentiti. Per eseguire correttamente un’estrazione, i seguenti endpoint devono essere accessibili dall’istanza in esecuzione AEM:

* Il target AEM ambiente as a Cloud Service: `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Servizio di archiviazione BLOB di Azure: `*.blob.core.windows.net`
* Endpoint I/O di mappatura utente: `usermanagement.adobe.io`

Per testare la connettività all&#39;ambiente di destinazione AEM as a Cloud Service, esegui il seguente comando cURL dalla shell dell&#39;istanza di origine (sostituisci `program_id`, `environment_id`e `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>Se `HTTP/2 200` è stata ricevuta una connessione a AEM as a Cloud Service.

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti)  {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Segui le indicazioni contenute in questa sezione per apprendere come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti in AEM as a Cloud Service (authoring/pubblicazione):

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Migrazione dei contenuti**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. Seleziona la **Trasferimento dei contenuti** opzione da **Migrazione dei contenuti** procedura guidata.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. La console seguente viene visualizzata quando crei il primo set di migrazione. Fai clic su **Create Migration Set** (Crea set di migrazione) per creare un nuovo set di migrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Se disponi di set di migrazione esistenti, nella console viene visualizzato l’elenco dei set di migrazione esistenti con il relativo stato corrente.


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
      >Puoi recuperare il token di accesso utilizzando il **Token di accesso aperto** pulsante . Devi accertarti di appartenere al gruppo &quot;Amministratori&quot; nell’istanza del Cloud Service di destinazione.

   1. **Parameters** (Parametri): seleziona i seguenti parametri per creare il set di migrazione:

      1. **Include Version** (Includi versione): seleziona in base alle esigenze. Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per la migrazione degli eventi di controllo.

         ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >Se intendi includere versioni come parte di un set di migrazione e stai eseguendo integrazioni con `wipe=false`, quindi devi disattivare l’eliminazione della versione a causa di un limite corrente nello strumento Content Transfer (Trasferimento contenuti). Se preferisci mantenere abilitata l’eliminazione della versione e stai eseguendo i top-up in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.


      1. **Paths to be included** (Percorsi da includere): utilizza il browser percorsi per selezionare i percorsi interessati dalla migrazione. Il selettore del percorso accetta l’input digitando o selezionando.

         >[!IMPORTANT]
         >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (alcuni) `/etc` i percorsi possono essere selezionati in CTT)


1. Fai clic su **Salva** dopo aver compilato tutti i campi nel **Crea set di migrazione** schermata dei dettagli.

1. Il set di migrazione verrà visualizzato in **Trasferimento dei contenuti** , come illustrato nella figura riportata di seguito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   Tutti i set di migrazione esistenti vengono visualizzati nella sezione **Trasferimento dei contenuti** procedura guidata con lo stato corrente e le informazioni sullo stato. Puoi vedere alcune di queste icone descritte di seguito.

   * Una *nuvola rossa* indica che non puoi completare il processo di estrazione.
   * A *nuvola verde* indica che puoi completare il processo di estrazione.
   * Un’*icona gialla* indica che non hai creato il set di migrazione esistente e che quello specifico è stato creato da un altro utente nella stessa istanza.

1. Seleziona un set di migrazione e fai clic su **Proprietà** per visualizzare o modificare le proprietà del set di migrazione. Durante la modifica delle proprietà, non è possibile modificare il **Nome set di migrazione** o **URL servizio**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### Determinazione delle dimensioni del set di migrazione e dello spazio su disco {#migration-set-size}

Dopo aver creato un set di migrazione, si consiglia vivamente di eseguire un controllo delle dimensioni del set di migrazione prima di avviare un processo di estrazione.
Eseguendo un controllo delle dimensioni del set di migrazione, potrai:
* Determinare se c&#39;è spazio su disco sufficiente nel `crx-quickstart` sottodirectory per completare l’estrazione.
* Determina se le dimensioni del set di migrazione rientrano nei limiti dei prodotti supportati ed evita l’inserimento non riuscito di contenuti.

Per eseguire un controllo delle dimensioni, effettua le seguenti operazioni:

1. Seleziona un set di migrazione e fai clic su **Dimensioni controllo**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. Verrà aperto il **Dimensioni controllo** finestra di dialogo.

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. Fai clic su **Dimensioni controllo** per avviare il processo. Tornerai quindi alla vista elenco set di migrazione e visualizzerai un messaggio che indica che **Dimensioni controllo** è in esecuzione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. Una volta **Dimensioni controllo** processo completato, lo stato verrà modificato in **COMPLETATO**. Seleziona lo stesso set di migrazione e fai clic su **Dimensioni controllo** per visualizzare i risultati.

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   Di seguito è riportato un esempio di **Dimensioni controllo** risultati senza avvisi.

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. Se la **Dimensioni controllo** i risultati indicano che lo spazio su disco è insufficiente e/o che il set di migrazione supera i limiti del prodotto, **AVVISO** verrà visualizzato lo stato .

![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

Di seguito è riportato un esempio di **Dimensioni controllo** risultati con avvisi.

![immagine](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## Novità {#whats-next}

Dopo aver imparato a creare un set di migrazione, ora puoi imparare a usare i processi di estrazione e acquisizione nello strumento Content Transfer (Trasferimento contenuti). Prima di apprendere questi processi, è necessario rivedere [Gestione di archivi di contenuti di grandi dimensioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service.
