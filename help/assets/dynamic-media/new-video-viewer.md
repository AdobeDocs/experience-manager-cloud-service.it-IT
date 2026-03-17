---
title: Nuovo visualizzatore video
description: Il nuovo Visualizzatore video di Dynamic Media offre un’esperienza di riproduzione video migliorata
role: User
source-git-commit: 1ee4f1352a0fe1e8d1f2fd7b79555ad4144bb02c
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 2%

---

# Nuovo visualizzatore video in Dynamic Media {#new-video-viewer-dynamic-media}

Il nuovo Visualizzatore video per Dynamic Media offre un’esperienza di riproduzione video modernizzata in Adobe Experience Manager (AEM). Offre un’esperienza di visualizzazione coerente ed estensibile negli ambienti di authoring, anteprima e Sites, continuando a lavorare con i flussi di lavoro di Dynamic Media esistenti.

I visualizzatori video esistenti in Dynamic Media supportano i requisiti di riproduzione di base, ma forniscono estensibilità limitata e integrazione a livello di evento per scenari di analisi e integrazione moderni

Il nuovo visualizzatore video consente di superare queste limitazioni:

* Fornire un’esperienza di riproduzione più coerente
* Consentire la selezione esplicita del visualizzatore
* Emissione di eventi di riproduzione strutturati per utilizzo programmatico
* Supporto dell’integrazione con analisi esterne e sistemi esterni

Il visualizzatore è disponibile come opzione aggiuntiva e richiede una selezione esplicita se supportata. Non sostituisce automaticamente i visualizzatori video esistenti.

Il nuovo Visualizzatore video è destinato alle organizzazioni che richiedono un’esperienza video migliorata ed estensibile senza interrompere le implementazioni esistenti.

> **NOTA**
>
> Il nuovo visualizzatore video è una funzione a disponibilità limitata. Per abilitarlo, crea un [ticket di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).


## Funzionamento del nuovo visualizzatore video {#how-it-works}

Il nuovo visualizzatore video funziona come segue:

1. Una risorsa video viene acquisita in una cartella sincronizzata con Dynamic Media.
2. Il video può essere visualizzato in anteprima dalla pagina dei dettagli della risorsa utilizzando **Video (nuovo)**.
3. Il nuovo visualizzatore video può essere selezionato nel componente **Dynamic Media** durante la creazione di pagine Sites.
4. Durante la riproduzione, il visualizzatore emette eventi strutturati nella finestra principale.
5. È possibile utilizzare modificatori di visualizzatore opzionali per controllare il comportamento di riproduzione.

## Differenze chiave rispetto al visualizzatore video esistente {#key-differences}

| Area | Descrizione |
|------|-------------|
| Disponibilità visualizzatore | Viene visualizzata come nuova opzione denominata **Video (nuovo)** |
| Selezione visualizzatore | Deve essere selezionato in modo esplicito |
| Estensibilità | Genera eventi di riproduzione strutturati |
| Integrazione | Continua a funzionare con i flussi di lavoro Dynamic Media esistenti |

## Prerequisiti {#prerequisites}

Prima di utilizzare il nuovo Visualizzatore video, accertati di soddisfare i seguenti prerequisiti:

| Requisito | Descrizione |
|------------|-------------|
| Sincronizzazione Dynamic Media | La cartella delle risorse deve essere sincronizzata con Dynamic Media. |
| Profilo video | Alla cartella deve essere applicato un profilo video. |
| Risorsa video | Un video deve essere acquisito nella cartella. |

Il nuovo visualizzatore video è disponibile a partire da **AEM as a Cloud Service versione 2025.7.0**.

Per abilitare o disabilitare il nuovo visualizzatore video, contatta l’Assistenza clienti di Adobe.

## Visualizzare l&#39;anteprima del nuovo visualizzatore video {#preview}

Per visualizzare in anteprima il nuovo visualizzatore video dalla pagina dei dettagli della risorsa, effettua le seguenti operazioni:

1. Passa a **Assets** > **File** e apri la cartella contenente la risorsa video.
2. Fai clic sulla risorsa video per aprire la pagina dei dettagli della risorsa.
3. Nel pannello a sinistra, fai clic su **Visualizzatori**.
4. Nel pannello **Visualizzatori**, seleziona **Video (nuovo)**.
5. Fai clic su **URL** per copiare il collegamento di anteprima.
   ![Copia URL](assets/Copy-url1.jpg)

## Utilizzare il nuovo Visualizzatore video in Sites {#use-in-sites}

Il nuovo visualizzatore video è disponibile tramite il componente **Dynamic Media** esistente in AEM Sites.

### Aggiungere il componente Dynamic Media

Per aggiungere un video utilizzando il componente Dynamic Media, effettua le seguenti operazioni:

