---
title: Supporto IMS per Adobe Experience Manager as a Cloud Service
description: Supporto del sistema di gestione delle immagini per Adobe Experience Manager as a Cloud Service
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '1993'
ht-degree: 100%

---

# Supporto IMS per Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introduzione {#introduction}

* AEM as a Cloud Service include il supporto Admin Console per le istanze AEM e l’autenticazione basata su Adobe IMS (Identity Management System).
* Admin Console consente agli amministratori di gestire tutti gli utenti di Experience Cloud da una posizione centralizzata.
* Gli utenti e i gruppi possono essere assegnati a profili di prodotto associati a un’istanza di AEM as a Cloud Service, per consentire loro di accedere a tale istanza.

>[!TIP]
>
>Per un’introduzione su come gli utenti si autenticato utilizzando Adobe IMS per AEM as a Cloud Service, consulta [Configurare l’accesso ad AEM per gli amministratori](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem&amp;lang=it). Scopri anche il modo in cui gli utenti, i gruppi di utenti e i profili di prodotto Adobe IMS vengono utilizzati per controllare l’accesso ad AEM e alle relative funzioni e funzionalità. Adobe ID richiesto.

>[!NOTE]
>
>AEM attualmente non supporta l’assegnazione di gruppi ai profili. Gli utenti devono essere aggiunti singolarmente.

## Elementi di rilievo {#key-highlights}

AEM as a Cloud Service offre il supporto per l’autenticazione IMS solo per gli utenti con privilegi di autore, amministratore e sviluppatore, e non per gli utenti finali esterni che visitano i siti dei clienti.

* In Admin Console i clienti sono rappresentati come organizzazioni IMS, mentre le istanze di authoring e pubblicazione di un ambiente sono rappresentate come istanze del contesto di prodotto. Grazie a questa rappresentazione gli amministratori di sistema e di prodotto possono gestire l’accesso alle istanze.
* I profili di prodotto in Admin Console determinano le istanze accessibili a un determinato utente.
* Per l’accesso Single Sign-On, i clienti possono utilizzare provider di identità (IDP) personali conformi a SAML 2.
* Per l’accesso Single Sign-On dei clienti sono supportati solo Enterprise ID o Federated ID e non gli Adobe ID personali.

## Architettura {#architecture}

Per l’autenticazione IMS viene utilizzato il protocollo OAuth tra AEM e l’endpoint Adobe IMS. Dopo essere stato aggiunto a IMS, un utente con Adobe ID può accedere al servizio authoring di AEM utilizzando le sue credenziali IMS.

Come illustrato nel flusso di accesso dell’utente di seguito, l’utente viene reindirizzato a IMS ed eventualmente all’IDP del cliente per l’accesso SSO e quindi reindirizzato nuovamente ad AEM.

![Architettura di IMS](/help/security/assets/ims1.png)

## Configurazione {#how-to-set-up}

### Onboarding di organizzazioni in Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

L’onboarding cliente in Adobe Admin Console costituisce un prerequisito per l’utilizzo di Adobe IMS per l’autenticazione in AEM.

In primo luogo, è necessario aver effettuato il provisioning di un’organizzazione per i clienti in Adobe IMS. I clienti Adobe Enterprise sono rappresentati come organizzazioni IMS in [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html). Quest’area è il portale utilizzato dai clienti Adobe per gestire i diritti dei prodotti per i propri utenti e gruppi.

Quando si effettua il provisioning di un’organizzazione per i clienti AEM in IMS, le istanze dei clienti diventano disponibili in Admin Console per gestire i diritti e l’accesso utente.

Dopo aver predisposto l’organizzazione IMS, il cliente deve configurare il proprio sistema come riepilogato di seguito:

![Onboarding in IMS](/help/security/assets/ims2.png)

