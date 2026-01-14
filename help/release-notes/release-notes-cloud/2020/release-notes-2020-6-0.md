---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.6.0'
description: '[!DNL Adobe Experience Manager] Note sulla versione 2020.6.0 di as a Cloud Service.'
exl-id: fd6ebe2b-6d98-498c-a45d-b9a9c34e6be7
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 91%

---

# Note sulla versione per AEM as a Cloud Service 2020.6.0 {#release-notes}

Questa pagina illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.6.0.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Experience Manager] as a Cloud Service 2020.6.0 è il 4 giugno 2020.

## Novità di AEM Sites {#aem-sites}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di AEM Sites in AEM as a Cloud Service, versione 2020.6.0.

### Novità {#whats-new-2020.6.0}

La versione 2.9.0 dei [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) è ora disponibile come parte di AEM Sites e include:

* Integrazione tra [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer) e i componenti core
* Attributi ID HTML configurabili per tutti i componenti
* Un nuovo componente Barra di avanzamento
* Numerose correzioni di bug

### Correzioni di bug {#sites-bug-fixes}

* I componenti all’interno del contenitore layout non sono visibili quando esso viene copiato e incollato nuovamente su una pagina.

* È stato corretto un problema relativo al ridimensionamento del componente layout.

* È stata aggiunta la possibilità di gestire l’indirizzamento delle sole pagine Angular e delle pagine AEM/Angular.

### Accessibilità {#accessibility}

* Ruolo e stato di commento sono ora possibili per gli elementi Masonry nella finestra di dialogo **Crea pagina** mentre ci si sposta in modalità navigazione tramite la freccia giù.

* È stato aggiunto un collegamento nella navigazione per consentire agli utenti di passare direttamente al contenuto principale.

* Sono stati apportati dei miglioramenti all’assistente vocale.

## Novità negli elementi di base di AEM as a Cloud Service {#foundations}

I tempi di creazione dei progetti AEM miglioreranno grazie alla rimozione di tutti i riferimenti all&#39;archivio remoto `https://downloads.experiencecloud.adobe.com/content/maven/public` nel file pom.xml del progetto AEM.

Il file Jar dell’API SDK di AEM as a Cloud Service, precedentemente ospitato in tale posizione, ora si trova in Maven Central, l’archivio di artefatti predefinito di Maven.

## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.6.0.

### Novità {#what-is-new-cloud-manager}

* Ora l’utente con il ruolo *Proprietario business* in Cloud Manager può eliminare un programma sandbox dalla pagina di destinazione (tramite il pulsante di azione rapida nella scheda Programma) o dall’interno del programma.

  Per ulteriori informazioni, consulta [Eliminazione di un programma sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html?lang=it).

* Ora l’utente del programma sandbox con il ruolo di *Proprietario business* o *Responsabile della distribuzione* in Cloud Manager può eliminare il set di ambienti di produzione e di staging impostato tramite l’interfaccia utente di Cloud Manager. L’opzione di eliminazione è ora disponibile sia nella scheda Ambiente nella pagina **Panoramica dei programmi** sia nella pagina **Ambienti**. Selezionando l’opzione di eliminazione nell’ambiente di produzione o staging, viene eliminato anche l’altro nel set.

  Per ulteriori informazioni, consulta [Eliminazione di un programma sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html?lang=it).

* Delle descrizioni sulla pagina di destinazione forniscono all’utente istruzioni di base sulla navigazione.

* Delle descrizioni nella pagina **Panoramica del programma** forniscono all’utente istruzioni di base sulla navigazione in Cloud Manager, utili per iniziare a usarlo.

* Cloud Manager ora presenta una pagina **SCOPRI**, accessibile tramite la navigazione superiore. Questa pagina include risorse per aiutare gli utenti a conoscere i flussi di lavoro più utilizzati in base ai loro ruoli assegnati in Cloud Manager.

