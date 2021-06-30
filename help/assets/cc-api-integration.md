---
title: Automazione dei contenuti per l'integrazione con Creative Cloud
description: Generare varianti di risorse utilizzando l’integrazione con Creative Cloud
contentOwner: AG
feature: Caricare, Elaborazione delle risorse, Pubblicazione, Microservizi di Asset compute, Flusso di lavoro
role: Business Practitioner,Administrator
source-git-commit: ffca94ef8d93cf95011d7e3128c49929f69cdc28
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# Generare varianti di risorse utilizzando l’integrazione [!DNL Adobe Creative Cloud] {#content-automation}

Il componente aggiuntivo per l’automazione dei contenuti integra Experience Manager Assets come Cloud Service e le API Adobe Creative Cloud per elaborare in modo creativo le risorse su larga scala. Experience Manager utilizza i [microservizi per le risorse basati su cloud](/help/assets/asset-microservices-overview.md) per sfruttare le funzioni Adobe Creative Cloud e automatizzare la creazione delle risorse e la gestione dei contenuti multimediali.

Per modificare le risorse in [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], non è necessario scaricare, modificare e caricare in [!DNL Experience Manager Assets]. È sufficiente creare e configurare un profilo di elaborazione, applicare il profilo a una cartella e caricare le risorse nella cartella. Le risorse caricate nella cartella vengono elaborate per creare diverse varianti di tale risorsa. L’elaborazione e l’editing in serie delle risorse sono stati semplici e coerenti e hanno consentito di risparmiare tempo e velocizzare i contenuti. Inoltre, gli sviluppatori e i partner possono estendere i microservizi per le risorse con accesso diretto a queste API e includere una logica personalizzata.

Gli utenti possono creare profili di elaborazione per automatizzare le seguenti operazioni creative sulle risorse:

* **Tono** automatico: Utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e apporta in modo intelligente correzioni di luce e colore in base agli attributi unici dell&#39;immagine.
* **Automatico verticale**: Utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e correggere la prospettiva distorta nelle immagini. Ad esempio, per creare orizzonti di livello.
* **Predefiniti** Lightroom: Applica un aspetto definito dall’utente alle immagini per ottenere un aspetto uniforme utilizzando i predefiniti personalizzati.
* **Ritaglio** immagine: Utilizza l&#39;intelligenza artificiale per creare una selezione intorno agli oggetti più importanti e rimuovere lo sfondo con un singolo comando.
* **Maschera** immagine: Utilizza l&#39;intelligenza artificiale per creare una maschera intorno agli oggetti più importanti con un unico comando.
* **Azioni** Photoshop: Applica una serie di attività (in Photoshop) a un file o a un batch di file.
* **Sostituzione** di oggetti avanzati: Esegue la personalizzazione su scala consentendo di scambiare le immagini mantenendo tutti gli effetti e le regolazioni applicati all&#39;interno di un file PSD.

## Utilizzare un profilo di elaborazione per elaborare le risorse {#process-assets}

Per utilizzare i profili di elaborazione per creare automaticamente le varianti, effettua le seguenti operazioni:

1. Contatta l’ [Adobe Customer Care](https://experienceleague.adobe.com/#support) per ricevere la licenza.

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]**.

1. Seleziona **[!UICONTROL Crea]** e specifica un **[!UICONTROL Nome]**.

1. Seleziona la scheda **[!UICONTROL Creative]** , specifica la cartella di output e seleziona **[!UICONTROL Aggiungi nuovo]** per aggiungere configurazioni creative.

1. Fornisci **[!UICONTROL Nome rappresentazione]** (o nome output), **[!UICONTROL Estensione]** (o tipo di file), seleziona **[!UICONTROL Qualità]** (o parametri di output), seleziona Include and Excludes MIME type lists (Include and Excludes MIME type lists) (o il filtro risorse di input) e seleziona l’operazione creativa richiesta.

1. Alcune operazioni richiedono un parametro aggiuntivo (risorsa). Se necessario, fornisci valori per tali parametri aggiuntivi.

1. Aggiungi più operazioni creative come parte dello stesso profilo di elaborazione o Salva il profilo.

1. Applica il profilo di elaborazione a una cartella. Nella pagina **[!UICONTROL Proprietà]** di una cartella, seleziona **[!UICONTROL Elaborazione risorse]** e seleziona il profilo di elaborazione da applicare.

Dopo aver applicato il profilo di elaborazione a una cartella DAM, tutte le risorse caricate o aggiornate in questa cartella eseguono le operazioni definite in aggiunta all’elaborazione standard. Le sottocartelle ereditano gli stessi profili applicati alle cartelle principali. Gli utenti possono ignorare questa ereditarietà.

Per elaborare le risorse esistenti, seleziona le risorse, seleziona l’opzione **[!UICONTROL Rielabora]** , quindi seleziona il profilo di elaborazione richiesto.

## Suggerimenti e limitazioni {#limitations-best-practices}

* [!DNL Experience Manager] limita l’elaborazione delle risorse a 300 richieste al minuto per ambiente e a 700 richieste al minuto per organizzazione.
* La dimensione del file è limitata a 4 GB per le operazioni [!DNL Adobe Photoshop] API e a 1 GB per le operazioni [!DNL Adobe Lightroom].

>[!MORELIKETHIS]
>
>* [Configura e utilizza i microservizi per le risorse tramite i profili](/help/assets/asset-microservices-configure-and-use.md) di elaborazione.
>* [ [!DNL Experience Manager] Effettua l’integrazione con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).

