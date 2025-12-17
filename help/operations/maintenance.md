---
title: Attività di manutenzione in AEM as a Cloud Service
description: Scopri le attività di manutenzione in AEM as a Cloud Service e come configurarle.
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: d5addc40eb48000c515b670ef5f7c7a7e8b79928
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 28%

---


# Attività di manutenzione in AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Attività di manutenzione"
>abstract="Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare l’archivio. Con AEM as a Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni di infrastruttura."

Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare l’archivio. Con AEM as a Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni di infrastruttura.

## Configurazione delle attività di manutenzione {#maintenance-tasks-configuring}

Nelle versioni precedenti di AEM, era possibile configurare le attività di manutenzione utilizzando la scheda Manutenzione (Strumenti > Operazioni > Manutenzione). In AEM as a Cloud Service la scheda di manutenzione non è più disponibile, pertanto le configurazioni devono essere salvate nel controllo sorgente e distribuite utilizzando Cloud Manager. Adobe gestisce le attività di manutenzione che presentano impostazioni non configurabili dai clienti (ad esempio, Raccolta oggetti inattivi del datastore). I clienti possono configurare altre attività di manutenzione, come descritto nella tabella seguente.

>[!CAUTION]
>
>Adobe si riserva il diritto di sovrascrivere le impostazioni di configurazione delle attività di manutenzione di un cliente per attenuare problemi come il degrado delle prestazioni.

### Attività di manutenzione {#maintenance-tasks}

Nella tabella seguente sono illustrate le attività di manutenzione disponibili.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Attività di manutenzione</th>
    <th>A chi appartiene la configurazione</th>
    <th>Come configurare (facoltativo)</th>
  </tr>  
  <tr>
    <td>Raccolta oggetti inattivi del datastore</td>
    <td>Adobe</td>
    <td>N/D: gestito completamente da Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Pulizia delle versioni</td>
    <td>Cliente</td>
    <td>L'eliminazione della versione è attualmente disabilitata per impostazione predefinita, ma è possibile configurare il criterio come descritto nella sezione <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Attività di manutenzione dell'eliminazione della versione e del log di controllo</a>.<br/><br/>La rimozione verrà presto abilitata per impostazione predefinita e tali valori potranno essere sovrascritti.<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>Elimina registro di controllo</td>
    <td>Cliente</td>
    <td>L'eliminazione del registro di controllo è attualmente disabilitata per impostazione predefinita, ma è possibile configurare il criterio come descritto nella sezione <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Attività di manutenzione dell'eliminazione della versione e del registro di controllo</a>.<br/><br/>La rimozione verrà presto abilitata per impostazione predefinita e tali valori potranno essere sovrascritti.<br>
   </td>
   </td>
  </tr>
  <tr>
    <td>Pulizia dati binari di Lucene</td>
    <td>Adobe</td>
    <td>Non utilizzato e quindi disabilitato da Adobe.</td>
  </td>
  </tr>
  <tr>
    <td>Eliminazione di attività ad hoc</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Sovrascrivere il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà nella cartella <code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> o <code>granite_monthly</code>.</p>
    <p>Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito. Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo superiore. Denominarlo <code>granite_TaskPurgeTask</code>, con l'attributo <code>sling:resourceType</code> impostato su <code>granite/operations/components/maintenance/task</code> e l'attributo <code>granite.maintenance.name</code> impostato su <code>TaskPurge</code>. Configurare le proprietà OSGI. Per l'elenco delle proprietà, vedere <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code>.</p>
  </td>
  </tr>
    <tr>
    <td>Eliminazione flussi di lavoro</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Sovrascrivere il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà nella cartella <code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> o <code>granite_monthly</code>. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito.</p>
    <p>Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo superiore (denominalo <code>granite_WorkflowPurgeTask</code>) con le proprietà opportune. Configurare le proprietà OSGI. Vedere <a href="/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances">Rimozione regolare delle istanze del flusso di lavoro</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Eliminazione progetti</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Sovrascrivere il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà nella cartella <code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> o <code>granite_monthly</code>. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito.</p>
    <p>Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo superiore (denominalo <code>granite_ProjectPurgeTask</code>) con le proprietà appropriate. Vedi l'elenco delle <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi">proprietà OSGi</a> per <b>configurazione rimozione progetti Adobe</b>.</p>
  </td>
  </tr>
  </tbody>
</table>

