---
title: Supporto IMS per Adobe Experience Manager as a Cloud Service
description: Supporto IMS per Adobe Experience Manager as a Cloud Service
translation-type: tm+mt
source-git-commit: d51d0e8c57a4c3d3af3083c58a4c1510869c5604

---


# Supporto IMS per Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introduzione {#introduction}

* AEM as a Cloud Service include il supporto Admin Console per le istanze AEM e l’autenticazione basata su Adobe IMS (Identity Management System).
* Admin Console consente agli amministratori di gestire tutti gli utenti di Experience Cloud da una posizione centralizzata.
* Gli utenti e i gruppi possono essere assegnati a profili di prodotto associati a istanze di AEM as a Cloud Service, per consentire loro di accedere a tale istanza.

## Elementi di rilievo {#key-highlights}

AEM as a Cloud Service offre il supporto per l’autenticazione IMS solo per gli utenti con privilegi di autore, amministratore e sviluppatore, e non per gli utenti finali esterni che visitano i siti dei clienti.

* In Admin Console i clienti saranno rappresentati come organizzazioni IMS, mentre le istanze di authoring e pubblicazione di un ambiente saranno rappresentate come istanze del contesto di prodotto. In questo modo gli amministratori di sistema e di prodotto potranno gestire l’accesso alle istanze.
* I profili di prodotto in Admin Console determinano le istanze accessibili a un determinato utente.
* Per l’accesso Single Sign-On i clienti potranno utilizzare provider di identità (IDP) personali conformi a SAML 2.
* Per l’accesso Single Sign-On dei clienti saranno supportati solo Enterprise ID o Federated ID e non gli Adobe ID personali.

## Architettura {#architecture}

Per l’autenticazione IMS viene utilizzato il protocollo OAuth tra AEM e l’endpoint Adobe IMS. Dopo essere stato aggiunto a IMS, un utente con Adobe ID può accedere al servizio authoring di AEM utilizzando le sue credenziali IMS.

Come illustrato nella figura seguente, relativa al flusso dell’accesso utente, l’utente verrà reindirizzato a IMS ed eventualmente all’IDP del cliente per l’accesso SSO e quindi reindirizzato nuovamente ad AEM.

![Architettura di IMS](/help/security/assets/ims1.png)

## Configurazione {#how-to-set-up}

### Onboarding di organizzazioni in Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

L’onboarding del cliente in Adobe Admin Console costituisce un prerequisito per l’utilizzo di Adobe IMS per l’autenticazione in AEM.

In primo luogo, è necessario aver effettuato il provisioning di un’organizzazione per i clienti in Adobe IMS. I clienti Adobe Enterprise sono rappresentati come organizzazioni IMS in [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html), ovvero il portale utilizzato dai clienti Adobe per gestire le adesioni dei prodotti per i propri utenti e gruppi.

Quando si effettua il provisioning di un’organizzazione per i clienti AEM in IMS, le istanze dei clienti diventeranno disponibili in Admin Console e sarà possibile gestire le adesioni e l’accesso utente.

Una volta predisposta l’organizzazione IMS, il cliente dovrà configurare il proprio sistema come riepilogato di seguito:

![Onboarding in IMS](/help/security/assets/ims2.png)

1. L’amministratore di sistema designato riceve un invito ad accedere a Cloud Manager. Dopo aver effettuato l’accesso a Cloud Manager, gli amministratori di sistema possono scegliere se effettuare il provisioning di programmi e ambienti AEM oppure passare ad Admin Console per eseguire attività amministrative.
1. L’amministratore di sistema richiede un dominio per confermare la proprietà del rispettivo dominio, ad esempio acme.com.
1. L’amministratore di sistema configura le directory utente.
1. L’amministratore di sistema esegue la configurazione IDP in Admin Console per configurare l’accesso Single Sign-On.
1. L’amministratore AEM gestisce i gruppi locali, nonché autorizzazioni e privilegi come al solito.

Le informazioni di base su Adobe Identity Management, inclusa la configurazione IDP, sono disponibili [qui](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html).

