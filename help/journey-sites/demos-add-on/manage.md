---
title: Gestire i siti demo
description: Scopri gli strumenti disponibili per gestire i siti demo e come rimuoverli.
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Gestire i siti demo {#manage-demo-sites}

Scopri gli strumenti disponibili per gestire i siti demo e come rimuoverli.

## La storia finora {#story-so-far}

Nel documento precedente del percorso aggiuntivo Demos di riferimento AEM, [Crea sito,](create-site.md) hai creato un nuovo sito demo basato sui modelli del componente aggiuntivo Demo di riferimento. Ora dovresti:

* Scopri come accedere all’ambiente di authoring AEM.
* Scopri come creare un sito basato su un modello.
* Scopri le nozioni di base per navigare nella struttura del sito e modificare una pagina.

Se anche [abilitato AEM Screens per il sito dimostrativo,](screens.md) inoltre:

* Scopri le basi di AEM Screens.
* Comprendere il contenuto demo di We.Cafe .
* Scopri come configurare AEM Screens per We.Cafe.

Ora che hai il tuo sito demo da esplorare, questo articolo descrive gli strumenti disponibili per aiutarti a gestire i tuoi siti demo e come rimuoverli.

## Obiettivo {#objective}

Questo documento illustra come gestire i siti demo creati. Dopo la lettura è necessario:

* Scopri come accedere alle utility demo self-service.
* Scopri quali utilità sono disponibili per te.
* Come eliminare un sito o un modello demo esistente.

## Accesso alle utility demo self-service {#accessing-utilities}

Ora che avete i vostri siti dimostrativi, probabilmente vorreste sapere come gestirli. La pipeline non solo ha implementato i modelli di sito per fornire il contenuto dei siti demo, ma ha anche implementato un set di utilità per gestire tali siti.

1. Dalla barra di navigazione globale AEM, seleziona **Strumenti** -> **Demo di riferimento** -> **Utilità Demo di riferimento**.

   ![Utilità demo self-service](assets/demo-utilities.png)

1. Utilità demo di riferimento è una raccolta di utili funzionalità per la configurazione e il monitoraggio dell’ambiente Adobe Experience Manager. La visualizzazione iniziale è la **Dashboard**, che funge da controllo dello stato dell’ambiente e della relativa funzionalità demo.

   ![Dashboard](assets/dashboard.png)

Utilità demo self-service fornisce una serie di strumenti.

* **Elimina siti** - Seleziona il sito da eliminare in questa istanza di Adobe Experience Manager. Tieni presente che si tratta di un’azione distruttiva e non può essere annullata una volta avviata.
* **Elimina modelli di sito** - Seleziona il modello di sito da eliminare in questa istanza di Adobe Experience Manager. Prima di eliminare un modello di sito, assicurati che vengano eliminati anche tutti i siti che fanno riferimento al modello. Tieni presente che si tratta di un’azione distruttiva e non può essere annullata una volta avviata.
* **Cache Prime Author** - In questo modo verranno recuperate diverse risorse all’interno dell’istanza di Adobe Experience Manager, velocizzando i tempi di recupero. Potrebbero volerci diversi secondi.
* **App Android** - Strumenti per l’installazione e l’avvio della dimostrazione dell’app Android. Crea un sito basato su **App a pagina singola WKND** per compilare la pagina. Utilizza da un dispositivo Android, un emulatore o Bluestacks.
* **Preferenze utente** - Disattivare le finestre di dialogo a comparsa dei tutorial.
* **Configurazione GraphQL** - Configurazione rapida dell’endpoint GraphQL globale.

## Eliminazione di siti e modelli demo {#deleting}

Dopo aver testato un set di funzionalità AEM, potrebbe non essere più necessario il sito demo o persino il modello su cui si basa. È facile eliminare sia i siti demo che i modelli di sito.

1. Accedere al **Utilità Demo di riferimento** e tocca o fai clic su **Elimina siti**.

   ![Elimina siti](assets/delete-sites.png)

1. I siti disponibili sono presentati in un elenco. Controlla il sito o i siti che desideri eliminare, quindi tocca o fai clic su **Elimina**.

   >[!CAUTION]
   >
   >L’eliminazione di siti e modelli è un’azione distruttiva e non può essere annullata una volta avviata.

1. Conferma l’eliminazione del sito nella finestra di dialogo.

   ![Conferma eliminazione sito](assets/confirm-site-delete.png)

1. AEM elimina il sito o i siti selezionati e ne mostra l’avanzamento quando **Elimina** precedentemente.

   ![Elimina stato](assets/delete-progress.png)

Il sito viene ora eliminato.

È possibile eliminare i modelli nello stesso modo sotto l’intestazione **Elimina modelli di sito** in **Utilità Demo di riferimento**.

>[!CAUTION]
>
>Prima di eliminare un modello di sito, assicurati che vengano eliminati anche tutti i siti che fanno riferimento al modello.

## Fine del Percorso? {#end-of-journey}

Congratulazioni! Hai completato il percorso aggiuntivo Demos di riferimento AEM! Ora dovresti:

* Scopri le nozioni di base di Cloud Manager e come le pipeline forniscono contenuti e configurazioni da AEM.
* Scopri come utilizzare Cloud Manager per creare un nuovo programma.
* Scopri come attivare il componente aggiuntivo Demos di riferimento per il nuovo programma ed essere in grado di eseguire una pipeline per distribuire il contenuto aggiuntivo.
* Scopri come accedere all’ambiente di authoring AEM per creare un sito basato su un modello.
* Scopri come accedere alle utility demo self-service.
* Scopri come eliminare un sito o un modello demo esistente.

Ora puoi esplorare le funzionalità di AEM utilizzando i tuoi siti demo. Tuttavia AEM è uno strumento potente e ci sono molte opzioni aggiuntive disponibili. Consulta alcune delle risorse aggiuntive disponibili nella sezione [Sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Per ulteriori informazioni sulle funzioni di Cloud Manager, consulta direttamente i documenti tecnici approfonditi.
* [Crea sito](/help/sites-cloud/administering/site-creation/create-site.md) - Scopri come utilizzare AEM per creare un sito utilizzando i modelli di sito per definire lo stile e la struttura del sito.
* [AEM convenzioni di denominazione delle pagine.](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices) - Per informazioni sulle convenzioni per l’organizzazione delle pagine AEM, consulta questa pagina .
* [AEM Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Esplora questo documento se hai poca esperienza AEM comprendere i concetti di base, come la navigazione e l’organizzazione della console.
* [AEM documentazione tecnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) - Se hai già una conoscenza approfondita di AEM, potresti voler consultare direttamente i documenti tecnici approfonditi.
* [Modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md) - Per ulteriori informazioni sulla struttura dei modelli di sito e sulla relativa modalità di creazione, consulta questo documento.
