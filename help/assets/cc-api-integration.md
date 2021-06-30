---
title: Automazione dei contenuti per l'integrazione con Creative Cloud
description: Generare varianti di risorse utilizzando l’integrazione con Creative Cloud
contentOwner: AG
feature: Caricare, Elaborazione delle risorse, Pubblicazione, Microservizi di Asset compute, Flusso di lavoro
role: Business Practitioner,Administrator
source-git-commit: 05f2bfac12d37b8ef9940e3381c709891cabe236
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Generare varianti di risorse utilizzando l’integrazione [!DNL Adobe Creative Cloud] {#content-automation}

Il componente aggiuntivo per l’automazione dei contenuti integra Experience Manager Assets come Cloud Service e le API Adobe Creative Cloud per elaborare in modo creativo le risorse su larga scala. Experience Manager utilizza i [microservizi per le risorse basati su cloud](/help/assets/asset-microservices-overview.md) per sfruttare le funzioni Adobe Creative Cloud e automatizzare la creazione delle risorse e la gestione dei contenuti multimediali.

Per modificare le risorse in [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], non è necessario scaricare, modificare e caricare in [!DNL Experience Manager Assets]. È sufficiente creare e configurare un profilo di elaborazione, applicare il profilo a una cartella e caricare le risorse nella cartella. Le risorse caricate nella cartella vengono elaborate per creare diverse varianti di tale risorsa. L’elaborazione e l’editing in serie delle risorse sono stati semplici e coerenti e hanno consentito di risparmiare tempo e velocizzare i contenuti. Inoltre, gli sviluppatori e i partner possono estendere i microservizi per le risorse con accesso diretto a queste API e includere una logica personalizzata.

Gli utenti possono creare profili di elaborazione per automatizzare le seguenti operazioni creative sulle risorse:

**Tono** automatico: Utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e apporta in modo intelligente correzioni di luce e colore in base agli attributi unici dell&#39;immagine.
**Automatico verticale**: Utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e correggere la prospettiva distorta nelle immagini. Ad esempio, per creare orizzonti di livello.
**Predefiniti** Lightroom: Applica un aspetto definito dall’utente alle immagini per ottenere un aspetto uniforme utilizzando i predefiniti personalizzati.
**Ritaglio** immagine: Utilizza l&#39;intelligenza artificiale per creare una selezione intorno agli oggetti più importanti e rimuovere lo sfondo con un singolo comando.
**Maschera** immagine: Utilizza l&#39;intelligenza artificiale per creare una maschera intorno agli oggetti più importanti con un unico comando.
**Azioni** Photoshop: Applica una serie di attività (in Photoshop) a un file o a un batch di file.
**Sostituzione** di oggetti avanzati: Esegue la personalizzazione su scala consentendo di scambiare le immagini mantenendo tutti gli effetti e le regolazioni applicati all&#39;interno di un file PSD.

## Utilizzare un profilo di elaborazione per elaborare le risorse {#process-assets}

Per utilizzare i profili di elaborazione per creare automaticamente le varianti, effettua le seguenti operazioni:

1. Contatta l’Assistenza clienti Adobe per acquisire la licenza.
1. Passa a Strumenti > Risorse > Profili di elaborazione.
1. Selezionare Crea e specificare un Nome.
1. Seleziona la scheda Creativo . Specifica la cartella di output, seleziona [!UICONTROL Aggiungi nuovo] per aggiungere configurazioni creative. Specifica Nome rappresentazione (o nome di output), Estensione (o tipo di file), seleziona Qualità (o parametri di output), seleziona Include and Excludes MIME type lists (Include and Excludes MIME type lists) (o Input asset filter) e seleziona l’operazione creativa richiesta.
1. Per alcune operazioni è necessario un parametro aggiuntivo (risorsa). Se richiesto, fornisci valori per questi parametri aggiuntivi.

1. Aggiungi più operazioni creative come parte dello stesso profilo di elaborazione o Salva il profilo.

1. Applica il profilo di elaborazione a una cartella. Seleziona Proprietà cartella, Elaborazione risorse e seleziona il profilo di elaborazione creato.

Una volta applicato il profilo di elaborazione a una cartella DAM, tutte le risorse caricate o aggiornate in questa cartella (o in sottocartelle, a meno che non siano sostituite) eseguono le operazioni definite in aggiunta all’elaborazione standard.

Per elaborare manualmente le risorse esistenti, seleziona le risorse e seleziona l’opzione **[!UICONTROL Rielabora]** , quindi seleziona il profilo di elaborazione richiesto.

## Suggerimenti e limitazioni {#limitations-best-practices}

* [!DNL Experience Manager] limita l’elaborazione delle risorse a 300 richieste al minuto per ambiente e a 700 richieste al minuto per organizzazione.
* La dimensione del file è limitata a 4 GB per le operazioni [!DNL Adobe Photoshop] API e a 1 GB per le operazioni [!DNL Adobe Lightroom].

>[!MORELIKETHIS]
>
>* [Configura e utilizza i microservizi per le risorse tramite i profili](/help/assets/asset-microservices-configure-and-use.md) di elaborazione.
>* [ [!DNL Experience Manager] Effettua l’integrazione con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).

