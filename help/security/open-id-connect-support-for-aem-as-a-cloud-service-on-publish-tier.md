---
title: Supporto OpenID Connect per AEM as a Cloud Service sul livello di pubblicazione
description: Scopri come configurare Open ID Connect (OIDC) per AEM as a Cloud Service sul livello di pubblicazione
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 70687e4f2ea0df923e44237bc20635745c46323a
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 53%

---

# Supporto OpenID Connect per AEM as a Cloud Service sul livello di pubblicazione {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## Introduzione {#introduction}

Man mano che le organizzazioni modernizzano le proprie esperienze digitali, la gestione delle identità sicura e scalabile diventa un requisito fondamentale. Adobe Experience Manager (AEM) Cloud Service ora supporta OpenID Connect (OIDC) sul livello di pubblicazione, che consente un&#39;integrazione fluida e basata su standard con i principali provider di identità (IdP) come Entra ID (Azure AD), Google, Okta, Auth0, Ping Identity, ForgeRock e gli IDP supportati da OIDC.

OIDC è un livello di identità sopra il protocollo OAuth 2.0 che consente una solida autenticazione utente mantenendo al contempo la semplicità per gli sviluppatori. È ampiamente adottato per scenari business-to-consumer (B2C), Intranet e portale partner, in cui sono necessari account utente sicuri e federazioni di identità.

Finora, i clienti di AEM erano responsabili dell&#39;implementazione della propria logica di accesso personalizzata sul livello di pubblicazione, che ha aumentato i tempi di sviluppo e introdotto problemi di manutenzione e sicurezza a lungo termine. Con il supporto nativo per OIDC, AEM Cloud Service rimuove questo carico fornendo un meccanismo di autenticazione sicuro, estensibile e supportato da Adobe per gli utenti finali che accedono agli ambienti di pubblicazione.

Che tu stia distribuendo un sito web consumer personalizzato o un portale interno autenticato, OIDC on Publish semplifica la federazione delle identità e riduce i rischi tramite la governance centralizzata delle identità. Consente inoltre alle organizzazioni di soddisfare i moderni standard di conformità e sicurezza senza sacrificare l&#39;agilità.

## Configurare AEM per l&#39;autenticazione OIDC {#configure-aem-oidc-authentication}

### Prerequisiti {#prerequisits}

Si presuppone che siano disponibili o definite le seguenti informazioni:

1. Percorsi del contenuto da proteggere nell’archivio AEM
1. Un identificatore dell’IdP da configurare. Può essere qualsiasi stringa

Informazioni dalla configurazione IdP:

1. ID client configurato nell&#39;IdP
1. Il segreto client configurato nell’Idp. Se PKCE è stato configurato nell’Idp, il segreto client non è disponibile. Non memorizzare il valore di testo normale nel file di configurazione. Usa un Segreto CM e fai riferimento a esso
1. Ambiti configurati nell&#39;Idp. È necessario specificare almeno l&#39;ambito `openid`
1. Se PKCE è abilitato nell&#39;IdP
1. `callbackUrl` è definito utilizzando uno dei percorsi configurati definiti al punto 1 e aggiungendo il suffisso: `/j_security_check`
1. `baseUrl` per accedere al file `.well-known` standard. Ad esempio, se l&#39;URL noto è: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`, `baseUrl` è: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### Panoramica dei file di configurazione {#overview-of-the-configuration-files}

Di seguito è riportato un elenco di file da configurare:

1. **Connessione OIDC**: verrà utilizzata da `OidcAuthenticationHandler` per autenticare gli utenti o da altri componenti per [autorizzare l&#39;accesso alle risorse protette dall&#39;IdP tramite OAuth](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **Gestore autenticazione OIDC**: gestore di autenticazione utilizzato per autenticare gli utenti che accedono ai percorsi configurati
1. **UserInfoProcessor**: questo componente elabora le informazioni ricevute dall&#39;IdP. Può essere esteso dai clienti per implementare una logica personalizzata
1. [**Gestore di sincronizzazione predefinito**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html): questo componente crea l&#39;utente nell&#39;archivio
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html): questo componente autentica l&#39;utente nell&#39;archivio oak locale.

