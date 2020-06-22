---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.6.0'
description: Note sulla versione 2020.6.0 di Experience Manager
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 61%

---


# Note sulla versione di AEM as a Cloud Service 2020.6.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.6.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Experience Manager] as a Cloud Service 2020.6.0 è il 4 giugno 2020.

## Novità di AEM Sites {#aem-sites}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di AEM Sites in AEM as a Cloud Service, versione 2020.6.0.

### Novità {#whats-new-2020.6.0}

La release 2.9.0 dei componenti [](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) core è ora disponibile come parte di AEM Sites tra cui:

* Integrazione tra [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer) e i componenti core
* Attributi ID HTML configurabili per tutti i componenti
* Nuovo componente Barra di avanzamento
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

La creazione dei progetti AEM risulterà più rapida grazie alla rimozione di tutti i riferimenti all’archivio remoto `https://downloads.experiencecloud.adobe.com/content/maven/public` nel file pom.xml del progetto AEM.

Il Jar dell’API SDK di AEM as a Cloud Service, in precedenza ospitato in tale percorso, ora si trova in Maven Central, l’archivio degli artefatti predefinito di Maven.

## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.6.0.

### Novità {#what-is-new-cloud-manager}

* Un utente con il ruolo *Proprietario business* in Cloud Manager è ora in grado di eliminare un programma sandbox dalla pagina di destinazione (tramite il pulsante di azione rapida nella scheda Programma) o dall’interno del programma.

   Per ulteriori informazioni, vedere [Eliminazione di un programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) sandbox.

* Un utente del programma sandbox con il ruolo di *Proprietario business* o *Manager implementazione* in Cloud Manager è ora in grado di eliminare l’ambiente di produzione e stage impostato tramite l’interfaccia di Cloud Manager. The delete option is now available from both the Environment card on the **Programs Overview** page as well as the **Environments** page. Selezionando l’opzione Elimina in Produzione o Stage, viene eliminato anche l’altro nel set.

   Per ulteriori informazioni, vedere [Eliminazione di un programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) sandbox.

* Delle descrizioni sulla pagina di destinazione forniscono all’utente istruzioni di base sulla navigazione.

* Coach marks on the **Program Overview** page to inform and instruct the user about basic navigation inside Cloud Manager to get them started.

* Cloud Manager ora presenta una pagina **SCOPRI**, accessibile tramite la navigazione superiore. Questa pagina include risorse per aiutare gli utenti a conoscere i flussi di lavoro più utilizzati in base ai loro ruoli assegnati in Cloud Manager.

* Sandbox Programs are now identified by means of a **Sandbox** badge that will be displayed on the program card on the landing page as well as next to the program name in the **Program Overview** page.

* Un utente con il ruolo SysAdmin ora ha accesso con un solo clic alla posizione in Admin Console da cui è possibile gestire i ruoli o le autorizzazioni degli utenti per Cloud Manager. A **Manage Access** button is now available on the landing page next to the **Add Program** button.

   Per ulteriori informazioni, consulta Attività [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) SysAdmin.

