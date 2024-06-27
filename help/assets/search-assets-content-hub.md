---
title: Cercare risorse in Content Hub
description: Scopri come cercare le risorse in [!DNL Content Hub]
role: User
source-git-commit: 15a266ccb6e4117c769d775a5f579fba943389bf
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---


# Cerca in Assets [!DNL Content Hub] {#search-assets}

![Condividere l&#39;immagine del banner delle risorse](assets/search.png)

Se nell’archivio sono presenti numerose risorse, la ricerca della risorsa corretta richiede tempo. [!DNL The Content Hub] la funzione di ricerca consente di cercare le risorse approvate in modo da poter eseguire azioni aggiuntive, ad esempio scaricare, condividere o creare raccolte. Puoi utilizzare varie funzionalità per limitare i risultati della ricerca, ad esempio eseguire ricerche basate su testo, utilizzare filtri, eseguire tag o ricerche specifiche per i tag avanzati, cercare un particolare formato di file e così via.

## Cosa è possibile cercare  {#what-you-can-search}

Il [!DNL Content Hub] la ricerca fornisce risultati in base a:

* **Testo corrispondente:** Il [!DNL Content Hub] la ricerca consente di cercare una risorsa utilizzando il suo nome o la sua descrizione. Puoi eseguire ricerche basate su parole chiave, in cui la parola chiave viene confrontata con il testo disponibile nelle proprietà di una risorsa.

* **Contesto corrispondente:** [!DNL Content Hub] l’elenco dei risultati della ricerca contiene i risultati approssimativi delle risorse ottenuti in base al contesto corrispondente. Ad esempio, se si digita `cool` nella barra di ricerca, le risorse correlate a `winter`, `snow`, `cold surroundings`, viene visualizzato nell&#39;elenco di ricerca.

* **Informazioni sulla risorsa (titolo, tag o tag avanzati):** [!DNL Content Hub] utilizza l’algoritmo di ricerca intelligente per classificare i risultati della ricerca in modo accurato e pertinente. [Metadati](#asset-properties.md) è la raccolta di tutti i dati disponibili per una risorsa, ma potrebbe non essere necessariamente contenuta in tale risorsa. [Consente di categorizzare ulteriormente le risorse ed è utile quando la quantità di informazioni digitali aumenta](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub).

* **Data ultima modifica:** Le risorse modificate di recente vengono visualizzate all’inizio dell’elenco dei risultati di ricerca. Puoi anche filtrare l’intervallo di date in base alle tue esigenze.

* **Utilizzo:** Le risorse di uso comune vengono visualizzate nella parte superiore dell’elenco di ricerca.

* **Cronologia ricerche:** Fare clic all&#39;interno della casella di ricerca senza digitare un carattere per ottenere la cronologia di ricerca. È inoltre possibile rimuovere qualsiasi parola chiave specifica dalla cronologia. La cronologia di ricerca viene salvata nella memoria cache di un browser web, il che significa che, se accedi a [!DNL Content Hub] eseguire la ricerca in un browser diverso o cancellare la memoria cache del browser, non è più possibile visualizzare la cronologia di ricerca.

* **Cerca durante la digitazione:** Il [!DNL Content Hub] la funzione di ricerca migliora l&#39;esperienza di ricerca fornendo suggerimenti al completamento automatico quando si inizia a digitare.

## Ricerca di base {#basic-search}

Per eseguire una ricerca di base su [!DNL the Content Hub], passare alla barra di ricerca e specificare la parola chiave da cercare. Passa ai filtri disponibili nel riquadro a sinistra e applicali per limitare i risultati della ricerca.

Ad esempio, cerca tutte le **[!UICONTROL JPEG]** immagini con parola chiave `architect` in esso, che viene modificato nell’ultimo anno. Per eseguire questo scenario, esegui i seguenti passaggi:

1. Specifica `architect` come parola chiave di ricerca.

1. Passa al pannello dei filtri > **[!UICONTROL Formato]** > seleziona **[!UICONTROL JPEG]**.

1. Accedi a **[!UICONTROL Modificato]** > specifica l’intervallo di date.

   ![Ricerca di base](assets/basic-search.png)

## Restringi i risultati della ricerca utilizzando i filtri {#narrow-down-search-results}

Utilizza il pannello Filtri per cercare le risorse in base ai metadati. Puoi filtrare i risultati della ricerca in base a vari predicati di ricerca. Puoi selezionare tutti i predicati appropriati per ridurre o ridurre al minimo i risultati della ricerca. Quando selezioni più opzioni all’interno di un filtro, Content Hub visualizza le risorse che corrispondono a una qualsiasi delle opzioni selezionate all’interno di un filtro. Tuttavia, quando selezioni più opzioni tra i filtri, in Content Hub vengono visualizzate solo le risorse che corrispondono a tutte le opzioni selezionate tra i filtri, per limitare i risultati della ricerca.

I filtri predefiniti includono formato file, approvato da, data approvata, risorse scadute e non scadute e data di scadenza. Gli amministratori possono anche configurare i filtri visualizzati nell’elenco dei filtri. Per ulteriori informazioni, consulta [Configurare l’interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-filters-content-hub).

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
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's Sensei AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## Fare di più con la ricerca {#do-more-with-search}

[!DNL The Content Hub] non è limitato alla ricerca, ma consente di eseguire azioni aggiuntive, come [scaricare](download-assets-content-hub.md), [condividere](share-assets-content-hub.md), e [aggiungere risorse alla raccolta](collections-content-hub.md), direttamente dall’interfaccia di ricerca o anteprima. Seleziona le risorse nella pagina dei risultati della ricerca per visualizzare queste opzioni.