### Configurazioni finestre di manutenzione {#maintenance-window-configurations}

La tabella seguente illustra le configurazioni delle finestre di manutenzione disponibili.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Configurazione della finestra di manutenzione</th>
    <th>A chi appartiene la configurazione</th>
    <th>Tipo di configurazione</th>
    <th>Parametri</th>
  </tr>
  <tr>
    <td>Giornaliero</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
  <td>
  <p><strong>windowSchedule=daily</strong> (questo valore non deve essere modificato)</p>
  <p><strong>windowStartTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono iniziare l’esecuzione.</p>
  <p><strong>windowEndTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono interrompere l’esecuzione se non sono già state completate.</p>
  <p>Un'attività di manutenzione non può essere eseguita più di una volta in questo intervallo di tempo.</p>
  </td> 
  </tr>
  <tr>
    <td>Settimanale</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> (questo valore non deve essere modificato)</p>
    <p><strong>windowStartTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione settimanale devono iniziare l’esecuzione.</p>
    <p><strong>windowEndTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione settimanale devono interrompere l’esecuzione se non sono già state completate.</p>
    <p>Un'attività di manutenzione non può essere eseguita più di una volta in questo intervallo di tempo.</p>
    <p><strong>windowScheduleWeekdays= Array di due valori da 1 a 7 (ad esempio, [5,5])</strong> Il primo valore dell’array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L’ora esatta di inizio e di fine è regolata rispettivamente da windowStartTime e windowEndTime.</p>
    </td>
  </tr>
  <tr>
    <td>Mensile</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=month</strong> (questo valore non deve essere modificato)</p>
    <p><strong>windowStartTime=HH:MM</strong> utilizzando un orologio da 24 ore.  Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono iniziare l’esecuzione.</p>
    <p><strong>windowEndTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono interrompere l’esecuzione se non sono già state completate.</p>
    <p>Un'attività di manutenzione non può essere eseguita più di una volta in questo intervallo di tempo.</p>
    <p><strong>windowScheduleWeekdays=Array di due valori da 1 a 7 (ad esempio, [5,5])</strong> Il primo valore dell’array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L’ora esatta di inizio e di fine è regolata rispettivamente da windowStartTime e windowEndTime.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 per pianificare la prima settimana del mese o 1 per pianificare l’ultima settimana del mese. L'assenza di un valore consente di pianificare in modo efficace i processi nel giorno gestito da windowScheduleWeekdays (ogni mese).</p>
    </td>
    </tr>
    </tbody>
</table>

### Posizioni {#locations}

* Giornaliero: /conf/global/settings/granite/operations/maintenance/granite_daily
* Settimanale: /conf/global/settings/granite/operations/maintenance/granite_weekly
* Mensile: /conf/global/settings/granite/operations/maintenance/granite_month

### Esempi di codice {#code-samples}

**Esempio di codice 1 (giornaliero)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

**Esempio di codice 2 (settimanale)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

**Esempio di codice 3 (mensile)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

## Attività di manutenzione Pulizia delle versioni e del registro di controllo {#purge-tasks}

L’eliminazione delle versioni e del registro di audit riduce le dimensioni dell’archivio e, in alcuni scenari, può migliorare le prestazioni.

>[!NOTE]
>
>I clienti di AEM Guides non devono configurare Pulizia delle versioni.

### Impostazioni predefinite {#defaults}

Attualmente, la rimozione non è abilitata per impostazione predefinita, ma questa impostazione cambierà in futuro. Gli ambienti creati prima dell’abilitazione dell’eliminazione predefinita hanno una soglia più conservativa, in modo che l’eliminazione non avvenga in modo imprevisto. Per ulteriori dettagli sui criteri di rimozione predefiniti, consulta le sezioni seguenti Pulizia delle versioni e Pulizia del registro di controllo.
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

I valori di eliminazione predefiniti possono essere ignorati dichiarando un file di configurazione e distribuendolo come descritto di seguito.

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### Applicazione di una configurazione {#configure-purge}

Dichiara un file di configurazione e distribuiscilo come descritto nei passaggi seguenti.

>[!NOTE]
>Dopo aver distribuito il nodo di eliminazione della versione nel file di configurazione, è necessario mantenerlo dichiarato e non rimuoverlo. Se tenti di farlo, la pipeline di configurazione avrà esito negativo.
> 
>Allo stesso modo, una volta distribuito il nodo di eliminazione del registro di controllo nel file di configurazione, è necessario mantenerlo dichiarato e non rimuoverlo.

