---
title: Accedere a Admin Console
description: Una volta comprese le operazioni preliminari all’onboarding e le nozioni di base sulla struttura di AEM as a Cloud Service, puoi effettuare il primo accesso a Admin Console.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 8ed13eb6f476bab07da07549a83ab9ac16bdea72
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 55%

---

# Accedere a Admin Console {#accessing-admin-console}

In questa sezione del [percorso di onboarding](overview.md) scoprirai le operazioni preliminari necessarie per accedere al sistema per la prima volta.

## Obiettivo {#objective}

Ora che hai letto l’articolo [Terminologia di AEM as a Cloud Service](terminology.md) e conosci le nozioni di base della struttura di AEMaaCS, puoi effettuare il primo accesso a Admin Console.

In qualità di amministratore di sistema, sei responsabile della gestione degli utenti all’interno della tua organizzazione utilizzando Admin Console. Dopo aver letto questa sezione dovresti essere in grado di effettuare le seguenti operazioni:

* Che cos’è un Adobe ID.
* Essere in grado di accedere ad Admin Console.
* Scopri come rivedere i tuoi privilegi di amministratore di sistema tramite Admin Console.
* Come contattare il supporto Adobe per ricevere assistenza.

## Informazioni su Admin Console {#admin-console}

Adobe Admin Console è una piattaforma centralizzata da cui amministrare e gestire le licenze e gli utenti dei prodotti Adobe. Con Admin Console è possibile creare e gestire gli utenti da un’unica posizione anziché dalle singole soluzioni individuali.

### Adobe ID {#adobe-id}

Per accedere a Admin Console è necessario un Adobe ID. Un Adobe ID è un account associato a un indirizzo e-mail specifico, necessario per accedere ad AEM as a Cloud Service o a una qualsiasi delle soluzioni Adobe. Utilizzando il tuo Adobe ID, mantieni tutti i piani e i prodotti di Adobe associati a un singolo account.

Quando configuri il team come amministratore di sistema in Admin Console, specifica l’indirizzo e-mail da utilizzare come Adobe ID.

Esistono tre tipi di Adobe ID:

* **ID personale**: il tipo predefinito di Adobe ID e viene creato in adobe.com. Gestito da Adobe, chiunque può creare un account di questo tipo.

* **Enterprise ID**: le organizzazioni in genere desiderano aumentare il controllo sugli account degli utenti. Solo gli amministratori di sistema possono creare gli Enterprise ID: è l’organizzazione a gestire questi account, in cui Adobe funge solo da host.

* **Federated ID**: con i Federated ID, l&#39;organizzazione assume la piena proprietà e il controllo completo degli account. L&#39;organizzazione deve integrare Adobe Experience Cloud con il sistema Single Sign-On (SSO) SAML2. In questo modo gli utenti possono autenticarsi dal sistema SSO dell’organizzazione anziché da un account ospitato da Adobe.

In qualità di amministratore di sistema, puoi effettuare l’onboarding te stesso e del tuo team in AEM as a Cloud Service con gli ID personali. Esegui questa attività prima che siano presenti Enterprise ID o Federated ID. Dopo aver impostato gli Enterprise ID o i Federated ID, i membri possono passare a utilizzarli.

### Accedi direttamente ad Admin Console {#steps-admin-console}

Prima di poter gestire gli utenti del team con Admin Console, assicurati di poter accedere correttamente e di disporre delle autorizzazioni appropriate.

1. In qualità di amministratore di sistema, come parte del processo di onboarding ricevi più e-mail da Adobe. Cerca l’e-mail di benvenuto con le informazioni sul nome dell’organizzazione a cui hai accesso.

1. Per accedere a Admin Console, fai clic sul collegamento **Inizia** nell&#39;e-mail di benvenuto. Se non riesci a trovare l’e-mail, apri un browser per accedere direttamente ad Admin Console all’indirizzo [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![E-mail di benvenuto](/help/journey-onboarding/assets/get-started-email.png)

