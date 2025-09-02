---
title: Ottimizzare le immagini utilizzando Dynamic Media con funzionalità OpenAPI
description: Scopri come ottimizzare le immagini al volo prima della distribuzione pubblica utilizzando le funzionalità di ottimizzazione delle immagini di Dynamic Media con funzionalità OpenAPI
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 74c5fbda5ee1ad46b5fcab5ba89f0fd96873e3cf
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# Ottimizzare le immagini utilizzando Dynamic Media con funzionalità OpenAPI{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] offre funzionalità di ottimizzazione delle immagini come [!DNL Smart Crop], [!DNL Image Presets] e [!DNL Smart Imaging]. Queste funzionalità consentono di fornire immagini reattive di alta qualità che vengono caricate rapidamente su diversi dispositivi e reti.

## Ritaglio avanzato{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[Ritaglio avanzato](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) è una funzionalità di ridimensionamento dinamico di [!DNL Dynamic Media with OpenAPI capabilities]. [!DNL Smart Crop] è una tecnica di elaborazione delle immagini avanzata che utilizza il ritaglio basato sul riconoscimento dei contenuti basato sull&#39;intelligenza artificiale per ritagliare in modo intelligente le immagini per diverse dimensioni dello schermo, preservando al contempo il contesto visivo nelle versioni ritagliate. L’intelligenza artificiale analizza l’immagine per identificare il punto focale o il punto di interesse desiderato, quindi ritaglia automaticamente l’immagine in modo da mantenere il punto focale in tutte le versioni ritagliate. [!DNL Smart Crop], un elemento chiave della progettazione reattiva, offre un modo conveniente e rapido per ritagliare le immagini.

Consulta l&#39;articolo [Profili immagine Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles) per scoprire come [creare copie trasformate Smart Crop](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles) in [!DNL Admin View], [applicarle alle cartelle](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders) o [modificare le copie trasformate](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image) già applicate a un&#39;immagine o a una cartella. Scopri come creare un [!DNL Smart Crop] passaggio per passaggio in questo [video](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

Il parametro [!DNL Smart Crop] prevede che esistano profili named-smartcrop e che siano stati applicati alla risorsa. Per ulteriori informazioni sul parametro [ e sulla modalità di applicazione dei profili denominati ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request), consulta [!DNL Smart Crop]Profili di ritaglio avanzato[!DNL Smart Crop].

>[!IMPORTANT]
>
> È possibile creare [!DNL Smart Crop] copie trasformate solo nella visualizzazione Amministratore.

## Predefiniti immagine{#image-presets-using-dynamic-media-with-openapi-capabilities}

Trasforma al volo le immagini utilizzando la funzionalità [Predefiniti immagine](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request) in [!DNL Dynamic Media with OpenAPI capabilities]. Un [!DNL image preset] è un insieme predefinito di regole di ridimensionamento e formattazione per un&#39;immagine di output.

[!DNL Dynamic Media with OpenAPI capabilities] utilizza nomi predefiniti per trasformare un&#39;immagine al volo e generarne immediatamente la rappresentazione. Quando si richiede un&#39;immagine tramite un URL di consegna [!DNL Dynamic Media with OpenAPI] che include un parametro predefinito, [!DNL DM with OpenAPI] applica le trasformazioni del predefinito, crea la rappresentazione su richiesta e la consegna all&#39;utente.

È possibile applicare un singolo predefinito a più immagini tramite i relativi URL di consegna [!DNL Dynamic Media with OpenAPI]. In questo modo viene garantita una formattazione coerente tra le risorse, senza dover modificare manualmente ciascuna risorsa.

Consulta l&#39;articolo [gestione dei predefiniti immagine](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets) per scoprire [come creare predefiniti immagine in Admin View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets) e [come creare predefiniti immagine reattivi](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset) che adattano automaticamente le risorse in base a dimensioni dello schermo diverse.

### Vantaggi dell&#39;utilizzo dei predefiniti immagine{#benefits-of-image-presets}

[!DNL Image Presets] offre diversi vantaggi per la gestione e la distribuzione di immagini in [!DNL Dynamic Media with OpenAPI]. Alcuni dei vantaggi principali includono:

