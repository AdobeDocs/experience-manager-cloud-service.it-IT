---
title: Supporto IMS per Adobe Experience Manager come servizio cloud
description: 'Supporto IMS per Adobe Experience Manager come servizio cloud '
translation-type: tm+mt
source-git-commit: bef17376f0b7de79511f9ad6ceb00e9f084f45d2

---


# Supporto IMS per Adobe Experience Manager come servizio cloud {#ims-support-for-aem-as-a-cloud-service}

## Introduzione {#introduction}

* AEM come servizio Cloud include il supporto Admin Console per le istanze AEM e l&#39;autenticazione basata su Adobe Identity Management System (IMS per le istanze brevi).
* Admin Console consente agli amministratori di gestire centralmente tutti gli utenti di Experience Cloud.
* Gli utenti e i gruppi possono essere assegnati ai profili di prodotto associati ad AEM come istanze del servizio cloud, consentendo loro di accedere a tale istanza.

## Evidenziazioni chiave {#key-highlights}

AEM come servizio Cloud offre il supporto per l&#39;autenticazione IMS solo per gli utenti Author, Admin e Dev. Non offre supporto per gli utenti finali esterni di siti cliente come i visitatori del sito.

* Admin Console rappresenterà i clienti come organizzazioni IMS, istanze di Autore e Pubblicazione in un ambiente come istanze del contesto del prodotto. Ciò consentirà agli amministratori di sistema e di prodotto di gestire l&#39;accesso alle istanze.
* I profili di prodotto in Admin Console determinano le istanze a cui un utente può accedere.
* I clienti potranno utilizzare i propri provider di identità (IDP) conformi a SAML 2 per Single Sign On.
* Solo Enterprise ID o Federated ID per il cliente Single Sign On saranno supportati, nessun Adobe ID personale.

## Architettura {#architecture}

L&#39;autenticazione IMS funziona utilizzando il protocollo OAuth tra AEM e l&#39;endpoint Adobe IMS. Una volta aggiunto l’utente a IMS e dotato di Adobe Identity, può accedere al servizio di creazione AEM utilizzando le credenziali IMS.

Il flusso di accesso dell&#39;utente è riportato di seguito, l&#39;utente verrà reindirizzato a IMS ed eventualmente all&#39;IDP del cliente per SSO e quindi reindirizzato nuovamente ad AEM.

![Architettura IMS](/help/security/assets/ims1.png)

## Come impostare {#how-to-set-up}

### Organizzazione in Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

L&#39;accesso del cliente ad Adobe Admin Console è un prerequisito per utilizzare Adobe IMS per l&#39;autenticazione AEM.

Come primo passo, i clienti devono avere un&#39;organizzazione predisposta in Adobe IMS. I clienti Adobe Enterprise sono rappresentati come organizzazioni IMS in [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) Questo è il portale utilizzato dai clienti Adobe per gestire le adesioni dei prodotti per i loro utenti e gruppi.

I clienti AEM devono già disporre di un&#39;organizzazione e, come parte del provisioning IMS, le istanze dei clienti saranno rese disponibili in Admin Console per la gestione delle adesioni e dell&#39;accesso degli utenti.

Una volta che un cliente esiste come organizzazione IMS, dovrà configurare il proprio sistema come riepilogato di seguito:

![Onboarding IMS](/help/security/assets/ims2.png)

1. L&#39;amministratore di sistema designato riceve un invito ad accedere a Cloud Manager. Dopo aver effettuato l&#39;accesso a Cloud Manager, gli amministratori di sistema possono scegliere di fornire programmi e ambienti AEM oppure accedere ad Admin Console per le attività amministrative.
1. L&#39;amministratore di sistema richiede un dominio per confermare la proprietà del rispettivo dominio (ad esempio acme.com)
1. L&#39;amministratore di sistema imposta le directory utente
1. L&#39;amministratore di sistema esegue la configurazione IDP in Admin Console per configurare Single Sign On.
1. L&#39;amministratore AEM gestisce i gruppi locali e le autorizzazioni e i privilegi come al solito.