1. Apri la pagina nell&#39;editor **Sites**.
2. Trascina il componente **Dynamic Media** nella posizione desiderata sulla pagina.
3. Seleziona il componente **Dynamic Media** nella pagina.
4. Fai clic sul componente per aprire il selettore risorse.
5. Seleziona una risorsa video.

![Trascina componente Dynamic Media](assets/drag-component.jpeg)

### Configurare il visualizzatore

Per configurare il predefinito visualizzatore, effettua le seguenti operazioni:

1. Seleziona il componente **Dynamic Media** nella pagina.
2. Fare clic su **Configura** nella barra degli strumenti del componente.
   ![Apri impostazioni Dynamic Media](assets/configure-asset.png)

3. Nella finestra di dialogo **Impostazioni Dynamic Media**, seleziona **Video (nuovo)** dall&#39;elenco a discesa **Predefinito visualizzatore**.
   ![Seleziona predefinito visualizzatore video (nuovo)](assets/viewer-preset.jpeg)

4. Immettere i modificatori richiesti nel campo **Modificatori visualizzatore** (ad esempio, `autoplay=true&muted=true`).
   ![Modificatori visualizzatore](assets/additional-modifiers.jpeg)

5. Salva le modifiche.

Il video viene caricato sulla pagina utilizzando il nuovo Visualizzatore video.

> **Nota:** il nuovo visualizzatore video non sostituisce automaticamente i video esistenti. Gli utenti devono selezionare manualmente **Video (nuovo)** nel **Predefinito visualizzatore** quando utilizzano il componente Dynamic Media, oppure aggiornare gli URL diretti in modo che puntino al Nuovo Visualizzatore video, se necessario.

### Migrazione di video tramite URL diretti

Se i video sono accessibili tramite URL diretti invece del componente Dynamic Media, puoi passare al nuovo visualizzatore video aggiornando l’URL. Esempio: `https://s7d1.scene7.com/dmviewers/html5/VideoViewer.html?asset=<video-asset>`

## Modificatori visualizzatore {#viewer-modifiers}

I modificatori di visualizzatore consentono di controllare il caricamento delle risorse, il comportamento di riproduzione, la selezione del formato di streaming e la presentazione del visualizzatore.

| Modificatore | Descrizione |
|--------|-------------|
| `asset` | Specifica l’ID della risorsa del video o del set di video adattivi. |
| `posterimage` | Specifica l&#39;immagine visualizzata prima dell&#39;inizio della riproduzione. |
| `serverurl` | Specifica il percorso della directory principale di Image Server. |
| `contenturl` | Specifica il percorso della directory principale del contenuto. |
| `videoserverurl` | Specifica il percorso della directory principale del server video. |
| `sources.dash` | Specifica l&#39;URL del manifesto DASH per la riproduzione. |
| `sources.hls` | Specifica l&#39;URL del manifesto di HLS per la riproduzione. |
| `autoplay=true` | Avvia la riproduzione automaticamente al caricamento del video. |
| `controls=true/false` | Mostra o nasconde i controlli di riproduzione video. |
| `loop=true` | Riavvia la riproduzione automaticamente al termine del video. |
| `muted=true` | Avvia la riproduzione in uno stato di disattivazione audio. |
| `playbackrates` | Specifica le opzioni di velocità di riproduzione disponibili. |
| `playback` | Specifica il formato di streaming (automatico, hls, trattino o progressivo). |
| `progressivebitrate` | Specifica il bitrate per la riproduzione progressiva. |
| `initialbitrate` | Specifica il bitrate iniziale per lo streaming adattivo. |
| `isletterboxed=true/false` | Controlla se il video è in formato letterbox o esteso. |
| `customcss` | Specifica un file CSS personalizzato per lo stile del visualizzatore. |
| `transition` | Specifica il comportamento di transizione Mostra o Nascondi per i controlli visualizzatore. |

I modificatori sono specificati come parametri di query nel campo **Modificatori visualizzatore**.

## Eventi supportati {#supported-events}

Durante la riproduzione, il nuovo visualizzatore video genera i seguenti eventi:

| Tipo di evento | Descrizione |
|-----------|-------------|
| play | Il video inizia la riproduzione |
| pausa | Il video è in pausa |
| ricerca | L’utente cerca all’interno del video |
| carica | Il video è caricato |
| chiudi | Il lettore è chiuso |
| metadati | Metadati come durata |
| milestone | Cardine di riproduzione raggiunto |
| current_time | Posizione riproduzione periodica |
| fullscreen | Passa a schermo intero |
| un_fullscreen | Esci da schermo intero |

## Gestione degli eventi nella finestra padre {#handling-events}

Il nuovo visualizzatore video invia messaggi relativi alla riproduzione alla pagina padre durante le interazioni video.

