---
title: Modifica dei programmi
description: Scopri come modificare i programmi di produzione e sandbox per regolare le loro opzioni dopo averli creati.
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Modifica dei programmi {#editing-programs}

Gli utenti con le autorizzazioni necessarie possono modificare [programmi di produzione creati nella tua organizzazione](creating-production-programs.md) nonché [programmi sandbox creati nella tua organizzazione.](creating-sandbox-programs.md) Modificando un programma è possibile:

* Aggiungi la soluzione Sites a un programma esistente con Assets e viceversa.
* Rimuovi Sites o Assets da un programma esistente sia con Sites che con Assets.
* Aggiungi un secondo diritto non utilizzato alla soluzione a un programma esistente o a un nuovo programma.
* Elimina i programmi sandbox.

>[!NOTE]
>
>Devi essere un membro del **Proprietario business** ruolo per modificare programmi o eliminare programmi sandbox.

Segui questi passaggi per modificare un programma.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Fai clic sul programma da modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma in alto a sinistra nella pagina e seleziona **Modifica programma**.

   ![Opzione Modifica programma](assets/edit-program-overview.png)

1. La **Modifica programma** vengono visualizzate due schede: **Generale** e **Soluzioni e componenti aggiuntivi**. Seleziona la **Generale** per modificare il nome e la descrizione del programma.

   * È necessario selezionare almeno una soluzione per un programma.

   ![Scheda Generale](assets/edit-program-prod1.png)

1. Seleziona la **Soluzioni e componenti aggiuntivi** per modificare le soluzioni del programma.

   ![Selezionare le soluzioni](assets/edit-prg.png)

1. Fai clic sulla freccia prima dei nomi delle soluzioni per visualizzare i componenti aggiuntivi facoltativi, ad esempio selezionando la **Commerce** opzione add-on in **Sites**.

   ![Modificare i componenti aggiuntivi](assets/edit-program-add-on.png)

1. Fai clic su **Aggiorna** per salvare le modifiche apportate al programma.

Una volta effettuati gli aggiornamenti, se le soluzioni selezionate sono cambiate, tali modifiche avranno effetto dopo la distribuzione successiva.

## Eliminazione dei programmi sandbox {#delete-sandbox-program}

L’eliminazione di un programma sandbox comporta la rimozione di tutti gli ambienti e le pipeline ad esso associate.

>[!TIP]
>
>Utenti con **Proprietario business** o **Gestione distribuzione** In alternativa, i ruoli possono eliminare i rispettivi ambienti di produzione e di stage invece dell’intero programma sandbox.

Per eliminare un programma sandbox, effettua le seguenti operazioni.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Fai clic sul programma da modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma in alto a sinistra nella pagina e seleziona **Elimina programma**.

   ![Opzione Elimina programma](assets/delete-sandbox1.png)

In alternativa, puoi fare clic sul pulsante con i puntini di sospensione sulla scheda del programma dalla pagina di panoramica di Cloud Manager e selezionare **Elimina programma**.

![Elimina sandbox dalla scheda del programma](assets/delete-sandbox2.png)

>[!NOTE]
>
>È possibile eliminare solo i programmi sandbox. Impossibile eliminare i programmi di produzione.