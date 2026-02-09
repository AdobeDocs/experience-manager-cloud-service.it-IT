---
title: Registrazione, accesso e profilo utente
description: Scopri di più su Registrazione, Accesso, Dati utente e Sincronizzazione dei gruppi per AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 3cc787fe9a0be9a687f7c20744d93f1df4b76f87
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 58%

---

# Registrazione, accesso e profilo utente {#registration-login-and-userprofile}

## Introduzione {#introduction}

Le applicazioni Web spesso forniscono funzioni di gestione dell&#39;account per gli utenti finali che si registrano su un sito Web; in questo modo le informazioni sui dati dell&#39;utente vengono conservate, consentendo loro di effettuare l&#39;accesso in futuro e di godere di un&#39;esperienza coerente. Questo articolo descrive i seguenti concetti per AEM as a Cloud Service:

* Registrazione
* Accesso
* Memorizzazione dei dati del profilo utente
* Iscrizione a gruppi
* Sincronizzazione dati

## Registrazione {#registration}

Quando un utente registra un account su un&#39;applicazione AEM, viene creato un account utente sul servizio AEM Publish, come riportato in una risorsa utente in `/home/users` nell’archivio JCR.

Esistono due approcci per implementare la registrazione, come descritto di seguito.

### AEM Managed {#aem-managed-registration}

È possibile scrivere un codice di registrazione personalizzato che accetta, come minimo, il nome utente e la password dell’utente e crea un record utente in AEM che può essere utilizzato per l’autenticazione durante l’accesso. i passaggi di questo meccanismo di registrazione sono:

1. Visualizza un componente AEM personalizzato che raccoglie le informazioni sulla registrazione
1. Dopo l’invio, un utente del servizio con provisioning appropriato viene utilizzato per
   1. Verificare che un utente esistente non sia già registrato, utilizzando uno dei metodi`findAuthorizables()` delle API di UserManager 
   1. Creare un record utente utilizzando uno dei metodi`createUser()` delle API UserManager 
   1. Mantenere i dati del profilo acquisiti tramite i metodi`setProperty()` dell&#39;interfaccia Authorizable
1. Flussi facoltativi, ad esempio per richiedere all’utente di convalidare la propria e-mail.

**Prerequisito:**

