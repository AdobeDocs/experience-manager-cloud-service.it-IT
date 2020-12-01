---
title: 'Registrazione, login e profilo utente '
description: Informazioni su Registrazione, Accesso e Profilo utente nel livello di pubblicazione
translation-type: tm+mt
source-git-commit: 2c00c3723c3c84365044b5cd2fe6779de0360736
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Registrazione, login e profilo utente {#registration-login-and-userprofile}

## Introduzione {#introduction}

Le applicazioni Web forniscono spesso funzioni di gestione dell&#39;account per consentire agli utenti finali di registrarsi su un sito Web, il che persiste nelle informazioni sul loro profilo utente, consentendo loro di accedere in futuro e di godere di un&#39;esperienza coerente. Questo articolo descrive:

* Registrazione
* Accesso
* Memorizzazione dei dati del profilo utente
* iscrizione al gruppo
* Sincronizzazione dei dati

>[!IMPORTANT]
>
>Affinché la funzionalità descritta in questo articolo possa funzionare, è necessario abilitare la funzione di sincronizzazione dei dati utente, che in questa fase richiede una richiesta all&#39;assistenza clienti per indicare il programma e gli ambienti appropriati. Se questa opzione non è attivata, le informazioni sugli utenti verranno mantenute per un breve periodo (da 1 a 24 ore) prima di scomparire.

## Registrazione {#registration}

Quando un utente finale si registra per un account su un&#39;applicazione AEM, viene creato un account utente sul servizio AEM Publish, come si riflette su una risorsa utente in `/home/users` nell&#39;archivio JCR.

Esistono due approcci per implementare la registrazione, come descritto di seguito.

### AEM gestito {#aem-managed-registration}

Il codice di registrazione personalizzato può essere scritto che prende, in modo minimo, il nome utente e la password dell&#39;utente finale, e crea un record utente in AEM che può essere utilizzato per l&#39;autenticazione durante il login. Per creare questo meccanismo di registrazione vengono in genere utilizzati i seguenti passaggi:

1. Visualizzare un componente AEM personalizzato che raccoglie le informazioni di registrazione
1. Dopo l&#39;invio, un utente del servizio con il provisioning corretto viene utilizzato per
   1. Verificare che un utente esistente non esista già, utilizzando uno dei metodi `findAuthorizables()` dell&#39;API UserManager
   1. Creare un record utente utilizzando uno dei metodi `createUser()` dell&#39;API UserManager
   1. Mantenere qualsiasi dato di profilo acquisito utilizzando i metodi `setProperty()` dell&#39;interfaccia autorizzabile
1. Flussi opzionali, ad esempio la richiesta all&#39;utente di convalidare la propria e-mail.

### Esterno {#external-managed-registration}

In alcuni casi, la registrazione o la creazione di utenti si è già verificata in infrastrutture esterne a AEM. In questo scenario, il record utente viene creato in AEM durante l&#39;accesso.

## Accesso {#login}

Dopo che un utente finale è registrato nel servizio AEM Publish, questi utenti possono accedere per ottenere l&#39;accesso autenticato (tramite AEM meccanismi di autorizzazione) e i dati specifici dell&#39;utente persistenti, come i dati del profilo.

## Implementazione {#implementation}

Il login può essere implementato con i due approcci seguenti:

### AEM gestito {#aem-managed-implementation}

I clienti possono scrivere i propri componenti personalizzati. Per saperne di più, è consigliabile acquisire familiarità con:

* [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Inoltre, è consigliabile [chiedere agli esperti AEM community ](http://bit.ly/ATACEFeb15) informazioni sull&#39;accesso.

### Integrazione con un provider di identità {#integration-with-an-idp}

I clienti possono integrarsi con un IdP (provider di identità) che esegue l&#39;autenticazione dell&#39;utente. Le tecnologie di integrazione includono SAML e OAuth/SSO, come descritto di seguito.

**BASATO SU SAML**

I clienti possono utilizzare l&#39;autenticazione basata su SAML tramite il proprio ID SAML preferito. Quando si utilizza un IdP con AEM, l&#39;IdP è responsabile dell&#39;autenticazione delle credenziali dell&#39;utente finale e dell&#39;intermediazione dell&#39;autenticazione dell&#39;utente con AEM, della creazione del record utente in AEM secondo necessità e della gestione dell&#39;appartenenza al gruppo dell&#39;utente in AEM, come descritto dall&#39;asserzione SAML.

>[!NOTE]
>
>Solo l&#39;autenticazione iniziale delle credenziali dell&#39;utente viene autenticata dall&#39;IdP e le richieste successive a AEM vengono eseguite utilizzando un cookie di token di accesso AEM, purché il cookie sia disponibile.

Per ulteriori informazioni sul gestore di autenticazione [SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler), consultare la documentazione.

**OAuth/SSO**

Per informazioni sull&#39;utilizzo AEM servizio gestore autenticazione SSO, vedere la documentazione relativa a [Single Sign On (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html).

L&#39;interfaccia `com.adobe.granite.auth.oauth.provider` può essere implementata con il provider OAuth di vostra scelta.

### Sessioni permanenti e token incapsulati {#sticky-sessions-and-encapsulated-tokens}

AEM come Cloud Service sono abilitate le sessioni di pubblicazione basate su cookie, che garantiscono che un utente finale venga instradato sullo stesso nodo di pubblicazione per ogni richiesta. Per migliorare le prestazioni, la funzione del token incapsulato è abilitata per impostazione predefinita, pertanto non è necessario fare riferimento al record utente presente nell&#39;archivio su ogni richiesta. Se il nodo di pubblicazione per il quale un utente finale ha un&#39;affinità viene sostituito, il relativo record ID utente sarà disponibile sul nuovo nodo di pubblicazione, come descritto nella sezione di sincronizzazione dei dati seguente.

## Profilo utente {#user-profile}

Esistono vari approcci ai dati persistenti, a seconda della natura di tali dati.

### AEM repository {#aem-repository}

Le informazioni sul profilo utente possono essere scritte e lette in due modi:

* Utilizzo lato server con l&#39;interfaccia `com.adobe.granite.security.user` UserPropertiesManager dell&#39;interfaccia utente, che posizionerà i dati sotto il nodo dell&#39;utente in `/home/users`. Verificate che le pagine univoche per utente non siano memorizzate nella cache.
* Lato client che utilizza ContextHub, come descritto da [la documentazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Archiviazione di dati di terze parti {#third-party-data-stores}

I dati dell&#39;utente finale possono essere inviati a fornitori di terze parti come CRM e recuperati tramite API al momento dell&#39;accesso dell&#39;utente per AEM e persistere (o aggiornare) sul nodo del profilo dell&#39;utente AEM, e utilizzati da AEM secondo necessità.

L&#39;accesso in tempo reale ai servizi di terze parti per recuperare gli attributi del profilo è possibile, tuttavia, è importante assicurarsi che questo non influisca materialmente sull&#39;elaborazione delle richieste in AEM.

## Autorizzazioni (gruppi di utenti chiusi) {#permissions-closed-user-groups}

I criteri di accesso al livello di pubblicazione, denominati anche Gruppi di utenti chiusi (CUG), sono definiti nell&#39;autore AEM come [descritti qui](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Per limitare determinate sezioni o pagine di un sito Web da parte di alcuni utenti, applicate i CUG in base alle esigenze utilizzando l’autore AEM, come descritto qui, e replicateli sul livello di pubblicazione.

* Se gli utenti accedono autenticandosi con un provider di identità (IdP) utilizzando SAML, il gestore di autenticazione identificherà le appartenenze del gruppo dell&#39;utente (che devono corrispondere ai CUG nel livello di pubblicazione) e persisterà l&#39;associazione tra l&#39;utente e il gruppo attraverso un record del repository
* Se l&#39;accesso viene eseguito senza l&#39;integrazione con IdP, il codice personalizzato può applicare le stesse relazioni di struttura del repository.

Indipendentemente dall’accesso, il codice personalizzato può anche persistere e gestire le appartenenze a un gruppo di utenti, in base alle esigenze specifiche di un’organizzazione.

## Sincronizzazione dati {#data-synchronization}

Gli utenti finali del sito Web si aspettano un&#39;esperienza coerente su ogni richiesta di pagina Web o anche quando accedono utilizzando un browser diverso, anche se non li conoscono, vengono portati a nodi server differenti dell&#39;infrastruttura del livello di pubblicazione. AEM come Cloud Service, questo avviene sincronizzando rapidamente la gerarchia di cartelle `/home` (informazioni sul profilo utente, appartenenza al gruppo, ecc.) tra tutti i nodi del livello di pubblicazione.

A differenza di altre soluzioni AEM, la sincronizzazione di membri di utenti e gruppi in AEM come Cloud Service non utilizza un approccio di messaggistica point-to-point, ma implementa un approccio di iscrizione a pubblicazione che non richiede la configurazione del cliente.

>[!NOTE]
>
>Per impostazione predefinita, la sincronizzazione del profilo utente e dell’appartenenza al gruppo non è abilitata e pertanto i dati non saranno sincronizzati o persistenti sul livello di pubblicazione. Per abilitare questa funzione, inviare una richiesta all&#39;Assistenza clienti indicando il programma e gli ambienti appropriati.

## Considerazioni sulla cache {#cache-considerations}

Le richieste HTTP autenticate possono essere difficili da memorizzare nella cache sia sul CDN che sul dispatcher, poiché comportano la possibilità che lo stato specifico dell&#39;utente venga trasferito come parte della risposta della richiesta. Se si memorizzano inavvertitamente nella cache le richieste autenticate e le si distribuiscono ad altri browser richiedenti, è possibile che si verifichino esperienze errate, o persino che i dati protetti o degli utenti vengano persi.

Gli approcci per mantenere un&#39;elevata capacità di memorizzazione nella cache delle richieste e supportare le risposte specifiche dell&#39;utente includono:

* AEM Dispatcher Permissions nella cache sensibile
* Sling Dynamic Include
* AEM ContextHub