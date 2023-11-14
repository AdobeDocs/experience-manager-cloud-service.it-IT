---
title: Utilizzo degli archivi GitHub in Cloud Manager
description: Scopri come configurare Cloud Manager per l’utilizzo degli archivi GitHub.
feature: Release Information
source-git-commit: 8d689ea08ab7caf9cb0fa84df23d7e0fd906f379
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---


# Utilizzo degli archivi GitHub in Cloud Manager {#byo-github}

Configurando Cloud Manager per l’utilizzo degli archivi GitHub, puoi convalidare il codice direttamente all’interno dell’archivio GitHub tramite Cloud Manager, eliminando la necessità di sincronizzare in modo coerente il codice con l’archivio di Adobe.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma early adopter.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Configurazione {#configuration}

La configurazione consiste di due passaggi principali:

1. [Aggiungi archivio](#add-repo)
1. [Convalida della proprietà dell’archivio privato](#validate-ownership)

### Aggiungi archivio {#add-repo}

1. In Cloud Manager, dalla sezione **Panoramica del programma** pagina, tocca o fai clic su **Archivi** per passare alla scheda **Archivi** pagina e fai clic su **Aggiungi archivio**.

1. In **Aggiungi archivio** finestra di dialogo, seleziona **Archivio privato** come tipo di archivio.

1. Fornisci i dettagli dell’archivio

   * **Nome archivio** - Un nome espressivo
   * **URL archivio** : l’URL dell’archivio, che deve terminare con `.git`
   * **Descrizione** (facoltativo): descrizione più lunga dell’archivio in base alle esigenze

   ![Aggiungi un proprio archivio](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Tocca o fai clic su **Salva**.

>[!TIP]
>
>Per informazioni dettagliate sulla gestione degli archivi in Cloud Manager, consulta il documento [Archivi di Cloud Manager.](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)

### Convalida proprietà archivio privato {#validate-ownership}

Cloud Manager ora è a conoscenza dell’archivio GitHub, ma deve ancora accedervi. Per concedere l’accesso, devi installare l’app GitHub Adobe e verificare di essere il proprietario dell’archivio specificato.

1. Dopo l’aggiunta del tuo archivio, il **Convalida proprietà archivio privato** viene aperta una finestra di dialogo.

   ![Convalida proprietà archivio privato](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager utilizza un’app GitHub per interagire in modo sicuro con l’archivio.
   * Un proprietario dell’organizzazione GitHub deve installare l’app che si trova in `https://github.com/apps/cloud-manager-for-aem-stage` e concedono l’accesso all’archivio.
   * Fai riferimento alla documentazione di GitHub per informazioni dettagliate su come eseguire questa operazione.

1. Per migliorare la protezione, è necessario creare un file segreto nel ramo predefinito dell’archivio. Tocca o fai clic su **Genera**.

1. Conferma la generazione del file segreto toccando o facendo clic su **Conferma**.

   ![Conferma generazione segreto](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. Torna in **Convalida proprietà archivio privato** Cloud Manager ha generato il contenuto del file privato nella finestra **Contenuto del file segreto** campo. Copia il contenuto da quel campo.

   * Il contenuto del file segreto verrà visualizzato una sola volta. Se non copi il contenuto prima di chiudere questa finestra, dovrai rigenerare il segreto.

   ![Copia contenuto file segreto](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. Crea un nuovo file nel ramo predefinito dell’archivio GitHub denominato `.well-known/adobe/cloud-manager-challenge` e incollare il contenuto del file segreto in tale file e salvarlo.

1. Una volta che l’app è installata e il file segreto esiste nell’archivio, puoi toccare o fare clic su **Convalida** nel **Convalida proprietà archivio privato** .

L’app può essere installata e il file segreto può essere creato in qualsiasi ordine. Tuttavia, entrambi i passaggi devono essere completati prima di poter eseguire la convalida.

Fino alla convalida, l’archivio viene elencato con un’icona rossa, a indicare che non è ancora stato convalidato e non può ancora essere utilizzato.

![Archivio non convalidato](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

Tieni presente che **Tipo** questa colonna identifica facilmente gli archivi forniti dall’Adobe (**Adobe**) e i tuoi archivi GitHub (**GitHub**).

Se per completare la convalida dovessi tornare all’archivio in una data successiva, il **Archivi** tocca o fai clic sul pulsante con i puntini di sospensione nella riga che rappresenta l’archivio GitHub appena aggiunto e seleziona **Convalida proprietà** dal menu a discesa.

## Utilizzo di archivi GitHub personalizzati con Cloud Manager {#using}

Dopo la convalida dell’archivio GitHub in Cloud Manager, l’integrazione è completata e puoi utilizzare l’archivio con Cloud Manager.

1. Quando crei una richiesta di pull, viene avviato automaticamente un controllo GitHub.

   ![Controlli GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Per ogni richiesta di pull, [pipeline di qualità del codice full stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) verrà creato automaticamente. Questa pipeline viene avviata a ogni aggiornamento della richiesta di pull.

1. Il controllo GitHub rimane in esecuzione fino al completamento dei controlli di qualità del codice. I risultati della qualità del codice verranno quindi propagati al controllo GitHub.

   ![Controlli di qualità del codice GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Quando la richiesta di pull viene chiusa o unita, la pipeline di qualità del codice full stack creata viene eliminata automaticamente.

## Limitazioni {#limitations}

Tieni presenti le seguenti limitazioni quando utilizzi archivi GitHub personalizzati con Cloud Manager.

* Non puoi utilizzare gli archivi GitHub come origine diretta dell’archivio per le pipeline gestite.
   * Questa funzionalità è pianificata.
* Non puoi mettere in pausa la convalida della richiesta di pull utilizzando il controllo GitHub di Cloud Manager.
   * Se l’archivio GitHub viene convalidato in Cloud Manager, Cloud Manager tenterà sempre di convalidare le richieste pull create per tale archivio.
Se l’app GitHub di Adobe viene rimossa dall’organizzazione GitHub, la funzione di convalida delle richieste pull verrà rimossa per tutti gli archivi.