Affinché la logica sopra descritta funzioni correttamente, abilita la [sincronizzazione dei dati](#data-synchronization-data-synchronization) inviando
una richiesta all’Assistenza clienti che indica il programma e gli ambienti appropriati.

### Esterno {#external-managed-registration}

In alcuni casi, la registrazione o la creazione di un utente si sono verificate in precedenza in infrastrutture al di fuori di AEM. In questo scenario, il record utente viene creato in AEM durante l&#39;accesso.

## Accesso {#login}

Una volta che un utente finale è registrato sul servizio AEM Publish, può effettuare il login per un accesso autenticato (utilizzando i meccanismi di autorizzazione di AEM) e salvare i dati specifici dell&#39;utente, come i dati del profilo.

## Implementazione {#implementation}

L’accesso può essere implementato con i due approcci seguenti:

### AEM Managed {#aem-managed-implementation}

I clienti possono creare i propri componenti personalizzati. Per saperne di più, acquisisci familiarità con:

* Il [Framework di autenticazione Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* E considera di [chiedere agli esperti della community AEM](https://bit.ly/ATACEFeb15) informazioni sull’accesso.

**Prerequisito:**

Affinché la logica sopra descritta funzioni correttamente, abilita la [sincronizzazione dei dati](#data-synchronization-data-synchronization) inviando
una richiesta all’Assistenza clienti che indica il programma e gli ambienti appropriati.

### Integrazione con un provider di identità {#integration-with-an-idp}

I clienti possono integrarsi con un IdP (provider di identità) che autentica l’utente. Le tecnologie di integrazione includono SAML e OAuth/SSO, come descritto di seguito.

**BASATO SU SAML**

I clienti possono utilizzare l’autenticazione basata su SAML tramite il proprio IDP SAML preferito. Quando si utilizza un IdP con AEM, l&#39;IdP è responsabile dell&#39;autenticazione delle credenziali dell&#39;utente e dell&#39;intermediazione dell&#39;autenticazione dell&#39;utente con AEM, della creazione del record utente in AEM in base alle esigenze e della gestione dell&#39;iscrizione dell&#39;utente al gruppo in AEM, come descritto dall&#39;asserzione SAML.

>[!NOTE]
>
>Solo l’autenticazione iniziale delle credenziali dell’utente viene autenticata dall’IdP e le richieste successive a AEM vengono eseguite utilizzando un cookie token di accesso AEM, purché il cookie sia disponibile.

Consulta la documentazione per ulteriori informazioni sul [Gestore autenticazione SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=it).

**OAuth/SSO**

Consulta la [documentazione Single Sign On (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html?lang=it) per informazioni sull&#39;utilizzo del servizio di gestione dell&#39;autenticazione SSO di AEM.

L’interfaccia`com.adobe.granite.auth.oauth.provider` può essere integrata con il provider OAuth desiderato.

**Prerequisito:**

Come best practice, considera sempre l’idP (Identity Provider) come un singolo punto di verità per l’archiviazione di dati specifici dell’utente. Se le informazioni utente aggiuntive sono memorizzate nell&#39;archivio locale, che non fa parte dell&#39;idP, abilitare la [sincronizzazione dati](#data-synchronization-data-synchronization) inviando una richiesta all&#39;Assistenza clienti indicando il programma e gli ambienti appropriati. Oltre alla [sincronizzazione dati](#data-synchronization-data-synchronization), nel caso del provider di autenticazione SAML verificare che sia abilitata l&#39;appartenenza al gruppo dinamico [&#128279;](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/authentication/saml-2-0).

### Sessioni permanenti e token incapsulati {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service abilita sessioni permanenti basate su cookie, garantendo che un utente finale venga indirizzato allo stesso nodo di pubblicazione su ogni richiesta. In casi particolari, come i picchi di traffico degli utenti, la funzione del token incapsulato potrebbe migliorare le prestazioni, pertanto non è necessario fare riferimento al record utente nell’archivio a ogni richiesta. Se viene sostituito il nodo di pubblicazione con cui un utente finale ha un&#39;affinità, il record del relativo ID utente sarà disponibile nel nuovo nodo di pubblicazione, come descritto nella sezione [sincronizzazione dati](#data-synchronization-data-synchronization) seguente.

Per sfruttare la funzione del token incapsulato, invia una richiesta all’Assistenza clienti indicando il programma e gli ambienti appropriati. Un aspetto ancora più importante è che il token incapsulato non può essere abilitato senza [sincronizzazione dati](#data-synchronization-data-synchronization) e deve essere abilitato insieme. Pertanto, rivedi attentamente il caso d’uso prima di abilitarlo e assicurati che la funzione sia essenziale.

## Profilo utente {#user-profile}

Esistono diversi approcci ai dati persistenti, a seconda della natura di tali dati.

### Archivio AEM {#aem-repository}

Le informazioni sul profilo utente possono essere scritte e lette in due modi:

* Utilizzo lato server con `com.adobe.granite.security.user` Interfaccia UserPropertiesManager, che inserirà i dati sotto il nodo dell&#39;utente in `/home/users`. Assicurati che le pagine univoche per utente non siano memorizzate nella cache.
* Lato client che utilizza ContextHub, come descritto [nella documentazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=it#personalization).

**Prerequisito:**

Per il corretto funzionamento della logica di persistenza del profilo utente lato server, abilitare [sincronizzazione dati](#data-synchronization-data-synchronization) inviando
una richiesta all’Assistenza clienti che indica il programma e gli ambienti appropriati.

### Archiviazione dati di terze parti {#third-party-data-stores}

I dati dell’utente finale possono essere inviati a fornitori di terze parti come CRM, recuperati tramite API al momento dell’accesso dell’utente a AEM, memorizzati (o aggiornati) sul nodo del profilo dell’utente AEM, e utilizzati in base alle esigenze.

È possibile accedere in tempo reale a servizi di terzi per recuperare gli attributi del profilo, tuttavia, è importante assicurarsi che questo non influisca materialmente sull’elaborazione delle richieste in AEM.

**Prerequisito:**

Affinché la logica sopra descritta funzioni correttamente, abilita la [sincronizzazione dei dati](#data-synchronization-data-synchronization) inviando
una richiesta all’Assistenza clienti che indica il programma e gli ambienti appropriati.

## Autorizzazioni (gruppi di utenti chiusi) {#permissions-closed-user-groups}

I criteri di accesso al livello di pubblicazione, denominati anche gruppi utenti chiusi, sono definiti nell&#39;autore di AEM. Vedere [Creazione di un gruppo utenti chiuso](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=it#applying-your-closed-user-group-to-content-pages). Per limitare alcune sezioni o pagine di un sito Web a determinati utenti, applica i CUG necessari utilizzando l’autore AEM, come descritto qui, e replicali sul livello di pubblicazione.

* Se gli utenti effettuano l&#39;accesso autenticandosi con un provider di identità (IdP) utilizzando SAML, il gestore di autenticazione identificherà l&#39;iscrizione degli utenti a gruppi (che devono corrispondere ai CUG sul livello di pubblicazione) e manterrà l&#39;associazione tra utente e gruppo attraverso un record dell&#39;archivio
* Se l&#39;accesso viene eseguito senza l&#39;integrazione IdP, il codice personalizzato può applicare le stesse relazioni di struttura dell&#39;archivio.

Indipendentemente dall’accesso, il codice personalizzato può anche persistere e gestire l&#39;iscrizione dell&#39;utente a un gruppo in base ai requisiti specifici di un’organizzazione.

## Sincronizzazione dati {#data-synchronization}

Gli utenti finali dei siti Web si aspettano un&#39;esperienza coerente a ogni richiesta di pagina o anche quando accedono utilizzando un altro browser, anche se a loro insaputa vengono portati su nodi server diversi dell&#39;infrastruttura a livello di pubblicazione. AEM as a Cloud Service esegue questa operazione sincronizzando rapidamente la gerarchia di cartelle `/home` (informazioni sul profilo utente, appartenenza al gruppo e così via) in tutti i nodi del livello di pubblicazione.

A differenza di altre soluzioni AEM, la sincronizzazione di utenti e iscrizione a gruppi in AEM as a Cloud Service non utilizza un approccio di messaggistica point-to-point, ma implementa un approccio publish-subscribe che non richiede la configurazione del cliente.

>[!NOTE]
>
>Per impostazione predefinita, la sincronizzazione di profilo utente e iscrizione a gruppi non è abilitata e pertanto i dati non verranno sincronizzati o memorizzati in modo permanente sul livello di pubblicazione. Per abilitare questa funzione, invia una richiesta all’Assistenza clienti indicando il programma e gli ambienti appropriati.

>[!IMPORTANT]
>
>Esegui il test dell’implementazione su larga scala prima di abilitare la sincronizzazione dei dati nell’ambiente di produzione. A seconda del caso d’uso e della persistenza dei dati, potrebbero verificarsi alcuni problemi di coerenza e latenza.

### Codice personalizzato e requisiti di migrazione {#custom-code-and-migration-requirements}

I seguenti requisiti si applicano solo nei casi in cui viene utilizzato codice personalizzato per creare utenti o gruppi locali. Quando Sincronizzazione dati è abilitata, tale codice personalizzato deve essere aggiornato per creare utenti e gruppi esterni con appartenenza a gruppi dinamici.

**Passaggi richiesti:**

* **Modifiche al codice personalizzato**: qualsiasi logica personalizzata responsabile della creazione di utenti o gruppi deve essere aggiornata a:

   * Creare utenti esterni impostando la proprietà `rep:externalId`
   * Creare gruppi esterni impostando la proprietà `rep:externalId`
   * Implementare l&#39;appartenenza a un gruppo dinamico utilizzando la proprietà `rep:externalPrincipalNames` anziché le relazioni dirette tra utenti e gruppi

* **Migrazione di dati preesistenti**: tutti gli utenti e i gruppi locali esistenti devono essere migrati al modello di identità esterna prima che la sincronizzazione dei dati sia abilitata negli ambienti di produzione.

Per istruzioni tecniche dettagliate sull&#39;aggiornamento delle implementazioni personalizzate e sulla migrazione di utenti e gruppi esistenti, consulta [Migrazione a identità esterna e appartenenza a gruppo dinamico](/help/security/migrating-to-external-identity.md).

## Considerazioni sulla cache {#cache-considerations}

Le richieste HTTP autenticate possono essere difficili da memorizzare in cache sia sulla CDN che sul Dispatcher, in quanto comportano la possibilità che lo stato specifico dell’utente venga trasferito come parte della risposta della richiesta. Memorizzare involontariamente nella cache le richieste autenticate e distribuirle ad altri browser richiedenti può causare esperienze inadeguate o anche la perdita di dati protetti o utente.

Gli approcci per mantenere un&#39;elevata capacità di cache delle richieste e supportare le risposte specifiche dell&#39;utente includono:

* Autorizzazioni AEM Dispatcher sensibili alla cache
* Sling Dynamic Include
* AEM ContextHub
