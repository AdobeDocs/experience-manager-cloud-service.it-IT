---
title: Integrazione nativa di AEM Assets con Adobi Express
description: L’integrazione nativa di AEM Assets con Adobi Express consente di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente di Adobi Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 8bbf9a2ba8f708a5a03d11bc0388d39b32d4c7b3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 6%

---

# Integrazione nativa con Adobi Express {#native-integration-adobe-express}

AEM Assets si integra in modo nativo con Adobi Express, che consente di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente di Adobi Express. Il contenuto gestito in AEM Assets può essere inserito nell’area di lavoro di Express e quindi il contenuto nuovo o modificato può essere salvato in un archivio AEM Assets. L’integrazione offre i seguenti vantaggi chiave:

* È stato migliorato il riutilizzo dei contenuti grazie alla modifica e al salvataggio di nuove risorse in AEM.

* È stato ridotto il tempo e l’impegno complessivi necessari per creare nuove risorse o nuove versioni di risorse esistenti.

## Prerequisiti {#prerequisites}

Diritti di accesso ad Adobi Express e ad almeno un ambiente in AEM Assets. L’ambiente può essere uno qualsiasi degli archivi in Assets as a Cloud Service o Assets Essentials.


## Utilizzare AEM Assets nell’editor di Adobi Express {#use-aem-assets-in-express}

Per iniziare a utilizzare AEM Assets nell’editor di Adobi Express, effettua le seguenti operazioni:

1. Apri l’applicazione web Adobi Express.

1. Apri una nuova area di lavoro vuota caricando un nuovo modello o progetto oppure creando una risorsa.

1. Clic **[!UICONTROL Risorse]** disponibile nel riquadro di navigazione a sinistra. In Adobe Express viene visualizzato l’elenco degli archivi a cui sei autorizzato ad accedere, insieme all’elenco delle risorse e cartelle disponibili a livello principale.

1. Sfoglia o cerca le risorse nel tuo archivio per trascinarle nell’area di lavoro. Puoi filtrare le risorse utilizzando vari filtri disponibili, ad esempio tipo di file, tipo MIME e dimensioni.

   ![inclusione delle risorse dal componente aggiuntivo di Assets](assets/adobe-express-native-integration.png)


## Salvare progetti di Adobe Express in AEM Assets {#save-express-projects-in-assets}

Dopo aver incorporato le modifiche appropriate nell’area di lavoro di Express, puoi salvarla nell’archivio di AEM Assets.

1. Clic **[!UICONTROL Condividi]** per aprire **[!UICONTROL Condividi]** .

   ![Salvare le risorse in AEM](assets/adobe-express-share.png)

1. Seleziona **[!UICONTROL AEM Assets]** dal **[!UICONTROL Storage]** disponibile nel riquadro a destra. In Adobe Express viene visualizzata la finestra di dialogo di caricamento.
1. Specifica un nome e un formato per la risorsa. È possibile salvare il contenuto dell&#39;area di lavoro in formato PNG o JPEG.

1. Fai clic sull’icona della cartella accanto al **[!UICONTROL Posizione]** , passa alla posizione in cui devi salvare la risorsa e fai clic su **[!UICONTROL Seleziona]**. Il nome della cartella viene visualizzato nel **[!UICONTROL Posizione]** campo.

   ![Salvare le risorse in AEM](assets/adobe-express-upload.png)

1. Facoltativo: puoi aggiungere i metadati della campagna per il caricamento utilizzando **[!UICONTROL Nome progetto o campagna]** campo. Puoi usare un nome esistente o crearne uno nuovo. Puoi definire più nomi di progetto o campagna per il caricamento. Durante la digitazione di un nome, fare clic in un punto qualsiasi della finestra di dialogo oppure premere il tasto `,` (Virgola) chiave per registrare il nome.

   Come best practice, l’Adobe consiglia di specificare i valori negli altri campi e di migliorare l’esperienza di ricerca delle risorse caricate.
1. Analogamente, definisci i valori per **[!UICONTROL Parole chiave]** e **[!UICONTROL Canali]** campi.

1. Clic **[!UICONTROL Carica]** per caricare la risorsa in AEM Assets.




## Limitazioni {#limitations}

Si è verificato un bug noto in alcuni utenti con accesso a più archivi Assets durante il salvataggio di un documento con risorse provenienti da più archivi.