Il diagramma seguente mostra come vengono collegati gli elementi di configurazione menzionati. Poiché si tratta di componenti `ServiceFactory`, `~uniqueid` può essere una qualsiasi stringa univoca casuale:

![Diagramma di configurazione OIDC](/help/security/assets/oidc-diagram.png)

### Configurare la connessione OIDC {#configure-the-oidc-connection}

Per prima cosa, è necessario configurare la connessione OIDC. È possibile configurare più connessioni OIDC, ognuna delle quali deve avere un nome diverso.

1. Crea un nuovo file `.cfg.json` che ospiterà la configurazione. Ad esempio, puoi utilizzare `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`, il suffisso **azure** deve essere un identificatore univoco per la connessione
1. Segui il formato di configurazione nell&#39;esempio seguente:

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/tenant-id/v2.0>",
    "clientId":"client-id-from-idp",
    "clientSecret":"xxxxxx"
   }
   ```

In alcuni ambienti, il provider di identità (IdP) potrebbe non esporre un endpoint `.well-known` valido.
In questo caso, gli endpoint richiesti possono essere definiti manualmente specificando le seguenti proprietà nel file di configurazione.
In questa modalità di configurazione, la proprietà `baseUrl` non deve essere impostata.

```
"authorizationEndpoint": "https://idp-url/oauth2/v1/authorize",
"tokenEndpoint": "https://idp-url/oauth2/v1/token",
"jwkSetURL":"https://idp-url/oauth2/v1/keys",
"issuer": "https://idp-url"
```

1. Configura le relative proprietà come segue:
   * **&quot;name&quot;** può essere definito dall&#39;utente
   * `baseUrl`, `clientid` e `clientSecret` sono valori di configurazione provenienti dall&#39;IdP.
   * Gli ambiti devono contenere almeno il valore `openid`.

### Configurare il Gestore autenticazione OIDC {#configure-oidc-authentication-handler}

Ora configura il gestore di autenticazione OIDC. È possibile configurare più connessioni OIDC. Ognuna deve avere un nome diverso. Se condividono lo stesso [Provider di identità esterno OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html), possono condividere gli utenti.

1. Crea il file di configurazione. Per questo esempio, utilizzeremo `org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json`. Il suffisso `azure` deve essere un identificatore univoco. Vedi un esempio del file di configurazione seguente:

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. Quindi, configura le relative proprietà come segue:
   * `path`: il percorso da proteggere
   * `callbackUri`: percorso da proteggere, aggiunta del suffisso: `/j_security_check`. Lo stesso callbackUri deve essere configurato anche nell&#39;IdP remoto come URL di reindirizzamento.
   * `defaultConnectionName`: configura con lo stesso nome definito per la connessione OIDC al passaggio precedente+
   * `pkceEnabled`: `true` PKCE (Proof Key for Code Exchange) nel flusso del codice di autorizzazione
   * `idp`: nome del [provider di identità esterna OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Diversi IDP di OAK non possono condividere utenti o gruppi

### Configurare SlingUserInfoProcessor {#configure-slinguserinfoprocessor}

1. Crea il file di configurazione. Per questo esempio, utilizzeremo `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json`. Il suffisso `azure` deve essere un identificatore univoco. Vedi un esempio del file di configurazione seguente:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false,
      "idpNameInPrincipals": true
   }
   ```

