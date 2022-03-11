---
title: Creazione e gestione dei canali in Screens as a Cloud Service
description: Questa pagina descrive come creare e gestire i canali in Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 7%

---

# Creazione e gestione di un canale in Screens as a Cloud Service {#creating-channels-screens-cloud}

Dopo aver creato un progetto AEM Screens, devi creare i canali.
***Canali***, visualizza una sequenza di contenuti (immagini e video), un sito web o un’applicazione a pagina singola.

## Obiettivo {#objective}

Questo documento è utile per comprendere come creare e gestire i canali per il progetto AEM Screens in Screens Content Provider. Dopo la lettura dovresti essere a:

* informazioni su come creare canali per Screens Content Provider
* gestire e modificare i contenuti nei canali

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


## Novità {#whats-next}

Ora che hai configurato un canale AEM Screens nel tuo progetto, devi pubblicare il canale. Fai riferimento a [Pubblicazione dei canali in Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) prima di gestire i lettori da Screens Services Provider.
