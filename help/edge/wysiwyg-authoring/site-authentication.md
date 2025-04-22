---
title: Configurazione dell’autenticazione del sito per l’authoring dei contenuti
description: Scopri come AEM Live supporta l’autenticazione basata su token e come configurare AEM per l’utilizzo dell’autenticazione con l’authoring WYSIWYG.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: b2838da2-79c7-49b1-a101-15c21e80197e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# Configurazione dell’autenticazione del sito per l’authoring dei contenuti {#site-authentication}

Scopri come AEM Live supporta l’autenticazione basata su token e come configurare AEM per l’utilizzo dell’autenticazione con l’authoring WYSIWYG.

## Panoramica {#overview}

AEM Live supporta l&#39;autenticazione basata su token. L’autenticazione del sito viene in genere applicata sia ai siti di anteprima che a quelli di pubblicazione, ma può anche essere configurata per proteggere singolarmente entrambi i siti.

>[!NOTE]
>
>Se scegli di attivare l’autenticazione del sito, devi configurarla anche negli ambienti di authoring di AEM

## Requisiti {#requirements}

Per configurare l&#39;autenticazione del sito per l&#39;utilizzo con l&#39;authoring dei contenuti, è necessario prima completare le attività seguenti:

* In questo documento si presuppone che sia già stato creato un sito per il progetto in base alla [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* È necessario che [abbia già abilitato la funzionalità di ripolling per il progetto.](/help/edge/wysiwyg-authoring/repoless.md)

## Configura autenticazione sito {#configure-authentication}

Per informazioni dettagliate su come configurare l&#39;autenticazione del sito, vedere il documento [Configurazione dell&#39;autenticazione del sito](https://www.aem.live/docs/authentication-setup-site).

Durante la configurazione dell’autenticazione, prendi nota delle seguenti informazioni:

* ID dell’account tecnico
* Token di autenticazione del sito

Questi elementi sono necessari per completare la configurazione dell’autenticazione del sito per l’ambiente di authoring AEM.

## Configura ambiente di authoring {#authoring-environment}

Una volta configurata l’autenticazione del sito, puoi abilitarla nell’ambiente di authoring AEM.

1. Accedi all&#39;istanza di authoring di AEM e vai a **Strumenti** -> **Servizi cloud** -> **Configurazione Edge Delivery Services** e seleziona la configurazione creata automaticamente per il tuo sito, quindi tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra **Configurazione Edge Delivery Services**, seleziona la scheda **Autenticazione** e fornisci il **Token di autenticazione sito**, che hai copiato in precedenza.

   ![Configurazione Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. Verifica che l&#39;**ID account tecnico** corrisponda a quello copiato in precedenza.

   * Questo campo è di sola lettura e predefinito.
   * L’account tecnico è lo stesso per tutti i siti in un singolo ambiente di authoring AEM.

1. Tocca o fai clic su **Salva e chiudi**.