1. Quindi, configura le relative proprietà come segue:
   * `groupsInIdToken`: impostato su vero se i gruppi vengono inviati in un token ID. Se il valore è falso o non specificato, i gruppi vengono letti dall&#39;endpoint UserInfo.
   * `groupsClaimName`: il nome dell&#39;attestazione contiene i gruppi da sincronizzare in AEM.
   * `connection`: configura con lo stesso nome definito per la connessione OIDC nel passaggio precedente
   * `storeAccessToken`: vero se il token di accesso deve essere memorizzato nell&#39;archivio. Per impostazione predefinita, questo valore è falso. Imposta su vero solo se AEM deve accedere alle risorse per conto dell&#39;utente memorizzate in server esterni protetti dallo stesso IdP.
   * `storeRefreshToken`: vero se il token di aggiornamento deve essere memorizzato nell&#39;archivio. Per impostazione predefinita, questo valore è falso. Impostalo su true solo se AEM deve accedere alle risorse per conto dell’utente memorizzate in server esterni protetti dallo stesso IdP e deve aggiornare il token dall’IdP.
   * `idpNameInPrincipals`: se è impostato su true, il nome dell&#39;IdP viene aggiunto come suffisso alle entità utente e gruppo separate da un punto e virgola (;). Ad esempio, se il nome IdP è `azure-idp` e il nome utente è `john.doe`, l&#39;entità archiviata in OAK sarà `john.doe;azure-idp`. Questa funzione è utile quando in OAK sono configurati più IdP per evitare conflitti tra utenti o gruppi con lo stesso nome provenienti da IdP diversi. Questa opzione può essere impostata anche per evitare conflitti con utenti o gruppi creati da altri gestori di autenticazione come Saml.
Tieni presente che il token di accesso e il token di aggiornamento sono memorizzati come crittografati con la chiave master di AEM.


### Configurare il gestore di sincronizzazione {#configure-the-synchronization-handler}

È necessario configurare almeno un gestore di sincronizzazione per sincronizzare gli utenti autenticati in oak. Per ulteriori dettagli, consulta [questa pagina](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html).

Crea un file denominato `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. Il suffisso **azure** deve essere un identificatore univoco. Per ulteriori informazioni su come configurarne le proprietà, consulta la [documentazione sulla sincronizzazione di utenti e gruppi di Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). Di seguito trovi un esempio di configurazione:

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

Durante lo sviluppo, i tempi di scadenza possono essere ridotti a un valore inferiore (ad esempio: 1 s) per velocizzare il test della sincronizzazione di utenti e gruppi in oak.
Di seguito sono riportati alcuni degli attributi più rilevanti da configurare in DefaultSyncHandler. Tieni presente che l&#39;Iscrizione al gruppo dinamico deve essere sempre abilitata nei Cloud Service.

| Nome proprietà | Note | Valore suggerito |
|---|---|---|
| `user.expirationTime` | Durata fino alla scadenza di un utente sincronizzato. Gli utenti vengono sincronizzati solo dopo l&#39;orario di scadenza. | 1 ora |
| `user.membershipExpTime` | Durata fino alla scadenza di un&#39;iscrizione utente sincronizzata. Le iscrizioni utente vengono sincronizzate solo dopo l&#39;orario di scadenza. | 1 ora |
| `user.dynamicMembership` | È consigliabile abilitare l&#39;iscrizione al gruppo dinamico | vero |
| `user.enforceDynamicMembership` | È consigliabile abilitare l&#39;applicazione dell&#39;iscrizione a un gruppo dinamico | vero |
| `group.dynamicGroups` | È consigliabile abilitare i gruppi dinamici | vero |
| user.propertyMapping | L&#39;implementazione fornita di `UserInfoProcessor` sincronizza solo alcune proprietà. Può essere modificata e personalizzata. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=nome/profilo&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |
| `user.membershipNestingDepth` | Restituisce la profondità massima della nidificazione del gruppo quando le relazioni delle iscrizioni vengono sincronizzate. Un valore pari a 0 disattiva efficacemente la ricerca dell&#39;iscrizione al gruppo. Il valore 1 aggiunge solo i gruppi diretti di un utente. Questo valore non ha alcun effetto quando si sincronizzano singoli gruppi solo durante la sincronizzazione dell&#39;origine dell&#39;iscrizione degli utenti. | 1 |

### Configurare il Modulo di accesso esterno {#configure-the-external-login-module}

Infine, devi configurare il Modulo di accesso esterno.

1. Crea un file denominato `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json`. Vedi un esempio di configurazione di seguito:

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. Configura le relative proprietà come segue:

   * `sync.handlerName`: nome del gestore di sincronizzazione definito in precedenza
   * `idp.name`: provider di identità OAK definito nel Gestore autenticazione OIDC

### Facoltativo: implementa un UserInfoProcessor personalizzato {#implement-a-custom-userinfoprocessor}

L&#39;utente è autenticato da un token ID e gli attributi aggiuntivi vengono recuperati dall&#39;endpoint `userInfo` definito per l&#39;IdP. `UserInfoProcessor` è responsabile della trasformazione dei dati ricevuti dal provider di identità in credenziali e attributi che AEM può utilizzare per la sincronizzazione degli utenti.

#### Quando creare un UserInfoProcessor personalizzato {#when-to-create-custom-userinfoprocessor}

Il [SlingUserInfoProcessorImpl](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) predefinito gestisce le attestazioni OIDC standard e la sincronizzazione dei gruppi. Potresti aver bisogno di un’implementazione personalizzata per:

* Estrarre ed elaborare le attestazioni personalizzate dal token ID o dalla risposta UserInfo
* Trasformare o mappare attestazioni a nomi di attributi diversi
* Implementare una logica personalizzata per l’estrazione di gruppi dalle attestazioni nidificate
* Aggiungi attributi utente aggiuntivi che non fanno parte del profilo OIDC standard
* Elabora token di accesso o aggiorna token per casi d’uso specifici
* Integrazione con sistemi esterni per arricchire i dati utente durante l’autenticazione

#### Informazioni sull&#39;interfaccia UserInfoProcessor {#understanding-userinfoprocessor-interface}

L&#39;interfaccia `UserInfoProcessor` del pacchetto `org.apache.sling.auth.oauth_client.spi` definisce due metodi:

```java
public interface UserInfoProcessor {
    /**
     * Process the UserInfo and token response to create OIDC credentials
     *
     * @param userInfo - JSON response from the UserInfo endpoint (may be null)
     * @param tokenResponse - JSON response from the token endpoint
     * @param oidcSubject - The subject claim from the ID token
     * @param idp - The configured IDP name
     * @return OidcAuthCredentials containing user attributes and group memberships
     */
    @NotNull OidcAuthCredentials process(
        @Nullable String userInfo,
        @NotNull String tokenResponse,
        @NotNull String oidcSubject,
        @NotNull String idp
    );

