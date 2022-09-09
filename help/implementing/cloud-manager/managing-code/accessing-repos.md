---
title: Accesso agli archivi
description: Scopri come accedere e gestire l’archivio Git utilizzando la gestione autonoma dell’account Git di Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---

# Accesso agli archivi {#accessing-repos}

Scopri come accedere e gestire l’archivio Git utilizzando la gestione autonoma dell’account Git di Cloud Manager.

## Utilizzo della gestione dell’account dell’archivio self-service {#self-service-repos}

Cloud Manager consente di recuperare facilmente le informazioni sull’archivio utilizzando **Accesso alle informazioni sul repository** pulsante disponibile in modo visibile sulla scheda della pipeline.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** e trova la **Accesso alle informazioni sul repository** per accedere e gestire il tuo archivio Git.

   ![Pulsante Accedi alle informazioni sui repository nella scheda Ambienti](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Fai clic sul pulsante **Visualizza informazioni repository** per aprire una finestra di dialogo da visualizzare:

   * URL dell’archivio Git di Cloud Manager.
   * Nome utente git.
   * La password git, il cui valore viene visualizzato quando **Genera password** fai clic su .

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Utilizzando queste credenziali, l’utente può clonare una copia locale dell’archivio, apportare modifiche all’archivio locale e, quando è pronto, eseguire il commit di eventuali modifiche al codice nell’archivio del codice remoto in Cloud Manager.

La **Accesso alle informazioni sul repository** è disponibile anche nella **Non produzione** scheda pipeline **Tubi** il Card.

![Pulsante Accedi alle informazioni sui repository nella scheda non di produzione](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>La **Accesso alle informazioni sul repository** è visibile agli utenti con **Sviluppatore** o **Gestione distribuzione** ruoli.
