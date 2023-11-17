---
title: "Interfaccia utente di [!DNL Assets view]"
description: Comprendere l’interfaccia utente e la navigazione in [!DNL Assets view].
role: User
exl-id: 534a8084-88f7-410e-b872-719e47e62b10
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 89%

---

# Accedere ai file e alle cartelle e visualizzare le risorse {#view-assets-and-details}

<!-- TBD: Give screenshots of all views with many assets. Zoom out to showcase how the thumbnails/tiles flow on the UI in different views. -->

<!-- TBD: The options in left sidebar may change. Shared with me and Shared by me are missing for now. Update this section as UI is updated. -->

## Interfaccia utente di [!DNL Assets view] {#understand-interface-navigation}

[!DNL Assets view] offre un’interfaccia utente intuitiva. che consente di trovare e ricordare facilmente le risorse e le relative informazioni.

Quando accedi a [!DNL Assets view], viene visualizzata la seguente interfaccia.

![[!DNL Assets view] - Interfaccia utente](assets/assets-view-interface.png)

    *A: Barra laterale sinistra per sfogliare l’archivio, fornisce l’accesso ad alcune altre opzioni*
    *B: Visualizzare o comprimere la barra laterale sinistra per aumentare l’area di visualizzazione delle risorse*
    *C: Filtrare i risultati della ricerca*
    *D: Selezionare tutti i contenuti della cartella selezionata*
    *E: Opzioni di ordinamento delle risorse*
    *F: Casella di ricerca*
    *G: Caricare o trascinare file utilizzando il pulsante `Add Assets`*
    *H: Creare una nuova cartella*
    *I: Passare da una visualizzazione all’altra*

<!-- TBD: Need an embedded video here with narration. It has to be hosted on MPC to be embeddable. -->

## Sfogliare e visualizzare le risorse e le cartelle {#browse-repository}

È possibile sfogliare le cartelle dall’interfaccia utente principale o dalla barra laterale a sinistra. Durante la navigazione, puoi visualizzare le miniature delle risorse per sfogliare visivamente l’archivio oppure i dettagli delle risorse per trovare rapidamente quella desiderata. Le opzioni disponibili nella barra laterale a sinistra sono:

* [La mia area di lavoro](/help/assets/my-workspace-assets-view.md): Assets ora include un’area di lavoro personalizzabile che fornisce widget per accedere facilmente a specifiche aree dell’interfaccia di Assets e alle informazioni che ti interessano di più. Questa pagina funge da soluzione unica per fornire una panoramica degli elementi di lavoro e consentire un accesso rapido ai flussi di lavoro chiave. L’accesso più comodo a queste opzioni aumenta l’efficienza e la velocità dei contenuti.
* [Attività](/help/assets/my-workspace-assets-view.md): nella scheda **Le mie attività** puoi visualizzare le attività che ti sono state assegnate. Nella scheda **Attività assegnate** trovi invece le attività che hai creato. Inoltre, le attività completate si trovano in **Attività completate** scheda.
* [Risorse](/help/assets/manage-organize-assets-view.md): elenco di tutte le cartelle a cui ai accesso, con struttura ad albero.
* **Visualizzate di recente**: elenco delle risorse visualizzate in anteprima di recente. [!DNL Assets view] mostra solo le risorse visualizzate in anteprima. Non visualizza le risorse che scorri quando esplori i file o le cartelle dell’archivio.
* [Raccolte](/help/assets/manage-collections-assets-view.md): una raccolta è un insieme di risorse, cartelle o altre raccolte nella vista Risorse di Adobe Experience Manager. Puoi utilizzare le raccolte per condividere le risorse tra i vari utenti. A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse. Puoi condividere più raccolte con un utente. Ogni raccolta contiene riferimenti alle risorse. L’integrità dei riferimenti alle risorse viene mantenuta tra le varie raccolte.