    /**
     * @return The name of the OIDC connection this processor is associated with
     */
    @NotNull String connection();
}
```

L&#39;oggetto `OidcAuthCredentials` restituito consente di:
* Impostare gli attributi utente tramite `setAttribute(key, value)` - questi sono sincronizzati in base ai mapping di proprietà `DefaultSyncHandler`
* Aggiungi appartenenze al gruppo tramite `addGroup(groupName)` - questi gruppi vengono creati/sincronizzati in AEM

#### Esempio: implementazione personalizzata di UserInfoProcessor {#custom-userinfoprocessor-implementation}

Di seguito è riportato un esempio completo che mostra come implementare un `UserInfoProcessor` personalizzato:

```java
package com.mycompany.aem.auth;

import java.nio.charset.StandardCharsets;
import java.util.Base64;

import org.apache.sling.auth.oauth_client.spi.OidcAuthCredentials;
import org.apache.sling.auth.oauth_client.spi.UserInfoProcessor;
import org.jetbrains.annotations.NotNull;
import org.jetbrains.annotations.Nullable;
import org.osgi.service.component.annotations.Activate;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.metatype.annotations.AttributeDefinition;
import org.osgi.service.metatype.annotations.Designate;
import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

/**
 * Custom UserInfoProcessor that extracts additional claims from the ID token
 * and adds custom user attributes and group memberships.
 */
@Component(service = UserInfoProcessor.class, property = {"service.ranking:Integer=50"})
@Designate(ocd = CustomUserInfoProcessor.Config.class, factory = true)
public class CustomUserInfoProcessor implements UserInfoProcessor {

    private static final Logger logger = LoggerFactory.getLogger(CustomUserInfoProcessor.class);

    @ObjectClassDefinition(name = "Custom UserInfo Processor")
    @interface Config {
        @AttributeDefinition(name = "Connection Name", description = "OIDC Connection Name")
        String connection();
    }

