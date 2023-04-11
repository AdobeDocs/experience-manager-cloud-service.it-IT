---
title: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
description: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 22%

---

# Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti) {#getting-started-content-transfer-tool}


## Disponibilità {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Scarica"
>abstract="Lo strumento di trasferimento dei contenuti può essere scaricato come file zip dal portale di distribuzione di software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it" text="Note sulla versione"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html" text="Portale di distribuzione di software"

Lo strumento di trasferimento dei contenuti può essere scaricato come file zip dal portale di distribuzione di software. Puoi installare il pacchetto tramite [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) sull’istanza Adobe Experience Manager (AEM) sorgente. Assicurati di scaricare la versione più recente. Per ulteriori dettagli sull’ultima versione, consulta [Note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

Sarà supportata solo la versione 2.0.0 o successiva ed è consigliabile utilizzare la versione più recente.

>[!NOTE]
>Scarica lo strumento Content Transfer (Trasferimento contenuti) dal portale di [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Connettività ambiente sorgente {#source-environment-connectivity}

>[!NOTE]
>
>Un errore di connessione può verificarsi anche se un set di migrazione è stato eliminato da Cloud Acceleration Manager.

L’istanza di origine AEM può essere in esecuzione dietro un firewall in cui può raggiungere solo alcuni host aggiunti a un Elenco consentiti. Per eseguire correttamente un’estrazione, i seguenti endpoint devono essere accessibili dall’istanza in esecuzione AEM:

* Servizio di archiviazione BLOB di Azure: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Se l’estrazione non riesce a causa del seguente errore: &quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: Creazione percorso PKIX non riuscita: sun.security.provider.certpath.SunCertPathBuilderException: impossibile trovare un percorso di certificazione valido per la destinazione richiesta&quot;, è possibile risolvere il problema importando il certificato CA pertinente.

### Abilita registrazione SSL {#enable-ssl-logging}

A volte può essere difficile comprendere i problemi di connessione SSL/TLS. Per risolvere i problemi di connessione durante un processo di estrazione, puoi abilitare la registrazione SSL tramite la console di sistema dell’ambiente AEM sorgente seguendo questi passaggi:

1. Passa alla console Web di Adobe Experience Manager nell’istanza sorgente, scegliendo **Strumenti - Operazioni - Console web** o direttamente all’URL in *https://serveraddress:serverport/system/console/configMgr*
1. Cerca **Configurazione del servizio di estrazione dello strumento Content Transfer (Trasferimento contenuti)**
1. Utilizza il pulsante icona a forma di matita per modificarne i valori di configurazione
1. Abilita la **Abilita la registrazione ssl per l’estrazione** premere **Salva**:

   ![immagine](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## Esecuzione dello strumento Content Transfer (Trasferimento contenuti)  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Strumento di trasferimento dei contenuti in esecuzione"
>abstract="Scopri come utilizzare lo strumento di trasferimento dei contenuti per migrare i contenuti a AEM as a Cloud Service (authoring/pubblicazione)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Vedi demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=it#migration" text="Tutorial: utilizzo dello strumento di trasferimento dei contenuti"

La sezione seguente si applica alla nuova versione dello strumento Content Transfer (Trasferimento contenuti). Leggi questa sezione per scoprire come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto in AEM as a Cloud Service:

### Estrazione fase di configurazione {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Estrazione fase di configurazione"
>abstract="Scopri come creare e gestire un set di migrazione e come copiare la chiave di estrazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=it#migration" text="Tutorial: utilizzo dello strumento di trasferimento dei contenuti"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. Accedi a Cloud Acceleration Manager (CAM) e fai clic sul progetto CAM creato in precedenza per valutare la tua disponibilità a passare a AEM as a Cloud Service. Se non hai creato un progetto CAM, consulta Creazione e gestione di un progetto in CAM.

1. Fai clic sul pulsante **Trasferimento dei contenuti** il Card. Viene visualizzata la vista Elenco set di migrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Crea un set di migrazione facendo clic su **Crea set di migrazione**.

   >[!NOTE]
   >
   >In Cloud Acceleration Manager è possibile creare un massimo di cinque set di migrazione, compresi i set scaduti, per progetto.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   Verrà visualizzata la seguente finestra di dialogo. Un set di migrazione scadrà dopo un periodo prolungato di inattività. Dopo aver visualizzato gli avvisi sulla scheda del progetto e sulle righe della tabella dei processi di migrazione per un periodo di tempo, il set di migrazione scadrà e i relativi dati non saranno più disponibili. Revisione [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. Ora puoi visualizzare l’elenco delle migrazioni nella vista a elenco. Fai clic sul simbolo dei tre punti (**...**) per aprire il menu a discesa e fare clic su **Copia chiave di estrazione**. Questa chiave sarà necessaria durante la fase di estrazione. Copia questa chiave di estrazione.

   >[!NOTE]
   >
   >La chiave di estrazione consente all’ambiente AEM sorgente di connettersi in modo sicuro al set di migrazione. Tratta questa chiave con la stessa attenzione che vorresti avere una password e non condividerla mai su un supporto non protetto come e-mail.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Popolamento del set di migrazione {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Popolare il set di migrazione"
>abstract="Dopo aver creato un set di migrazione, questo deve essere popolato con i contenuti dell’istanza di origine che devono essere spostati nell’ambiente AEM as a Cloud Service. A questo scopo, è necessario installare lo strumento di trasferimento dei contenuti nell’istanza di origine."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=it" text="Estrazione dei contenuti"

Per popolare il set di migrazione creato in Cloud Acceleration Manager, devi installare la versione più recente dello strumento Content Transfer (Trasferimento contenuti) sull’istanza Adobe Experience Manager (AEM) sorgente. Leggi questa sezione per scoprire come compilare il set di migrazione.

1. Dopo aver installato la versione più recente dello strumento Content Transfer (Trasferimento contenuti) sull’istanza Adobe Experience Manager sorgente, vai a **Operazioni - Migrazione dei contenuti**

1. Fai clic su **Crea set di migrazione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Incolla la chiave di estrazione copiata da CAM in precedenza nel campo di input della chiave di estrazione di **Crea set di migrazione** modulo. In questo modo, i campi Nome set di migrazione e Nome progetto Cloud Acceleration Manager (CAM) verranno compilati automaticamente. Devono corrispondere al nome del set di migrazione in CAM e al nome del progetto CAM creato. È ora possibile aggiungere percorsi di contenuto. Dopo aver aggiunto i percorsi dei contenuti, potrai salvare il set di migrazione. Puoi eseguire l’estrazione con versioni incluse o escluse.

   >[!NOTE]
   >
   >Assicurati che la chiave di estrazione sia valida e non sia vicina alla sua scadenza. Puoi ottenere queste informazioni nel **Crea set di migrazione** dopo aver incollato la chiave di estrazione. Se ricevi un errore di connessione, fai riferimento a [Connettività ambiente sorgente](#source-environment-connectivity) per ulteriori informazioni.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. Quindi, seleziona i seguenti parametri per creare un set di migrazione:

   1. **Include Version** (Includi versione): seleziona in base alle esigenze. Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per la migrazione degli eventi di controllo.

      ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

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

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Determinazione delle dimensioni del set di migrazione {#migration-set-size}

Dopo aver creato un set di migrazione, si consiglia vivamente di eseguire un controllo delle dimensioni del set di migrazione prima di avviare un processo di estrazione.
Eseguendo un controllo delle dimensioni del set di migrazione, potrai:
* Determinare se c&#39;è spazio su disco sufficiente nel `crx-quickstart` sottodirectory per completare l’estrazione.
* Determina se le dimensioni del set di migrazione rientrano nei limiti dei prodotti supportati ed evita l’inserimento non riuscito di contenuti.

Per eseguire un controllo delle dimensioni, effettua le seguenti operazioni:

1. Seleziona un set di migrazione e fai clic su **Dimensioni controllo**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Verrà aperto il **Dimensioni controllo** finestra di dialogo.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. Fai clic su **Dimensioni controllo** per avviare il processo. Tornerai quindi alla vista elenco set di migrazione e visualizzerai un messaggio che indica che **Dimensioni controllo** è in esecuzione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Una volta **Dimensioni controllo** processo completato, lo stato verrà modificato in **COMPLETATO**. Seleziona lo stesso set di migrazione e fai clic su **Dimensioni controllo** per visualizzare i risultati. Di seguito è riportato un esempio di **Dimensioni controllo** risultati senza avvisi.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. Se la **Dimensioni controllo** i risultati indicano che lo spazio su disco è insufficiente e/o che il set di migrazione supera i limiti del prodotto, **AVVISO** verrà visualizzato lo stato .

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## Passaggio successivo {#whats-next}

Dopo aver imparato a creare un set di migrazione, ora puoi imparare a usare i processi di estrazione e acquisizione nello strumento Content Transfer (Trasferimento contenuti). Prima di apprendere questi processi, è necessario rivedere [Gestione di archivi di contenuti di grandi dimensioni](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service.