1. Creare un file denominato `mt.yaml` o simile.

1. Posizionare il file in una cartella di primo livello denominata `config` o simile, come descritto in [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure).

1. Dichiara le proprietà nel file di configurazione, tra cui:

   * alcune proprietà sopra il nodo dati. Per una descrizione, vedere [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax). Il valore della proprietà `kind` deve essere *MaintenanceTasks* e la versione deve essere *1*.

   * un oggetto dati con `versionPurge` e `auditLogPurge` oggetti.

   Vedere le definizioni e la sintassi degli oggetti `versionPurge` e `auditLogPurge`.

   Struttura la configurazione in modo simile all’esempio seguente:

   ```
   kind: "MaintenanceTasks"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     versionPurge:
       maximumVersions: 15
       maximumAgeDays: 20
       paths: ["/content"]
       minimumVersions: 1
       retainLabelledVersions: false
     auditLogPurge:
       rules:
         - replication:
             maximumAgeDays: 15
             contentPath: "/content"
             types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
         - pages:
             maximumAgeDays: 15
             contentPath: "/content"
             types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
         - dam:
             maximumAgeDays: 15
             contentPath: "/content"
             types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
   ```

   Tieni presente che affinché la configurazione sia valida:

   * tutte le proprietà devono essere definite. Non sono presenti valori predefiniti ereditati.
   * devono essere rispettati i tipi (interi, stringhe, booleani, ecc.) nelle tabelle delle proprietà sottostanti.

1. Creare una pipeline di configurazione in Cloud Manager, come descritto nell&#39;articolo [pipeline di configurazione](/help/operations/config-pipeline.md#managing-in-cloud-manager).

### Pulizia delle versioni {#version-purge}

>[!NOTE]
>
>I clienti di AEM Guides non devono configurare Pulizia delle versioni.

#### Valori predefiniti eliminazione versione {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

Attualmente, la rimozione non è abilitata per impostazione predefinita, ma questa impostazione cambierà in futuro.

Gli ambienti creati dopo l’abilitazione dell’eliminazione predefinita avranno i seguenti valori predefiniti:

* Le versioni precedenti a 30 giorni vengono rimosse.
* Sono conservate le ultime cinque versioni negli ultimi 30 giorni.
* Indipendentemente dalle regole di cui sopra, viene mantenuta la versione più recente (oltre al file corrente).

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Gli ambienti creati prima dell’attivazione dell’eliminazione predefinita presentano i valori predefiniti elencati di seguito. Tuttavia, si consiglia di ridurli per ottimizzare le prestazioni.

* Le versioni più vecchie di 7 anni vengono rimosse.
* Sono conservate tutte le versioni degli ultimi 7 anni.
* Dopo 7 anni, vengono rimosse le versioni diverse da quella più recente (oltre al file corrente).

#### Proprietà rimozione versione {#version-purge-properties}

Le proprietà consentite sono elencate di seguito.

Le colonne che indicano *default* indicano i valori predefiniti in futuro, quando verranno applicati i valori predefiniti; *TBD* riflette un ID ambiente non ancora determinato.

| Proprietà | valore predefinito futuro per envs>TBD | valore predefinito futuro per envs&lt;=TBD | obbligatorio | tipo | Valori |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| percorsi | [&quot;/content&quot;] | [&quot;/content&quot;] | Sì | array di stringhe | Specifica in quali percorsi eliminare le versioni quando vengono create nuove versioni.  I clienti devono dichiarare questa proprietà, ma l’unico valore consentito è &quot;/content&quot;. |
| maximumAgeDays | 30 | 2557 (7 anni + 2 giorni bisestili) | Sì | Numero intero | Tutte le versioni precedenti al valore configurato vengono rimosse. Se il valore è 0, la rimozione non viene eseguita in base alla data della versione. |
| maximumVersions | 5 | 0 (nessun limite) | Sì | Numero intero | Qualsiasi versione precedente alla n-esima versione più recente viene rimossa. Se il valore è 0, la rimozione non viene eseguita in base al numero di versioni. |
| minimumVersions | 1 | 1 | Sì | Numero intero | Il numero minimo di versioni mantenute indipendentemente dall’età. Tieni presente che viene sempre mantenuta almeno 1 versione; il suo valore deve essere 1 o superiore. |
| keepLabellingVersioned | false | false | Sì | booleano | Determina se le versioni con etichetta esplicita verranno escluse dalla rimozione. Per una migliore ottimizzazione dell’archivio, si consiglia di impostare questo valore su false. |

