---
title: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
description: Scopri come iniziare a utilizzare lo strumento Content Transfer (Trasferimento contenuti)
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 14%

---


# Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti) {#getting-started-content-transfer-tool}


## Disponibilità {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Scarica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza di origine di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=it" text="Note sulla versione"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html" text="Portale di distribuzione software"

Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) nell&#39;istanza Adobe Experience Manager (AEM) di origine. Assicurati di scaricare la versione più recente. Per ulteriori dettagli sull&#39;ultima versione, vedere [Note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=it).

È supportata solo la versione 2.0.0 o successiva ed è consigliabile utilizzare la versione più recente.

>[!NOTE]
>Scarica lo strumento Content Transfer (Trasferimento contenuti) dal portale di [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Connettività dell’ambiente Source {#source-environment-connectivity}

>[!NOTE]
>
>Se un set di migrazione è stato eliminato da Cloud Acceleration Manager, può verificarsi anche un errore di connessione.

L’istanza AEM di origine potrebbe essere in esecuzione dietro un firewall e raggiungere solo alcuni host aggiunti a un Elenco consentiti. Per eseguire correttamente un’estrazione, i seguenti endpoint devono essere accessibili dall’istanza che esegue AEM:

* Servizio di archiviazione BLOB di Azure: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Se l&#39;estrazione non riesce a causa del seguente errore: &quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: generazione del percorso PKIX non riuscita: sun.security.provider.certpath.SunCertPathBuilderException: impossibile trovare un percorso di certificazione valido per la destinazione richiesta&quot;, è possibile risolvere il problema importando il certificato CA pertinente.

### Abilita registrazione SSL {#enable-ssl-logging}

Talvolta può essere difficile comprendere i problemi di connessione SSL/TLS. Per risolvere i problemi di connessione durante un processo di estrazione, puoi abilitare la registrazione SSL tramite la console di sistema dell’ambiente AEM sorgente seguendo la procedura riportata di seguito:

1. Passa alla console Web Adobe Experience Manager nell&#39;istanza di origine, da **Strumenti > Operazioni > Console Web** oppure direttamente all&#39;URL in *https://serveraddress:serverport/system/console/configMgr*
1. Cerca la **configurazione del servizio di estrazione dello strumento Content Transfer**
1. Utilizza il pulsante di icona della matita per modificarne i valori di configurazione
1. Abilita l&#39;impostazione **Abilita registrazione SSL per l&#39;estrazione**, quindi premi **Salva**:

   ![immagine](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>
>Questo flag è solo per il debug di problemi SSL. Assicurati che il flag sia disabilitato prima di eseguire l’estrazione, in quanto potrebbe richiedere una grande quantità di spazio su disco. Questo potrebbe potenzialmente riempire la capacità dell’unità e causare un errore nel processo di estrazione.

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti) {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Esecuzione dello strumento Content Transfer"
>abstract="Scopri come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti in AEM as a Cloud Service (authoring/pubblicazione)."
>additional-url="https://video.tv.adobe.com/v/327073/?quality=12&learn=on&captions=ita" text=" Guarda la dimostrazione"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=it#migration" text="Tutorial - Utilizzo dello strumento Content Transfer"

La sezione seguente si applica alla nuova versione dello strumento Content Transfer (Trasferimento contenuti). Leggi questa sezione per scoprire come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti ad AEM as a Cloud Service:

### Fase di configurazione dell’estrazione {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Fase di configurazione dell’estrazione"
>abstract="Scopri come creare e gestire un set di migrazione e come copiare la chiave di estrazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=it#migration" text="Tutorial - Utilizzo dello strumento Content Transfer"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Accedi a Cloud Acceleration Manager (CAM) e fai clic sul progetto CAM creato in precedenza per valutare se sei pronto a passare ad AEM as a Cloud Service. Se non avete creato un progetto CAM, consultate Creazione e gestione di un progetto in CAM.

1. Fai clic sulla scheda **Content Transfer** per aprire la visualizzazione Elenco set di migrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Creare un set di migrazione facendo clic su **Crea set di migrazione**.

   >[!NOTE]
   >
   >In Cloud Acceleration Manager è possibile creare un massimo di 10 set di migrazione, inclusi i set scaduti.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   Viene visualizzata la seguente finestra di dialogo. Tieni presente che un set di migrazione scadrà dopo un periodo prolungato di inattività. Dopo aver visualizzato gli avvisi sulla scheda del progetto e sulle righe della tabella del processo di migrazione per un periodo di tempo, il set di migrazione scadrà e i relativi dati non saranno più disponibili. Rivedi [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.

   Durante la creazione del set di migrazione è possibile scegliere l’area geografica in cui verranno memorizzati i dati di migrazione temporanea.  È consigliabile scegliere l’area più vicina all’ambiente cloud di destinazione per garantire prestazioni ottimali durante le acquisizioni.  Non è possibile modificare l’area geografica dopo la creazione del set di migrazione; per utilizzare un’area diversa è necessario creare un nuovo set di migrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >Il nome deve seguire le stesse convenzioni di un nodo AEM, pertanto non può contenere i seguenti caratteri: `. / : [ ] | * < > ^ ? { } % # ` né simboli o emoticon insoliti.

1. Ora l’elenco delle migrazioni dovrebbe essere visualizzato nella vista a elenco. Selezionare il simbolo dei tre punti (**...**) per aprire il menu a discesa e selezionare **Copia chiave di estrazione**. Questa chiave è necessaria durante la fase di estrazione. Copia questa chiave di estrazione.

   >[!NOTE]
   >
   >La chiave di estrazione consente all’ambiente AEM di origine di connettersi in modo sicuro al set di migrazione. Tratta questa chiave con la stessa attenzione con cui useresti una password e non condividerla mai tramite un mezzo non sicuro come l’e-mail.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Popolamento del set di migrazione {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Popolare un set di migrazione"
>abstract="Dopo aver creato un set di migrazione, questo deve essere popolato con il contenuto dell’istanza di origine da spostare nell’ambiente AEM as a Cloud Service. A questo scopo, è necessario installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di origine."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=it" text="Estrazione del contenuto"

Per popolare il set di migrazione creato in Cloud Acceleration Manager, installa la versione più recente dello strumento Content Transfer nell’istanza Adobe Experience Manager (AEM) di origine. Per informazioni su come popolare il set di migrazione, consulta questa sezione.

1. Dopo aver installato la versione più recente dello strumento Content Transfer (Trasferimento contenuti) nell&#39;istanza Adobe Experience Manager di origine, passa a **Operazioni - Migrazione contenuti**

1. Fare clic su **Crea set di migrazione**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Incolla la chiave di estrazione copiata in precedenza da CAM nel campo di input della chiave di estrazione del modulo **Crea set di migrazione**. Dopo aver eseguito questa operazione, i campi Nome set di migrazione e Nome progetto Cloud Acceleration Manager (CAM) vengono compilati automaticamente. Questi devono corrispondere al nome del Set di migrazione in CAM e al nome del progetto CAM creato. Ora puoi aggiungere percorsi di contenuto. Dopo aver aggiunto i percorsi dei contenuti, salva il set di migrazione. Puoi eseguire l’estrazione con le versioni incluse o escluse.

   >[!NOTE]
   >
   >Assicurati che la chiave di estrazione sia valida e non vicina alla scadenza. Puoi ottenere queste informazioni nella finestra di dialogo **Crea set di migrazione** dopo aver incollato la chiave di estrazione. Se si verifica un errore di connessione, vedere [Connettività ambiente Source](#source-environment-connectivity) per ulteriori informazioni.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/createMigrationSet.png)

1. Quindi, seleziona i seguenti parametri per creare un set di migrazione:

   1. **Includi versione**: seleziona in base alle esigenze. Quando sono incluse le versioni, il percorso `/var/audit` viene incluso automaticamente per migrare gli eventi di controllo.

      ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/includeVersion.png)

      >[!NOTE]
      >Se si desidera includere le versioni come parte di un set di migrazione e si stanno eseguendo integrazioni con `wipe=false`, è necessario disabilitare la rimozione delle versioni a causa di una limitazione corrente nello strumento Content Transfer (Trasferimento contenuti). Se preferisci mantenere abilitata l’eliminazione delle versioni e stai eseguendo integrazioni in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.

      >[!NOTE]
      >A partire dalla versione CTT (3.0.24), sono state incluse nuove funzioni nello strumento Content Transfer (Trasferimento contenuti), che migliorano il processo di inclusione e esclusione dei percorsi. In precedenza, i percorsi dovevano essere selezionati singolarmente, operazione noiosa e dispendiosa in termini di tempo. Ora gli utenti possono includere percorsi direttamente dall’interfaccia utente o caricare un file CSV in base alle loro preferenze.  Il file CSV deve avere un percorso per riga e nessuna virgola.

   1. **Percorsi da includere**: utilizzare il browser percorsi per selezionare i percorsi da migrare. Il selettore di percorsi accetta l’input digitando o selezionando. Gli utenti possono selezionare una sola opzione per l’inclusione dei percorsi: dall’interfaccia utente o caricando un file CSV.
      >[!IMPORTANT]
      >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (alcuni percorsi `/etc` possono essere selezionati in CTT)

      ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/includeAndExcludePath.png)

      1. È consentita solo la selezione del percorso e deve essere presente almeno un percorso. Se non viene selezionato alcun percorso, si verificherà un errore del server.

         ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ServerError.png)

      1. Quando si utilizza l&#39;opzione di caricamento **CSV**, il file CSV deve contenere percorsi validi.

         ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/validCsvUpload.png)

      1. Per tornare al selettore dei percorsi, gli utenti devono aggiornare la pagina e ricominciare.

      1. Se nel file CSV caricato vengono trovati **percorsi non validi**, in una finestra di dialogo separata verranno visualizzati i percorsi non validi.

         ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/invalidPathsInCsv.png)

      1. Gli utenti devono correggere il file CSV e caricarlo nuovamente oppure aggiornare l’interfaccia utente per selezionare i percorsi tramite il selettore dei percorsi.

   1. **Percorsi da escludere**: una nuova funzionalità consente agli utenti di escludere percorsi specifici se non desiderano includerli. Ad esempio, se il percorso nella sezione include è /content/dam, gli utenti possono ora escludere percorsi come /content/dam/catalogs.

      ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/excludePathHighlighted.png)

