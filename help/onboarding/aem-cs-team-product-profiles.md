---
title: AEM profili di team e prodotti as a Cloud Service
description: Scopri AEM profili di team e di prodotto as a Cloud Service e come concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# AEM profili di team e prodotti as a Cloud Service {#product-profiles}

Scopri AEM profili di team e di prodotto as a Cloud Service e come concedere e limitare l’accesso alle soluzioni di Adobe con licenza.

## Profili di prodotto {#profiles}

Quando si concede a un utente l&#39;accesso a una soluzione di Adobe specifica, non si desidera necessariamente concedere loro l&#39;accesso completo. I profili di prodotto consentono a ogni soluzione di disporre di un proprio set di autorizzazioni utente. Sono disponibili e accessibili tramite [Admin Console.](/help/journey-onboarding/admin-console.md)

## AEM profili di prodotto as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service è un’offerta completamente nativa per il cloud che fornisce AEM come servizio. Offre AEM in modo nativo cloud, con nuovi attributi come sempre attivi, sempre attuali, sempre sicuri e sempre in scala. Allo stesso tempo, mantiene la proposta di valore principale che AEM fornisce come piattaforma personalizzabile ai clienti e consente ai team di livello Enterprise di integrarsi nella loro procedura di sviluppo e consegna. Fai riferimento a [Introduzione ad Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) per ulteriori informazioni su AEM as a Cloud Service.

I membri del team AEM as a Cloud Service verranno aggiunti e assegnati a uno o più dei seguenti profili di prodotto tramite l’Admin Console durante l’onboarding.

* **Amministratori AEM**: Un amministratore AEM viene in genere assegnato agli sviluppatori, in particolare agli sviluppatori che dovranno avere accesso, ad esempio, agli ambienti di sviluppo. Il profilo di prodotto dell’amministratore AEM verrà utilizzato per concedere privilegi di amministratore nell’istanza AEM associata.

* **Utenti AEM**: Gli utenti AEM sono gli utenti dell’organizzazione che utilizzano AEM as a Cloud Service in genere per creare contenuti. Questi utenti dovranno accedere AEM per eseguire le loro attività. Il profilo di prodotto AEM utenti viene in genere assegnato a un autore di contenuti AEM che crea e rivede il contenuto. Questo contenuto può essere di molti tipi, ad esempio pagine, risorse, pubblicazioni e così via. Il profilo di prodotto AEM utenti mostrato di seguito viene assegnato a questi membri.

![Profili di prodotto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Ogni utente assegnato a un profilo di prodotto as a Cloud Service AEM ha accesso (in sola lettura) a Cloud Manager.

>[!TIP]
>
>Per ulteriori informazioni sul processo di onboarding, consulta la [percorso di bordo.](/help/journey-onboarding/overview.md)

## Profili di prodotto di Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager dispone di profili di prodotto preconfigurati che possono essere considerati come autorizzazioni basate su ruoli. L’amministratore di sistema è responsabile della configurazione del team Cloud Manager assegnandolo a questi profili di prodotto.

>[!TIP]
>
>Fare riferimento al documento [Autorizzazioni basate sul ruolo in Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) per ulteriori dettagli.

A ciascuno dei profili di prodotto sono associate autorizzazioni specifiche.

* **Proprietario business** - In questo ruolo si dispone dell&#39;autorizzazione per aggiungere un nuovo programma o modificare un programma, aggiungere o aggiornare un ambiente, aggiungere/modificare/eliminare/eseguire pipeline, distribuire il codice nell&#39;ambiente AEM o eseguire controlli di qualità del codice.
* **Gestione distribuzione** - In questo ruolo, disponi dell’autorizzazione per aggiungere o aggiornare un ambiente, eseguire qualsiasi pipeline e distribuire il codice AEM ambiente o eseguire controlli di qualità del codice.
* **Sviluppatore** - In questo ruolo, disponi dell’autorizzazione per generare token di accesso personali per l’accesso a Git.
* **Responsabile del programma** - In questo ruolo, si dispone dell&#39;autorizzazione per pianificare le pipeline, ignorare i gate di qualità a 3 livelli e fornire l&#39;approvazione di produzione.

Un utente può essere assegnato a più profili di prodotto. Ad esempio, l’assegnazione di entrambi **Proprietario business** e **Gestione distribuzione** I ruoli di un utente danno loro la somma di queste autorizzazioni.

Il team Cloud Manager includerà almeno:

* Uno **Proprietario business**, che in genere è anche l’amministratore di sistema e deve essere la prima persona ad accedere e accedere a Cloud Manager
* Uno **Gestione distribuzione**
* Uno **Sviluppatore**

>[!NOTE]
>
>Per poter accedere a AEM as a Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto: `AEM Users` o `AEM Administrators`. Le autorizzazioni per amministrare Cloud Manager non sono sufficienti.
