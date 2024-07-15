---
title: Note sulla versione 2021.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 46%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 è il 27 maggio 2021.
La seguente versione (2021.6.0) sarà del 28 giugno 2021.

## AEM as a Cloud Service Foundation {#foundation}

### Novità di AEM as a Cloud Service Foundation {#what-is-new-foundation}

* [Canale prerelease](/help/release-notes/prerelease.md): anteprima delle prossime funzionalità per un mese intero prima che vengano pubblicate in produzione!

* [API obsolete](/help/release-notes/deprecated-removed-features.md): è disponibile un elenco delle ultime API obsolete per AEM as a Cloud Service.

* [Plug-in Maven SDK Build Analyzer per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it): aggiorna i progetti Maven all&#39;ultima versione, con la verifica di API Java obsolete e altri miglioramenti.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Presto potrai verificare il contenuto in un nuovo [livello di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) per simulare l&#39;aspetto finale dell&#39;esperienza così come si presenterà nel livello Publish. Questa funzione è abilitata dalla procedura guidata Pubblicazione gestita in AEM Sites, che ora consente di scegliere una destinazione di pubblicazione tra Publish o Anteprima. Le esperienze in Anteprima sono quindi accessibili tramite un URL dedicato. Dopo la convalida nell’ambiente di Anteprima, il contenuto può essere pubblicato come di consueto da Authoring a Publish. Il servizio Anteprima negli ambienti AEM as a Cloud Service verrà introdotto gradualmente nelle prossime settimane.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* Puoi scaricare le risorse condivise utilizzando la funzionalità Condivisione collegamenti. Questo download utilizza ora un servizio asincrono che offre download più veloci e ininterrotti, anche per download di dimensioni molto grandi. Vedi [scarica risorse](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Scarica casella in entrata](/help/assets/assets/download-inbox.png)

### Nuove funzioni disponibili nel canale prerelease di {#what-is-new-assets-prerelease}

* Gli schemi di metadati possono essere applicati direttamente alle proprietà della cartella.

  ![Aggiungi schema metadati dalle proprietà della cartella](/help/assets/assets/metadata-schema-folder-properties.png)

* Lo strumento Asset Bulk Ingestor consente di aggiungere metadati durante un’acquisizione in blocco.

