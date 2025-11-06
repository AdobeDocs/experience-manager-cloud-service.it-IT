---
title: Aggiornamento dei frammenti di contenuto per riferimenti UUID
description: Scopri come aggiornare i frammenti di contenuto per riferimenti UUID ottimizzati in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
exl-id: 004d1340-8e3a-4e9a-82dc-fa013cea45a7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 2%

---

# Aggiornamento dei frammenti di contenuto per riferimenti UUID {#upgrade-content-fragments-for-UUID-references}

Per ottimizzare la stabilità dei filtri GraphQL, puoi aggiornare i riferimenti a contenuto e frammento nei Frammenti di contenuto in modo che utilizzino identificatori univoci universali (UUID).

In origine i modelli per frammenti di contenuto fornivano i tipi di dati **Riferimento contenuto** e **Riferimento frammento**. Entrambi questi riferimenti utilizzano un percorso per puntare alla risorsa di riferimento e possono diventare obsoleti se la risorsa viene spostata. Sebbene tali riferimenti siano più che sufficienti nella maggior parte degli scenari, i modelli per frammenti di contenuto sono stati estesi per fornire anche riferimenti basati su un UUID:

* **Riferimento contenuto (UUID)**
* **Riferimento frammento (UUID)**.

Questi nuovi tipi di riferimento possono essere utilizzati sia nei nuovi modelli e frammenti di frammento di contenuto che per estendere le istanze esistenti.

Per aggiornare frammenti di contenuto e modelli esistenti, puoi eseguire la procedura documentata qui.

