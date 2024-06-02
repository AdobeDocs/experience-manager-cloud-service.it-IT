---
title: Integrazione nativa di AEM Assets con Adobi Express
description: L’integrazione nativa di AEM Assets con Adobi Express consente di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente di Adobi Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 69d890eaae30468db89b9aff975a2a421f53fcff
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 9%

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

Dopo aver incorporato le modifiche appropriate nell’area di lavoro di Express, puoi salvarla nell’archivio di AEM Assets.

1. Clic **[!UICONTROL Condividi]** per aprire **[!UICONTROL Condividi]** .

   ![Salvare le risorse in AEM](assets/adobe-express-share.png)

2. Dalla sezione Archiviazione nel riquadro di destra, seleziona, **AEM Assets**. In Adobe Express viene visualizzata la finestra di dialogo di caricamento.
3. Specifica un nome e un formato per la risorsa. Puoi salvare il contenuto dell’area di lavoro nei formati PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. Il formato viene regolato automaticamente in base alle risorse.

   >[!NOTE]
   >
   >Selezionando &quot;Pagina corrente&quot; il file viene salvato nella cartella di destinazione. Selezionando &quot;Tutte le pagine&quot; viene creata una nuova cartella nella destinazione per tutti i file non PDF e li viene salvati mentre i file PDF vengono salvati come un singolo file nella cartella di destinazione.

4. Fare clic sull&#39;area di testo sotto **Cartella di destinazione** per selezionare una posizione e salvare le risorse.

   ![Salvare le risorse in AEM](/help/assets/assets/page-selection-and-destination-folder.png)

5. Facoltativo: puoi aggiungere i metadati della campagna per il caricamento utilizzando **Nome progetto o campagna** campo. Puoi usare un nome esistente o crearne uno nuovo. Puoi definire più nomi di progetto o campagna per il caricamento. Per registrare il nome, digitalo e premi Invio.
Come best practice, l’Adobe consiglia di specificare i valori negli altri campi e di migliorare l’esperienza di ricerca delle risorse caricate.

6. Analogamente, definisci i valori per **[!UICONTROL Parole chiave]** e **[!UICONTROL Canali]** campi.

7. Clic **[!UICONTROL Carica]** per caricare la risorsa in AEM Assets.




## Limitazioni {#limitations}

1. Per l&#39;importazione e l&#39;esportazione, il tipo di file video supportato è MP4.

2. Per l&#39;importazione video MP4:

   a) La dimensione massima del file supportata è 200 MB. Se questo limite viene superato, viene visualizzato un messaggio di avviso.
b) La risoluzione massima supportata è di 3840 X 3840 pixel.
c) I video con sfondi trasparenti (canale alfa) non sono supportati.

3. Per l&#39;esportazione video MP4:

   a) La dimensione massima del file supportata è 200 MB. Se questo limite supera, viene visualizzato un messaggio di avviso con un suggerimento di soluzione alternativa, come illustrato nell&#39;immagine seguente
   ![avviso con soluzione alternativa](/help/assets/assets/alert-with-workaround.png).
