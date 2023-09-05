---
title: Team e profili di prodotto di AEM as a Cloud Service
description: Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per consentire e limitare l’accesso alle soluzioni Adobe con licenza.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '759'
ht-degree: 100%

---

# Team e profili di prodotto di AEM as a Cloud Service {#product-profiles}

Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per consentire e limitare l’accesso alle soluzioni Adobe con licenza.

## Profili di prodotto {#profiles}

Quando consenti l’accesso a una soluzione Adobe specifica a un utente, non devi necessariamente dare accesso completo a ogni funzione. Con i profili di prodotto è possibile disporre di un set personalizzato di autorizzazioni utente per ogni soluzione. I profili di prodotto sono disponibili e accessibili tramite [Admin Console](/help/journey-onboarding/admin-console.md).

## Profili di prodotto di AEM as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service è un’offerta completamente nativa per il cloud che include AEM as a service. AEM viene fornito come applicazione nativa del cloud che offre nuove funzionalità sempre attive, sempre aggiornate, sempre sicure e sempre scalabili. Allo stesso tempo, conserva la proposta di valore principale offerta alla clientela da AEM come piattaforma personalizzabile che i team di livello Enterprise possono integrare nella procedura di sviluppo e distribuzione. Per ulteriori informazioni su AEM as a Cloud Service, consulta [Introduzione a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md).

Durante l’onboarding, i membri del gruppo di AEM as a Cloud Service vengono aggiunti e assegnati a uno o più dei seguenti profili di prodotto tramite Admin Console.

* **Amministratori AEM**: il ruolo Amministratore AEM in genere viene assegnato ai membri del team di sviluppo, in particolare a chi deve, ad esempio, accedere agli ambienti di sviluppo. Il profilo di prodotto Amministratore AEM consente di concedere i privilegi di amministratore nell’istanza AEM associata.

* **Utenti AEM**: gli utenti AEM sono le persone dell’organizzazione che utilizzano AEM as a Cloud Service a livello generale per creare contenuti. Questi utenti devono accedere a AEM per svolgere le loro attività. Il profilo di prodotto Utenti AEM viene in genere assegnato a un autore di contenuti AEM, che crea e rivede il contenuto. Tale contenuto può essere di molti tipi, ad esempio pagine, risorse, pubblicazioni e così via. Il profilo di prodotto Utenti AEM mostrato di seguito viene assegnato a questi membri.

![Profili di prodotto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Ogni utente assegnato a un profilo di prodotto di AEM as a Cloud Service ha accesso in sola lettura a Cloud Manager tramite il ruolo **Utente di Cloud Manager**.
>
>Gli utenti con il solo ruolo di **Utente di Cloud Manager** possono accedere a Cloud Manager e passare agli ambienti di authoring di AEM (se esistono) utilizzando le opzioni del menu **Programmi**. Il ruolo **Utente di Cloud Manager** non è sufficiente per accedere ai dettagli dei programmi. Se tale accesso è necessario, l’amministratore di sistema deve assegnare agli utenti ruoli aggiuntivi.

>[!WARNING]
>
>Il nome del profilo di prodotto **Amministratori AEM** non deve essere modificato. La modifica del nome del profilo di prodotto **Amministratori AEM** rimuoverà i diritti di amministratore da tutti gli utenti assegnati a quel profilo.

>[!TIP]
>
>* Per ulteriori informazioni sui profili di prodotto di AEM, consulta il documento [Assegnazione dei profili di prodotto di AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Per ulteriori informazioni sul processo di onboarding, consulta [percorso di onboarding](/help/journey-onboarding/overview.md).

## Profili di prodotto di Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager offre profili di prodotto preconfigurati che possono essere considerati alla stregua di autorizzazioni basate su ruoli. L’amministratore di sistema è responsabile della configurazione del team di Cloud Manager tramite l’assegnazione dei profili di prodotto ai vari membri.

>[!TIP]
>
>Per ulteriori dettagli, consulta [Autorizzazioni basate sul ruolo in Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

A ciascuno dei profili di prodotto sono associate autorizzazioni specifiche.

* **Proprietario business**: con questo ruolo l’utente dispone delle autorizzazioni per aggiungere un nuovo programma o modificarne uno esistente, aggiungere o aggiornare un ambiente, distribuire il codice in un ambiente AEM o eseguire controlli di qualità del codice.
* **Responsabile dell’implementazione**: con questo ruolo l’utente dispone delle autorizzazioni per aggiungere o aggiornare un ambiente, eseguire tutte le pipeline, distribuire il codice nell’ambiente AEM ed eseguire i controlli di qualità del codice.
* **Sviluppatore**: con questo ruolo l’utente dispone dell’autorizzazione per generare token di accesso personali per accedere a Git.
* **Responsabile del programma**: con questo ruolo l’utente dispone delle autorizzazioni per pianificare le pipeline, ignorare i gate di qualità a 3 livelli e approvare la produzione.

È possibile assegnare un singolo utente a più profili di prodotto. Ad esempio, assegnando a un utente entrambi i ruoli **Proprietario business** e **Responsabile dell’implementazione**, si assegna la somma delle rispettive autorizzazioni.

Il team di Cloud Manager deve includere almeno:

* Un utente con ruolo **Proprietario business**, che in genere corrisponde all’amministratore di sistema e che dovrà essere la prima persona ad accedere a Cloud Manager.
* Un utente con ruolo **Responsabile dell’implementazione**.
* Un utente con ruolo **Sviluppatore**.

>[!NOTE]
>
>Per poter accedere a AEM as a Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto `AEM Users` o `AEM Administrators`. Le autorizzazioni per gestire Cloud Manager non sono sufficienti.

>[!TIP]
>
>* Per ulteriori informazioni sui profili di prodotto di Cloud Manager, consulta il documento [Assegnazione di membri del team ai profili di prodotto di Cloud Manager](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Per ulteriori informazioni sul processo di onboarding, consulta [percorso di onboarding](/help/journey-onboarding/overview.md).
