---
title: Creazione e gestione dei canali in Screens as a Cloud Service
description: Questa pagina descrive come creare e gestire i canali in Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 9db22dca0fd6debaff0d93e1958e59536efabad8
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 4%

---

# Creazione e gestione di un canale in Screens as a Cloud Service {#creating-channels-screens-cloud}

Dopo aver creato un progetto AEM Screens, devi creare i canali.
***Canali***, visualizza una sequenza di contenuti (immagini e video), un sito web o un’applicazione a pagina singola.

## Obiettivo {#objective}

Questo documento è utile per comprendere come creare e gestire i canali per il progetto AEM Screens in Screens Content Provider. Dopo la lettura dovresti essere a:

* informazioni su come creare canali per Screens Content Provider
* gestire e modificare i contenuti nei canali
* pianificazione di attivazione per i canali

## Passaggi per creare un nuovo canale per sequenza in Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Prerequisiti**
>Prima di iniziare questa sezione della Guida, consulta [Creazione e gestione di progetti in Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Segui i passaggi seguenti per creare un nuovo canale per sequenza in Screens as a Cloud Service:

1. Passa a Provider di contenuti Screens.

1. Passa al progetto AEM Screens, ad esempio *FirstDigitalExperience*.

1. Seleziona la **Canali** cartella del progetto, ad esempio **FirstDigitalExperience** —> **Canali** e fai clic su **Crea** dalla barra delle azioni.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Seleziona il modello, ad esempio: **Canale per sequenza** dal **Crea** procedura guidata e fai clic su **Successivo**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > La **Crea** La procedura guidata fornisce diversi tipi di modelli durante la creazione di un canale. Consulta la sezione . [Modelli disponibili](#available-templates) in Creazione guidata per ulteriori dettagli.

1. Inserisci il nome del canale della sequenza, ad esempio, **LoopingChannelOne** e fai clic su **Crea**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Verrà ora visualizzata una **LoopingChannelOne** nella cartella Canali del progetto AEM Screens.

   Dopo aver creato il canale, ora puoi aggiungere contenuto al canale. Fai riferimento a [Aggiunta di contenuto a un canale](#add-content) per scoprire come aggiungere risorse (immagini/video) al tuo canale.

## Gestione di un canale {#managing-channels}

Puoi modificare, visualizzare le proprietà e il dashboard, copiare, visualizzare in anteprima e eliminare un canale.

Accedi al canale dal progetto e seleziona il canale, come illustrato nella figura seguente. Ora puoi selezionare le opzioni quali la modifica del canale, la visualizzazione delle proprietà, l’anteprima del contenuto, la gestione della pubblicazione o l’eliminazione del canale dalla barra delle azioni.

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### Aggiunta di contenuto a un canale {#add-content}

Per aggiungere o modificare il contenuto di un canale, segui i passaggi riportati di seguito:

1. Seleziona il canale da modificare, come illustrato nella figura riportata di seguito. Fai clic su **Modifica** dall’angolo in alto a sinistra della barra delle azioni per aprire l’editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. L’editor ti consente di aggiungere al canale risorse/componenti che desideri pubblicare.

1. Trascina e rilascia le risorse dal riquadro a sinistra e aggiungilo all’editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Fai clic su **Anteprima** per visualizzare in anteprima i contenuti del canale.
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Modelli disponibili in Creazione guidata {#available-templates}

I seguenti modelli sono disponibili durante l’utilizzo dei **Crea** procedura guidata canale:

| Modelli disponibili | Descrizione |
|--- |--- |
| Cartella canali | Consente di creare una cartella per memorizzare la raccolta dei canali. |
| Canale per sequenza | Consente di creare un canale che riproduce i componenti in sequenza (uno per uno in una presentazione). |
| Canale schermo diviso a barre L a sinistra o a destra | Consente agli autori di contenuti di visualizzare diversi tipi di risorse in aree di dimensioni appropriate. |

## Usa dettagli assegnazione predefiniti per i canali {#default-channels}

Questa funzionalità consente di definire una pianificazione di attivazione predefinita per un canale e di utilizzarla per impostazione predefinita per ogni assegnazione per una visualizzazione. Questo fornisce un metodo in modo che non sia necessario ripetere la definizione complessa della pianificazione.

### Creare i dettagli di assegnazione predefiniti per un canale {#create-default}

1. Passa alla pagina dei dettagli del canale da configurare.
1. Individua il **Dettagli assegnazione predefiniti** nella pagina.

   ![immagine](/help/screens-cloud/assets/display/Assignment1.png)

1. Fai clic su **Imposta dettagli predefiniti**.
1. Configura i dettagli di assegnazione predefiniti, tra cui priorità, date di inizio e fine, nonché i pattern di ricorrenza per il canale, e fai clic su **Assegna**.

   ![immagine](/help/screens-cloud/assets/display/Assignments2.png)

1. I dettagli dell&#39;assegnazione sono visualizzati nella sezione **Dettagli assegnazione predefiniti** riquadro:

   ![immagine](/help/screens-cloud/assets/display/Assignments3.png)

In questa sezione vengono visualizzate le seguenti informazioni:
* Priorità predefinita del canale nel display.
* Date di inizio e fine dell&#39;attivazione quando è programmata la riproduzione del canale.
* Vista sintetica della ricorrenza (Orario/Giorno/Settimanale/Mensile/Annuale e nome assegnato a tale ricorrenza).

### Utilizzare i dettagli di assegnazione predefiniti durante l&#39;assegnazione a una visualizzazione {#default-display}

I canali con dettagli di assegnazione predefiniti possono essere assegnati a visualizzazioni come i canali regolari, con l&#39;opzione aggiunta per sfruttare i dettagli di assegnazione predefiniti invece di definirli manualmente ogni volta.

1. Passa alla pagina dei dettagli di visualizzazione a cui desideri assegnare il canale e fai clic sul pulsante **Assegna canale**.
in alternativa, seleziona la visualizzazione desiderata nella vista Inventario e fai clic sul pulsante **Assegna canale**.
1. Viene visualizzata la finestra di dialogo di assegnazione del canale.

   ![immagine](/help/screens-cloud/assets/display/Assignments4.png)

1. Seleziona dal selettore canali il canale desiderato con i dettagli di assegnazione predefiniti.
1. Osserva le modifiche apportate alla finestra di dialogo di assegnazione del canale per consentire di scegliere i dettagli di assegnazione predefiniti o selezionarne di personalizzati:

   ![immagine](/help/screens-cloud/assets/display/Assignments5.png)

1. Fai clic su **Assegna** per completare l&#39;assegnazione, oppure fare clic su **Impostazione dei dettagli di assegnazione personalizzati** se preferisci ignorare i valori predefiniti con altri valori nel contesto di tale visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/Assignments6.png)

1. Osserva che **Canali assegnati** il riquadro viene aggiornato con la nuova assegnazione:

   ![immagine](/help/screens-cloud/assets/display/Assignments7.png)

1. Nota che i canali avranno un’icona diversa a seconda che utilizzino pianificazioni personalizzate (icona Orologio) o ereditino i dettagli predefiniti (icona Orologio mondiale), e facendo clic su di essi verranno visualizzati i dettagli della pianificazione.
1. Noterai inoltre che le azioni disponibili per ciascun tipo variano.

   ![immagine](/help/screens-cloud/assets/display/Assignments8.png)

**Nota:** Un&#39;assegnazione di canale che sfrutta i dettagli di assegnazione predefiniti non sarà modificabile nel contesto della visualizzazione.

* Se è necessario modificarlo in un&#39;assegnazione personalizzata, è necessario prima rimuoverlo e poi aggiungerlo nuovamente utilizzando la **Impostazione dei dettagli di assegnazione personalizzati** opzione .
* Se è necessario modificare le proprietà dei dettagli di assegnazione predefiniti, è necessario eseguire questa operazione direttamente dalla pagina dei dettagli del canale.

### Rimuovere i dettagli di assegnazione predefiniti da un canale {#remove-display}

1. Passare alla pagina dei dettagli del canale che si desidera rimuovere i dettagli di assegnazione predefiniti.
1. Individua il **Dettagli assegnazione predefiniti** nella pagina
1. Fai clic sul pulsante **Rimuovi predefinito**.

   ![immagine](/help/screens-cloud/assets/display/Assignments9.png)

1. Viene visualizzata una finestra di dialogo di conferma in cui i dettagli corrispondono a una delle seguenti condizioni:
   **a)** Il canale non viene utilizzato in alcuna visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/Assignments10.png)

**b)** Il canale viene utilizzato in un unico display.

![immagine](/help/screens-cloud/assets/display/Assignment11.png)

**c.** Il canale viene utilizzato in diverse visualizzazioni.

![immagine](/help/screens-cloud/assets/display/Assignments12.png)

1. Fai clic sul pulsante *Rimuovi* per convalidare la modifica.

**Nota:** Rimuovendo i dettagli di assegnazione predefiniti da un canale, verranno rimosse le assegnazioni corrispondenti su tutte le visualizzazioni che lo utilizzavano.
Di conseguenza, se non è disponibile alcun contenuto alternativo da riprodurre su tali display, ciò potrebbe causare la creazione di schermate vuote.

## Novità {#whats-next}

Ora che hai configurato un canale AEM Screens nel tuo progetto, devi pubblicare il canale. Fai riferimento a [Pubblicazione dei canali in Screens as a Cloud Service](manage-publish.md) prima di gestire i lettori da Screens Services Provider.
