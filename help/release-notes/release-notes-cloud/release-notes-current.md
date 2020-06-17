---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.6.0'
description: Note sulla versione 2020.6.0 di Experience Manager
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 7%

---


# Note sulla versione di AEM as a Cloud Service 2020.6.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.6.0.

## Data di rilascio {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.6.0 is June 04, 2020.

## Novità di AEM Sites {#aem-sites}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di AEM Sites in AEM as a Cloud Service, versione 2020.6.0.

### Novità {#whats-new-2020.6.0}

La release 2.9.0 dei componenti [](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) core è ora disponibile come parte di AEM Sites tra cui:

* Integrazione tra [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer) e i componenti core
* Attributi ID HTML configurabili per tutti i componenti
* Nuovo componente Barra di avanzamento
* Numerose correzioni di bug

### Correzioni di bug {#sites-bug-fixes}

* I componenti all&#39;interno del Contenitore di layout non sono visibili quando il Contenitore di layout viene copiato e incollato di nuovo su una pagina.

* È stato corretto un problema con il ridimensionamento del componente di layout.

* È stata aggiunta la possibilità di gestire il routing delle sole pagine Angular e delle pagine AEM/Angular.

### Accessibilità {#accessibility}

* Ruolo e stato di commento sono ora possibili per gli elementi Masoneria nella finestra di dialogo **Crea pagina** mentre si naviga in modalità di navigazione tramite la freccia rivolta verso il basso.

* È stato aggiunto un collegamento nella navigazione per consentire agli utenti di passare al contenuto principale.

* Miglioramenti dell&#39;assistente vocale.

## Novità nelle Fondazioni di AEM come Cloud Service {#foundations}

I tempi di creazione dei progetti AEM miglioreranno rimuovendo tutti i riferimenti nel file pom.xml del progetto AEM nell’archivio remoto `https://downloads.experiencecloud.adobe.com/content/maven/public`.

AEM come Cloud Service SDK API Jar, che in precedenza era ospitato in quella posizione, ora si trova in Maven Central, l&#39;archivio degli artifact predefinito di Maven.

## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.6.0.

### Novità {#what-is-new-cloud-manager}

* Un utente con il ruolo *Business Owner* in Cloud Manager è ora in grado di eliminare un programma sandbox dalla pagina di destinazione (tramite il pulsante di azione rapida sulla scheda Program) o dall&#39;interno del programma.

   Per ulteriori informazioni, vedere [Eliminazione di un programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) sandbox.

* Un utente del programma sandbox nel ruolo *Business Owner* o *Deployment Manager* in Cloud Manager è ora in grado di eliminare l&#39;ambiente di produzione e di fase impostato tramite l&#39;interfaccia utente di Cloud Manager. L&#39;opzione di eliminazione è ora disponibile dalla scheda Ambiente nella pagina Panoramica **** programmi e nella pagina **Ambienti** . Selezionando l&#39;opzione di eliminazione su Produzione o Stage, viene eliminato anche l&#39;altro nel set.

   Per ulteriori informazioni, vedere [Eliminazione di un programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) sandbox.

* Indicatori di supporto sulla pagina di destinazione per informare e informare l’utente sulla navigazione di base.

* Indicatori di supporto nella pagina Panoramica **del** programma per informare e informare l&#39;utente sulla navigazione di base in Cloud Manager per avviarla.

* Una pagina **LEARN** è ora disponibile in Cloud Manager, accessibile tramite la navigazione superiore. Questa pagina include risorse per aiutare gli utenti a conoscere i flussi di lavoro più utilizzati in base ai loro ruoli assegnati in Cloud Manager.

* I programmi sandbox ora sono identificati tramite un contrassegno **sandbox** che verrà visualizzato sulla scheda del programma sulla pagina di destinazione e accanto al nome del programma nella pagina Panoramica **del** programma.

