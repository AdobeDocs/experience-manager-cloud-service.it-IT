---
title: Modifica dei programmi
description: Scopri come modificare i programmi sandbox e di produzione per apportare modifiche alle opzioni dopo averli creati.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 401f853b197e67a6c54e4bf168081dc8165bd505
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 30%

---


# Modifica dei programmi {#editing-programs}

Per gestire e modificare i programmi, inizia da [**I miei programmi** console.](/help/implementing/cloud-manager/navigation.md) Il **I miei programmi** Questa pagina fornisce una panoramica di tutti i programmi a cui si ha accesso. Quando si seleziona un singolo programma, **Panoramica del programma** fornisce dettagli sul programma in una panoramica.

Dalla sezione **Panoramica del programma**, gli utenti con le autorizzazioni necessarie possono modificare [programmi di produzione creati nell’organizzazione](creating-production-programs.md) e [programmi sandbox creati nell’organizzazione.](creating-sandbox-programs.md) Modificando un programma è possibile:

* Aggiungere la soluzione Sites a un programma esistente con Assets e viceversa.
* Rimuovere Sites o Assets da un programma esistente con entrambi Sites e Assets.
* Aggiungere una seconda soluzione non utilizzata a un programma esistente o nuovo.
* Eliminare i programmi sandbox.

## Autorizzazioni {#permissions}

Devi essere membro di **Proprietario business** per modificare i programmi o eliminare i programmi sandbox e per accedere alla dashboard delle licenze.

## Modifica di un programma {#editing}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](#my-programs)** , fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Modifica programma**.

   ![Opzione Modifica programma](assets/edit-program-overview.png)

1. Il **Modifica programma** La pagina si apre su **Generale** scheda.

   ![Scheda Generale](assets/edit-program-prod1.png)

1. Le opzioni disponibili per la modifica del programma sono le stesse della creazione del programma.
   * Consulta i documenti [Creazione di programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) e [Creazione di programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) per informazioni dettagliate sulle singole opzioni.
   * [Opzioni aggiuntive](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) può essere disponibile per il programma di produzione in base ai diritti dell’organizzazione.

1. Clic **Aggiorna** per salvare le modifiche apportate al programma.

Le modifiche apportate al programma vengono salvate.

>[!NOTE]
>
>Ogni volta che si modifica un programma, incluso l&#39;aggiunta o la rimozione di una soluzione o di un componente aggiuntivo, tali modifiche diventano effettive dopo la distribuzione successiva.

## Eliminazione dei programmi sandbox {#delete-sandbox-program}

L’eliminazione di un programma sandbox comporta la rimozione di tutti gli ambienti e delle relative pipeline associate.

>[!TIP]
>
>In alternativa, gli utenti con i ruoli **Proprietario business** o **Responsabile dell’implementazione** possono eliminare gli ambienti di produzione e di staging al posto dell’intero programma sandbox.

Per eliminare un programma sandbox, effettuare le seguenti operazioni.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](#my-programs)** , fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Elimina programma**.

   ![Opzione Elimina programma](assets/delete-sandbox1.png)

In alternativa, dalla pagina della panoramica di Cloud Manager, accedi alla scheda del programma, fai clic sul pulsante con i puntini di sospensione e seleziona **Elimina programma**.

![Scheda Elimina sandbox da programma](assets/delete-sandbox2.png)

>[!NOTE]
>
>È possibile eliminare solo i programmi sandbox. I programmi di produzione non possono essere eliminati.
