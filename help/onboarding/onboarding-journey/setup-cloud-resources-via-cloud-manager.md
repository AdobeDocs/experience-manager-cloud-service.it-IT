---
title: Configurare le risorse Cloud tramite Cloud Manager
description: Segui questa pagina per scoprire come impostare le risorse di Cloud tramite Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 0af17da9f1795a2a28808e15ba18c539c74f63bf
workflow-type: tm+mt
source-wordcount: '939'
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

## Navigazione a Cloud Manager {#navigate-cloud-manager}

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

## Creazione di un programma Cloud Service {#create-cloud-service-program}


1. Passa alla pagina di destinazione di Cloud Manager come mostrato di seguito.

   >[!NOTE]
   >Devi essere un membro del team assegnato al profilo di prodotto Proprietario business di Cloud Manager per completare correttamente questo passaggio.

1. Selezionare Aggiungi programma per avviare la procedura guidata Aggiungi programma. Guarda il video per scoprire come creare il programma AEMaaCS e considerazioni importanti prima di creare il programma.

1. Per istruzioni dettagliate su come utilizzare la procedura guidata Aggiungi programma, visita questa pagina.

   >[!CAUTION]
   >Il nome del programma non può essere modificato dopo la creazione. Si consiglia di essere certi del nome che si desidera dare al programma.

   Nel caso in cui sia necessario modificare il nome del programma, sarà necessario aprire un caso con l&#39;assistenza Adobe o, in alternativa, contattare il proprio rappresentante Adobe. Essi contribuiranno a eliminare efficacemente il programma. Dovrai ricominciare da capo con la potenziale perdita di lavoro che il tuo team ha fatto.

1. Al termine della creazione del programma cloud è possibile passare al programma per visualizzare la pagina di panoramica del programma come mostrato di seguito:

1. Se non lo hai già fatto, è il momento di aggiungere i membri per sviluppatori al team Cloud Manager, vai al profilo di prodotto Aggiungi utenti a sviluppatori e segui i passaggi descritti.

1. I membri assegnati al profilo di prodotto per sviluppatori possono accedere a Cloud Manager e a Manage Cloud Manager Git.


   Ottimo lavoro! Dopo la creazione del programma, Cloud Manager Git è disponibile per i tuoi sviluppatori per l’accesso!


## Creazione di ambienti Cloud {#create-cloud-environments}

1. Dopo aver creato correttamente il programma cloud, crea gli ambienti cloud passando alla pagina di panoramica di Cloud Manager e selezionando Aggiungi dalla scheda ambiente.

   >[!NOTE]
   >Per completare correttamente questo passaggio, è necessario accedere a un utente di Cloud Manager con il ruolo Proprietario business o Gestore distribuzione.

   Inoltre, guarda l’esercitazione video rapida per scoprire di più sugli ambienti Cloud Manager e su come aggiungerli al programma.

1. Verrà avviata la procedura guidata di aggiunta dell’ambiente che guiderà le risorse aggiungendo l’ambiente. Aggiungi prima il tuo ambiente di sviluppo per familiarizzarti.

1. Se non lo hai già fatto, puoi andare avanti e aggiungere i tuoi membri per sviluppatori al team di Cloud Manager ora, vai al profilo di prodotto Aggiungi utenti a sviluppatori e segui i passaggi descritti. In questo modo, i tuoi sviluppatori possono iniziare a navigare su Cloud Manager e a gestire Cloud Manager Git.


   Congratulazioni! Ora gli ambienti del programma cloud sono stati creati e i tuoi sviluppatori sono stati aggiunti al team.

## Novità {#whats-next}

Ora ai membri del team devono essere concesse le autorizzazioni all’istanza, in quanto le autorizzazioni per amministrare Cloud Manager non saranno sufficienti. Ora che le risorse cloud sono state create e sono pronte per essere accessibili dal team, l’amministratore di sistema deve assegnare i membri del team a AEM come profili di prodotto di Cloud Service da Admin Console.

>[!NOTE]
>Per poter accedere a AEM come Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto &quot;Utenti AEM&quot; o &quot;Amministratori AEM&quot;. Per saperne di più.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* Tipi di programma e aggiunta di un programma
* Tipi di ambiente e aggiunta di un ambiente
* Gestione di Cloud Manager Git
* Configurazione dell’accesso a AEM come Cloud Service dall’Admin Console
