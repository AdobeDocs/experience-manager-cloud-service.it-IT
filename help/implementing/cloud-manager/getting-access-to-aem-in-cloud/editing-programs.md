---
title: Modificare programmi
description: Scopri come modificare i programmi sandbox e di produzione per apportare modifiche alle opzioni dopo averli creati.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 25%

---


# Modifica programmi {#editing-programs}

Per gestire e modificare i programmi, iniziare dalla console [**Programmi**](/help/implementing/cloud-manager/navigation.md). La pagina **Programmi personali** fornisce una panoramica di tutti i programmi a cui si ha accesso. Quando si seleziona un singolo programma, la pagina **Panoramica del programma** fornisce i dettagli del programma.

Dalla **Panoramica del programma**, gli utenti con le autorizzazioni necessarie possono modificare [programmi di produzione creati nell&#39;organizzazione](creating-production-programs.md) e [programmi sandbox creati nell&#39;organizzazione](creating-sandbox-programs.md). Modificando un programma è possibile:

* Aggiungere la soluzione Sites a un programma esistente con Assets e viceversa.
* Rimuovere Sites o Assets da un programma esistente con entrambi Sites e Assets.
* Aggiungere una soluzione non utilizzata a un programma esistente o crearne uno nuovo.
* Eliminare i programmi sandbox.

## Autorizzazioni {#permissions}

È necessario avere il ruolo **Proprietario business** per modificare i programmi, eliminare i programmi sandbox e accedere alla dashboard delle licenze.

## Modificare un programma {#editing}

Ogni volta che si modifica un programma, incluso l&#39;aggiunta o la rimozione di una soluzione o di un componente aggiuntivo, tali modifiche diventano effettive dopo la distribuzione successiva.

**Per modificare un programma:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella pagina **[Programmi personali](#my-programs)** fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Modifica programma**.

   ![Opzione Modifica programma](assets/edit-program-overview.png)

1. La pagina **Modifica programma** si apre nella scheda **Generale**.

   ![Scheda Generale](assets/edit-program-prod1.png)

1. Le opzioni disponibili per la modifica del programma sono le stesse per la creazione del programma.
   * Per informazioni dettagliate sulle singole opzioni, consulta [Creare programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) e [Creare programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).
   * [Ulteriori opzioni](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) potrebbero essere disponibili per il programma di produzione in base ai diritti dell&#39;organizzazione.

1. Fai clic su **Aggiorna** per salvare le modifiche apportate al programma.

## Eliminare un programma sandbox {#delete-sandbox-program}

L’eliminazione di un programma sandbox comporta la rimozione di tutti gli ambienti e delle relative pipeline associate.

>[!TIP]
>
>In alternativa, gli utenti con i ruoli **Proprietario business** o **Responsabile dell’implementazione** possono eliminare gli ambienti di produzione e di staging al posto dell’intero programma sandbox.

**Per eliminare un programma sandbox:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella pagina **[Programmi personali](#my-programs)** fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Elimina programma**.

   ![Opzione Elimina programma](assets/delete-sandbox1.png)

In alternativa, è possibile fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) sulla scheda del programma nella pagina della panoramica di Cloud Manager e selezionare **Elimina programma**.

![Scheda Elimina sandbox da programma](assets/delete-sandbox2.png)

>[!NOTE]
>
>È possibile eliminare solo i programmi sandbox. I programmi di produzione non possono essere eliminati.
