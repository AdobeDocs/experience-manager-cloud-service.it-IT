---
title: Migrazione a identità esterna e appartenenza a gruppo dinamico
description: Guida tecnica per la migrazione di utenti e gruppi locali a un modello di identità esterno con iscrizione dinamica ai gruppi in AEM as a Cloud Service
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: 1f8bd9eea249e0b2242f3fbe1490b3d51052f546
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 1%

---

# Migrazione a identità esterna e appartenenza a gruppo dinamico {#migrating-to-external-identity}

## Panoramica {#overview}

Quando [Sincronizzazione dati](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization) è abilitato in AEM as a Cloud Service, è possibile configurare il gestore di autenticazione SAML per eseguire automaticamente la migrazione alle identità esterne con l&#39;appartenenza dinamica al gruppo durante la gestione della creazione di utenti e gruppi. Se il progetto utilizza un codice personalizzato per creare utenti o gruppi, è necessario aggiornarlo per creare utenti e gruppi esterni, anziché utenti e gruppi locali.

### Perché sono necessari utenti e gruppi esterni {#why-external-required}

La migrazione da utenti e gruppi locali a identità esterne con iscrizione dinamica ai gruppi è essenziale per diversi motivi critici:

**Ottimizzazione delle prestazioni:**

* **Scritture repository ridotte**: l&#39;appartenenza al gruppo locale tradizionale richiede la scrittura di relazioni di appartenenza all&#39;archivio in una singola proprietà multivalore del nodo del gruppo. Con l&#39;appartenenza dinamica al gruppo, gli utenti dispongono di una singola proprietà `rep:externalPrincipalNames` contenente tutte le entità di gruppo, eliminando la necessità di sincronizzare il nodo del gruppo
* **Sincronizzazione più rapida**: quando si sincronizzano gli utenti tra i nodi del livello di pubblicazione, gli utenti esterni con appartenenza a gruppi dinamici richiedono un numero significativamente inferiore di operazioni di trasferimento dati e di scrittura rispetto agli utenti locali con appartenenze a gruppi tradizionali
* **Scalabilità**: i sistemi con un numero elevato di utenti e gruppi traggono notevole vantaggio dalla riduzione del sovraccarico dell&#39;archivio. L’iscrizione a un gruppo dinamico può essere scalata in modo efficiente anche con gruppi molto grandi.

Il presente documento fornisce indicazioni tecniche per:

* Informazioni sul modello di identità esterna
* Modifica del codice personalizzato per creare utenti e gruppi esterni
* Migrazione di utenti e gruppi locali esistenti al modello di identità esterno

## Informazioni sull’identità esterna {#understanding-external-identity}

### Utenti esterni {#external-users}

Gli utenti esterni sono identificati dalla proprietà `rep:externalId`, che collega l&#39;utente a un provider di identità esterno. Il formato è:

```
userId;idpName
```

Ad esempio: `john.doe;saml-idp`.

>[!NOTE]
>
> `idpName` fa riferimento al nome del provider di identità di Oak (Idp) come definito nella configurazione del gestore di autenticazione. Per le integrazioni SAML, questo è il valore impostato per l&#39;attributo `idpIdentifier` nel gestore di autenticazione SAML.

**Proprietà chiave:**

* `rep:externalId`: proprietà obbligatoria che contrassegna un utente come esterno (ad esempio, `john.doe;saml-idp`)
* `rep:externalPrincipalNames`: proprietà multivalore contenente entità di gruppo esterne per l&#39;appartenenza dinamica
* `rep:lastSynced`: timestamp dell&#39;ultima sincronizzazione
* `rep:lastDynamicSync`: timestamp dell&#39;ultima sincronizzazione di appartenenza al gruppo dinamico

### Gruppi esterni {#external-groups}

I gruppi esterni sono identificati anche dalla proprietà `rep:externalId` e utilizzano un formato di nome entità:

```
groupId;idpName
```

Esempio: `content-authors;saml-idp`

### Appartenenza a gruppo dinamico {#dynamic-group-membership}

