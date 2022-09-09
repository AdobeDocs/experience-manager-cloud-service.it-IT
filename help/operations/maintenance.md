---
title: Attività di manutenzione in AEM as a Cloud Service
description: Attività di manutenzione in AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: def7f7071dac447397f40186de1380b8e5575608
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 100%

---

# Attività di manutenzione in AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Attività di manutenzione"
>abstract="Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare l’archivio. Con AEM as a Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni di infrastruttura."

Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare l’archivio. Con AEM as a Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni di infrastruttura.

## Configurazione delle attività di manutenzione {#maintenance-tasks-configuring}

Nelle versioni precedenti di AEM, era possibile configurare le attività di manutenzione utilizzando la scheda Manutenzione (Strumenti > Operazioni > Manutenzione). In AEM as a Cloud Service la scheda di manutenzione non è più disponibile, pertanto le configurazioni devono essere salvate nel controllo sorgente e distribuite utilizzando Cloud Manager. Adobe gestisce le attività di manutenzione che presentano impostazioni non configurabili dai clienti (ad esempio, Raccolta rifiuti del datastore, Eliminazione del log di audit, Pulizia delle versioni). I clienti possono configurare altre attività di manutenzione, come descritto nella tabella seguente.

>[!CAUTION]
>
>Adobe si riserva il diritto di sovrascrivere le impostazioni di configurazione di un’attività di manutenzione del cliente per attenuare problemi come il degrado delle prestazioni.

Nella tabella seguente sono illustrate le attività di manutenzione disponibili al momento del rilascio di AEM as a Cloud Service.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Attività di manutenzione</th>
    <th>A chi appartiene la configurazione</th>
    <th>Come configurare (facoltativo)</th>
  </tr>  
  <tr>
    <td>Raccolta rifiuti del datastore</td>
    <td>Adobe</td>
    <td>N/D: gestito completamente da Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Pulizia delle versioni</td>
    <td>Adobe</td>
    <td>Affinché il livello di authoring rimanga performante, le versioni precedenti di ogni elemento di contenuto sotto il nodo dell’archivio <code>/content</code> vengono eliminate in base al seguente comportamento:<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->
     <ol>
       <li>Le versioni precedenti a 30 giorni vengono rimosse</li>
       <li>Le ultime 5 versioni degli ultimi 30 giorni vengono conservate</li>
       <li>Indipendentemente dalle regole di cui sopra, viene conservata la versione più recente.</li>
     </ol><br>NOTA: il comportamento descritto sopra viene applicato per impostazione predefinita per i nuovi ambienti creati dopo il 14 marzo 2022. Invia un ticket all’assistenza clienti se hai bisogno di impostazioni diverse.</td>
  </td>
  </tr>
  <tr>
    <td>Elimina log di controllo</td>
    <td>Adobe</td>
    <td>Affinché il livello di authoring rimanga performante, i registri di controllo più vecchi sotto il nodo <code>/content</code> dell’archivio vengono eliminati in base al seguente comportamento:<br><br> <!-- See above for the two line breaks -->
     <ol>
       <li>Per il controllo della replica, i registri di audit precedenti a 3 giorni vengono rimossi</li>
       <li>Per il controllo DAM (Assets), i registri di audit precedenti a 30 giorni vengono rimossi</li>
       <li>Per il controllo delle pagine, i registri con più di 3 giorni vengono rimossi.</li>
     </ol><br>NOTA: il comportamento descritto sopra viene applicato per impostazione predefinita per i nuovi ambienti creati dopo il 14 marzo 2022. Invia un ticket all’assistenza clienti se hai bisogno di impostazioni diverse.</td>
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
    <p>Deve essere eseguito in git. Sovrascrivi il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà sotto la cartella <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>.</p>
    <p>Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito. Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo superiore (denominalo <code>granite_TaskPurgeTask</code>) con le proprietà appropriate. Configura le proprietà OSGI.</p>
  </td>
  </tr>
    <tr>
    <td>Eliminazione flussi di lavoro</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Sovrascrivi il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà sotto la cartella <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito.</p>
    <p>Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo superiore (denominalo <code>granite_WorkflowPurgeTask</code>) con le proprietà appropriate. Configura le proprietà OSGI secondo la <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html?lang=it#regular-purging-of-workflow-instances">Documentazione delle attività di manutenzione di AEM 6.5</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Eliminazione progetti</td>
    <td>Cliente</td>
    <td>
    <p>Deve essere eseguito in git. Sovrascrivi il nodo di configurazione della finestra Manutenzione preconfigurata in <code>/libs</code> creando proprietà sotto la cartella <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> o <code>granite_daily</code>. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito.</p>
    <p>Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo superiore (denominalo <code>granite_ProjectPurgeTask</code>) con le proprietà opportune. Configura le proprietà OSGI.</p>
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
  <p><strong>windowStartTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono iniziare l’esecuzione.</p>
  <p><strong>windowEndTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono interrompere l’esecuzione se non sono già state completate.</p>
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
    <p><strong>windowScheduleWeekdays= Array di 2 valori da 1 a 7 (ad esempio [5,5])</strong> Il primo valore dell’array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L’ora esatta di inizio e di fine è regolata rispettivamente da windowStartTime e windowEndTime.</p>
    </td>
  </tr>
  <tr>
    <td>Mensile</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>
    <p><strong>windowSchedule=daily</strong> (questo valore non deve essere modificato)</p>
    <p><strong>windowStartTime=HH:MM</strong> utilizzando un orologio da 24 ore.  Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono iniziare l’esecuzione.</p>
    <p><strong>windowEndTime=HH:MM</strong> utilizzando un orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono interrompere l’esecuzione se non sono già state completate.</p>
    <p><strong>windowScheduleWeekdays=Array di 2 valori da 1 a 7 (ad esempio [5,5])</strong> Il primo valore dell’array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L’ora esatta di inizio e di fine è regolata rispettivamente da windowStartTime e windowEndTime.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 per pianificare la prima settimana del mese o 1 per pianificare l’ultima settimana del mese. L’assenza di un valore consente di pianificare ogni giorno in modo efficace i processi secondo le regole mensili di windowScheduleWeekdays.</p>
    </td> 
    </tr>
    </tbody>
</table>

**Posizioni**:

* Giornaliero: /apps/settings/granite/operations/maintenance/granite_daily
* Settimanale: /apps/settings/granite/operations/maintenance/granite_weekly
* Mensile: /apps/settings/granite/operations/maintenance/granite_monthly

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
