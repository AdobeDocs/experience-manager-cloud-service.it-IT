---
title: Integrazione nativa di AEM Assets con Adobi Express
description: L’integrazione nativa di AEM Assets con Adobi Express consente di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente di Adobi Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: d7e144d7f7722d4de96b3f85d44432863b350f92
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 8%

---

# Integrazione nativa con Adobi Express {#native-integration-adobe-express}

AEM Assets si integra in modo nativo con Adobe Express, che dalla sua interfaccia utente ti consente di accedere direttamente alle risorse memorizzate in AEM Assets. Il contenuto gestito in AEM Assets può essere inserito nell’area di lavoro di Express e quindi il contenuto nuovo o modificato può essere salvato in un archivio AEM Assets. L’integrazione offre i seguenti vantaggi chiave:

* È stato migliorato il riutilizzo dei contenuti grazie alla modifica e al salvataggio di nuove risorse in AEM.

* È stato ridotto il tempo e l’impegno complessivi necessari per creare nuove risorse o nuove versioni di risorse esistenti.

## Prerequisiti {#prerequisites}

Diritti di accesso ad Adobi Express e ad almeno un ambiente in AEM Assets. L’ambiente può essere uno qualsiasi degli archivi in Assets as a Cloud Service o Assets Essentials.


## Utilizzare AEM Assets nell’editor di Adobi Express {#use-aem-assets-in-express}

Per iniziare a utilizzare AEM Assets nell’editor di Adobi Express, effettua le seguenti operazioni:

1. Apri l’applicazione web Adobi Express.

2. Apri una nuova area di lavoro vuota caricando un nuovo modello o progetto oppure creando una risorsa.

3. Clic **[!UICONTROL Risorse]** disponibile nel riquadro di navigazione a sinistra. In Adobe Express viene visualizzato l’elenco degli archivi a cui sei autorizzato ad accedere, insieme all’elenco delle risorse e cartelle disponibili a livello principale.

4. Sfoglia o cerca le risorse nel tuo archivio per trascinarle nell’area di lavoro. Puoi filtrare le risorse utilizzando vari filtri disponibili, ad esempio tipo di file, tipo MIME e dimensioni.

   >[!NOTE]
   >
   >Il filtro per dimensione non si applica ai video.

   ![Inclusione delle risorse dal componente aggiuntivo di Assets](assets/adobe-express-native-integration.png)


## Salvare progetti di Adobe Express in AEM Assets {#save-express-projects-in-assets}

Dopo aver incorporato le modifiche appropriate nell’area di lavoro di Express, puoi salvarla nell’archivio AEM Assets.

1. Clic **[!UICONTROL Condividi]** per aprire **[!UICONTROL Condividi]** .

   ![Salvare le risorse in AEM](assets/adobe-express-share.png)

2. Dalla sezione Archiviazione nel riquadro di destra, selezionare **AEM Assets**. In Adobe Express viene visualizzata la finestra di dialogo di caricamento.
3. Seleziona una **Pagina corrente** o **Tutte le pagine**. Specifica un nome e un formato per le risorse da esportare. Puoi esportare i contenuti dell’area di lavoro nei formati PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. Il formato viene regolato automaticamente in base alle risorse presenti nelle pagine dell’area di lavoro.
Selezione **Pagina corrente** salva la risorsa nella pagina corrente nella cartella di destinazione. Se si seleziona **Tutte le pagine** e il formato di esportazione non è PDF, tutte le pagine canvas vengono salvate come file separati in una nuova cartella all’interno della cartella di destinazione. Se il formato di esportazione è PDF, tutte le pagine dell&#39;area di lavoro vengono salvate come un singolo file PDF nella cartella di destinazione.

4. Fai clic sull’icona della cartella in **Cartella di destinazione** per selezionare una posizione e salvare le risorse.

   ![Salvare le risorse in AEM](/help/assets/assets/page-selection-and-destination-folder.svg)

5. Facoltativo: puoi aggiungere i metadati della campagna per il caricamento utilizzando **Nome progetto o campagna** campo. Puoi usare un nome esistente o crearne uno nuovo. Puoi definire più nomi di progetto o campagna per il caricamento. Per registrare il nome, digitalo e premi Invio.
Come best practice, in Adobe è consigliabile specificare i valori negli altri campi e creare un’esperienza di ricerca avanzata per le risorse caricate.

6. Analogamente, definisci i valori per **[!UICONTROL Parole chiave]** e **[!UICONTROL Canali]** campi.

7. Clic **[!UICONTROL Carica]** per caricare le risorse su AEM Assets.

## Limitazioni {#limitations}

1. Per l&#39;importazione e l&#39;esportazione, il tipo di file video supportato è MP4.

2. Per l&#39;importazione video MP4:

   1. La dimensione massima del file supportata è 200 MB. Se questo limite viene superato, viene visualizzato un messaggio di avviso.
   2. La risoluzione massima supportata è di 3840 X 3840 pixel.
   3. I video con sfondi trasparenti (canale alfa) non sono supportati.

3. Per l&#39;esportazione video MP4:

   1. La dimensione massima del file supportata è 200 MB. Se questo limite viene superato, un avviso consiglia di tagliare il video a 200 MB o meno, oppure di caricarlo manualmente nella cartella di destinazione di AEM Assets dopo averlo scaricato.



