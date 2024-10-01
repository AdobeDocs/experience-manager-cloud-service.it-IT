---
title: Aggiungere un archivio di Adobi in Cloud Manager
description: Scopri come aggiungere un archivio gestito da un Adobe in Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f2364de6237ca9f0285815b581bcf3881488188d
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---

# Aggiungere un archivio di Adobi in Cloud Manager {#adobe-repositories}

Scopri come aggiungere un archivio gestito da un Adobe in Cloud Manager.

La pagina **Archivi** semplifica l&#39;aggiunta di ulteriori archivi gestiti da Adobe a un programma selezionato.

**Per aggiungere un archivio di Adobi in Cloud Manager:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l&#39;organizzazione e il programma appropriati a cui desideri aggiungere un archivio gestito da Adobe.

1. Nella pagina **Panoramica programma**, nel menu laterale, fare clic sulla scheda ![Icona cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Archivi**.

1. Nella pagina **Archivi**, in alto a destra, fare clic su **Aggiungi archivio**.

   ![Pulsante Aggiungi archivio](assets/add-repository.png)

1. Nella finestra di dialogo **Aggiungi archivio**, accertati che sia selezionato **Archivio Adobe** come tipo di archivio.

1. Nei rispettivi campi di testo, immetti quanto segue:

   * **Nome archivio** - Nome espressivo per il nuovo archivio.
   * **Anteprima URL archivio** - Non è necessario immettere un percorso URL o modificare il percorso esistente perché l&#39;infrastruttura del repository è già installata e completamente integrata e gestita da Adobe.
   * **Descrizione (facoltativa)**: descrizione dettagliata dell&#39;archivio.

   ![Finestra di dialogo Aggiungi archivio](assets/add-adobe-repository.png)

1. Fai clic su **Salva**.
Il nuovo archivio viene visualizzato nella tabella della pagina **Archivi**.

È ora possibile associare una [pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) a essa o gestirla all&#39;interno della [**pagina Archivi**](managing-repositories.md).

>[!TIP]
>
>Puoi anche aggiungere archivi GitHub da gestire direttamente come [archivi privati.](private-repositories.md)