* I programmi sandbox ora sono identificati da un contrassegno **Sandbox** visualizzato sulla scheda del programma nella pagina di destinazione e accanto al nome del programma nella pagina **Panoramica programma**.

* Un utente con il ruolo SysAdmin ora ha accesso con un solo clic alla posizione in Admin Console da cui è possibile gestire i ruoli o le autorizzazioni degli utenti per Cloud Manager. Nella pagina di destinazione è ora disponibile un pulsante **Gestisci accesso** accanto al pulsante **Aggiungi programma**.

  Per ulteriori dettagli, consulta [Attività amministratore di sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=it#sysadmin-tasks),

* Un utente con il ruolo SysAdmin ora dispone dell’accesso con un solo clic all’istanza di authoring direttamente da Cloud Manager.

  Per ulteriori dettagli, consulta [Gestione accesso all’istanza di authoring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=it#manage-access-aem).

* Il registro Build ora include l’elenco degli artefatti individuati, inclusi i pacchetti di contenuti ignorati.

* Il passaggio Build ora verifica se tutti i pacchetti di contenuto generati includono tutte le proprietà obbligatorie: nome, gruppo e versione.

* Il passaggio Build ora verifica se la build ha prodotto almeno un pacchetto di contenuti.

### Correzioni di bug {#bug-fixes-cm}

* In alcune situazioni, le icone nella finestra di dialogo **Crea programma** non erano allineate.

* L’identificatore di versione di AEM non veniva visualizzato in modo coerente nella pagina **Panoramica dei programmi**.

* Durante la configurazione della pipeline di produzione, l’opzione **Distribuzione pianificata** non era visibile per alcuni clienti.

### Problemi noti {#known-issues-cm}

* Gli ambienti di un programma sandbox vengono ibernati se non viene rilevata alcuna attività per un certo periodo di tempo. Questo stato non sarà osservato in Cloud Manager. Tuttavia, lo stato può essere osservato tramite la Console per sviluppatori. Questo problema sarà risolto in una versione successiva.

* Il collegamento alla Console per sviluppatori direttamente da Cloud Manager non mostra l’opzione per ibernare/riattivare l’ambiente di un programma sandbox. Per risolvere questo problema, una volta nella Console per sviluppatori, aggiungi il pattern `#release-cm-p1234-e5678` alla fine dell’URL, dove *1234* è l’ID del programma e *5678* è l’ID dell’ambiente. Questo problema sarà risolto in una versione successiva.

## Novità di [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Esperienza utente guidata per tag avanzati migliorati, basati su Adobe AI**

I tag avanzati migliorati consentono di addestrare modelli di assegnazione tag avanzati per riconoscere le immagini in base a tag aziendali specifici, oltre che ai tag avanzati generici.

Con questa versione, è disponibile una nuova user experience guidata che consente di impostare l’addestramento di tag avanzati per set di tag specifici dei clienti e di addestrarli con risorse che in futuro dovranno essere riconosciute e a cui dovranno essere assegnati i tag. L’esperienza è ora più intuitiva.
Addestra i tag avanzati migliorati in modo più intuitivo. Consulta [come aggiungere tag avanzati alle risorse](/help/assets/smart-tags.md).

**Supporto per l’acquisizione, l’anteprima e la distribuzione di contenuti 3D**

Le organizzazioni ora possono archiviare e utilizzare file 3D in AEM Assets. L’utente può caricare, visualizzare in anteprima e utilizzare una serie di file 3D di base, tra cui file OBJ, STL, GLTF e GLB. Aggiungendo [!DNL Dynamic Media], puoi configurare e distribuire esperienze 3D utilizzando URL agnostici o visualizzatori. Tra questi sono inclusi un Visualizzatore di esperienza 3D [!DNL Dynamic Media], un componente Visualizzatore 3D di Sites e la possibilità di distribuire file 3D tramite [!DNL Dynamic Media] (AR/VR). Consulta [Utilizzo delle risorse 3D in Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Supporto di Adobe Asset Link per Adobe XD**

La versione più recente, [!DNL Experience Manager Assets] supporta un nuovo plug-in [!DNL Adobe Asset Link] rilasciato con [!DNL Adobe XD] v29.3. L’integrazione consente ai designer di accedere alle risorse di [!DNL Experience Manager] e utilizzarle nelle proprie progettazioni senza dover uscire dall’applicazione [!DNL Adobe XD]. Consulta la [documentazione Adobe Asset Link per Adobe XD](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link-for-xd.html).

Con questa versione, gli utenti creativi e i designer possono lavorare con le risorse gestite in [!DNL AEM Assets] utilizzando [!DNL Adobe Asset Link] in una serie di app desktop di Creative Cloud, tra cui [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator] e [!DNL InDesign].

**Miglioramenti dell’accessibilità**

[!DNL Adobe Experience Manager Assets] è ora più accessibile in conformità alle linee guida WCAG (Web Content Accessibility Guidelines) v2.1. L’accessibilità è stata migliorata per i seguenti casi di utilizzo o interfacce:

Gli elementi dell’interfaccia utente sono compatibili con gli assistenti vocali, sono accessibili tramite una tastiera e hanno un contrasto migliore. Segue un elenco dettagliato dei miglioramenti:

* Le barre di avanzamento [!UICONTROL Opzioni], [!UICONTROL Ambito] e [!UICONTROL Flussi di lavoro] nella pagina [!UICONTROL Gestisci pubblicazione] non vengono lette dall’assistente vocale come barre di avanzamento. Al contrario, chi usa un assistente vocale percepisce questi indicatori di stato come un elenco di schede. (CQ-4273015)

* Quando si aggiungono dei tag nella pagina [!UICONTROL Proprietà] di una risorsa, gli utenti possono navigare in una struttura ad albero dei tag. La struttura ad albero non è accessibile, in quanto chi usa un assistente vocale non sente nulla durante la navigazione. (CQ-4272964)

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, l’assistente vocale

   * legge le informazioni della tabella non appena viene caricata la finestra di dialogo;
   * non è in grado di navigare su tutti i suggerimenti automatici elencati;
   * non legge i suggerimenti automatici visualizzati per la casella combinata [!UICONTROL Aggiungi indirizzo e-mail/Ricerca]. (CQ-4294232)

* La pagina [!UICONTROL Editor schema metadati] e i relativi elementi sono ora accessibili da tastiera e compatibili con gli assistenti vocali. (CQ-4272953) Gli utenti possono trascinare i componenti utilizzando la tastiera nella modalità Sfoglia di NVDA. (CQ-4296326)

* Nell’interfaccia di Assets, le impostazioni di visualizzazione non sono accessibili dalla tastiera. (CQ-4289038)

* Il rapporto di luminosità è inferiore a 3:1 per le icone di classificazione di colore giallo. È svantaggioso per gli utenti ipovedenti e senza percezione dei colori. Le stelle di valutazione vengono visualizzate nella scheda della risorsa o nella visualizzazione a schede

* Il colore e il contrasto di alcuni elementi dell’interfaccia utente sono stati aggiornati in modo che gli utenti con vista limitata o senza percezione del colore possano distinguere tali elementi. Ad esempio, le icone delle stelle di valutazione nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nelle [!UICONTROL Proprietà] di una risorsa e nella visualizzazione a schede sono ora di un colore con contrasto adeguato. (CQ-4295106)

* Gli assistenti vocali ora possono leggere le voci del menu a comparsa della casella combinata (in vari campi su pagine diverse) come un elenco di opzioni. (CQ-4294017)

* Per applicare un flusso di lavoro a una risorsa, è possibile accedere alla freccia della [!UICONTROL Timeline] tramite una tastiera. (CQ-4289268)

* Gli utenti possono rimuovere i tag selezionati nel campo [!UICONTROL Tag] della scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa utilizzando il simbolo `x`. Gli assistenti vocali ora leggono lo scopo e il numero dei tag selezionati. (CQ-4273033)

* I campi modulo di sola lettura possono essere attivati utilizzando una tastiera. Ad esempio, i campi disattivati nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa. (CQ-4273031)

* È ora possibile accedere alle opzioni per filtrare le risorse nella barra laterale sinistra utilizzando una tastiera. (CQ-4273018)

* L’assistente vocale legge lo scopo di vari elementi della casella combinata, ad esempio il campo Percorso, e l’opzione per aprire la finestra di dialogo Selezione nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa. (CQ-4273016)

* I controlli del volume per i video sono accessibili tramite una tastiera. (CQ-4272696)

* Molte opzioni attivabili nell’interfaccia di Assets non indicano se sono attive quando si utilizza la tastiera. (CQ-4272694)

* Gli utenti che utilizzano gli assistenti vocali ora sanno quando le righe nella vista a elenco sono selezionabili utilizzando una tastiera. Queste informazioni vengono lette quando si passa il cursore sulle righe. (CQ-4271824)

* Alcuni campi modulo, come nome utente e password nella pagina di accesso, si basano sui valori dei segnaposto per assegnare un’etichetta accessibile. (CQ-4271716)

* È ora possibile accedere da tastiera agli elementi interattivi dell’interfaccia, ad esempio collegamenti e opzioni (opzioni di intestazione e zoom della pagina delle risorse o navigazione delle cartelle). (CQ-4271412)

* I titoli di tutte le pagine visualizzate in [!DNL Adobe Experience Manager] Assets ora sono univoci. (CQ-4271409)

**Altri miglioramenti**

La versione include i seguenti ulteriori miglioramenti:

* Possibilità di rielaborare le risorse con profili di elaborazione delle risorse, offrendo così agli utenti il controllo completo del processo (elaborazione completa delle risorse, applicazione di un profilo di elaborazione specifico ed eventuale esecuzione di un flusso di lavoro di post-elaborazione).
* Le query di ricerca ora restituiscono i risultati più rapidamente quando l’istanza del cluster sottostante viene riavviata dietro le quinte (in un caso simile, l’esecuzione della ricerca iniziale poteva durare più a lungo prima).
* È possibile ordinare per “Nome” le risorse nella vista a elenco nell’interfaccia di Assets e nei risultati di ricerca. Consulta [Cercare le risorse](/help/assets/search-assets.md#sort).
* È possibile ordinare per &quot;Creato&quot; (data) le risorse nella vista a elenco nell’interfaccia di Assets e nei risultati di ricerca. Consulta [Cercare le risorse](/help/assets/search-assets.md#sort).
* Supporto per la conversione di file EPS in immagini tramite i microservizi delle risorse.

### Correzioni di bug {#assets-bug-fixes}

Oltre alle nuove funzioni di cui sopra, la versione corrente fornisce le correzioni di bug seguenti in base ai feedback ricevuti dai clienti su [!DNL Assets].

* Per i file di musica MP3, il pulsante di riproduzione visualizzato sulla miniatura nell’anteprima DAM non funziona. (CQ-4294731)
* Passando il puntatore del mouse sulla vista a schede, lo schermo scorre in seguito all’attivazione (automatica) dell’area delle azioni rapide disponibili nella scheda. (GRANITE-26895)
* La visualizzazione di un numero eccessivo di immagini dopo lo scorrimento di numerosi risultati di ricerca provoca l’arresto anomalo del browser. (GRANITE-26432)
* Quando si scarica una risorsa, se è selezionata l’opzione e-mail e viene fornito un ID e-mail valido, l’opzione di download non è disponibile. (CQ-4296535)
* I filtri personalizzati salvati come raccolte avanzate non vengono applicati correttamente alle risorse. (CQ-4294942)
* Sono stati introdotti numerosi miglioramenti a livello di ricerca e indicizzazione e correzioni di bug per migliorare le prestazioni. (CQ-4286373)
* Non è possibile accedere alla scheda delle proprietà della cartella in Assets e restituisce un errore 500. (CQ-4295701)
