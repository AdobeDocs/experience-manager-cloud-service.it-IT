---
title: Percorso in Dynamic Media, parte II
description: Il Percorso Dynamic Media illustra le nozioni di base di Dynamic Media, il suo funzionamento, le sue funzioni e il suo valore per il tuo lavoro e per i tuoi clienti.
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
source-git-commit: 9202cf44595070c98ca3d21887dff257bcd88b87
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 0%

---

# percorso Dynamic Media: Nozioni di base, parte II  {#dm-journey-part2}

Benvenuto nel Percorso Dynamic Media: Nozioni di base, parte II, in cui ti aspetti di imparare quanto segue:

* Anatomia di un URL Dynamic Media e modalità di distribuzione dei contenuti da parte di Dynamic Media
* Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse
* Set di immagini, set 360 gradi e set di file multimediali diversi

Vedi anche [percorso Dynamic Media; Nozioni di base, parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Per ottenere risultati ottimali, Adobe consiglia di leggere e visualizzare questo Percorso Dynamic Media su un computer desktop.

## Anatomia di un URL Dynamic Media e modalità di distribuzione dei contenuti da parte di Dynamic Media {#dm-journey-d}

Dopo aver caricato e pubblicato le risorse Dynamic Media, puoi copiare l’URL generato di una risorsa e incollarlo nel browser per vedere come apparirà la risorsa a un cliente. Il seguente URL copiato per un’immagine orologio è suddiviso per colore per facilitare la lettura e la comprensione.

![Anatomia di un URL Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomia di un URL Dynamic Media._

La prima parte dell’URL in rosso fa riferimento al dominio del server stesso. In questo caso, Dynamic Media è in esecuzione su un dominio server generico, ovvero `https://s7d1.scene7.com/is/image/`. È facile guardare un set di immagini e capire se vengono servite da Dynamic Media solo guardando il dominio del server. L’URL sarà abbastanza coerente. Tuttavia, alcuni clienti Dynamic Media hanno effettuato il passaggio a un dominio server dedicato in cui potrebbe essere `name-of-your-company.scene7.com`. Per Smart imaging è necessario un dominio server dedicato.

Il nome dell&#39;account è la porzione in viola. In questo caso, l’account viene chiamato `jpearldemo`.

ID o nome della risorsa, `AdobeStock_28563982` è in verde. Tieni presente che la risorsa ha _no_ estensione di file, ad esempio `.png` o `.jpg`. Quando le risorse vengono acquisite in Dynamic Media, l’estensione del file viene rimossa e viene creato un tipo diverso di file: un file piramidale-TIFF. Il TIFF piramidale consente a Dynamic Media di creare rapidamente rappresentazioni on-the-fly.

Infine, ci sono alcuni parametri di elaborazione delle immagini, `?wid=1000&fmt=jpeg&qlt=85`, in giallo alla fine.

L’intero percorso URL è live. [Provate](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target=&quot;_blank&quot;}.

Con la finestra del browser ancora aperta all’URL Dynamic Media e all’immagine Watch, cerchiamo di vedere più da vicino come creare rappresentazioni dell’immagine semplicemente modificando l’URL.

### Rendering dell’immagine dell’orologio tramite l’URL

Per iniziare, elimina manualmente solo le regole di elaborazione dell’immagine nel percorso URL; lascia il nome del server, il nome dell’account e l’ID della risorsa o il nome dell’immagine. [Provate](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target=&quot;_blank&quot;}.

Ora aggiungi un parametro di elaborazione dell’immagine alla fine dell’URL. Nel campo URL, a destra del nome dell’immagine, digita `?wid=500`, quindi premi **[!UICONTROL Invio]**. [Provate](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target=&quot;_blank&quot;}.

Si noti che viene generata una nuova rappresentazione dell’orologio. Un elemento fondamentale da capire da questo semplice esercizio di modifica della larghezza dell&#39;immagine, è che l&#39;immagine visualizzata è generata al 100% in modo dinamico.

Ora modifica il valore della larghezza di `500` pixel a `1000` pixel, quindi premere **[!UICONTROL Invio]**. [Provate](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target=&quot;_blank}.
Il momento in cui premi **[!UICONTROL Invio]**, il browser torna al server di immagini Dynamic Media. Genera una nuova rappresentazione dell’orologio, basata sul nuovo valore di larghezza appena inserito, quindi restituisce la nuova immagine al browser e la memorizza in cache.

Dynamic Media dispone di numerosi parametri di elaborazione delle immagini che è possibile utilizzare per perfezionare le risorse delle immagini sulle pagine web. È possibile [consulta qui un elenco](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

Ora prova ad aggiungere un parametro di rotazione all&#39;immagine dell&#39;orologio. E la fine del percorso URL, subito dopo `wid=1000`, tipo `&rotate=90`, quindi premere **[!UICONTROL Invio]**. [Provate](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target=&quot;_blank&quot;}.

L&#39;orologio è ancora leggermente inclinato a sinistra. Modifica il valore di rotazione di `90` a `92`, quindi premere **[!UICONTROL Invio]**. [Provate](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target=&quot;_blank&quot;}.

Di nuovo, quando premete **[!UICONTROL Invio]**, una nuova rappresentazione dell’orologio viene generata quasi istantaneamente. Potete vedere il tipo di prestazioni che ottenete, che spiega perché Dynamic Media può fornire più di 800.000 richieste di immagini, _al secondo_, in un weekend occupato, o una vacanza importante.

Anche se è possibile modificare i parametri di elaborazione delle immagini in un URL a livello di immagine per immagine, non è un metodo efficiente, soprattutto se si dispone di decine di migliaia di immagini che compongono il tuo sito web. Un approccio molto migliore consiste nell’utilizzare i predefiniti per immagini.

## Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse {#dm-journey-e}

Esistono diversi modi e luoghi in cui desideri creare un’immagine o rendere disponibile un’immagine. Tradizionalmente, un creativo entra in Adobe Photoshop e salva ognuna di queste diverse rappresentazioni come immagini statiche.

![Immagini statiche](/help/assets/dynamic-media/assets/dm-static-images.png)
_Buono: immagini statiche, ciascuna creata manualmente._

Immaginate ora che il Creative Director guardi le immagini e dica:

_&quot;Volevo questa ripresa in modo che la mano grande puntasse verso i quattro, e la mano piccola puntasse verso il 1 per rendere il quadrante dell&#39;orologio più facile da vedere.&quot;_

Il creativo dovrebbe riprendere tutte queste nuove immagini statiche.

Tuttavia, con Dynamic Media, se hai diversi predefiniti per immagini, puoi usarli ovunque ne hai bisogno. I predefiniti per immagini applicano gli standard.

![Approccio principale dei file](/help/assets/dynamic-media/assets/dm-onefile.png)
_Migliore: un file con più rappresentazioni create al volo utilizzando predefiniti per immagini, ad esempio `Search_Grid` e `Thumbnail`._

| **Perché utilizzare i predefiniti immagine?** |  |
|---|---|
| Standard | I predefiniti immagine applicano un trattamento standard di elaborazione delle immagini su qualsiasi immagine con cui viene richiesto. |
| Gestione delle modifiche | Se devi modificare l’elaborazione dell’immagine, è sufficiente modificare il parametro del predefinito per immagini esistente. La definizione aggiornata viene propagata automaticamente a tutte le richieste. |

Ogni luogo in cui è necessario avere un particolare tipo di immagine, ad esempio:

* una pagina dettagliata del prodotto,
* griglia di ricerca,
* miniatura,
* carta commerciale, oppure
* immagine protagonista

L’immagine deve essere consegnata con gli stessi parametri ovunque vengano utilizzati.

Per un momento, vediamo come viene creato un predefinito per immagini in Dynamic Media.

![Creazione di un predefinito per immagini a partire dalla scheda Base](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Creazione di un predefinito per immagini a partire dalla scheda Base ._

Nell’esempio precedente, puoi vedere che è stato creato un nuovo predefinito per immagini con il nome _Media_. Dynamic Media utilizza un esempio di immagine preconfigurata, lo zaino, per consentirti di vedere le caratteristiche del predefinito immagine quando lo crei.

La _Media_ immagine preimpostata ha una larghezza di 500 pixel e un&#39;altezza di 800 pixel. Nella parte I di questo Percorso, leggi come consegnare risorse in diversi formati. Da **[!UICONTROL Formato]** menu a discesa, puoi scegliere di distribuire le risorse come JPEG, PNG, TIFF o diversi altri formati. Qui c&#39;è flessibilità.

Selezione della **[!UICONTROL Avanzate]** La scheda ti offre le opzioni per lo spazio colore della risorsa. A seconda del formato selezionato nella **[!UICONTROL Base]** scheda : nell’esempio precedente, è stato selezionato JPEG; è possibile distribuire le risorse in RGB, Scala di grigio o CMYK. Da **[!UICONTROL Profilo colore]** menu a discesa, puoi selezionare come distribuire una risorsa immagine CMYK da utilizzare per la stampa. Tieni presente che sono disponibili parametri aggiuntivi da applicare per la nitidezza delle immagini. In questo caso, **[!UICONTROL Maschera definizione dettagli]** è stato applicato.

![Creazione di un predefinito per immagini selezionando le opzioni dalla scheda Avanzate](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Creazione di un predefinito per immagini selezionando le opzioni dalla scheda Avanzate ._

Ti ricordi di [Anatomia di un URL Dynamic Media](#dm-journey-d) prima, leggi l’URL di Dynamic Media e la relativa modalità di creazione. La **[!UICONTROL Modificatore immagine]** nella casella di testo è possibile digitare tutti i parametri di elaborazione immagine desiderati. I parametri vengono inclusi nel nome predefinito dell&#39;URL quando le immagini vengono consegnate, utilizzando il predefinito. Nella schermata precedente, il parametro `bgc=451B15` è stato aggiunto. In altre parole, è stato aggiunto un colore di sfondo marrone scuro.

È possibile considerare un predefinito per immagini come una ricetta per le immagini. Fornirà tutte le immagini che utilizzano il preset, in modo costante, ogni volta; sarà lo stesso. Il parametro `&op_brightness=+10` è stato aggiunto anche per aumentare leggermente la luminosità.

Al termine, salvi il predefinito ed è ora disponibile per tutte le immagini in tuo possesso. In questo caso, vogliamo applicare il _Media_ immagine preimpostata su un&#39;immagine di una ciotola di cioccolato liquido.

![Applicazione del predefinito per immagini *Media* per generare un rendering di un’immagine](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Applicazione del predefinito per immagini Media per generare un rendering di un’immagine._

Copia l’URL, quindi incollalo nel browser per controllare l’aspetto dell’immagine. [Provate](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target=&quot;_blank&quot;}.

Nel browser, noterai il nome del predefinito per immagini _Media_ nel percorso URL completo.

Potete vedere il tipo di chiarezza che viene visualizzata nell&#39;immagine. Questa qualità è in parte dovuta al modo in cui è stata girata la ciotola di cioccolato. Inoltre, in parte perché con Dynamic Media è possibile archiviare immagini più grandi di quelle consegnate ai canali digitali.

Se tutto sembra soddisfacente per la tua ciotola di cioccolato, incolla l&#39;URL nelle tue pagine web in cui vuoi che l&#39;immagine appaia sul tuo sito web.

Se guardi di nuovo l&#39;immagine dell&#39;orologio qui sotto, puoi vedere che c&#39;è un `Cart` predefinito per immagini, `Grid` preimpostazione, un `Large` preimpostazione, un `PDP-page` (Pagina dettagli prodotto) e molti altri.

![Predefiniti immagine statici e dinamici](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Predefiniti immagine statici e dinamici. L’immagine dell’orologio è stata riprodotta utilizzando l’ `PDP-page` predefinito immagine._

Ma cosa succede se devi cambiare un&#39;immagine sul tuo sito web? Ad esempio, supponi di aver effettuato alcuni test e di aver rilevato che l&#39;immagine di 120 x 120 (il `Cart` immagine preimpostata) non viene ricevuto come si pensava. È necessario ingrandire l’immagine aumentando la larghezza a 175 pixel e aumentando l’altezza a 175 pixel. Tradizionalmente, bisognerebbe andare in Adobe Photoshop e ricreare tutte quelle immagini del carrello. Ma con Dynamic Media, è sufficiente modificare il predefinito immagine aggiornando i valori di Larghezza e Altezza a 175 e salvare il predefinito, come mostrato nell&#39;esempio seguente.

![Modifica di un predefinito per immagini](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Modifica della larghezza e dell’altezza del `Cart` predefinito immagine._

Dopo aver modificato il predefinito per immagini e aver svuotato la cache, tutte le immagini vengono aggiornate e tutti gli URL utilizzati con quel predefinito, fanno _not_ cambia ovunque. Ciò significa che non sono necessari collegamenti interrotti e nessun reindirizzamento di pagine web.

## Set di immagini, set 360 gradi e set di file multimediali diversi {#dm-journey-f}

Alcuni degli usi più comuni di Dynamic Media sono la possibilità di creare set di immagini, set 360 gradi e set di file multimediali diversi.

I set di immagini sono in genere costituiti da una serie di risorse di immagini presentate come una singola entità. Questo tipo di set offre agli utenti un’esperienza di visualizzazione integrata, in cui gli utenti possono vedere diverse visualizzazioni di un elemento facendo clic su una miniatura. I set di immagini consentono di presentare viste alternative di qualcosa e il visualizzatore offre strumenti di zoom per esaminare attentamente le immagini. [Visualizzare un set di immagini denominato &quot;In esecuzione&quot; che utilizza il visualizzatore a comparsa](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Qui in Dynamic Media potete vedere diverse immagini di scarpe da corsa. È una serie di linee di prodotti che le vendite e il marketing desiderano che i clienti visualizzino come una singola presentazione; un set di immagini.

![Creazione di un set di immagini](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_L&#39;inizio della creazione di un set di immagini._

Per creare il set di immagini, scegliete **[!UICONTROL Set di immagini]** dal **[!UICONTROL Crea]** menu a discesa. Nel menu sono inoltre disponibili opzioni per creare un **[!UICONTROL Set di file multimediali diversi]**, **[!UICONTROL Set 360 gradi]** e **[!UICONTROL Set carosello]**. I set vengono creati nello stesso modo di un set di immagini.

Un set di file multimediali diversi può contenere immagini, set di campioni, set 360 gradi, video e set di video adattivi. [Provate](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Un set 360 gradi simula l’atto reale di trasformare un oggetto per esaminarlo. I set 360 gradi consentono di visualizzare i dettagli visivi principali da qualsiasi angolo. [Provate](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target=&quot;_blank&quot;}.

La creazione di un set di immagini è semplice. È sufficiente aggiungere le risorse immagine da includere nel set.

![Creazione di un set di immagini](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_L’Editor set di immagini consente di aggiungere risorse immagine e riordinarne l’aspetto nel set._

È necessario assegnare un nome al set. Scegli attentamente il nome perché non potrai modificarlo in un secondo momento! Nell’esempio precedente, il set è chiamato `Running`. Al termine, salva il set.

Ed ecco la `Running` Set di immagini in Experience Manager Assets.

![Set di immagini in esecuzione in Experience Manager Assets, Vista a schede](/help/assets/dynamic-media/assets/dm-image-set.png)
_La `Running` Set di immagini in Experience Manager Assets, Vista a schede._

Dopo aver creato un set di immagini, un set di file multimediali diversi, un set 360 gradi o qualsiasi altro supporto interattivo, è necessario vedere come appare e si comporta per un cliente. Dynamic Media dispone di numerosi visualizzatori integrati che consentono di farlo.

Per iniziare, seleziona il set di immagini generato per aprirlo in un’anteprima, come illustrato nell’esempio seguente.

![Il set di immagini in esecuzione nell’anteprima con l’opzione Visualizzatori selezionata](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_La `Running` Set di immagini in anteprima con l’opzione Visualizzatori selezionata._

Nell’anteprima è possibile selezionare i campioni delle scarpe da corsa e ingrandire e ridurre le scarpe. Per applicare un visualizzatore al set, seleziona **[!UICONTROL Visualizzatori]** dal menu a discesa.

![Set di immagini in esecuzione con il visualizzatore a comparsa applicato](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_La `Running` Set di immagini con il visualizzatore a comparsa applicato._

In questo caso, il `Flyout` visualizzatore selezionato. A questo punto, puoi visualizzare in anteprima il set di immagini nel visualizzatore. Ma è meglio visualizzarlo nel browser, come lo vede un cliente. Seleziona **[!UICONTROL URL]** in basso a sinistra, quindi copia l’URL e incollalo nel browser. [Provate](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target=&quot;_blank&quot;}.

L’URL singolo consente di utilizzare il set di immagini e il visualizzatore in cui sono necessari sul sito web. Nell&#39;esempio precedente si può notare che **[!UICONTROL Incorpora]** è a destra del pulsante URL. Selezionando **[!UICONTROL Incorpora]**, puoi copiare il codice per questo set di immagini/visualizzatore e aggiungerlo a una pagina web o a un componente Experience Manager Sites.

Il visualizzatore a comparsa è un visualizzatore predefinito predefinito di cui è possibile modificare le proprietà. Oppure, proprio come per la creazione di un predefinito per immagini, puoi creare un visualizzatore personalizzato.

Ora, supponendo che al tuo team di vendita e marketing non piaccia il visualizzatore a comparsa. Gli piace la funzione di zoom, ma i clienti vogliono vedere l&#39;effetto di zoom direttamente sulle scarpe. In questo caso, è sufficiente applicare il visualizzatore InlineZoom al set di immagini e copiare e incollare il suo URL nel browser per vedere come si comporta. [Provate](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target=&quot;_blank&quot;}.

Quando si sposta il puntatore del mouse sulla scarpa, si ingrandisce l&#39;immagine e si possono vedere più dettagli mentre si sposta il puntatore. E il motivo è semplicemente la dimensione dell&#39;immagine che è stata inizialmente caricata in Dynamic Media.

Quando consideri di vivere come un consumatore, o come lavori nel tuo ruolo quotidiano, e mentre vai su siti web diversi, vedi cose come questa. Pensa a come si sta facendo e a come puoi usare la potenza di Dynamic Media nel tuo lavoro e sul sito web della tua azienda.

Leggete un po&#39; i set di immagini e i visualizzatori. Diamo un&#39;occhiata ad un paio di altri visualizzatori e proviamoli su singole risorse. Per reimpostare il visualizzatore, fai clic sul pulsante **[!UICONTROL Aggiorna]** nell&#39;angolo in basso a sinistra.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` visualizzatore applicato a una risorsa immagine. [Provate](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target=&quot;_blank&quot;}.
* `Zoom_light` visualizzatore applicato a un’immagine. [Provate](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target=&quot;_blank&quot;}.

## Facoltativo - Ulteriori informazioni

Per saperne di più su ciò che hai appena letto, utilizza i materiali qui sotto per esplorare i concetti in modo più dettagliato. Altrimenti, il Percorso Dynamic Media è completo!

_Argomenti dell’Aiuto di Dynamic Media_

* [Come creare i predefiniti per immagini](/help/assets/dynamic-media/image-presets.md)
* Un elenco di [parametri di elaborazione delle immagini](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) che puoi utilizzare nel campo modificatore immagine quando crei un predefinito per immagini
* [Come visualizzare in anteprima le risorse](/help/assets/dynamic-media/previewing-assets.md)
* [Come visualizzare in anteprima le risorse 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Come creare i set di immagini](/help/assets/dynamic-media/image-sets.md)
* [Come creare set 360 gradi](/help/assets/dynamic-media/spin-sets.md)
* [Come creare set di file multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md)

_Tutorial su Dynamic Media_

* [Utilizzare Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=it)
* [Libreria dei contenuti di Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (ricerca su _Dynamic Media_)

_Visualizzatori Dynamic Media_

* [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) di ciascun visualizzatore

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->