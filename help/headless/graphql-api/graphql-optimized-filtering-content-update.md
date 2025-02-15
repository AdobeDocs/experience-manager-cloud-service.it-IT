---
title: Aggiornamento dei frammenti di contenuto per un filtro GraphQL ottimizzato
description: Scopri come aggiornare i frammenti di contenuto per il filtro GraphQL ottimizzato in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 8d14936ad21dc5879c72383defc3db22ce9a24ef
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 57%

---

# Aggiornamento dei frammenti di contenuto per un filtro GraphQL ottimizzato {#updating-content-fragments-for-optimized-graphql-filtering}

Per ottimizzare le prestazioni dei filtri di GraphQL, esegui una procedura per aggiornare i frammenti di contenuto.

>[!NOTE]
>
>Dopo aver aggiornato i frammenti di contenuto, puoi seguire i consigli per [Ottimizzare le query GraphQL](/help/headless/graphql-api/graphql-optimization.md).


## Prerequisiti {#prerequisites}

Questa attività presenta i seguenti prerequisiti:

1. Assicurati di disporre almeno della versione 2023.1.0 di AEM as a Cloud Service.

1. Assicurati che l’utente che esegue l’attività disponga delle autorizzazioni necessarie:

   * come minimo, è necessario il ruolo `Deployment Manager` in Cloud Manager.

## Aggiornamento dei frammenti di contenuto {#updating-content-fragments}

1. Abilita l’aggiornamento impostando le seguenti variabili per l’istanza tramite l’interfaccia utente di Cloud Manager:

   ![Configurazione ambiente Cloud Manager](assets/cfm-graphql-update-01.png "Configurazione ambiente Cloud Manager")

   Le variabili disponibili sono:

   | | Nome | Valore | Valore predefinito | Servizio | Applicato | Tipo | Note |
   |---|---|---|---|---|---|---|---|
   | 1 | `CF_MIGRATION_ENABLED` | `1` | `0` | Tutti i bundle  | | Variabile | Abilita (!=0) o disabilita (0) l’attivazione del processo di migrazione dei frammenti di contenuto. |
   | 2 | `CF_MIGRATION_ENFORCE` | `1` | `0` | Tutti i bundle  | | Variabile | Applica (!=0) migrazione di frammenti di contenuto. Se si imposta questo flag su 0, viene eseguita una migrazione incrementale dei CF. Ciò significa che, se il processo viene terminato per qualsiasi motivo, la successiva esecuzione del processo inizia la migrazione dal punto in cui è stato terminato. Si consiglia di eseguire la prima migrazione per l’applicazione (valore=1). |
   | 3 | `CF_MIGRATION_BATCH` | `50` | `50` | Tutti i bundle  | | Variabile | Dimensione del batch per il salvataggio del numero di frammenti di contenuto dopo la migrazione. Questo è rilevante per il numero di CF salvati nell’archivio in un batch e può essere utilizzato per ottimizzare il numero di scritture nell’archivio. |
   | 4 | `CF_MIGRATION_LIMIT` | `1000` | `1000` | Tutti i bundle  | | Variabile | Numero massimo di frammenti di contenuto da elaborare alla volta. Vedere anche le note per `CF_MIGRATION_INTERVAL`. |
   | 5 | `CF_MIGRATION_INTERVAL` | `60` | `600` | Tutti i bundle  | | Variabile | Intervallo (secondi) per elaborare i frammenti di contenuto rimanenti fino al limite successivo. Questo intervallo viene anche considerato come un tempo di attesa prima di avviare il processo e un ritardo tra l&#39;elaborazione di ogni successivo numero di CF CF CF_MIGRATION_LIMIT. (*) |

   >[!NOTE]
   >
   >(*)
   >
   >Il valore di `CF_MIGRATION_INTERVAL` può inoltre essere utile per approssimare il tempo totale di esecuzione del processo di migrazione.
   >
   >Esempio:
   >
   >* Numero totale frammenti di contenuto = 20.000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60 (sec)
   >* Tempo approssimativo necessario per completare la migrazione = 60 + (20.000/1000 * 60) = 1260 sec = 21 minuti
   >  I “60” secondi aggiuntivi aggiunti all’avvio sono dovuti al ritardo iniziale all’avvio del processo.
   >
   >Tempo *minimo* necessario per completare il processo. Non è incluso il tempo di I/O. Il tempo effettivamente impiegato potrebbe essere superiore a questa stima.

