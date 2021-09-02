---
title: 'Assegnazione di membri del team ai profili di prodotto di Cloud Manager '
description: Segui questa pagina per scoprire come assegnare i membri del team ai profili di prodotto di Cloud Manager
feature: Onboarding
role: Admin, User, Developer
source-git-commit: d8ff6f4386ab0e5df4f770cdb566facc1cc0cc98
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---


# Assegnare membri del team ai profili di prodotto di Cloud Manager {#assign-team-members}

Dopo aver appreso come accedere a [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en) e aver visualizzato i privilegi come [Amministratore di sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en), ora puoi assegnare i membri del team ai profili di prodotto di Cloud Manager.

## Obiettivo {#objective}

In questo documento viene riepilogato come assegnare i membri del team ai profili di prodotto di Cloud Manager da Adobe Admin Console.

Dopo aver letto questa sezione dovresti essere in grado di:

* Scopri perché e come aggiungere i membri del team.
* Scopri tre diversi profili di prodotto di Cloud Manager, ad esempio Proprietario business, Manager distribuzione e Sviluppatore.
* Assegna i membri del team ai profili di prodotto di Cloud Manager, ad esempio Proprietario business, Manager distribuzione e Sviluppatore.

## Prerequisiti {#prerequisites}

Prima di avviare questa sezione, è necessario tenere in considerazione i seguenti prerequisiti. Devi:

* È un amministratore di sistema e scopri i [profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).
* Informazioni di base su [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en).
* Dettagli sui membri del tuo team. Un amministratore di sistema deve disporre dei nomi, degli indirizzi e-mail e dei ruoli e delle responsabilità dei membri del team che avranno bisogno dell’accesso a AEM come Cloud Service.

   >[!NOTE]
   >Ai fini dell’onboarding, è consigliabile aggiungere inizialmente utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il resto dell’onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi scalare un numero maggiore di utenti in un secondo momento.

## Esamina i profili di prodotto di Cloud Manager {#review-product-profiles}

Dall’Adobe Admin Console puoi vedere l’elenco dei profili di Cloud Manager.

>[!NOTE]
>Prima di esaminare i profili di prodotto di Cloud Manager da Admin Console, si consiglia di esaminare i [profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) disponibili.

Per visualizzare l’elenco dei profili di Cloud Manager, effettua le seguenti operazioni:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/). Dalla pagina **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** dalla scheda **Prodotti e servizi**.

   ![](/help/journey-onboarding/assets/assign-team1.png)

   >[!NOTE]
   >Per informazioni su come utilizzare Admin Console, consulta Accesso ad Admin Console .


1. Passa all&#39;istanza **Cloud Manager** dall&#39;elenco di tutte le istanze.

   ![](/help/journey-onboarding/assets/assign-team2.png)

1. Verrà visualizzato l&#39;elenco dei profili di prodotto [Cloud Manager preconfigurati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

   ![](/help/journey-onboarding/assets/assign-team3.png)


## Assegnare utenti al profilo di prodotto proprietario business {#assign-users-business-owner}

Ora puoi aggiungere utenti e assegnarli al profilo di prodotto Proprietario business di Cloud Manager.

