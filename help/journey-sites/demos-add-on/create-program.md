---
title: Crea programma
description: Scopri come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.
exl-id: 06287618-0328-40b1-bba8-84002283f23f
source-git-commit: 7c33a618f474914ca80dff525552017c55a32517
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 68%

---


# Crea programma {#creating-a-program}

Scopri come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo.

## La storia finora {#story-so-far}

Nel documento precedente di AEM Reference Demos Add-On, [Comprendere l’installazione di AEM Reference Demos Add-On,](installation.md) hai imparato come funziona il processo di installazione del componente aggiuntivo Reference Demos, illustrando come funzionano i diversi componenti insieme. Ora dovresti:

* Avere una conoscenza di base di Cloud Manager.
* Scoprire come le pipeline forniscono contenuto e configurazione ad AEM.
* Scoprire come i modelli possono creare nuovi siti precompilati con contenuti dimostrativi con pochi clic.

Questo articolo si basa su tali elementi fondamentali e mostra il primo passaggio di configurazione per creare un programma a scopo di test e utilizza una pipeline per distribuire il contenuto aggiuntivo.

## Obiettivo {#objective}

Questo documento spiega come impostare un nuovo programma e una nuova pipeline per distribuire il componente aggiuntivo. Dopo la lettura dovresti:

* Scopri come utilizzare Cloud Manager per creare un nuovo programma.
* Scopri come attivare AEM Reference Demos Add-On per il nuovo programma.
* Puoi eseguire una pipeline per distribuire il contenuto aggiuntivo.

## Creare un programma {#create-program}

Dopo aver effettuato l’accesso a Cloud Manager, puoi creare un nuovo programma sandbox a scopo di test e demo.

>[!NOTE]
>
>L&#39;utente deve essere membro di **Proprietario business** ruolo in Cloud Manager nella tua organizzazione per creare programmi.

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Una volta effettuato l’accesso, assicurati di essere nell’organizzazione corretta controllando nell’angolo in alto a destra dello schermo. Se sei membro di una sola organizzazione, questo passaggio non è necessario.

   ![Panoramica di Cloud Manager](assets/cloud-manager.png)

1. Tocca o fai clic su **Aggiungi programma** in alto a destra nella finestra.

1. In **Crea il tuo programma** finestra di dialogo:

   1. Inserisci un **Nome del programma** per descriverlo.
   1. Tocca o fai clic su **Configura una sandbox** per l&#39;**Obiettivo del programma**
   1. Tocca o fai clic su **Continua**.

   ![Finestra di dialogo Crea programma](assets/create-program.png)

1. In **Configurare la sandbox** finestra di dialogo in **Soluzioni e componenti aggiuntivi** tabella, espandi **Sites** per inserire nell’elenco, tocca o fai clic su di esso, quindi seleziona **Demo di riferimento**.

   * Se desideri anche creare demo per AEM Screens, spunta anche l&#39;opzione **Screens** nell’elenco. Tocca o fai clic su **Aggiorna**.

   ![Selezione del componente aggiuntivo per una demo di riferimento nella configurazione del programma](assets/select-reference-demo-add-on.png)


1. Tocca o fai clic su **Crea** e Cloud Manager inizia a configurare il programma sandbox. Viene visualizzata la schermata di panoramica del programma e una breve notifica del banner indica che il processo è stato avviato. È stata aggiunta una scheda alla pagina della panoramica del nuovo programma. Il processo di configurazione richiederà alcuni minuti.

1. Una volta completata la configurazione, la scheda dell’ambiente nella pagina della panoramica mostra il suo stato come **Pronto**. Tocca o fai clic sulla scheda per aprire l’ambiente.

   ![Creazione del programma completata](assets/ready.png)

1. L’ambiente è pronto e il componente aggiuntivo è ora abilitato come opzione, ma il contenuto della demo deve essere distribuito all’AEM per essere disponibile. A questo scopo, tocca o fai clic sul pulsante con i puntini di sospensione accanto alla pipeline Distribuisci su sviluppo nel **Pipeline** e seleziona **Esegui**.

   ![Avvia](assets/run.png)

1. La pipeline viene avviata e viene visualizzata una pagina che descrive l’avanzamento della distribuzione. Puoi spostarti da questa schermata quando il programma viene creato e, se necessario, tornare in un secondo momento.

   ![Distribuzione](assets/deployment.png)

Il completamento della pipeline può richiedere alcuni minuti. Una volta completato, il componente aggiuntivo e il relativo contenuto demo sono disponibili per l’utilizzo nell’ambiente di authoring AEM.

## Novità {#what-is-next}

Adesso che hai completato questa parte del percorso di AEM Reference Demo Add-On, dovresti:

* Scopri come utilizzare Cloud Manager per creare un nuovo programma.
* Scopri come attivare AEM Reference Demos Add-On per il nuovo programma.
* Puoi eseguire una pipeline per distribuire il contenuto aggiuntivo.

Approfondisci questo argomento e continua il percorso con AEM Reference Demos Add-On consultando il documento successivo [Creare un sito demo,](create-site.md) dove imparerai a creare un sito demo in AEM basato su una libreria di modelli preconfigurati distribuiti dalla pipeline.

## Risorse aggiuntive {#additional-resources}

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=it): per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
