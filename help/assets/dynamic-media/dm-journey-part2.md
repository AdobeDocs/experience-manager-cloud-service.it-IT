---
title: Percorso in Dynamic Media, Parte II
description: Il Percorso Dynamic Media tratta le nozioni di base di Dynamic Media, il suo funzionamento, ciò che può fare per te e il valore che apporta al tuo lavoro e ai tuoi clienti.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---

# Percorso Dynamic Media: nozioni di base, parte II  {#dm-journey-part2}

{{see-also-dm}}

Benvenuti in Percorso Dynamic Media: nozioni di base, parte II, dove è possibile apprendere quanto segue:

* Anatomia di un URL di Dynamic Media e del modo in cui Dynamic Media distribuisce i contenuti.
* Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse.
* Set di immagini, set 360 gradi e set di file multimediali diversi.

Vedere anche [Percorso Dynamic Media; Nozioni di base, Parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Per ottenere risultati ottimali, Adobe consiglia di leggere e visualizzare questo Percorso Dynamic Media su un computer desktop.

## Anatomia di un URL di Dynamic Media e modo in cui Dynamic Media distribuisce i contenuti {#dm-journey-d}

Dopo aver caricato e pubblicato le risorse Dynamic Media, puoi copiare l’URL generato di una risorsa e incollarlo nel browser per vedere come verrà visualizzata da un cliente. Il seguente URL copiato per un’immagine di controllo viene suddiviso per colore per facilitarne la lettura e la comprensione.

![Anatomia di un URL Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomia di un URL Dynamic Media._

La prima parte dell’URL in rosso fa riferimento al dominio del server stesso. In questo caso, Dynamic Media è in esecuzione su un dominio server generico, ovvero `https://s7d1.scene7.com/is/image/`. È facile osservare un set di immagini e capire se Dynamic Media le sta servendo semplicemente osservando il dominio del server. L’URL sarà abbastanza coerente. Tuttavia, alcuni clienti Dynamic Media sono passati a un dominio server dedicato in cui potrebbe essere `name-of-your-company.scene7.com`. Per l&#39;imaging avanzato è necessario un dominio server dedicato.

Il nome dell’account è la porzione in viola. In questo caso, l&#39;account è denominato `jpearldemo`.

L&#39;ID o il nome della risorsa, `AdobeStock_28563982`, è in verde. Tieni presente che la risorsa ha l&#39;estensione _no_ come `.png` o `.jpg`. Quando le risorse vengono acquisite in Dynamic Media, l’estensione del file viene eliminata e viene creato un tipo diverso di file: un file piramidale-TIFF. La pyramic-TIFF consente a Dynamic Media di creare rapidamente rappresentazioni istantanee.

Infine, alcuni parametri di elaborazione delle immagini, `?wid=1000&fmt=jpeg&qlt=85`, sono visualizzati in giallo alla fine.

L’intero percorso URL è live. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&fmt=jpeg&qlt=85){target="_blank"}.

Con la finestra del browser ancora aperta sull’URL di Dynamic Media e sull’immagine di controllo, esaminiamo più da vicino come creare rappresentazioni dell’immagine modificando semplicemente l’URL.

### Rendering dell’immagine dell’orologio tramite l’URL

Inizia eliminando manualmente solo le regole di elaborazione delle immagini nel percorso URL; lascia il nome del server, il nome dell’account e l’ID della risorsa o il nome dell’immagine. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

Ora aggiungi un parametro di elaborazione dell’immagine alla fine dell’URL. Nel campo URL, a destra del nome dell&#39;immagine, digitare `?wid=500`, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

Viene generata una nuova rappresentazione dell’orologio. Un aspetto fondamentale di questo semplice esercizio di modifica della larghezza dell&#39;immagine è che l&#39;immagine visualizzata viene generata al 100% in modo dinamico.

Modificare il valore della larghezza di `500` pixel in `1000` pixel, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
Quando si preme **[!UICONTROL Invio]**, il browser torna al server immagini Dynamic Media. Genera una nuova rappresentazione dell’orologio, basata sul nuovo valore di larghezza appena inserito, quindi consegna la nuova immagine al browser e la memorizza in cache.

Dynamic Media dispone di numerosi parametri di elaborazione delle immagini che puoi utilizzare per ottimizzare le risorse delle immagini nelle pagine web. Puoi [visualizzarne un elenco](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=it).

Provare ora ad aggiungere un parametro di rotazione all&#39;immagine dell&#39;orologio. E la fine del percorso URL, subito dopo `wid=1000`, digitare `&rotate=90`, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&rotate=90){target="_blank"}.

L&#39;orologio è ancora leggermente inclinato verso sinistra. Modificare il valore di rotazione di `90` in `92`, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&rotate=9){target="_blank"}.

Anche in questo caso, quando si preme **[!UICONTROL Invio]**, viene generato quasi istantaneamente un nuovo rendering dell&#39;orologio. Puoi vedere il tipo di prestazioni ottenute, il che spiega perché Dynamic Media può fornire più di 800.000 richieste di immagini, _al secondo_, in un weekend intenso o in una festività importante.

Anche se è possibile modificare i parametri di elaborazione delle immagini in un URL immagine per immagine, non è un metodo efficiente, soprattutto se si dispone di decine di migliaia di immagini che compongono il sito web. Un approccio migliore consiste nell&#39;utilizzare immagini preimpostate.

## Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse {#dm-journey-e}

Esistono diversi modi e luoghi in cui desideri creare un’immagine o renderla disponibile. In genere, un Creative entra in Adobe Photoshop e salva ciascuno di questi diversi rendering come immagini statiche.

![Immagini statiche](/help/assets/dynamic-media/assets/dm-static-images.png)
_Buono: immagini statiche, ognuna creata manualmente._

Ora immaginate che il direttore Creative guardi le immagini e dica:

_&quot;Volevo davvero che questa ripresa facesse in modo che la mano grande puntasse verso le quattro e la mano piccola puntasse verso l&#39;1 per rendere più facile da vedere il quadrante dell&#39;orologio.&quot;_

Il team creativo dovrebbe riprendere tutte le nuove immagini statiche.

Tuttavia, con Dynamic Media, se disponi di diversi predefiniti per le immagini, puoi utilizzarli ovunque. I predefiniti immagine impongono gli standard.

![Approccio file primario](/help/assets/dynamic-media/assets/dm-onefile.png)
_Migliore: un file con più rappresentazioni create al volo utilizzando predefiniti immagine, ad esempio `Search_Grid` e `Thumbnail`._

| **Perché utilizzare i predefiniti immagine?** | |
|---|---|
| Standard | I predefiniti per immagini impongono un trattamento standard di elaborazione per tutte le immagini richieste. |
| Gestione delle modifiche | Se è necessario modificare l’elaborazione dell’immagine, è sufficiente modificare il parametro del predefinito immagine esistente. La definizione aggiornata viene propagata automaticamente a tutte le richieste. |

In ogni luogo in cui è necessario avere un particolare tipo di immagine, ad esempio,

* una pagina dei dettagli del prodotto,
* griglia di ricerca,
* miniatura,
* carta acquisti, oppure
* immagine protagonista

Desideri che l’immagine venga distribuita con gli stessi parametri ovunque verranno utilizzati.

Vediamo per un momento come viene creato un predefinito immagine in Dynamic Media.

![Creazione di un predefinito immagine a partire dalla scheda Base](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Creazione di un predefinito immagine a partire dalla scheda Base._

Nell&#39;esempio precedente è stato creato un nuovo predefinito immagine con il nome _Medium_. Dynamic Media utilizza un esempio di immagine preconfigurata, lo zaino, per aiutarti a visualizzare le caratteristiche del predefinito dell’immagine durante la sua creazione.

Il predefinito per immagini _Medium_ ha una larghezza di 500 pixel e un&#39;altezza di 800 pixel. Nella Parte I di questo Percorso, leggi come distribuire risorse in diversi formati. Dal menu a discesa **[!UICONTROL Formato]**, puoi scegliere di distribuire risorse come JPEG, PNG, TIFF o diversi altri formati. Avete flessibilità qui.

Se selezioni la scheda **[!UICONTROL Avanzate]**, puoi scegliere lo spazio colore della risorsa. A seconda del formato selezionato nella scheda **[!UICONTROL Base]**, nell&#39;esempio precedente è stato selezionato JPEG, è possibile distribuire le risorse in RGB, Scala di grigi o CMYK. Dal menu a discesa **[!UICONTROL Profilo colore]**, puoi selezionare come distribuire una risorsa immagine CMYK da utilizzare per la stampa. Inoltre, è possibile applicare parametri aggiuntivi per la nitidezza delle immagini. In questo caso, è stata applicata **[!UICONTROL Maschera definizione dettagli]**.

![Creazione di un predefinito immagine selezionando le opzioni dalla scheda Avanzate](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Creazione di un predefinito immagine tramite la selezione delle opzioni dalla scheda Avanzate._

Ricordi in [Anatomia di un URL Dynamic Media](#dm-journey-d), di aver letto dell&#39;URL Dynamic Media e di come è stato generato. Nella casella di testo **[!UICONTROL Modificatore immagine]** è possibile digitare qualsiasi parametro di elaborazione immagine aggiuntivo desiderato. I parametri vengono inclusi nel nome predefinito dell’URL quando le immagini vengono distribuite, utilizzando il predefinito. Nella schermata precedente è stato aggiunto il parametro `bgc=451B15`. In altre parole, è stato aggiunto un colore di sfondo marrone scuro.

Potete immaginare un predefinito immagine come una ricetta per le immagini. Fornirà sempre tutte le immagini che usano il predefinito in modo coerente; sarà sempre lo stesso. È stato aggiunto anche il parametro `&op_brightness=+10` per aumentare leggermente la luminosità.

Una volta terminato, salvate il predefinito, che ora è disponibile per tutte le immagini. In questo caso, si desidera applicare il predefinito immagine _Medium_ a un&#39;immagine di una ciotola di cioccolato liquido.

![Applicazione del predefinito immagine *Medium* per generare una rappresentazione di un&#39;immagine](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Applicazione del predefinito immagine Medium per generare una rappresentazione di un&#39;immagine._

Copiate l&#39;URL, quindi incollatelo nel browser per verificare l&#39;aspetto dell&#39;immagine. [Prova](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

Nel browser, noterai il nome del predefinito immagine _Medium_ nel percorso URL completo.

Potete vedere il tipo di chiarezza che viene visualizzata nell&#39;immagine. Questa qualità è dovuta in parte al modo in cui è stata girata la ciotola di cioccolato. Inoltre, questo accade in parte perché con Dynamic Media è possibile memorizzare immagini più grandi di quelle distribuite ai canali digitali.

Se tutto sembra soddisfacente per la tua ciotola di cioccolato, incollare l&#39;URL nelle pagine web in cui si desidera che l&#39;immagine appaia sul tuo sito web.

Se osservi di nuovo l&#39;immagine dell&#39;orologio qui sotto, noterai un predefinito immagine `Cart`, un predefinito `Grid`, un predefinito `Large`, un predefinito `PDP-page` (pagina dettagli prodotto) e molti altri.

![Predefiniti immagine statici e dinamici](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Predefiniti per immagini statiche e dinamiche. È stato eseguito il rendering dell&#39;immagine di controllo utilizzando il predefinito immagine `PDP-page`._

Ma cosa succede se devi cambiare un&#39;immagine sul tuo sito web? Si supponga, ad esempio, di aver eseguito alcuni test e di aver rilevato che l&#39;immagine di 120 x 120 (predefinito immagine `Cart`) non viene ricevuta come previsto. Per ingrandire l&#39;immagine, aumentate la larghezza a 175 pixel e l&#39;altezza a 175 pixel. In genere, è necessario accedere ad Adobe Photoshop e ricreare tutte le immagini del carrello. Tuttavia, con Dynamic Media è sufficiente modificare il predefinito immagine aggiornando i valori di Larghezza e Altezza a 175 e salvare il predefinito, come illustrato nell’esempio seguente.

![Modifica di un predefinito immagine](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Modifica della larghezza e dell&#39;altezza del predefinito immagine `Cart`._

Dopo aver modificato il predefinito immagine e aver eliminato la cache, tutte le immagini vengono aggiornate e tutti gli URL utilizzati con tale predefinito, _non_ vengono modificati in alcun punto. Ciò significa che non sono necessari collegamenti interrotti e reindirizzamenti alle pagine web.

## Set di immagini, set 360 gradi e set di file multimediali diversi {#dm-journey-f}

Alcuni degli utilizzi più comuni di Dynamic Media sono la possibilità di creare set di immagini, set 360 gradi e set di file multimediali diversi.

I set di immagini sono in genere costituiti da una serie di risorse di immagini presentate come una singola entità. Questo tipo di set offre agli utenti un’esperienza di visualizzazione integrata, in cui gli utenti possono visualizzare diverse visualizzazioni di un elemento facendo clic su un’immagine di miniatura. I set di immagini consentono di presentare viste alternative di un elemento e il visualizzatore offre strumenti di zoom per esaminare attentamente le immagini. [Visualizza un set di immagini denominato &quot;In esecuzione&quot; che utilizza il visualizzatore a comparsa](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

All’interno di Dynamic Media è possibile vedere diverse immagini di scarpe da corsa. Si tratta di una serie di linee di prodotti che i reparti vendite e marketing desiderano visualizzare come una singola presentazione, un set di immagini.

![Creazione di un set di immagini](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_Inizio della creazione di un set di immagini._

Per creare il set di immagini, scegliere **[!UICONTROL Set di immagini]** dal menu a discesa **[!UICONTROL Crea]**. Nel menu sono inoltre disponibili opzioni per creare un **[!UICONTROL set di file multimediali diversi]**, un **[!UICONTROL set 360 gradi]** e un **[!UICONTROL set carosello]**. Questi set vengono creati in modo analogo a un set di immagini.

Un set di file multimediali diversi può contenere immagini, set di campioni, set 360 gradi, video e set di video adattivi. [Prova](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Un set 360 gradi simula l&#39;atto reale di girare un oggetto per esaminarlo. I set 360 gradi consentono di visualizzare i dettagli visivi chiave da qualsiasi angolazione. [Prova](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&stagesize=500,400){target="_blank"}.

La creazione di un set di immagini è semplice. È sufficiente aggiungere le risorse immagine da includere nel set.

![Creazione di un set di immagini](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_L&#39;Editor set di immagini consente di aggiungere risorse immagine e riordinarne l&#39;aspetto nel set._

È necessario assegnare un nome al set. Scegli il nome attentamente, poiché non potrai modificarlo in un secondo momento. Nell&#39;esempio precedente, il set è denominato `Running`. Al termine, salvate il set.

Ecco l&#39;immagine `Running` impostata in Experience Manager Assets.

![Immagine in esecuzione impostata in Experience Manager Assets, vista a schede](/help/assets/dynamic-media/assets/dm-image-set.png)
_L&#39;immagine `Running` impostata in Experience Manager Assets, vista a schede._

Dopo aver creato un set di immagini, un set di file multimediali diversi, un set 360 gradi o qualsiasi altro file multimediale interattivo, vuoi vedere come si presenta e si comporta per un cliente. Dynamic Media dispone di numerosi visualizzatori incorporati che consentono di fare proprio questo.

Si inizia selezionando il set di immagini generato per aprirlo in un&#39;anteprima, come illustrato nell&#39;esempio seguente.

![Immagine in esecuzione impostata in anteprima con l&#39;opzione Visualizzatori selezionata](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_L&#39;immagine `Running` impostata nell&#39;anteprima con l&#39;opzione Visualizzatori selezionata._

Nell’anteprima puoi selezionare i campioni di scarpe da corsa e ingrandire e ridurre le scarpe. Per applicare un visualizzatore al set, selezionare **[!UICONTROL Visualizzatori]** dal menu a discesa.

![Set di immagini in esecuzione a cui è applicato il visualizzatore a comparsa](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_Set di immagini `Running` a cui è applicato il visualizzatore a comparsa._

In questo caso, è stato selezionato il visualizzatore `Flyout`. A questo punto, puoi visualizzare in anteprima il set di immagini nel visualizzatore. Tuttavia, è meglio visualizzarlo nel browser, esattamente come lo vede un cliente. Seleziona **[!UICONTROL URL]** in basso a sinistra, quindi copia l&#39;URL e incollalo nel browser. [Prova](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&config=jpearldemo/Flyout){target="_blank"}.

Il singolo URL consente di utilizzare il set di immagini e il visualizzatore nel punto desiderato sul sito web. È possibile che nell&#39;esempio precedente **[!UICONTROL Incorpora]** si trovi a destra del pulsante URL. Selezionando **[!UICONTROL Incorpora]**, puoi copiare il codice per questo set di immagini o visualizzatore e aggiungerlo a una pagina Web o a un componente Experience Manager Sites.

Il visualizzatore a comparsa è un visualizzatore predefinito le cui proprietà possono essere modificate. Oppure, come per la creazione di un predefinito immagine, puoi creare un visualizzatore personalizzato.

Ora, supponiamo che al tuo team di vendita e marketing non piaccia il visualizzatore a comparsa. Gli piace la funzione di zoom, ma vogliono che i clienti vedano l&#39;effetto zoom direttamente sopra le scarpe. In questo caso, è sufficiente applicare il visualizzatore InlineZoom al set di immagini e copiarne e incollarne l’URL nel browser per vedere come si comporta. [Prova](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&config=jpearldemo/InlineZoom){target="_blank"}.

Spostando il puntatore del mouse sulla scarpa, si ingrandisce l&#39;immagine e si visualizzano maggiori dettagli quando si sposta il puntatore. E il motivo è semplicemente la dimensione dell&#39;immagine che è stata caricata inizialmente in Dynamic Media.

Se consideriamo la vita come consumatore, o come lavori nel tuo ruolo quotidiano, e vai su siti web diversi, vedi cose come questa. Pensa a come questo viene fatto, e a come utilizzare la potenza di Dynamic Media nel tuo lavoro e sul sito web della tua azienda.

Leggi solo i set di immagini e i visualizzatori. Osserviamo un paio di altri visualizzatori e proviamoli con risorse singole. Per ripristinare il visualizzatore, fare clic sul pulsante **[!UICONTROL Aggiorna]** nell&#39;angolo inferiore sinistro.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* Visualizzatore `ZoomVertical_dark` applicato a una risorsa immagine. [Prova](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* Visualizzatore `Zoom_light` applicato a un&#39;immagine. [Prova](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&config=jpearldemo/Zoom_light){target="_blank"}.

## Facoltativo - Ulteriori informazioni

Per ulteriori informazioni su ciò che hai appena letto, utilizza i materiali riportati di seguito per approfondire i concetti. In caso contrario, il Percorso Dynamic Media è completo.

<!--
_Dynamic Media Help topics_

* [How to create image presets](/help/assets/dynamic-media/image-presets.md)
* A list of [image processing parameters](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=it) that you can use in the Image Modifier field when you create an image preset
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to create Image sets](/help/assets/dynamic-media/image-sets.md)
* [How to create Spin sets](/help/assets/dynamic-media/spin-sets.md)
* [How to create Mixed Media sets](/help/assets/dynamic-media/mixed-media-sets.md) -->

_Esercitazioni Dynamic Media_

* [Utilizza Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=it)
* [Libreria contenuti Adobe Experience Manager](https://experienceleague.adobe.com/it?lang=en#recommended/solutions/experience-manager) (ricerca in _Dynamic Media_)

_Visualizzatori Dynamic Media_

* [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) di ogni visualizzatore

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->