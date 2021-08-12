---
title: Accesso agli archivi
seo-title: Accesso agli archivi
description: Questa pagina descrive come accedere e gestire l’archivio Git.
seo-description: Segui questa pagina per scoprire come accedere e gestire l’archivio Git.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 9898baebfbb43059f2497fa6b4db801eef12a9d0
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 4%

---

# Accesso agli archivi {#accessing-repos}

Puoi accedere e gestire il tuo archivio Git utilizzando Self-Service Git Account Management (Gestione account Git self-service) dall’interfaccia utente di Cloud Manager.

## Utilizzo di Self-Service Repository Account Management {#self-service-repos}

Utilizza il pulsante **Access Repo Info** disponibile dall’interfaccia utente di Cloud Manager, che si trova più in evidenza sulla scheda della pipeline.

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma**.

1. Per accedere e gestire l’archivio Git, visualizzerai l’opzione **Access Repo Info** .

   ![](assets/repos/access-repo1.png)

   Inoltre, se selezioni la scheda della pipeline **Non-Produzione** , visualizzerai anche l&#39;opzione **Accedi alle informazioni sul repository**.

   ![](assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >L&#39;opzione **Access Repo Info** è visibile agli utenti nel ruolo Developer o Deployment Manager. Facendo clic su questo pulsante si apre una finestra di dialogo che consente all’utente di trovare l’URL del proprio archivio Git di Cloud Manager insieme al nome utente e alla password.

   ![](assets/repos/access-repo-create.png)

   Le considerazioni importanti per gestire il Git in Cloud Manager sono le seguenti:

   * **URL**: URL del repository
   * **Nome utente**: Nome utente
   * **Password**: valore visualizzato quando si fa clic sul pulsante **Generate Password (Genera password)**.


      >[!NOTE]
      >Un utente può estrarre una copia del proprio codice e apportare modifiche nell&#39;archivio del codice locale. Quando è pronto, l’utente può eseguire nuovamente il commit delle modifiche del codice nell’archivio del codice remoto in Cloud Manager.