Per gestire questi eventi, l’applicazione principale deve ascoltare gli eventi dei messaggi del browser e convalidare l’origine del messaggio prima di elaborare i dati.

Il payload dell’evento include informazioni quali il tipo di evento, lo stato di riproduzione, il tempo di riproduzione corrente e metadati aggiuntivi. Questi eventi possono essere utilizzati per supportare il tracciamento di Analytics, le interazioni personalizzate o l’integrazione con sistemi esterni.

Adobe consiglia di convalidare l’origine del messaggio per garantire che gli eventi vengano elaborati solo dai domini Dynamic Media attendibili.

## Rapporto Coinvolgimento video per il nuovo visualizzatore video {#video-engagement-report}

Il rapporto Coinvolgimento video fornisce metriche di analisi per i video riprodotti con il nuovo visualizzatore video in Dynamic Media. Il report fornisce dati aggregati sulle prestazioni per il mese specificato e supporta la creazione di report mensili.

I rapporti vengono generati su richiesta. Per richiedere un report, crea un [ticket di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) e fornisci i seguenti dettagli:

* Mese del rapporto: specifica il mese per il quale è richiesto il rapporto (ad esempio, gennaio 2026).
* Indirizzo e-mail di consegna: indirizzo e-mail del gruppo (consigliato) o dell’individuo a cui inviare il rapporto

Il rapporto fornisce metriche di coinvolgimento per video, tra cui visualizzazioni, impression, tempo di osservazione, tasso di completamento e punteggio di coinvolgimento.

### Formato del rapporto

* I rapporti vengono consegnati in formato CSV.
* Ogni riga rappresenta un singolo video.
* Le metriche vengono aggregate per il periodo di reporting selezionato.
* Le risorse eliminate sono escluse dal rapporto.
* Supporta il filtro per `tenant_name`.

### Campi del rapporto

Il rapporto Coinvolgimento video include i campi seguenti:

| Campo | Descrizione | Calcolo |
|-------|------------|-------------|
| `video_id` | Identificatore video univoco. | ND |
| `video_name` | Nome della risorsa video. | ND |
| `video_created_date` | Data di creazione del video. | ND |
| `duration_in_seconds` | Durata del video in secondi. | ND |
| `video_views` | Numero totale di eventi di riproduzione video durante il periodo di reporting selezionato. | ND |
| `video_impressions` | Numero totale di caricamenti del video. | ND |
| `video_watched_seconds` | Totale secondi osservati in tutti gli eventi di riproduzione. | Somma dei secondi osservati in tutti gli eventi di riproduzione |
| `play_rate` | Percentuale di riproduzioni video relative ai caricamenti video. | (`video_views` ÷ `video_impressions`) × 100 |
| `avg_time_watched_in_seconds` | Media di secondi osservati per visualizzazione. | `video_watched_seconds` ÷ `video_views` |
| `avg_completion_rate` | Percentuale di visualizzazioni che hanno raggiunto il completamento video completo. | (Visualizzazioni completate ÷ `video_views`) × 100 |
| `engagement_score` | Percentuale media di ascolto su tutti gli eventi di riproduzione. | (Percentuale totale di sequenze temporali video visualizzate in tutte le sessioni ÷ `video_views`) |
| `tenant_name` | Identificatore della società o del tenant associato ai dati. | ND |

## Domande frequenti {#faq-video-engagement}

+++Se un video è impostato su Riproduzione automatica, viene conteggiato come visualizzazione automaticamente o solo dopo che l’utente ha guardato per una durata minima?

La riproduzione automatica viene conteggiata come una visualizzazione video. La riproduzione avviata automaticamente viene registrata come visualizzazione.

+++

+++Se un utente guarda solo una parte del video (ad esempio, i primi 2 secondi e gli ultimi 2 secondi di un video di 10 secondi), viene conteggiata come visualizzazione completata?

Una visualizzazione viene conteggiata come completata quando la riproduzione raggiunge la fine della timeline del video, anche se alcune parti del video sono state saltate.

+++

+++Se un utente scorre all’indietro e guarda nuovamente parti del video, aumenta il conteggio di video_views, engagement_score o entrambi?

Il re-watching di parti del video non aumenta il conteggio di video_views. Una riproduzione aggiuntiva contribuisce al engagement_score.

+++

+++Se lo stesso utente guarda lo stesso video più volte senza ricaricare la pagina, come vengono calcolati video_views e engagement_score?

La riproduzione ripetuta senza ricaricare la pagina non aumenta il conteggio di video_views. Una riproduzione aggiuntiva contribuisce al engagement_score.

+++

+++La sospensione e la ripresa di un video influiscono sul tracciamento del coinvolgimento o sul calcolo del tasso di completamento?

La sospensione e la ripresa della riproduzione non influiscono sul tracciamento del coinvolgimento o sul calcolo del tasso di completamento.

+++
