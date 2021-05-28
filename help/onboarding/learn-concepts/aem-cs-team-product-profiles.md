---
title: AEM come team di Cloud Service e profili di prodotto
description: Segui questa pagina per informazioni su AEM come team di Cloud Service e profili di prodotto.
source-git-commit: 312b1ce7dc660d1bb4fe199be0e7403069d30161
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---


# AEM come team di Cloud Service e profili di prodotto {#product-profiles}

AEM come Cloud Service è l’offerta completamente nativa per il cloud che fornisce AEM come servizio. Offre AEM in modo nativo cloud, con nuovi attributi come sempre attivi, sempre attuali, sempre sicuri e sempre in scala. Allo stesso tempo, mantiene la proposta di valore principale che AEM fornisce come piattaforma personalizzabile ai clienti e consente ai team di livello Enterprise di integrarsi nella loro procedura di sviluppo e consegna. Per ulteriori informazioni su AEM come Cloud Service, consulta [Introduzione ad Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) .

I membri del team di Cloud Service AEM verranno aggiunti e assegnati a uno o più dei seguenti profili di prodotto tramite Admin Console durante l’onboarding.


## AEM come profili di prodotto del Cloud Service {#aem-product-profiles}

I seguenti profili di prodotto sono disponibili in AEM come team di Cloud Service:

* **Amministratore** AEM: Un amministratore AEM viene in genere assegnato agli sviluppatori, in particolare agli sviluppatori che dovranno avere accesso, ad esempio, agli ambienti di sviluppo. Il profilo di prodotto Amministratori AEM verrà utilizzato per concedere privilegi di amministratore nell’istanza AEM associata.

* **Utente** AEM: Gli utenti AEM sono gli utenti della tua organizzazione che utilizzano AEM come Cloud Service nell’ambito del contratto con Adobe. Questi membri dovranno accedere AEM per svolgere i loro compiti. Il profilo di prodotto Utenti AEM viene generalmente assegnato a un autore di contenuti AEM che crea e rivede il contenuto (può essere di diversi tipi; ad esempio pagine, risorse, pubblicazioni e così via) prima della pubblicazione sul sito web. Il profilo di prodotto Utenti AEM mostrato di seguito viene assegnato a questi membri.

   >[!NOTE]
   >Ogni utente assegnato a un AEM come profilo di prodotto di Cloud Service dispone dell’accesso (in sola lettura) a Cloud Manager.

## Profili di prodotto di Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager dispone di profili di prodotto preconfigurati o, più semplicemente, di autorizzazioni basate su ruoli. L’amministratore di sistema sarà responsabile dell’impostazione del team Cloud Manager assegnando l’ a questi profili di prodotto, deve acquisire familiarità con questi profili di prodotto e a quale membro del team assegnarli.
>[!NOTE]
>Per ulteriori informazioni, consulta [Autorizzazioni basate sul ruolo in Cloud Manager](/help/onboarding/what-is-required/user-roles-permissions.md) .

A ciascun profilo di prodotto sono associate autorizzazioni specifiche. Ad esempio, se ti trovi nel ruolo di un:

* **Proprietario business**, disponi dell’autorizzazione per aggiungere un nuovo programma o modificare un programma, aggiungere o aggiornare un ambiente, aggiungere/modificare/eliminare la pipeline ed eseguire qualsiasi pipeline e distribuire il codice per AEM ambiente o qualità del codice.

* **Deployment Manager**, è disponibile l’autorizzazione per aggiungere o aggiornare un ambiente, eseguire una pipeline e distribuire il codice per AEM ambiente o qualità del codice.

* **Sviluppatore**, disponi dell’autorizzazione per generare Token di accesso personale per accedere a Git.

* **Gestione programmi**, disponi dell’autorizzazione per accedere a Git.

Un utente può essere assegnato a più profili di prodotto. Ad esempio, l&#39;assegnazione di ruoli Business Owner (Proprietario business) e Deployment Manager a un utente fornisce loro la combinazione o la somma di queste autorizzazioni.

Il team Cloud Manager includerà almeno:

* Un proprietario unico, che in genere è anche amministratore di sistema, e deve essere la prima persona ad accedere e accedere a Cloud Manager
* One Deployment Manager
* Uno sviluppatore

   >[!NOTE]
   >Per poter accedere a AEM come Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto `AEM Users-xxx` o `AEM Administrators-xxx`. Devi disporre delle autorizzazioni per l’istanza. Le autorizzazioni per amministrare il Cloud Manager associato non saranno sufficienti.