Invece delle relazioni dirette tra utenti e gruppi archiviate nell&#39;archivio, l&#39;appartenenza dinamica ai gruppi utilizza la proprietà `rep:externalPrincipalNames` nel nodo utente. Quando un utente ha un nome principale esterno che corrisponde all’ID di un gruppo esterno, diventa automaticamente membro di quel gruppo. Per ulteriori informazioni, consulta la [documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html).

**Vantaggi:**

* Riduzione delle scritture nell’archivio (nessun nodo di appartenenza al gruppo viene modificato quando gli utenti vengono aggiunti/rimossi dai gruppi)
* Sincronizzazione più rapida tra i nodi del livello di pubblicazione
* Gestione scalabile delle appartenenze ai gruppi
* Compatibile con i requisiti di sincronizzazione dei dati

## Configurazione utente del servizio {#service-user-configuration}

Tutte le operazioni che creano o modificano utenti e gruppi esterni devono essere eseguite utilizzando un **utente del servizio** configurato correttamente per ignorare la protezione predefinita nelle proprietà `rep:externalId` e `rep:externalPrincipalNames`.

### Perché è richiesto un utente del servizio {#why-is-a-service-user-required}

Per impostazione predefinita, la sicurezza di Oak impedisce alle sessioni regolari di modificare proprietà protette come:

* `rep:externalId` - Contrassegna utenti/gruppi come esterni
* `rep:externalPrincipalNames` - Memorizza le entità di appartenenza al gruppo dinamico

Solo un utente del servizio configurato correttamente può modificare queste proprietà.

### Configurazione e mappatura degli utenti del servizio {#service-user-configuration-mapping}

Per configurare un utente del servizio per la gestione delle identità esterne sono necessarie tre configurazioni coordinate:

1. Crea l&#39;utente del servizio tramite `repoinit`
2. Configura protezione `ExternalPrincipal`
3. Mappa l’utente del servizio sul bundle dell’applicazione.

Per una descrizione dettagliata di questi passaggi, vedi di seguito.

#### Passaggio 1: creare l&#39;utente del servizio tramite Repoinit {#create-the-serviice-user-via-repoinit}

Questo passaggio descrive la creazione dell&#39;utente del servizio con le autorizzazioni necessarie utilizzando uno script `repoinit`.

**File di configurazione:** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**Posizione esemplare:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**Panoramica autorizzazioni**

* `jcr:read`: lettura utenti e gruppi
* `jcr:readAccessControl`: Lettura ACL
* `jcr:modifyAccessControl`: modificare gli ACL (necessari per impostare le proprietà)
* `rep:userManagement`: crea e gestisci utenti/gruppi
* `rep:write`: proprietà di scrittura, inclusi `rep:externalId` e `rep:externalPrincipalNames`

>[!NOTE]
>
>L&#39;utente del servizio viene creato in `/home/users/system/yourproject` per mantenerlo organizzato con altri utenti di sistema.

#### Passaggio 2: configurare la protezione ExternalPrincipal {#configure-externalprincipal-protection}

Di seguito è riportata una configurazione di esempio per inserire in una whitelist l’utente del servizio in modo che possa ignorare la protezione applicata alle proprietà di identità esterne.

**Nome file di configurazione:** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**Percorso di esempio:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**Proprietà configurazione:**

* `protectExternalIdentities`: controlla il livello di protezione per le proprietà di identità esterne:
   * `"Strict"`: solo le entità di sistema nella whitelist possono modificare le proprietà esterne. Questo è il livello consigliato per la produzione.
   * `"Warn"`: registra gli avvisi ma consente le modifiche. Utile per sviluppo/test.
   * `"None"`: nessuna protezione. Non consigliato.
* `systemPrincipalNames`: elenco dei nomi utente del servizio autorizzati a modificare `rep:externalId` e `rep:externalPrincipalNames`. Includi tutti gli utenti del servizio che devono gestire identità esterne (ad esempio, `group-provisioner`, `saml-migration-service`).