* [Approfondimenti](/help/assets/manage-reports-assets-view.md#view-live-statistics): in [!DNL Assets view], puoi visualizzare insight in tempo reale nella tua dashboard. Vista Risorse consente di visualizzare in tempo reale i dati del tuo ambiente vista Risorse, con la dashboard Insight. Puoi visualizzare le metriche degli eventi in tempo reale negli ultimi 30 giorni o negli ultimi 12 mesi.
* **Cestino**: mostra l’elenco delle risorse eliminate dalla cartella principale **[!UICONTROL Risorse]**. È possibile selezionare una risorsa nella cartella Cestino per ripristinarla nella posizione originale o eliminarla definitivamente. Puoi anche specificare una parola chiave o applicare filtri standard o personalizzati per cercare le risorse appropriate all’interno della cartella Cestino. Per ulteriori informazioni sull’utilizzo di filtri standard e personalizzati, consulta [Cercare le risorse nella vista Risorse](/help/assets/search-assets-view.md).
* **Impostazioni**: puoi configurare diverse opzioni della vista Risorse utilizzando **Impostazioni**, ad esempio Moduli di metadati, Report e Gestione tassonomia.

<!-- TBD: Not sure if we want to publish these right now. CC Libs are beta as per Greg.
* **Libraries**: Access to [!DNL Adobe Creative Cloud Team] (CCT) Libraries view. This view is visible only if the user is entitled to CCT Libraries.
-->

<!-- TBD: My Work Space shows task inbox and it is not visible on AEM Cloud Demos as of now. It is the source of truth server hence not documenting My Work Space option for now.
-->

Puoi aprire o comprimere la barra laterale a sinistra per aumentare l’area disponibile per la visualizzazione delle risorse.

In [!DNL Assets view], puoi visualizzare le risorse, le cartelle e i risultati di ricerca in quattro diversi tipi di layout.

* ![icona della vista elenco](assets/do-not-localize/list-view.png) [!UICONTROL Vista a elenco]
* ![icona della vista griglia](assets/do-not-localize/grid-view.png) [!UICONTROL Vista a griglia]
* ![icona della vista galleria](assets/do-not-localize/gallery-view.png) [!UICONTROL Vista galleria]
* ![icona della vista cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista a cascata]

Per individuare una risorsa, puoi ordinare le risorse in ordine crescente o decrescente di `Name`, `Relevancy`, `Size`, `Modified` e `Created`.

Per accedere a una cartella, fai doppio clic sulle miniature della cartella o selezionala dalla barra laterale a sinistra. Per visualizzare i dettagli di una cartella, selezionala e fai clic su Dettagli nella barra degli strumenti in alto. Per spostarsi verso l’alto o il basso nella gerarchia, utilizza la barra laterale a sinistra o le breadcrumb in alto.

![Sfogliare le cartelle](assets/browsing-folders.png)

*Figura: Per sfogliare la gerarchia, utilizza le breadcrumb in alto o la barra laterale a sinistra.*

## Visualizzare l’anteprima delle risorse {#preview-assets}

Prima di utilizzare, condividere o scaricare una risorsa, puoi visualizzarla più da vicino. La funzione di anteprima consente di visualizzare non solo le immagini ma anche alcuni altri tipi di risorse supportati.

Per visualizzare in anteprima una risorsa, selezionala e fai clic sull’[!UICONTROL Dettagli] ![icona dei dettagli](assets/do-not-localize/edit-in-icon.png) dalla barra degli strumenti nella parte superiore. Non puoi solo visualizzare la risorsa, ma anche i metadati dettagliati e intraprendere altre azioni.

![Visualizzare in anteprima una risorsa](assets/preview-asset-2.png)

*A: Tornare alla cartella corrente o al risultato della ricerca corrente nell’archivio*
*B: Nome e formato del file che si sta visualizzando in anteprima*
*C: Assegnare le attività*
*D: Scaricare la risorsa*
*E: Anteprima della risorsa e visualizzazione delle informazioni sui metadati*
*D: Metadati avanzati*
*E: Parole chiave e tag avanzati*
*F: Commentare e annotare*
*G: Visualizzare le attività relative alla risorsa selezionata*
*H: Visualizzare e gestire le versioni*
*I: Visualizzare le rappresentazioni dell’immagine*
*J: Modificare l’immagine*
*K: Metadati di base*
*L: Metadati avanzati*
*M: Parole chiave e tag avanzati*
*N: Visualizzare un’anteprima più dettagliata. Zoom, Schermo intero e altre opzioni*
*O: Passare alla risorsa precedente o successiva nella cartella corrente senza tornare alla cartella*

Puoi anche visualizzare in anteprima i video.

![Anteprima video](assets/preview-video.png)

Se visualizzi esplicitamente l’anteprima di una risorsa, [!DNL Assets view] la mostra come risorsa visualizzata di recente.

<!-- TBD: Describe the options.

Explicitly previewed assets are displayed as recently viewed assets. Give screenshot of this.
Other use cases after previewing.
-->

## Passaggi successivi {#next-steps}

* Fornisci feedback sui prodotti utilizzando l’opzione [!UICONTROL Feedback] disponibile nell’interfaccia utente della vista Risorse

* Fornisci feedback alla documentazione utilizzando [!UICONTROL Modifica questa pagina] ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema] ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibile sulla barra laterale destra

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/?support-solution=General&amp;lang=it#support)

>[!MORELIKETHIS]
>
>* [Visualizzare le versioni di una risorsa](/help/assets/manage-organize-assets-view.md#view-versions).
