---
title: Best practice per la mappatura degli utenti del servizio Sling e la definizione degli utenti del servizio
description: Scopri le best practice per la mappatura degli utenti del servizio Sling e la definizione degli utenti del servizio
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 99%

---

# Best practice per la mappatura degli utenti del servizio Sling e la definizione degli utenti del servizio {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## Mappatura degli utenti del servizio {#service-user-mapping}

Per aggiungere una mappatura dal servizio agli utenti del sistema corrispondenti, è necessario creare una configurazione di fabbrica per il servizio `ServiceUserMapper`. Per mantenerle modulari, tali configurazioni possono essere fornite utilizzando il meccanismo di “correzione” di Sling (consulta [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) per maggiori dettagli). Il modo consigliato per installare tali configurazioni con il bundle è quello di aggiungerlo al modello di provisioning Quickstart, come descritto nell’esempio seguente:

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### Formato di mappatura {#mapping-format}

A partire dalla versione AEM 6.4, il formato di mappatura è definito nel modo seguente:

>[!NOTE]
>
>Lo `userName` è obsoleto e non deve più essere utilizzato.

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` e `subserviceName` identificano il servizio, `userName/principalNames` identificano l’utente del servizio e `principalNames` è un elenco separato da virgole.

Inoltre, tieni presente che `principalNames` è l’elenco dei nomi principali degli utenti del servizio che, per impostazione predefinita, sono identici all’ID.


**Best practice**

* Nomi di servizi secondari per attività diverse: se i servizi del bundle eseguono attività diverse, si consiglia di identificare i `subserviceNames` per raggrupparli in base alle attività
* Se un determinato servizio esegue operazioni diverse (ad esempio, lettura del contenuto delle risorse e aggiornamento delle informazioni sotto una sottostruttura di `/var`), si consiglia di tenerne conto aggregando diverse entità principali del servizio che riflettono la singola operazione, come l’aggregazione del `dam-reader-service` comune con le specifiche funzionalità `assetreport-writer-service`
* Ogni servizio è idealmente associato a un insieme di operazioni molto specifico e limitato
* Il nuovo formato con `[one,or,multiple,principalNames]` è il metodo consigliato per definire le mappature degli utenti del servizio a partire dalla versione AEM 6.4.

Di seguito è riportato un elenco dei motivi per modificare il formato e perché Adobe consiglia di utilizzarlo al posto della versione con la mappatura limitata a un singolo ID utente:

* Possibilità di riutilizzare gli utenti del servizio combinando le esigenze speciali della clientela con le attività comuni
* Evitare la duplicazione della configurazione delle autorizzazioni
* Migliore comprensione delle autorizzazioni (e delle attività) effettive che un determinato servizio sta realmente eseguendo
* Non è necessaria l’iscrizione esplicita al gruppo degli utenti del servizio. Questo può avere effetti secondari dannosi come il cambiamento delle autorizzazioni di gruppo
* Miglioramento delle prestazioni e scalabilità

## Risoluzione mappatura e accesso al servizio {#mapping-resolution-and-service-login}

### Risoluzione mappatura servizio {#service-mapping-resolution}

La sequenza di chiamate per risolvere la mappatura del servizio è descritta di seguito:

1. Cerca la mappatura attiva di `principalNames` per determinati `bundleId` e `subserviceName`
1. Mappatura di `principalNames` per `bundleId` e `subserviceName` nullo
1. Mappatura di `userName` per `bundleId` e `subserviceName`
1. Mappatura di `userName` per `bundleId` e `subserviceName` nullo
1. Mappatura predefinita
1. Utente predefinito

### SlingRepository - Accesso al servizio {#slingrepository-servicelogin}

La sequenza per ottenere un servizio `Session/ResourceResolver` è la seguente:

1. Ottieni nomi di entità da `ServiceUserMapper` => pre-autenticazione per l’accesso all’archivio nel modo descritto di seguito
1. Recupera ID utente da `ServiceUserMapper`
1. Cerca `1ServiceUserConfiguration` obsoleto per l&#39;ID utente corrente
1. Accesso al servizio Sling predefinito con l’ID utente (ad esempio, una sequenza di `createAdministrativeSession` e impersonare l’ID utente del servizio)

La nuova mappatura con i nomi delle entità determina il seguente accesso semplificato all’archivio:

* L’insieme dei nomi di entità viene considerato come l’entità o le entità effettive da utilizzare per compilare il `Subject`
* L’accesso all’archivio può quindi essere preautenticato
* Nessuna risoluzione di iscrizione al gruppo

  >[!NOTE]
  >
  >Tutte le autorizzazioni richieste devono essere dichiarate per gli utenti del servizio. Le autorizzazioni ‘tutti’ e altri gruppi non verranno più ereditate.

* Non viene creato alcun accesso amministratore aggiuntivo per disporre del servizio-`Session/ResourceResolver`.

### ServiceUserConfiguration obsoleto {#deprecated-serviceUserConfiguration}

Tieni presente che specificare un singolo nome utente nella mappatura è equivalente al `ServiceUserConfiguration.simpleSubjectPopulation` esistente. Con il nuovo formato la soluzione alternativa fornita da `ServiceUserConfiguration` può essere riflessa direttamente con la mappatura degli utenti del servizio. Il `ServiceUserConfiguration` è stato pertanto dichiarato obsoleto per AEM e tutti gli utilizzi esistenti devono essere sostituiti.

## Utenti del servizio {#service-users}

### Riutilizzo degli utenti del servizio esistenti {#reusing-existing-service-users}

Si consiglia di riutilizzare gli utenti del servizio esistenti se sono soddisfatte le seguenti condizioni:

* Le tue esigenze corrispondono all’intento dell’utente del servizio esistente
* Il servizio richiede di eseguire un’attività comune trattata da un utente comune del servizio esistente. In questo caso, si consiglia di riutilizzare l’utente del servizio invece di introdurre una duplicazione
* Il servizio richiede un’attività specifica trattata da un utente del servizio esistente. In caso di dubbi, rivolgiti al team che gestisce le funzioni.

Non riutilizzare gli utenti del servizio esistenti se:

* Dovrai modificare le relative autorizzazioni in modo non correlato per farle funzionare
* Hai bisogno solo di un piccolo sottoinsieme dell’autorizzazione che fornisce e lo riutilizzerai semplicemente per il corretto funzionamento della funzione e non perché è una vera corrispondenza
* Il nome indica un’intenzione completamente diversa da quella richiesta. Sceglierla perché funziona può causare problemi durante il lavoro, in quanto il team delle funzionalità proprietario di un servizio specifico potrebbe modificare le autorizzazioni e interrompere la funzione.

### Creare un utente del servizio {#creating-a-service-user}

Dopo aver verificato che nessun utente del servizio esistente in AEM è applicabile al tuo caso d’uso e i problemi RTC corrispondenti sono stati approvati, puoi procedere e aggiungere il nuovo utente al contenuto predefinito. Idealmente un membro del team di sicurezza esteso è coinvolto nella votazione RTC, quindi assicurati di coinvolgere anche le parti interessate.

**Convenzione di denominazione**

Il team di sicurezza di AEM ha definito la seguente convenzione di denominazione per gli utenti del servizio al fine di garantire coerenza ai nuovi utenti del servizio e migliorarne la leggibilità e la manutenzione.

Un nome utente del servizio è costituito da 3 elementi separati da un trattino **‘-’**:

1. La funzionalità/entità logica di destinazione delle operazioni del servizio (evita elementi dei percorsi che potrebbero cambiare)
1. L’attività che i servizi eseguiranno
1. **‘Servizio’** finale per essere in grado di individuare facilmente dall’ID e dal nome dell’entità che l’utente è un utente del servizio

**Best practice**

* Non combinare entità/funzioni diverse. Suddividi in singoli utenti del servizio e aggregali nella mappatura se il servizio ha esigenze diverse
* Limitati a un’attività ben definita per ogni utente del servizio. Suddividi se finisci per concedere troppe autorizzazioni o autorizzazioni non correlate
* Dedica del tempo a identificare le reali esigenze del servizio
* Dedica del tempo a trovare un nome utente del servizio valido, significativo e intuitivo
* Chiedi un feedback e controlla: gli sviluppatori che non hanno familiarità con la tua funzione devono essere in grado di leggere e comprendere le tue intenzioni. In futuro potrebbero essere incaricati di apportare correzioni o provvedere alla manutenzione.

Alla fine, il nome utente del servizio deve mostrare:

* Come è destinato ad essere utilizzato e se può essere riutilizzato:

   * Molto generico: `content-writer-service`. Riutilizzabile in modo sicuro in aggregazione se i servizi devono essere anche in grado di leggere tutto il contenuto
   * Molto specifico: `asset-linkshare-service`. Riutilizzabile in modo sicuro solo se il servizio esegue realmente anche la condivisione dei collegamenti delle risorse.

* Le funzioni che dovrebbero avere impostate le autorizzazioni:

   * L’entità logica deve corrispondere alla configurazione delle autorizzazioni:

      * Un `content-foo-service` deve essere associato solo alle operazioni sul contenuto. Concedere le autorizzazioni per operare su altre entità, come la configurazione o gli utenti, sarebbe sbagliato
      * Un servizio specifico come `personalization-foo-service` deve inoltre disporre di autorizzazioni specifiche. Se alla fine si concedono le autorizzazioni su tutti i contenuti, non sarà più specifico. Riflettilo nel nome o riutilizza un utente comune nell’aggregazione
      * Un servizio specifico per la funzione come `msm-xyz-service` deve disporre solo di autorizzazioni relative a MSM. Non estendere le autorizzazioni a funzioni non correlate, ad esempio la gestione della configurazione delle community o degli utenti di Screens.

   * L’attività deve corrispondere alle autorizzazioni:

      * Un `foo-reader-service` deve solo essere in grado di leggere gli elementi regolari. Non concedere mai autorizzazioni di scrittura
      * Un `foo-writer-service` dovrebbe poter eseguire operazioni di scrittura. Tuttavia, non deve disporre delle autorizzazioni per leggere/modificare il contenuto del controllo degli accessi
      * Un `foo-replicator-service` deve poter avere l’autorizzazione per `crx:replicate`.

**Esempi**

Esempi di `configuration-reader-service`:

* Il nome indica che si riferisce alle configurazioni in generale e non alla configurazione di una particolare funzione, come la configurazione dell’integrazione DM. Un utente del servizio specificamente destinato alla configurazione della lettura di tale integrazione dovrebbe piuttosto essere definito `dmconfig-reader-service` o `s7config-reader-service`

  >[!NOTE]
  >
  >Nessuna informazione sul percorso è inclusa nella denominazione. Le configurazioni sono state spostate da `/etc` a `/conf`.

* L’elemento attività indica che i servizi associati a tale utente eseguiranno solo operazioni di lettura.

Esempi di `userproperties-copy-service`:

* I servizi associati a questo utente del servizio opereranno su proprietà di utenti/gruppi come profili o preferenze
* Lo scopo specifico è solo quello di copiare tali informazioni, a differenza di un nome come `userproperties-writer-service` che includerebbe qualsiasi tipo di operazione di scrittura. È, pertanto, possibile che l’impostazione delle autorizzazioni per queste operazioni di copia consenta solo di aggiungere elementi in una posizione e di rimuovere elementi in un’altra.

**Best practice per la configurazione delle autorizzazioni**

* Utilizzare sempre la configurazione di controllo degli accessi basata su entità principali per gli utenti del servizio. Per ulteriori dettagli, consulta gli esempi seguenti:

   * Consenti di contrassegnare gli utenti del servizio e le relative autorizzazioni come contenuto immutabile dell’applicazione in Skyline
   * Non è necessario creare percorsi e strutture ad albero

* Concedi solo le autorizzazioni, mai negarle
* Limita le autorizzazioni

   * Concedi solo il set minimo di autorizzazioni necessarie
   * Per ulteriori informazioni, consulta la documentazione [Mapping Privileges to Items](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) (Mappatura dei privilegi agli elementi) e [Mapping API Calls to Privileges](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html) (Mappatura delle chiamate API ai privilegi)
   * Non concedere l’autorizzazione per `jcr:all`. Molto probabilmente questo non è il set minimo.

* Riduci ambito

   * Posiziona i criteri di controllo dell’accesso in sottostrutture specifiche per la funzione
   * In caso di articoli distribuiti: utilizza restrizioni per limitare l’ambito (consulta [la documentazione](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) per un elenco di restrizioni incorporate).

* Garantire coerenza

   * Rendi le autorizzazioni coerenti con l’entità e l’attività che hai utilizzato nel nome dell’utente del servizio
   * Evita di aggiungere autorizzazioni non correlate. Ad esempio, sarebbe strano avere un `workflow-administration-service` e concedergli le autorizzazioni per eseguire operazioni di gestione degli utenti in `/home/users/screens` o lasciare che legga s7-config.

* Completezza

   * Assicurati che il servizio disponga di tutte le autorizzazioni necessarie per eseguire le attività per le quali è progettato. Il servizio deve essere pronto all’uso anche negli ambienti della clientela.
   * Non aspettarti/chiedere mai alla clientela di espandere la configurazione delle autorizzazioni (ad esempio, sotto `/apps`)

* Evitare la duplicazione della configurazione delle autorizzazioni

   * Riutilizza gli utenti comuni del servizio
   * Aggregali con gli utenti del servizio specifici della tua funzione che forniscono l’autorizzazione esplicita di cui hai anche bisogno

* Non suddividere l’impostazione delle autorizzazioni tra diverse funzioni. La necessità di eseguire questa operazione indica che l’utente del servizio non è definito correttamente o esegue troppe operazioni diverse
* Non inserire utenti del servizio in gruppi perché:

   * Ciò combinerebbe i dettagli di implementazione degli utenti del servizio con i gruppi ‘pubblici’
   * Non avresti il controllo sulle modifiche delle autorizzazioni (con il rischio di regressioni ed escalation dei privilegi)
   * Accesso e prestazione della valutazione
   * Non funziona con la configurazione AC basata su entità

* L’accesso al nodo user-home (o a qualsiasi sottostruttura in esso contenuto), che non dispone di un percorso prevedibile, viene ottenuto in repo init utilizzando home(`userId`). Per maggiori dettagli, consulta la [documentazione](https://sling.apache.org/documentation/bundles/repository-initialization.html) di repo init Sling.
* RTC: crea un problema RTC dedicato se modifichi le autorizzazioni di un utente del servizio esistente e assicurati che venga esaminato dal team di sicurezza.

**Creazione con inizializzazione dell’archivio**

Usa sempre `repo-init` per definire gli utenti del servizio e l’impostazione delle relative autorizzazioni e inserisci entrambi nella sezione corretta del modello della funzione Quickstart:

**Best practice**

* Usa sempre `repo-init` per creare l’utente del servizio
* Specifica sempre un percorso intermedio per la creazione di utenti del servizio
* Tutti gli utenti del servizio incorporati per AEM devono essere situati sotto `system/cq:services/internal`
* Aggiungi inoltre al percorso relativo intermedio al gruppo gli utenti del servizio in base alla funzione: `system/cq:services/internal/<your-feature>`
* Gli utenti del servizio definiti della clientela devono trovarsi sotto `system/cq:services/<customer-intermediate-rel-path>` e mai sotto la struttura interna
* Utilizza **con percorso forzato** invece di **con percorso** se un utente esiste già e deve essere spostato nella nuova posizione che supporta l’autorizzazione basata su entità.

**Esempi**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### Pulizia utenti del servizio e autorizzazioni {#cleanup-service-users-and-permissions}

Il seguente comando repo init può essere utilizzato per pulire gli utenti del servizio inutilizzati e le relative autorizzazioni:

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### Test degli utenti del servizio {#testing-service-users}

È fondamentale scrivere test lato server per gli utenti del servizio e la configurazione delle autorizzazioni. Questo non solo verifica il corretto funzionamento della configurazione, ma consente anche di individuare regressioni ed errori non intenzionali durante la modifica del contenuto di controllo dell’accesso o degli utenti del servizio.

La libreria `com.adobe.granite.testing.clients` fornisce molte utilità che semplificano la scrittura di SST per gli utenti del servizio.
