---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: e29f70aa1a8164787c7d310a05c24d7e501803e5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 2%

---

# Connettere un modulo adattivo all’archiviazione SQL di Azure

Forms adattivo in Adobe Experience Manager (AEM) può integrarsi con database esterni per memorizzare o recuperare dati.
Questo articolo illustra come connettere un modulo adattivo a un database SQL di Azure utilizzando JDBC tramite AEM as a Cloud Service.

>
> 
> Questa guida si applica agli ambienti AEM as a Cloud Service non sandbox con rete avanzata abilitata.

## Vantaggi

L’integrazione di Adaptive Forms con Azure SQL offre diversi vantaggi:

* **Interazione dati in tempo reale:** consente la lettura e la scrittura di dati in tempo reale tra i moduli e il database di Azure.
* **Scalabilità:** Azure SQL fornisce prestazioni di database scalabili adatte alle applicazioni di livello enterprise.
* **Archiviazione dati centralizzata:** mantiene gli invii dei moduli e i dati recuperati archiviati in modo sicuro in un&#39;unica posizione centrale.
* **Conformità alla sicurezza:** sfrutta le opzioni di rete, firewall e crittografia integrate di Azure per garantire comunicazioni sicure.
* **Integrazione nativa per il cloud:** Ideale per architetture moderne basate sul cloud che utilizzano AEM as a Cloud Service.

## Prerequisiti

* Creare il [database SQL di Azure](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal) e verificare che la **connessione proxy** sia abilitata.

  >[!NOTE]
  >
  > Passare a: `Azure Portal → SQL Server → Security → Networking → Connectivity` per abilitare **connessione proxy**.

  ![Crea database di Azure](/help/forms/assets/create-azure-db.png)

* Abilita [Rete avanzata configurata utilizzando un IP in uscita dedicato](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address) per il database di Azure creato.

  >[!NOTE]
  >
  >    Dopo aver abilitato l’IP in uscita dedicato. Vai a `Azure Portal → SQL Server → Security → Networking → Public Access` e aggiungi l&#39;IP in uscita alle regole del firewall.

  ![IP in uscita](/help/forms/assets/cretae-azure-db-egress-ip.png)

* Imposta l’inoltro delle porte nell’ambiente cloud con:
   * **portOrigin**: tra `30000–30999`
   * **portDest**: `1433` (porta predefinita per SQL di Azure)
Esempio: `portOrigin: 30433 → portDest: 1433`

     >
     > 
     > Per configurare l’inoltro porta, contatta il supporto Cloud Manager di Adobe.


## Passaggi per connettere Forms adattivo a SQL di Azure

**Passaggio1: clonare l&#39;archivio Git AEM as a Cloud Service**

1. Aprire la riga di comando e scegliere una directory in cui archiviare l&#39;archivio AEM as a Cloud Service, ad esempio `/cloud-service-repository/`.

1. Esegui il comando seguente per clonare l’archivio:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Dove trovare queste informazioni?**

   Per istruzioni dettagliate su come individuare questi dettagli, consulta l&#39;articolo di Adobe Experience League &quot;[Accesso a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot;.

   Al termine del comando viene visualizzata una nuova cartella creata nella directory locale. Questa cartella prende il nome dall&#39;applicazione.

1. Apri la cartella dell’archivio in un editor.

**Passaggio2: Aggiungi JAR richiesti**

Includere la [dipendenza del driver SQL](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true) nel progetto AEM tramite il pacchetto `all`.:

>[!NOTE]
>
> Per includere la dipendenza SQL nel progetto, fare riferimento alla sezione [Dipendenze driver SQL](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies).

**Passaggio 3: aggiunta della configurazione JDBC**

1. Passa alla seguente directory all&#39;interno di `<application folder>` in cui deve essere posizionata la configurazione OSGi per il pool JDBC:

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**Passaggio 4: creare il file di configurazione della connessione SQL di Azure**

1. Crea il file:

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. Aggiungi le seguenti righe di codice:

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   >
   >
   > Sostituisci `jdbc.username` con il nome utente di Azure effettivo e `jdbc.password` con la password sicura effettiva.

**Passaggio 5: conferma e invia le modifiche**

Apri il terminale ed esegui i seguenti comandi:

```bash
git add .
git commit -m "<commit message>"
git push 
```

**Passaggio 6: distribuire le modifiche tramite pipeline Cloud Manager**

1. Accedi a **AEM Cloud Manager**.
1. Passa al progetto ed esegui la pipeline per distribuire le modifiche.

**Passaggio 7: creare un modello dati modulo (FDM)**

Una volta completata l’installazione di AEM e Azure e distribuite le modifiche al codice:

1. Passa all’istanza Autore AEM.
1. Passa a **Strumenti** > **Forms** > **Integrazioni dati**.
1. Crea nuovo **modello dati modulo**.
1. Nella scheda **Origini dati** selezionare la configurazione JDBC creata.
1. Fai clic su **[!UICONTROL Crea]** e verifica la connessione.

![Crea modello dati modulo](/help/forms/assets/create-azure-sql-fdm.png)

**Passaggio 8: utilizzare l&#39;FDM creato in un modulo adattivo**

1. Apri un modulo adattivo in modalità di modifica.
1. Selezionate l&#39;FDM creato nel passo precedente come modello dati.
1. Utilizzare [associazioni dati per connettere i campi modulo con l&#39;origine dati SQL di Azure](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services) e configurare l&#39;azione di invio.

## Best practice

* Utilizza **gestione segreti** per evitare password hardcoding nei file di configurazione.
* Ruota regolarmente le credenziali del database e aggiorna la configurazione in modo sicuro.
* Monitora i registri di connettività JDBC per individuare errori e latenza.
* Segui le best practice di Azure per proteggere i database SQL e le configurazioni del firewall.
* Evitare di utilizzare account di database con privilegi elevati per l&#39;accesso ai moduli.

## Articoli correlati

{{af-submit-action}}