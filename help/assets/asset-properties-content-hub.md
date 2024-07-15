---
title: Proprietà risorsa in [!DNL the Content Hub]
description: Scopri come visualizzare e gestire le proprietà delle risorse in [!DNL Content Hub]
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 8%

---


# Gestire le proprietà delle risorse in Content Hub {#asset-properties}

![Immagine banner metadati](assets/metadata-banner-image.png)

[!DNL The Content Hub] consente di visualizzare informazioni sulla risorsa, che sono fondamentali per una distribuzione efficiente delle risorse. Si tratta della raccolta di tutti i dati disponibili per una risorsa.

La visualizzazione delle proprietà delle risorse consente di categorizzare ulteriormente le risorse ed è utile in caso di aumento della quantità di informazioni digitali. Ricorrendo solo ai nomi dei file, alle miniature e alla memoria dell’utente, è possibile gestire alcune centinaia di file. Tuttavia, questo approccio non è scalabile quando aumentano il numero di persone coinvolte e il numero di risorse gestite. Inoltre, il valore di una risorsa digitale aumenta man mano che la risorsa diventa:

* Più accessibile: i sistemi e gli utenti possono trovarla facilmente.
* Più semplice da gestire: puoi trovare facilmente le risorse con lo stesso set di proprietà e applicarvi modifiche.
* Completo: la risorsa contiene più informazioni e contesto.

## Prerequisiti {#prerequisites}

[Gli utenti di Content Hub](deploy-content-hub.md#onboard-content-hub-users) possono eseguire le azioni indicate in questo articolo.

## Visualizzare le proprietà di una risorsa {#properties-ui}

Prima di utilizzare, condividere o scaricare una risorsa, puoi visualizzarla più da vicino. La funzione di anteprima consente di visualizzare non solo le immagini, ma anche alcuni altri tipi di risorse supportati. Oltre a visualizzare la risorsa, puoi visualizzarne le informazioni dettagliate e intraprendere altre azioni. Per visualizzare le informazioni di una risorsa, passa alla risorsa o [cerca](search-assets.md) la risorsa, quindi fai clic sulla risorsa per aprirne le proprietà. La figura seguente illustra i campi disponibili nella pagina delle proprietà di una risorsa:

![Proprietà dell&#39;interfaccia utente di una risorsa](assets/properties-ui.png)

* **A:** titolo di una risorsa
* **B:** Percentuale di risorse di zoom o anteprima più vicine mediante zoom avanti o indietro
* **C:** Annulla zoom alla percentuale selezionata in precedenza
* **D:** Passare alla risorsa precedente o successiva
* **E:** conteggio Assets
* **F:** scarica la risorsa
* **G:** Modifica risorsa tramite [!DNL Adobe Express]
* **H:** Comprimi o visualizza in anteprima le informazioni di una risorsa
* **I:** Condividi la risorsa
* **J:** Aggiungi risorsa a [!DNL Collection]
* **K:** Chiudi la schermata di anteprima
* **L:** informazioni di una risorsa che includono titolo, formato, dimensione, risoluzione, tag, tag colore e smart tag.

## Formati supportati {#supported-formats}

Nella tabella seguente sono illustrati i formati di file supportati in [!DNL the Content Hub]:

<table> 
    <tbody>
     <tr>
      <th><strong>Tipo di file</strong></th>
      <th><strong>Formati supportati</strong></th>
     </tr>
     <tr>
      <td>Immagine</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL SVG]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Video</td>
      <td>
        <ul>
            <li>[!UICONTROL Quicktime]</li>  
            <li>[!UICONTROL MP4]</li> 
        </ul>
      </td>
     </tr>
      <tr>
      <td>Documento</td>
      <td>
        <ul>
            <li>[!UICONTROL txt] (semplice)</li>  
            <li>[!UICONTROL Doc/Docx]</li> 
            <li>[!UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Supporti di stampa</td>
      <td>
        <ul>
            <li>[!UICONTROL PDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### Proprietà derivate dopo il caricamento di una risorsa {#derived-properties}

Dopo aver caricato una risorsa, Content Hub ne deriva alcune proprietà che vengono generate automaticamente. Di seguito è riportato un elenco di alcuni di essi:

* **Dimensioni:** Le dimensioni mostrano il valore logico di una risorsa in base alle dimensioni. Questo chiarisce lo spazio occupato da una risorsa in un archivio. [!DNL The Content Hub] supporta risorse fino a 2 GB.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Tag avanzati:** [!DNL The Content Hub] utilizza i servizi di contenuti avanzati di Adobe Sensei per addestrare le risorse utilizzando l&#39;algoritmo di riconoscimento sulla struttura basata su tag. Questa content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse. Grazie ai tag avanzati è possibile velocizzare le attività relative ai contenuti dei progetti grazie alla possibilità di trovare rapidamente le risorse rilevanti. Gli smart tag sono un esempio di informazioni sulla risorsa non contenute nell’immagine. [!DNL The Content Hub] applica automaticamente i tag avanzati alle risorse per impostazione predefinita.

* **Tag colore:** [I tag colore](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) consentono di riconoscere una risorsa utilizzando colori identificati automaticamente in una risorsa mediante le funzionalità di IA per l&#39;analisi dei colori di Adobe in Sensei.

* Data di caricamento

* Caricato da

* Ultima modifica

* Ultima modifica eseguita da

Sono inoltre disponibili proprietà specificate durante l’aggiunta di risorse a Content Hub. Per ulteriori informazioni, consulta [Aggiungere risorse approvate dal marchio a Content Hub](upload-brand-approved-assets.md). Tali proprietà vengono visualizzate anche nella pagina delle proprietà della risorsa.

Gli amministratori possono anche configurare le proprietà visualizzate per ogni risorsa. Per ulteriori informazioni, vedere [Configurare l&#39;interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