>[!IMPORTANT]
>
>I nomi utente del servizio in `systemPrincipalNames` devono corrispondere esattamente agli ID utente del servizio creati nello script Repoinit.

#### Passaggio 3: mappatura degli utenti del servizio {#service-user-mapping}

Mappa l’utente del servizio sul bundle dell’applicazione in modo che il codice possa utilizzarlo.

**File di configurazione:** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**Posizione:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**Formato mappatura:**

* `yourproject.core`: nome del bundle simbolico (trovato in `pom.xml` `<Bundle-SymbolicName>`)
* `group-provisioner` (prima di `=`): nome del servizio secondario che verrà utilizzato nel codice
* `[group-provisioner]` (dopo `=`): l&#39;ID utente effettivo del servizio creato in repoinit

### Utilizzo dell’utente del servizio nel codice {#using-the-service-user-in-code}

Quando apri una sessione per eseguire operazioni di migrazione o creazione di utenti/gruppi, devi utilizzare l’utente del servizio:

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>Se non si configura correttamente l&#39;utente del servizio, i tentativi di impostazione di `rep:externalId` o `rep:externalPrincipalNames` non riusciranno e si verificheranno errori di autorizzazione. Verificare che l&#39;utente del servizio sia configurato correttamente nella configurazione `ExternalPrincipal` prima di tentare la migrazione.

## Esempio di configurazione completa {#complete-configuration-example}

Di seguito è riportato un esempio di lavoro completo che mostra tutte e tre le configurazioni insieme:

### Struttura dei file {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### Modifica del codice personalizzato {#modifying-custom-code}

#### Creazione di utenti esterni {#creating-external-users}

**Prima (utente locale):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**Dopo (Utente Esterno):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### Creazione di gruppi esterni {#creating-external-groups}

**Prima (gruppo locale):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**Dopo (gruppo esterno):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### Assegnazione dell’iscrizione al gruppo dinamico {#assigning-dynamic-membership}

**Prima (iscrizione diretta):**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**Dopo (appartenenza dinamica):**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## Processo di migrazione {#migration-process}

La migrazione di utenti e gruppi locali esistenti all’identità esterna non è necessaria quando il codice personalizzato è stato aggiornato prima di abilitare Data Synchronization Services.

Se gli utenti e i gruppi locali sono già stati salvati in modo permanente nell’archivio e l’ambiente viene utilizzato attivamente, ti consigliamo di eseguire una migrazione a più passaggi come quella riportata di seguito, al fine di evitare interruzioni o incoerenze.

