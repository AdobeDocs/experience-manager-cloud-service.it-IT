---
title: Percorso in Dynamic Medie, Parte II
description: Il Percorso Dynamic Medie illustra le nozioni di base di Dynamic Medie, il suo funzionamento, il suo potenziale vantaggio e il valore che apporta al lavoro e ai clienti.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '2872'
ht-degree: 0%

---

# Percorso Dynamic Medie: nozioni di base, parte II  {#dm-journey-part2}

Benvenuti nel Percorso Dynamic Medie: Nozioni di base, parte II, dove è possibile aspettarsi di apprendere quanto segue:

* Anatomia di un URL Dynamic Medie e modo in cui Dynamic Medie distribuisce i contenuti
* Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse
* Set di immagini, set 360 gradi e set di file multimediali diversi

Vedi anche [Percorso Dynamic Medie; nozioni di base, parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Per ottenere risultati ottimali, l&#39;Adobe consiglia di leggere e visualizzare questo Percorso Dynamic Medie su un computer desktop.

## Anatomia di un URL Dynamic Medie e modo in cui Dynamic Medie distribuisce i contenuti {#dm-journey-d}

Dopo aver caricato e pubblicato le risorse Dynamic Medie, puoi copiare l’URL generato di una risorsa e incollarlo nel browser per vedere come verrà visualizzata da un cliente. Il seguente URL copiato per un’immagine di controllo viene suddiviso per colore per facilitarne la lettura e la comprensione.

![Anatomia di un URL Dynamic Medie](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomia di un URL Dynamic Medie._

La prima parte dell’URL in rosso fa riferimento al dominio del server stesso. In questo caso, Dynamic Medie è in esecuzione su un dominio server generico `https://s7d1.scene7.com/is/image/`. È facile osservare un insieme di immagini e capire se Dynamic Medie le sta servendo semplicemente osservando il dominio del server. L’URL sarà abbastanza coerente. Tuttavia, alcuni clienti di Dynamic Medie sono passati a un dominio server dedicato in cui potrebbe `name-of-your-company.scene7.com`. Per l&#39;imaging avanzato è necessario un dominio server dedicato.

Il nome dell’account è la porzione in viola. In questo caso, l’account viene chiamato `jpearldemo`.

ID o nome della risorsa, `AdobeStock_28563982` è in verde. Tieni presente che la risorsa ha _no_ estensione file come `.png` o `.jpg`. Quando le risorse vengono acquisite in Dynamic Medie, l’estensione del file viene eliminata e viene creato un tipo diverso di file: un file piramidale-TIFF. Il pyramic-TIFF consente a Dynamic Medie di creare rapidamente copie trasformate in tempo reale.

E infine, ci sono alcuni parametri di elaborazione dell&#39;immagine, `?wid=1000&fmt=jpeg&qlt=85`, visualizzato in giallo alla fine.

L’intero percorso URL è live. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}.

Con la finestra del browser ancora aperta all’URL di Dynamic Medie e all’immagine di controllo, esaminiamo più da vicino come creare rappresentazioni dell’immagine modificando semplicemente l’URL.

### Rendering dell’immagine dell’orologio tramite l’URL

Inizia eliminando manualmente solo le regole di elaborazione delle immagini nel percorso URL; lascia il nome del server, il nome dell’account e l’ID della risorsa o il nome dell’immagine. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

Ora aggiungi un parametro di elaborazione dell’immagine alla fine dell’URL. Nel campo URL, a destra del nome dell’immagine, digita `?wid=500`, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

Viene generata una nuova rappresentazione dell’orologio. Un aspetto fondamentale di questo semplice esercizio di modifica della larghezza dell&#39;immagine è che l&#39;immagine visualizzata viene generata al 100% in modo dinamico.

Ora modifica il valore della larghezza di `500` pixel a `1000` pixel, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
Nel momento in cui premi **[!UICONTROL Invio]**, il browser torna al server immagini Dynamic Medie. Genera una nuova rappresentazione dell’orologio, basata sul nuovo valore di larghezza appena inserito, quindi consegna la nuova immagine al browser e la memorizza in cache.

Dynamic Medie dispone di numerosi parametri di elaborazione delle immagini che puoi utilizzare per ottimizzare le risorse delle immagini nelle pagine web. È possibile [consulta un elenco](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

Provare ora ad aggiungere un parametro di rotazione all&#39;immagine dell&#39;orologio. E la fine del percorso URL, immediatamente successivo `wid=1000`, tipo `&rotate=90`, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target="_blank"}.

L&#39;orologio è ancora leggermente inclinato verso sinistra. Modificare il valore di rotazione di `90` a `92`, quindi premere **[!UICONTROL Invio]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}.

Di nuovo, nel momento in cui premi **[!UICONTROL Invio]**, viene generata quasi istantaneamente una nuova rappresentazione dell’orologio. Potete vedere il tipo di prestazioni che ottenete, il che spiega perché Dynamic Medie può fornire più di 800.000 richieste di immagini, _al secondo_, in un weekend intenso o in una festività importante.

Anche se è possibile modificare i parametri di elaborazione delle immagini in un URL immagine per immagine, non è un metodo efficiente, soprattutto se si dispone di decine di migliaia di immagini che compongono il sito web. Un approccio migliore consiste nell&#39;utilizzare immagini preimpostate.

## Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse {#dm-journey-e}

Esistono diversi modi e luoghi in cui desideri creare un’immagine o renderla disponibile. In genere, i contenuti creativi vengono inseriti in Adobe Photoshop e salvano ciascuna di queste diverse rappresentazioni come immagini statiche.

![Immagini statiche](/help/assets/dynamic-media/assets/dm-static-images.png)
_Corretto: immagini statiche, ciascuna creata manualmente._

Ora immaginate che Creative Director guardi le immagini e dica:

_&quot;Volevo davvero effettuare questa ripresa in modo che la mano grande indicasse le quattro e la mano piccola indicasse l&#39;1 per rendere più facile da vedere il quadrante dell&#39;orologio.&quot;_

Il team creativo dovrebbe riprendere tutte le nuove immagini statiche.

Ma con Dynamic Medie, se avete predefiniti di immagine diversi, potete usarli ovunque. I predefiniti immagine impongono gli standard.

![Approccio basato sul file principale](/help/assets/dynamic-media/assets/dm-onefile.png)
_Migliore: un file con più rappresentazioni create al volo utilizzando predefiniti per immagini, ad esempio `Search_Grid` e `Thumbnail`._

| **Perché utilizzare i predefiniti per immagini?** | |
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

Vediamo per un momento come viene creato un predefinito immagine in Dynamic Medie.

![Creazione di un predefinito immagine a partire dalla scheda Base](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Creazione di un predefinito immagine a partire dalla scheda Base._

Nell’esempio precedente, puoi vedere che è stato creato un nuovo predefinito immagine con il nome _Medio_. Dynamic Medie utilizza un esempio di immagine preconfigurata, lo zaino, per aiutarti a visualizzare le caratteristiche del predefinito dell&#39;immagine durante la sua creazione.

Il _Medio_ il predefinito per immagini ha una larghezza di 500 pixel e un&#39;altezza di 800 pixel. Nella Parte I di questo Percorso, leggi come distribuire risorse in diversi formati. Dalla sezione **[!UICONTROL Formato]** menu a discesa, puoi scegliere di distribuire risorse come JPEG, PNG, TIFF o in diversi altri formati. Avete flessibilità qui.

Selezione del **[!UICONTROL Avanzate]** Questa scheda ti offre le opzioni per lo spazio colore della risorsa. A seconda del formato selezionato in **[!UICONTROL Base]** nell’esempio precedente, era selezionato JPEG . Puoi distribuire le risorse in RGB, Gradazioni di grigio o CMYK. Dalla sezione **[!UICONTROL Profilo colore]** menu a discesa, puoi selezionare come distribuire una risorsa immagine CMYK da utilizzare per la stampa. Inoltre, è possibile applicare parametri aggiuntivi per la nitidezza delle immagini. In questo caso, **[!UICONTROL Maschera definizione dettagli]** è stato applicato.

![Creazione di un predefinito immagine selezionando le opzioni dalla scheda Avanzate](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Per creare un predefinito immagine, seleziona le opzioni dalla scheda Avanzate._

Ricordi in [Anatomia di un URL Dynamic Medie](#dm-journey-d) in precedenza, hai letto dell’URL di Dynamic Medie e di come viene creato. Il **[!UICONTROL Modificatore immagine]** è la casella di testo in cui è possibile digitare qualsiasi parametro di elaborazione immagine aggiuntivo desiderato. I parametri vengono inclusi nel nome predefinito dell’URL quando le immagini vengono distribuite, utilizzando il predefinito. Nella schermata precedente, il parametro `bgc=451B15` è stato aggiunto. In altre parole, è stato aggiunto un colore di sfondo marrone scuro.

Potete immaginare un predefinito immagine come una ricetta per le immagini. Fornirà sempre tutte le immagini che usano il predefinito in modo coerente; sarà sempre lo stesso. Il parametro `&op_brightness=+10` per aumentare leggermente la luminosità.

Una volta terminato, salvate il predefinito, che ora è disponibile per tutte le immagini. In questo caso, vogliamo applicare la _Medio_ predefinito immagine di un&#39;immagine di una ciotola di cioccolato liquido.

![Applicazione del predefinito immagine *Medio* per generare una rappresentazione di un&#39;immagine](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Applicazione del predefinito immagine Media per generare una rappresentazione di un&#39;immagine._

Copiate l&#39;URL, quindi incollatelo nel browser per verificare l&#39;aspetto dell&#39;immagine. [Prova](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

Nel browser, notate il nome del predefinito immagine _Medio_ nel percorso URL completo.

Potete vedere il tipo di chiarezza che viene visualizzata nell&#39;immagine. Questa qualità è dovuta in parte al modo in cui è stata girata la ciotola di cioccolato. Inoltre, ciò è dovuto in parte al fatto che con Dynamic Medie è possibile archiviare immagini di dimensioni maggiori rispetto a quelle distribuite ai canali digitali.

Se tutto sembra soddisfacente per la tua ciotola di cioccolato, incollare l&#39;URL nelle pagine web in cui si desidera che l&#39;immagine appaia sul tuo sito web.

Se osservi nuovamente l’immagine dell’orologio qui sotto, noterai che è presente un `Cart` predefinito immagine, un `Grid` predefinito, un `Large` predefinito, un `PDP-page` (Product Detail Page) e molti altri.

![Predefiniti per immagini statiche e dinamiche](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Predefiniti per immagini statiche e dinamiche. L’immagine dell’orologio è stata riprodotta utilizzando `PDP-page` predefinito immagine._

Ma cosa succede se devi cambiare un&#39;immagine sul tuo sito web? Si supponga, ad esempio, di aver eseguito alcuni test e di aver rilevato che l&#39;immagine di 120 x 120 `Cart` predefinito immagine) non viene ricevuto come pensavi. Per ingrandire l&#39;immagine, aumentate la larghezza a 175 pixel e l&#39;altezza a 175 pixel. In genere, è necessario accedere ad Adobe Photoshop e ricreare tutte le immagini del carrello. Con Dynamic Medie, invece, è sufficiente modificare il predefinito immagine aggiornando i valori di Larghezza e Altezza a 175 e salvare il predefinito, come mostrato nell’esempio seguente.

![Modifica di un predefinito immagine](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Modifica della larghezza e dell’altezza del `Cart` predefinito immagine._

Dopo aver modificato il predefinito immagine e aver eliminato la cache, tutte le immagini vengono aggiornate e tutti gli URL utilizzati con tale predefinito, esegui _non_ cambiate ovunque. Ciò significa che non sono necessari collegamenti interrotti e reindirizzamenti alle pagine web.

## Set di immagini, set 360 gradi e set di file multimediali diversi {#dm-journey-f}

Alcuni degli utilizzi più comuni di Dynamic Medie è la possibilità di creare set di immagini, set 360 gradi e set di file multimediali diversi.

I set di immagini sono in genere costituiti da una serie di risorse di immagini presentate come una singola entità. Questo tipo di set offre agli utenti un’esperienza di visualizzazione integrata, in cui gli utenti possono visualizzare diverse visualizzazioni di un elemento facendo clic su un’immagine di miniatura. I set di immagini consentono di presentare viste alternative di un elemento e il visualizzatore offre strumenti di zoom per esaminare attentamente le immagini. [Visualizzare un set di immagini denominato &quot;In esecuzione&quot; che utilizza il visualizzatore a comparsa](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Qui in Dynamic Medie potete vedere diverse immagini di scarpe da corsa. Si tratta di una serie di linee di prodotti che i reparti vendite e marketing desiderano visualizzare come una singola presentazione, un set di immagini.

![Creazione di un set di immagini](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_Inizio della creazione di un set di immagini._

Per creare il set di immagini, scegli **[!UICONTROL Set immagini]** dal **[!UICONTROL Crea]** menu a discesa. Si noti che sono disponibili anche opzioni per la creazione di un **[!UICONTROL Set di file multimediali diversi]**, a **[!UICONTROL Set 360 gradi]**, e un **[!UICONTROL Set carosello]**. Questi set vengono creati in modo analogo a un set di immagini.

Un set di file multimediali diversi può contenere immagini, set di campioni, set 360 gradi, video e set di video adattivi. [Prova](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Un set 360 gradi simula l&#39;atto reale di girare un oggetto per esaminarlo. I set 360 gradi consentono di visualizzare i dettagli visivi chiave da qualsiasi angolazione. [Prova](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}.

La creazione di un set di immagini è semplice. È sufficiente aggiungere le risorse immagine da includere nel set.

![Creazione di un set di immagini](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_L’Editor set di immagini consente di aggiungere risorse immagine e di riordinarne l’aspetto nel set._

È necessario assegnare un nome al set. Scegli il nome attentamente, poiché non potrai modificarlo in un secondo momento. Nell’esempio precedente, il set è denominato `Running`. Al termine, salvate il set.

Ed ecco il `Running` Set di immagini in Experience Manager Assets.

![Immagine in esecuzione impostata in Experience Manager Assets, Vista a schede](/help/assets/dynamic-media/assets/dm-image-set.png)
_Il `Running` Immagine impostata in Experience Manager Assets, Vista a schede._

Dopo aver creato un set di immagini, un set di file multimediali diversi, un set 360 gradi o qualsiasi altro file multimediale interattivo, vuoi vedere come si presenta e si comporta per un cliente. Dynamic Medie dispone di numerosi visualizzatori incorporati che permettono di fare proprio questo.

Si inizia selezionando il set di immagini generato per aprirlo in un&#39;anteprima, come illustrato nell&#39;esempio seguente.

![Immagine in esecuzione impostata in anteprima con l&#39;opzione Visualizzatori selezionata](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_Il `Running` Immagine impostata in anteprima con l&#39;opzione Visualizzatori selezionata._

Nell’anteprima puoi selezionare i campioni di scarpe da corsa e ingrandire e ridurre le scarpe. Per applicare un visualizzatore al set, seleziona **[!UICONTROL Visualizzatori]** dal menu a discesa.

![Set di immagini in esecuzione a cui è applicato il visualizzatore a comparsa](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_Il `Running` Set di immagini con il visualizzatore a comparsa applicato._

In questo caso, il `Flyout` visualizzatore selezionato. A questo punto, puoi visualizzare in anteprima il set di immagini nel visualizzatore. Tuttavia, è meglio visualizzarlo nel browser, esattamente come lo vede un cliente. Selezione effettuata **[!UICONTROL URL]** in basso a sinistra, copia l’URL e incollalo nel browser. [Prova](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}.

Il singolo URL consente di utilizzare il set di immagini e il visualizzatore nel punto desiderato sul sito web. Nell’esempio precedente, potresti aver notato che **[!UICONTROL Incorpora]** si trova a destra del pulsante URL. Selezionando **[!UICONTROL Incorpora]**, è possibile copiare il codice per questo set di immagini/visualizzatore e aggiungerlo a una pagina web o a un componente Experience Manager Sites.

Il visualizzatore a comparsa è un visualizzatore predefinito le cui proprietà possono essere modificate. Oppure, come per la creazione di un predefinito immagine, puoi creare un visualizzatore personalizzato.

Ora, supponiamo che al tuo team di vendita e marketing non piaccia il visualizzatore a comparsa. Gli piace la funzione di zoom, ma vogliono che i clienti vedano l&#39;effetto zoom direttamente sopra le scarpe. In questo caso, è sufficiente applicare il visualizzatore InlineZoom al set di immagini e copiarne e incollarne l’URL nel browser per vedere come si comporta. [Prova](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}.

Spostando il puntatore del mouse sulla scarpa, si ingrandisce l&#39;immagine e si visualizzano maggiori dettagli quando si sposta il puntatore. E il motivo è semplicemente la dimensione dell&#39;immagine che è stata caricata inizialmente in Dynamic Medie.

Se consideriamo la vita come consumatore, o come lavori nel tuo ruolo quotidiano, e vai su siti web diversi, vedi cose come questa. Pensate a come viene fatto, e come potete usare la potenza di Dynamic Medie nel vostro lavoro e sul sito web della vostra azienda.

Leggi solo i set di immagini e i visualizzatori. Osserviamo un paio di altri visualizzatori e proviamoli con risorse singole. Per reimpostare il visualizzatore, fare clic su **[!UICONTROL Aggiorna]** nell&#39;angolo inferiore sinistro.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` visualizzatore applicato a una risorsa immagine. [Prova](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* `Zoom_light` visualizzatore applicato a un&#39;immagine. [Prova](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}.

## Facoltativo - Ulteriori informazioni

Per ulteriori informazioni su ciò che hai appena letto, utilizza i materiali riportati di seguito per approfondire i concetti. In caso contrario, il Percorso Dynamic Medie è completo.

_Argomenti della Guida di Dynamic Medie_

* [Creare predefiniti immagine](/help/assets/dynamic-media/image-presets.md)
* Un elenco di [parametri di elaborazione delle immagini](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) che potete utilizzare nel campo Modificatore immagine quando create un predefinito immagine
* [Visualizzare in anteprima le risorse](/help/assets/dynamic-media/previewing-assets.md)
* [Visualizzare in anteprima le risorse 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Come creare set di immagini](/help/assets/dynamic-media/image-sets.md)
* [Come creare i set 360 gradi](/help/assets/dynamic-media/spin-sets.md)
* [Come creare set di file multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md)

_Tutorial su Dynamic Medie_

* [Utilizzare Dynamic Medie con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=it)
* [Libreria di contenuti Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (ricerca il _Dynamic Medie_)

_Visualizzatori Dynamic Medie_

* [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) di ogni visualizzatore

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->