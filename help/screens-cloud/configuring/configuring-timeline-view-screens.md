---
title: Configurazione della vista Timeline per AEM Screens
description: Questa pagina descrive come configurare una vista timeline in Screens as a Cloud Service.
exl-id: 53afe1f5-8f0b-4cca-a819-d3e9375cbe37
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 12%

---

# Configurazione della vista Timeline per AEM Screens {#configuring-timelineview-screens}

## Introduzione {#introduction}

Questa sezione descrive come creare una vista Timeline per AEM Screens.

AEM fornisce una suite di funzioni che consente a più persone appartenenti a gruppi all’interno di un’organizzazione di collaborare alla creazione, alla gestione e all’utilizzo dei canali.
La timeline, che si trova nella barra a sinistra, descrive i canali, la posizione o il ciclo di vita di una cartella di schermate in ordine temporale per trasmettere ciò che è successo a essa nel corso della sua vita. Questo può essere filtrato verso il basso per tipo.
Oltre ai registri del ciclo di vita, la barra Timeline fornisce le seguenti funzioni.

![Applica profilo alla cartella](/help/screens-cloud/assets/configure/Screens-timeline1.jpg)

![Applica profilo alla cartella](/help/screens-cloud/assets/configure/screens-timeline2.jpg)

La procedura seguente illustra come creare una vista Timeline per AEM Screens:

1. Aggiungi un commento
1. Salvare una versione
1. Avviare un flusso di lavoro

Le sezioni seguenti descrivono in dettaglio questi passaggi.

### Aggiungi un commento {#addcomment}

I commenti disponibili tramite la timeline consentono agli utenti di creare una registrazione centralizzata e cronologica per le discussioni che si svolgono sul canale, sulla posizione o su qualsiasi cartella nello schermo.
I commenti forniscono un modo consolidato per consentire agli utenti di AEM di discutere di un modo che può essere mantenuto, consentendo ad altri di comprendere le decisioni chiave.

1. Passare al canale per il quale si desidera aggiungere un commento.
1. Seleziona il canale.
1. Apri la colonna **Timeline**.
1. Aggiungi il tuo commento e premi **Invio**.

![Aggiungi un commento](/help/screens-cloud/assets/configure/screen-timeline3.jpg)

Le informazioni nella timeline vengono aggiornate per indicare che il commento è stato aggiunto.

![Aggiungi un commento](/help/screens-cloud/assets/configure/screens-timeline4.jpg)

### Salva una versione {#saveversion}

Il controllo delle versioni crea un&#39;istantanea di un canale in un determinato momento. Con il controllo delle versioni è possibile eseguire le azioni seguenti:

* Crea una versione di un canale.
* Ripristina un canale a una versione precedente; ad esempio:
   * per annullare una modifica apportata alla pagina.
* Confronta la versione corrente di un canale con una versione precedente:
   * per evidenziare le differenze nel contenuto del canale.


#### Crea una nuova versione {#createnewversion}

1. Passare al canale per il quale si desidera aggiungere un commento.
1. Seleziona il canale.
1. Apri la colonna **Timeline**.
1. Fai clic sul pulsante (tre punti) accanto al campo commento nella parte inferiore della pagina.

   ![Aggiungi un commento](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. Seleziona **Salva come versione**.
1. Immettere un **etichetta** e un **commento** per la versione.

   ![Aggiungi un commento](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. Confermare la nuova versione selezionando **Crea**. Le informazioni nella sequenza temporale vengono aggiornate per indicare che si tratta di una nuova versione.

#### Ripristina una versione {#revertversion}

Per ripristinare la pagina selezionata in una versione precedente:

1. Passa al canale per aggiungere un commento.
1. Seleziona il canale.
1. Apri la colonna **Timeline**.
1. Seleziona **Mostra tutti** o **Versioni** dal menu a discesa dei filtri. Vengono elencate le versioni del canale selezionato.
1. Seleziona la versione da ripristinare. Vengono visualizzate le opzioni disponibili:

   ![Aggiungi un commento](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. Seleziona **Ripristina questa versione**. La versione selezionata viene ripristinata e le informazioni nella timeline aggiornate.

#### Anteprima di una versione {#previewversion}

Puoi visualizzare l’anteprima di una versione specifica:

1. Passa al canale per aggiungere un commento.
1. Seleziona il canale.
1. Apri la colonna **Timeline**.
1. Seleziona **Mostra tutti** o **Versioni** dal menu a discesa dei filtri. Vengono elencate le versioni del canale selezionato.
1. Seleziona la versione da visualizzare in anteprima. Vengono visualizzate le opzioni disponibili:

   ![Anteprima versione](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. Seleziona **Anteprima**. Il canale viene visualizzato in una nuova scheda.

#### Confrontare una versione con la versione corrente {#compareversion}

Puoi confrontare una versione specifica con la versione corrente:

1. Passare al canale per il quale si desidera aggiungere un commento.
1. Seleziona il canale.
1. Apri la colonna **Timeline**
1. Seleziona **Mostra tutti** o **Versioni** dal menu a discesa dei filtri. Vengono elencate le versioni del canale selezionato.
1. Seleziona la versione da confrontare. Vengono visualizzate le opzioni disponibili:

   ![Confronta versione](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. Seleziona **Confronta con corrente**. Viene visualizzata la finestra a comparsa per visualizzare le differenze.

### Avvia un flusso di lavoro {#workflowstart}

Durante l’authoring, è possibile richiamare i flussi di lavoro per intraprendere azioni sui canali; è inoltre possibile applicare più di un flusso di lavoro.
Quando applichi il flusso di lavoro, specifichi le informazioni seguenti:

* Flusso di lavoro da applicare.
* Facoltativamente, un titolo che consente di identificare l’istanza del flusso di lavoro nella casella in entrata di un utente.
* Il payload del flusso di lavoro.

#### Avvio del flusso di lavoro

1. Passare al canale per il quale si desidera aggiungere un commento.
1. Seleziona il canale.
1. Apri la colonna **Timeline**.
1. Fai clic sul pulsante (tre punti) accanto al campo commento nella parte inferiore.

   ![Avvia flusso di lavoro](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. Seleziona **Avvia flusso di lavoro**.
1. Viene visualizzata la procedura guidata Crea flusso di lavoro che consente di specificare i dettagli del flusso di lavoro.
1. Selezionare **Modello flusso di lavoro** dall&#39;elenco a discesa e immettere il titolo del flusso di lavoro.

   ![Avvia flusso di lavoro](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. Continua facendo clic su **Avanti**.
1. Nel passaggio ambito puoi effettuare le seguenti operazioni:
   * **Aggiungi contenuto** per aggiungere ulteriori risorse al flusso di lavoro.
   * **Includi elementi figlio** per specificare gli elementi figlio di tale risorsa che verranno inclusi nel flusso di lavoro.
   * **Rimuovi selezione** per rimuovere tale risorsa dal flusso di lavoro.

   ![Avvia flusso di lavoro](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. Seleziona **Crea** per chiudere la procedura guidata e creare l&#39;istanza del flusso di lavoro.
1. A seconda del modello di flusso di lavoro selezionato, potrebbe essere necessario eseguire alcune azioni aggiuntive per completare il flusso di lavoro.

   ![Avvia flusso di lavoro](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
