---
title: Modificare programmi
description: Scopri come modificare i programmi sandbox e di produzione per apportare modifiche alle opzioni dopo averli creati.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 1c42dff8efb505d050583c8af2f150a7f862d8c9
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 11%

---


# Modifica programmi {#editing-programs}

Per gestire e modificare i programmi, iniziare dalla console [**Programmi**](/help/implementing/cloud-manager/navigation.md). La pagina **Programmi personali** fornisce una panoramica di tutti i programmi a cui si ha accesso. Quando si seleziona un singolo programma, la pagina **Panoramica del programma** fornisce una panoramica dei dettagli del programma.

Dalla **Panoramica del programma**, gli utenti con le autorizzazioni necessarie possono modificare [programmi di produzione creati nell&#39;organizzazione](creating-production-programs.md) e [programmi sandbox creati nell&#39;organizzazione](creating-sandbox-programs.md). Modificando un programma, è possibile effettuare le seguenti operazioni:

* Aggiungere la soluzione Sites a un programma esistente con Assets e viceversa.
* Rimuovi Sites o Assets da un programma esistente con sia Sites che Assets.
* Aggiungere una soluzione non utilizzata a un programma esistente o crearne uno nuovo.
* Contrassegna i programmi di produzione per l&#39;eliminazione.
* Eliminare i programmi sandbox.

## Autorizzazioni {#permissions}

È necessario avere il ruolo **Proprietario business** per modificare i programmi, eliminare i programmi sandbox, contrassegnare i programmi di produzione per l&#39;eliminazione e accedere alla dashboard delle licenze.

## Modificare un programma {#editing}

Ogni volta che si modifica un programma, incluso l&#39;aggiunta o la rimozione di una soluzione o di un componente aggiuntivo, tali modifiche diventano effettive dopo la distribuzione successiva.

**Per modificare un programma:**

1. Accedi a Cloud Manager all&#39;indirizzo [experience.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
1. Seleziona l’organizzazione appropriata.
1. Nella pagina **Programmi personali** fare clic sul programma che si desidera modificare.
1. Fare clic sul nome del programma nell&#39;angolo superiore sinistro della pagina, quindi selezionare **Modifica programma**.

   ![Opzione Modifica programma nel menu a discesa del programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program.png)

1. Nella finestra di dialogo **Modifica programma**, utilizzare le schede per impostare le varie opzioni desiderate.

   ![Scheda Generale](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program-dialog-box.png)

   Le opzioni disponibili per la modifica del programma sono le stesse per la creazione del programma.
   * Puoi configurare se viene eseguito il provisioning di un livello di pubblicazione per i nuovi ambienti (Beta). Consulta [Livello di pubblicazione flessibile (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).
   * Per informazioni dettagliate sulle singole opzioni, consulta [Creare programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) e [Creare programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).
   * [Ulteriori opzioni](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) potrebbero essere disponibili per il programma di produzione in base ai diritti dell&#39;organizzazione.

1. Fai clic su **Aggiorna** per salvare le modifiche.

## Contrassegna un programma di produzione per l&#39;eliminazione {#delete-production-program}

L’eliminazione di un programma di produzione è un processo in due fasi. Un Proprietario business contrassegna il programma per l’eliminazione, che attiva una convalida e un periodo di rimozione. Il programma viene quindi rimosso definitivamente dopo la scadenza del periodo di rimozione.

Quando un programma di produzione è contrassegnato per l’eliminazione, si verifica quanto segue:

* Il credito associato al programma di produzione viene restituito al cliente.
* Vengono rimossi tutti gli ambienti appartenenti al programma di produzione.

Prima di avviare la contrassegnazione per l&#39;eliminazione, il sistema verifica se il programma di produzione è idoneo per l&#39;eliminazione. Se il contrassegno non riesce, il programma di produzione passa a uno stato `Failed to mark for deletion`.

>[!NOTE]
>
>Questo processo non influisce sui programmi sandbox. Per eliminare un programma sandbox, vedere [Eliminare un programma sandbox](#delete-sandbox-program).

**Per contrassegnare un programma di produzione per l&#39;eliminazione:**

1. Accedi a Cloud Manager all&#39;indirizzo [experience.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
1. Seleziona l’organizzazione appropriata.
1. Nella pagina **I miei programmi**, per il programma di produzione che si desidera contrassegnare per l&#39;eliminazione, fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi su **Elimina programma**.

   ![Se si seleziona Elimina programma dall&#39;elenco a discesa di un programma di produzione ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete1.png)*L&#39;esempio di programma di produzione sopra riportato è solo a scopo illustrativo.*

1. Nella finestra di dialogo **Contrassegna programma di produzione per l&#39;eliminazione**, controlla l&#39;avviso che elenca le risorse collegate al programma, inclusi gli ambienti di produzione, stage e sviluppo.

   ![Finestra di dialogo Elimina programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2.png)


   >[!NOTE]
   >
   >Se il programma di produzione dispone di risorse di blocco, ad esempio ambienti in fase di aggiornamento, il pulsante **Contrassegna per eliminazione** è disabilitato. Prima di contrassegnare il programma per l&#39;eliminazione, attendere che tutte le risorse del programma siano sbloccate.
   >
   >![La finestra di dialogo Contrassegna programma di produzione per l&#39;eliminazione indica che il programma non può essere eliminato perché contiene risorse di blocco](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2b.png)


1. Per confermare, digitare il nome del programma come visualizzato nella finestra di dialogo, quindi fare clic su **Contrassegna per l&#39;eliminazione**.

   Dopo la conferma, il programma di produzione mostra uno stato **Contrassegno per l&#39;eliminazione** durante l&#39;esecuzione del processo.

   ![Contrassegno dello stato di eliminazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete3.png)

   Al termine, la scheda del programma di produzione si aggiorna a **Contrassegnato per l&#39;eliminazione** con un badge di avviso associato.

   ![Stato contrassegnato per l&#39;eliminazione con badge di avviso associato](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete4.png)

1. Fai clic sul badge Avviso sulla scheda del programma di produzione per visualizzare la data di rimozione permanente pianificata.

   ![Visualizzazione della data di rimozione permanente pianificata del programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete5.png)

   Trascorso il periodo di rimozione, il programma viene rimosso definitivamente e non può essere ripristinato.

### Rimuovere il contrassegno da un programma di produzione per eliminarlo {#unmark-from-deletion}

È possibile ripristinare un programma di produzione contrassegnato ** per l&#39;eliminazione finché non si è ancora verificata la rimozione permanente.

>[!IMPORTANT]
>
>Il ripristino di un programma di produzione contrassegnato per l&#39;eliminazione richiede che il cliente disponga di crediti disponibili.

**Per annullare il contrassegno di un programma di produzione dall&#39;eliminazione:**

1. Nella pagina **I miei programmi**, individua la scheda del programma di produzione che mostra **Contrassegnato per l&#39;eliminazione**.

1. Nella scheda del programma di produzione, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi fai clic su **Rimuovi contrassegno per l&#39;eliminazione**.

   ![Annullamento del contrassegno della data di rimozione permanente pianificata del programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-unmarkfordelete6.png)

   Il programma di produzione non è contrassegnato per l’eliminazione.

## Eliminare un programma sandbox {#delete-sandbox-program}

L’eliminazione di un programma sandbox comporta la rimozione di tutti gli ambienti e delle relative pipeline associate.

>[!TIP]
>
>In alternativa, gli utenti con i ruoli **Proprietario business** o **Responsabile dell’implementazione** possono eliminare gli ambienti di produzione e di staging al posto dell’intero programma sandbox.

**Per eliminare un programma sandbox:**

1. Accedi a Cloud Manager all&#39;indirizzo [experience.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
1. Seleziona l’organizzazione appropriata.

1. Nella pagina **[I miei programmi](#my-programs)**, fare clic sul programma sandbox che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma sandbox in alto a sinistra della pagina e seleziona **Elimina programma**.

   ![Opzione Elimina programma](assets/delete-sandbox1.png)

In alternativa, puoi fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) sulla scheda del programma sandbox nella pagina della panoramica di Cloud Manager e selezionare **Elimina programma**.

![Scheda Elimina sandbox da programma](assets/delete-sandbox2.png)