    private final String connection;

    @Activate
    public CustomUserInfoProcessor(Config config) {
        this.connection = config.connection();
        logger.info("CustomUserInfoProcessor activated for connection: {}", connection);
    }

    @Override
    public @NotNull OidcAuthCredentials process(
            @Nullable String userInfo,
            @NotNull String tokenResponse,
            @NotNull String oidcSubject,
            @NotNull String idp) {

        // Parse the token response to extract tokens
        JsonObject tokenJson = JsonParser.parseString(tokenResponse).getAsJsonObject();
        String accessToken = tokenJson.has("access_token") ?
            tokenJson.get("access_token").getAsString() : null;
        String idToken = tokenJson.has("id_token") ?
            tokenJson.get("id_token").getAsString() : null;

        logger.debug("Processing authentication for subject: {}", oidcSubject);

        // Decode and extract claims from ID Token
        JsonObject claims = null;
        if (idToken != null) {
            claims = decodeJwtPayload(idToken);
            logger.debug("Extracted claims from ID token: {}", claims);
        }

        // Create credentials object
        OidcAuthCredentials credentials = new OidcAuthCredentials(oidcSubject, idp);
        credentials.setAttribute(".token", "");

        // Extract standard profile attributes
        if (claims != null) {
            // Standard OIDC claims
            setAttributeIfPresent(credentials, claims, "given_name", "profile/given_name");
            setAttributeIfPresent(credentials, claims, "family_name", "profile/family_name");
            setAttributeIfPresent(credentials, claims, "email", "profile/email");
            setAttributeIfPresent(credentials, claims, "name", "profile/name");

            // Custom claims from your IdP
            setAttributeIfPresent(credentials, claims, "department", "profile/department");
            setAttributeIfPresent(credentials, claims, "employee_id", "profile/employeeId");
            setAttributeIfPresent(credentials, claims, "job_title", "profile/jobTitle");
        }

        // Extract group memberships from claims
        if (claims != null && claims.has("groups")) {
            if (claims.get("groups").isJsonArray()) {
                claims.get("groups").getAsJsonArray().forEach(group -> {
                    credentials.addGroup(group.getAsString());
                });
            }
        }

        // Optionally store tokens if needed for later API calls
        // Note: Only store tokens if your application needs to call external APIs
        // on behalf of the user. Tokens are encrypted before storage.
        if (accessToken != null) {
            credentials.setAttribute("access_token", accessToken);
        }

        return credentials;
    }

    @Override
    public @NotNull String connection() {
        return connection;
    }

    /**
     * Helper method to set attribute if present in claims
     */
    private void setAttributeIfPresent(OidcAuthCredentials credentials,
                                      JsonObject claims,
                                      String claimName,
                                      String attributeName) {
        if (claims.has(claimName) && !claims.get(claimName).isJsonNull()) {
            String value = claims.get(claimName).getAsString();
            if (value != null && !value.isEmpty()) {
                credentials.setAttribute(attributeName, value);
            }
        }
    }

    /**
     * Decode JWT payload (middle part) to extract claims
     */
    private JsonObject decodeJwtPayload(String jwt) {
        try {
            String[] parts = jwt.split("\\.");
            if (parts.length != 3) {
                logger.warn("Invalid JWT format");
                return null;
            }

            // Decode the payload (second part)
            String payload = parts[1];
            // Add padding if needed
            payload = payload + "====".substring(0, (4 - payload.length() % 4) % 4);
            // Replace URL-safe characters
            payload = payload.replace('-', '+').replace('_', '/');

            byte[] decoded = Base64.getDecoder().decode(payload);
            String json = new String(decoded, StandardCharsets.UTF_8);
            return JsonParser.parseString(json).getAsJsonObject();
        } catch (Exception e) {
            logger.error("Failed to decode JWT payload", e);
            return null;
        }
    }
}
```

#### Configurazione {#custom-userinfoprocessor-configuration}

Crea un file di configurazione per `UserInfoProcessor` personalizzato nel progetto AEM in `ui.config/src/main/content/jcr_root/apps/myapp/osgiconfig/config.publish/`:

**com.mycompany.aem.auth.CustomUserInfoProcessor~azure.cfg.json**

```json
{
  "connection": "azure"
}
```

La configurazione deve corrispondere al nome della connessione definito nella configurazione `OidcConnectionImpl`. La proprietà `service.ranking` nell&#39;annotazione `@Component` (impostata su `50` nell&#39;esempio) determina la priorità se più processori sono registrati per la stessa connessione. Le classificazioni superiori hanno la precedenza rispetto a `SlingUserInfoProcessorImpl` (che ha una classificazione di `0`) predefinito.

#### Dipendenze {#custom-userinfoprocessor-dependencies}

Aggiungi le dipendenze seguenti a `pom.xml` del modulo core:

```xml
<dependency>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.auth.oauth-client</artifactId>
    <version>0.1.7</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.9</version>
    <scope>provided</scope>
