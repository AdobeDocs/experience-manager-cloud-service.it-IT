---
title: Configura un sito Edge Delivery per l’utilizzo di un archivio Git esterno
description: Scopri come collegare un sito Edge Delivery a un archivio Git privato o aziendale.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# Configura un sito Edge Delivery per l’utilizzo di un archivio Git esterno

Puoi configurare il tuo sito Edge Delivery per estrarre il codice da qualsiasi archivio Git privato già integrato in Cloud Manager.

**Fornitori Git supportati**

| Livello di supporto | Fornitori | Note |
| --- | --- | --- |
| Disponibilità generale | · GitHub Enterprise (versione self-hosted)<br>· Bitbucket (versione cloud)<br>· GitLab (versione cloud e self-hosted) | Connettersi senza richieste di abilitazione |
| Programma Alpha | Azure DevOps (versione cloud) | [Richiedi l’accesso](mailto:grp-cloudmanager_byog@adobe.com) |
| Programma Beta | Archivio ospitato da Adobe (creato in Cloud Manager) | [Richiedi l’accesso](mailto:grp-cloudmanager_byog@adobe.com) |

**Per configurare un sito Edge Delivery per l&#39;utilizzo di un archivio Git esterno:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** seleziona il programma con Edge Delivery Services configurato, in cui desideri configurare un sito Edge Delivery per utilizzare un archivio Git esterno.
1. Nella barra a sinistra, sotto l’intestazione **Programma**, fai clic su **![Icona Panoramica](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) Panoramica**.
1. Nella pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**.
1. Nella tabella **siti Edge Delivery**, fai clic su ![Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga del sito che desideri configurare per l’utilizzo di un archivio esterno, quindi fai clic su **Utilizza il tuo archivio Git**.
1. Nella finestra di dialogo Utilizza il tuo archivio Git, scegli nell’elenco a discesa **Nome archivio** un archivio Git con stato `READY`, quindi fai clic su **Conferma**.

   Cloud Manager restituisce un token segreto monouso. Se riconfiguri il sito, Cloud Manager genera un nuovo token segreto.

1. Copia il token e aggiungilo alla configurazione del sito in **helix-admin**, come descritto nella [guida sull’utilizzo del tuo archivio Git](https://www.aem.live/developer/byo-git).
1. In Cloud Manager, fai clic sull’![Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga del sito che hai appena configurato per l’utilizzo di un archivio esterno, quindi fai clic su **Codice di sincronizzazione**.
1. Scegli il ramo da sincronizzare e fai clic su **Sincronizza**.

Ogni commit su qualsiasi ramo ora attiva una sincronizzazione automatica. Utilizza di nuovo **Codice di sincronizzazione** ogni volta che è necessaria una sincronizzazione manuale completa.
