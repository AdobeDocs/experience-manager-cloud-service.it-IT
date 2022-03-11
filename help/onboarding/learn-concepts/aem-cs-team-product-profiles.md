---
title: AEM profili di team e prodotti as a Cloud Service
description: Segui questa pagina per scoprire AEM profili di team e prodotti as a Cloud Service.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# AEM profili di team e prodotti as a Cloud Service {#product-profiles}

## Profili di prodotto {#profiles}

Quando si concede a un utente l&#39;accesso a una soluzione di Adobe specifica, non si desidera necessariamente concedere loro l&#39;accesso completo. I profili di prodotto consentono a ogni soluzione di disporre di un proprio set di autorizzazioni utente. Sono disponibili e accessibili tramite [Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md).

Ulteriori informazioni [AEM profili di prodotto as a Cloud Service](#aem-product-profiles) e [Profili di prodotto di Cloud Manager](#cloud-manager-product-profiles) per capire come questi funzionano in concerto durante la configurazione del team.

## AEM profili di prodotto as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service è l’offerta completamente nativa per il cloud che fornisce AEM come servizio. Offre AEM in modo nativo cloud, con nuovi attributi come sempre attivi, sempre attuali, sempre sicuri e sempre in scala. Allo stesso tempo, mantiene la proposta di valore principale che AEM fornisce come piattaforma personalizzabile ai clienti e consente ai team di livello Enterprise di integrarsi nella loro procedura di sviluppo e consegna. Fai riferimento a [Introduzione ad Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) per ulteriori informazioni su AEM as a Cloud Service.

I membri del team AEM as a Cloud Service verranno aggiunti e assegnati a uno o più dei seguenti profili di prodotto tramite Admin Console durante l’onboarding.

* **Amministratori AEM**: Un amministratore AEM viene in genere assegnato agli sviluppatori, in particolare agli sviluppatori che dovranno avere accesso, ad esempio, agli ambienti di sviluppo. Il profilo di prodotto Amministratori AEM verrà utilizzato per concedere privilegi di amministratore nell’istanza AEM associata.

* **Utenti AEM**: Gli utenti AEM sono gli utenti della tua organizzazione che utilizzano AEM as a Cloud Service come parte del contratto con Adobe. Questi membri dovranno accedere AEM per svolgere i loro compiti. Il profilo di prodotto Utenti AEM viene generalmente assegnato a un autore di contenuti AEM che crea e rivede il contenuto (può essere di diversi tipi; ad esempio pagine, risorse, pubblicazioni e così via) prima della pubblicazione sul sito web. Il profilo di prodotto Utenti AEM mostrato di seguito viene assegnato a questi membri.

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >Ogni utente assegnato a un profilo di prodotto as a Cloud Service AEM ha accesso (in sola lettura) a Cloud Manager.

## Profili di prodotto di Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager dispone di profili di prodotto preconfigurati o, più semplicemente, di autorizzazioni basate su ruoli. L’amministratore di sistema sarà responsabile dell’impostazione del team Cloud Manager assegnando l’ a questi profili di prodotto, deve acquisire familiarità con questi profili di prodotto e a quale membro del team assegnarli.
>[!NOTE]
>Fai riferimento a [Autorizzazioni basate sul ruolo in Cloud Manager](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions) per ulteriori dettagli.

A ciascun profilo di prodotto sono associate autorizzazioni specifiche. Ad esempio, se ti trovi nel ruolo di un:

* **Proprietario business**, l’utente dispone dell’autorizzazione per aggiungere un nuovo programma o modificare un programma, aggiungere o aggiornare un ambiente, aggiungere/modificare/eliminare la pipeline ed eseguire qualsiasi pipeline e distribuire il codice per AEM ambiente o qualità del codice.

* **Gestione distribuzione**, disponi dell’autorizzazione per aggiungere o aggiornare un ambiente, eseguire qualsiasi pipeline e distribuire il codice per AEM ambiente o qualità del codice.

* **Sviluppatore**, disponi dell’autorizzazione per generare il Token di accesso personale per accedere a Git.

* **Responsabile del programma**, disponi dell’autorizzazione per pianificare le pipeline, ignorare i gate di qualità a 3 livelli e fornire l’approvazione di produzione.

Un utente può essere assegnato a più profili di prodotto. Ad esempio, l&#39;assegnazione di ruoli Business Owner (Proprietario business) e Deployment Manager a un utente fornisce loro la combinazione o la somma di queste autorizzazioni.

Il team Cloud Manager includerà almeno:

* Un proprietario unico, che in genere è anche amministratore di sistema, e deve essere la prima persona ad accedere e accedere a Cloud Manager
* One Deployment Manager
* Uno sviluppatore

   >[!NOTE]
   >Per poter accedere a AEM as a Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto: `AEM Users` o `AEM Administrators`. È necessario disporre delle autorizzazioni per l’istanza. Le autorizzazioni per amministrare Cloud Manager associato non saranno sufficienti.