</dependency>
```

#### Sincronizzazione degli attributi con DefaultSyncHandler {#synchronizing-custom-attributes}

Per garantire che gli attributi personalizzati vengano mantenuti nei nodi utente nel JCR, aggiorna la configurazione `DefaultSyncHandler` per includere le mappature delle proprietà:

**org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json**

```json
{
  "user.expirationTime": "1h",
  "user.membershipExpTime": "1h",
  "user.propertyMapping": [
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "profile/department=profile/department",
    "profile/employeeId=profile/employeeId",
    "profile/jobTitle=profile/jobTitle",
    "access_token=access_token"
  ],
  "user.pathPrefix": "azure",
  "handler.name": "azure"
}
```

Il formato è `jcrPropertyPath=credentialAttributeName`. Il lato sinistro è il punto in cui la proprietà viene memorizzata nel nodo utente in `/home/users` e il lato destro corrisponde al nome dell&#39;attributo impostato in `UserInfoProcessor` utilizzando `credentials.setAttribute()`.

#### Distribuzione e test {#custom-userinfoprocessor-deployment}

1. **Crea e distribuisci** il tuo progetto AEM contenente `UserInfoProcessor` personalizzato:

   ```bash
   mvn clean install -PautoInstallPackage
   ```

2. **Verifica la registrazione** nella console OSGi in `/system/console/components`:
   * Cerca il nome della classe di processore personalizzata
   * Verificare che il componente sia attivo e che la configurazione della connessione sia corretta

3. **Flusso di autenticazione di prova**:
   * Accedere a un percorso protetto configurato in `OidcAuthenticationHandler`
   * Dopo l&#39;autenticazione, controllare il nodo utente in CRXDE in `/home/users/<prefix>/<username>`
   * Verificare che gli attributi personalizzati siano sincronizzati
   * Controlla appartenenze al gruppo in `/home/groups`

4. **Abilita la registrazione di debug** per la risoluzione dei problemi:

   ```
   Logger: com.mycompany.aem.auth
   Log Level: DEBUG
   ```

#### Best practice {#custom-userinfoprocessor-best-practices}

* **Riduci al minimo l&#39;archiviazione dei token**: archivia i token di accesso o aggiorna i token solo se l&#39;applicazione deve effettuare chiamate API a servizi esterni per conto degli utenti. I token sono crittografati, ma aggiungono comunque il sovraccarico.
* **Convalida attestazioni**: verificare sempre se le attestazioni esistono e non sono nulle prima di elaborarle.
* **Gestione errori**: registrare gli errori in modo appropriato, ma assicurarsi che il flusso di autenticazione possa essere completato anche se mancano attestazioni facoltative.
* **Prestazioni**: mantenere leggera la logica di elaborazione in quanto viene eseguita su ogni autenticazione.
* **Sicurezza**: non registrare mai informazioni riservate come token completi o password utente. Usa `substring()` se registri i token per il debug.
* **Test**: esegui il test con vari profili utente dal tuo IdP per garantire che tutte le varianti di attestazione siano gestite correttamente.

### Configurare ACL per gruppi esterni {#configure-acl-for-external-groups}

Quando gli utenti vengono autenticati tramite OIDC, le appartenenze ai loro gruppi vengono in genere sincronizzate dal provider di identità esterno.
Questi gruppi esterni vengono creati in modo dinamico nell’archivio di AEM, ma non vengono associati automaticamente ad alcuna voce di controllo di accesso.
Per garantire che gli utenti dispongano delle autorizzazioni appropriate, è necessario definire in modo esplicito gli elenchi di controllo di accesso (ACL, Access Control List) per questi gruppi.

Sono disponibili due approcci primari.

### Opzione 1 — Gruppi locali

Il gruppo esterno può essere aggiunto come membro di un gruppo locale che dispone già degli ACL richiesti.

* Il gruppo esterno deve esistere nel repository, che si verifica automaticamente quando un utente appartenente a tale gruppo accede per la prima volta.
* Questa opzione è generalmente preferita quando sono in uso gruppi chiusi di utenti (CUG), in quanto il gruppo locale esiste sia nell’ambiente di authoring che in quello di pubblicazione.

### Opzione 2 — ACL diretti su gruppi esterni tramite RepoInit

Gli ACL possono essere applicati direttamente ai gruppi esterni utilizzando gli script RepoInit.

* Questo approccio è più efficiente ed è da preferirsi quando i gruppi di utenti chiusi (CUG) non vengono utilizzati.
* L&#39;esempio seguente mostra una configurazione RepoInit che assegna autorizzazioni di lettura a un gruppo esterno. L&#39;opzione `ignoreMissingPrincipal` consente la creazione dell&#39;ACL anche se il gruppo non esiste ancora nell&#39;archivio:

  ```
  {
    "scripts":[
      "set ACL for \"my-group;my-idp\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/magazine\r\nend"
    ]
  }    
  ```

>[!NOTE]
>L’interfaccia utente Autorizzazioni di AEM può essere utilizzata per verificare gli ACL assegnati alle entità del gruppo

## Esempio: configurare l&#39;autenticazione OIDC con Azure Active Directory

### Configurare una nuova applicazione in Azure Active Directory {#configure-a-new-application-in-azure-ad}

1. Crea una nuova applicazione in Azure Active Directory seguendo la [documentazione di Azure Active Directory](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Di seguito è riportata una schermata con i dettagli della panoramica dell&#39;applicazione:

   ![Panoramica dell&#39;applicazione](/help/security/assets/odic-application-overview.png)

1. Se sono necessari gruppi o ruoli di applicazione, segui la [documentazione](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) per abilitarli per l&#39;applicazione e inviarli nel token ID. Di seguito un esempio di gruppi configurati:

![ID token attestazione OIDC](/help/security/assets/oidc-claim-id-token.png)

1. Segui i passaggi documentati in precedenza per creare i file di configurazione richiesti. Di seguito è riportato un esempio specifico per Azure AD in cui:
   * Il nome della connessione oidc, del gestore di autenticazione e di DefaultSyncHandler sono definiti come: `azure`
   * L&#39;url del sito web è: `www.mywebsite.com`
   * Proteggiamo il percorso `/content/wknd/us/en/adventures` accessibile solo agli utenti autenticati membri del gruppo `adventures`
   * Il tenant è: `tennat-id`,
   * L&#39;ID client è: `client-id`,
   * Il segreto è: `secret`,
   * I gruppi vengono inviati nel token ID in un&#39;attestazione denominata: `groups`

### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email"
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

### org.apache.sling.jcr.repoinit.RepositoryInitializer~azure.cfg.json

```
{
  "scripts":[
    "set ACL for \"adventures;azure\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/adventures\r\nend"
  ]
}
```

### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### Informazioni aggiuntive sui gruppi di Azure AD {#additional-information-about-azure-ad-groups}

Per configurare un gruppo per l&#39;applicazione enterprise nel portale di Microsoft Azure, è necessario cercare l&#39;applicazione in **Applicazioni enterprise** e aggiungere i gruppi: <!-- Alexandru: this bit cound be clearer-->

![Aggiunta di un gruppo OIDC](/help/security/assets/oidc-ad-additional-info.png)

Per abilitare l&#39;attestazione di gruppo nel token ID, aggiungi l&#39;attestazione nella sezione **Configurazione token** del portale di Microsoft Azure: <!-- Alexandru: this bit cound be clearer as well-->

![ID token attestazione OIDC](/help/security/assets/oidc-claim-id-token.png)

La configurazione di `SlingUserInfoProcessor` deve essere modificata come nell&#39;esempio seguente.

Il nome file da modificare è `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`. Il contenuto deve essere configurato come segue:

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```