>[!IMPORTANT]
>
>Tutti i passaggi di migrazione devono essere eseguiti utilizzando un utente del servizio configurato correttamente (ad esempio, `group-provisioner`) a cui sono state concesse le autorizzazioni per ignorare la protezione sulle proprietà `rep:externalId` e `rep:externalPrincipalNames`. Per ulteriori dettagli, vedere [Configurazione utente del servizio](#service-user-configuration).

### Passaggio 1: creare una struttura di gruppo esterna {#step-1-create-external-group-structure}

Per ogni gruppo locale di cui è necessario eseguire la migrazione:

1. Creare un gruppo esterno corrispondente con nome entità: `<localGroupId>;<idpName>`. Utilizza una convenzione di denominazione che faciliti il collegamento di gruppi esterni con gruppi locali
1. Imposta la proprietà `rep:externalId` sul gruppo esterno con i valori: `<localGroupId>;<idpName>`
1. Aggiungere il gruppo esterno come membro del gruppo locale originale.

**Convalida**

* Puoi convalidare i risultati verificando se a ogni gruppo locale corrisponde un gruppo esterno. Inoltre, ogni gruppo esterno è membro del gruppo locale corrispondente.

**Endpoint Servlet Di Esempio:**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**Utilizzo:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### Passaggio 2: convertire gli utenti e assegnare l&#39;appartenenza dinamica {#step-2-convert-users-and-assign-dynamic-membership}

Per ogni utente membro di un gruppo locale:

1. Assicurarsi che sia impostato `rep:externalId` (se necessario, convertire in utente esterno).
1. Per ogni appartenenza al gruppo, aggiungere l&#39;entità del gruppo esterno corrispondente a `rep:externalPrincipalNames`
1. Aggiorna i timestamp di sincronizzazione.

>[!IMPORTANT]
>
>Ignora i gruppi di sistema come &quot;tutti&quot; durante questo processo.

**Endpoint Servlet Di Esempio:**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**Utilizzo:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**Convalida**

Per convalidare questa impostazione, verificare che ogni utente disponga degli attributi `rep:externalId` e `rep:externalPrincipalName` con `principalName` di ogni gruppo esterno. Gli utenti sono membri dei gruppi locali *e* dei gruppi esterni.

### Passaggio 3: rimuovere le appartenenze utente diretto {#step-3-remove-direct-user-memberships}

Dopo aver configurato l&#39;appartenenza a un gruppo dinamico:

1. Rimuovere le appartenenze utente diretto dai gruppi locali
1. Mantenere le appartenenze da gruppo a gruppo (inclusa l&#39;appartenenza a gruppo esterno)

**Endpoint Servlet Di Esempio:**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**Utilizzo:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**Convalida**

* È possibile convalidare questa impostazione verificando che ogni gruppo locale abbia come membro solo il gruppo esterno corrispondente o altri gruppi.


## Flusso di lavoro di migrazione {#migration-workflow}

### Elenco di controllo pre-migrazione {#pre-migration-checklist}

* **Configura utente del servizio**: crea e configura l&#39;utente del servizio (ad esempio, `group-provisioner`) con le autorizzazioni appropriate
* **Verifica configurazione ExternalPrincipal**: verificare che l&#39;utente del servizio sia configurato per ignorare la protezione in `rep:externalId` e `rep:externalPrincipalNames`
* **Verifica autorizzazioni utente servizio**: verificare che l&#39;utente del servizio possa impostare proprietà di identità esterne in fase di sviluppo
* Identifica tutto il codice personalizzato che crea utenti o gruppi
* Rivedi e aggiorna il codice personalizzato per utilizzare il modello di identità esterno
* Test del codice aggiornato nell&#39;ambiente di sviluppo
* Inventario di tutti gli utenti e i gruppi locali esistenti da migrare
* Test del processo di migrazione in ambienti di dimensioni inferiori

### Passaggi di esecuzione {#execution-steps}

1. **Distribuisci codice aggiornato**: distribuisci le modifiche al codice personalizzato per creare utenti/gruppi esterni

1. **Crea gruppi esterni** (per ogni gruppo locale):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **Esegui migrazione utenti** (per ogni utente):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **Pulizia** (per ogni gruppo migrato):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **Verifica**: verifica le appartenenze ai gruppi di utenti e verifica le autorizzazioni di accesso

1. **Abilita sincronizzazione dati**: contattare l&#39;Assistenza clienti per abilitare la funzione

### Convalida post-migrazione {#post-migration-validation}

Verifica la migrazione:

1. **Controlla proprietà utente**:

   Nei nodi utente verifica la presenza di:

   * `rep:externalId`: il formato deve essere `userId;idpName`
   * `rep:externalPrincipalNames`: Array di entità di gruppo in formato `groupId;idpName`
   * `rep:lastSynced`: timestamp impostato su molto futuro (circa 10 anni dalla data di migrazione)
   * `rep:lastDynamicSync`: timestamp impostato su molto futuro (circa 10 anni dalla data di migrazione)

   **Nota**: le marche temporali sono impostate intenzionalmente su una data futura lontana come soluzione alternativa per OAK-12079. Questo è il comportamento previsto.

1. **Verifica proprietà gruppo**:

   Nei nodi del gruppo locale verificare la presenza di:

   * Membro del gruppo esterno con formato `groupId;idpName`
   * Nessun membro utente diretto (solo dopo il passaggio 3)

1. **Accesso utente di prova**: verificare che gli utenti possano accedere e disporre delle autorizzazioni corrette

1. **Controllo dell&#39;accesso di prova**: verificare che gli utenti possano accedere al contenuto protetto da CUG/ACL

## Risoluzione dei problemi {#troubleshooting}

### Problemi comuni {#common-issues}

**Problema: errori di autorizzazione durante l&#39;impostazione di `rep:externalId` o`rep:externalPrincipalNames`**

**Messaggi di errore:**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**Soluzione**: è necessario aprire la sessione utilizzando un utente del servizio configurato correttamente che dispone delle autorizzazioni necessarie per ignorare la protezione nelle proprietà di identità esterne.

**Passaggi da risolvere:**

1. **Verificare che l&#39;utente del servizio esista**: verificare che l&#39;utente del servizio (ad esempio, `group-provisioner`) sia stato creato tramite repoinit
1. **Verificare il mapping degli utenti del servizio**: verificare che il servlet o il servizio utilizzi `repository.loginService("group-provisioner", null)`
1. **Verifica configurazione ExternalPrincipal**: verificare che `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration` sia configurato correttamente
1. **Verifica le autorizzazioni utente del servizio**: l&#39;utente del servizio ha bisogno di `rep:write` e di `rep:userManagement` autorizzazioni per `/home/users` e `/home/groups`

Per istruzioni di installazione complete, vedere [Configurazione utente del servizio](#service-user-configuration).

**Problema:`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**Soluzione**: gli utenti devono avere `rep:externalId` impostato prima di impostare `rep:externalPrincipalNames`. Assicurarsi che il passaggio 2 converta prima gli utenti in utenti esterni.

**Problema: gli utenti perdono l&#39;appartenenza al gruppo dopo la migrazione**

**Soluzione**: verificare che:

* Il gruppo esterno è stato creato con il formato corretto del nome entità (`groupId;idpName`)
* Il gruppo esterno è stato aggiunto come membro del gruppo locale (passaggio 1)
* L&#39;utente ha corretto i nomi principali esterni in `rep:externalPrincipalNames` (passaggio 2)
* Il passaggio 3 è stato eseguito solo dopo il completamento dei passaggi 1 e 2

**Problema: le appartenenze a gruppi esterni vengono rimosse in modo imprevisto dopo l&#39;accesso dell&#39;utente (OAK-12079)**

**Problema**: a causa del bug di Oak [OAK-12079](https://issues.apache.org/jira/browse/OAK-12079), il meccanismo di sincronizzazione di Oak potrebbe eliminare anticipatamente le appartenenze ai gruppi esterni in base alle marche temporali `rep:lastSynced` e `rep:lastDynamicSync`.

**Soluzione**: impostare le marche temporali `rep:lastSynced` e `rep:lastDynamicSync` su una data futura lontana (tra 10 anni) invece dell&#39;ora corrente. Questo impedisce al processo di pulizia della sincronizzazione di rimuovere le appartenenze ai gruppi esterni.

**Implementazione:**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**Perché funziona**: impostando i timestamp su una data futura lontana, la logica di sincronizzazione di Oak tratta questi utenti come &quot;sincronizzati di recente&quot; e non attiva il processo di pulizia che rimuoverebbe i nomi di entità esterne e le appartenenze ai gruppi.

**Nota**: questa è una soluzione alternativa temporanea fino a quando OAK-12079 non verrà risolto in una versione futura di Oak. Tutti gli esempi di codice in questo documento includono già questa soluzione alternativa.

**Problema: il gruppo di sistema &quot;Everyone&quot; causa errori**

**Soluzione**: ignorare sempre il gruppo di sistema &quot;tutti&quot; durante la migrazione degli utenti (passaggio 2). Questo gruppo viene gestito automaticamente da AEM.

### Procedura di ripristino {#rollback-procedure}

Se si verificano problemi durante la migrazione:

1. Interrompi processo di migrazione
1. Ripristina dal backup in caso di dati critici
1. Ripristina le modifiche apportate al codice per creare utenti e gruppi esterni con appartenenza a un gruppo dinamico
1. Rivedi e correggi i problemi prima di ritentare la migrazione.

## Best practice {#best-practices}

* **Verifica approfondita**: verifica sempre la migrazione negli ambienti di sviluppo e di staging prima della produzione
* **Elaborazione batch**: per basi utente di grandi dimensioni, elabora le migrazioni in batch per evitare problemi di timeout
* **Monitora prestazioni**: controlla le prestazioni dell&#39;archivio durante la migrazione
* **Gestisci prova di verifica**: registra tutte le operazioni di migrazione per la risoluzione dei problemi
* **Autorizzazioni utente del servizio**: assicurarsi che i servlet di migrazione utilizzino gli utenti del servizio appropriati con le autorizzazioni richieste. L&#39;utente del servizio deve essere configurato nella configurazione ExternalPrincipal per ignorare la protezione nelle proprietà `rep:externalId` e `rep:externalPrincipalNames`
* **Operazioni Idempotent**: rieseguibilità sicura del codice di migrazione della progettazione
* **Convalida a ogni passaggio**: prima di procedere, verifica i risultati dopo ogni passaggio di migrazione

## Protezione dei servlet di migrazione {#securing-migration-servlets}

I servlet di migrazione dispongono di privilegi elevati per creare e modificare utenti e gruppi. È fondamentale limitare l’accesso a questi endpoint per impedire l’accesso non autorizzato.

### Approccio consigliato: autenticazione account tecnico IMS {#recommended-approach-ims-technical-account}

L’approccio consigliato consiste nel proteggere questi servlet utilizzando l’integrazione Adobe IMS, consentendo l’accesso solo a un account tecnico autorizzato.

#### Passaggio 1: creare un account tecnico in AEM Developer Console {#create-a-technical-account-in-aem-developer-console}

1. Passa a [Experience Manager](https://experience.adobe.com/) e quindi a **Cloud Manager**
1. Seleziona il programma e fai clic sull’ambiente in cui desideri creare l’account tecnico
1. Fai clic su **Developer Console** nel menu con i puntini di sospensione dell&#39;ambiente
1. In AEM Developer Console, vai alla scheda **Integrazioni**
1. Fai clic su **Crea nuovo account tecnico**
1. Specifica un nome per l’integrazione (ad esempio, &quot;Account del servizio di migrazione&quot;)
1. Fai clic su **Crea**.
1. Osserva i seguenti valori dall’integrazione creata:
   * **ID client**
   * **Segreto client**
   * **ID account tecnico** (questo sarà l&#39;ID utente che accede ai servlet - formato: `XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`)

Per istruzioni dettagliate, consulta [Generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

Codice di esempio per verificare se il chiamante è autorizzato:

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### Difesa in profondità: restrizioni basate su IP {#defense-in-depth-ip-based-restrictions}

Come ulteriore livello di sicurezza, puoi configurare le regole CDN per limitare l’accesso agli endpoint di migrazione in base all’indirizzo IP. Questa funzione è utile quando le migrazioni vengono eseguite da un’infrastruttura nota.

>[!NOTE]
>
>Le restrizioni IP da sole non sono sufficienti. Combina sempre con i controlli di autenticazione come descritto sopra.

### Elenco di controllo della sicurezza {#security-checklist}

Prima di distribuire i servlet di migrazione alla produzione:

* Creare l’integrazione IMS in AEM Developer Console
* Configurare i servlet per convalidare l’ID account tecnico
* Flusso di autenticazione di test in ambienti di sviluppo/staging
* Considerare ulteriori restrizioni basate su IP a livello CDN
* Pianifica la disattivazione o la rimozione dei servlet di migrazione al termine della migrazione
* Controlla e registra tutti gli accessi agli endpoint di migrazione

>[!IMPORTANT]
>
>Al termine della migrazione, è consigliabile disabilitare o rimuovere i servlet di migrazione dalla distribuzione per eliminare eventuali rischi per la sicurezza.

## Risorse aggiuntive {#additional-resources}

* [Sincronizzazione utenti e gruppi per livello di pubblicazione](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [Gestore autenticazione SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=it)
* [Provider di identità esterno](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)
* [Appartenenza a gruppo dinamico](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
