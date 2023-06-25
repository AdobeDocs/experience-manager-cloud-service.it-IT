---
title: Creazione e gestione dei canali in Screens as a Cloud Service
description: Questa pagina descrive come creare e gestire i canali in Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 1%

---

# Creazione e gestione di un canale in Screens as a Cloud Service {#creating-channels-screens-cloud}

Dopo aver creato un progetto AEM Screens, devi creare i canali.
***Canali***, visualizza una sequenza di contenuti (immagini e video), un sito web o un’applicazione a pagina singola.

## Obiettivo {#objective}

Questo documento spiega come creare e gestire i canali per il progetto AEM Screens nel provider di contenuti Screens. Dopo aver letto dovresti essere a:

* informazioni su come creare canali per il provider di contenuti Screens
* gestire e modificare i contenuti nei canali
* pianificazione di attivazione per i canali

## Passaggi per creare un nuovo canale di sequenza in Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Prerequisiti**
>Prima di iniziare questa sezione della Guida TV, leggere [Creazione e gestione di progetti in Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Segui i passaggi seguenti per creare un nuovo canale di sequenza in Screens as a Cloud Service:

1. Passa a Provider di contenuti Screens.

1. Passa al progetto AEM Screens, ad esempio *FirstDigitalExperience*.

1. Seleziona la **Canali** cartella del progetto, ad esempio **FirstDigitalExperience** —> **Canali** e fai clic su **Crea** dalla barra delle azioni.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Seleziona il modello, ad esempio: **Canale sequenza** dal **Crea** e fai clic su **Successivo**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > Il **Crea** La procedura guidata fornisce diversi tipi di modelli durante la creazione di un canale. Consulta la sezione [Modelli disponibili](#available-templates) in Creazione guidata per ulteriori dettagli.

1. Immetti il nome del canale della sequenza, ad esempio: **LoopChannelOne** e fai clic su **Crea**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Ora visualizzerai un **LoopChannelOne** nella cartella Canali del progetto AEM Screens.

   Dopo aver creato il canale, ora puoi aggiungere contenuti al canale. Fai riferimento a [Aggiunta di contenuto a un canale](#add-content) per scoprire come aggiungere risorse (immagini/video) al tuo canale.

## Gestione di un canale {#managing-channels}

Puoi modificare, visualizzare proprietà e dashboard, copiare, visualizzare in anteprima ed eliminare un canale.

Passa al canale dal progetto e seleziona il canale, come illustrato nella figura riportata di seguito. È ora possibile selezionare le opzioni, ad esempio modificare il canale, visualizzare le proprietà, visualizzare l’anteprima del contenuto, gestire la pubblicazione o eliminare il canale dalla barra delle azioni.

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### Aggiunta di contenuto a un canale {#add-content}

Per aggiungere o modificare il contenuto di un canale, effettua le seguenti operazioni:

1. Selezionate il canale da modificare, come illustrato nella figura riportata di seguito. Fai clic su **Modifica** dall’angolo in alto a sinistra della barra delle azioni per aprire l’editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. L’editor ti consente di aggiungere al canale le risorse/componenti che desideri pubblicare.

1. Trascina e rilascia le risorse dal riquadro a sinistra e aggiungilo all’editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Fai clic su **Anteprima** per visualizzare in anteprima il contenuto del canale.
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Modelli disponibili nella Creazione guidata {#available-templates}

Sono disponibili i seguenti modelli quando si utilizza **Crea** procedura guidata canale:

| Modelli disponibili | Descrizione |
|--- |--- |
| Cartella canali | Consente di creare una cartella in cui archiviare la raccolta di canali. |
| Canale per sequenza | Consente di creare un canale che riproduce i componenti in sequenza (uno per uno in una presentazione). |
| Canale schermo diviso barra a L sinistra o destra | Consente agli autori di contenuto di visualizzare diversi tipi di risorse in aree di dimensioni appropriate. |

## Usa dettagli assegnazione predefiniti per i canali {#default-channels}

Questa funzionalità consente di definire una pianificazione di attivazione predefinita per un canale e di utilizzarla per impostazione predefinita per ogni assegnazione di una visualizzazione. Questo fornisce un metodo in modo che non sia necessario ripetere la complicata definizione della pianificazione.

### Creare dettagli di assegnazione predefiniti per un canale {#create-default}

1. Passa alla pagina dei dettagli del canale che desideri configurare.
1. Individua il **Dettagli assegnazione predefiniti** sulla pagina.

   ![immagine](/help/screens-cloud/assets/display/Assignment1.png)

1. Clic **Imposta dettagli predefiniti**.
1. Configurare i dettagli di assegnazione predefiniti, tra cui priorità, date di inizio e fine e criteri di ricorrenza per il canale, quindi fare clic su **Assegna**.

   ![immagine](/help/screens-cloud/assets/display/Assignments2.png)

1. I dettagli dell&#39;assegnazione sono visualizzati nella **Dettagli assegnazione predefiniti** riquadro:

   ![immagine](/help/screens-cloud/assets/display/Assignments3.png)

In questa sezione vengono visualizzate le seguenti informazioni:
* Priorità predefinita del canale nella visualizzazione.
* Date di inizio e fine dell’attivazione quando è pianificata la riproduzione del canale.
* Vista sintetica della ricorrenza (Oraria/Giornaliera/Settimanale/Mensile/Annuale e nome assegnato alla ricorrenza).

### Utilizza i dettagli di assegnazione predefiniti per l’assegnazione a una visualizzazione {#default-display}

I canali a cui sono assegnati dettagli di assegnazione predefiniti possono essere assegnati come di consueto; è stata aggiunta l’opzione per utilizzare i dettagli di assegnazione predefiniti invece di definire manualmente quelli personalizzati ogni volta.

1. Passa alla pagina dei dettagli di visualizzazione a cui desideri assegnare il canale e fai clic su **Assegna canale**.
in alternativa, seleziona la visualizzazione desiderata nella vista inventario e fai clic sul pulsante **Assegna canale**.
1. Viene visualizzata la finestra di dialogo assegnazione canale.

   ![immagine](/help/screens-cloud/assets/display/Assignments4.png)

1. Seleziona il canale desiderato con i dettagli di assegnazione predefiniti dal selettore canale.
1. La finestra di dialogo assegnazione canale viene modificata per consentire di scegliere i dettagli di assegnazione predefiniti o di selezionare quelli personalizzati:

   ![immagine](/help/screens-cloud/assets/display/Assignments5.png)

1. Clic **Assegna** per finalizzare l&#39;assegnazione o fare clic su **Imposta dettagli assegnazione personalizzata** se preferisci ignorare i valori predefiniti con altri valori nel contesto di quella particolare visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/Assignments6.png)

1. Osserva **Canali assegnati** il riquadro viene aggiornato con la nuova assegnazione:

   ![immagine](/help/screens-cloud/assets/display/Assignments7.png)

1. Tieni presente che i canali avranno un’icona diversa a seconda che utilizzino pianificazioni personalizzate (icona Orologio) o che ereditino i dettagli predefiniti (icona Orologio); facendo clic su di essi verranno visualizzati i dettagli della pianificazione.
1. Inoltre, le azioni disponibili per ciascun tipo saranno diverse.

   ![immagine](/help/screens-cloud/assets/display/Assignments8.png)

**Nota:** Un&#39;assegnazione di canale che utilizza i dettagli di assegnazione predefiniti non sarà modificabile nel contesto della visualizzazione.

* Se è necessario modificarla in un&#39;assegnazione personalizzata, è necessario innanzitutto rimuoverla e quindi aggiungerla nuovamente utilizzando **Imposta dettagli assegnazione personalizzata** opzione.
* Se è necessario modificare le proprietà dei dettagli di assegnazione predefiniti, è necessario farlo direttamente dalla pagina dei dettagli del canale.

### Rimuovere i dettagli di assegnazione predefiniti da un canale {#remove-display}

1. Passare alla pagina dei dettagli del canale per il quale si desidera rimuovere i dettagli di assegnazione predefiniti.
1. Individua il **Dettagli assegnazione predefiniti** affiancare nella pagina
1. Fai clic su **Rimuovi predefinito**.

   ![immagine](/help/screens-cloud/assets/display/Assignments9.png)

1. Viene visualizzata una finestra di dialogo di conferma e i dettagli corrispondono a una delle seguenti condizioni:
   **a.** Il canale non viene utilizzato in alcun display.

   ![immagine](/help/screens-cloud/assets/display/Assignments10.png)

**b.** Il canale viene utilizzato in un singolo display.

![immagine](/help/screens-cloud/assets/display/Assignment11.png)

**c.** Il canale viene utilizzato in diversi display.

![immagine](/help/screens-cloud/assets/display/Assignments12.png)

1. Fai clic su *Rimuovi* per convalidare la modifica.

**Nota:** Se si rimuovono i dettagli di assegnazione predefiniti da un canale, le assegnazioni corrispondenti verranno rimosse da tutte le visualizzazioni che lo utilizzavano.
Di conseguenza, questo può portare alla creazione di schermate vuote se su tali schermi non è presente contenuto alternativo da riprodurre.

## Passaggio successivo {#whats-next}

Ora che hai configurato un canale AEM Screens nel progetto, devi pubblicare il tuo canale. Fai riferimento a [Pubblicazione di canali in Screens as a Cloud Service](manage-publish.md) prima di gestire i lettori da Screens Services Provider.