## Reindirizzamento personalizzato dopo l&#39;autenticazione {#custom-redirect-after-authentication}

Per impostazione predefinita, una volta completata l’autenticazione OIDC, gli utenti vengono reindirizzati all’URL richiesto originariamente. Tuttavia, è possibile personalizzare questo comportamento utilizzando il parametro di query `redirect`.

### Utilizzo del parametro di reindirizzamento

Quando si avvia l&#39;autenticazione, è possibile specificare un URL di reindirizzamento personalizzato aggiungendo il parametro `redirect` alla richiesta di autenticazione:

```
/content/wknd/us/en/adventures?redirect=/content/wknd/us/en/welcome
```

In questo esempio, dopo l&#39;autenticazione riuscita, l&#39;utente verrà reindirizzato a `/content/wknd/us/en/welcome` anziché alla pagina richiesta originariamente.

### Vincoli di sicurezza

Per motivi di sicurezza, il parametro `redirect` presenta le seguenti restrizioni:

* **Deve essere un percorso relativo**: l&#39;URL di reindirizzamento deve iniziare con `/` (ad esempio, `/content/mysite/dashboard`)
* **Nessun reindirizzamento tra siti**: gli URL assoluti (ad esempio, `https://external-site.com`) non sono consentiti
* **Nessun URL relativo al protocollo**: gli URL che iniziano con `//` vengono rifiutati per impedire reindirizzamenti relativi al protocollo

