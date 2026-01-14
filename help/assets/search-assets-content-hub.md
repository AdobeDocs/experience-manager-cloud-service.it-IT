---
title: Cercare risorse in Content Hub
description: Scopri come cercare le risorse in [!DNL Content Hub]
role: User
exl-id: 8578d7d0-32b9-4e5c-80ef-3827e358ac6c
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Cerca in Assets in [!DNL Content Hub] {#search-assets}

Se nell’archivio sono presenti numerose risorse, la ricerca della risorsa corretta richiede tempo. La ricerca di [!DNL The Content Hub] consente di cercare le risorse approvate in modo da poter eseguire azioni aggiuntive, ad esempio il download, la condivisione o la creazione di raccolte. È possibile utilizzare varie funzionalità per limitare i risultati della ricerca, ad esempio l&#39;esecuzione di ricerche basate su testo, l&#39;utilizzo di filtri, l&#39;esecuzione di tag o di ricerche specifiche per i tag avanzati, la ricerca di un particolare formato di file e così via.

## Prerequisiti {#prerequisites}

[Gli utenti di Content Hub](deploy-content-hub.md#onboard-content-hub-users) possono eseguire le azioni indicate in questo articolo.

## Cosa è possibile cercare  {#what-you-can-search}

La ricerca di [!DNL Content Hub] fornisce risultati basati su:

* **Testo corrispondente:** La ricerca di [!DNL Content Hub] consente di cercare una risorsa utilizzando il nome o la descrizione. Puoi eseguire ricerche basate su parole chiave, in cui la parola chiave viene confrontata con il testo disponibile nelle proprietà di una risorsa.

* **Contesto corrispondente:** L&#39;elenco dei risultati della ricerca [!DNL Content Hub] contiene i risultati approssimativi delle risorse ottenuti in base al contesto corrispondente. Se ad esempio si digita `cool` nella barra di ricerca, le risorse relative a `winter`, `snow`, `cold surroundings` verranno visualizzate nell&#39;elenco di ricerca.

* **Informazioni sulla risorsa (titolo, tag o tag avanzati):** [!DNL Content Hub] utilizza l&#39;algoritmo di ricerca intelligente per classificare i risultati della ricerca in modo accurato e pertinente. [I metadati](#asset-properties.md) sono la raccolta di tutti i dati disponibili per una risorsa, ma potrebbero non essere necessariamente contenuti in tale risorsa. [Consente di categorizzare ulteriormente le risorse ed è utile in quanto la quantità di informazioni digitali aumenta](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub).

* **Data ultima modifica:** Le risorse modificate di recente vengono visualizzate all&#39;inizio dell&#39;elenco dei risultati di ricerca. Puoi anche filtrare l’intervallo di date in base alle tue esigenze.

* **Utilizzo:** Le risorse di uso comune vengono visualizzate all&#39;inizio dell&#39;elenco di ricerca.

* **Cronologia ricerche:** Fare clic all&#39;interno della casella di ricerca senza digitare un carattere per ottenere la cronologia delle ricerche. È inoltre possibile rimuovere qualsiasi parola chiave specifica dalla cronologia. La cronologia di ricerca viene salvata nella memoria cache di un browser Web. Se si accede alla ricerca [!DNL Content Hub] in un altro browser o si cancella la memoria cache del browser, non sarà più possibile visualizzare la cronologia di ricerca.

* **Ricerca durante la digitazione:** La ricerca di [!DNL Content Hub] migliora l&#39;esperienza di ricerca fornendo suggerimenti di completamento automatico quando si inizia a digitare.

## Ricerca di base {#basic-search}

Per eseguire la ricerca di base in [!DNL the Content Hub], passare alla barra di ricerca e specificare la parola chiave da cercare. Passa ai filtri disponibili nel riquadro a sinistra e applicali per limitare i risultati della ricerca.

Cercare ad esempio tutte le immagini **[!UICONTROL JPEG]** contenenti la parola chiave `architect`, che è stata modificata nell&#39;ultimo anno. Per eseguire questo scenario, esegui i seguenti passaggi:

1. Specificare `architect` come parola chiave di ricerca.

1. Passa a pannello filtri > **[!UICONTROL Formato]** > seleziona **[!UICONTROL JPEG]**.

1. Passa a **[!UICONTROL Modificato]** > specifica l&#39;intervallo di date.

   ![Ricerca di base](assets/basic-search.png)

## Restringi i risultati della ricerca utilizzando i filtri {#narrow-down-search-results}

Utilizza il pannello Filtri per cercare le risorse in base ai metadati. Puoi filtrare i risultati della ricerca in base a vari predicati di ricerca. Puoi selezionare tutti i predicati appropriati per ridurre o ridurre al minimo i risultati della ricerca. Puoi scegliere più di 10 predicati mentre filtri i risultati della ricerca. Quando selezioni più opzioni all’interno di un filtro, Content Hub visualizza le risorse che corrispondono a una qualsiasi delle opzioni selezionate all’interno di un filtro. Tuttavia, quando selezioni più opzioni tra i filtri, in Content Hub vengono visualizzate solo le risorse che corrispondono a tutte le opzioni selezionate tra i filtri, per limitare i risultati della ricerca.

I filtri predefiniti includono formato file, approvato da, data approvata, risorse scadute e non scadute e data di scadenza. Gli amministratori possono anche configurare i filtri visualizzati nell’elenco dei filtri. Per ulteriori informazioni, vedere [Configurare l&#39;interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-filters-content-hub).

<!--

<table>
    <tbody>
     <tr>
      <th><strong>Search Predicate</strong></th>
      <th><strong>Description</strong></th>
      <th><strong>Properties</strong></th>
     </tr>
     <tr>
      <td> Campaigns </td>
      <td> Allows you to search using planned activity performed to take any particular action. For example, advertisement campaign run on Ferrari to know the understand the interests of people using number of clicks people perform.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Channels </td>
      <td> Helps you to understand the path from where the asset is coming from. For example, web, social media, books, catalog, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Region </td>
      <td> Helps you to understand the location where the asset is created. For example, Japan, EMEA, Worldwide, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Keywords </td>
      <td> Keyword helps you search using terms or the words that you enter based on the topic. For example, images, low-resolution, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Timeframe </td>
      <td> Helps you search assets using timeline. For example, search by year 2024, Q3 2023, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td>File format</td>
      <td>Composition of an asset. The supported assets include image, document, video, printable media, and so on.</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL Quicktime]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL WebP]</li> 
            <li>[!UICONTROL MP4]</li> 
            <li>[!UICONTROL Plain]</li> 
            <li>[!UICONTROL PDF]</li>
            <li>[!UICONTROL SVG + XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Tags</td>
      <td>Tags help you categorize assets that can be browsed and searched more efficiently based on hierarchical taxonomies.</td>
      <td>
        <ul>
            <li>Field label</li>
            <li>Property name</li>
            <li>Path</li>
            <li>Description</li>
        </ul>
      </td>
     </tr>
     <!--<tr>
      <td>Subject</td>
      <td>Classification of assets based on their theme. For example, colorful, hiking, outdoors.</td>
      <td>NA</td>
     </tr>
          <tr>
      <td>Last modified</td>
      <td>Search assets based on their last modification. Specify the date range using the Start date and End date fields.</td>
      <td>
        <ul>
            <li>Range text (From)</li> 
            <li>Range text (To) </li>
        </ul>
      </td>
     </tr>    
     <!--<tr>
      <td>Asset ID</td>
      <td>Unique number that identifies the asset.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Colors </td>
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## Ricerca in blocco {#bulk-search}

La ricerca in blocco di risorse consente di cercare più risorse contemporaneamente inserendo un elenco di identificatori (come nomi, formati di file, colori, tag e altro ancora). Invece di cercare le risorse una alla volta, la funzione di ricerca in blocco di [!DNL Content Hub] consente di individuare più rapidamente le risorse necessarie. Con questa funzionalità, puoi immettere più valori per qualsiasi proprietà di filtro, separati da un delimitatore (ad esempio, più ID SKU), e recuperare immediatamente tutte le risorse corrispondenti con una singola ricerca.

Per cercare più risorse contemporaneamente, immetti più valori in una singola query separandoli con delimitatori ` [ , | \t | \r | \n | \r\n ]`. Puoi anche aggiungere altri delimitatori a seconda del caso d’uso. Vedi [Configurare la ricerca in blocco](configure-content-hub-ui-options.md#bulk-search-configuration).

Per eseguire la ricerca in blocco in [!DNL Content Hub], eseguire i passaggi seguenti:

1. Una volta che la ricerca in blocco è [configurata](configure-content-hub-ui-options.md#bulk-search-configuration), puoi visualizzare l&#39;opzione di ricerca in blocco nelle proprietà del filtro [!DNL Content Hub] configurate. Puoi abilitarlo o disabilitarlo in base al requisito.

1. Aggiungi una query di ricerca contenente i delimitatori specificati nella configurazione. La query di ricerca deve contenere una stringa accompagnata da più valori separati da virgola.

![Interfaccia utente per la ricerca in blocco](assets/bulk-search-ui.png)

## Fare di più con la ricerca {#do-more-with-search}

[!DNL The Content Hub] non è limitato alla ricerca, ma consente di eseguire azioni aggiuntive, ad esempio [download](download-assets-content-hub.md), [condivisione](share-assets-content-hub.md) e [aggiungere risorse alla raccolta](collections-content-hub.md), direttamente dall&#39;interfaccia di ricerca o anteprima. Seleziona le risorse nella pagina dei risultati della ricerca per visualizzare queste opzioni.

Ulteriori informazioni sulla [configurazione delle risorse in [!DNL Content Hub]](configure-content-hub-ui-options.md).