1. Monitora l’avanzamento e il completamento dell’aggiornamento.

   A questo scopo, controlla i registri sull’authoring e la pubblicazione in gold da:

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * Registri di authoring; ad esempio:

        ```shell
        23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
        ...
        23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        
        23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

      * Registri di pubblicazione in gold; ad esempio:

        ```shell
        23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
        
        23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        ...
        23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

   I clienti che hanno abilitato l’accesso ai registri dell’ambiente utilizzando Splunk possono utilizzare la query di esempio riportata di seguito per monitorare il processo di aggiornamento. Per informazioni dettagliate sull&#39;abilitazione della registrazione Splunk, vedere [Debug di produzione e staging](/help/implementing/developing/introduction/logging.md#debugging-production-and-stage).

   ```splunk
   index=<indexName> sourcetype=aemerror aem_envId=<environmentId> msg="*com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished*" 
   (aem_tier=golden-publish OR aem_tier=author) | table _time aem_tier pod_name msg | sort -_time desc
   ```

   Dove:

   * `environmentId` - identificatore dell’ambiente del cliente; ad esempio, `e1234`
   * `indexName` - nome di indice del cliente, per la raccolta di eventi `aemerror`

   Esempio di output:

   <table style="table-layout:auto">
     <thead>
       <tr>
       <th>_time</th>
       <th>aem_tier</th>
       <th>pod_name</th>
       <th>msg</th>
       </tr>
     </thead> 
     <tbody>
       <tr>
         <td>2023-04-21 06:00:35.723</td>
         <td>author</td>
         <td>cm-p1234-e1234-aem-author-76d6dc4b79-8lsb5</td>
         <td>[sling-threadpool-bb5da4dd-6b05-4230-93ea-1d5cd242e24f-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 391m, slingJobId: 2023/4/20/23/16/db7963df-e267-489b-b69a-5930b0dadb37_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=36756, failedCount=0, skippedCount=0}</td>
       </tr>
       <tr>
         <td>2023-04-21 06:05:48.207</td>
         <td>golden-publish</td>
         <td>cm-p1234-e1234-aem-golden-publish-644487c9c5-lvkv2</td>
         <td>[sling-threadpool-284b9a9a-8454-461e-9bdb-44866c6ddfb1-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 211m, slingJobId: 2023/4/20/23/15/66c1690a-cdb7-4e66-bc52-90f33394ddfc_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=19557, failedCount=0, skippedCount=0}</td>
       </tr>
     </tbody>
   <table>

1. Disattiva la procedura di aggiornamento.

   >[!IMPORTANT]
   >
   >Questo passaggio è necessario per completare l’aggiornamento.

   Al termine della procedura di aggiornamento, reimposta la variabile di ambiente cloud `CF_MIGRATION_ENABLED` a “0”, per attivare il riutilizzo di tutti i pod.

   | | Nome | Valore | Valore predefinito | Servizio | Applicato | Tipo | Note |
   |---|---|---|---|---|---|---|---|
   | | `CF_MIGRATION_ENABLED` | `0` | `0` | Tutti i bundle  | | Variabile | Disabilita(0) (o Abilita(!=0)) attivazione del processo di migrazione dei frammenti di contenuto. |

   >[!NOTE]
   >
   >Questo è importante per il livello di pubblicazione, in quanto l’aggiornamento del contenuto viene eseguito solo su golden-publish e, quando si ricicla il pod, tutti i normali pod di pubblicazione si basano su golden-publish.

1. Verificare il completamento della procedura di aggiornamento.

   Puoi verificare il completamento corretto dell’aggiornamento utilizzando il browser dell’archivio nella Console per sviluppatori di Cloud Manager dove puoi controllare i dati dei frammenti di contenuto.

   * Prima della prima migrazione completa, la proprietà `cfGlobalVersion` non esiste.
Pertanto, la presenza di questa proprietà sul nodo JCR `/content/dam` con un valore di `1` conferma il completamento della migrazione.

   * Puoi anche controllare le seguenti proprietà sui singoli frammenti di contenuto:

      * `_strucVersion` deve avere il valore di `1`
      * La struttura `indexedData` deve esistere

     >[!NOTE]
     >
     >La procedura aggiorna i frammenti di contenuto nelle istanze Autore e Publish.
     >
     >Pertanto, Adobe consiglia di eseguire la verifica tramite il browser del repository per *almeno* un autore *e* un&#39;istanza di Publish.

## Limitazioni {#limitations}

Tieni presente le seguenti limitazioni:

* L&#39;ottimizzazione delle prestazioni dei filtri GraphQL è possibile solo dopo un aggiornamento completo di tutti i frammenti di contenuto (indicato dalla presenza della proprietà `cfGlobalVersion` per il nodo JCR `/content/dam`)

* Se i frammenti di contenuto vengono importati da un pacchetto di contenuto (utilizzando `crx/de`) dopo l&#39;esecuzione della procedura di aggiornamento, tali frammenti di contenuto non vengono considerati nei risultati della query GraphQL fino a quando la procedura di aggiornamento non viene eseguita nuovamente.
