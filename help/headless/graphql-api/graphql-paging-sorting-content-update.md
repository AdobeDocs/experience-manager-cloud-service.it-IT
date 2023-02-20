---
title: Aggiornamento dei frammenti di contenuto per la gestione delle pagine e l’ordinamento
description: Scopri come aggiornare i frammenti di contenuto per Paging e Ordinamento in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
source-git-commit: 130f653a1b0db55ea6d49a87be1215001223bf78
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 6%

---


# Aggiornamento dei frammenti di contenuto per la gestione delle pagine e l’ordinamento in GraphQL Filtering {#updating-content-fragments-for-paging-and-sorting-graphql-filtering}

Per ottimizzare le prestazioni dei filtri GraphQL, è necessario eseguire una procedura per aggiornare i frammenti di contenuto.

>[!NOTE]
>
>Dopo aver aggiornato i frammenti di contenuto, puoi seguire le raccomandazioni per [Ottimizzazione delle query GraphQL](/help/headless/graphql-api/graphql-optimization.md).


## Prerequisiti {#prerequisites}

Assicurati di disporre di un minimo della versione 2023.1.0 di AEM as a Cloud Service.

## Aggiornamento dei frammenti di contenuto {#updating-content-fragments}

Per eseguire la procedura, attenersi alla seguente procedura:

1. Abilita l’aggiornamento impostando le seguenti variabili per la tua istanza utilizzando l’interfaccia utente di Cloud Manager:

   ![Configurazione dell’ambiente Cloud Manager](assets/cfm-graphql-update-01.png "Configurazione dell’ambiente Cloud Manager")

   Le variabili disponibili sono:

   <table>
    <tbody>
     <tr>
      <th> </th>
      <th>Nome</th>
      <th>Valore</th>
      <th>Valore predefinito</th>
      <th>Servizio</th>
      <th>Applicato</th>
      <th>Tipo</th>
      <th>Note</th>
     </tr>
     <tr>
      <td>1</td>
      <td>`AEM_RELEASE_CHANNEL` </td>
      <td>`prerelease` </td>
      <td> </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Obbligatorio per abilitare la funzione. </td>
     </tr>
     <tr>
      <td>2</td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Abilita(!=0) o disabilita (0) l’attivazione del processo di migrazione dei frammenti di contenuto. </td>
     </tr>
     <tr>
      <td>3</td>
      <td>`CF_MIGRATION_ENFORCE` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Applica (!=0) Ri-migrazione dei frammenti di contenuto.<br>Impostando questo flag su 0 si esegue una migrazione incrementale di CF. Ciò significa che, se il processo viene terminato a causa di qualsiasi motivo, l'esecuzione successiva del processo avvierà la migrazione dal punto in cui è stato terminato. Si consiglia di applicare la prima migrazione (value=1). </td>
     </tr>
     <tr>
      <td>4</td>
      <td>`CF_MIGRATION_BATCH` </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Dimensione del batch per il salvataggio del numero di frammenti di contenuto dopo la migrazione.<br>Questo è pertinente al numero di CF che verranno salvati nell'archivio in un unico batch e può essere utilizzato per ottimizzare il numero di scritture nell'archivio. </td>
     </tr>
     <tr>
      <td>5</td>
      <td>`CF_MIGRATION_LIMIT` </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Numero massimo di frammenti di contenuto da elaborare alla volta.<br>Vedere anche le note per 'CF_MIGRATION_INTERVAL'. </td>
     </tr>
     <tr>
      <td>6</td>
      <td>`CF_MIGRATION_INTERVAL` </td>
      <td>`60` </td>
      <td>`600` </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Intervallo (secondi) per elaborare i frammenti di contenuto rimanenti fino al limite successivo<br>Questo intervallo viene anche considerato come un tempo di attesa prima dell'avvio del processo, così come un ritardo tra l'elaborazione di ogni successivo numero CF_MIGRATION_LIMIT di CF.<br>(*)</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >(*)
   >
   >Il valore di `CF_MIGRATION_INTERVAL` può inoltre essere utile per approssimare il tempo totale di esecuzione del processo di migrazione.
   >
   >Esempio:
   >
   >* Numero totale di frammenti di contenuto = 20.000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60 (sec)
   >* Tempo approssimativo necessario per completare la migrazione = 60 + (20.000/1000 * 60) = 1260 Sec = 21 Minutes
      >  I &quot;60&quot; secondi aggiuntivi aggiunti all&#39;inizio sono dovuti al ritardo iniziale all&#39;avvio del processo.

   >
   >È inoltre necessario tenere presente che si tratta solo della *minimo* il tempo necessario per completare il processo e non include il tempo di I/O. Il tempo reale potrebbe essere molto più di questa stima.

