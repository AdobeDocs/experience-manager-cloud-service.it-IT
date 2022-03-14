---
title: Attività di manutenzione in AEM as a Cloud Service
description: Attività di manutenzione in AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 6af0a140005bcc684c72151024affb117437f6ce
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 4%

---

# Attività di manutenzione in AEM as a Cloud Service

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Attività di manutenzione"
>abstract="Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare il repository. Con AEM as a Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni dell&#39;infrastruttura."

Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare il repository. Con AEM as a Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni dell&#39;infrastruttura.

## Configurazione delle attività di manutenzione

Nelle versioni precedenti di AEM, è possibile configurare le attività di manutenzione utilizzando la scheda Manutenzione (Strumenti > Operazioni > Manutenzione). Per AEM as a Cloud Service, la scheda di manutenzione non è più disponibile, pertanto le configurazioni devono essere salvate nel controllo del codice sorgente e distribuite utilizzando Cloud Manager. Adobe gestisce le attività di manutenzione che presentano impostazioni non configurabili dai clienti (ad esempio, Raccolta rifiuti del datastore, Eliminazione del log di controllo, Pulizia delle versioni). I clienti possono configurare altre attività di manutenzione, come descritto nella tabella seguente.

>[!CAUTION]
>
>Adobe si riserva il diritto di ignorare le impostazioni di configurazione di un&#39;attività di manutenzione del cliente per attenuare problemi come il degrado delle prestazioni.

Nella tabella seguente sono illustrate le attività di manutenzione disponibili al momento del rilascio di AEM as a Cloud Service.

