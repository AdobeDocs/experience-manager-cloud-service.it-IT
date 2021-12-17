---
title: Crea sito demo
description: Crea un sito demo in AEM basato su una libreria di modelli preconfigurati.
source-git-commit: 52d65251744ce0ae5cf7a7e0a45b39d8fe78f13a
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 2%

---


# Crea sito demo {#creating-a-site}

Crea un sito demo in AEM basato su una libreria di modelli preconfigurati.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione di siti rapidi AEM, [Crea programma,](create-program.md) hai fatto il primo passaggio di configurazione per creare un programma a scopo di test e hai utilizzato una pipeline per distribuire il contenuto aggiuntivo. Ora dovresti:

* Scopri come utilizzare Cloud Manager per creare un nuovo programma.
* Scopri come attivare il componente aggiuntivo Demo di riferimento per il nuovo programma.
* Puoi eseguire una pipeline per distribuire il contenuto aggiuntivo.

Questo articolo descrive il passaggio successivo del processo creando un nuovo sito in AEM basato sui modelli del componente aggiuntivo Demo di riferimento.

## Obiettivo {#objective}

Questo documento spiega come creare un nuovo sito basato sui modelli del componente aggiuntivo Demo di riferimento. Dopo la lettura è necessario:

* Scopri come accedere all’ambiente di authoring AEM.
* Scopri come creare un sito basato su un modello.
* Scopri le nozioni di base per navigare nella struttura del sito e modificare una pagina.

## Creare un sito demo {#create-site}

Una volta implementato il componente aggiuntivo Demo di riferimento, la pipeline può accedere all’ambiente di authoring AEM per creare siti demo in base al contenuto aggiuntivo.

1. Dalla pagina di panoramica del programma in Cloud Manager, tocca o fai clic sul collegamento all’ambiente di authoring AEM.

   ![Accesso all’ambiente di authoring](assets/access-author.png)

1. Dal menu principale di AEM, tocca o fai clic su **Sites**.

   ![Accedere ai siti](assets/access-sites.png)

1. Dalla console Sites, tocca o fai clic su **Crea** in alto a destra dello schermo e seleziona **Sito da modello** nel menu a discesa .

   ![Crea sito da modello](assets/create-site-from-template.png)

1. Viene avviata la procedura guidata di creazione del sito. Nella colonna a sinistra puoi vedere i modelli demo distribuiti dalla pipeline nell’istanza di authoring. Tocca o fai clic su uno per selezionarlo e visualizzare i dettagli nella colonna a destra. Tocca o fai clic su **Avanti**.

   ![Creazione guidata sito](assets/site-creation-wizard.png)

1. Nella schermata successiva, specifica un titolo per il sito. Se omesso, è possibile specificare un nome di sito o generarlo dal titolo. Tocca o fai clic su **Crea**.

   * Il titolo del sito viene visualizzato nella barra del titolo del browser.
   * Il nome del sito diventa parte dell’URL.
   * Il nome del sito deve rispettare AEM convenzioni di denominazione delle pagine, i cui dettagli sono disponibili nella [Risorse aggiuntive](#additional-resources) sezione .

   ![Dettagli del sito](assets/site-details.png)

1. La creazione del sito viene confermata con una finestra di dialogo. Tocca o fai clic su **Fine**.

   ![Creazione del sito completata](assets/site-creation-complete.png)

Ora hai creato il tuo sito demo!

## Usa sito demo {#use-site}

Una volta creato il sito demo, puoi navigarlo e utilizzarlo come qualsiasi altro sito in AEM.

1. Il sito viene ora visualizzato nella console Sites.

   ![Nuovo sito demo nella console Sites](assets/new-demo-site.png)

1. Nell’angolo in alto a destra dello schermo, accertati che la visualizzazione della console sia impostata su **Vista a colonne**.

   ![Vista a colonne](assets/column-view.png)

1. Tocca o fai clic sul sito per esplorarne la struttura e il contenuto. La vista a colonne si espande continuamente durante la navigazione nella struttura del contenuto del sito demo.

   ![Struttura del sito](assets/site-structure.png)

1. Tocca o fai clic su una pagina per selezionarla, quindi tocca o fai clic su **Modifica** nella barra degli strumenti.

   ![Selezionate la pagina](assets/select-page.png)

1. Puoi modificare la pagina come qualsiasi altra pagina di contenuto AEM, ad esempio aggiungere o modificare componenti o risorse, e testare la funzionalità di AEM.

   ![Modifica pagina](assets/edit-page.png)

Congratulazioni! È ora possibile esplorare ulteriormente il contenuto del sito demo e scoprire tutto quello che AEM da offrire attraverso il contenuto delle best practice del componente aggiuntivo Demo di riferimento.

Crea siti aggiuntivi basati su altri modelli per esplorare altre funzionalità AEM.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso aggiuntivo Demo di riferimento AEM , devi:

* Scopri come accedere all’ambiente di authoring AEM.
* Scopri come creare un sito basato su un modello.
* Scopri le nozioni di base per navigare nella struttura del sito e modificare una pagina.

È ora possibile testare le funzioni di AEM utilizzando il contenuto aggiuntivo. Per capire come gestire questo contenuto demo, continua il percorso aggiuntivo Demo di riferimento AEM esaminando il documento successivo [Gestire i siti demo,](manage.md) informazioni sugli strumenti disponibili per gestire i siti demo e su come rimuoverli.

## Risorse aggiuntive {#additional-resources}

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Crea sito](/help/sites-cloud/administering/site-creation/create-site.md) - Scopri come utilizzare AEM per creare un sito utilizzando i modelli di sito per definire lo stile e la struttura del sito.
* [AEM convenzioni di denominazione delle pagine.](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices) - Per informazioni sulle convenzioni per l’organizzazione delle pagine AEM, consulta questa pagina .
* [AEM Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Esplora questo documento se hai poca esperienza AEM comprendere i concetti di base, come la navigazione e l’organizzazione della console.