**Interazioni proprietà**

Gli esempi seguenti illustrano il modo in cui le proprietà interagiscono quando combinate.

Esempio:

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

Se al giorno 23 sono presenti 11 versioni, la versione meno recente verrà eliminata alla successiva esecuzione dell&#39;attività di manutenzione di eliminazione, poiché la proprietà `maximumVersions` è impostata su 10.

Se al giorno 31 sono presenti 5 versioni, solo 3 verranno eliminate poiché la proprietà `minimumVersions` è impostata su 2.

Esempio:

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

Non verranno eliminate versioni più recenti di 30 giorni, poiché la proprietà `maximumVersions` è impostata su 0.

Verrà conservata una versione precedente ai 30 giorni.

### Elimina registro di controllo {#audit-purge}

#### Valori predefiniti eliminazione log di controllo {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

Attualmente, la rimozione non è abilitata per impostazione predefinita, ma questa impostazione cambierà in futuro.

Gli ambienti creati dopo l’abilitazione dell’eliminazione predefinita avranno i seguenti valori predefiniti:

* I registri di replica, DAM e controllo delle pagine precedenti a 7 giorni vengono rimossi.
* Tutti gli eventi possibili vengono registrati.

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Gli ambienti creati prima dell’attivazione dell’eliminazione predefinita presentano i valori predefiniti elencati di seguito. Tuttavia, si consiglia di ridurli per ottimizzare le prestazioni.

* I registri di replica, DAM e audit delle pagine più vecchi di 7 anni vengono rimossi.
* Tutti gli eventi possibili vengono registrati.

>[!NOTE]
>Si consiglia ai clienti, che devono rispettare i requisiti normativi per la produzione di registri di audit non modificabili, di integrarsi con servizi esterni specializzati.

#### Proprietà eliminazione registro di controllo {#audit-purge-properties}

Le proprietà consentite sono elencate di seguito.

Le colonne che indicano *default* indicano i valori predefiniti in futuro, quando verranno applicati i valori predefiniti; *TBD* riflette un ID ambiente non ancora determinato.

| Proprietà | valore predefinito futuro per envs>TBD | valore predefinito futuro per envs&lt;=TBD | obbligatorio | tipo | Valori |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| regole | - | - | Sì | Oggetto | Uno o più dei seguenti nodi: replica, pagine, dam. Ciascuno di questi nodi definisce regole, con le proprietà seguenti. Tutte le proprietà devono essere dichiarate. |
| maximumAgeDays | 7 giorni | per tutti, 2557 (7 anni + 2 giorni bisestili) | Sì | intero | Per replica, pagine o dam: il numero di giorni in cui vengono conservati i registri di audit. I registri di controllo precedenti al valore configurato vengono eliminati. |
| contentPath | &quot;/content&quot; | &quot;/content&quot; | Sì | Stringa | Percorso in cui verranno eliminati i registri di audit, per il tipo correlato. Deve essere impostato su &quot;/content&quot;. |
| tipi | tutti i valori | tutti i valori | Sì | Array di enumerazione | Per **replication**, i valori enumerati sono: Activate, Deactivate, Delete, Test, Reverse, Internal Poll. Per **pagine**, i valori enumerati sono: PageCreated, PageModified, PageMoved, PageDeleted, VersionCreated, PageRestored, PageRolled Out, PageValid, PageInvalid. Per **dam**, i valori enumerati sono: ASSET_EXPIRING, METADATA_UPDATED, ASSET_EXPIRED, ASSET_REMOVED, RESTORED, ASSET_MOVE, ASSET_VIEWED, PROJECT_VIEWED, PUBLISHED_EXTERNAL, COLLECTION_VIEWED, VERSIONED, ADDED_COMMENT, RENDITION_UPDATED, ACCEPTED, DOWNLOADED, SUBASSET_UPDATED, SUBASSET_REMOVED, ASSET_CREATED, ASSET_SHARED, RENDITION_REMOVED, ASSET_PUBLISHED, ORIGINAL_UPDATED, RENDITION_DOWNLOADED, REJECTED. |