* Un utente con il ruolo SysAdmin ora ha accesso con un solo clic all&#39;istanza di creazione direttamente da Cloud Manager.

   Per ulteriori informazioni, consultate [Gestione dell&#39;accesso all&#39;istanza](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) Author.

* Il registro Build ora include l’elenco degli artefatti individuati, inclusi i pacchetti di contenuti saltati.

* Il passaggio Build ora verifica se tutti i pacchetti di contenuto generati includono tutte le proprietà obbligatorie: nome, gruppo e versione.

* Il passaggio Build ora verifica se la build ha prodotto almeno un pacchetto di contenuto.

### Correzioni di bug {#bug-fixes-cm}

* In alcune situazioni, le icone nella finestra di dialogo **Crea programma** non erano allineate.

* The AEM release identifier was not consistently displayed on the **Programs Overview** page.

* Durante la configurazione della pipeline di produzione, l’opzione **Scheduled Deployment** (Implementazione pianificata) non era visibile per alcuni clienti.

### Problemi noti {#known-issues-cm}

* Gli ambienti di un programma sandbox vengono ibernati se non viene rilevata alcuna attività per un certo periodo di tempo. Questo stato non sarà osservato in Cloud Manager. Tuttavia, lo stato può essere osservato tramite la Console per sviluppatori. Questo problema sarà risolto in una versione successiva.

* Il collegamento alla Console per sviluppatori direttamente da Cloud Manager non mostra l’opzione per ibernare/riattivare l’ambiente di un programma sandbox. Per risolvere questo problema, una volta nella Console per sviluppatori, aggiungi il pattern `#release-cm-p1234-e5678` alla fine dell’URL, dove *1234* è l’ID del programma e *5678* è l’ID dell’ambiente. Questo problema sarà risolto in una versione successiva.

## Novità di [!DNL Adobe Experience Manager Assets] {#aem-assets}

**User experience guidata per tag avanzati migliorati, basati su Adobe Sensei**

I tag avanzati migliorati consentono di addestrare modelli di assegnazione tag avanzati per riconoscere le immagini in base a tag aziendali specifici, oltre che ai tag avanzati generici.

Con questa versione, è disponibile una nuova user experience guidata che consente di impostare l’addestramento di tag avanzati per set di tag specifici dei clienti e di addestrarli con risorse che in futuro dovranno essere riconosciute e a cui dovranno essere assegnati i tag. Si tratta di un’esperienza più intuitiva.
Addestra i tag avanzati migliorati in modo più intuitivo. Scoprite [come aggiungere smart tag alle risorse](/help/assets/smart-tags.md) e [configurare l’assegnazione di smart tag](/help/assets/smart-tags-configuration.md).

**Supporto per l’acquisizione, l’anteprima e la distribuzione di contenuti 3D**

Le organizzazioni ora possono archiviare e utilizzare file 3D in AEM Assets. L’utente può caricare, visualizzare in anteprima e sfruttare una serie di file 3D di base, tra cui file .obj, .stl, .gltf e .glb. Con l’aggiunta di [!DNL Dynamic Media], le esperienze 3D possono essere configurate e distribuite tramite URL o visualizzatori agnostici. Tra questi sono inclusi un Visualizzatore di esperienza 3D [!DNL Dynamic Media], un componente Visualizzatore 3D di Sites e la possibilità di distribuire file 3D tramite [!DNL Dynamic Media] (AR/VR). Consultate [Utilizzo delle risorse 3D in Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Supporto di Adobe Asset Link per Adobe XD**

Con la versione più recente, [!DNL Experience Manager Assets] fornisce il supporto per un nuovo [!DNL Adobe Asset Link] plug-in rilasciato con [!DNL Adobe XD] v29.3. L’integrazione consente ai designer di accedere e utilizzare le risorse [!DNL Experience Manager] nelle proprie progettazioni, senza dover uscire dall’ [!DNL Adobe XD] applicazione. Consultate [Adobe Asset Link (Collegamento risorse Adobe) per la documentazione](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html)Adobe XD.

Con questa versione, gli utenti creativi e i designer possono ora lavorare con le risorse gestite [!DNL AEM Assets] utilizzando [!DNL Adobe Asset Link] in una serie di app desktop Creative Cloud, tra cui [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator]e [!DNL InDesign].

**Miglioramenti dell’accessibilità**

[!DNL Adobe Experience Manager Assets] è ora più accessibile in conformità alle linee guida WCAG (Web Content Accessibility Guidelines) v2.1. L’accessibilità è stata migliorata per i seguenti casi di utilizzo o interfacce:

Gli elementi dell&#39;interfaccia utente sono intuitivi per gli assistenti vocali, sono accessibili tramite una tastiera e hanno un contrasto migliore. Segue un elenco dettagliato di miglioramenti:

* Gli indicatori di avanzamento [!UICONTROL Opzioni], [!UICONTROL Ambito] e [!UICONTROL Flussi di lavoro] nella pagina [!UICONTROL Gestisci pubblicazione] non vengono letti dall’assistente vocale come indicatori di avanzamento. Al contrario, chi usa un assistente vocale percepisce questi indicatori di stato come un elenco di schede. (CQ-4273015)

* Quando si aggiungono dei tag nella pagina [!UICONTROL Proprietà] di una risorsa, gli utenti possono navigare in una struttura ad albero dei tag. La struttura ad albero non è accessibile, in quanto chi usa un assistente vocale non sente nulla durante la navigazione. (CQ-4272964)

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, l’assistente vocale

   * legge le informazioni della tabella non appena la finestra di dialogo viene caricata;
   * non è in grado di navigare su tutti i suggerimenti automatici elencati:
   * non legge i suggerimenti automatici visualizzati per la casella combinata [!UICONTROL Aggiungi indirizzo e-mail/Ricerca]. (CQ-4294232)

* La pagina Editor [!UICONTROL schema] metadati e i relativi elementi sono ora accessibili e l&#39;assistente vocale è intuitivo. Le opzioni possono essere utilizzate utilizzando una tastiera. (CQ-4272953) Gli utenti possono trascinare i componenti utilizzando la tastiera in modalità di ricerca NVDA. (CQ-4296326)

* Nell’interfaccia di Assets, le impostazioni di visualizzazione non sono accessibili dalla tastiera. (CQ-4289038)

* Il rapporto di luminosità è inferiore a 3:1 per le icone di classificazione colorate in giallo. È svantaggioso per gli utenti ipovedenti e senza percezione dei colori. Le stelle di valutazione vengono visualizzate nella scheda della risorsa o nella vista a schede

* Il colore e il contrasto di alcuni elementi dell&#39;interfaccia utente vengono aggiornati in modo che gli utenti con visione limitata o senza percezione del colore possano distinguere questi elementi dell&#39;interfaccia utente. Ad esempio, il colore delle icone di valutazione a stella nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] della [!UICONTROL scheda] Proprietàdi una risorsa e nella vista a schede viene modificato per il contrasto appropriato. (CQ-4295106)

* Il menu a comparsa della casella di riepilogo della casella combinata (in vari campi su pagine diverse) ora visualizza le voci come un elenco di opzioni che possono essere annunciate dagli assistenti vocali. (CQ-4294017)

* Per applicare un flusso di lavoro a una risorsa, è possibile accedere alla freccia della [!UICONTROL timeline] tramite una tastiera. (CQ-4289268)

* Gli utenti possono rimuovere i tag selezionati nel campo [!UICONTROL Tag] della scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa utilizzando il `x` simbolo . Lo scopo è stato annunciato dagli assistenti vocali insieme al numero di tag selezionati (CQ-4273033).

* I campi del modulo di sola lettura possono essere concentrati utilizzando una tastiera. Ad esempio, i campi disattivati nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa. (CQ-4273031)

* È possibile accedere alle opzioni per filtrare le risorse nella barra laterale sinistra utilizzando una tastiera. (CQ-4273018)

* The purpose of various combo box elements such as Path field and the option to open Selection dialog in [!UICONTROL Basic] tab of an asset&#39;s [!UICONTROL Properties] page are now correctly announced by screen readers. (CQ-4273016)

* I controlli del volume per i video sono accessibili tramite una tastiera. (CQ-4272696)

* Molte opzioni attivabili nell’interfaccia di Assets non indicano se sono attive quando si utilizza la tastiera. (CQ-4272694)

* Gli utenti di utilità di lettura dello schermo ora sanno quando le righe nella vista a elenco sono selezionabili utilizzando una tastiera. Le informazioni vengono annunciate quando si posiziona il puntatore sulle righe. (CQ-4271824)

* Alcuni campi modulo, come il nome utente e la password, si basano sui valori dei segnaposto per assegnare un&#39;etichetta accessibile. (CQ-4271716)

* È ora possibile accedere agli elementi interattivi dell&#39;interfaccia utente, ad esempio collegamenti e opzioni quali le opzioni di intestazione e zoom delle risorse per la navigazione nella pagina o nella cartella tramite una tastiera. (CQ-4271412)

* I titoli di tutte le pagine visualizzate in [!DNL Adobe Experience Manager] Assets ora sono univoci. (CQ-4271409)

**Altri miglioramenti**

La versione include i seguenti miglioramenti aggiuntivi:

* Possibilità di rielaborare le risorse con profili di elaborazione delle risorse, offrendo così agli utenti il controllo completo del processo (elaborazione completa delle risorse, applicazione di un profilo di elaborazione specifico ed eventuale esecuzione di un flusso di lavoro di post-elaborazione).
* Le query di ricerca ora restituiscono i risultati più rapidamente quando l’istanza del cluster sottostante viene riavviata dietro le quinte (in un caso simile, l’esecuzione della ricerca iniziale poteva durare più a lungo prima).
* È possibile ordinare per “Nome” le risorse nella vista a elenco nell’interfaccia di Assets e nei risultati di ricerca. Consultate [Cercare le risorse](/help/assets/search-assets.md#sort).
* È possibile ordinare per “Creato” (data) le risorse nella vista a elenco nell’interfaccia di Assets e nei risultati di ricerca. Consultate [Cercare le risorse](/help/assets/search-assets.md#sort).
* Supporto per la conversione di file EPS in immagini tramite i microservizi delle risorse.

### Correzioni di bug {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

In addition to the above new features, the current release provides the following bug fixes based on customer feedback for [!DNL Assets].

* Per i file di musica MP3, il pulsante di riproduzione visualizzato sulla miniatura nell’anteprima DAM non funziona. (CQ-4294731)
* Passando il puntatore del mouse sulla vista a schede, lo schermo scorre in seguito all’attivazione (automatica) dell’area delle azioni rapide disponibili nella scheda. (GRANITE-26895)
* La visualizzazione di un numero eccessivo di immagini dopo lo scorrimento di un numero elevato di risultati di ricerca provoca l’arresto anomalo del browser. (GRANITE-26432)
* Quando si scarica una risorsa, se è selezionata l’opzione e-mail e viene fornito un ID e-mail valido, l’opzione di download non è disponibile. (CQ-4296535)
* I filtri personalizzati salvati come raccolte avanzate non vengono applicati correttamente alle risorse. (CQ-4294942)
* Sono stati introdotti numerosi miglioramenti a livello di ricerca e indicizzazione e correzioni di bug per migliorare le prestazioni. (CQ-4286373)
