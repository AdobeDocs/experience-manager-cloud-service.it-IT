---
title: Configurare un sito Edge Delivery per l’utilizzo di un archivio Git esterno
description: Scopri come collegare un sito Edge Delivery a un archivio Git privato o aziendale.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 239ee3021057dd108d18ab2d7729680692223403
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 7%

---


# Configurare un sito Edge Delivery per l’utilizzo di un archivio Git esterno

Puoi configurare il tuo sito Edge Delivery per estrarre il codice da qualsiasi archivio Git privato già integrato in Cloud Manager.

**Fornitori Git supportati**

| Livello di supporto | Fornitori | Note |
| --- | --- | --- |
| Disponibilità generale | · GitHub Enterprise (versione self-hosted)<br>· Bitbucket (versione cloud)<br>· GitLab (versione cloud e self-hosted) | Connettersi senza richieste di abilitazione |
| Programma Alpha | Azure DevOps (versione cloud) | [Richiedi accesso](mailto:grp-cloudmanager_byog@adobe.com) |
| programma Beta | Archivio ospitato da Adobe (creato in Cloud Manager) | [Richiedi accesso](mailto:grp-cloudmanager_byog@adobe.com) |

**Per configurare un sito Edge Delivery per l&#39;utilizzo di un archivio Git esterno:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, selezionare il programma con Edge Delivery Services configurato, in cui si desidera configurare un sito Edge Delivery per l&#39;utilizzo di un archivio Git esterno.

1. Nella barra a sinistra, sotto l&#39;intestazione **Programma**, fai clic su **![Icona Panoramica](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) Panoramica**.

1. Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**.

1. Nella tabella **Edge Delivery Sites**, fai clic su ![Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga il cui sito desideri configurare per l&#39;utilizzo di un archivio esterno, quindi fai clic su **Porta il tuo Git**.

1. Nella finestra di dialogo Porta il tuo Git, seleziona dall&#39;elenco a discesa **Nome archivio** un archivio Git con stato `READY`, quindi fai clic su **Conferma**.

   Cloud Manager restituisce un token segreto monouso. Se riconfiguri il sito, Cloud Manager genera un nuovo token segreto.

1. Copiare il token e aggiungerlo alla configurazione del sito in **helix-admin**, come descritto nella [guida Git BYO](https://www.aem.live/developer/byo-git).

1. In Cloud Manager, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga il cui sito è stato appena configurato per l&#39;utilizzo di un archivio esterno, quindi fai clic su **Codice di sincronizzazione**.

1. Selezionare il ramo da sincronizzare e fare clic su **Sincronizza**.

Ogni commit su qualsiasi ramo ora attiva una sincronizzazione automatica. Utilizza di nuovo **Codice di sincronizzazione** ogni volta che è necessaria una sincronizzazione manuale completa.

