---
title: Configurare le risorse Cloud tramite Cloud Manager
description: Segui questa pagina per scoprire come impostare le risorse di Cloud tramite Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 5a909976909eb7ce2c008d2eac9ffb60e906023e
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---

# Configurare le risorse Cloud tramite Cloud Manager {#setup-cloud-resources}

L’amministratore di sistema assegnato al ruolo *Proprietario business* deve accedere e accedere a Cloud Manager. Di seguito, un membro del team assegnato al profilo di prodotto *Proprietario business* deve accedere a Cloud Manager e creare il programma cloud e gli ambienti in modo che il team di esperti possa iniziare.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come vengono create le risorse cloud e chi può farlo.

Dopo aver letto questa sezione è necessario comprendere:

* Un amministratore di sistema assegnato al ruolo *Proprietario business* deve essere il primo ad accedere e accedere a Cloud Manager.
* Creazione del programma e degli ambienti cloud.

## Introduzione {#introduction}

L’aggiunta delle risorse cloud viene eseguita tramite Cloud Manager dal membro del team assegnato al profilo di prodotto Business Owner di Cloud Manager. Si tratta in genere di un utente che capisce le esigenze aziendali e che completa la configurazione iniziale di Cloud Manager.

Segui le sezioni seguenti per scoprire come creare i tuoi [programmi di servizi cloud](#create-cloud-service-program) e [ambienti](#create-cloud-environments).

### Prerequisiti {#prerequisites}

* L’amministratore di sistema assegnato al ruolo *Proprietario business* deve accedere e accedere a Cloud Manager.

* Scopri come [navigare e accedere a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en).

* Acquisisci familiarità con i [profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

* Scopri le considerazioni per la creazione del programma. Guarda questo video per ulteriori informazioni.

* Comprendere i concetti di Cloud Manager [programmi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en) e [ambienti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)

## Passa a Cloud Manager {#navigate-cloud-manager}

1. L&#39;utente *Proprietario business* riceverà un&#39;e-mail di benvenuto da dove può iniziare o, se non riesce a trovarlo, passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com/#/@ccs/home) e accedi utilizzando il tuo Adobe ID.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources1.png)

1. Dalla home page di Adobe Experience Cloud, seleziona **Experience Manager**.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. Verrà visualizzata la home page di AEM. Da qui, avvia **Cloud Manager** .

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. Viene visualizzata la pagina di destinazione di Cloud Manager, come illustrato nella figura riportata di seguito.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

1. Verifica di aver ricevuto l&#39;assegnazione del profilo di prodotto Proprietario business. A tale scopo, seleziona il profilo dall’alto a destra, come illustrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. Selezionare **Ruoli utente** e assicurarsi di essere assegnato al proprietario business.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. Questo conferma il tuo ruolo utente come Proprietario business.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   Ottimo lavoro! Accesso a Cloud Manager come proprietario aziendale completato.

## Crea programma Cloud Service {#create-cloud-service-program}

Per creare il programma di servizi cloud da Cloud Manager, effettua le seguenti operazioni:

1. Passa alla pagina di destinazione di Cloud Manager, come illustrato di seguito.

   >[!NOTE]
   >Devi essere un membro del team assegnato al profilo di prodotto Proprietario business di Cloud Manager per completare correttamente questo passaggio.

   Da qui, fai clic su **Aggiungi programma** per avviare la procedura guidata Aggiungi programma.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

   >[!NOTE]
   >Guarda il [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) per scoprire come creare il programma AEM as a Cloud e per scoprire importanti considerazioni prima di creare il programma.

   >[!IMPORTANT]
   >Per istruzioni dettagliate su come utilizzare la procedura guidata Aggiungi programma, vai [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en).
   >
   >* Il nome del programma non può essere modificato dopo la creazione. Si consiglia di essere certi del nome che si desidera dare al programma.
   >* Nel caso in cui sia necessario modificare il nome del programma, sarà necessario aprire un caso con l&#39;assistenza Adobe o, in alternativa, contattare il proprio rappresentante Adobe. Essi contribuiranno a eliminare efficacemente il programma. Dovrai ricominciare da capo con la potenziale perdita di lavoro che il tuo team ha fatto.


1. Al termine della creazione del programma cloud è possibile passare al programma per visualizzare la pagina **Panoramica** del programma, come illustrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources8.png)

   >[!NOTE]
   >Se non lo hai già fatto, è il momento di aggiungere i membri per sviluppatori al team Cloud Manager. Fai riferimento al profilo di prodotto Aggiungi utenti a sviluppatori e segui i passaggi descritti.

1. I membri assegnati al profilo di prodotto per sviluppatori possono accedere a Cloud Manager e a [Manage Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   Ottimo lavoro! Dopo la creazione del programma, Cloud Manager Git è disponibile per i tuoi sviluppatori per l’accesso!


## Creare gli ambienti cloud {#create-cloud-environments}

Dopo aver creato correttamente il programma cloud, crea gli ambienti cloud.

Per creare ambienti cloud da Cloud Manager, effettua le seguenti operazioni:

1. Passa alla pagina **Panoramica** di Cloud Manager e seleziona **Aggiungi** dalla scheda ambiente.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources9.png)

   >[!IMPORTANT]
   >Per completare correttamente questo passaggio, è necessario accedere a un utente di Cloud Manager con il ruolo Proprietario business o Gestore distribuzione.

   Inoltre, guarda il tutorial rapido [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en) per informazioni sugli ambienti Cloud Manager e su come aggiungerli al programma.

1. Verrà avviata la procedura guidata di aggiunta dell’ambiente che guiderà le risorse aggiungendo l’ambiente. Aggiungi prima il tuo ambiente di sviluppo per familiarizzarti. Per ulteriori informazioni, consulta [Aggiunta di un ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments) .

   >[!NOTE]
   >Se non lo hai già fatto, è il momento di aggiungere i membri per sviluppatori al team Cloud Manager. Fai riferimento al profilo di prodotto Aggiungi utenti a sviluppatori e segui i passaggi descritti.

1. I membri assegnati al profilo di prodotto per sviluppatori possono accedere a Cloud Manager e a [Manage Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   Ottimo lavoro! Dopo la creazione del programma, Cloud Manager Git è disponibile per i tuoi sviluppatori per l’accesso!

   Congratulazioni! Ora gli ambienti del programma cloud sono stati creati e i tuoi sviluppatori sono stati aggiunti al team.

## Novità {#whats-next}

Ai membri del team devono essere concesse le autorizzazioni all’istanza, in quanto le autorizzazioni per amministrare Cloud Manager non sono sufficienti. Ora che le risorse cloud sono state create e sono pronte per essere accessibili dal team, l’amministratore di sistema deve assegnare i membri del team a AEM come profili di prodotto di Cloud Service da Adobe Admin Console.

>[!NOTE]
>Per poter accedere a AEM come Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto `AEM Users` o `AEM Administrators`. Per ulteriori informazioni, consulta [Gestione dei prodotti e dell’accesso utente in Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console) .

Continua il tuo percorso di onboarding esaminando il documento Assegnazione di membri del team a AEM come profili di prodotto di Cloud Service.


## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Tipi di programma e aggiunta di un programma](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [Tipi di ambiente e aggiunta di un ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [Gestione di Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [Configurazione dell’accesso a AEM come Cloud Service dall’Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