1. L’amministratore di sistema designato riceve un invito ad accedere a Cloud Manager. Dopo aver effettuato l’accesso a Cloud Manager, gli amministratori di sistema possono scegliere se effettuare il provisioning di programmi e ambienti AEM oppure passare ad Admin Console per eseguire attività amministrative.
1. L’amministratore di sistema richiede un dominio per confermare la proprietà del rispettivo dominio, ad esempio acme.com.
1. L’amministratore di sistema configura le directory utente.
1. L’amministratore di sistema esegue la configurazione IDP in Admin Console per configurare l’accesso Single Sign-On.
1. L’amministratore AEM gestisce i gruppi locali, nonché autorizzazioni e privilegi come al solito.

Le informazioni di base su Adobe Identity Management, inclusa la configurazione IDP, sono disponibili [qui](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html).

L’utilizzo di Enterprise Administration e Admin Console è invece trattato [qui](https://helpx.adobe.com/it/enterprise/admin-guide.html).

### Onboarding degli utenti in Admin Console {#onboarding-users-in-admin-console}

Sono disponibili tre metodi per l’onboarding degli utenti. Ogni metodo dipende dalle dimensioni del cliente e dalle sue preferenze. Puoi creare manualmente gli utenti in Admin Console, caricare un file .csv o sincronizzare gli utenti dall’Active Directory aziendale della clientela.

**Aggiunta manuale tramite l’interfaccia di Admin Console**

È possibile creare manualmente utenti e gruppi nell’interfaccia di Admin Console. Se il numero di utenti da gestire non è troppo elevato, puoi utilizzare questo metodo. Ad esempio con meno di 50 utenti di AEM o se stai già utilizzando questo metodo per amministrare altri prodotti Adobe come le applicazioni Creative Cloud, Analytics o Target.

![Onboarding degli utenti](/help/security/assets/ims3.png)

**Caricamento di file nell’interfaccia di Admin Console**

Per facilitare la creazione di utenti, è possibile caricare un file `.csv` per aggiungere utenti in blocco.

![Caricamento di file](/help/security/assets/ims4.png)

**Strumento User Sync**

Lo strumento User Sync (UST, User Sync Tool) consente alla clientela aziendale di creare e gestire gli utenti di Adobe che utilizzano Active Directory. Questo strumento funziona anche con altri servizi di directory OpenLDAP testati. È destinato al personale di amministrazione di identità IT (directory Enterprise o personale di amministrazione di sistema) che potrà installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che la clientela possa modificarlo in base a esigenze specifiche.

Quando viene eseguito, lo strumento User Sync recupera un elenco di utenti dall’istanza di Active Directory dell’organizzazione e lo confronta con quello presente in Admin Console. Chiama quindi l’API User Management di Adobe in modo che Admin Console sia sincronizzato con la directory dell’organizzazione. Il flusso delle modifiche è completamente unidirezionale, pertanto eventuali modifiche apportate in Admin Console non vengono inviate alla directory.

Questo strumento consente al servizio di amministrazione di sistema di mappare i gruppi di utenti nella directory della clientela con la configurazione del prodotto e i gruppi di utenti in Admin Console.

Per configurare User Sync, l’organizzazione deve creare un set di credenziali in modo analogo a come userebbe l’[API User Management](https://developer.adobe.com/umapi/).

![Strumento User Sync](/help/security/assets/ims5.png)

Lo strumento User Sync viene distribuito tramite l’archivio Github di Adobe disponibile [qui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2).

>[!NOTE]
>
>La versione prerelease **2.4RC1** include il supporto per la creazione di gruppi dinamici ed è disponibile [qui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Le funzioni principali di questa versione includono la possibilità di mappare dinamicamente i nuovi gruppi LDAP per l’iscrizione degli utenti in Admin Console, nonché la creazione dinamica di gruppi di utenti.

Ulteriori informazioni sulle nuove funzioni per i gruppi sono disponibili [qui](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options).

**Documentazione di User Sync**

Per ulteriori dettagli, consulta la [documentazione di User Sync](https://adobe-apiplatform.github.io/user-sync.py/en/).

Lo strumento User Sync deve essere registrato come client UMAPI di Adobe Developer come descritto nella procedura disponibile [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

La documentazione di Adobe Developer Console è disponibile [qui](https://developer.adobe.com/developer-console/).

L’API User Management utilizzata dallo strumento User Sync è descritta [qui](https://adobe-apiplatform.github.io/user-sync.py/en/).

## Configurazione di Adobe Experience as a Cloud Service {#aem-configuration}

>[!NOTE]
>
>La configurazione di AEM IMS richiesta viene impostata automaticamente durante il provisioning degli ambienti e delle istanze di AEM. Tuttavia, l’amministratore può modificarla in base alle proprie esigenze utilizzando il metodo descritto [qui](/help/implementing/deploying/overview.md).

La configurazione di AEM IMS richiesta viene impostata automaticamente durante il provisioning degli ambienti e delle istanze di AEM. Gli amministratori dei clienti possono modificare parte della configurazione in base alle proprie esigenze.

L’approccio generale consiste nel configurare Adobe IMS come provider OAuth. È possibile modificare il **gestore di sincronizzazione predefinito Apache Jackrabbit Oak** in modo analogo alla sincronizzazione LDAP.

Di seguito sono descritte le configurazioni OSGI principali da modificare per cambiare proprietà come l’iscrizione automatica degli utenti o le mappature dei gruppi.

<!-- Arun to provide list of osgi configs -->

## Guida all’uso {#how-to-use}

### Gestione dei prodotti e dell’accesso utente in Admin Console {#managing-products-and-user-access-in-admin-console}

Quando la persona responsabile dell’amministrazione del prodotto accede ad Admin Console, visualizza più istanze del contesto di prodotto di AEM as a Cloud Service, come mostrato di seguito. Ad esempio, seleziona uno dei prodotti dalla pagina **Panoramica**:

![Accesso alle istanze](/help/security/assets/ims6.png)

Viene visualizzato un elenco delle istanze esistenti:

![Accesso alle istanze 2](/help/security/assets/ims7.png)

In ogni istanza del contesto di prodotto, ci sono istanze che si estendono sui servizi di authoring o di pubblicazione in ambienti di produzione, staging o sviluppo. Ogni istanza viene associata ai ruoli di profili di prodotto o Cloud Manager. che vengono utilizzati per assegnare a utenti e gruppi l’accesso con il privilegio richiesto.

Il profilo **Amministratori AEM_xxx** verrà utilizzato per concedere privilegi di amministratore all’istanza AEM associata, mentre il profilo **Utenti AEM_xxx** verrà usato per aggiungere utenti standard.

Tutti gli utenti e i gruppi aggiunti in questo profilo di prodotto potranno accedere a questa particolare istanza, come mostrato nell’esempio seguente:

![Profilo di prodotto](/help/security/assets/ims8.png)

>[!WARNING]
>
>Non modificare il nome profilo di prodotto **Amministratori AEM**. La modifica del nome profilo di prodotto **Amministratori AEM** rimuove i diritti di amministratore da tutti gli utenti assegnati a quel profilo.

### Accesso ad Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Accesso amministratore locale**

AEM può continuare a supportare gli accessi locali per gli utenti Admin. La schermata di accesso consente di accedere localmente:

![Accesso locale](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Accesso basato su IMS**

Per gli altri utenti, l’accesso basato su IMS viene utilizzato dopo la configurazione di IMS sull’istanza. L’utente fa clic sul pulsante Accedi con Adobe come illustrato di seguito:

![Accesso IMS](/help/security/assets/ims10.png)


>[!NOTE]
>
>Per la creazione di qualsiasi utente in IMS è possibile utilizzare un Adobe ID o un Federated ID. Se un utente viene configurato utilizzando Federated ID, l’autenticazione per l’accesso viene effettuata tramite il provider di identità della sua azienda.

L’utente viene reindirizzato alla schermata di accesso IMS, dove deve inserire le proprie credenziali:

![Accesso IMS 2](/help/security/assets/ims11.png)

![Accesso IMS 3](/help/security/assets/ims12.png)

Se durante la configurazione iniziale di Admin Console viene configurato un IDP federato, l’utente verrà reindirizzato all’IDP cliente per SSO:

![Accesso IMS 4](/help/security/assets/ims13.png)

Una volta completata l’autenticazione, l’utente verrà reindirizzato ad AEM per eseguire l’accesso:

![Accesso IMS 5](/help/security/assets/ims14.png)

### Gestione di autorizzazioni e ACL in Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

Gli ACL e le autorizzazioni continuano a essere gestiti in AEM. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali in cui sono definiti gli ACL e i privilegi.

Nell’esempio seguente, i gruppi sincronizzati vengono aggiunti al gruppo **Dam_Users** locale.

L’utente fa parte dei seguenti gruppi in IMS:

![ACL 1](/help/security/assets/ims15.png)

Quando l’utente esegue l’accesso, le iscrizioni ai gruppi vengono sincronizzate, come illustrato di seguito:

![ACL 2](/help/security/assets/ims16.png)

In AEM i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, come **DAM Users**.

![ACL 3](/help/security/assets/ims17.png)

Come mostrato di seguito, il gruppo **AEM-GRP_008** eredita le autorizzazioni e i privilegi degli **Utenti DAM**. Questa ereditarietà è un modo efficace per gestire le autorizzazioni di gruppi sincronizzati ed è comunemente utilizzata nel metodo di autenticazione basato su LDAP.

![ACL 3](/help/security/assets/ims18.png)


### Accesso a Cloud Manager {#accessing-cloud-manager}

Per poter accedere a Cloud Manager o agli ambienti in AEM as a Cloud Service, l’utente deve essere assegnato ai profili di prodotto Cloud Manager.

Per ulteriori informazioni sui ruoli degli utenti che determinano la disponibilità di funzionalità specifiche in Cloud Manager, consulta le definizioni dei ruoli.

>[!NOTE]
>Cloud Manager dispone di ruoli preconfigurati con le autorizzazioni appropriate. Per informazioni su ciascuno dei ruoli con autorizzazioni specifiche, attività preconfigurate o autorizzazioni associate a ogni ruolo, consulta la descrizione delle [autorizzazioni basate sul ruolo](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions.html?lang=it).

**Procedura per aggiungere un utente**

1. Puoi aggiungere un utente a un particolare profilo dalla schermata di un utente esistente o da una nuova schermata utente.

1. In alternativa, puoi aggiungere un utente dalla schermata **Panoramica**, come illustrato nella figura riportata di seguito.

   ![ACL 3](/help/security/assets/ims23.png)

   >[!NOTE]
   >Puoi assegnare a un utente più di un profilo, come illustrato nella figura riportata di seguito.

   ![ACL 3](/help/security/assets/ims22.png)


1. Dopo avere aggiunto il profilo appropriato, dovresti essere in grado di accedere ai rispettivi tenant in Cloud Manager tramite [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) dall’angolo in alto a destra dell’interfaccia utente.


### Accesso a un’istanza in AEM as a Cloud Service {#accessing-instance-cloud-service}

>[!IMPORTANT]
>Prima di poter accedere a un’istanza in AEM as a Cloud Service, è necessario avere già completato i passaggi indicati nella sezione precedente.

Per poter accedere a un’istanza AEM in **Admin Console**, nell’elenco di prodotti in **Admin Console**, dovresti visualizzare il programma Cloud Manager e gli ambienti al suo interno. 

Ad esempio, nella schermata seguente sono presenti due ambienti: un ambiente di *authoring* e uno di *pubblicazione*.

![ACL 3](/help/security/assets/ims19.png)

Per accedere alle istanze AEM, l’utente deve essere aggiunto a un gruppo del prodotto Cloud Service appropriato.

Ogni istanza di authoring ha un profilo Amministratori AEM e Utenti AEM, mentre ogni istanza di pubblicazione ha un profilo Utenti AEM. Puoi aggiungere altri profili in base alle esigenze.

Per poter accedere come amministratore all’istanza di AEM, aggiungi l’utente al profilo degli amministratori di AEM per quel particolare prodotto.
