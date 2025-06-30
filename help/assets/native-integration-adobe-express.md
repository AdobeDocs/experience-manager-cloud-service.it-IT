---
title: Integrazione nativa di AEM Assets con Adobe Express
description: L’integrazione nativa di AEM Assets con Adobe Express consente di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente di Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 8%

---

# Integrazione nativa con Adobe Express {#native-integration-adobe-express}

AEM Assets si integra in modo nativo con Adobe Express, che dalla sua interfaccia utente ti consente di accedere direttamente alle risorse memorizzate in AEM Assets. Il contenuto gestito in AEM Assets può essere inserito nell’area di lavoro di Express e quindi il contenuto nuovo o modificato può essere salvato in un archivio AEM Assets. L’integrazione offre i seguenti vantaggi chiave:

* È stato aumentato il riutilizzo dei contenuti modificando e salvando nuove risorse in AEM.

* È stato ridotto il tempo e l’impegno complessivi necessari per creare nuove risorse o nuove versioni di risorse esistenti.

## Prerequisiti {#prerequisites}

Diritti di accesso ad Adobe Express e ad almeno un ambiente in AEM Assets. L’ambiente può essere uno qualsiasi degli archivi in Assets as a Cloud Service o Assets Essentials.


## Utilizzare AEM Assets nell’editor di Adobe Express {#use-aem-assets-in-express}

Per iniziare a utilizzare AEM Assets nell’editor di Adobe Express, effettua le seguenti operazioni:

1. Apri l’applicazione web Adobe Express.

2. Apri una nuova area di lavoro vuota caricando un nuovo modello o progetto oppure creando una risorsa.

3. Fai clic su **[!UICONTROL Assets]** disponibile nel riquadro di navigazione a sinistra. Adobe Express mostra l’elenco degli archivi a cui hai diritto di accesso e l’elenco delle risorse e cartelle disponibili a livello principale.

4. Sfoglia o cerca le risorse nel tuo archivio per trascinarle nell’area di lavoro. Puoi filtrare le risorse utilizzando vari filtri disponibili, ad esempio tipo di file, tipo MIME e dimensioni.

   >[!NOTE]
   >
   >Il filtro per dimensione non si applica ai video.

   ![Inclusione delle risorse dal componente aggiuntivo di Assets](assets/adobe-express-native-integration.png)


## Salvare progetti Adobe Express in AEM Assets {#save-express-projects-in-assets}

Dopo aver incorporato le modifiche appropriate nell’area di lavoro di Express, puoi salvarla nell’archivio AEM Assets.

1. Fai clic su **[!UICONTROL Condividi]** per aprire la finestra di dialogo **[!UICONTROL Condividi]**.

   ![Salva risorse in AEM](assets/adobe-express-share.png)

2. Dalla sezione Archiviazione nel riquadro di destra, selezionare **AEM Assets**. Adobe Express visualizza la finestra di dialogo di caricamento.
3. Selezionare **Pagina corrente** o **Tutte le pagine**. Specifica un nome e un formato per le risorse da esportare. Puoi esportare i contenuti dell’area di lavoro nei formati PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. Il formato viene regolato automaticamente in base alle risorse presenti nelle pagine dell’area di lavoro.
Se selezioni **Pagina corrente**, la risorsa nella pagina corrente verrà salvata nella cartella di destinazione. Se si seleziona **Tutte le pagine** e il formato di esportazione non è PDF, tutte le pagine dell&#39;area di lavoro vengono salvate come file separati in una nuova cartella all&#39;interno della cartella di destinazione. Se il formato di esportazione è PDF, tutte le pagine canvas vengono salvate come un singolo file PDF nella cartella di destinazione.

4. Fai clic sull&#39;icona della cartella in **Cartella di destinazione** per selezionare un percorso e salvare le risorse.

   ![Salva risorse in AEM](/help/assets/assets/page-selection-and-destination-folder.svg)

5. Facoltativo: puoi aggiungere i metadati della campagna per il caricamento utilizzando il campo **Nome progetto o campagna**. Puoi usare un nome esistente o crearne uno nuovo. Puoi definire più nomi di progetto o campagna per il caricamento. Per registrare il nome, digitalo e premi Invio.
Come best practice, Adobe consiglia di specificare i valori negli altri campi e di creare un’esperienza di ricerca avanzata per le risorse caricate.

6. Allo stesso modo, definisci i valori per i campi **[!UICONTROL Parole chiave]** e **[!UICONTROL Canali]**.

7. Fai clic su **[!UICONTROL Carica]** per caricare le risorse in AEM Assets.

## Limitazioni {#limitations}

1. Per l&#39;importazione e l&#39;esportazione, il tipo di file video supportato è MP4.

2. Per l&#39;importazione video MP4:

   1. La dimensione massima del file supportata è 200 MB. Se questo limite viene superato, viene visualizzato un messaggio di avviso.
   2. La risoluzione massima supportata è di 3840 X 3840 pixel.
   3. I video con sfondi trasparenti (canale alfa) non sono supportati.

3. Per l&#39;esportazione video MP4:

   1. La dimensione massima del file supportata è 200 MB. Se questo limite viene superato, un avviso consiglia di tagliare il video a 200 MB o meno, oppure di caricarlo manualmente nella cartella di destinazione di AEM Assets dopo averlo scaricato.



