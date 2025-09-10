---
title: Supporto OpenID Connect per AEM as a Cloud Service sul livello di pubblicazione
description: Scopri come configurare Open ID Connect (OIDC) per AEM as a Cloud Service sul livello di pubblicazione
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: f3cd1bc761c513ebb85351185e7aa0b6f6eb6f33
workflow-type: ht
source-wordcount: '1469'
ht-degree: 100%

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
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. Configura le relative proprietà come segue:
   * **&quot;name&quot;** può essere definito dall&#39;utente
   * `baseUrl`, `clientid` e `clientSecret` sono valori di configurazione provenienti dall&#39;IdP.
   * Gli ambiti devono contenere almeno il valore `openid`.

### Configurare il Gestore autenticazione OIDC {#configure-oidc-authentication-handler}

Ora configura il gestore di autenticazione OIDC. È possibile configurare più connessioni OIDC. Ognuna deve avere un nome diverso. Se condividono lo stesso [Provider di identità esterno OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html), possono condividere gli utenti.

1. Crea il file di configurazione. Per questo esempio, utilizzeremo `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`. Il suffisso `azure` deve essere un identificatore univoco. Vedi un esempio del file di configurazione seguente:

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
   * `callbackUri`: verso il percorso da proteggere, aggiunta del suffisso: `/j_security_check`
   * `defaultConnectionName`: configura con lo stesso nome definito per la connessione OIDC al passaggio precedente+
   * `pkceEnabled`: `true` PKCE (Proof Key for Code Exchange) nel flusso del codice di autorizzazione
   * `idp`: nome del [provider di identità esterna OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Diversi IDP di OAK non possono condividere utenti o gruppi

### Configurare SlingUserInfoProcessor

1. Crea il file di configurazione. Per questo esempio, utilizzeremo `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`. Il suffisso `azure` deve essere un identificatore univoco. Vedi un esempio del file di configurazione seguente:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. Quindi, configura le relative proprietà come segue:
   * `groupsInIdToken`: impostato su vero se i gruppi vengono inviati in un token ID. Se il valore è falso o non specificato, i gruppi vengono letti dall&#39;endpoint UserInfo.
   * `groupsClaimName`: il nome dell&#39;attestazione contiene i gruppi da sincronizzare in AEM.
   * `connection`: configura con lo stesso nome definito per la connessione OIDC nel passaggio precedente
   * `storeAccessToken`: vero se il token di accesso deve essere memorizzato nell&#39;archivio. Per impostazione predefinita, questo valore è falso. Imposta su vero solo se AEM deve accedere alle risorse per conto dell&#39;utente memorizzate in server esterni protetti dallo stesso IdP.
   * `storeRefreshToken`: vero se il token di aggiornamento deve essere memorizzato nell&#39;archivio. Per impostazione predefinita, questo valore è falso. Impostalo su vero solo se AEM deve accedere alle risorse per conto dell&#39;utente memorizzate in server esterni protetti dallo stesso IdP e deve aggiornare il token dall&#39;IdP.
Tieni presente che il token di accesso e il token di aggiornamento sono memorizzati come crittografati con la chiave master di AEM.


### Configurare il gestore di sincronizzazione {#configure-the-synchronization-handler}

È necessario configurare almeno un gestore di sincronizzazione per sincronizzare gli utenti autenticati in oak. Per ulteriori dettagli, consulta [questa pagina](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html).

Crea un file denominato `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. Il suffisso **azure** deve essere un identificatore univoco. Per ulteriori informazioni su come configurarne le proprietà, consulta la [documentazione sulla sincronizzazione di utenti e gruppi di Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). Di seguito trovi un esempio di configurazione:

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

Di seguito sono riportati alcuni degli attributi più rilevanti da configurare in DefaultSyncHandler. Tieni presente che l&#39;Iscrizione al gruppo dinamico deve essere sempre abilitata nei Cloud Service.

| Nome proprietà | Note | Valore suggerito |
|---|---|---|
| `user.expirationTime` | Durata fino alla scadenza di un utente sincronizzato. Gli utenti vengono sincronizzati solo dopo l&#39;orario di scadenza. | 1 ora |
| `user.membershipExpTime` | Durata fino alla scadenza di un&#39;iscrizione utente sincronizzata. Le iscrizioni utente vengono sincronizzate solo dopo l&#39;orario di scadenza. | 1 ora |
| `user.dynamicMembership` | È consigliabile abilitare l&#39;iscrizione al gruppo dinamico | vero |
| `user.enforceDynamicMembership` | È consigliabile abilitare l&#39;applicazione dell&#39;iscrizione a un gruppo dinamico | vero |
| `group.dynamicGroups` | È consigliabile abilitare i gruppi dinamici | vero |
| user.propertyMapping | L&#39;implementazione fornita di `UserInfoProcessor` sincronizza solo alcune proprietà. Può essere modificata e personalizzata. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=nome/profilo&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
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

L&#39;utente è autenticato da un token ID e gli attributi aggiuntivi vengono recuperati nell&#39;endpoint `userInfo` definito per l&#39;IdP. Se è necessario eseguire altre operazioni non standard, l&#39;implementazione predefinita di Sling è un&#39;implementazione personalizzata di [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java).

## Esempio: configurare l&#39;autenticazione OIDC con Azure Active Directory

### Configurare una nuova applicazione in Azure Active Directory {#configure-a-new-application-in-azure-ad}

1. Crea una nuova applicazione in Azure Active Directory seguendo la [documentazione di Azure Active Directory](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Di seguito è riportata una schermata con i dettagli della panoramica dell&#39;applicazione:

   ![Panoramica dell&#39;applicazione](/help/security/assets/odic-application-overview.png)

1. Se sono necessari gruppi o ruoli di applicazione, segui la [documentazione](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) per abilitarli per l&#39;applicazione e inviarli nel token ID. Di seguito un esempio di gruppi configurati:

![ID token attestazione OIDC](/help/security/assets/oidc-claim-id-token.png)

1. Segui i passaggi documentati in precedenza per creare i file di configurazione richiesti. Di seguito è riportato un esempio specifico per Azure AD in cui:
   * Il nome della connessione oidc, del gestore di autenticazione e di DefaultSyncHandler sono definiti come: `azure`
   * L&#39;url del sito web è: `www.mywebsite.com`
   * Il percorso `/content/wknd/us/en/adventures` è protetto
   * Il tenant è: `tennat-id`,
   * L&#39;ID client è: `client-id`,
   * Il segreto è: `secret`,
   * I gruppi vengono inviati nel token ID in un&#39;attestazione denominata: `groups`

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

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

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
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

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

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
