---
title: Pubblicare contenuti tradotti
description: Scopri come pubblicare i contenuti localizzati.
source-git-commit: 3ab886361dc01c943bd00025695d34a218b1aa41
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# Pubblicare contenuti tradotti {#publish-content}

Scopri come pubblicare i contenuti localizzati.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di localizzazione AEM headless, [Traduci contenuto](configure-connector.md) hai imparato a utilizzare AEM progetti di traduzione per tradurre i contenuti headless. Ora dovresti:

* Scopri cos’è un progetto di traduzione.
* Potrai creare nuovi progetti di traduzione.
* Utilizza i progetti di traduzione per tradurre i tuoi contenuti headless.

Al termine della traduzione iniziale, questo articolo illustra il passaggio successivo per la pubblicazione dei contenuti e le operazioni da eseguire per aggiornare le traduzioni man mano che il contenuto principale della lingua cambia.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come pubblicare contenuti headless in AEM e come creare un flusso di lavoro continuo per mantenere le traduzioni aggiornate. Dopo aver letto questo documento, è necessario:

* Comprendere il modello di AEM di pubblicazione dell’autore.
* Scopri come pubblicare i contenuti tradotti.
* Puoi implementare un modello di aggiornamento continuo per i contenuti tradotti.

## Modello di pubblicazione AEM {#author-publish}

Prima di pubblicare i contenuti, è utile comprendere AEM modello di pubblicazione dell’autore. Nei termini più semplici, AEM divide gli utenti del sistema in due gruppi.

1. Coloro che creano e gestiscono il contenuto e il sistema
1. Coloro che utilizzano il contenuto dal sistema.

AEM è quindi fisicamente separato in due istanze.

1. L’istanza **author** è il sistema in cui autori e amministratori di contenuti lavorano per creare e gestire i contenuti.
1. L&#39;istanza **publish** è il sistema che consegna il contenuto ai consumatori.

Una volta creato il contenuto sull’istanza di authoring, deve essere trasferito nell’istanza di pubblicazione per renderlo disponibile per il consumo. Il processo di trasferimento dall&#39;autore alla pubblicazione si chiama **pubblicazione**.

## Pubblicazione del contenuto tradotto {#publishing}

Una volta che sei soddisfatto dello stato dei contenuti tradotti, puoi pubblicarli in modo che i servizi headless possano usarli. Il modo più semplice per farlo è passare alla cartella delle risorse del progetto.

```text
/content/dam/<your-project>/
```

In questo percorso sono presenti sottocartelle per ogni lingua di traduzione e puoi scegliere quale pubblicare.

1. Vai a **Navigazione** -> **Risorse** -> **File** e apri la cartella del progetto.
1. Qui è possibile visualizzare la cartella principale della lingua e tutte le altre cartelle della lingua. Seleziona la lingua o le lingue localizzate da pubblicare.
   ![Seleziona cartella della lingua](assets/select-language-folder.png)
1. Tocca o fai clic su **Gestisci pubblicazione**.
1. Nella finestra **Gestisci pubblicazione** , accertati che **Pubblica** sia selezionato automaticamente in **Azione** e che **Ora** sia selezionato in **Pianificazione**. Tocca o fai clic su **Avanti**.
   ![Gestione delle opzioni di pubblicazione](assets/manage-publication-options.png)
1. Nella finestra successiva **Gestisci pubblicazione**, verifica che sia selezionato il percorso o i percorsi corretti. Tocca o fai clic su **Pubblica**.
   ![Gestisci ambito pubblicazione](assets/manage-publication-scope.png)
1. AEM conferma l’azione di pubblicazione con un messaggio a comparsa nella parte inferiore dello schermo.
   ![Banner risorse pubblicate](assets/resources-published-message.png)

Il tuo contenuto localizzato headless è ora pubblicato! È ora possibile accedervi e utilizzarli dai servizi headless.

>[!TIP]
>
>Per pubblicare più localizzazioni alla volta, è possibile selezionare più elementi (ad esempio cartelle multilingue) durante la pubblicazione.

Sono disponibili opzioni aggiuntive per la pubblicazione dei contenuti, ad esempio per la pianificazione di un orario di pubblicazione che va oltre l’ambito di questo percorso. Per ulteriori informazioni, consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine del documento.