* I predefiniti abbreviano gli URL di consegna delle immagini. Invece di aggiungere più modificatori di immagini che allungano l’URL di consegna, utilizza un singolo predefinito. URL più brevi sono più facili da gestire e garantiscono una distribuzione coerente delle immagini tra siti web, app mobili, e-mail e altri canali.
* I predefiniti per immagini creano rappresentazioni just-in-time da un file di immagine sorgente. Questa funzionalità di generazione di copie trasformate on-demand elimina la necessità di creare e archiviare più copie trasformate statiche dello stesso file, risparmiando tempo e spazio di archiviazione.
* Applica un singolo predefinito a un set di risorse di grandi dimensioni contemporaneamente, evitando modifiche manuali a ogni risorsa singolarmente, garantendo una formattazione coerente e abilitando la scalabilità.
* Quando si aggiornano i parametri di un predefinito, tutte le immagini che lo utilizzano vengono riformattate automaticamente. Questo semplifica le modifiche centralizzando gli aggiornamenti della formattazione ed eliminando la necessità di modificare singole risorse o codice web.
* Migliora l’efficienza e le prestazioni con le rappresentazioni dinamiche memorizzate nella cache dalla rete CDN, velocizzando il caricamento e ottimizzando le prestazioni su dispositivi e reti.

### Usa predefiniti immagine{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

