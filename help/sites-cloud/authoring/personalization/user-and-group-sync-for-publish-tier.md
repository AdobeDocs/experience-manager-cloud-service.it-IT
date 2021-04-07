---
title: 'Registrazione, accesso e profilo utente '
description: Scopri Registrazione, Accesso, Dati utente e Sincronizzazione di gruppo per AEM come Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
translation-type: tm+mt
source-git-commit: 4d76d8bac41e19168abb1819841dfc62be07ea0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Registrazione, accesso e profilo utente {#registration-login-and-userprofile}

## Introduzione {#introduction}

Le applicazioni web forniscono spesso funzioni di gestione dell’account che consentono agli utenti finali di registrarsi su un sito web e che persistono le informazioni sui dati utente, consentendo loro di accedere in futuro e di godere di un’esperienza coerente. Questo articolo descrive i seguenti concetti per AEM come Cloud Service:

* Registrazione
* Accesso
* Memorizzazione dei dati del profilo utente
* Iscrizione al gruppo
* Sincronizzazione dati

>[!IMPORTANT]
>
>Affinché la funzionalità descritta in questo articolo funzioni, è necessario abilitare la funzione Sincronizzazione dati utente, che al momento richiede una richiesta al supporto clienti per indicare il programma e gli ambienti appropriati. Se non è abilitata, le informazioni utente verranno mantenute per un breve periodo (da 1 a 24 ore) prima di scomparire.

## Registrazione {#registration}

Quando un utente finale si registra per un account su un&#39;applicazione AEM, viene creato un account utente sul servizio AEM Publish, come riportato su una risorsa utente in `/home/users` nell&#39;archivio JCR.

Esistono due approcci per implementare la registrazione, come descritto di seguito.

### AEM gestito {#aem-managed-registration}

Il codice di registrazione personalizzato può essere scritto che prende, minimamente, il nome utente e la password dell&#39;utente finale, e crea un record utente in AEM che può poi essere utilizzato per l&#39;autenticazione durante l&#39;accesso. I seguenti passaggi vengono generalmente utilizzati per creare questo meccanismo di registrazione:

1. Visualizza un componente AEM personalizzato che raccoglie le informazioni sulla registrazione
1. Dopo l’invio, un utente di servizio con provisioning appropriato viene utilizzato per
   1. Verifica che un utente esistente non esista già, utilizzando uno dei metodi `findAuthorizables()` dell&#39;API UserManager
   1. Creare un record utente utilizzando uno dei metodi `createUser()` dell&#39;API UserManager
   1. Mantieni i dati del profilo acquisiti utilizzando i metodi `setProperty()` dell’interfaccia autorizzabile
1. Flussi facoltativi, ad esempio per richiedere all’utente di convalidare la propria e-mail.

### Esterno {#external-managed-registration}

In alcuni casi, la registrazione o la creazione di utenti si è verificata in precedenza in infrastrutture al di fuori di AEM. In questo scenario, il record utente viene creato in AEM durante l&#39;accesso.

## Accesso {#login}

Una volta registrato un utente finale sul servizio AEM Publish, questi utenti possono accedere per avere accesso autenticato (utilizzando AEM meccanismi di autorizzazione) e dati persistenti specifici dell’utente, come i dati del profilo.

## Implementazione {#implementation}

L’accesso può essere implementato con i due approcci seguenti:

### AEM gestito {#aem-managed-implementation}

I clienti possono scrivere i propri componenti personalizzati. Per saperne di più, è consigliabile acquisire familiarità con:

* [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Inoltre, considera la possibilità di [chiedere informazioni sull&#39;accesso alla sessione AEM Community Experts](http://bit.ly/ATACEFeb15) .

### Integrazione con un provider di identità {#integration-with-an-idp}

I clienti possono integrarsi con un IdP (provider di identità) che autentica l’utente. Le tecnologie di integrazione includono SAML e OAuth/SSO, come descritto di seguito.

**BASATO SU SAML**

I clienti possono utilizzare l’autenticazione basata su SAML tramite il proprio IDP SAML preferito. Quando si utilizza un IdP con AEM, l&#39;IdP è responsabile dell&#39;autenticazione delle credenziali dell&#39;utente finale e dell&#39;intermediazione dell&#39;autenticazione dell&#39;utente con AEM, della creazione del record utente in AEM secondo necessità e della gestione dell&#39;appartenenza al gruppo dell&#39;utente in AEM, come descritto dall&#39;asserzione SAML.

>[!NOTE]
>
>Solo l’autenticazione iniziale delle credenziali dell’utente viene autenticata dall’IdP e le richieste successive a AEM vengono eseguite utilizzando un cookie di token di accesso AEM, purché il cookie sia disponibile.

Consulta la documentazione per ulteriori informazioni sul [Gestore autenticazione SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler).

**OAuth/SSO**

Per informazioni sull&#39;utilizzo del servizio Gestore autenticazione AEM SSO, consulta la documentazione [Single Sign On (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) .

Puoi implementare l’interfaccia `com.adobe.granite.auth.oauth.provider` con il provider OAuth desiderato.

### Sessioni permanenti e token incapsulati {#sticky-sessions-and-encapsulated-tokens}

AEM come Cloud Service dispone di sessioni permanenti basate su cookie abilitate, che garantiscono che un utente finale venga indirizzato allo stesso nodo di pubblicazione su ogni richiesta. Per migliorare le prestazioni, la funzione del token incapsulato è abilitata per impostazione predefinita, pertanto non è necessario fare riferimento al record utente nell’archivio su ogni richiesta. Se viene sostituito il nodo di pubblicazione a cui un utente finale ha un&#39;affinità, il record del relativo ID utente sarà disponibile sul nuovo nodo di pubblicazione, come descritto nella sezione di sincronizzazione dei dati seguente.

## Profilo utente {#user-profile}

Esistono diversi approcci ai dati persistenti, a seconda della natura di tali dati.

### Archivio AEM {#aem-repository}

Le informazioni sul profilo utente possono essere scritte e lette in due modi:

* Uso lato server con l&#39;interfaccia `com.adobe.granite.security.user` UserPropertiesManager dell&#39;interfaccia, che inserisce i dati sotto il nodo dell&#39;utente in `/home/users`. Assicurati che le pagine univoche per utente non siano memorizzate nella cache.
* Lato client che utilizza ContextHub, come descritto da [la documentazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Archiviazione di dati di terze parti {#third-party-data-stores}

I dati dell’utente finale possono essere inviati a fornitori di terze parti come CRM e recuperati tramite API al momento dell’accesso dell’utente a AEM e memorizzati (o aggiornati) sul nodo del profilo dell’utente AEM, e utilizzati da AEM in base alle esigenze.

È possibile accedere in tempo reale a servizi di terze parti per recuperare gli attributi del profilo, tuttavia è importante assicurarsi che questo non influisca in modo rilevante sull’elaborazione delle richieste in AEM.

## Autorizzazioni (gruppi di utenti chiusi) {#permissions-closed-user-groups}

I criteri di accesso al livello di pubblicazione, denominati anche gruppi di utenti chiusi (CUG), sono definiti nell’autore AEM come [descritto qui](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Per limitare alcune sezioni o pagine di un sito web a determinati utenti, applica i CUG necessari utilizzando l’autore AEM, come descritto qui, e replicali sul livello di pubblicazione.

* Se gli utenti effettuano l&#39;accesso autenticandosi con un provider di identità (IdP) utilizzando SAML, il gestore di autenticazione identificherà le appartenenze al gruppo dell&#39;utente (che devono corrispondere ai CUG sul livello di pubblicazione) e persisterà l&#39;associazione tra l&#39;utente e il gruppo attraverso un record del repository
* Se l&#39;accesso viene eseguito senza l&#39;integrazione IdP, il codice personalizzato può applicare le stesse relazioni di struttura dell&#39;archivio.

Indipendentemente dall’accesso, il codice personalizzato può anche persistere e gestire le appartenenze a un gruppo di utenti in base ai requisiti specifici di un’organizzazione.

## Sincronizzazione dati {#data-synchronization}

Gli utenti finali del sito web si aspettano un’esperienza coerente su ogni richiesta di pagina web o anche quando effettuano l’accesso utilizzando un browser diverso, anche se non sono a loro conoscenza, vengono portati a diversi nodi server dell’infrastruttura del livello di pubblicazione. AEM come Cloud Service esegue questa operazione sincronizzando rapidamente la gerarchia delle cartelle `/home` (informazioni sul profilo utente, appartenenza al gruppo, ecc.) in tutti i nodi del livello di pubblicazione.

A differenza di altre soluzioni AEM, la sincronizzazione dell’appartenenza di utenti e gruppi in AEM come Cloud Service non utilizza un approccio di messaggistica punto-to-point, ma implementa un approccio di pubblicazione-sottoscrizione che non richiede la configurazione del cliente.

>[!NOTE]
>
>Per impostazione predefinita, la sincronizzazione del profilo utente e dell’appartenenza al gruppo non è abilitata e pertanto i dati non verranno sincronizzati o persistono in modo permanente sul livello di pubblicazione. Per abilitare questa funzione, invia una richiesta all’Assistenza clienti indicando il programma e gli ambienti appropriati.

## Considerazioni sulla cache {#cache-considerations}

Le richieste HTTP autenticate possono essere difficili da memorizzare in cache sia sulla CDN che sul Dispatcher, in quanto comportano la possibilità che lo stato specifico dell’utente venga trasferito come parte della risposta della richiesta. Memorizzare involontariamente nella cache le richieste autenticate e distribuirle ad altri browser richiedenti può causare esperienze errate o anche la perdita di dati protetti o utente.

Gli approcci per mantenere un&#39;elevata capacità di cache delle richieste e supportare le risposte specifiche dell&#39;utente includono:

* Memorizzazione in cache sensibile AEM autorizzazioni di Dispatcher
* Sling Dynamic Include
* AEM ContextHub
