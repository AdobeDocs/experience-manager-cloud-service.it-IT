---
title: Crea programma
description: Scopri come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.
exl-id: 06287618-0328-40b1-bba8-84002283f23f
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 100%

---


# Crea programma {#creating-a-program}

Scopri come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.

## La storia finora {#story-so-far}

Nel documento precedente del percorso del componente aggiuntivo Demo di riferimento Adobe Experience Manager (AEM), [Comprendere l’installazione del componente aggiuntivo Demo di riferimento AEM,](installation.md), hai imparato come funziona il processo di installazione del componente aggiuntivo Demo di riferimento, illustrando come funzionano i diversi componenti insieme. Ora dovresti:

* Avere una conoscenza di base di Cloud Manager.
* Scoprire come le pipeline forniscono contenuto e configurazione ad AEM.
* Scoprire come i modelli possono creare siti precompilati con contenuti dimostrativi con pochi clic.

Questo articolo si basa su tali elementi fondamentali e mostra il primo passaggio di configurazione per creare un programma a scopo di test e utilizza una pipeline per distribuire il contenuto aggiuntivo.

## Obiettivo {#objective}

Questo documento spiega come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo. Dopo aver letto questo documento, dovresti essere in grado di effettuare le seguenti operazioni:

* Comprendere e spiegare come utilizzare Cloud Manager per creare un programma.
* Attivare il componente aggiuntivo Demo di riferimento per il nuovo programma.
* Eseguire una pipeline per distribuire il contenuto del componente aggiuntivo.

## Creazione di un programma {#create-program}

Dopo aver effettuato l’accesso a Cloud Manager, puoi creare un programma sandbox a scopo di test e demo.

>[!NOTE]
>
>L’utente deve avere il ruolo di **Proprietario business** in Cloud Manager nella tua organizzazione per poter creare programmi.

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Una volta effettuato l’accesso, assicurati di essere nell’organizzazione corretta controllando nell’angolo in alto a destra dello schermo. Se sei membro di una sola organizzazione, questo passaggio non è necessario.

   ![Panoramica di Cloud Manager](assets/cloud-manager.png)

1. Seleziona **Aggiungi programma** in alto a destra nella finestra.

1. Nella finestra di dialogo **Creiamo il tuo programma**:

   1. Inserisci un **Nome del programma** per descriverlo.
   1. Seleziona **Configura una sandbox** per il tuo **Obiettivo del programma**
   1. Seleziona **Continua**.

   ![Finestra di dialogo Crea programma](assets/create-program.png)

1. Nella finestra dii dialogo **Configura una sandbox** nella tabella **Soluzioni e componenti aggiuntivi**, espandi la voce **Sites** dell’elenco, toccandola o facendo clic su di essa, quindi seleziona **Demo di riferimento**.

   * Se desideri anche creare demo per AEM Screens, spunta l’opzione **Screens** nell’elenco. Seleziona **Aggiorna**.

   ![Selezione del componente aggiuntivo per una Demo di riferimento nella configurazione del programma](assets/select-reference-demo-add-on.png)


1. Seleziona **Crea** e Cloud Manager avvierà la configurazione del programma sandbox. Viene visualizzata la schermata panoramica del programma e una breve notifica nel banner indica che il processo è stato avviato. È stata aggiunta una scheda alla pagina panoramica del nuovo programma. Il processo di configurazione richiede alcuni minuti.

1. Una volta completata la configurazione, la scheda dell’ambiente nella pagina panoramica mostrerà lo stato come **Pronto**. Seleziona la scheda per poter aprire l’ambiente.

   ![Creazione del programma completata](assets/ready.png)

1. L’ambiente è pronto e il componente aggiuntivo è ora abilitato come opzione, ma il contenuto della Demo deve essere distribuito in AEM per essere disponibile. A questo scopo, seleziona il pulsante con i puntini di sospensione accanto alla pipeline Implementa nell’ambiente di sviluppo nella scheda **Pipeline** e seleziona **Esegui**.

   ![Avvia](assets/run.png)

1. La pipeline viene avviata e viene visualizzata una pagina che descrive l’avanzamento della distribuzione. Puoi spostarti da questa schermata quando il programma viene creato e, se necessario, tornare in un secondo momento.

   ![Distribuzione](assets/deployment.png)

Il completamento della pipeline può richiedere alcuni minuti. Una volta completata, il componente aggiuntivo e il relativo contenuto demo sono disponibili per l’utilizzo nell’ambiente di authoring AEM.

## Passaggio successivo {#what-is-next}

Adesso che hai completato questa parte del percorso del Componente aggiuntivo Demo di riferimento AEM, è necessario:

* Scopri come utilizzare Cloud Manager per creare un programma.
* Scopri come attivare il componente aggiuntivo Demo di riferimento per il programma.
* Puoi eseguire una pipeline per distribuire il contenuto aggiuntivo.

Approfondisci l’argomento e continua il tuo percorso del componente aggiuntivo Demo di riferimento AEM passando al documento [Creare un sito demo](create-site.md). In questa sezione imparerai a creare un sito demo in AEM basato su una libreria di modelli preconfigurati distribuiti dalla pipeline.

## Risorse aggiuntive {#additional-resources}

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=it): per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