>[!NOTE]
>Per eseguire correttamente questa operazione, da Admin Console di Adobe devi aggiungere un utente sia al prodotto (AEM come Cloud Service in questo caso) che al [Profilo di prodotto Business Owner di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

I seguenti passaggi ti guideranno attraverso questo:

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Proprietario business. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** prodotto dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la scheda **Utenti** dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team**, digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. Nella selezione del prodotto, seleziona **Adobe Experience Manager as a Cloud Service** e assegna all&#39;utente il profilo di prodotto **Proprietario business** come mostrato di seguito.

   >[!NOTE]
   >Fai riferimento a [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell’Admin Console, come mostrato di seguito.

   ![](/help/journey-onboarding/assets/assign-team6.png)

   >[!NOTE]
   >Assegna l’utente ad almeno un profilo di prodotto in modo che l’utente possa accedere a Cloud Manager. Ricordarsi di assegnarsi (amministratore di sistema) al proprietario dell&#39;azienda.

1. Fai clic su **Salva**. Viene inviata un’e-mail di benvenuto all’utente aggiunto. L’utente invitato può accedere a Cloud Manager facendo clic sul collegamento presente nell’e-mail di benvenuto e accedendo utilizzando il proprio Adobe ID.

   Congratulazioni! Il team Cloud Manager di nuova formazione (incluso l’utente assegnato al ruolo &quot;Proprietario business&quot;) è stato configurato. I membri riceveranno un’e-mail di benvenuto che li invita ad accedere e ad accedere a Cloud Manager. Nel ruolo di Business Owner (Proprietario business), ora sei a solo un passo dall’accesso a Cloud Manager e dall’abilitazione della creazione delle risorse cloud.

## Assegnare utenti al profilo di prodotto di Deployment Manager {#assign-users-deployment-manager}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto di Deployment Manager. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business (come descritto nella sezione precedente).

1. Nella pagina [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** prodotto dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la scheda **Utenti** dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team**, digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. Nella selezione del prodotto, seleziona **Adobe Experience Manager as a Cloud Service** e assegna all&#39;utente il profilo di prodotto **Deployment Manager** come mostrato di seguito.

   >[!NOTE]
   >Fai riferimento a [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell&#39;Admin Console come mostrato di seguito.

   ![](/help/journey-onboarding/assets/assign-team6.png).

   >[!IMPORTANT]
   >Puoi aggiungere l’utente al profilo di prodotto di Deployment Manager dopo la creazione delle risorse di Cloud Manager.

## Assegnare utenti al profilo di prodotto per sviluppatori {#assign-users-developer}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Sviluppatore. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** prodotto dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la scheda **Utenti** dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team**, digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   >[!NOTE]
   >Per ulteriori informazioni sui tipi di identità in Adobe Admin Console, consulta [Panoramica sull’identità](https://helpx.adobe.com/enterprise/using/identity.html).

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. Nella selezione del prodotto, seleziona **Adobe Experience Manager as a Cloud Service** e assegna all&#39;utente il profilo di prodotto **Sviluppatore** come mostrato di seguito.

   >[!NOTE]
   >Fai riferimento a [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell&#39;Admin Console come mostrato di seguito.

   ![](/help/journey-onboarding/assets/assign-team6.png).


   >[!IMPORTANT]
   >Puoi aggiungere un utente al profilo di prodotto Sviluppatore dopo la creazione delle risorse di Cloud Manager.

## Novità {#whats-next}

Hai appreso tre profili di prodotto Cloud Manager diversi, ad esempio Proprietario business, Manager distribuzione e Sviluppatore. Successivamente, hai assegnato i membri del team ai profili di prodotto di Cloud Manager, ad esempio Business Owner (Proprietario business), Deployment Manager (Gestore distribuzione) e Developer. È ora possibile continuare il percorso di onboarding esaminando il documento [Configurazione delle risorse cloud tramite Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md) dove verrà illustrato:

1. In qualità di amministratore di sistema assegnato al ruolo *Proprietario business* , devi accedere a Cloud Manager e accedervi.

1. Successivamente, un utente di Cloud Manager con il ruolo *Proprietario business* può accedere e configurare le risorse cloud, inclusi il programma cloud e gli ambienti. In questo modo, il team di esperti potrà iniziare ad accedere al AEM il prima possibile.

1. Dopo che *Business Owner* ha configurato le risorse cloud, *Developers* e *Deployment Manager* che sono stati aggiunti con successo ai profili di prodotto di Cloud Manager possono accedere a Cloud Manager e acquisire familiarità con il modo in cui possono continuare nel loro percorso di apprendimento.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Panoramica su Admin Console Identity](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
