---
title: Aggiungere un archivio di Adobe in Cloud Manager
description: Scopri come aggiungere un archivio gestito da Adobe in Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# Aggiungere un archivio di Adobe in Cloud Manager {#adobe-repositories}

Scopri come aggiungere un archivio gestito da Adobe in Cloud Manager.

La pagina **Archivi** consente di aggiungere facilmente al programma selezionato altri archivi gestiti da Adobe.

**Per aggiungere un archivio di Adobe in Cloud Manager:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati a cui desideri aggiungere un archivio gestito da Adobe.

1. Dalla pagina **Panoramica programma**, nel menu laterale, fai clic sulla scheda ![Icona cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Archivi**.

1. Nella pagina **Archivi**, in alto a destra, fai clic su **Aggiungi archivio**.

   ![Pulsante Aggiungi archivio](assets/add-repository.png)

1. Nella finestra di dialogo **Aggiungi archivio**, accertati che **Archivio Adobe** sia selezionato come tipo di archivio.

1. Nei rispettivi campi di testo, immetti quanto segue:

   * **Nome archivio**: un nome espressivo per il nuovo archivio.
   * **Anteprima URL archivio**: non è necessario immettere un percorso URL o modificare il percorso esistente perché l’infrastruttura dell’archivio è già presente, completamente integrata e gestita da Adobe.
   * **Descrizione (facoltativa)**: una descrizione dettagliata dell’archivio.

   ![Finestra di dialogo Aggiungi archivio](assets/add-adobe-repository.png)

1. Fai clic su **Salva**.
Il nuovo archivio viene visualizzato nella tabella della pagina **Archivi**.

A questo punto potrai associarvi una [pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) o gestirlo all’interno della pagina](managing-repositories.md) [**Archivi**.

>[!TIP]
>
>Puoi anche aggiungere archivi GitHub da gestire direttamente come [archivi privati](private-repositories.md).
