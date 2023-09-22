---
title: Modifica dei programmi
description: Scopri come modificare i programmi sandbox e di produzione per apportare modifiche alle opzioni dopo averli creati.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 50%

---

# Modifica dei programmi {#editing-programs}

Gli utenti con le autorizzazioni necessarie possono modificare [programmi di produzione creati nell’organizzazione](creating-production-programs.md) e [programmi sandbox creati nell’organizzazione.](creating-sandbox-programs.md) Modificando un programma è possibile:

* Aggiungere la soluzione Sites a un programma esistente con Assets e viceversa.
* Rimuovere Sites o Assets da un programma esistente con entrambi Sites e Assets.
* Aggiungere una seconda soluzione non utilizzata a un programma esistente o nuovo.
* Eliminare i programmi sandbox.

## Autorizzazioni {#permissions}

Per modificare i programmi o eliminare i programmi sandbox, è necessario avere il ruolo di **Proprietario business**.

## Modifica di un programma {#editing}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Modifica programma**.

   ![Opzione Modifica programma](assets/edit-program-overview.png)

1. Viene visualizzata la pagina **Modifica programma**. Dalla scheda **Generale**, modifica il nome e la descrizione del programma.

   * È necessario selezionare almeno una soluzione per programma.

   ![Scheda Generale](assets/edit-program-prod1.png)

1. Dalla scheda **Soluzioni e componenti aggiuntivi**, modifica le soluzioni del programma.

   ![Selezione delle soluzioni](assets/edit-prg.png)

1. Fai clic sulla freccia che precede il nome della soluzione per visualizzare i componenti aggiuntivi facoltativi, ad esempio per selezionare **Commerce** opzione del componente aggiuntivo in **Sites**.

   ![Modifica dei componenti aggiuntivi](assets/edit-program-add-on.png)

1. Dalla scheda **Impostazioni pubblicazione**, modifica la data di pubblicazione pianificata per il programma.

   ![Modifica delle impostazioni di pubblicazione](assets/edit-program-go-live.png)

   * Questa data è esclusivamente a scopo informativo. Attiva il widget di pubblicazione nella pagina di panoramica del programma. A sua volta, fornisce collegamenti interni alla documentazione sulle best practice as a Cloud Service di Adobe Experience Manager (AEM) per allinearsi al percorso, che culmina in un’esperienza di lancio di successo.
   * Questa scheda non è disponibile per i programmi sandbox.

1. Clic **Aggiorna** per salvare le modifiche apportate al programma.

Ogni volta che si modifica un programma, incluso l&#39;aggiunta o la rimozione di una soluzione o di un componente aggiuntivo, tali modifiche diventano effettive dopo la distribuzione successiva.

Se il programma di produzione aveva abilitato la sicurezza avanzata, sarà disponibile la scheda aggiuntiva **Sicurezza avanzata** nella finestra **Modifica programma**, per confermare che la funzione è attiva per il programma.

![Protezione avanzata attiva per un programma](assets/edit-program-enhanced.png)

Non è possibile modificare questa impostazione dopo la creazione del programma. Per ulteriori informazioni sull&#39;opzione di protezione avanzata, vedere [Creazione di programmi di produzione](creating-production-programs.md).

## Eliminazione dei programmi sandbox {#delete-sandbox-program}

L’eliminazione di un programma sandbox comporta la rimozione di tutti gli ambienti e delle relative pipeline associate.

>[!TIP]
>
>In alternativa, gli utenti con i ruoli **Proprietario business** o **Responsabile dell’implementazione** possono eliminare gli ambienti di produzione e di staging al posto dell’intero programma sandbox.

Per eliminare un programma sandbox, effettuare le seguenti operazioni.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Elimina programma**.

   ![Opzione Elimina programma](assets/delete-sandbox1.png)

In alternativa, dalla pagina della panoramica di Cloud Manager, accedi alla scheda del programma, fai clic sul pulsante con i puntini di sospensione e seleziona **Elimina programma**.

![Scheda Elimina sandbox da programma](assets/delete-sandbox2.png)

>[!NOTE]
>
>È possibile eliminare solo i programmi sandbox. I programmi di produzione non possono essere eliminati.