Se viene fornito un URL di reindirizzamento non valido, l’autenticazione non riuscirà e verrà restituito un errore.

### Casi d’uso di esempio

1. **Pagina di benvenuto dopo l&#39;accesso**: reindirizza gli utenti a una pagina di benvenuto personalizzata dopo il primo accesso

   ```
   /content/mysite/secure-area?redirect=/content/mysite/welcome
   ```

2. **Reindirizzamento dashboard**: reindirizzare gli utenti a un dashboard specifico dopo l&#39;autenticazione

   ```
   /content/mysite/login?redirect=/content/mysite/user/dashboard
   ```

3. **Collegamenti profondi**: consenti agli utenti di eseguire l&#39;autenticazione e quindi di accedere a una risorsa specifica

   ```
   /content/mysite/protected?redirect=/content/mysite/protected/specific-document
   ```

## Come migrare dal gestore di autenticazione Saml al gestore di autenticazione Oidc

Quando AEM è già configurato con un gestore di autenticazione SAML e gli utenti sono presenti nel repository con [sincronizzazione dati](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) abilitata, possono verificarsi conflitti tra gli utenti SAML originali e i nuovi utenti OIDC.

1. Configura [OidcAuthenticationHandler](#configure-oidc-authentication-handler) e abilita `idpNameInPrincipals` nella configurazione [SlingUserInfoProcessor](#configure-slinguserinfoprocessor)
1. Imposta [ACL per gruppi esterni](#configure-acl-for-external-groups).
1. Dopo l’accesso da parte degli utenti, è possibile eliminare i vecchi utenti creati dallo stesso gestore di autenticazione.

>[!NOTE]
>Dopo aver disabilitato il gestore di autenticazione SAML e aver abilitato il gestore di autenticazione OIDC, se [la sincronizzazione dei dati](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) non è abilitata, le sessioni esistenti non saranno più valide. Agli utenti verrà richiesto di eseguire nuovamente l’autenticazione, che determinerà la creazione di nuovi nodi utente OIDC nell’archivio.