L’utilizzo di Enterprise Administration e Admin Console è invece trattato [qui](https://helpx.adobe.com/it/enterprise/managing/user-guide.html).

### Onboarding degli utenti in Admin Console {#onboarding-users-in-admin-console}

A seconda delle dimensioni del cliente e delle loro preferenze, è possibile eseguire l’onboarding dei clienti in tre modi diversi, ovvero creare manualmente gli utenti in Admin Console, caricare un file .csv oppure sincronizzare gli utenti dall’istanza aziendale di Active Directory del cliente.

**Aggiunta manuale tramite l’interfaccia di Admin Console**

È possibile creare manualmente utenti e gruppi nell’interfaccia di Admin Console. Utilizza questo metodo se il numero di utenti da gestire non è troppo elevato, ad esempio con meno di 50 utenti AEM o se stai già utilizzando questo metodo per amministrare altri prodotti Adobe come le applicazioni Creative Cloud, Analytics o Target.

![Onboarding degli utenti](/help/security/assets/ims3.png)

**Caricamento di file nell’interfaccia di Admin Console**

Per facilitare la creazione di utenti, è possibile caricare un file `.csv` per aggiungere utenti in blocco.

![Caricamento di file](/help/security/assets/ims4.png)

**Strumento User Sync**

Lo strumento User Sync consente ai clienti aziendali di creare e gestire utenti Adobe che utilizzano Active Directory. Questo strumento funziona anche con altri servizi di directory OpenLDAP testati. È destinato ad amministratori di identità IT (directory Enterprise o amministratori di sistema) che potranno installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che i clienti possano modificarlo in base a esigenze specifiche.

Quando viene eseguito, lo strumento User Sync recupera un elenco di utenti dall’istanza di Active Directory dell’organizzazione e lo confronta con quello presente in Admin Console.  Chiama quindi l’API User Management di Adobe in modo che Admin Console sia sincronizzato con la directory dell’organizzazione. Il flusso delle modifiche è completamente unidirezionale, pertanto eventuali modifiche apportate in Admin Console non vengono inviate alla directory.

Questo strumento consente all’amministratore di sistema di mappare i gruppi di utenti nella directory del cliente con la configurazione del prodotto e i gruppi di utenti in Admin Console.

Per configurare User Sync, l’organizzazione deve creare un set di credenziali in modo analogo a come userebbe l’[API User Management](https://www.adobe.io/apis/experienceplatform/umapi-new.html).

![Strumento User Sync](/help/security/assets/ims5.png)

Lo strumento User Sync viene distribuito tramite l’archivio Github di Adobe disponibile [qui](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> La versione prerelease **2.4RC1** include il supporto per la creazione di gruppi dinamici ed è disponibile [qui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Le funzioni principali di questa versione includono la possibilità di mappare dinamicamente i nuovi gruppi LDAP per l’iscrizione degli utenti in Admin Console, nonché la creazione dinamica di gruppi di utenti.

Ulteriori informazioni sulle nuove funzioni per i gruppi sono disponibili [qui](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Documentazione di User Sync**

Per ulteriori informazioni, consulta la [documentazione di User Sync](https://adobe-apiplatform.github.io/user-sync.py/en/).

Lo strumento User Sync deve essere registrato come client UMAPI di Adobe I/O come descritto nella procedura disponibile [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

La documentazione della console di Adobe I/O è disponibile [qui](https://www.adobe.io/apis/cloudplatform/console.html).

L’API User Management utilizzata dallo strumento User Sync viene descritta [qui](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## Configurazione di Adobe Experience as a Cloud Service {#aem-configuration}

>[!NOTE]
>
>La configurazione di AEM IMS richiesta verrà impostata automaticamente durante il provisioning degli ambienti e delle istanze di AEM. Tuttavia, l’amministratore può modificarla in base alle proprie esigenze utilizzando il metodo descritto [qui](/help/implementing/deploying/overview.md).

La configurazione di AEM IMS richiesta verrà impostata automaticamente durante il provisioning degli ambienti e delle istanze di AEM.  Gli amministratori dei clienti possono modificare parte della configurazione in base alle proprie esigenze.

L’approccio generale consiste nel configurare Adobe IMS come provider OAuth. È possibile modificare il **gestore di sincronizzazione predefinito Apache Jackrabbit Oak** in modo analogo alla sincronizzazione LDAP.

Di seguito sono descritte le configurazioni OSGI principali da modificare per cambiare proprietà come l’iscrizione automatica degli utenti o le mappature dei gruppi.

<!-- Arun to provide list of osgi configs -->

## Guida all’uso {#how-to-use}

### Gestione dei prodotti e dell’accesso utente in Admin Console {#managing-products-and-user-access-in-admin-console}

Quando l’amministratore di prodotto accede ad Admin Console, visualizza più istanze del contesto di prodotto di AEM Managed Services come mostrato di seguito:

![Accesso alle istanze](/help/security/assets/ims6.png)

In questo esempio l’organizzazione **AEM-MS-Onboard** dispone di 32 istanze distribuite in topologie e ambienti diversi come Stage o Prod.

![Accesso alle istanze 2](/help/security/assets/ims7.png)

In ogni istanza del contesto di prodotto sono presenti profili di prodotto associati, che vengono utilizzati per assegnare a utenti e gruppi l’accesso con il privilegio richiesto.

Il profilo **Administrator_xxx** verrà utilizzato per concedere privilegi di amministratore nell’istanza di AEM associata, mentre il profilo **User_xxx** viene utilizzato per aggiungere utenti normali.

Tutti gli utenti e i gruppi aggiunti in questo profilo di prodotto potranno accedere a questa particolare istanza come mostrato nell’esempio seguente:

![Profilo di prodotto](/help/security/assets/ims8.png)

### Logging into Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Accesso amministratore locale**

AEM può continuare a supportare gli accessi locali per gli utenti Admin. La schermata di accesso include un’opzione per eseguire l’accesso in locale:

![Accesso locale](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Accesso basato su IMS**

Per altri utenti, è possibile utilizzare l’accesso basato su IMS dopo che IMS è stato configurato per l’istanza. L’utente farà prima clic sul pulsante Accedi con Adobe, come illustrato di seguito:

![Accesso IMS](/help/security/assets/ims10.png)


>[!NOTE]
> Qualsiasi utente creato in IMS può essere creato utilizzando Adobe ID o Federated ID. Se un utente è configurato con l&#39;Adobe ID, viene autenticato utilizzando il provider di identità della propria Azienda per accedere.

Verrà quindi reindirizzato alla schermata di accesso di IMS e dovrà immettere le proprie credenziali:

![Accesso IMS 2](/help/security/assets/ims11.png)

![Accesso IMS 3](/help/security/assets/ims12.png)

Se durante la configurazione iniziale di Admin Console viene configurato un IDP federato, l’utente verrà reindirizzato all’IDP del cliente per l’accesso SSO:

![Accesso IMS 4](/help/security/assets/ims13.png)

Una volta completata l’autenticazione, l’utente verrà reindirizzato ad AEM per eseguire l’accesso:

![Accesso IMS 5](/help/security/assets/ims14.png)

### Gestione di autorizzazioni e ACL in Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

Gli ACL e le autorizzazioni continueranno a essere gestiti in AEM. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali in cui sono definiti ACL e privilegi.

Nell’esempio seguente, ad esempio, i gruppi sincronizzati vengono aggiunti al gruppo **Dam_Users** locale.

L’utente fa parte dei seguenti gruppi in IMS:

![ACL 1](/help/security/assets/ims15.png)

Quando l’utente esegue l’accesso, le iscrizioni ai gruppi vengono sincronizzate, come illustrato di seguito:

![ACL 2](/help/security/assets/ims16.png)

In AEM i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, come **DAM Users**.

![ACL 3](/help/security/assets/ims17.png)

Come mostrato di seguito, il gruppo **AEM-GRP_008** eredita le autorizzazioni e i privilegi di **DAM Users**. Si tratta di un modo efficace per gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nel metodo di autenticazione basato su LDAP.

![ACL 3](/help/security/assets/ims18.png)


### Accesso a Cloud Manager {#accessing-cloud-manager}

Per poter accedere a Cloud Manager o AEM come ambienti di servizio cloud, devi essere assegnato ai profili del prodotto Cloud Manager.

Il prodotto Cloud Manager ha i seguenti profili:

* Proprietario
* Gestione distribuzione
* Program Manager
* Sviluppatore
* Integrazioni

>[!NOTE]
>Cloud Manager dispone di ruoli preconfigurati con le autorizzazioni appropriate. Per informazioni su ciascuno dei ruoli con autorizzazioni specifiche, attività preconfigurate o autorizzazioni associate a ciascun ruolo, fare riferimento a Autorizzazioni [basate sul](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html)ruolo.

**Passaggi per l’aggiunta di un utente**

1. Aggiungete un utente a un particolare profilo dalla schermata di un utente esistente o da una nuova schermata utente.

1. In alternativa, potete anche aggiungere un utente dalla schermata **Panoramica** , come illustrato nella figura riportata di seguito.

   ![ACL 3](/help/security/assets/ims23.png)

   >[!NOTE]
   >Potete assegnare più profili a un utente, come illustrato nella figura riportata di seguito.

   ![ACL 3](/help/security/assets/ims22.png)


1. Una volta aggiunto il profilo appropriato, dovresti essere in grado di accedere ai rispettivi tenant in Cloud Manager tramite [Adobe Experience Cloud](http://my.cloudmanager.adobe.com) utilizzando l&#39;angolo in alto a destra dell&#39;interfaccia utente.


### Accesso a un’istanza in AEM come servizio cloud {#accessing-instance-cloud-service}

>[!IMPORTANT]
>I passaggi indicati nella sezione precedente devono essere già stati completati prima di poter accedere a un’istanza in AEM come servizio cloud.

Per poter accedere a un’istanza di AEM all’interno di **Admin Console**, nell’elenco dei prodotti di **Admin Console** dovresti vedere il Programma Cloud Manager e gli ambienti all’interno del programma.

Ad esempio, nella schermata seguente, sono disponibili due ambienti: *dev author* e *publish*.

![ACL 3](/help/security/assets/ims19.png)

Per accedere alle istanze di AEM, l&#39;utente dovrà essere aggiunto a un gruppo del prodotto Servizio Cloud appropriato.

Ogni istanza di autore avrà un profilo Amministratori AEM e Utenti AEM, e ogni istanza di pubblicazione avrà un profilo Utenti AEM. Potete aggiungere altri profili in base alle esigenze.

Per ottenere l&#39;accesso a livello di amministratore all&#39;istanza di AEM, aggiungi l&#39;utente al profilo di amministratori AEM per quel particolare prodotto.