* Un utente con il ruolo SysAdmin ora dispone di un solo clic per accedere al percorso in  Admin Console da cui è possibile gestire i ruoli utente o le autorizzazioni per Cloud Manager. È ora disponibile un pulsante **Gestisci accesso** nella pagina di destinazione accanto al pulsante **Aggiungi programma** .

   Per ulteriori informazioni, consulta Attività [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) SysAdmin.

* Un utente con il ruolo SysAdmin ora ha accesso con un solo clic all&#39;istanza di creazione direttamente da Cloud Manager.

   Per ulteriori informazioni, consultate [Gestione dell&#39;accesso all&#39;istanza](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) Author.

* Il registro Build ora include l&#39;elenco degli artefatti scoperti, inclusi i pacchetti di contenuto saltati.

* Il passaggio Genera ora convalida che tutti i pacchetti di contenuto generati includono tutte le proprietà obbligatorie: nome, gruppo e versione.

* Il passaggio Genera ora convalida che la build produca almeno un pacchetto di contenuto.

### Correzioni di bug {#bug-fixes-cm}

* In alcune situazioni, le icone presenti nella finestra di dialogo **Crea programma** non erano allineate.

* L’identificatore di rilascio di AEM non veniva visualizzato in modo coerente nella pagina Panoramica **dei** programmi.

* Durante la configurazione della pipeline di produzione, l&#39;opzione Distribuzione **** pianificata non era visibile per alcuni clienti.

### Problemi noti {#known-issues-cm}

* Gli ambienti all&#39;interno di un programma sandbox saranno vietati quando non viene rilevata alcuna attività per una certa durata. Questo stato non verrà osservato in Cloud Manager. Tuttavia, lo stato può essere osservato tramite Developer Console. Questo verrà risolto in una prossima release.

* Il collegamento a Developer Console direttamente da Cloud Manager non mostrerà l&#39;opzione per disattivare/attivare l&#39;ambiente di un programma sandbox. Per risolvere questo problema, una volta nella Developer Console, aggiungere il pattern `#release-cm-p1234-e5678` alla fine dell&#39;URL, dove *1234* è l&#39;ID del programma e *5678* è l&#39;ID dell&#39;ambiente. Questo verrà risolto in una prossima release.

## What&#39;s New in [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Esperienza utente guidata per smart tag avanzati avanzati, con tecnologia Adobe Sensei**

I tag avanzati avanzati consentono alle organizzazioni di formare modelli di smart tag in grado di riconoscere le immagini in base ai tag aziendali specifici dei clienti, oltre a smart tag generici.

Con questa versione, è disponibile una nuova esperienza utente guidata che consente di impostare la formazione sugli smart tag per set di tag specifici per i clienti e di formarli con risorse, che in futuro dovranno essere riconosciute e contrassegnate con loro. Questa è un&#39;esperienza più intuitiva.
Train Smart Tags avanzato per una formazione più intuitiva per Smart Tags. Scoprite [come aggiungere smart tag alle risorse](/help/assets/smart-tags.md) e [configurare l’assegnazione di smart tag](/help/assets/smart-tags-configuration.md).

**Supporto per l&#39;assimilazione, l&#39;anteprima e la distribuzione di contenuti 3D**

Le organizzazioni ora possono archiviare e utilizzare file 3D all&#39;interno di AEM Assets. L’utente può caricare, visualizzare in anteprima e sfruttare una serie di file 3D di base, tra cui file .obj, .stl, .gltf e .glb. Con l&#39;aggiunta di [!DNL Dynamic Media]esperienze 3D, possono essere configurate e distribuite tramite URL agnostici o visualizzatori. Questo include un visualizzatore esperienza [!DNL Dynamic Media] 3D, un componente Visualizzatore 3D di siti e la possibilità di distribuire file 3D tramite [!DNL Dynamic Media] (AR/VR). Consultate [Utilizzo delle risorse 3D in Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Supporto di Adobe Asset Link per Adobe XD**

Con la versione più recente, [!DNL Experience Manager Assets] fornisce il supporto per un nuovo [!DNL Adobe Asset Link] plug-in rilasciato con [!DNL Adobe XD] v29.3. L’integrazione consente ai designer di accedere e utilizzare le risorse [!DNL Experience Manager] nelle proprie progettazioni, senza dover uscire dall’ [!DNL Adobe XD] applicazione. Consultate [Adobe Asset Link (Collegamento risorse Adobe) per la documentazione](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html)Adobe XD.

Con questa versione, gli utenti creativi e i designer possono ora lavorare con le risorse gestite [!DNL AEM Assets] utilizzando [!DNL Adobe Asset Link] in una serie di app desktop Creative Cloud, tra cui [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator]e [!DNL InDesign].

**Miglioramenti dell&#39;accessibilità**

[!DNL Adobe Experience Manager Assets] è ora più accessibile in conformità alle linee guida WCAG (Web Content Accessibility Guidelines) v2.1. L&#39;accessibilità è stata migliorata per i seguenti casi di utilizzo o interfacce:

Gli elementi dell&#39;interfaccia utente sono intuitivi per gli assistenti vocali, sono accessibili tramite una tastiera e hanno un contrasto migliore. Segue un elenco dettagliato di miglioramenti:

* Gli indicatori di avanzamento [!UICONTROL Opzioni], [!UICONTROL Ambito]e Flussi di [!UICONTROL lavoro] nella pagina [!UICONTROL Gestisci pubblicazione] non vengono letti dall&#39;assistente vocale come indicatori di avanzamento. Al contrario, gli utenti di utilità di lettura dello schermo percepiscono questi indicatori di stato come un elenco di schede. (CQ-4273015)

* Quando aggiungete tag nella pagina [!UICONTROL Proprietà] di una risorsa, gli utenti possono spostarsi in una struttura ad albero di tag. La struttura ad albero non è accessibile, in quanto gli utenti di utilità di lettura dello schermo non ascoltano nulla durante la navigazione. (CQ-4272964)

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, l’assistente vocale,

   * riporta le informazioni della tabella non appena la finestra di dialogo viene caricata.
   * non è in grado di passare a tutti i suggerimenti automatici elencati.
   * non riporta i suggerimenti automatici visualizzati per la casella combinata [!UICONTROL Aggiungi indirizzo e-mail/Ricerca] . (CQ-4294232)

* La pagina Editor [!UICONTROL schema] metadati e i relativi elementi sono ora accessibili e l&#39;assistente vocale è intuitivo. Le opzioni possono essere utilizzate utilizzando una tastiera. (CQ-4272953) Gli utenti possono trascinare i componenti utilizzando la tastiera in modalità di ricerca NVDA. (CQ-4296326)

* Nell’interfaccia utente di Risorse, le impostazioni di visualizzazione non sono accessibili dalla tastiera. (CQ-4289038)

* Il rapporto di luminosità è inferiore a 3:1 per le icone di classificazione colorate in giallo. Non è utile per gli utenti con visione limitata e senza percezione del colore. Le stelle di valutazione vengono visualizzate nella scheda della risorsa o nella vista a schede

* Il colore e il contrasto di alcuni elementi dell&#39;interfaccia utente vengono aggiornati in modo che gli utenti con visione limitata o senza percezione del colore possano distinguere questi elementi dell&#39;interfaccia utente. Ad esempio, il colore delle icone di valutazione a stella nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] della [!UICONTROL scheda] Proprietàdi una risorsa e nella vista a schede viene modificato per il contrasto appropriato. (CQ-4295106)

* Il menu a comparsa della casella di riepilogo della casella combinata (in vari campi su pagine diverse) ora visualizza le voci come un elenco di opzioni che possono essere annunciate dagli assistenti vocali. (CQ-4294017)

* Per applicare un flusso di lavoro a una risorsa, è possibile accedere alla freccia della [!UICONTROL timeline] tramite una tastiera. (CQ-4289268)

* Gli utenti possono rimuovere i tag selezionati nel campo [!UICONTROL Tag] della scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa utilizzando il `x` simbolo . Lo scopo è stato annunciato dagli assistenti vocali insieme al numero di tag selezionati (CQ-4273033).

* I campi del modulo di sola lettura possono essere concentrati utilizzando una tastiera. Ad esempio, i campi disattivati nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa. (CQ-4273031)

* È possibile accedere alle opzioni per filtrare le risorse nella barra laterale sinistra utilizzando una tastiera. (CQ-4273018)

* Gli assistenti vocali annunciano correttamente lo scopo di vari elementi della casella combinata, come il campo Percorso e l&#39;opzione per aprire la finestra di dialogo di selezione nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa. (CQ-4273016)

* I controlli del volume per i video sono accessibili tramite una tastiera. (CQ-4272696)

* Molte opzioni attivabili sull’interfaccia utente di Risorse non indicano lo stato attivo quando si utilizza la tastiera. (CQ-4272694)

* Gli utenti di utilità di lettura dello schermo ora sanno quando le righe nella vista a elenco sono selezionabili utilizzando una tastiera. Le informazioni vengono annunciate quando si posiziona il puntatore sulle righe. (CQ-4271824)

* Alcuni campi modulo, come il nome utente e la password, si basano sui valori dei segnaposto per assegnare un&#39;etichetta accessibile. (CQ-4271716)

* È ora possibile accedere agli elementi interattivi dell&#39;interfaccia utente, ad esempio collegamenti e opzioni quali le opzioni di intestazione e zoom delle risorse per la navigazione nella pagina o nella cartella tramite una tastiera. (CQ-4271412)

* I titoli di tutte le pagine visualizzate su [!DNL Adobe Experience Manager] Risorse ora sono univoci. (CQ-4271409)

**Altri miglioramenti**

La versione include i seguenti miglioramenti aggiuntivi:

* Possibilità di rielaborare le risorse con i profili di elaborazione delle risorse, per dare agli utenti il controllo completo del processo (esecuzione dell’elaborazione completa delle risorse, applicazione di un profilo di elaborazione specifico e scelta se eseguire il flusso di lavoro di post-elaborazione).
* Le query di ricerca restituiscono i risultati più rapidamente ora che l’istanza del cluster sottostante è stata riavviata dietro le quinte (in questo caso l’esecuzione di ricerca iniziale potrebbe durare più a lungo).
* Ordina per &#39;Nome&#39; quando visualizzate le risorse nella visualizzazione a elenco nell&#39;interfaccia Risorse e nei risultati della ricerca. Consultate [Cercare le risorse](/help/assets/search-assets.md#sort).
* Ordina per &quot;Creato&quot; (data) quando visualizzate le risorse nella vista a elenco nell’interfaccia Risorse e nei risultati della ricerca. Consultate [Cercare le risorse](/help/assets/search-assets.md#sort).
* Supporto per la conversione di file EPS in immagini tramite i microservizi delle risorse.

### Correzioni di bug {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

Oltre alle nuove funzioni di cui sopra, la versione corrente fornisce le seguenti correzioni di bug in base al feedback dei clienti per [!DNL Assets].

* Per i file musicali MP3, il pulsante di riproduzione visualizzato sulla miniatura nell&#39;anteprima DAM non funziona. (CQ-4294731)
* Passando il puntatore del mouse sulla vista a schede, lo schermo scorre in modo automatico in base alle azioni rapide disponibili nella scheda. (GRANITE-26895)
* La visualizzazione di troppe immagini dopo lo scorrimento di un numero elevato di risultati di ricerca provoca l’arresto anomalo del browser. (GRANITE-26432)
* Quando si scarica una risorsa, se è selezionata l’opzione e-mail e anche se è fornito un ID e-mail valido, l’opzione di download non è disponibile. (CQ-4296535)
* I filtri personalizzati salvati come raccolte avanzate non vengono applicati correttamente alle risorse. (CQ-4294942)
* Numerosi miglioramenti a livello di ricerca e indicizzazione e correzioni di bug per migliorare le prestazioni. (CQ-4286373)
