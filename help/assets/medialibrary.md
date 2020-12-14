---
title: AEM Assets e AEM MediaLibrary a confronto
description: Domande frequenti su  AEM Assets e AEM Media Library, comprese le differenze tra i due elementi.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 3%

---


#  AEM Assets e AEM MediaLibrary domande frequenti {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager (AEM) Assets è parte integrante della piattaforma AEM. Questa integrazione è vista come un vantaggio importante per la AEM e assicura la coerenza nella gestione dei contenuti e un&#39;elevata produttività per gli autori dei contenuti.

## Cos&#39;è  AEM Assets? {#what-is-aem-assets}

 AEM Assets è un&#39;applicazione della piattaforma AEM che consente ai clienti di gestire le proprie risorse digitali (immagini, video, documenti e clip audio) in un archivio basato su Web.  AEM Assets include il supporto dei metadati, le rappresentazioni, il Finder di Digital Asset Management e l&#39;amministrazione tramite l&#39;interfaccia utente.

## Cos&#39;è la AEM Media Library? {#what-is-the-aem-media-library}

AEM Media Library è una parte designata dell&#39;archivio di contenuti WCM AEM in cui vengono memorizzate le immagini e altre risorse condivise. La libreria Media utilizza le funzionalità di gestione delle risorse digitali di AEM WCM.

## Cosa si ottiene da  AEM Assets che non fa parte di AEM WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Le funzioni uniche disponibili solo per  clienti di AEM Assets sono:

1. la possibilità di estrarre e modificare metadati diversi da titolo, tag e descrizione.
1. l&#39;amministratore di AEM Assets , disponibile dalla schermata di benvenuto facendo clic sul secondo pulsante accanto all&#39;amministratore del sito.
1. Tutti i passaggi del flusso di lavoro relativi alla gestione delle risorse digitali,  ad esempio l’inserimento di AEM Assets,  l’eliminazione di AEM Assets,  la gestione delle risorse secondarie di AEM Assets  l’estrazione di metadati AEM Assets.
1. librerie che includono &quot;dam&quot; im package space.

L&#39;utilizzo di queste funzioni richiede una licenza valida di  AEM Assets.

##  AEM Assets è disponibile come pacchetto separato? {#is-aem-assets-available-as-a-separate-package}

No. Per semplificare l&#39;installazione e la distribuzione, tutte AEM applicazioni e componenti aggiuntivi vengono distribuiti in un unico pacchetto con tutte le funzionalità incluse. Ciò non implica che si disponga dell&#39;autorizzazione per utilizzare tutte le funzioni del pacchetto.

## Desidero modificare i metadati delle risorse digitali. Ho bisogno  AEM Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Se intendete modificare metadati diversi da titolo, descrizione e tag, è necessario disporre della licenza per  AEM Assets.

## Voglio usare il predicato della categoria sul mio sito web. Ho bisogno  AEM Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sì, il predicato della categoria, insieme a tutti gli altri componenti, fanno parte di  AEM Assets e richiedono una licenza AEM Assets .

## È possibile ridimensionare automaticamente le immagini al momento dell&#39;importazione. Ho bisogno  AEM Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Sì. Il ridimensionamento delle immagini e la trasformazione automatica basata su flusso di lavoro, nonché la capacità di gestire le rappresentazioni, fanno parte di  AEM Assets e richiedono una licenza AEM Assets .

## Voglio ridimensionare le immagini utilizzando un componente immagine personalizzato. Ho bisogno  AEM Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Il componente immagine fa parte di AEM WCM. La libreria grafica utilizzata dal componente immagine (ma anche da  AEM Assets) fa parte della piattaforma AEM e non richiede una licenza  AEM Assets.

## Come posso impedire ai miei utenti di utilizzare  AEM Assets se non ho ottenuto la licenza  AEM Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Puoi rimuovere da AEM tutti  flussi di lavoro, componenti, tassonomie, opzioni specifici di AEM Assets e l’amministratore  AEM Assets. In questo modo si evita che gli utenti utilizzino accidentalmente  funzioni AEM Assets che non sono state autorizzate.

## Desidero aggiungere delle immagini a una pagina e ritagliarle e ridimensionarle. Ho bisogno  AEM Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Per questo caso d’uso non è necessario acquistare  AEM Assets, anche l’utilizzo di Media Library non è richiesto per utilizzare immagini su un sito Web, in quanto il componente per immagini intelligenti consente di caricare le immagini direttamente nella pagina.

## Elenco dettagliato delle funzioni disponibili in  AEM Assets vs Media Library {#listoffeatures}

**AEM Assets**

* Raccolte e lightbox
* Gestione e proprietà avanzate dei metadati
* Collegamento  risorsa Adobe (collegamento ad Creative Cloud per Enterprise)
* App desktop AEM
* Profili di elaborazione
* Integrazione  server InDesign
* Modelli di risorse e framework di produttori di cataloghi
*  risorse collegate ai Adobe Photoshop,  Illustrator e 
* Gestione multilingue delle risorse
* Integrazione PIM
* Rights Management
* Supporto Camera Raw
* Gestione e configurazione dei facet di ricerca
* Flussi di lavoro DAM pregenerati (ad esempio, photoshot)
* Reporting delle risorse e analisi: Informazioni sulle risorse
* Gestione risorse 3D
* Risorse collegate
* Brand Portal
* Accesso self-service
* Sfogliare, cercare e scaricare
* Raccolte e condivisione cartelle
* Strumenti di amministrazione
* Tag avanzati
* Visual Search
* Interfaccia utente Amministratore risorse

**Libreria multimediale**

* Proprietà metadati di base
* Gestione tag
* Controllo della versione
* Rappresentazioni statiche
* Progetti, Attività, Authoring dei flussi di lavoro
* Flusso attività (timeline)
* Query Builder (API)
* Integrazione Marketing Cloud
* Personalizzazione ed estensione dell&#39;interfaccia utente
* Commenti e annotazioni