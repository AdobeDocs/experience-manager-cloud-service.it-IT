---
title: Best practice per la mappatura degli utenti e la definizione degli utenti del servizio Sling
description: Scopri le best practice per la mappatura utente del servizio sling e la definizione utente del servizio
source-git-commit: b6f7b6996b377ecfa372742ce1ad22139547ebdd
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---


# Best practice per la mappatura degli utenti e la definizione degli utenti del servizio Sling {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## Mappatura utenti del servizio {#service-user-mapping}

Per aggiungere una mappatura dal servizio agli utenti del sistema corrispondenti, è necessario creare una configurazione di fabbrica per `ServiceUserMapper` servizio. Per mantenere questo modulare, tali configurazioni possono essere fornite utilizzando il meccanismo di &quot;modifica&quot; di Sling (vedi [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) per maggiori dettagli). Il modo consigliato per installare tali configurazioni con il bundle è quello di aggiungerlo al modello di provisioning Quickstart, come descritto nell’esempio seguente:

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### Formato mappatura {#mapping-format}

A partire da AEM 6.4, il formato di mappatura è definito come segue:

>[!NOTE]
>
>Il `userName` è obsoleto e non deve più essere utilizzato.

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` e `subserviceName` identificare il servizio, `userName/principalNames` identificare l&#39;utente del servizio e `principalNames` è un elenco separato da virgole.

Inoltre, tieni presente che `principalNames` è l’elenco dei nomi principali dell’utente del servizio che, come impostazione predefinita, sono identici all’id.


**Best practice**

* Nomi di servizi secondari per attività diverse: se i servizi del bundle eseguono attività diverse, si consiglia di identificare `subserviceNames` per raggrupparli per attività
* Se un determinato servizio esegue operazioni diverse (ad esempio, lettura del contenuto delle risorse e aggiornamento delle informazioni sotto una sottostruttura di `/var`), si consiglia di tenere conto di ciò aggregando diversi principi di servizio che riflettono la singola operazione, come l&#39;aggregazione dei `dam-reader-service` con specifiche funzionalità `assetreport-writer-service`
* Ogni servizio è idealmente associato a un insieme di operazioni molto specifico e limitato
* Il nuovo formato con `[one,or,multiple,principalNames]` è il metodo consigliato per definire le mappature degli utenti del servizio a partire da AEM 6.4.

Di seguito è riportato un elenco dei motivi per cui è necessario modificare il formato e perché Adobe consiglia di utilizzarlo al posto della mappatura della versione solo per un singolo userID:

* Possibilità di riutilizzare gli utenti del servizio combinando le esigenze speciali dei clienti con le attività comuni
* Evita la duplicazione della configurazione delle autorizzazioni
* Migliore comprensione delle autorizzazioni (e delle attività) effettive che un determinato servizio sta effettivamente eseguendo
* Non è necessaria l&#39;iscrizione esplicita al gruppo degli utenti del servizio. Questo può avere effetti collaterali dannosi come il cambiamento delle autorizzazioni di gruppo
* Miglioramenti delle prestazioni e scalabilità

## Risoluzione mappatura e accesso al servizio {#mapping-resolution-and-service-login}

### Risoluzione mappatura servizi {#service-mapping-resolution}

La sequenza di chiamate per risolvere la mappatura del servizio descritta di seguito:

1. Cerca attivo `principalNames` mappatura per il dato `bundleId` e `subserviceName`
1. `principalNames` mappatura per `bundleId` e nulle `subserviceName`
1. `userName` mappatura per `bundleId` e `subserviceName`
1. `userName` mappatura per `bundleId` e nulle `subserviceName`
1. Mappatura predefinita
1. Utente predefinito

### SlingRepository - Accesso al servizio {#slingrepository-servicelogin}

Sequenza per ottenere un servizio `Session/ResourceResolver` funziona come segue:

1. Ottieni nomi entità da `ServiceUserMapper` => pre-autenticazione dell’accesso all’archivio come descritto di seguito
1. Recupera ID utente da `ServiceUserMapper`
1. Controlla se l’ID utente corrente è obsoleto: 1ServiceUserConfiguration
1. L’accesso al servizio Sling predefinito con l’ID utente (ad esempio, una sequenza di `createAdministrativeSession` e rappresenta per l’id utente del servizio)

La nuova mappatura con i nomi delle entità determina il seguente accesso semplificato all’archivio:

* L&#39;insieme di nomi di entità viene considerato come l&#39;entità o le entità effettive da utilizzare per compilare `Subject`
* L’accesso all’archivio può quindi essere preautenticato
* Nessuna risoluzione di appartenenza ai gruppi

  >[!NOTE]
  >
  >Tutte le autorizzazioni richieste devono essere dichiarate per gli utenti del servizio. Le autorizzazioni &#39;tutti&#39; e di altri gruppi non verranno più ereditate.

* Nessun accesso amministratore aggiuntivo per disporre del servizio-`Session/ResourceResolver` vengono create.

### ServiceUserConfiguration obsoleto {#deprecated-serviceUserConfiguration}

Tieni presente che specificare un singolo nome utente nella mappatura equivale a `ServiceUserConfiguration.simpleSubjectPopulation`. Con il nuovo formato la soluzione alternativa fornita da `ServiceUserConfiguration` può essere riflessa direttamente con la mappatura degli utenti del servizio. Il `ServiceUserConfiguration` è stato pertanto dichiarato obsoleto per l’AEM e tutti gli utilizzi esistenti devono essere sostituiti.

## Utenti del servizio {#service-users}

### Riutilizzo degli utenti del servizio esistenti {#reusing-existing-service-users}

Si consiglia di riutilizzare gli utenti del servizio esistenti se sono soddisfatte le seguenti condizioni:

* Le tue esigenze corrispondono all’intento dell’utente del servizio esistente
* Il servizio richiede di eseguire un&#39;attività comune coperta da un utente comune del servizio esistente. In questo caso, si consiglia di riutilizzare l’utente del servizio invece di introdurre la duplicazione
* Il servizio richiede un&#39;attività specifica coperta da un utente del servizio esistente. In caso di dubbi, rivolgiti al team che gestisce le funzioni.

Non riutilizzare gli utenti del servizio esistenti se:

* Dovrai modificare le relative autorizzazioni in modo non correlato per farle funzionare
* Se hai bisogno solo di un piccolo sottoinsieme dell’autorizzazione che fornisce, puoi semplicemente riutilizzarlo perché fa funzionare la tua funzione non perché è una vera corrispondenza
* Se il nome indica un&#39;intenzione completamente diversa da quella richiesta. Sceglierlo perché funziona può causare problemi durante il lavoro, in quanto il team delle funzionalità proprietario di un servizio specifico potrebbe modificare le autorizzazioni e interrompere la funzione.

### Creazione di un utente del servizio {#creating-a-service-user}

Dopo aver verificato che nessun utente di servizio esistente in AEM è applicabile al tuo caso d’uso e aver approvato i problemi RTC corrispondenti, puoi procedere e aggiungere il nuovo utente al contenuto predefinito. Idealmente un membro del team di sicurezza è coinvolto nella votazione RTC, quindi assicurati di coinvolgere anche le parti interessate.

**Convenzione di denominazione**

Il team di sicurezza dell’AEM ha definito la seguente convenzione di denominazione per gli utenti del servizio al fine di garantire coerenza ai nuovi utenti del servizio e migliorarne la leggibilità e la manutenibilità.

Un nome utente del servizio è costituito da 3 elementi separati da un trattino **&#39;-&#39;**:

1. Entità/funzionalità logica di destinazione delle operazioni del servizio (evitare elementi dei percorsi che potrebbero cambiare)
1. Attività che i servizi eseguiranno
1. Finale **&#39;servizio&#39;** essere in grado di individuare facilmente dall’id e dal nome dell’entità che l’utente è un utente del servizio

**Best practice**

* Non combinare entità/funzionalità diverse. Suddividi per singoli utenti del servizio e aggregali nella mappatura se il servizio ha esigenze diverse
* Limitarsi a un&#39;attività ben definita per ogni utente del servizio. Dividi se finisci per concedere troppe autorizzazioni o autorizzazioni non correlate
* Trascorri del tempo a identificare le reali esigenze del servizio
* Trascorri del tempo a trovare un nome utente di servizio valido, significativo e auto-esplicativo
* Chiedi un feedback e rivedi: gli sviluppatori che non hanno familiarità con la tua funzione devono essere in grado di leggere e comprendere le tue intenzioni. In futuro potrebbero essere incaricati di ripararla o di mantenerla.

Alla fine, il nome utente del servizio dovrebbe mostrare:

* Come è destinato ad essere utilizzato e se può essere riutilizzato:

   * Molto generico: `content-writer-service`. Riutilizzabile in modo sicuro in aggregazione se i servizi devono essere in grado di leggere tutto il contenuto
   * Molto specifico: `asset-linkshare-service`. Il riutilizzo è sicuro solo se il servizio esegue realmente anche la condivisione di collegamenti delle risorse.

* Descrizione del set di funzioni e dell’impostazione delle autorizzazioni

   * L’entità logica deve corrispondere alla configurazione delle autorizzazioni:

      * A `content-foo-service` deve essere associato solo alle operazioni sul contenuto. Concedere al reparto IT le autorizzazioni per operare su altre entità, come la configurazione o gli utenti, sarebbe sbagliato
      * Un servizio specifico come `personalization-foo-service` devono inoltre disporre di autorizzazioni specifiche. Se alla fine concedi le autorizzazioni per tutti i contenuti, non sarà più specifico. Rifletti nel nome o riutilizza un utente comune nell’aggregazione
      * Un servizio specifico per la funzione come `msm-xyz-service` deve disporre solo di autorizzazioni relative a msm. Non espandere le autorizzazioni a funzioni non correlate, ad esempio la gestione della configurazione delle community o degli utenti di Screens.

   * L’attività deve corrispondere alle autorizzazioni:

      * A `foo-reader-service` deve essere in grado di leggere solo gli elementi regolari. Non concedere mai autorizzazioni di scrittura
      * A `foo-writer-service` è previsto che esegua operazioni di scrittura. Tuttavia, non deve disporre delle autorizzazioni necessarie per leggere/modificare il contenuto di controllo degli accessi
      * A `foo-replicator-service` può avere `crx:replicate` concesso.

**Esempi**

Esempi di `configuration-reader-service`:

* Il nome indica che si riferisce alle configurazioni in generale e non alla configurazione di una particolare funzione, come la configurazione dell&#39;integrazione DM. Un utente di servizio specificamente destinato alla lettura della configurazione di tale integrazione preferirebbe essere nominato `dmconfig-reader-service` o `s7config-reader-service`

  >[!NOTE]
  >
  >Nessuna informazione di percorso è inclusa nella denominazione. Configurazioni spostate da `/etc` a `/conf`.

* L&#39;elemento task indica che i servizi associati a tale utente eseguiranno solo operazioni di lettura.

Esempi di `userproperties-copy-service`:

* I servizi associati a questo utente del servizio opereranno su proprietà di utenti/gruppi come profili o preferenze
* Il suo scopo specifico è quello di copiare tali informazioni, a differenza di un nome come `userproperties-writer-service` che includerebbe qualsiasi tipo di operazione di scrittura. È pertanto possibile che l&#39;impostazione delle autorizzazioni per queste operazioni di copia consenta solo di aggiungere elementi in una posizione e di rimuovere elementi in un&#39;altra.

**Configurazione delle best practice per le autorizzazioni**

* Utilizzare sempre le impostazioni di controllo dell&#39;accesso basate su entità per gli utenti del servizio. Per ulteriori dettagli, vedi gli esempi seguenti:

   * Consenti agli utenti del servizio di contrassegnare gli utenti e le relative autorizzazioni come contenuto immutabile dell’applicazione in skyline
   * Non è necessario creare tracciati e strutture ad albero

* Concedi solo le autorizzazioni, mai negare
* Limita autorizzazioni

   * Concedi solo il set minimo di autorizzazioni necessarie
   * Per ulteriori informazioni, consultare [Mappatura dei privilegi agli elementi](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) e [Mappatura delle chiamate API ai privilegi](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html) documentazione
   * Non concedere l’autorizzazione per `jcr:all`. Molto probabilmente non è il set minimo.

* Riduci ambito

   * Posizionare i criteri di controllo dell&#39;accesso in sottostrutture specifiche per la caratteristica
   * In caso di articoli distribuiti: utilizzare restrizioni per limitare l&#39;ambito (consultare [la documentazione](http://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) per un elenco di restrizioni integrate).

* Assicurare coerenza

   * Rendere le autorizzazioni coerenti con l&#39;entità e l&#39;attività utilizzate nel nome utente del servizio
   * Evita di aggiungere autorizzazioni non correlate. Ad esempio, sarebbe strano avere un `workflow-administration-service` e concederle le autorizzazioni per eseguire operazioni di gestione degli utenti in `/home/users/screens` o lasciare che legga s7-config.

* Completezza

   * Assicurati che il servizio disponga di tutte le autorizzazioni necessarie per eseguire le attività per le quali è progettato. Il servizio deve essere pronto all’uso anche negli ambienti dei clienti.
   * Non aspettarti/chiedi mai ai clienti di espandere la configurazione delle autorizzazioni (ad esempio, di seguito `/apps`)

* Evita la duplicazione della configurazione delle autorizzazioni

   * Riutilizzo degli utenti comuni dei servizi
   * Aggregali con gli utenti del servizio specifici della tua funzione che forniscono l’autorizzazione specifica necessaria. Inoltre

* Non suddividere l’impostazione delle autorizzazioni tra diverse funzioni. La necessità di eseguire questa operazione indica che l’utente del servizio non è definito correttamente o esegue troppe operazioni diverse
* Non inserire utenti del servizio in gruppi, perché:

   * Combina i dettagli di implementazione degli utenti del servizio con i gruppi &quot;pubblici&quot;
   * Non hai il controllo sulle modifiche delle autorizzazioni (soggetto a regressioni ed escalation dei privilegi)
   * Prestazioni di accesso e valutazione
   * Non funziona con la configurazione CA basata su entità

* L’accesso al nodo user-home (o a qualsiasi sottoalbero in esso contenuto), che non dispone di un percorso prevedibile, viene ottenuto nell’archivio iniziale utilizzando home(`userId`). Vedi l’archivio sling iniziale [documentazione](https://sling.apache.org/documentation/bundles/repository-initialization.html) per i dettagli.
* RTC: crea un problema RTC dedicato se modifichi le autorizzazioni di un utente del servizio esistente e ti assicuri che venga esaminato dal team di sicurezza.

**Creazione con inizializzazione archivio**

Usa sempre `repo-init` per definire gli utenti del servizio e le relative impostazioni delle autorizzazioni e inserire entrambi nella sezione corretta del modello di funzionalità Quickstart:

**Best practice**

* Usa sempre `repo-init` per creare l&#39;utente del servizio
* Specificare sempre un percorso intermedio per la creazione di utenti del servizio
* Tutti gli utenti di servizi integrati per AEM devono essere situati qui sotto `system/cq:services/internal`
* Aggiungi inoltre al percorso relativo intermedio per raggruppare gli utenti del servizio in base alla funzione: `system/cq:services/internal/<your-feature>`
* Gli utenti del servizio definito dal cliente devono trovarsi di seguito `system/cq:services/<customer-intermediate-rel-path>` e mai sotto l&#39;albero interno
* Utilizzare **con percorso forzato** invece di **con percorso** se un utente esiste già e deve essere spostato nella nuova posizione che supporta l’autorizzazione basata su entità.

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

### Pulizia utenti e autorizzazioni del servizio {#cleanup-service-users-and-permissions}

Il seguente comando di inizializzazione dell’archivio può essere utilizzato per pulire gli utenti del servizio inutilizzati e le relative autorizzazioni:

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

### Verifica degli utenti del servizio {#testing-service-users}

È fondamentale scrivere test lato server per gli utenti del servizio e la loro configurazione delle autorizzazioni. Questo non solo verifica il corretto funzionamento della configurazione, ma consente anche di individuare regressioni ed errori non intenzionali durante la modifica del contenuto di controllo dell’accesso o degli utenti del servizio.

Il `com.adobe.granite.testing.clients` La libreria fornisce molte utilità che semplificano la scrittura di SST per gli utenti del servizio.





