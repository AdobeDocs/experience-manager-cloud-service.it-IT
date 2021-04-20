---
title: Attività di manutenzione in AEM come Cloud Service
description: Attività di manutenzione in AEM come Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
translation-type: tm+mt
source-git-commit: 256363d166591137b53d4a6b5a31436064dfb3d2
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 2%

---

# Attività di manutenzione in AEM come Cloud Service

Le attività di manutenzione sono processi eseguiti secondo una pianificazione al fine di ottimizzare il repository. Con AEM come Cloud Service, la necessità per i clienti di configurare le proprietà operative delle attività di manutenzione è minima. I clienti possono concentrare le proprie risorse sui problemi a livello di applicazione, lasciando ad Adobe le operazioni dell&#39;infrastruttura.

Per ulteriori informazioni sulle attività di manutenzione, consulta le pagine seguenti:

* [Guida alla manutenzione AEM](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Attività di manutenzione del dashboard delle operazioni](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Configurazione delle attività di manutenzione

Nelle versioni precedenti di AEM, è possibile configurare le attività di manutenzione utilizzando la scheda Manutenzione (Strumenti > Operazioni > Manutenzione). Per AEM come Cloud Service, la scheda di manutenzione non è più disponibile, pertanto le configurazioni devono essere inviate al controllo del codice sorgente e distribuite utilizzando Cloud Manager. Adobe gestirà le attività di manutenzione che non richiedono decisioni del cliente (ad esempio, Raccolta rifiuti di Datastore), mentre altre attività di manutenzione possono essere configurate dal cliente (vedi la tabella seguente).

>[!CAUTION]
>
>Adobe si riserva il diritto di ignorare le impostazioni di configurazione di un&#39;attività di manutenzione del cliente per attenuare problemi come il degrado delle prestazioni.

Nella tabella seguente sono illustrate le attività di manutenzione disponibili al momento del rilascio di AEM come Cloud Service.

| Attività di manutenzione | A chi appartiene la configurazione | Come configurare (facoltativo) |
|---|---|---|
| Raccolta rifiuti di Datastore | Adobe | N/D - interamente di proprietà Adobe |
| Pulizia delle versioni | Adobe | Di proprietà completa di Adobe, ma in futuro i clienti saranno in grado di configurare alcuni parametri. |
| Elimina log di controllo | Adobe | Di proprietà completa di Adobe, ma in futuro i clienti saranno in grado di configurare alcuni parametri. |
| Pulizia binary di Lucene | Adobe | Non utilizzato e quindi disabilitato per Adobe. |
| Rimozione di attività ad hoc | Cliente | Deve essere fatto in github. <br> Ignora il nodo di configurazione della finestra Manutenzione predefinita in  `/libs` creando proprietà sotto la cartella  `/apps/settings/granite/operations/maintenance/granite_weekly` o  `granite_daily`. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito. <br> Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominalo  `granite_TaskPurgeTask`) con le proprietà appropriate. <br> Configurare le proprietà OSGI consulta la documentazione relativa all’attività di manutenzione  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Svuotamento flusso di lavoro | Cliente | Deve essere fatto in github. <br> Ignorare il nodo di configurazione della finestra Manutenzione predefinita in  `/libs` creando proprietà nella `/apps/settings/granite/operations/maintenance/granite_weekly` cartella  `granite_daily`. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito. <br> Abilita l’attività di manutenzione aggiungendo un altro nodo sotto il nodo sopra (denominalo  `granite_WorkflowPurgeTask`) con le proprietà appropriate. <br> Configurare le proprietà OSGI consulta la documentazione relativa all’attività di manutenzione  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Eliminazione progetti | Cliente | Deve essere fatto in github. <br> Ignora il nodo di configurazione della finestra Manutenzione predefinita in  `/libs` creando proprietà sotto la cartella  `/apps/settings/granite/operations/maintenance/granite_weekly` o  `granite_daily`. Per ulteriori informazioni sulla configurazione, consulta la tabella Finestra di manutenzione riportata di seguito. <br> Abilita l’attività di manutenzione aggiungendo un nodo sotto il nodo precedente (denominalo  `granite_ProjectPurgeTask`) con le proprietà appropriate. <br> Configurare le proprietà OSGI consulta la documentazione relativa all’attività di manutenzione  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

