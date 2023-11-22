---
title: Utilizzo degli archivi GitHub personali in Cloud Manager
description: Scopri come configurare Cloud Manager per l’utilizzo degli archivi GitHub personali.
feature: Release Information
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: 237b4a8e01af74dbaac0ba1715b5fa95c931be7c
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 70%

---

# Utilizzo degli archivi GitHub personali in Cloud Manager {#byo-github}

Con la configurazione di Cloud Manager per l’utilizzo con gli archivi GitHub personali, puoi convalidare il codice direttamente all’interno dell’archivio GitHub tramite Cloud Manager, eliminando la necessità di sincronizzare in modo coerente il codice con l’archivio di Adobe.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma di adozione anticipata.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Configurazione {#configuration}

La configurazione consiste di due passaggi principali:

1. [Aggiungi archivio](#add-repo)
1. [Convalida della proprietà dell’archivio privato](#validate-ownership)

### Aggiungi archivio {#add-repo}

1. In Cloud Manager, dalla sezione **Panoramica del programma** , seleziona la **Archivi** per passare alla scheda **Archivi** pagina e fai clic su **Aggiungi archivio**.

1. Nella finestra di dialogo **Aggiungi archivio**, seleziona **Archivio privato** come tipo di archivio.

1. Specifica i dettagli dell’archivio

   * **Nome archivio**: un nome espressivo
   * **URL archivio**: l’URL dell’archivio, che deve terminare con `.git`
   * **Descrizione** (facoltativa): una descrizione più lunga dell’archivio in base alle esigenze

   ![Aggiungi un archivio personale](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Seleziona **Salva**.

>[!TIP]
>
>Per informazioni dettagliate sulla gestione degli archivi in Cloud Manager, consulta [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

### Convalida della proprietà dell’archivio privato {#validate-ownership}

Cloud Manager ora è a conoscenza del tuo archivio GitHub, ma deve ancora accedervi. Per concedere l’accesso, devi installare l’app Adobe GitHub e verificare di essere il proprietario dell’archivio specificato.

1. Dopo l’aggiunta del tuo archivio, il **Convalida proprietà archivio privato** viene visualizzata una finestra di dialogo.

   ![Convalida delle proprietà dell’archivio privato](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager utilizza un’app GitHub per interagire in modo sicuro con l’archivio.
   * Un proprietario dell’organizzazione GitHub deve installare l’app che si trova in `https://github.com/apps/cloud-manager-for-aem-stage` e concedere l’accesso all’archivio.
   * Consulta la documentazione di GitHub per informazioni dettagliate su come eseguire questa operazione.

1. Per una maggiore sicurezza, è necessario creare un file segreto nel ramo predefinito dell’archivio. Seleziona **Genera**.

1. Conferma la generazione del file segreto toccando o facendo clic su **Conferma**.

   ![Conferma la generazione del segreto](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. Nella finestra **Convalida delle proprietà dell’archivio privato**, Cloud Manager ha generato il contenuto del file privato nel campo **Contenuto file segreto**. Copia il contenuto da quel campo.

   * Il contenuto del file segreto verrà visualizzato una sola volta. Se non si copia il contenuto prima di chiudere la finestra, rigenerare il segreto.

   ![Copia il contenuto del file segreto](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. Crea un nuovo file nel ramo predefinito dell’archivio GitHub denominato `.well-known/adobe/cloud-manager-challenge` e incolla il contenuto del file segreto in tale file e salvalo.

1. Una volta installata l’app e inserito il file segreto nell’archivio, puoi selezionare **Convalida** nel **Convalida proprietà archivio privato** .

L’app può essere installata e il file segreto può essere creato in qualsiasi ordine. Tuttavia, entrambi i passaggi devono essere completati prima di poter eseguire la convalida.

Fino alla convalida, l’archivio viene elencato con un’icona rossa, a indicare che non è ancora stato convalidato e non può ancora essere utilizzato.

![Archivio non convalidato](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

Il **Tipo** questa colonna identifica facilmente gli archivi forniti dall’Adobe (**Adobe**) e i tuoi archivi GitHub (**GitHub**).

Se per completare la convalida dovrai tornare all’archivio in una data successiva, il **Archivi** , seleziona il pulsante con i puntini di sospensione nella riga che rappresenta l’archivio GitHub appena aggiunto e fai clic su **Convalida proprietà** dal menu a discesa.

## Utilizzo di archivi GitHub personali con Cloud Manager {#using}

Dopo la convalida dell’archivio GitHub in Cloud Manager, l’integrazione è completata e puoi utilizzare l’archivio con Cloud Manager.

1. Quando crei una richiesta pull, viene avviata automaticamente una verifica GitHub.

   ![Verifiche GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Per ogni richiesta pull, verrà creata automaticamente una [pipeline di qualità del codice full stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Tale pipeline viene avviata ogni volta che la richiesta pull viene aggiornata.

1. La verifica GitHub rimane in esecuzione fino al completamento dei controlli di qualità del codice. I risultati di qualità del codice verranno propagati quindi alla verifica GitHub.

   ![Controlli di qualità del codice GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Quando la richiesta pull viene chiusa o unita, la pipeline di qualità del codice full-stack creata viene eliminata automaticamente.

## Limitazioni {#limitations}

Limitazioni quando si utilizzano archivi GitHub personalizzati con Cloud Manager.

* Non è possibile utilizzare gli archivi GitHub come origine diretta dell’archivio per le pipeline gestite.
   * Questa funzionalità è pianificata.
* Non è possibile sospendere la convalida della richiesta di pull utilizzando il controllo GitHub da Cloud Manager.
   * Se l’archivio GitHub viene convalidato in Cloud Manager, Cloud Manager tenterà sempre di convalidare le richieste pull create per quell’archivio.
Se l’app GitHub di Adobe viene rimossa dall’organizzazione GitHub, la funzione di convalida delle richieste pull verrà rimossa per tutti gli archivi.
