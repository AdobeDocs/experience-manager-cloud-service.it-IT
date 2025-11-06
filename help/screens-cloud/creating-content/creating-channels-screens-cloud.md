---
title: Creazione e gestione di canali in Screens as a Cloud Service
description: Questa pagina descrive come creare e gestire i canali in Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---

# Creazione e gestione di un canale in Screens as a Cloud Service {#creating-channels-screens-cloud}

Dopo aver creato un progetto AEM Screens, devi creare i canali.
***Canali***, visualizza una sequenza di contenuti (immagini e video), un sito Web o un&#39;applicazione a pagina singola.

## Obiettivo {#objective}

Questo documento spiega come creare e gestire i canali per il progetto AEM Screens in Screens Content Provider. Dopo aver letto dovresti essere a:

* informazioni su come creare canali per il provider di contenuti Screens
* gestire e modificare i contenuti nei canali
* gestisci la pianificazione di assegnazione e attivazione per i canali in [Screens Service Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)

## Passaggi per creare un nuovo canale di sequenza in Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Prerequisiti**
>Prima di iniziare questa sezione della Guida TV, controlla [Creazione e gestione di progetti in Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Segui i passaggi seguenti per creare un canale di sequenza in Screens as a Cloud Service:

1. Passa a Provider di contenuti Screens.

1. Passa al progetto AEM Screens, ad esempio *FirstDigitalExperience*.

1. Seleziona dal progetto la cartella **Canali**, ad esempio **FirstDigitalExperience** —> **Canali** e fai clic su **Crea** nella barra delle azioni.

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Seleziona il modello, ad esempio **Canale sequenza** dalla procedura guidata **Crea** e fai clic su **Avanti**.

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > La procedura guidata **Crea** fornisce diversi tipi di modelli durante la creazione di un canale. Per ulteriori dettagli, vedere [Modelli disponibili](#available-templates) nella Creazione guidata.

1. Immetti il nome del canale della sequenza, ad esempio **LoopingChannelOne** e fai clic su **Crea**.

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   Verrà ora visualizzato un **LoopingChannelOne** nella cartella Canali del progetto AEM Screens.

   Dopo aver creato il canale, ora puoi aggiungere contenuti al canale. Consulta [Aggiunta di contenuto a un canale](#add-content) per scoprire come aggiungere risorse (immagini/video) al tuo canale.

## Gestione di un canale {#managing-channels}

Puoi modificare, visualizzare proprietà e dashboard, copiare, visualizzare in anteprima ed eliminare un canale.

Passa al canale dal progetto e seleziona il canale, come illustrato nella figura riportata di seguito. È ora possibile selezionare le opzioni, ad esempio modificare il canale, visualizzare le proprietà, visualizzare l’anteprima del contenuto, gestire la pubblicazione o eliminare il canale dalla barra delle azioni.

![channelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### Aggiunta di contenuto a un canale {#add-content}

Per aggiungere o modificare il contenuto di un canale, effettua le seguenti operazioni:

1. Selezionate il canale da modificare, come illustrato nella figura riportata di seguito. Fai clic su **Modifica** dall&#39;angolo superiore sinistro della barra delle azioni per aprire l&#39;editor.

   ![modifica-canale1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. L’editor ti consente di aggiungere al canale risorse/componenti che desideri pubblicare.

1. Trascina e rilascia le risorse dal riquadro a sinistra e aggiungilo all’editor.

   ![modifica-canale2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Fai clic su **Anteprima** per visualizzare in anteprima il contenuto del tuo canale.
   >![modifica-anteprima canale](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Modelli disponibili nella Creazione guidata {#available-templates}

Sono disponibili i seguenti modelli durante l&#39;utilizzo della procedura guidata **Crea** canale:

| Modelli disponibili | Descrizione |
|--- |--- |
| Cartella canali | Consente di creare una cartella in cui archiviare la raccolta di canali. |
| Canale per sequenza | Consente di creare un canale che riproduce i componenti in sequenza (uno per uno in una presentazione). |
| Canale schermo diviso barra a L sinistra o destra | Consente agli autori di contenuto di visualizzare diversi tipi di risorse in aree di dimensioni appropriate. |

## Usa dettagli assegnazione predefiniti per i canali {#default-channels}

Questa funzionalità consente di definire una pianificazione di attivazione predefinita per un canale e di utilizzarla per impostazione predefinita per ogni assegnazione di una visualizzazione. Questo fornisce un metodo in modo che non sia necessario ripetere la complicata definizione della pianificazione.

1. Passare a [Provider servizi Screens](https://experience.adobe.com/screens).

### Creare dettagli di assegnazione predefiniti per un canale {#create-default}

1. Passa alla pagina dei dettagli del canale che desideri configurare.
1. Individua il riquadro **Dettagli assegnazione predefiniti** nella pagina.

   ![immagine](/help/screens-cloud/assets/display/Assignment1.png)

1. Fare clic su **Imposta dettagli predefiniti**.
1. Configura i dettagli di assegnazione predefiniti, tra cui priorità, date di inizio e fine e criteri di ricorrenza per il canale, quindi fai clic su **Assegna**.

   ![immagine](/help/screens-cloud/assets/display/Assignments2.png)

1. I dettagli dell&#39;assegnazione sono visualizzati nella sezione **Dettagli assegnazione predefiniti**:

   ![immagine](/help/screens-cloud/assets/display/Assignments3.png)

In questa sezione vengono visualizzate le seguenti informazioni:

* Priorità predefinita del canale nella visualizzazione.
* Date di inizio e fine dell’attivazione quando è pianificata la riproduzione del canale.
* Vista sintetica della ricorrenza (Oraria/Giornaliera/Settimanale/Mensile/Annuale e nome assegnato alla ricorrenza).

### Utilizza i dettagli di assegnazione predefiniti per l’assegnazione a una visualizzazione {#default-display}

I canali a cui sono assegnati dettagli di assegnazione predefiniti possono essere assegnati come di consueto; è stata aggiunta l’opzione per utilizzare i dettagli di assegnazione predefiniti invece di definire manualmente quelli personalizzati ogni volta.

1. Passare alla pagina dei dettagli di visualizzazione a cui si desidera assegnare il canale e fare clic su **Assegna canale**.
in alternativa, selezionare la visualizzazione desiderata nella visualizzazione [inventory](https://experience.adobe.com/screens/displays) e fare clic su **Assegna canale**.
1. Viene visualizzata la finestra di dialogo assegnazione canale.

   ![immagine](/help/screens-cloud/assets/display/Assignments4.png)

1. Seleziona il canale desiderato con i dettagli di assegnazione predefiniti dal selettore canale.
1. La finestra di dialogo assegnazione canale viene modificata per consentire di scegliere i dettagli di assegnazione predefiniti o di selezionare quelli personalizzati:

   ![immagine](/help/screens-cloud/assets/display/Assignments5.png)

1. Fare clic su **Assegna** per finalizzare l&#39;assegnazione oppure fare clic su **Imposta dettagli assegnazione personalizzati** se si preferisce ignorare i valori predefiniti con altri valori nel contesto di quella particolare visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/Assignments6.png)

1. La sezione **Canali assegnati** è stata aggiornata con la nuova assegnazione:

   ![immagine](/help/screens-cloud/assets/display/Assignments7.png)

1. Tieni presente che i canali avranno un’icona diversa a seconda che utilizzino pianificazioni personalizzate (icona Orologio) o che ereditino i dettagli predefiniti (icona Orologio); facendo clic su di essi verranno visualizzati i dettagli della pianificazione.
1. Inoltre, le azioni disponibili per ciascun tipo saranno diverse.

   ![immagine](/help/screens-cloud/assets/display/Assignments8.png)

**Nota:** un&#39;assegnazione di canale che utilizza i dettagli di assegnazione predefiniti non sarà modificabile nel contesto della visualizzazione.

* Se devi modificarla in un&#39;assegnazione personalizzata, rimuoverla e aggiungerla nuovamente utilizzando l&#39;opzione **Imposta dettagli assegnazione personalizzata**.
* Se è necessario modificare le proprietà dei dettagli di assegnazione predefiniti, farlo direttamente dalla pagina dei dettagli del canale.

### Rimuovere i dettagli di assegnazione predefiniti da un canale {#remove-display}

1. Passare alla pagina dei dettagli del canale per il quale si desidera rimuovere i dettagli di assegnazione predefiniti.
1. Individua il riquadro **Dettagli assegnazione predefiniti** nella pagina
1. Fare clic su **Rimuovi predefinito**.

   ![immagine](/help/screens-cloud/assets/display/Assignments9.png)

1. Viene visualizzata una finestra di dialogo di conferma e i dettagli corrispondono a una delle seguenti condizioni:
   Canale **a.** non utilizzato in alcuna visualizzazione.

   ![immagine](/help/screens-cloud/assets/display/Assignments10.png)

Il canale **b.** è utilizzato in un&#39;unica visualizzazione.

![immagine](/help/screens-cloud/assets/display/Assignment11.png)

Il canale **c.** è utilizzato in diverse visualizzazioni.

![immagine](/help/screens-cloud/assets/display/Assignments12.png)

1. Fai clic su *Rimuovi* per convalidare la modifica.

**Nota:** se si rimuovono i dettagli di assegnazione predefiniti da un canale, le assegnazioni corrispondenti verranno rimosse in tutte le visualizzazioni che lo utilizzavano.
Di conseguenza, questo può portare alla creazione di schermate vuote se su tali schermi non è presente alcun contenuto alternativo da riprodurre.

## Passaggio successivo {#whats-next}

Ora che hai configurato un canale AEM Screens nel progetto, devi pubblicare il tuo canale. Consulta [Pubblicazione dei canali in Screens as a Cloud Service](manage-publish.md) prima di gestire i lettori dal provider di servizi Screens.
