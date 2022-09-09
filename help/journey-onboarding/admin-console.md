---
title: Accesso all’Admin Console
description: Una volta compresa la preparazione necessaria all’onboarding e le nozioni di base della struttura AEMaaCS, puoi accedere all’Admin Console per la prima volta.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Accesso all’Admin Console {#accessing-admin-console}

In questa parte del [percorso di bordo,](overview.md) apprenderai la preparazione necessaria prima di poter accedere al sistema per la prima volta.

## Obiettivo {#objective}

Ora che hai letto l&#39;articolo [Terminologia as a Cloud Service AEM](terminology.md) e comprendi le nozioni di base della struttura AEMaaCS, sei pronto per accedere all’Admin Console per la prima volta!

In qualità di amministratore di sistema, sei responsabile della gestione degli utenti all’interno dell’organizzazione. A tale scopo, utilizza l’Admin Console . Dopo aver letto questa sezione devi:

* Scopri cos’è un Adobe ID.
* Puoi accedere ad Admin Console.
* Scopri come rivedere i privilegi di amministratore di sistema tramite Admin Console.
* Scopri come contattare il supporto Adobe per ricevere assistenza.

## L&#39;Admin Console {#admin-console}

Adobe Admin Console è un luogo centrale per amministrare e gestire le licenze e gli utenti dei prodotti Adobe. L’Admin Console ti consente di creare e gestire gli utenti in un’unica posizione invece che all’interno delle singole soluzioni.

## Adobe ID {#adobe-id}

Per accedere all’Admin Console, è necessario un Adobe ID. E Adobe ID è un account associato a un indirizzo e-mail specifico che è necessario per accedere e accedere AEM as a Cloud Service o a una delle soluzioni di Adobe. Utilizzando il tuo Adobe ID mantieni tutti i tuoi piani di Adobe e i prodotti associati a un singolo account.

Quando nell’Admin Console l’amministratore di sistema imposta il team, specifica l’indirizzo e-mail che verrà utilizzato come Adobe ID.

Esistono tre tipi di ID Adobe:

* **ID personale**: Questo è il tipo predefinito di Adobe ID e viene creato su adobe.com. Questo account è gestito da Adobe e chiunque può creare un account di questo tipo.

* **Enterprise ID**: Le organizzazioni in genere desiderano aumentare il controllo degli account utente. Solo gli amministratori di sistema possono creare Enterprise ID e l&#39;organizzazione possiede questi account con Adobe che funge solo da host.

* **Federated ID**: Con gli ID federati l&#39;organizzazione assume la piena proprietà e il controllo degli account. A questo scopo, la tua organizzazione deve integrare Adobe Experience Cloud con il tuo sistema di single sign-on (SSO) SAML2. Questo consente agli utenti di effettuare l’autenticazione sul sistema SSO della propria organizzazione anziché su un account ospitato da Adobe.

In qualità di amministratore di sistema, puoi decidere di effettuare l’onboarding di te stesso e del tuo team in AEM as a Cloud Service utilizzando gli ID personali prima che gli Enterprise ID o Federated ID siano impostati. Una volta impostati gli Enterprise ID o Federated ID, è possibile effettuare la transizione dei membri all&#39;utilizzo di tali ID.

## Accesso ad Admin Console {#steps-admin-console}

Prima di poter utilizzare l’Admin Console per amministrare gli utenti all’interno del team, è necessario assicurarsi di poter accedervi correttamente e di disporre delle autorizzazioni appropriate.

1. In qualità di amministratore di sistema, riceverai più e-mail da Adobe come parte del processo di onboarding. Cerca l’e-mail di benvenuto che fornisce le informazioni sul nome dell’organizzazione a cui ti è stato concesso l’accesso.

1. Fai clic sul pulsante **Introduzione** nel messaggio e-mail di benvenuto per passare ad Admin Console. Se non riesci a trovare l’e-mail, apri un browser direttamente all’Admin Console in [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![E-mail di benvenuto](/help/journey-onboarding/assets/get-started-email.png)

1. Effettua il login utilizzando il tuo Adobe ID. Al termine dell’accesso, verrà visualizzata la **Panoramica** della Adobe Admin Console.

   ![L&#39;Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Se hai accesso a più organizzazioni, assicurati di aver effettuato l’accesso all’organizzazione corretta. Per modificare l’organizzazione, fai clic sul nome dell’organizzazione nell’angolo in alto a destra e scegli l’organizzazione a cui devi accedere.

   ![Cambia organizzazione](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Seleziona **Amministratori** dal **Utenti** per verificare di essere un amministratore di sistema.

   ![Amministratori di revisione](/help/journey-onboarding/assets/get-started2.png)

1. Una volta fatto clic su **Amministratori** dal **Utenti** scheda, puoi eseguire la ricerca inserendo il tuo indirizzo e-mail Adobe ID, nome utente, nome utente o cognome.

   ![Ricerca utenti](/help/journey-onboarding/assets/get-started3.png)

1. Se tutto funziona correttamente, la ricerca restituirà il record. Se il valore in **RUOLO AMMINISTRATORE** presentazioni a colonne **Sistema**, l’utente (o l’utente visualizzato) è un amministratore di sistema.

   ![Stato del sistema](/help/journey-onboarding/assets/get-started4.png)

Congratulazioni, amministratore di sistema!

## Adobe Identity Management System {#ims}

AEM as a Cloud Service è preconfigurato con Adobe Identity Management System (noto anche come IMS) per l’autenticazione. Non è necessario eseguire alcuna operazione in qualità di amministratore di sistema per eseguire questa operazione.

Utilizzando IMS, AEM as a Cloud Service consolida l’esperienza di accesso tra AEM e il resto del Adobe Experience Cloud. Le organizzazioni con più prodotti Adobe beneficiano in particolare della creazione di gruppi basati su ruoli nell’Admin Console e dell’assegnazione dell’accesso a più prodotti, tra cui AEM as a Cloud Service tramite IMS.

Ulteriori informazioni sui profili di prodotto e sull’assegnazione di utenti nella parte successiva di questo percorso di onboarding.

## Contattare il supporto Adobe {#support}

In caso di problemi, è possibile accedere al supporto Adobe tramite l’Admin Console . La **Supporto** tab consente di accedere a varie funzioni di supporto di Adobe tramite un’interfaccia semplice e intuitiva.

![Scheda Supporto](/help/journey-onboarding/assets/support-menu.png)

La scheda ti consente di creare e gestire i casi, di chattare direttamente con i rappresentanti di assistenza clienti Adobi e di pianificare le sessioni con gli esperti. Gli amministratori di sistema e gli amministratori di supporto devono effettuare l’accesso per accedere ai casi di assistenza e alle opzioni di sessione esperte.

## Novità {#whats-next}

Dopo aver letto questo documento, devi:

* Scopri cosa è e Adobe ID.
* Puoi accedere ad Admin Console.
* Scopri come rivedere i privilegi di amministratore di sistema tramite Admin Console.
* Scopri come contattare il supporto Adobe per ricevere assistenza.

Sei pronto a continuare il tuo percorso di onboarding imparando come [assegnare i membri del team a profili di prodotto Cloud Manager](assign-profiles-cloud-manager.md) in modo che i tuoi colleghi possano accedere anche ad AEMaaCS.

## Risorse aggiuntive {#additional-resources}

* [Panoramica dell’Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) - Panoramica completa dell&#39;Admin Console
* [Crea o aggiorna il tuo Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Scopri come creare un Adobe ID, modificarlo e gestire più ID Adobe.
* [Gestore autenticazione SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEM navi con un gestore di autenticazione SAML. Questo gestore fornisce il supporto per SAML 2.0 Authentication Request Protocol (profilo Web-SSO) utilizzando il binding HTTP POST.
* [Ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html) - Utilizzando Adobe Admin Console, le organizzazioni possono definire una gerarchia amministrativa flessibile che consenta una gestione dettagliata dell’accesso e dell’utilizzo dei prodotti Adobe.
* [Sessioni di supporto ed esperti](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - Scopri come accedere alle opzioni di supporto nell’Admin Console, gestire i casi di assistenza, pianificare una sessione di esperti e altro ancora.