1. Accedi con il tuo Adobe ID. Dopo aver effettuato l’accesso, viene visualizzata la pagina **Panoramica** di Adobe Admin Console.

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Se hai accesso a più organizzazioni, assicurati di aver effettuato l’accesso all’organizzazione corretta. Per cambiare organizzazione, fai clic sul relativo nome nell’angolo in alto a destra e scegli l’organizzazione a cui desideri accedere.

   ![Cambiare organizzazione](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Dalla scheda **Utenti**, seleziona **Amministratori** per verificare di essere uno degli amministratori di sistema.

   ![Verifica degli amministratori](/help/journey-onboarding/assets/get-started2.png)

1. Dopo aver fatto clic su **Amministratori** dalla scheda **Utenti**, puoi effettuare una ricerca inserendo e-mail, nome utente, nome o cognome associati all’Adobe ID.

   ![Ricerca utenti](/help/journey-onboarding/assets/get-started3.png)

1. Se tutto funziona correttamente, la ricerca restituisce il record. Se il valore nella colonna **RUOLO AMMINISTRATORE** mostra **Sistema**, l’amministratore di sistema sei tu (o l’utente visualizzato).

   ![Stato sistema](/help/journey-onboarding/assets/get-started4.png)

Congratulazioni, amministratore di sistema.

## Accedere ad Admin Console tramite Experience Hub  {#access-admin-console-via-experience-hub}

[Experience Hub](/help/experience-hub.md) è la home unificata e personalizzata di AEM. Unisce gli strumenti di AEM e Admin Console in un’unica posizione.

Opzione ![Admin Console visualizzata nella home page di Experience Hub](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**Per accedere ad Admin Console tramite Experience Hub:**

1. Fai clic su [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) per aprire la home page di Experience Hub.

1. Nel raggruppamento **Accesso rapido**, fai clic su [**Admin Console**](https://experience.adobe.com).

## Adobe Identity Management System {#ims}

AEM as a Cloud Service è preconfigurato con Adobe Identity Management System (anche noto come Adobe IMS) per l’autenticazione. Non è necessario eseguire alcuna operazione in qualità di amministratore di sistema per abilitare questa funzionalità.

Con IMS, AEM as a Cloud Service consolida l’esperienza di accesso tra AEM e Adobe Experience Cloud. Le organizzazioni con molti prodotti Adobe ottengono il massimo. Crea gruppi basati sui ruoli in Admin Console e concedi l’accesso ai prodotti tramite IMS, ad esempio AEM as a Cloud Service.

Nella sezione successiva di questo percorso di onboarding troverai ulteriori informazioni sui profili di prodotto.

## Contatta il supporto Adobe {#support}

In caso di problemi, accedi al supporto Adobe tramite Admin Console. Nella scheda **Supporto** sono disponibili diverse funzioni di assistenza offerte da Adobe tramite un’interfaccia utente di semplice utilizzo.

![Scheda Supporto](/help/journey-onboarding/assets/support-menu.png)

Dalla scheda è possibile creare e gestire i casi, chattare direttamente con l’assistenza clienti Adobe e pianificare le sessioni con gli esperti. Gli amministratori di sistema e gli amministratori del supporto devono effettuare l’accesso per accedere ai casi e alle opzioni delle sessioni con gli esperti.

## Passaggio successivo {#whats-next}

Ora che hai letto questo documento dovresti sapere:

* Che cos’è un Adobe ID.
* Essere in grado di accedere ad Admin Console.
* Scopri come rivedere i tuoi privilegi di amministratore di sistema utilizzando Admin Console.
* Come contattare il supporto Adobe per ricevere assistenza.

Sei pronto a continuare il tuo percorso di onboarding scoprendo come [assegnare i membri del gruppo ai profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md) in modo che i tuoi colleghi possano accedere anche a AEMaaCS.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Panoramica di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html): una panoramica completa di Admin Console.
* [Creazione o aggiornamento dell’Adobe ID](https://helpx.adobe.com/it/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID/): scopri come creare un Adobe ID, come modificarlo e gestirne più di uno.
* [Gestore autenticazione SAML 2.0](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#): AEM viene fornito con un gestore per l’autenticazione SAML. Questo gestore fornisce il supporto per il protocollo di richiesta di autenticazione SAML 2.0 (profilo Web-SSO) utilizzando l’associazione HTTP POST.
* [Ruoli amministrativi](https://helpx.adobe.com/it/enterprise/using/admin-roles.html): con Adobe Admin Console le organizzazioni possono definire una gerarchia amministrativa flessibile per una gestione dettagliata dell’accesso e dell’utilizzo dei prodotti Adobe.
* [Supporto e sessioni con gli esperti](https://helpx.adobe.com/it/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html): scopri come accedere alle opzioni di supporto in Admin Console, gestire i casi di assistenza, pianificare una sessione con gli esperti e altro ancora.
