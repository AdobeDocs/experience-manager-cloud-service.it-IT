---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 4c3007b9e38f8a18d61b781ddbcd00bd45b67729
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] come Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] come Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Per informazioni sugli aggiornamenti della documentazione non direttamente correlati a una versione, consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) .

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 è il 27 maggio 2021.
La versione seguente (2021.6.0) sarà del 24 giugno 2021.

## AEM come base di Cloud Service {#foundation}

### Novità di AEM as a Cloud Service Foundation {#what-is-new-foundation}

* [Canale](/help/release-notes/prerelease.md) pre-rilascio: Anteprima delle prossime funzionalità per un mese intero prima che diventino live in produzione!

* [Obsolescenza API](/help/release-notes/deprecated-apis.md): è disponibile un elenco delle API obsolete più recenti per AEM as a Cloud Service .

* [AEM come Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html): Aggiorna i progetti Maven all’ultima versione, che include un controllo Java API obsoleto e altri miglioramenti.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* A breve potrai verificare il contenuto di un nuovo [livello di anteprima](/help/sites-cloud/authoring/fundamentals/previewing-content.md) per simulare l’aspetto e l’aspetto dell’esperienza finale come faresti sul livello di pubblicazione. Questa opzione è abilitata dalla procedura guidata Pubblicazione gestita di AEM Sites che consente di scegliere una destinazione di pubblicazione tra Pubblica o Anteprima. È quindi possibile accedere alle esperienze in anteprima tramite un URL dedicato. Dopo la convalida in Anteprima, il contenuto può essere pubblicato come di consueto da Author a Publish. L’abilitazione del servizio di anteprima in ambienti AEM come Cloud Service verrà gradualmente implementato nelle prossime settimane.

## [!DNL Adobe Experience Manager Assets] come  [!DNL Cloud Service] {#assets}

### Nuove funzioni disponibili nel canale pre-rilascio {#what-is-new-assets-prerelease}

* Gli schemi di metadati possono essere applicati direttamente alle proprietà della cartella.

   ![Aggiungi schema metadati dalle proprietà della cartella](/help/assets/assets/metadata-schema-folder-properties.png)

* Lo strumento Asset Bulk Ingestor consente di aggiungere metadati durante un’acquisizione in blocco.

* I miglioramenti dell’esperienza utente visualizzano il numero di risorse presenti in una cartella. Per più di 1000 risorse in una cartella, [!DNL Assets] visualizza più di 1000 risorse.

   ![Nell’interfaccia viene visualizzato il numero di risorse presenti in una cartella](/help/assets/assets/browse-folder-number-of-assets.png)

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

* Il caricamento di file di grandi dimensioni causa l&#39;arresto anomalo del sistema [!DNL Experience Manager desktop app]. (CQ-4320942)
* Le opzioni della barra degli strumenti sono diverse quando la stessa raccolta è selezionata all’interno di una cartella e quando è selezionata da un risultato di ricerca. (CQ-4321406)

#### Novità in [!DNL Dynamic Media] {#what-is-new-dm}

* Le funzioni DPR (Smart Imaging Device Pixel Ratio) e di ottimizzazione della larghezza di banda della rete consentono di fornire immagini di alta qualità in modo efficiente su dispositivi con display ad alta risoluzione e larghezza di banda limitata della rete. Consulta [domande frequenti sull&#39;imaging intelligente](/help/assets/dynamic-media/imaging-faq.md).

   >[!NOTE]
   >
   >La timeline della versione per i miglioramenti di Smart imaging riportati sopra è:
   >
   >* Nord America 24 maggio 2021 in NA,
      >
      >
   * Europa, Medio Oriente e Africa 25 giugno 2021,
      >
      >
   * Asia-Pacifico, 19 luglio 2021.


* È stato introdotto il supporto per AVIF in formato immagine di nuova generazione in [!DNL Dynamic Media] consegna (modificatore URL fmt).

   >[!NOTE]
   >
   >La timeline della versione per il supporto AVIF è la seguente:
   >
   >* Nord America 10 maggio 2021,
      >
      >
   * Europa, Medio Oriente e Africa 24 maggio 2021,
      >
      >
   * Asia-Pacifico, 24 giugno 2021.


## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0.

### Data di rilascio {#release-date-cm-may}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.5.0 è il 6 maggio 2021.
La prossima versione è prevista per il 3 giugno 2021.

### Novità {#what-is-new-may}

* La regola di qualità PackageOverlaps ora rileva i casi in cui lo stesso pacchetto è stato distribuito più volte, ovvero in più posizioni incorporate, nello stesso set di pacchetti distribuito.

* L’endpoint dell’archivio nell’API pubblica ora include l’URL Git.

* Il registro di distribuzione scaricato da un utente di Cloud Manager sarà più dettagliato e ora includerà dettagli sugli errori e sugli scenari di successo.

* Sono stati risolti gli errori intermittenti durante il push del codice all’Git di Adobe.

* È ora possibile applicare il componente aggiuntivo Commerce ai programmi Sandbox durante il flusso di lavoro Modifica programma .

* L&#39;esperienza del programma Edit è stata aggiornata.

* La tabella Nomi di dominio nella pagina Dettagli ambiente visualizza fino a 250 nomi di dominio tramite impaginazione.

* La scheda Soluzioni nei flussi di lavoro Aggiungi programma e Modifica programma visualizzerà la soluzione, anche se per il programma è disponibile una sola soluzione.

* Il messaggio di errore nel registro dei passaggi della build quando la build non produceva pacchetti di contenuto distribuiti non era chiaro.

### Correzioni di bug {#bug-fixes-cm-may}

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Invece di rimuovere le variabili &quot;eliminate&quot;, le variabili delle pipeline API le contrassegnavano solo con lo stato **ELIMINATO**.

* Alcuni problemi di qualità del tipo di odore del codice hanno avuto un impatto errato sul rating di affidabilità.

* Poiché i domini con caratteri jolly non sono supportati, l’interfaccia utente non consente all’utente di inviare un dominio con caratteri jolly.

* Quando è stata avviata l’esecuzione di una pipeline tra la mezzanotte e l’1:00 UTC, la versione dell’artefatto generata da Cloud Manager non era garantita come maggiore di una versione creata il giorno precedente.

* Durante la configurazione del programma Sandbox, una volta che il progetto con codice di esempio è stato creato correttamente, Manage Git (Gestisci Git) apparirà come collegamento dalla scheda eroe nella pagina Overview (Panoramica).

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

### Data di rilascio {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.4.0 è l’11 maggio 2021.

### Novità {#what-is-new-ctt-may}

* Questa versione dello strumento Content Transfer (Trasferimento contenuti) crea rappresentazioni di testo per le risorse da migrare al Cloud Service. Le rappresentazioni di testo sono necessarie per supportare la ricerca full-text sulle risorse acquisite.
* Il numero massimo di set di migrazione dello strumento Content Transfer (Trasferimento contenuti) che un utente può creare è stato aumentato da 4 a 10.

### Correzioni di bug {#bug-fixes-ctt-may}

* Correzioni di bug multipli relative alla funzione di aggiornamento automatico nell’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti).
* Lo strumento Content Transfer (Trasferimento contenuti) con `wipe=true` causava un indice di contatore errato nel target. Questo problema è stato risolto.

## Componente aggiuntivo Commerce {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto per l’impaginazione del contenuto associato nelle proprietà della console del prodotto

### Correzioni di bug {#bug-fixes-commerce}

* Miniature delle risorse non visualizzate nella scheda Risorsa delle proprietà del prodotto

* Breadcrumb ripristina i dati di anteprima nella console del prodotto
