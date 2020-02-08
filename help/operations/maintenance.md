---
title: Attività di manutenzione in AEM come servizio cloud
description: 'Attività di manutenzione in AEM come servizio cloud '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e

---


# Attività di manutenzione in AEM come servizio cloud

Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare il repository. Con AEM come servizio Cloud, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando le operazioni dell&#39;infrastruttura ad Adobe.

Per ulteriori informazioni sulle attività di manutenzione, consulta le pagine seguenti:

* [Guida alla manutenzione di AEM](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Operazioni di manutenzione del dashboard](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Configurazione delle attività di manutenzione

Nelle versioni precedenti di AEM, era possibile configurare le attività di manutenzione utilizzando la scheda di manutenzione (Strumenti > Operazioni > Manutenzione). Per AEM come servizio cloud, la scheda di manutenzione non è più disponibile, pertanto le configurazioni devono essere salvate nel controllo del codice sorgente e distribuite utilizzando Cloud Manager. Adobe gestirà le attività di manutenzione che non richiedono decisioni da parte del cliente (ad esempio, DataStore Garbage Collection), mentre altre attività di manutenzione possono essere configurate dal cliente (vedere la tabella seguente).

>[!CAUTION]
>
>Adobe si riserva il diritto di ignorare le impostazioni di configurazione delle attività di manutenzione del cliente al fine di attenuare problemi quali il degrado delle prestazioni.

La tabella seguente illustra le attività di manutenzione disponibili al momento del rilascio di AEM come servizio cloud.

| Attività di manutenzione | Chi possiede la configurazione | Come configurare (facoltativo) |
|---|---|---|
| Raccolta rifiuti dataStore | Adobe | N/D - interamente di proprietà di Adobe |
| Pulizia delle versioni | Adobe | Di proprietà di Adobe, ma in futuro i clienti potranno configurare alcuni parametri. |
| Rimozione registro di controllo | Adobe | Di proprietà di Adobe, ma in futuro i clienti potranno configurare alcuni parametri. |
| Pulizia binary di Lucene | Adobe | Inutilizzato e quindi disabilitato da Adobe. |
| Rimozione attività ad hoc | Cliente | Deve essere fatto in github. <br> Ignorare il nodo di configurazione della finestra Manutenzione sotto `/libs` e `/apps` con `/conf/global/settings/granite/operations/maintenance/granite_weekly` o `granite_daily`. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra manutenzione riportata di seguito. <br> Attivate l’attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominatelo `granite_TaskPurgeTask`) con le proprietà appropriate. <br> Configurare le proprietà OSGI consulta la documentazione sulle attività di manutenzione di [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Svuotamento flusso di lavoro | Cliente | Deve essere fatto in github. <br> Ignorare il nodo di configurazione della finestra Manutenzione sotto `/libs` e `/apps` con `/conf/global/settings/granite/operations/maintenance/granite_weekly` o `granite_daily`. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra manutenzione riportata di seguito. <br> Attivate l’attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominatelo `granite_WorkflowPurgeTask`) con le proprietà appropriate. <br> Configurare le proprietà OSGI consulta la documentazione sulle attività di manutenzione di [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Eliminazione progetti | Cliente | Deve essere fatto in github. <br> Ignorare il nodo di configurazione della finestra Manutenzione sotto `/libs` e `/apps` con `/conf/global/settings/granite/operations/maintenance/granite_weekly` o `granite_daily`. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra manutenzione riportata di seguito. <br> Attivate l’attività di manutenzione aggiungendo un nodo sotto il nodo sopra (denominatelo `granite_ProjectPurgeTask`) con le proprietà appropriate. <br> Configurare le proprietà OSGI vedere la documentazione delle attività di manutenzione di [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

I clienti possono pianificare ciascuna delle attività di manutenzione Rimozione flusso di lavoro, Rimozione attività ad hoc e Rimozione progetti da eseguire durante le finestre di manutenzione giornaliera, settimanale o mensile. Queste configurazioni devono essere modificate direttamente nel controllo del codice sorgente. La tabella seguente descrive i parametri di configurazione disponibili per ciascuna finestra.

<table>
  <tr>
    <th>Configurazione della finestra di manutenzione</th>
    <th>Chi possiede la configurazione</th>
    <th>Tipo di configurazione</th>
    <th>Dove si trova</th>
    <th>Esempio</th>
    <th>Parametri</th>
  </tr>
  <tr>
    <td>Giornaliero</td>
    <td>Cliente</td>
    <td>Definizione nodo JCR</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_daily </code> (che sostituisce il nodo in <code>/apps</code> e <code>/libs</code>)</td>
    <td>Vedi l'esempio di codice 1 seguente</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = Daily (questo valore non deve essere modificato)</li>
    <li><strong>windowStartTime</strong> = HH:MM che utilizza come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione giornaliera devono iniziare a essere eseguite.</li>
    <li><strong>windowEndTime</strong> = HH:MM che utilizza come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione giornaliera devono interrompere l'esecuzione se non sono già state completate.</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>Settimanale</td>
    <td>Cliente</td>
    <td>Definizione nodo JCR</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code> (che sostituisce il nodo in <code>/apps</code> e <code>/libs</code>)</td>
    <td>Vedi l'esempio di codice 2 seguente</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = settimanale (questo valore non deve essere modificato)</li>
    <li><strong>windowStartTime</strong> = HH:MM che utilizza come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione settimanale devono iniziare a essere eseguite.</li>
    <li><strong>windowEndTime</strong> = HH:MM che utilizza come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione settimanale devono interrompere l'esecuzione se non sono già state completate.</li>
    <li><strong>windowScheduleWeekDays = array di 2 valori da 1 a 7. ad esempio [5,5].</strong> Il primo valore dell'array è il giorno iniziale in cui viene pianificato il processo e il secondo è il giorno finale in cui il processo viene interrotto. L'ora esatta dell'inizio e della fine è regolata rispettivamente da windowStartTime e windowEndTime.</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>Mensile</td>
    <td>Cliente</td>
    <td>Definizione nodo JCR</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_monthly</code> (che sostituisce il nodo in <code>/apps</code> e <code>/libs</code>)</td>
    <td>Cfr. codice di esempio 3</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = Daily (questo valore non deve essere modificato)</li>
    <li><strong>windowStartTime</strong> = HH:MM che utilizza come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione mensile devono iniziare a essere eseguite.</li>
    <li><strong>windowEndTime</strong> = HH:MM che utilizza come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione mensile devono interrompere l'esecuzione se non sono già state completate.</li>
    <li><strong>windowScheduleWeekDays = array di 2 valori da 1 a 7. ad esempio [5,5].</strong> Il primo valore dell'array è il giorno iniziale in cui viene pianificato il processo e il secondo è il giorno finale in cui il processo viene interrotto. L'ora esatta dell'inizio e della fine è regolata rispettivamente da windowStartTime e windowEndTime.</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0 per pianificare la prima settimana del mese o 1 per l'ultima settimana del mese. L'assenza di un valore consente di pianificare i processi quotidianamente secondo quanto stabilito da windowScheduleWeekday ogni mese.</li>
    </ul> </td> 
  </tr>
</table>

Esempio di codice 1

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

Esempio di codice 2

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

Codice di esempio 3

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
