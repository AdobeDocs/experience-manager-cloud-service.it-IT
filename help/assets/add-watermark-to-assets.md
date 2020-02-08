---
title: Aggiungere una filigrana alle risorse digitali
description: Scoprite come usare la funzione Filigrana per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Inserimento di filigrane {#watermarking}

La funzione Filigrana di Risorse Adobe Experience Manager (AEM) consente di aggiungere una filigrana digitale alle risorse, per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. Risorse AEM supporta il testo da usare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi il passaggio Filigrana nel flusso di lavoro Aggiorna risorsa DAM.

1. Toccate o fate clic sul logo AEM, quindi andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli di workflow, selezionate il flusso di lavoro **[!UICONTROL DAM Update Asset]** (Aggiorna risorsa) e fate clic su **[!UICONTROL Edit (Modifica)]**.

1. Dal pannello laterale, trascina il passaggio **[!UICONTROL Aggiungi filigrana]** nel flusso di lavoro Aggiorna risorsa DAM.

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>Posizionare il passaggio Aggiungi filigrana prima del passaggio Miniatura processo.

1. Aprite il passaggio **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. Nella scheda **[!UICONTROL Argomenti]** , specificate valori validi nei vari campi, inclusi testo, tipo di font, dimensione, colore, posizione, orientamento e così via. Per confermare le modifiche, toccate o fate clic sull’icona Fine.

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. Salva il flusso di lavoro Aggiorna risorsa **** DAM con il passaggio Filigrana.
1. Dall’interfaccia utente Risorse, caricate una risorsa di esempio. La filigrana viene visualizzata con la dimensione del font, il colore e così via, nella posizione configurata nei passaggi precedenti.