## Aggiornamento del contenuto tradotto {#updating-translations}

La localizzazione e la traduzione raramente sono un esercizio una tantum. In genere, al termine della localizzazione iniziale, gli autori dei contenuti continuano ad aggiungere e modificare il contenuto nella directory principale lingua. Questo significa che dovrai anche aggiornare il contenuto tradotto.

Requisiti di progetto specifici definiranno la frequenza con cui sarà necessario aggiornare le traduzioni e il processo decisionale da seguire prima di eseguire un aggiornamento. Una volta che hai deciso di aggiornare le tue traduzioni, il processo in AEM è molto semplice. Poiché la traduzione iniziale era basata su un progetto di traduzione, lo sono anche gli aggiornamenti.

1. Passa a **Navigazione** -> **Risorse** -> **File**. Il contenuto headless in AEM viene memorizzato come risorse note come Frammenti di contenuto.
1. Seleziona la directory principale della lingua del progetto. In questo caso abbiamo selezionato `/content/dam/wknd/en`.
1. Tocca o fai clic sul selettore della barra e mostra il pannello **Riferimenti** .
1. Tocca o fai clic su **Copie per lingua**.
1. Seleziona la casella di controllo **Copie per lingua** .
1. Espandi la sezione **Aggiorna copie per lingua** nella parte inferiore del pannello Riferimenti.
1. Nel menu a discesa **Progetto**, seleziona **Aggiungi a un progetto di traduzione esistente**.
1. Nel menu a discesa **Progetto di traduzione esistente** , seleziona il progetto creato per la traduzione iniziale.
1. Tocca o fai clic su **Avvia**.

![Aggiungi elementi al progetto di traduzione esistente](assets/add-to-existing-project.png)

Il contenuto viene aggiunto al progetto di traduzione esistente. Per visualizzare il progetto di traduzione:

1. Passa a **Navigazione** -&amp; **Progetti**.
1. Tocca o fai clic sul progetto appena aggiornato.
1. Tocca o fai clic sulla lingua o su una delle lingue aggiornate.

Al progetto è stata aggiunta una nuova carta di lavoro. In questo esempio è stata aggiunta un’altra traduzione spagnola.

![Processo di traduzione aggiuntivo aggiunto](assets/additional-translation-job.png)

Noterai che le statistiche elencate nella nuova scheda (numero di risorse e frammenti di contenuto) sono diverse. Questo perché AEM riconosce ciò che è cambiato dopo l’ultima traduzione e include solo nuovi contenuti che devono essere tradotti (sia i contenuti aggiornati tradotti nuovamente che la prima traduzione di nuovi contenuti).

Da questo punto [inizia e gestisci il lavoro di traduzione esattamente come hai fatto con l&#39;originale.](translate-content.md#using-translation-project)

## Fine del Percorso? {#end-of-journey}

Congratulazioni! Hai completato il percorso di localizzazione headless! Ora dovresti:

* Panoramica della distribuzione headless dei contenuti.
* Avere una comprensione di base AEM funzionalità headless.
* Comprendere AEM funzioni di localizzazione e come si relazionano al contenuto headless.
* Possibilità di iniziare a localizzare il proprio contenuto headless.

Ora puoi localizzare il tuo contenuto headless in AEM. Tuttavia AEM è uno strumento potente e ci sono molte opzioni aggiuntive disponibili. Consulta alcune delle risorse aggiuntive disponibili nella sezione successiva per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Gestione dei progetti di traduzione](/help/sites-cloud/administering/translation/managing-projects.md) : scopri i dettagli dei progetti di traduzione e le funzioni aggiuntive, come i flussi di lavoro di traduzione umana e i progetti multilingue.
* [Concetti di authoring](/help/sites-cloud/authoring/getting-started/concepts.md)  - Scopri il modello di authoring e pubblicazione di AEM più dettagliatamente. Questo documento si concentra sull’authoring delle pagine anziché sui frammenti di contenuto, ma la teoria è ancora valida.
* [Pubblicazione di pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)  - Scopri le funzioni aggiuntive disponibili per la pubblicazione dei contenuti. Questo documento si concentra sull’authoring delle pagine anziché sui frammenti di contenuto, ma la teoria è ancora valida.
