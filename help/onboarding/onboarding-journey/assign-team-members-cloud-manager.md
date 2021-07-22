---
title: 'Assegnazione di membri del team ai profili di prodotto di Cloud Manager '
description: Segui questa pagina per scoprire come assegnare i membri del team ai profili di prodotto di Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 21fae2eff51e46ee026cebe135c8a16625ed8f10
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---


# Assegnazione di membri del team ai profili di prodotto di Cloud Manager {#assign-team-members}

Dopo aver appreso come accedere a [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en) e aver visualizzato i privilegi come [Amministratore di sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en), ora puoi assegnare i membri del team ai profili di prodotto di Cloud Manager.

## Obiettivo {#objective}

In questo documento viene riepilogato come assegnare i membri del team ai profili di prodotto di Cloud Manager dall’Admin Console.

Dopo aver letto questa sezione dovresti essere in grado di:

* Scopri perché e come aggiungere i membri del team.
* Scopri tre diversi profili di prodotto di Cloud Manager, ad esempio Proprietario business, Manager distribuzione e Sviluppatore.
* Assegna i membri del team ai profili di prodotto di Cloud Manager, ad esempio Proprietario business, Manager distribuzione e Sviluppatore.

## Prerequisiti {#prerequisites}

Prima di avviare questa sezione, è necessario tenere in considerazione i seguenti prerequisiti. Devi essere un:

* Un amministratore di sistema e scopri i [profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).
* Comprende le nozioni di base di [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en).
* Devono avere i dettagli sui membri del tuo team. Un amministratore di sistema deve disporre dei nomi e degli indirizzi e-mail e dei ruoli e delle responsabilità dei membri del team che avranno bisogno dell’accesso a AEM come Cloud Service.

   >[!NOTE]
   >Ai fini dell’onboarding, è consigliabile aggiungere inizialmente utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il resto dell’onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi scalare un numero maggiore di utenti in un secondo momento.

## Verifica dei profili di prodotto di Cloud Manager {#review-product-profiles}

Dall’Admin Console è possibile visualizzare l’elenco dei profili di Cloud Manager.

>[!NOTE]
>Prima di esaminare i profili di prodotto di Cloud Manager da Admin Console, si consiglia di esaminare i [profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) disponibili.

Per visualizzare l’elenco dei profili di Cloud Manager, effettua le seguenti operazioni:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/). Dalla pagina **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** dalla scheda **Prodotti e servizi**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

   >[!NOTE]
   >Per informazioni su come utilizzare Admin Console, consulta Accesso ad Admin Console .


1. Passa all’istanza **Cloud Manager** dalla tabella con l’elenco di tutte le istanze.

   ![](/help/onboarding/onboarding-journey/assets/assign-team2.png)

1. Verrà visualizzato l&#39;elenco dei profili di prodotto [Cloud Manager preconfigurati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/assign-team3.png)


## Assegnazione di utenti al profilo di prodotto del proprietario business {#assign-users-business-owner}

Ora puoi aggiungere utenti e assegnarli al profilo di prodotto Proprietario business di Cloud Manager.

>[!NOTE]
>Per eseguire correttamente questa operazione, da Admin Console di Adobe devi aggiungere un utente sia al prodotto (AEM come Cloud Service in questo caso) che al [Profilo di prodotto Business Owner di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

I seguenti passaggi ti guideranno attraverso questo:

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Proprietario business. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** prodotto dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Seleziona la scheda **Utenti** dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team**, digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. Nella selezione del prodotto, seleziona **Adobe Experience Manager as a Cloud Service** e assegna all&#39;utente il profilo di prodotto **Proprietario business** come mostrato di seguito.

   >[!NOTE]
   >Fai riferimento a [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell&#39;Admin Console come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png)

   >[!NOTE]
   >Assegna l’utente ad almeno un profilo di prodotto in modo che l’utente possa accedere a Cloud Manager. Ricordarsi di assegnarsi (amministratore di sistema) al proprietario dell&#39;azienda.

1. Fai clic su **Salva**. Viene inviata un’e-mail di benvenuto all’utente aggiunto. L’utente invitato può accedere a Cloud Manager facendo clic sul collegamento presente nell’e-mail di benvenuto e accedendo utilizzando il proprio Adobe ID.

Congratulazioni! Ora è stato configurato il team Cloud Manager di nuova formazione, incluso l’utente assegnato al ruolo &quot;Proprietario business&quot;. I membri riceveranno un’e-mail di benvenuto che li invita ad accedere e ad accedere a Cloud Manager. Nel ruolo di Business Owner (Proprietario business), ora sei a solo un passo dall’accesso a Cloud Manager e dall’abilitazione della creazione delle risorse cloud.

## Assegnazione di utenti al profilo di prodotto di Deployment Manager {#assign-users-deployment-manager}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto di Deployment Manager. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** prodotto dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Seleziona la scheda **Utenti** dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team**, digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. Nella selezione del prodotto, seleziona **Adobe Experience Manager as a Cloud Service** e assegna all&#39;utente il profilo di prodotto **Deployment Manager** come mostrato di seguito.

   >[!NOTE]
   >Fai riferimento a [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell&#39;Admin Console come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png).

   >[!IMPORTANT]
   >Puoi aggiungere l’utente al profilo di prodotto di Deployment Manager dopo la creazione delle risorse di Cloud Manager.

## Assegnazione di utenti al profilo di prodotto per sviluppatori {#assign-users-developer}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Sviluppatore. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Panoramica**, seleziona **Adobe Experience Manager as a Cloud Service** prodotto dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Seleziona la scheda **Utenti** dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team**, digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. Nella selezione del prodotto, seleziona **Adobe Experience Manager as a Cloud Service** e assegna all&#39;utente il profilo di prodotto **Sviluppatore** come mostrato di seguito.

   >[!NOTE]
   >Fai riferimento a [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell&#39;Admin Console come mostrato di seguito.

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png).


   >[!IMPORTANT]
   >Puoi aggiungere un utente al profilo di prodotto Sviluppatore dopo la creazione delle risorse di Cloud Manager.

## Novità {#whats-next}

In qualità di amministratore di sistema assegnato al ruolo *Proprietario business* , devi accedere a Cloud Manager e accedervi.
>[!NOTE]
>Per informazioni su come accedere e accedere a Cloud Manager, consulta [Navigazione a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en) .

Un utente di Cloud Manager con il ruolo Proprietario business può accedere e configurare le risorse cloud, inclusi i programmi e gli ambienti. In questo modo, il team di esperti potrà iniziare ad accedere al AEM il prima possibile.
Dopo che il proprietario business ha configurato le risorse cloud, gli sviluppatori e i gestori di distribuzione che sono stati aggiunti con successo ai profili di prodotto di Cloud Manager possono accedere a Cloud Manager e acquisire familiarità con le modalità per continuare il loro percorso di apprendimento.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Panoramica su Admin Console Identity](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