Le nozioni di base di Adobe Identity Management, inclusa la configurazione IDP, sono descritte [qui](https://helpx.adobe.com/enterprise/using/set-up-identity.html).

L&#39;utilizzo di Enterprise Administration e Admin Console è trattato [qui](https://helpx.adobe.com/enterprise/managing/user-guide.html).

### Accesso agli utenti in Admin Console {#onboarding-users-in-admin-console}

Esistono tre modi per integrare gli utenti a seconda delle dimensioni del cliente e delle loro preferenze: creare manualmente gli utenti in Admin Console, caricare un file .csv o sincronizzare gli utenti dall&#39;Enterprise Active Directory del cliente.

**Aggiunta manuale tramite l’interfaccia utente di Admin Console**

Gli utenti e i gruppi possono essere creati manualmente nell’interfaccia utente di Admin Console. Questo metodo può essere utilizzato se non si dispone di un numero elevato di utenti da gestire. Ad esempio, meno di 50 utenti AEM o se state già utilizzando questo metodo per amministrare altri prodotti Adobe come Analytics, Target o le applicazioni Creative Cloud.

![Configurazione utente](/help/security/assets/ims3.png)

**Caricamento file nell’interfaccia utente di Admin Console**

Per facilitare la gestione della creazione di utenti, è possibile caricare un `.csv` file per aggiungere utenti in massa.

![Caricamento file](/help/security/assets/ims4.png)

**Strumento di sincronizzazione utenti**

Lo strumento di sincronizzazione utenti (UST in breve) consente ai clienti aziendali di creare e gestire gli utenti Adobe che utilizzano Active Directory. Questo funziona anche per altri servizi di directory OpenLDAP testati. Gli utenti di destinazione sono amministratori di identità IT (Enterprise Directory o System Admins) che potranno installare e configurare lo strumento. Lo strumento open source è personalizzabile in modo che i clienti possano modificarlo in base alle proprie esigenze.

Quando la sincronizzazione utenti viene eseguita, recupera un elenco di utenti da Active Directory dell&#39;organizzazione e lo confronta con l&#39;elenco di utenti all&#39;interno di Admin Console.  Quindi chiama l’API di gestione utenti Adobe in modo che Admin Console sia sincronizzato con la directory dell’organizzazione. Il flusso di variazione è solo un modo. Eventuali modifiche effettuate in Admin Console non vengono inviate alla directory.

Questo strumento consente all&#39;amministratore di sistema di mappare i gruppi di utenti nella directory del cliente con la configurazione del prodotto e i gruppi di utenti nell&#39;Admin Console.

Per configurare la sincronizzazione utenti, l&#39;organizzazione deve creare un set di credenziali nello stesso modo in cui utilizzerebbero l&#39;API [di gestione](https://www.adobe.io/apis/experienceplatform/umapi-new.html)utente.

![Strumento di sincronizzazione utenti](/help/security/assets/ims5.png)

Lo strumento di sincronizzazione utenti è distribuito tramite l’archivio di Adobe Github [in questa posizione](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> La versione prerelease **2.4RC1** è disponibile con supporto per la creazione di gruppi dinamici ed è disponibile [qui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Le funzioni principali di questa versione sono la possibilità di mappare dinamicamente i nuovi gruppi LDAP per l’iscrizione degli utenti nell’Admin Console, nonché la creazione di gruppi di utenti dinamici.

Ulteriori informazioni sulle nuove funzioni del gruppo sono disponibili [in questa posizione](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Documentazione sulla sincronizzazione degli utenti**

Per ulteriori informazioni, fare riferimento alla documentazione [](https://adobe-apiplatform.github.io/user-sync.py/en/) UST.

Lo strumento di sincronizzazione utenti deve registrarsi come UMAPI client di I/O Adobe utilizzando la procedura [qui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

La documentazione della console di I/O di Adobe è disponibile [qui](https://www.adobe.io/apis/cloudplatform/console.html).

L&#39;API di gestione utente utilizzata dallo strumento di sincronizzazione degli utenti è [qui](https://www.adobe.io/apis/cloudplatform/umapi-new.html)illustrato.

## Adobe Experience as a Cloud Service Configuration {#aem-configuration}

> [!NOTE]
>
>La configurazione AEM IMS richiesta verrà configurata automaticamente al momento del provisioning degli ambienti e delle istanze AEM. Tuttavia, l&#39;amministratore può modificarlo secondo le proprie esigenze utilizzando il metodo descritto [qui](/help/implementing/deploying/overview.md).

La configurazione AEM IMS necessaria verrà configurata automaticamente al momento del provisioning degli ambienti e delle istanze AEM.  Gli amministratori dei clienti possono modificare parte della configurazione in base alle proprie esigenze

L’approccio generale consiste nel configurare Adobe IMS come fornitore OAuth. Il gestore **** di sincronizzazione predefinito Apache Jackrabbit Oak può essere modificato come per la sincronizzazione LDAP.

Di seguito sono riportate le configurazioni OSGI chiave che devono essere modificate per modificare proprietà come Appartenenza automatica utente o Mappature gruppi.

<!-- Arun to provide list of osgi configs -->

## Guida all’uso {#how-to-use}

### Gestione di prodotti e accesso utente in Admin Console {#managing-products-and-user-access-in-admin-console}

Quando l&#39;amministratore di prodotto accede ad Admin Console, visualizzeranno più istanze del contesto di prodotti dei servizi gestiti AEM come mostrato di seguito:

![Accesso istanze](/help/security/assets/ims6.png)

In questo esempio, l’organizzazione **AEM-MS-Onboard** dispone di 32 istanze che si estendono su topologie e ambienti diversi come Stage o Prod.

![Accesso istanze2](/help/security/assets/ims7.png)

In ciascuna istanza Contesto prodotto, saranno associati Profili prodotto. Questi profili di prodotto vengono utilizzati per assegnare l&#39;accesso a Utenti e gruppi con i privilegi richiesti.

Il profilo **Administrator_xxx** verrà utilizzato per concedere privilegi di amministratore nell&#39;istanza AEM associata, mentre il profilo **User_xxx** viene utilizzato per aggiungere utenti regolari.

Tutti gli utenti e i gruppi aggiunti sotto questo profilo di prodotto potranno accedere a tale istanza come mostrato nell&#39;esempio seguente:

![Profilo prodotto](/help/security/assets/ims8.png)

### Accesso ad Adobe Experience Manager come servizio Cloud (#logging-in-aem)

**Login amministratore locale**

AEM può continuare a supportare gli accessi locali per gli utenti Admin. La schermata di login dispone di un’opzione per effettuare il login in locale:

![Login locale](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Login basato su IMS**

Per altri utenti, l&#39;accesso basato su IMS può essere utilizzato una volta che IMS è configurato sull&#39;istanza. L&#39;utente farà clic sul pulsante Accedi con Adobe, come illustrato di seguito:

![Login IMS](/help/security/assets/ims10.png)

Saranno quindi reindirizzati alla schermata di accesso IMS e dovranno immettere le proprie credenziali:

![Login IMS2](/help/security/assets/ims11.png)

![Login IMS3](/help/security/assets/ims12.png)

Se durante la configurazione iniziale di Admin Console è configurato un IDP federato, l&#39;utente verrà reindirizzato all&#39;IDP del cliente per SSO:

![Login IMS4](/help/security/assets/ims13.png)

Al termine dell&#39;autenticazione, l&#39;utente verrà reindirizzato ad AEM e ha effettuato l&#39;accesso:

![Login IMS5](/help/security/assets/ims14.png)

### Gestione di autorizzazioni e ACL in Adobe Experience Manager come servizio Cloud {#managing-permissions-in-aem}

Gli ACL e le autorizzazioni continueranno a essere gestiti in AEM. I gruppi di utenti sincronizzati da IMS possono essere assegnati a gruppi locali in cui sono definiti ACL e privilegi.

Nell&#39;esempio seguente, come esempio, vengono aggiunti gruppi sincronizzati al gruppo **Dam_Users** locale.

L’utente fa parte dei seguenti gruppi in IMS:

![ACL1](/help/security/assets/ims15.png)

Quando l’utente accede, le appartenenze al gruppo vengono sincronizzate, come illustrato di seguito:

![ACL2](/help/security/assets/ims16.png)

In AEM, i gruppi di utenti sincronizzati da IMS possono essere aggiunti come membri a gruppi locali esistenti, come Utenti **** DAM.

![ACL3](/help/security/assets/ims17.png)

Come mostrato di seguito, il gruppo **AEM-GRP_008** eredita le autorizzazioni e i privilegi degli utenti **** DAM, questo è un modo efficace per gestire le autorizzazioni per i gruppi sincronizzati ed è comunemente utilizzato anche nel metodo di autenticazione basato su LDAP.

![ACL3](/help/security/assets/ims18.png)