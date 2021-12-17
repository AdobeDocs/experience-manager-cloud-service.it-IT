---
title: Crea programma
description: Scopri come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.
source-git-commit: 52d65251744ce0ae5cf7a7e0a45b39d8fe78f13a
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# Crea programma {#creating-a-program}

Scopri come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione di siti rapidi AEM, [Comprendere l’installazione del componente aggiuntivo Demo di riferimento,](installation.md) hai imparato come funziona il processo di installazione del Reference Demos Add-On, illustrando come funzionano i diversi pezzi insieme. Ora dovresti:

* Conoscenza di base di Cloud Manager.
* Scopri come le pipeline forniscono contenuto e configurazione a AEM.
* Scopri come i modelli possono creare nuovi siti precompilati con contenuti dimostrativi con pochi clic.

Questo articolo si basa su tali elementi fondamentali e fa il primo passaggio di configurazione per creare un programma a scopo di test e utilizza una pipeline per distribuire il contenuto aggiuntivo.

## Obiettivo {#objective}

Questo documento spiega come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo. Dopo la lettura è necessario:

* Scopri come utilizzare Cloud Manager per creare un nuovo programma.
* Scopri come attivare il componente aggiuntivo Demo di riferimento per il nuovo programma.
* Puoi eseguire una pipeline per distribuire il contenuto aggiuntivo.

## Creare un programma {#create-program}

Dopo aver effettuato l’accesso a Cloud Manager, puoi creare un nuovo programma sandbox a scopo di test e demo.

>[!NOTE]
>
>L&#39;utente deve essere membro del **Proprietario business** in Cloud Manager nella tua organizzazione per creare programmi.

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Una volta effettuato l’accesso, assicurati di essere nell’organizzazione corretta effettuando il controllo nell’angolo in alto a destra dello schermo. Se sei membro di una sola organizzazione, questo passaggio non è necessario.

   ![Panoramica di Cloud Manager](assets/cloud-manager.png)

1. Tocca o fai clic su **Aggiungi programma** in alto a destra nella finestra.

1. In **Creiamo il programma** , assicurati che **Adobe Experience Manager** è selezionato in **Prodotti** quindi tocca o fai clic su **Continua**.

   ![Finestra di dialogo Crea programma](assets/create-program.png)

1. Nella finestra di dialogo successiva:

   * Fornisci un **Nome del programma** per descrivere il programma.
   * Tocca o fai clic su **Configurare una sandbox** per **Obiettivo del programma**

   Quindi tocca o fai clic su **Crea**.

   ![Nome del programma](assets/program-name.png)

1. Viene visualizzata la schermata di panoramica del programma in cui è possibile osservare il processo di creazione del programma. Cloud Manager fornisce stime del tempo rimanente. È possibile spostarsi da questa schermata quando il programma viene creato e, se necessario, tornare in un secondo momento.

   ![Creazione di programmi](assets/program-creation.png)

1. Al termine, Cloud Manager presenta una panoramica che include gli ambienti e le pipeline creati automaticamente.

   ![Creazione del programma completata](assets/creation-complete.png)

1. Modifica i dettagli del programma facendo clic sul nome del programma in alto a sinistra della pagina e nel menu a discesa seleziona **Modifica programma**.

   ![Modifica programma](assets/edit-program.png)

1. In **Modifica programma** finestra di dialogo, passa alla **Soluzioni e componenti aggiuntivi** scheda .

   ![Finestra di dialogo Modifica programma](assets/edit-program-dialog.png)

1. Sulla **Soluzioni e componenti aggiuntivi** scheda , espandi **Sites** voce nell&#39;elenco e quindi controllare **Demo di riferimento**. Tocca o fai clic su **Aggiorna**.

   ![Opzione Controlla demo di riferimento](assets/edit-program-add-on.png)

1. Il componente aggiuntivo è ora abilitato come opzione, ma il relativo contenuto deve essere distribuito per AEM essere disponibile. Torna alla pagina della panoramica del programma, tocca o fai clic su **Inizio** per avviare la pipeline per distribuire il contenuto aggiuntivo a AEM.

   ![Avvia](assets/deploy.png)

1. La pipeline viene avviata e viene visualizzata una pagina che descrive l’avanzamento della distribuzione. È possibile spostarsi da questa schermata quando il programma viene creato e, se necessario, tornare in un secondo momento.

   ![Implementazione](assets/deployment.png)

Una volta completata la pipeline, il componente aggiuntivo e il relativo contenuto demo sono disponibili per l’utilizzo nell’ambiente di authoring AEM.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso aggiuntivo Demo di riferimento AEM , devi:

* Scopri come utilizzare Cloud Manager per creare un nuovo programma.
* Scopri come attivare il componente aggiuntivo Demo di riferimento per il nuovo programma.
* Puoi eseguire una pipeline per distribuire il contenuto aggiuntivo.

Sviluppa questa conoscenza e continua il percorso aggiuntivo Demo di riferimento AEM esaminando il documento successivo [Creare un sito demo,](create-site.md) dove imparerai a creare un sito demo in AEM basato su una libreria di modelli preconfigurati distribuiti dalla pipeline.

## Risorse aggiuntive {#additional-resources}

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