>[!CAUTION]
>
>Prima di eseguire la procedura di aggiornamento, è sempre necessario [eseguire un&#39;esecuzione a secco](#execute-a-dry-run) per evidenziare eventuali problemi potenziali con il contenuto.

## Cosa viene aggiornato {#what-is-upgraded}

Vengono apportati i seguenti aggiornamenti:

* Campi dei tipi di dati:
   * **Il riferimento contenuto** è convertito in **Riferimento contenuto (UUID)**
   * **I riferimenti frammento** sono convertiti in **riferimenti frammento (UUID)**
* I valori dei riferimenti basati sul percorso contenuti in questi campi vengono sostituiti dai corrispondenti UUID

>[!NOTE]
>
>Dopo l’aggiornamento, entrambi i tipi di dati sono ancora disponibili nell’editor modelli per frammenti di contenuto. Puoi creare nuovi campi basati su entrambi i tipi (anche se si prevede di utilizzare i tipi basati su UUID) e, se necessario, eseguire nuovamente l’aggiornamento.

## Cosa NON è aggiornato {#what-is-not-upgraded}

I seguenti riferimenti non vengono aggiornati:

* Riferimenti pagina - UUID non ancora supportati
* Eventuali riferimenti non validi; ad esempio, dove la destinazione del percorso del frammento di contenuto o del percorso della risorsa non esiste

   * I riferimenti non validi non vengono aggiornati, come se il percorso del frammento di contenuto, o percorso della risorsa, non fosse valido in assenza di un UUID corrispondente da assegnare. Il riferimento originale rimane invariato.

   * Utilizza una [prova](#execute-a-dry-run) per rilevare eventuali riferimenti non validi.

  >[!NOTE]
  >
  >Non essendo valide, non sono utilizzabili, indipendentemente dall’aggiornamento.

## Quando non effettuare l’aggiornamento {#when-you-should-not-upgrade}

Non aggiornare:

* Quando uno dei frammenti di contenuto utilizza i riferimenti di pagina; poiché gli UUID non sono ancora supportati per i riferimenti di pagina

## Limitazioni dei riferimenti UUID {#limitations-of-uuid-references}

Attualmente, quando si utilizzano riferimenti basati su un UUID si applicano le seguenti limitazioni:

* Modelli

   * Non è possibile creare nuovi modelli per frammenti di contenuto con campi UUID frammento di contenuto o UUID riferimento contenuto tramite OpenAPI.
   * Il campo `id` per i modelli non è stato modificato per essere basato su UUID. Utilizza il percorso decodificato base64 del modello. I modelli non possono essere spostati, pertanto questo valore è ancora stabile.

* Risorse

   * Durante la creazione di un frammento di contenuto tramite OpenAPI, è necessario utilizzare i tipi di campo `fragment-reference` o `content-reference` per specificare i riferimenti rispettivamente a un frammento o a una risorsa, anche quando si imposta il valore di un campo di riferimento basato su UUID.

## Pianificazione dell&#39;aggiornamento {#upgrade-planning}

Sono disponibili alcuni passaggi di preparazione prima di eseguire l’aggiornamento.

### Esecuzione di un&#39;esecuzione di prova {#execute-a-dry-run}

Si consiglia di eseguire un&#39;esecuzione di prova *ogni* volta che si aggiorna il contenuto. Verranno creati file di registro con voci che evidenziano eventuali problemi:

* Riferimenti non validi
* Riferimenti pagina

Eseguire l&#39;aggiornamento del contenuto in modalità `dryRun` per:

* identificare eventuali riferimenti non validi, elencandoli nei file di registro
Puoi quindi correggere questi riferimenti prima di eseguire l’aggiornamento effettivo del contenuto.
* identificare eventuali riferimenti di pagina, inserendoli nei file di registro
Quando vengono rilevati riferimenti di pagina, [non deve eseguire l&#39;aggiornamento del contenuto](#when-you-should-not-upgrade).


### Imporre un blocco dei contenuti {#enforce-a-content-freeze}

L’esecuzione dell’aggiornamento del contenuto deve essere pianificata durante un periodo di blocco dei contenuti.

La durata del blocco dei contenuti dipende dal volume di Frammenti di contenuto da aggiornare. Di conseguenza, l’aggiornamento può variare da pochi minuti a poche ore e dipende anche dai parametri utilizzati all’avvio dell’aggiornamento del contenuto.

## Esecuzione dell’aggiornamento del contenuto {#running-the-content-upgrade}

L&#39;aggiornamento del contenuto può essere gestito utilizzando l&#39;endpoint: `/libs/dam/cfm/maintenance.json`

>[!NOTE]
>
>Il tuo account ha bisogno del ruolo `Administrator` per accedere all&#39;endpoint.

### Avviare un aggiornamento del contenuto {#start-a-content-upgrade}

| Endpoint | Tipo di richiesta HTTP | Commenti |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Parametri richiesta** | **Valore** | |
| azione | `start` | |
| serviceTypeId | `uuidUpgradeService` | ID del tipo di servizio (predefinito, valore fisso). |
|  segmentSize | `1000` | Il numero di frammenti di contenuto o modelli che verranno aggiornati in un segmento (batch). |
| basePath | `/conf` | Specificare:<ul><li>la radice `/conf` per aggiornare tutte le configurazioni di AEM</li><li>un percorso di configurazione di AEM selezionato. per cui viene eseguito l&#39;aggiornamento del contenuto<br>Ad esempio: `/conf/wknd-shared` aggiorna solo il singolo tenant `wknd-shared`</li></ul> |
| intervallo | `10` | Intervallo in secondi dopo il quale viene aggiornato il segmento successivo di Frammenti di contenuto o modelli. |
| modalità | `replicate`, `noReplicate` | <ul><li>`replicate`: replica lo stesso processo in tutte le istanze di AEM Publish</li><li>`noReplicate`: esegue il processo solo sulle istanze di AEM Author</li></ul> |
| dryRun |  `true`, `false` | <ul><li>`false`: simulare l&#39;aggiornamento del contenuto senza salvare le modifiche apportate</li><li>`true`: eseguire l&#39;aggiornamento del contenuto e salvare le modifiche apportate al contenuto</li></ul> |
| **Dettagli risposta** | **Valore** | |
| jobId | `UUID` |  ID del processo che esegue l’aggiornamento del contenuto.<ul><li>Questo ID è richiesto in tutte le chiamate successive relative a questa esecuzione.</li><li>Se il valore `mode` è impostato su `replicate`, anche l&#39;esecuzione sulle istanze AEM Publish deve trovarsi nello stesso `jobId`.</li></ul> |
| parametri | Parametri di aggiornamento del contenuto | Questi includono i parametri iniziali forniti per avviare l’aggiornamento del contenuto e alcuni valori predefiniti interni. |


### Esempio di richiesta di aggiornamento del contenuto {#example-content-upgrade-request}

+++Richiesta

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++Risposta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### Ottenere lo stato di un aggiornamento del contenuto {#get-the-status-of-a-content-upgrade}

| Endpoint | Tipo di richiesta HTTP | Commenti |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **Parametri richiesta** | **Valore** | |
| azione | stato | |
| jobId | `<UUID>` | `jobId` restituito dalla chiamata per avviare l&#39;aggiornamento del contenuto. |
| **Dettagli risposta** | **Valore** | |
| stato | Valori JSON | Contiene lo stato dettagliato dell’aggiornamento del contenuto:<ul><li>Aggiornato dopo ogni intervallo (secondi).</li><li>L&#39;esecuzione di `uuidUpgradeService` prevede due fasi:<ol><li>fase 0 per aggiornare i modelli per frammenti di contenuto</li><li>fase 1: aggiornamento dei frammenti di contenuto</li></ol></li><li>In ogni fase, le statistiche vengono aggiornate dopo ogni intervallo.</li><li>&quot;jobStatus&quot;: &quot;COMPLETED&quot; contrassegna l&#39;aggiornamento come completato correttamente.</li><li>Altri valori di stato sono auto-esplicativi.</li></ul> |

### Esempio di richiesta di stato dell’aggiornamento del contenuto {#example-content-upgrade-status-request}

+++Richiesta

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++Risposta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++File di registro di esempio

Oltre allo stato di un aggiornamento del contenuto in esecuzione ottenuto dall’endpoint HTTP, i registri di AEM forniscono informazioni dettagliate sull’avanzamento a livello di contenuto. Ad esempio:

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

Inoltre, dopo l’elaborazione di ciascun segmento (batch) di Frammenti di contenuto e Modelli, viene registrato uno stato accumulato che riepiloga l’avanzamento finora. Ad esempio:

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### Interrompere un aggiornamento del contenuto {#abort-a-content-upgrade}

>[!CAUTION]
>
>Interruzione di un aggiornamento del contenuto (che non è un’esecuzione in prova):
>
>* non ripristina le modifiche già apportate
>* potrebbe lasciare il contenuto in uno stato misto
>
>Utilizza questa azione con cautela.

| Endpoint | Tipo di richiesta HTTP | Commenti |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Parametri richiesta** | **Valore** | |
| azione | abort | |
| jobId | `<UUID>` | `jobId` restituito dalla chiamata per avviare l&#39;aggiornamento del contenuto. |
| **Dettagli risposta** | **Valore** | |
| stato | Valori JSON | Contiene lo stato dettagliato dell’aggiornamento del contenuto:<ul><li>Lo stato da notare è &quot;jobStatus&quot;: &quot;ABORTED&quot;.<br>Dopo un&#39;azione di interruzione, i segmenti di dati in sospeso non verranno elaborati.</li><li>Se jobStatus è &quot;COMPLETED&quot; prima di un&#39;interruzione, la chiamata non ha alcun effetto.</li></ul> |

### Esempio di richiesta di interruzione di un aggiornamento del contenuto {#example-abort-content-upgrade-request}

+++Richiesta

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++Risposta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
