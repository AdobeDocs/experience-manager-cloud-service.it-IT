---
title: Sospensione e riattivazione degli ambienti sandbox
description: Scopri in che modo gli ambienti di un programma sandbox entrano automaticamente in modalità di sospensione e come riattivarli.
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 42%

---


# Sospensione e riattivazione degli ambienti sandbox {#hibernating-introduction}

Gli ambienti di un programma sandbox entrano in modalità di sospensione se non viene rilevata alcuna attività per otto ore. La sospensione è specifica per gli ambienti dei programmi sandbox. Gli ambienti dei programmi di produzione non possono essere sospesi.

## Sospensione {#hibernation-introduction}

La sospensione può essere attivata automaticamente o manualmente.

* **Automatica**: la sospensione degli ambienti di un programma sandbox viene attivata automaticamente dopo otto ore di inattività. L’inattività è definita come l’assenza di richieste ai servizi di authoring, anteprima e pubblicazione.
* **Manuale**: l’utente può attivare manualmente la sospensione di un ambiente di un programma sandbox. Non è necessario perché la sospensione si verifica automaticamente come descritto in precedenza.

Potrebbero essere necessari alcuni minuti prima che gli ambienti del programma sandbox entrino in modalità di sospensione. Durante la sospensione i dati vengono conservati.

### Sospensione manuale di un ambiente di un programma sandbox {#using-manual-hibernation}

Puoi sospendere manualmente il programma sandbox da Console sviluppatori. L’accesso a Developer Console per un programma sandbox è disponibile per tutti gli utenti di Cloud Manager.

**Per sospendere manualmente un ambiente di un programma sandbox:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)**, fare clic su un *programma sandbox* che si desidera sospendere per visualizzarne i dettagli.

1. Nella scheda **Ambienti**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi su **Developer Console**.

   * Per ulteriori dettagli su Developer Console, consulta [Accesso a Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console).

   ![Opzione di menu Console sviluppatori](/help/implementing/cloud-manager/assets/developer-console-menu-option.png)

1. Nella pagina **Developer Console** fare clic su **Sospendi**.

<!-- UPDATE THESE SCREENSHOTS WHEN NEW AEM DEVELOPER CONSOLE UI IS RELEASED. AS OF OCTOBER 14, 2024, NEW UI IS STILL IN PRIVATE BETA -->

![Pulsante Sospendi](assets/hibernate-1.png)

1. Per confermare, fai clic su **Sospendi**.

   ![Conferma della sospensione](assets/hibernate-2.png)

Quando la sospensione viene eseguita correttamente, nella schermata **Developer Console** viene visualizzata la notifica di completamento del processo di sospensione per l&#39;ambiente in uso.

![Conferma della sospensione](assets/hibernate-4.png)

In Developer Console, fai clic sul collegamento **Ambienti** nel percorso di navigazione sopra l&#39;elenco a discesa **Pod** per visualizzare gli ambienti disponibili per la sospensione.

![Elenco degli ambienti da sospendere](assets/hibernate-1b.png)

## Riattivazione manuale di un programma sandbox da Developer Console {#de-hibernation-introduction}

Puoi sospendere manualmente il programma sandbox da Developer Console.

>[!IMPORTANT]
>
>L’utente con il ruolo **Sviluppatore** può riattivare un ambiente di un programma sandbox.

**Per riattivare manualmente un programma sandbox da Developer Console:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** fare clic sul programma che si desidera riattivare per visualizzarne i dettagli.

1. Nella scheda **Ambienti**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi su **Developer Console**.

   * Per ulteriori dettagli su Developer Console, consulta [Accesso a Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console).

1. Fare clic su **Riattiva**.

   ![Pulsante Riattiva](assets/de-hibernation-img1.png)

1. Per confermare, fai clic su **Riattiva**.

   ![Conferma riattivazione](assets/de-hibernation-img2.png)

1. Viene visualizzata una notifica dell’avvio del processo di riattivazione e aggiornamenti sull’avanzamento.

   ![Notifica dell’avanzamento della sospensione](assets/de-hibernation-img3.png)

1. Al termine del processo, l’ambiente del programma sandbox è nuovamente attivo.

   ![Riattivazione completa](assets/de-hibernation-img4.png)

In Developer Console, fai clic sul collegamento **Ambienti** nel percorso di navigazione sopra l&#39;elenco a discesa **Pod** per accedere agli ambienti disponibili per la riattivazione.

![Elenco dei pod sospesi](assets/de-hibernate-1b.png)

### Autorizzazioni per la riattivazione {#permissions-de-hibernate}

Tutti gli utenti con un profilo di prodotto che consente di accedere a AEM as a Cloud Service possono accedere a **Console sviluppatori** e riattivare l’ambiente.

## Accedere a un ambiente sospeso {#accessing-hibernated-environment}

Quando un utente effettua una richiesta del browser al servizio Author, Anteprima o Publish di un ambiente sospeso, incontra una pagina di destinazione. Questa pagina illustra lo stato di sospensione dell’ambiente e fornisce un collegamento a Developer Console per la riattivazione.

![Pagina di destinazione del servizio sospeso](assets/de-hibernation-img5.png)

## Distribuzioni e aggiornamenti di AEM {#deployments-updates}

Negli ambienti sospesi è ancora possibile eseguire distribuzioni e aggiornamenti AEM manuali.

* È possibile utilizzare una pipeline per distribuire il codice personalizzato negli ambienti sospesi. L’ambiente rimane sospeso e il nuovo codice viene visualizzato nell’ambiente alla sua riattivazione.

* Gli aggiornamenti AEM possono essere applicati agli ambienti sospesi e attivati manualmente da Cloud Manager. L’ambiente rimane sospeso e la nuova versione viene visualizzata nell’ambiente alla sua riattivazione.

## Sospensione ed eliminazione {#hibernation-deletion}

* Gli ambienti in un programma sandbox vengono automaticamente sospesi dopo otto ore di inattività.
   * L’inattività è definita come l’assenza di richieste ai servizi di authoring, anteprima e pubblicazione.
   * Una volta sospesi, possono essere [riattivati manualmente](#de-hibernation-introduction).
* I programmi sandbox vengono eliminati dopo sei mesi di sospensione continua. Al termine di questo periodo, possono essere ricreati.

>[!NOTE]
>
>Solo gli ambienti sandbox vengono eliminati automaticamente dopo sei mesi di ibernazione continua. Il programma sandbox con il relativo archivio e codice viene mantenuto.
