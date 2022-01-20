---
title: Configurare le risorse Cloud tramite Cloud Manager
description: Segui questa pagina per scoprire come impostare le risorse di Cloud tramite Cloud Manager
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 7fe39bbc8d5e965af7f339b2a524420c76360552
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Configurare le risorse Cloud tramite Cloud Manager {#setup-cloud-resources}

L’amministratore di sistema assegnato al ruolo Proprietario business deve accedere e accedere a Cloud Manager. Di seguito, un membro del team assegnato al profilo di prodotto Proprietario business deve accedere a Cloud Manager e creare il programma cloud e gli ambienti in modo che il team di esperti possa iniziare.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come vengono create le risorse cloud e chi può farlo.

Dopo aver letto questa sezione è necessario comprendere:

* Un amministratore di sistema assegnato al ruolo Proprietario business deve essere il primo ad accedere e accedere a Cloud Manager.
* Creazione del programma e degli ambienti cloud.

## Introduzione {#introduction}

L’aggiunta delle risorse cloud viene eseguita tramite Cloud Manager dal membro del team assegnato al profilo di prodotto Business Owner di Cloud Manager. Si tratta in genere di un utente che capisce le esigenze aziendali e che completa la configurazione iniziale di Cloud Manager.

Segui le sezioni seguenti per scoprire come creare [programmi di servizi cloud](#create-cloud-service-program) e [ambienti.](#create-cloud-environments)

### Prerequisiti {#prerequisites}

* L’amministratore di sistema assegnato al ruolo Proprietario business deve accedere e accedere a Cloud Manager.

* Comprendere come [naviga e accedi a Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Acquisisci familiarità con [Profili di prodotto di Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Comprendere i concetti di Cloud Manager [programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) e [ambienti.](/help/implementing/cloud-manager/manage-environments.md)

## Passa a Cloud Manager {#navigate-cloud-manager}

L’utente proprietario dell’attività riceverà un’e-mail di benvenuto con un collegamento per iniziare o, se non è in grado di trovarlo, accederà [Cloud Manager](https://my.cloudmanager.adobe.com/) effettuando l’accesso direttamente con il tuo Adobe ID.

Segui i passaggi seguenti per passare a Cloud Manager:

1. Dal tuo messaggio e-mail di benvenuto clicca su **Introduzione**, come illustrato nella figura seguente.
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. Accedi a Cloud Manager’ **Programmi e prodotti** pagina.

   >[!IMPORTANT]
   >
   >In alternativa, puoi anche passare direttamente alla pagina di accesso di Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Aggiungi un segnalibro a questa pagina per riferimenti futuri e per aiutarti a passare direttamente alla pagina di destinazione di Cloud Manager.

1. Verrai indirizzato alla pagina di destinazione di Cloud Manager. Vedi [Visualizzazione dei programmi di Cloud Manager](#viewing-programs) per ulteriori dettagli.

Inoltre, puoi passare a Cloud Manager’s **Programmi e prodotti** dalla home page di Adobe Experience Cloud. Effettua le seguenti operazioni:

1. Passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com) e accedi utilizzando il tuo Adobe ID.

1. Dalla home page di Adobe Experience Cloud, seleziona **Experience Manager**.

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. Verrà visualizzata la home page di AEM. Da qui, lancio **Cloud Manager** .

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. Dopo l’accesso, verrai indirizzato alla pagina di destinazione di Cloud Manager. Vedi [Visualizzazione dei programmi di Cloud Manager](#viewing-programs) per ulteriori dettagli.

   >[!NOTE]
   >
   >A seconda dei ruoli assegnati in [!UICONTROL Cloud Manager] e lo stato dell&#39;applicazione, visualizzerai schermate diverse durante l&#39;utilizzo [!UICONTROL Cloud Manager] Interfaccia utente.

### Visualizzazione dei programmi nella pagina di destinazione di Cloud Manager {#viewing-programs}

Dopo l’accesso, verrai indirizzato alla pagina di destinazione di Cloud Manager. Verrà visualizzata una delle tre opzioni descritte di seguito:

#### In Cloud Manager non esiste alcun programma {#no-programs}

Se nell’organizzazione non è presente alcun programma, la pagina di destinazione ti invita a creare il primo programma, come illustrato nella figura riportata di seguito.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### Quando in Cloud Manager sono già presenti programmi {#programs-exist}

Se nell’organizzazione sono già presenti programmi, nella pagina di destinazione viene indicato di aggiungere un altro programma e vengono visualizzati anche tutti i programmi esistenti, come illustrato nella figura riportata di seguito.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### Quando esiste un programma e l&#39;utente è amministratore di sistema {#programs-exist-sysadmin}

Se nell&#39;organizzazione sono già presenti programmi e sei amministratore di sistema, viene visualizzata la pagina di destinazione **Gestisci accesso** insieme a **Aggiungi programma** come illustrato nella figura riportata di seguito.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verifica dei ruoli utente {#verify-user-roles}

Dopo aver effettuato l’accesso a Cloud Manager, segui i passaggi seguenti per verificare che ti sia stato assegnato il profilo di prodotto Proprietario business :

1. Seleziona il tuo profilo dall’alto a destra, come mostrato di seguito.

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. Seleziona **Ruoli utente** e assicurati di essere assegnato al proprietario dell&#39;azienda.

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. Questo conferma il tuo ruolo utente come Proprietario business.

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   Ottimo lavoro! Accesso a Cloud Manager come proprietario aziendale completato.

## Crea programma Cloud Service {#create-cloud-service-program}

Per creare il programma di servizi cloud da Cloud Manager, effettua le seguenti operazioni:

1. Passa alla pagina di destinazione di Cloud Manager, come illustrato di seguito.

   >[!NOTE]
   >
   >Devi essere un membro del team assegnato al profilo di prodotto Proprietario business di Cloud Manager per completare correttamente questo passaggio.

   Da qui, fai clic su **Aggiungi programma** per avviare la procedura guidata Aggiungi programma.

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Guarda il [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) per scoprire come creare il programma AEM as a Cloud e per informazioni su importanti considerazioni prima di creare il programma.

   >[!TIP]
   >
   >Per istruzioni dettagliate su come utilizzare la procedura guidata Aggiungi programma, fare clic su [qui](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md).

1. Al termine della creazione del programma cloud, puoi passare al programma per visualizzare **Panoramica** pagina del programma, come illustrato di seguito.

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >
   >Se non lo hai già fatto, è il momento di aggiungere i membri per sviluppatori al team Cloud Manager. Fai riferimento al profilo di prodotto Aggiungi utenti a sviluppatori e segui i passaggi descritti.

1. I membri assegnati al profilo di prodotto Sviluppatore possono accedere a Cloud Manager e [Gestione Git Di Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

   Ottimo lavoro! Dopo la creazione del programma, Cloud Manager Git è disponibile per i tuoi sviluppatori per l’accesso!


## Creare gli ambienti cloud {#create-cloud-environments}

Dopo aver creato correttamente il programma cloud, crea gli ambienti cloud.

Per creare ambienti cloud da Cloud Manager, effettua le seguenti operazioni:

1. Passa a Cloud Manager’ **Panoramica** e seleziona **Aggiungi** dalla scheda ambiente.

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >
   >Per completare correttamente questo passaggio, è necessario accedere a un utente di Cloud Manager con il ruolo Proprietario business o Gestore distribuzione.

   Inoltre, guarda la [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) tutorial per scoprire gli ambienti di Cloud Manager e come aggiungerli al programma.

1. Verrà avviata la procedura guidata di aggiunta dell’ambiente che ti guiderà nell’aggiunta dell’ambiente. Aggiungi prima l’ambiente di sviluppo per acquisire familiarità con la procedura guidata. Fai riferimento a [Aggiunta di un ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-environments) per saperne di più.

   >[!NOTE]
   >
   >Se non lo hai già fatto, è il momento di aggiungere i membri per sviluppatori al team Cloud Manager. Fai riferimento al profilo di prodotto Aggiungi utenti a sviluppatori e segui i passaggi descritti.

1. I membri assegnati al profilo di prodotto Sviluppatore possono accedere a Cloud Manager e [Gestione Git Di Cloud Manager.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

   Ottimo lavoro! Ora il tuo programma viene creato correttamente e il tuo Git di Cloud Manager è disponibile per i tuoi sviluppatori per accedere!

   Congratulazioni! Ora gli ambienti del programma cloud sono stati creati e i tuoi sviluppatori sono stati aggiunti al team.

## Novità {#whats-next}

Ai membri del team devono essere concesse le autorizzazioni all’istanza, in quanto le autorizzazioni per amministrare Cloud Manager non sono sufficienti. Ora che le risorse cloud sono state create e sono pronte per essere accessibili dal team, l’amministratore di sistema deve assegnare i membri del team a AEM profili di prodotto as a Cloud Service da Adobe Admin Console.

>[!NOTE]
>
>Per poter accedere a AEM utenti as a Cloud Service deve appartenere a uno dei due profili di prodotto `AEM Users` o `AEM Administrators`. Vedi [Gestione di prodotti e accesso utente in Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) per saperne di più.

Continua il tuo percorso di onboarding esaminando il documento [Assegnazione di membri del team a AEM profili di prodotto as a Cloud Service.](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)


## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Tipi di programma e aggiunta di un programma](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Tipi di ambiente e aggiunta di un ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Gestione di Cloud Manager Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Configurazione dell’accesso a AEM as a Cloud Service dall’Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