Dopo aver creato [!DNL Image Presets], puoi utilizzarli per i seguenti flussi di lavoro:
* [Utilizza i predefiniti nell’URL di consegna delle immagini per crearne al volo le rappresentazioni prima di consegnarle all’utente finale](#use-presets-in-delivery-urls)
* [Utilizzare i predefiniti durante l’authoring in AEM Sites](#use-presets-during-authoring-in-aem-sites)

#### Utilizzare i predefiniti nell’URL di consegna dell’immagine{#use-presets-in-delivery-urls}

I predefiniti abbreviano e semplificano l’utilizzo degli URL di consegna.  Ogni nome di predefinito funge da identificatore univoco nell’URL di consegna. Invece di aggiungere più modificatori all’URL di consegna di una risorsa, fai riferimento al nome del predefinito per generarne immediatamente la rappresentazione. [Scopri come applicare i predefiniti per le immagini Dynamic Media all&#39;immagine](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets).
L’esempio seguente confronta un URL con un predefinito con un URL senza un predefinito.

**URL senza predefinito (URL lungo)**:

`https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true`

**URL con predefinito (URL breve)**:

`https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail`.
La miniatura predefinita racchiude le stesse impostazioni del modificatore di immagine.

#### Utilizzare i predefiniti durante l’authoring in AEM Sites{#use-presets-during-authoring-in-aem-sites}

Gli autori possono selezionare [!DNL Image Presets] durante la modifica delle pagine nella pagina di authoring [!DNL AEM Sites] quando è abilitato il supporto per [!DNL Dynamic Media].
Per utilizzare i predefiniti immagine nella pagina di authoring, effettua le seguenti operazioni:
1. Passa alla pagina di authoring di Sites.
1. Eseguire i passaggi descritti nella sezione [Accedere alle risorse remote nell&#39;Editor pagina di AEM](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) per utilizzare il pannello [!DNL Asset Selector] per selezionare una risorsa.
1. Nel pannello [!DNL asset selector], scorri verso il basso fino al tipo di predefinito **&#x200B;**&#x200B;e specifica `Preset=Preset Name` nel campo **[!UICONTROL Modificatori immagine]**.
   ![predefinito](/help/assets/assets/preset-in-asset-selector-panel.png)

## Imaging avanzato{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

Quando si utilizza [!DNL Dynamic Media with OpenAPI capabilities] per la consegna delle immagini, le immagini vengono ottimizzate automaticamente tramite [Smart imaging](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/). La distribuzione ottimizzata garantisce un caricamento più rapido delle immagini, una qualità visiva massima e dimensioni minime dei file. Questo consente di caricare le pagine più rapidamente e di ottenere una qualità visiva costantemente elevata su dispositivi e reti, con un consumo di larghezza di banda minimo e un sito web più veloce e reattivo.

[!DNL Smart Imaging] include le seguenti funzionalità:
* [Conversione automatica del formato](#auto-format-conversion)
* [Ottimizzazione della larghezza di banda di rete](#network-bandwidth-optimisation)

### Conversione automatica del formato{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [converte automaticamente le immagini in formati moderni ottimizzati per il Web come AVIF o WEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request). La conversione dipende dalle funzionalità del browser e da [licenza-diritto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate), indipendentemente dal formato richiesto.
I formati AVIF e WEBP offrono una compressione migliore, rendendo le immagini più piccole e veloci da consegnare e caricare. AVIF viene utilizzato come formato predefinito in quanto gestisce tutte le funzionalità del browser.
[!DNL Dynamic Media with OpenAPI] utilizza il parametro di query `auto-format` per controllare il comportamento del browser per la conversione di un&#39;immagine in vari formati per una consegna ottimizzata. La conversione automatica del formato include **promozione automatica** e **abbassamento di livello automatico**. Quando il sistema promuove un formato ottimizzato per il web (AVIF o WEBP) su JPEG o PNG per la distribuzione, viene chiamato promozione automatica.

Per impostazione predefinita, il parametro di query `auto-format` è impostato su `true`. Quando `auto-format` è abilitato (true), il sistema ignora il formato richiesto e seleziona automaticamente un formato ottimizzato per il Web (AVIF o WEBP) in base alle caratteristiche dell&#39;immagine, alle funzionalità del browser e alla [licenza-diritto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate).

Quando `auto-format` è true, il sistema distribuisce il formato immagine nella seguente sequenza:
* ***AVIF***: AVIF viene consegnato se il browser lo supporta e se la licenza lo consente. Si chiama promozione automatica.
* ***WEBP***: WEBP viene recapitato se AVIF non è supportato o concesso in licenza. Questa è anche la promozione automatica.
* ***JPEG***: JPEG viene consegnato solo quando AVIF e WEBP non sono supportati e l&#39;immagine non ha un canale alfa (trasparenza). Questa operazione viene chiamata riduzione automatica.
* ***PNG***: PNG viene consegnato quando il browser non supporta i formati moderni e l&#39;immagine dispone di un canale alfa (trasparenza). Questa operazione viene anche chiamata riduzione automatica.

Disabilitare `auto-format` impostando il parametro di query su `false`, quindi specificare il formato richiesto per la consegna dell&#39;immagine in tale formato.

### Ottimizzazione della larghezza di banda di rete{#network-bandwidth-optimisation}

Le immagini vengono ottimizzate automaticamente in base alle condizioni di rete del cliente, per garantire una distribuzione più rapida e un caricamento fluido. I parametri [Quality](#quality-parameter) e [Max-quality](#max-quality-parameter) regolano automaticamente la qualità controllando i livelli di compressione delle immagini, con valori compresi tra 1 e 100.

Vedere i seguenti comportamenti chiave di `quality` e `max-quality ` parametri:

* Se vengono specificati sia [!DNL quality] che [!DNL max-quality], [!DNL quality] ha la precedenza.
* Se si specifica solo [!DNL quality], la qualità viene distribuita indipendentemente dal tempo di caricamento in base alla velocità della rete.
* Se si specifica solo [!DNL max-quality], la qualità dell&#39;immagine viene regolata automaticamente in base alle condizioni di rete, fornendo la migliore qualità possibile fino al valore [!DNL max-quality] specificato.
* Se non viene specificato nessuno dei due, il sistema applica l&#39;ottimizzazione dinamica con `max-quality` predefinito di `85`.

#### Parametro di qualità{#quality-parameter}

Il parametro di qualità dà priorità alla qualità delle immagini rispetto alla velocità di caricamento. Corregge la qualità dell&#39;immagine di output al valore richiesto (tra 1 e 100) e ignora le condizioni di rete. Ulteriori informazioni sul [parametro di qualità](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).

#### Parametro di qualità massima{#max-quality-parameter}

La qualità massima bilancia la qualità dell&#39;immagine e il tempo di caricamento in base alla velocità della rete del cliente. Dà la priorità a tempi di caricamento più rapidi riducendo la qualità delle immagini su reti più lente, pur garantendo la qualità più elevata possibile (1-100) per le condizioni di rete specificate. Ulteriori informazioni sul parametro [max-quality](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).