<!--| Maintenance Task | Who owns the configuration | How to configure (optional)  |
|---|---|---|
| Datastore garbage collection | Adobe | N/A - fully Adobe owned |
| Version Purge | Adobe | Fully owned by Adobe, but in the future, customers will be able to configure certain parameters. |
| Audit Log Purge  | Adobe | Fully owned by Adobe, but in the future, customers will be able to configure certain parameters. |
| Lucene Binaries Cleanup | Adobe | Unused and therefore disabled by Adobe. |
| Ad-hoc Task Purge | Customer | Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder `/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding another node under the node above (name it `granite_TaskPurgeTask`) with the appropriate properties. <br> Configure the OSGI properties see the [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)|
| Workflow Purge | Customer |  Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder`/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding another node under the node above (name it `granite_WorkflowPurgeTask`) with the appropriate properties. <br> Configure the OSGI properties see [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Project Purge | Customer |  Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder `/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding a node under the node above (name it `granite_ProjectPurgeTask`) with the appropriate properties. <br> Configure OSGI properties see [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Customers can schedule each of the Workflow Purge, Ad-hoc Task Purge and Project Purge Maintenance tasks to be executed during the daily, weekly, or monthly maintenance windows. These configurations should be edited directly in source control. The table below describes the configuration parameters available for each of the window. Also, see the locations and code samples provided after the table.-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Attività di manutenzione</th>
    <th>A chi appartiene la configurazione</th>
    <th>Come configurare (facoltativo)</th>
  </tr>  
  <tr>
    <td>Raccolta rifiuti di Datastore</td>
    <td>Adobe</td>
    <td>N/D - interamente di proprietà Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Pulizia delle versioni</td>
    <td>Adobe</td>
    <td>Affinché il livello di authoring rimanga performante, le versioni precedenti di ogni elemento di contenuto sotto il <code>/content</code> il nodo del repository viene eliminato in base al seguente comportamento:<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->
     <ol>
       <li>Le versioni con età superiore a 30 giorni vengono rimosse</li>
       <li>Le ultime 5 versioni negli ultimi 30 giorni sono conservate</li>
       <li>Indipendentemente dalle regole di cui sopra, viene conservata la versione più recente.</li>
     </ol><br>NOTA: il comportamento descritto sopra viene applicato per i nuovi ambienti a partire dal 14 marzo 2022 e verrà applicato per gli ambienti esistenti (quelli creati prima del 14 marzo 2022) il 21 aprile 2022.</td>
  </td>
  </tr>
  <tr>
    <td>Elimina log di controllo</td>
    <td>Adobe</td>
    <td>Affinché il livello di authoring rimanga performante, i registri di controllo più vecchi sotto la sezione <code>/content</code> il nodo del repository viene eliminato in base al seguente comportamento:<br><br> <!-- See above for the two line breaks -->
     <ol>
       <li>Per il controllo della replica, i registri di controllo più vecchi di 3 giorni vengono rimossi</li>
       <li>Per il controllo DAM (Assets), i registri di controllo con età maggiore di 30 giorni vengono rimossi</li>
       <li>Per il controllo delle pagine, i registri più vecchi di 3 giorni vengono rimossi.</li>
     </ol><br>NOTA: il comportamento descritto sopra viene applicato per i nuovi ambienti a partire dal 14 marzo 2022 e verrà applicato per gli ambienti esistenti (quelli creati prima del 14 marzo 2022) il 21 aprile 2022.</td>
   </td>
  </tr>
  <tr>
    <td>Pulizia binary di Lucene</td>
    <td>Adobe</td>
    <td>Non utilizzato e quindi disabilitato per Adobe.</td>
  </td>
  </tr>
  <tr>
    <td>Rimozione di attività ad hoc</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Ignorare il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà sotto la cartella <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>.</p>
    <p>Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito. Abilita l'attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominalo <code>granite_TaskPurgeTask</code>) con le proprietà appropriate. Configura le proprietà OSGI per visualizzare le <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">Documentazione relativa alle attività di manutenzione di AEM 6.5</a>.</p>
  </td>
  </tr>
    <tr>
    <td>Svuotamento flusso di lavoro</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Ignorare il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà sotto la cartella <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito.</p>
    <p>Abilita l'attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominalo <code>granite_WorkflowPurgeTask</code>) con le proprietà appropriate. Configura le proprietà OSGI vedi <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">Documentazione relativa alle attività di manutenzione di AEM 6.5</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Eliminazione progetti</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Ignorare il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà sotto la cartella <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito.</p>
    <p>Abilita l'attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominalo <code>granite_ProjectPurgeTask</code>) con le proprietà appropriate. Configura le proprietà OSGI vedi <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">Documentazione relativa alle attività di manutenzione di AEM 6.5</a>.</p>
  </td>
  </tr>
  </tbody>
</table>

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
  <p><strong>windowStartTime=HH:MM</strong> utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono iniziare a essere eseguite.</p>
  <p><strong>windowEndTime=HH:MM</strong> utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono interrompere l'esecuzione se non sono già state completate.</p>
  </td> 
  </tr>
  <tr>
    <td>Settimanale</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> (questo valore non deve essere modificato)</p>
    <p><strong>windowStartTime=HH:MM</strong> utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione settimanale devono iniziare a essere eseguite.</p>
    <p><strong>windowEndTime=HH:MM</strong> utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione settimanale devono interrompere l'esecuzione se non sono già state completate.</p>
    <p><strong>windowScheduleWeekdays= Array di 2 valori da 1 a 7 (ad esempio [5,5])</strong> Il primo valore dell'array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L'ora esatta dell'inizio e della fine è regolata rispettivamente da windowStartTime e windowEndTime.</p>
    </td>
  </tr>
  <tr>
    <td>Mensile</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=daily</strong> (questo valore non deve essere modificato)</p>
    <p><strong>windowStartTime=HH:MM</strong> utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono iniziare a essere eseguite.</p>
    <p><strong>windowEndTime=HH:MM</strong> utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono interrompere l'esecuzione se non sono già state completate.</p>
    <p><strong>windowScheduleWeekdays=Array di 2 valori da 1 a 7 (ad esempio [5,5])</strong> Il primo valore dell'array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L'ora esatta dell'inizio e della fine è regolata rispettivamente da windowStartTime e windowEndTime.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 per pianificare la prima settimana del mese o 1 per pianificare l’ultima settimana del mese. L'assenza di un valore consente di pianificare in modo efficace i processi ogni giorno secondo le regole di windowScheduleWeekdays ogni mese.</p>
    </td> 
    </tr>
    </tbody>
</table>

**Posizioni**:

* Giornaliero - /apps/settings/granite/operations/maintenance/granite_daily
* Settimanale - /apps/settings/granite/operations/maintenance/granite_weekly
* Mensile - /apps/settings/granite/operations/maintenance/granite_month

**Esempi di codice**:

Esempio di codice 1 (giornaliero)

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

Esempio di codice 2 (settimanale)

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

Esempio di codice 3 (mensile)

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
