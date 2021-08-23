---
title: 'Assegnare i membri del team a AEM come profili di prodotto del Cloud Service '
description: Segui questa pagina per scoprire come assegnare i membri del team a AEM come profili di prodotto del Cloud Service
hide: true
index: false
source-git-commit: 4ef8c167e24a18af578d58c21fd1079a080f71d1
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---


# Assegnare i membri del team a AEM come profili di prodotto del Cloud Service {#assign-team-members-cloud-service}

## Obiettivo {#objective}

Questo documento aiuta a comprendere i passaggi che l’amministratore di sistema deve seguire per assegnare i membri del team a AEM come profili di prodotto di Cloud Service e perché è fondamentale per consentire agli autori AEM di iniziare il proprio percorso con AEM.

Dopo aver letto questa sezione è necessario comprendere:

* Perché e come i membri del team vengono assegnati a AEM come profili di prodotto di Cloud Service.
* Come aggiungere membri del team al profilo di prodotto AEM utente.
* Come aggiungere membri del team al profilo di prodotto Amministratori AEM.


## Introduzione {#introduction}

Per poter accedere a AEM come Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto:  `AEM Users` o `AEM Administrators`. Ai membri del team devono essere concesse le autorizzazioni per l’istanza AEM, in quanto le autorizzazioni per amministrare Cloud Manager non sono sufficienti. Per saperne di più.

>[!NOTE]
>Ogni utente assegnato a AEM profilo di prodotto utente dall’amministratore di sistema avrà accesso (in sola lettura) a Cloud Manager.

## Prerequisiti {#prerequisites}

Prima di iniziare a leggere questa sezione, è necessario considerare quanto segue:

* Comprendere [AEM come profili di prodotto di Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* Acquisisci familiarità con [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* I profili di prodotto di Cloud Manager sono stati assegnati ai membri del team a seconda delle necessità e le risorse cloud sono state configurate
* Dettagli sul membro del team: L’amministratore di sistema deve disporre dei nomi e degli indirizzi e-mail e dei ruoli e delle responsabilità dei membri del team che avranno bisogno dell’accesso a AEM come Cloud Service.

   >[!NOTE]
   >Ai fini dell’onboarding, è consigliabile aggiungere inizialmente utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il resto dell’onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi scalare un numero maggiore di utenti in un secondo momento.


   >[!IMPORTANT]
   >Prima di iniziare a rivedere i passaggi per assegnare i membri del team a AEM come profili di prodotto di Cloud Service, assicurati di seguire questi due passaggi:
   >
   >1. Accedi a [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). Per ulteriori informazioni, consulta Accesso ad Admin Console .
      >
      >
   1. Rivedi [AEM come profilo di prodotto di Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


Per visualizzare l’elenco dei profili di Cloud Manager da Adobe Admin Console, effettua le seguenti operazioni:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/). Dalla pagina **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** dalla scheda **Prodotti e servizi**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Passa all’istanza (istanza autore dell’ambiente di sviluppo) e selezionala come illustrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/cloud-profiles-1.png)


1. Vedrai l’elenco dei AEM come profili di prodotto di Cloud Service che dovranno essere assegnati a un utente in base al loro ruolo.

   >[!NOTE]
   >Per ulteriori informazioni, consulta [AEM come Cloud Service di profili di prodotto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/cloud-profiles-2.png)


## Aggiungi membri del team a AEM profilo di prodotto utente o AEM amministratore {#add-team-members}

Per poter accedere a AEM come istanza di Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto `AEM Users` o `AEM Administrators`.

>[!NOTE]
>È necessario disporre delle autorizzazioni per l’istanza. Le autorizzazioni per amministrare Cloud Manager non saranno sufficienti. Per saperne di più.

I passaggi seguenti devono essere seguiti da un amministratore di sistema che si trova anche nel ruolo Proprietario business.

1. Passa al programma da Cloud Manager e seleziona il pulsante **Gestisci accesso** dal contesto dell&#39;ambiente di interesse come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/add-team1.png)

1. Una nuova scheda consente di accedere a Adobe Admin Console da dove puoi accedere all’istanza di authoring dell’ambiente. Seleziona *AEM Amministratori* o *AEM Utenti* in base alle autorizzazioni che devono essere concesse a questa persona. Ulteriori informazioni su [AEM come profili di prodotto di Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/add-team2.png)

1. Seleziona `AEM Administrator` o `AEM User` e fai clic su **Aggiungi utente** come mostrato di seguito e invia i dettagli necessari per completare l&#39;aggiunta del membro del team.

   ![](/help/onboarding/onboarding-journey/assets/add-team3.png)

   L’utente aggiunto avrà ora accesso all’AEM come servizi di authoring di Cloud Service!

   >[!NOTE]
   >Se si dispone delle informazioni dei membri del team che hanno bisogno di accedere, è necessario ripetere questi passaggi per tutti gli ambienti, inclusi Sviluppo, Stage e Produzione.


## Novità {#whats-next}

Gli utenti che hai assegnato a AEM come profili di prodotto di Cloud Service ora sono pronti per imparare ad accedere a Author e per acquisire familiarità con l’authoring delle pagine in AEM come Cloud Service. È necessario seguire il percorso, esaminando successivamente il percorso di apprendimento del documento per gli utenti AEM o il percorso di apprendimento per gli sviluppatori e i responsabili della distribuzione.

## Risorse aggiuntive {#additional-resources}

* [Configurazione dell’accesso a AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [Guida rapida all’authoring delle pagine](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
