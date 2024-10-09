---
title: Creazione dei lanci
description: Puoi creare un lancio per abilitare l’aggiornamento di una nuova versione delle pagine web esistenti per l’attivazione futura.
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: b5ded40d1cb8b8fab28583467b68c4586eecf1a0
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 96%

---

# Creazione dei lanci {#creating-launches}

Crea un lancio per abilitare l’aggiornamento di una nuova versione delle pagine web esistenti per l’attivazione futura. Per creare un lancio, è necessario specificare un titolo e la pagina di origine:

* Il titolo viene visualizzato nella barra [Riferimenti](/help/sites-cloud/authoring/sites-console/console-side-panel.md#references), dalla quale gli autori potranno accedere per lavorarci.
* Per impostazione predefinita, le pagine secondarie della pagina sorgente sono incluse nel lancio. Se necessario, puoi utilizzare solo la pagina sorgente.
* Per impostazione predefinita, [Live Copy](/help/sites-cloud/administering/msm/overview.md) aggiorna automaticamente le pagine del lancio durante il cambio delle pagine sorgente. È possibile specificare di creare una copia statica per impedire modifiche automatiche.

Facoltativamente, puoi specificare la **Data lancio** (e l’ora) per definire quando promuovere e attivare le pagine del lancio. Tuttavia, la **Data lancio** funziona solo in combinazione con il flag **Production Ready** (vedi la sezione [Modifica di una configurazione di lancio](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)). Affinché le azioni vengano effettivamente eseguite in automatico, è necessario impostare entrambe.

>[!NOTE]
>
>Quando crei un lancio, le pagine più in alto nella gerarchia non sono copie delle pagine sorgente. Sono segnaposto, creati con il modello:
>
>* `/libs/launches/templates/outofscope`
>
>Non è possibile modificare queste pagine. Viene visualizzato il messaggio:
>
>* **Questa pagina non fa parte del lancio. Vai alla pagina produzione**

## Creazione di un lancio {#creating-a-launch}

Puoi creare un lancio dalla console Sites o Lanci:

1. Apri la console **Sites** o **Lanci**.

   >[!NOTE]
   >
   >Quando si utilizza la console **Sites** solitamente si passa alla posizione della pagina sorgente, ma questo non è obbligatorio dato che puoi navigare quando selezioni la **Sorgente del lancio** nella procedura guidata.

1. A seconda della console in uso:
   * **Lanci**:
      1. Seleziona **Crea lancio** dalla barra degli strumenti per aprire la procedura guidata.
   * **Sites**:
      1. Seleziona **Crea** nella barra degli strumenti per aprire la casella di selezione.
      1. Da questa seleziona **Crea lancio** per aprire la procedura guidata.

   >[!NOTE]
   >
   >Nella console **Sites** è inoltre possibile utilizzare la [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) per scegliere una pagina prima di fare clic su **Crea**.
   >
   >La pagina selezionata verrà così utilizzata come pagina sorgente iniziale.

1. Nel passaggio **Seleziona origine** è necessario usare la funzione **Aggiungi pagine**. Puoi selezionare più pagine, specificando il percorso per ciascuna:
   * Passa alla posizione desiderata.
   * Seleziona le pagine sorgente e conferma (segno di spunta).

   Ripeti in base alle esigenze.  

   ![Seleziona origine lancio](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Per aggiungere pagine e/o rami a un lancio, questi devono essere all’interno di un sito; ovvero, in una directory comune di primo livello.
   >
   >Se un sito contiene directory principali per lingue inferiori al primo livello, le pagine e i rami di un lancio devono essere in una directory principale per lingua comune.

1. Per ogni voce è possibile specificare se:

   * **Includere le pagine secondarie**:

      * Specifica se creare il lancio con o senza pagine figlie.  Per impostazione predefinita, le pagine secondarie sono incluse.

   Procedi con **Successivo**.

   ![Seleziona origine lancio](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. Nel passaggio **Proprietà** della procedura guidata puoi specificare:

   * **Titolo lancio**: il nome del lancio. Il nome deve essere significativo per gli autori.
   * **con contenuto esistente**: il contenuto originale viene utilizzato per creare il lancio.
   * **con un nuovo modello per sostituire la pagina**: per ulteriori dettagli, vedi [Creare un lancio con un nuovo modello](#create-launch-with-new-template).
   * **Eredita i dati live della pagina di origine**: seleziona questa opzione per aggiornare automaticamente il contenuto delle pagine di lancio quando cambiano le pagine di origine. Con questa opzione il lancio diventa una [Live Copy](/help/sites-cloud/administering/msm/overview.md). Per impostazione predefinita, questa opzione è selezionata.-->
   * **Data lancio**: la data e l&#39;ora in cui la copia del lancio deve essere attivata (in base alla segnalazione **Produzione pronta**; consulta [Lanci: l&#39;ordine degli eventi](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)).

   ![Proprietà lancio](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Utilizza **Crea** per completare il processo e creare il nuovo lancio. La finestra di dialogo di conferma chiederà se desideri aprire immediatamente il lancio.

   Se torni alla console (con **Fine**) puoi visualizzare (e accedere) al lancio da:

   * Console [**Lanci**](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * [**Riferimenti** nella console **Sites**](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Creare un lancio con un nuovo modello {#create-launch-with-new-template}

Quando creai un lancio puoi utilizzare un nuovo modello scegliendo la seguente opzione:

>[!NOTE]
>
>Questa opzione è disponibile solo quando crei un lancio dalla console **Sites**. Non è disponibile quando crei un lancio dalla console **Lanci**.

La ![creazione di un lancio con un nuovo modello](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Quando selezioni questa opzione:

* aggiorna le altre opzioni disponibili,
* aggiunge un nuovo passaggio che permette di selezionare il modello desiderato.

![Selezione di un nuovo modello](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>Quando utilizzi un modello diverso, la nuova pagina è vuota. A causa della diversa struttura della pagina, non viene copiato alcun contenuto.
>
>Questo meccanismo può essere utilizzato per modificare il modello di una [pagina esistente](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page), anche se va considerata la perdita di contenuto.

### Creazione di un lancio nidificato {#creating-a-nested-launch}

La creazione di un lancio nidificato (un lancio all’interno di un lancio) ti consente di creare un lancio da un lancio esistente in modo che gli autori possano sfruttare le modifiche già apportate, anziché dover apportare le stesse modifiche più volte per ogni lancio.

>[!NOTE]
>
>Vedi anche [Promozione di un lancio nidificato](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Creazione di un lancio nidificato: console Lanci {#creating-a-nested-launch-launches-console}

La creazione di un lancio nidificato dalla console **Lanci** è molto simile alla creazione di qualsiasi altra forma di lancio, con l’eccezione che è necessario passare al ramo dei lanci `/content/launches`:

1. Nella console **Lanci** seleziona **Crea**.
1. Fai clic su **Aggiungi pagine**, quindi vai al ramo lanci specificando `/content/launches` in **Filtri**. Scegli il lancio necessario e conferma con **Seleziona**:

   ![Creazione di un lancio nidificato](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Procedi con **Successivo**.

1. Completa le **Proprietà** come con qualsiasi altro lancio.

1. Completa con **Crea**.

#### Creazione di un lancio nidificato: console Sites {#creating-a-nested-launch-sites-console}

Per creare un lancio nidificato dalla console **Sites**, basato su un lancio esistente:

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Crea lancio** per aprire la procedura guidata (poiché l’origine è già stata selezionata, ignorerà il passaggio **Seleziona origine**).
1. Immetti il **Titolo lancio** e tutti gli altri dettagli richiesti (come con un normale lancio).
1. Utilizza **Crea** per completare il processo e creare il nuovo lancio. La finestra di dialogo di conferma chiederà se desideri aprire immediatamente il lancio.

Se fai clic su **Fine**, vieni riportato alla barra **Riferimenti** della console **Sites**, se selezioni la pagina appropriata viene visualizzato il tuo nuovo lancio.

### Clonazione di un lancio {#cloning-a-launch}

È possibile clonare un lancio dalla console [Launches](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Seleziona il lancio toccando o facendo clic sulla miniatura.
* Viene visualizzata la barra degli strumenti. Seleziona Clona.
   * Il clone verrà visualizzato nella console.

## Eliminazione di un lancio {#deleting-a-launch}

Puoi eliminare un lancio dalla [console lanci](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Seleziona il lancio toccando o facendo clic sulla miniatura.
* Viene visualizzata la barra degli strumenti: seleziona Elimina.
* Conferma l’azione.

>[!CAUTION]
>
>L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.