* I miglioramenti dell’esperienza utente consentono di visualizzare il numero di risorse presenti in una cartella. Se una cartella contiene più di 1000 risorse, [!DNL Assets] visualizza la dicitura &quot;1000+&quot;.

  ![Numero di risorse in una cartella visualizzate nell&#39;interfaccia](/help/assets/assets/browse-folder-number-of-assets.png)

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

* Il caricamento di file di grandi dimensioni provoca l&#39;arresto anomalo di [!DNL Experience Manager desktop app]. (CQ-4320942)
* Le opzioni della barra degli strumenti sono diverse quando la stessa raccolta viene selezionata all’interno di una cartella e quando viene selezionata da un risultato di ricerca. (CQ-4321406)

#### Novità di Dynamic Medie {#what-is-new-dm}

* La funzione Smart Imaging DPR (Device Pixel Ratio) e l&#39;ottimizzazione della larghezza di banda della rete consentono di fornire immagini di alta qualità in modo efficiente su dispositivi con display ad alta risoluzione e larghezza di banda limitata. Per ulteriori informazioni, consulta [Domande frequenti su Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) e [Ottimizzazione immagine con formati immagine di nuova generazione WebP e AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* È stato introdotto il supporto per il formato AVIF di nuova generazione nella distribuzione Dynamic Medie (modificatore URL fmt).

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Guida contestuale**: è stata aggiunta una guida contestuale per l’editor di moduli adattivi, l’editor di modelli e l’editor di temi per aiutare gli autori a comprendere meglio le varie funzioni degli editor.
* **Messaggi di errore nel browser Proprietà**: sono stati aggiunti messaggi di errore per ogni proprietà nel browser Proprietà dei moduli adattivi. Questi messaggi aiutano a comprendere i valori consentiti per un campo.

### Prossima funzione beta di [!DNL Forms] {#what-is-new-forms-prerelease}

Output as a Cloud Service: il servizio di output consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità batch sincrona e asincrona. Il servizio di output consente di creare applicazioni che permettono di:

* Generare i documenti compilando i file modello con dati XML.
* Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
* Generare PDF di stampa da PDF modulo XFA.

Per registrarti al programma beta, puoi inviare un’e-mail all’indirizzo formscsbeta@adobe.com.

### Bug corretti in [!DNL Forms] {#forms-bugs-fixed}

* In un passaggio Assegna attività dei flussi di lavoro di AEM Forms, quando sostituisci l’icona predefinita dei pulsanti di azione con un’icona Coral, il flusso di lavoro smette di funzionare e registra un’eccezione. Il flusso di lavoro funziona come previsto quando vengono utilizzate le icone predefinite.
* Nel livello di layout, quando modifichi il numero di colonne, quando apri il livello di modifica e trascini alcuni componenti in un pannello, le caselle blu quadrate iniziano a comparire nell’area del contenuto dell’editor di moduli adattivi e l’editor inizia a non rispondere.
* Il messaggio di errore di un’opzione di un editor di regole per fornire l’URL di una risorsa adattiva o esterna è troppo lungo e non è di facile utilizzo.


## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0.

### Data di rilascio {#release-date-cm-may}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.5.0 è il 6 maggio 2021.
La prossima versione è pianificata per il venerdì 3 giugno 2021.

### Novità {#what-is-new-may}

* Ora la regola di qualità PackageOverlaps rileva i casi in cui lo stesso pacchetto viene distribuito più volte, ovvero in più posizioni incorporate, nello stesso set di pacchetti distribuito.

* L’endpoint dell’archivio nell’API pubblica ora include l’URL di Git.

* I registri di distribuzione scaricati da un utente di Cloud Manager sono più dettagliati e includono dettagli sugli errori e sugli scenari di successo.

* Sono stati risolti gli errori intermittenti che si verificavano durante il push del codice nell’archivio Git di Adobe.

* Ora è possibile applicare il componente aggiuntivo Commerce ai programmi sandbox durante il flusso di lavoro Modifica programma.

* L’esperienza Modifica programma è stata aggiornata.

* La tabella Nomi di dominio nella pagina Dettagli dell’ambiente visualizza fino a 250 nomi di dominio tramite impaginazione.

* La scheda Soluzioni nei flussi di lavoro Aggiungi programma e Modifica programma mostrano la soluzione anche se per il programma ne è disponibile solo una.

* Il messaggio di errore nel registro della fase di build relativo a quando la build non produceva pacchetti di contenuto distribuiti non era chiaro.

### Correzioni di bug {#bug-fixes-cm-may}

* In alcuni casi, l’utente visualizzava uno stato verde “attivo” a fianco di un elenco IP consentiti anche quando tale configurazione non era stata distribuita.

* Anziché rimuovere le variabili “eliminate”, l’API delle variabili della pipeline si limitava a contrassegnarle con lo stato **ELIMINATE**.

* Alcuni problemi di qualità di tipo code smell influivano erroneamente sulla valutazione dell’affidabilità.

* Poiché i domini con caratteri jolly non sono supportati, l’interfaccia utente non consente all’utente di inviare un dominio con caratteri jolly.

* Quando l’esecuzione di una pipeline veniva avviata tra la mezzanotte e l’1:00 UTC, la versione dell’artefatto generata da Cloud Manager non era sempre superiore alla versione creata il giorno precedente.

* Ora durante la configurazione del programma sandbox, al termine della creazione corretta del progetto con il codice di esempio, viene visualizzato il collegamento Gestisci Git nella scheda hero della pagina Panoramica.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.4.6 è il 27 maggio 2021.

### Novità {#what-is-new-ctt-latest}

* Se l&#39;utente non dispone dell&#39;autorizzazione di esecuzione per l&#39;eseguibile Java, è stata aggiunta una nuova istruzione di registrazione al registro degli errori dell&#39;avvio rapido.

* Quando un utente elimina un set di migrazione dall&#39;interfaccia utente CTT, in cui è stata eseguita un&#39;estrazione, la cartella `tmp` associata a tale set di migrazione viene eliminata per risparmiare spazio.

### Correzioni di bug {#bug-fixes-ctt-latest}

* Durante l’eliminazione di un set di migrazione, a volte veniva visualizzato un messaggio di errore non utile nell’interfaccia utente dello strumento Content Transfer. Questo problema è stato risolto.

* Durante l’esecuzione di Mappatura utenti, se gli utenti avevano lo stesso indirizzo e-mail sulla destinazione e sull’host, ma nomi utente diversi, l’intera acquisizione non riusciva. Questo problema è stato risolto. In questo caso, l&#39;utente/gruppo viene ignorato e registrato come conflitto nel file di registro.

### Data di rilascio {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.4.0 è l’11 maggio 2021.

### Novità {#what-is-new-ctt-may}

* Questa versione dello strumento Content Transfer (Trasferimento contenuti) crea rappresentazioni testuali delle risorse di cui si esegue la migrazione al Cloud Service. Le rappresentazioni testuali sono necessarie per supportare la ricerca full-text sulle risorse acquisite.
* Il numero massimo di set di migrazione dello strumento Content Transfer (Trasferimento contenuti) che un utente può creare è stato aumentato da 4 a 10.

### Correzioni di bug {#bug-fixes-ctt-may}

* Sono state apportate diverse correzioni di bug alla funzione di aggiornamento automatico nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti).
* Lo strumento Content Transfer con `wipe=true` ha prodotto un indice del contatore errato sulla destinazione. Questo problema è stato risolto.

## Componente aggiuntivo Commerce {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto dell’impaginazione per il contenuto associato nelle proprietà della console del prodotto

### Correzioni di bug {#bug-fixes-commerce}

* Le miniature delle risorse non vengono visualizzate nella scheda Risorsa delle proprietà del prodotto

* Breadcrumb ripristina i dati di anteprima nella console prodotto