I clienti possono pianificare ciascuna delle attività di eliminazione del flusso di lavoro, eliminazione delle attività ad hoc e manutenzione dell’eliminazione dei progetti da eseguire durante le finestre di manutenzione giornaliere, settimanali o mensili. Queste configurazioni devono essere modificate direttamente nel controllo del codice sorgente. La tabella seguente descrive i parametri di configurazione disponibili per ciascuna finestra.

<table>
  <tr>
    <th>Configurazione della finestra di manutenzione</th>
    <th>A chi appartiene la configurazione</th>
    <th>Tipo di configurazione</th>
    <th>Dove si trova</th>
    <th>Esempio</th>
    <th>Parametri</th>
  </tr>
  <tr>
    <td>Giornaliero</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>Vedi la posizione 1 di seguito</td>
    <td>Vedi il codice di esempio 1 di seguito</td>
  <td>
  <strong>windowSchedule</strong> = day (questo valore non deve essere modificato) 
  <strong>windowStartTime</strong>  = HH:MM utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono iniziare a essere eseguite.
  <strong>windowEndTime</strong> = HH:MM utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono interrompere l'esecuzione se non sono già state completate.
  </td> 
  </tr>
  <tr>
    <td>Settimanale</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>Vedi la posizione 2 di seguito</td>
    <td>Vedi il codice di esempio 2 di seguito</td>
    <td>
    <strong>windowSchedule</strong> = settimanale (questo valore non deve essere modificato) 
    <strong>windowStartTime</strong> = HH:MM utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra di manutenzione settimanale devono iniziare a essere eseguite.
    <strong>windowEndTime</strong> = HH:MM utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione settimanale devono interrompere l'esecuzione se non sono già state completate.
    <strong>windowScheduleWeekdays = Array di 2 valori da 1 a 7. ad esempio [5,5]</strong> Il primo valore dell'array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L'ora esatta dell'inizio e della fine è regolata rispettivamente da windowStartTime e windowEndTime.
    </td> 
  </tr>
  <tr>
    <td>Mensile</td>
    <td>Cliente</td>
    <td>Definizione del nodo JCR</td>
    <td>Vedi la posizione 3 di seguito</td>
    <td>Vedi il codice di esempio 3 di seguito</td>
    <td>
    <strong>windowSchedule</strong> = day (questo valore non deve essere modificato) 
    <strong>windowStartTime</strong>  = HH:MM utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono iniziare a essere eseguite.
    <strong>windowEndTime</strong> = HH:MM utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione mensile devono interrompere l'esecuzione se non sono già state completate.
    <strong>windowScheduleWeekdays = Array di 2 valori da 1 a 7. ad esempio [5,5]</strong> Il primo valore dell'array è il giorno iniziale in cui il processo viene pianificato e il secondo valore è il giorno finale in cui il processo viene interrotto. L'ora esatta dell'inizio e della fine è regolata rispettivamente da windowStartTime e windowEndTime.
    <strong>windowFirstLastStartDay - 0/1</strong> 0 per pianificare la prima settimana del mese o 1 per l'ultima settimana del mese. L'assenza di un valore consente di pianificare in modo efficace i processi ogni giorno secondo le regole di windowScheduleWeekdays ogni mese.
    </td> 
    </tr>
</table>

Posizioni:

1. /apps/settings/granite/operations/maintenance/granite_daily
2. /apps/settings/granite/operations/maintenance/granite_weekly
3. /apps/settings/granite/operations/maintenance/granite_month

Esempi di codice:

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

Esempio di codice 3

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

| Configurazione della finestra di manutenzione | A chi appartiene la configurazione | Tipo di configurazione | Dove si trova | Esempio | Parametri |
|---|---|---|---|---|---|
| Giornaliero | Cliente | Definizione del nodo JCR | Vedi la posizione 2 di seguito | Vedi il codice di esempio 2 di seguito | `windowSchedule= daily` (questo valore non deve essere modificato).  <br> `windowStartTime=HH:MM` utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono iniziare a essere eseguite. <br> **windowEndTime= HH:** utilizzando come orologio da 24 ore. Definisce quando le attività di manutenzione associate alla finestra Manutenzione giornaliera devono interrompere l&#39;esecuzione se non sono già state completate. |