1. Monitora l&#39;avanzamento e il completamento dell&#39;aggiornamento.

   A questo scopo, controlla i registri sull’autore e su golden-publish da:

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * i registri dell’autore; ad esempio:

         ```shell
         23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
         ...
         23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
         
         23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
         ```
   * tronchi di pubblicazione dorata; ad esempio:

      ```shell
      23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
      
      23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
      ...
      23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
      ```


1. Disattiva la procedura di aggiornamento.

   >[!IMPORTANT]
   >
   >Questo passaggio è necessario per completare l’aggiornamento.

   Dopo l&#39;esecuzione della procedura di aggiornamento, reimposta la variabile di ambiente cloud `CF_MIGRATION_ENABLED` a &quot;0&quot;, per attivare il riciclaggio di tutti i baccelli.

   <table>
    <tbody>
     <tr>
      <th> </th>
      <th>Nome</th>
      <th>Valore</th>
      <th>Valore predefinito</th>
      <th>Servizio</th>
      <th>Applicato</th>
      <th>Tipo</th>
      <th>Note</th>
     </tr>
     <tr>
      <td></td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>Tutti i bundle  </td>
      <td> </td>
      <td>Variabile </td>
      <td>Disabilita(0) (o Abilita(!=0)) attivazione del processo di migrazione dei frammenti di contenuto. </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >Questo è particolarmente importante per il livello di pubblicazione, in quanto l’aggiornamento dei contenuti viene eseguito solo su golden-publish, e quando si ricicla i pod, tutti i normali pod di pubblicazione sono basati su golden-publish.

1. Verifica il completamento della procedura di aggiornamento.

   Puoi verificare il completamento dell’aggiornamento utilizzando il browser dell’archivio nella console per sviluppatori di Cloud Manager per controllare i dati dei frammenti di contenuto.

   * Prima della prima migrazione completa, l’ `cfGlobalVersion` la proprietà non esiste.
Pertanto, la presenza di questa proprietà, sul nodo JCR `/content/dam` con un valore di `1`, conferma il completamento della migrazione.

   * Puoi anche controllare le seguenti proprietà nei singoli frammenti di contenuto:

      * `_strucVersion` deve avere il valore di `1`
      * `indexedData` la struttura deve esistere

      >[!NOTE]
      >
      >La procedura aggiorna i frammenti di contenuto nelle istanze di authoring e pubblicazione.
      >
      >Pertanto, si raccomanda di eseguire la verifica tramite il browser del repository per *almeno* un autore *e* un&#39;istanza di pubblicazione.


## Limitazioni {#limitations}

Tieni presente le seguenti limitazioni:

* L’ottimizzazione delle prestazioni dei filtri GraphQL sarà possibile solo dopo un aggiornamento completo di tutti i frammenti di contenuto (indicato dalla presenza di `cfGlobalVersion` proprietà per il nodo JCR `/content/dam`)

* Se i frammenti di contenuto vengono importati da un pacchetto di contenuto (utilizzando `crx/de`) dopo l’esecuzione della procedura di aggiornamento, tali frammenti di contenuto non verranno considerati nei risultati della query GraphQL, fino a quando la procedura di aggiornamento non viene eseguita nuovamente.