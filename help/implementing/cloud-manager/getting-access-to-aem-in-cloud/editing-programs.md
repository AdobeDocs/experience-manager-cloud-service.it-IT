---
title: Modifica dei programmi
description: Scopri come modificare i programmi di produzione e sandbox per regolare le loro opzioni dopo averli creati.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: d805ed744af0e5c95863a1c67439b384cc5d11b2
workflow-type: tm+mt
source-wordcount: '450'
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

1. La **Modifica programma** viene visualizzata la pagina . Sulla **Generale** , modifica il nome e la descrizione del programma.

   * È necessario selezionare almeno una soluzione per un programma.

   ![Scheda Generale](assets/edit-program-prod1.png)

1. Sulla **Soluzioni e componenti aggiuntivi** , modifica le soluzioni per il programma.

   ![Selezionare le soluzioni](assets/edit-prg.png)

1. Fai clic sulla freccia prima dei nomi delle soluzioni per visualizzare i componenti aggiuntivi facoltativi, ad esempio selezionando la **Commerce** opzione add-on in **Sites**.

   ![Modificare i componenti aggiuntivi](assets/edit-program-add-on.png)

1. Sulla **Vai alle impostazioni live** , modifica la data di pubblicazione pianificata per il programma.

   ![Modificare le impostazioni in tempo reale](assets/edit-program-go-live.png)

   * Questa data è solo per uso informativo e attiva il widget Go Live sulla pagina di panoramica del programma per fornire collegamenti all’interno del prodotto alla documentazione sulle best practice as a Cloud Service in modo tempestivo per allinearsi con il percorso che culmina in un’esperienza Go Live di successo e fluida.

1. Fai clic su **Aggiorna** per salvare le modifiche apportate al programma.

Tutte le volte che un programma viene modificato, inclusa l&#39;aggiunta o la rimozione di una soluzione o di un componente aggiuntivo, tali modifiche avranno effetto dopo la distribuzione successiva.

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