1. Fai clic su **Salva** dopo aver compilato tutti i campi nella schermata dei dettagli **Crea set di migrazione**.

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Determinazione delle dimensioni del set di migrazione {#migration-set-size}

Dopo aver creato un set di migrazione, si consiglia vivamente di eseguire un controllo delle dimensioni del set di migrazione prima di avviare un processo di estrazione.
Eseguendo un controllo delle dimensioni sul set di migrazione, è possibile:

* Determinare se lo spazio su disco nella sottodirectory `crx-quickstart` è sufficiente per completare l&#39;estrazione.
* Determina se le dimensioni del set di migrazione rientrano nei limiti dei prodotti supportati ed evita l’acquisizione di contenuti non riuscita.

Per eseguire un controllo delle dimensioni, attenersi alla procedura descritta di seguito.

1. Selezionare un set di migrazione e fare clic su **Verifica dimensioni**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Verrà aperta la finestra di dialogo **Verifica dimensioni**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/checkMigrationSetSize.png)

1. Fare clic su **Verifica dimensioni** per avviare il processo. Si tornerà quindi alla visualizzazione elenco dei set di migrazione e si dovrebbe visualizzare un messaggio che indica che **Verifica dimensione** è in esecuzione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Al termine del processo di **Verifica dimensioni**, lo stato diventa **COMPLETATO**. Selezionare lo stesso set di migrazione e fare clic su **Verifica dimensioni** per visualizzare i risultati. Di seguito è riportato un esempio di **risultati del controllo dimensioni** senza avvisi.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/checkSizeAfterFinished.png)

1. Se i risultati del controllo di **Dimensione** indicano che lo spazio su disco è insufficiente o che il set di migrazione supera i limiti del prodotto o entrambi, verrà visualizzato uno stato **AVVISO**.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## Passaggio successivo {#whats-next}

Dopo aver appreso come creare un set di migrazione, puoi iniziare a conoscere i processi di estrazione e acquisizione dallo strumento Content Transfer (Trasferimento contenuti). Prima di apprendere questi processi, è necessario rivedere [Gestione di archivi di contenuti di grandi dimensioni](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) per velocizzare in modo significativo le fasi di estrazione e acquisizione dell&#39;attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service.
