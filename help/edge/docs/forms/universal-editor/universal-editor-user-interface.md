---
title: Informazioni sull’editor universale
description: Questo tutorial ti consentirà rapidamente di utilizzare l’interfaccia dell’editor universale. Ti fornisce una guida alla comprensione dell’interfaccia utente per la creazione di moduli Edge Delivery Services personalizzati nell’editor universale.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 10%

---


# Esplorazione dell’interfaccia dell’editor universale (WYSIWYG)

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) offre un&#39;interfaccia What You See Is What You Get (WYSIWYG) semplice, visiva e intuitiva per Adobe Edge Delivery Services Forms. Fornisce un’interfaccia moderna con funzionalità di trascinamento per l’authoring efficiente dei moduli.

![Interfaccia utente dell’editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Cosa imparerai

Al termine di questa esercitazione:

- Comprendere i componenti principali dell&#39;interfaccia di Universal Editor
- Naviga nelle diverse sezioni dell’interfaccia
- Scopri come accedere e utilizzare gli strumenti essenziali per la creazione di moduli
- Conoscere le scelte rapide da tastiera che aumentano la produttività

## Informazioni sull&#39;interfaccia dell&#39;editor universale

Quando si modifica un modulo utilizzando Universal Editor, la console apre un&#39;interfaccia WYSIWYG interattiva che consente di avviare immediatamente le modifiche. Questa interfaccia fornisce un feedback visivo in tempo reale durante il lavoro, mostrando esattamente come il modulo apparirà agli utenti finali.

>[!NOTE]
>
> Per informazioni sull’authoring dei moduli con l’editor universale, consulta l’articolo [Guida introduttiva di Edge Delivery Services per AEM Forms utilizzando l’editor universale (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interfaccia utente dell’editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

L&#39;interfaccia di Universal Editor è divisa in quattro parti logiche:

- **[A: intestazione di Experience Cloud](#experience-cloud-header)**
- **[B: barra degli strumenti dell’editor universale](#universal-editor-toolbar)**
- **[C: pannello Proprietà](#properties-panel)**
- **[D: editor](#editor)**

Esaminiamo ogni sezione nel dettaglio.

### Intestazione di Experience Cloud

L’intestazione Experience Cloud viene visualizzata nella parte superiore della console e fornisce il contesto di navigazione all’interno dell’ecosistema Adobe Experience Cloud più ampio. Mostra la posizione corrente e consente di accedere rapidamente ad altre applicazioni Experience Cloud.

![Intestazione editor universale Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

Esaminiamo ogni componente:

- **Adobe Experience Cloud**

  Facendo clic sul collegamento **Adobe Experience Cloud** sul lato sinistro della schermata, puoi passare alla directory principale della soluzione Experience Manager. Da qui è possibile accedere ad altri strumenti come Experience Manager Sites, Experience Manager Assets e Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **Nome organizzazione**

  In **Nome organizzazione** viene visualizzato il nome dell&#39;organizzazione del sistema Identity Management (IMS) a cui si è attualmente connessi. Se hai accesso a più organizzazioni, puoi passare da una all’altra utilizzando questo menu a discesa. Ad esempio, nella schermata l’organizzazione IMS attualmente selezionata è &quot;AEM Forms Internal01&quot;.

  ![Organizzazione](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **Guida**

  L’icona Aiuto consente di accedere rapidamente alle risorse di apprendimento e supporto. Questa funzione è particolarmente utile quando devi affrontare una serie di sfide o hai bisogno di assistenza su caratteristiche specifiche. Puoi anche inviare un feedback tramite questa sezione.

  ![Guida](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **Notifiche**

  Nella sezione **Notifiche** viene visualizzato il numero di notifiche incomplete, richieste e attività correnti attualmente assegnate nell&#39;organizzazione IMS. Tieni d’occhio questa sezione per aiutarti a mantenere il tuo flusso di lavoro.

  ![Notifica](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **Soluzioni**

  Il menu **Soluzioni** ti consente di passare ad altre soluzioni Adobe Experience Cloud, semplificando il passaggio da uno strumento all&#39;altro nel flusso di lavoro.

  ![Soluzioni](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **Profilo utente**

  Questa icona mostra le informazioni sul profilo e il nome dell’organizzazione IMS a cui hai effettuato l’accesso. Fai clic su questa icona per accedere alle impostazioni dell’account e alle opzioni di disconnessione.

  ![Autore](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### Barra degli strumenti dell’editor universale

La barra degli strumenti fornisce strumenti essenziali di navigazione e modifica. Consente di spostarsi tra i moduli, pubblicare o annullare la pubblicazione dei moduli, modificare le proprietà dei moduli e accedere all’editor di regole per aggiungere comportamenti dinamici.

![Barra degli strumenti dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Ecco cosa offre ogni componente:

- **Pulsante Home**

  Il pulsante Home consente di tornare alla pagina iniziale di Universal Editor. Questa opzione è utile quando è necessario iniziare a lavorare su un modulo diverso. Puoi anche immettere direttamente un URL nella barra della posizione per passare a qualsiasi modulo desideri modificare.

  ![Pagina Home dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **Barra località**

  La **Barra località** visualizza l&#39;indirizzo del modulo che stai modificando. Per passare a un modulo diverso, fai clic sulla barra della posizione e immetti il relativo URL. La scelta rapida da tastiera per attivare la barra della posizione è `l`.

  ![Barra località](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **Editor di regole**

  L&#39;**Editor regole** consente di aggiungere comportamenti dinamici ai moduli tramite un&#39;interfaccia visiva intuitiva. Consente di creare condizioni, convalide e azioni che rispondono agli input dell&#39;utente, rendendo i moduli interattivi e intelligenti.

  ![Editor di regole](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - Per impostazione predefinita, l’estensione Editor regole non è abilitata in Universal Editor. Per abilitare questa potente funzionalità, contattaci all&#39;indirizzo [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) dal tuo indirizzo e-mail ufficiale.
  > - Per informazioni su come creare e gestire le regole, fare riferimento all&#39;articolo [Introduzione all&#39;editor di regole in WYSIWYG Authoring](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

- **Modifica proprietà modulo**

  L&#39;opzione **Modifica proprietà modulo** consente di configurare importanti impostazioni del modulo, ad esempio il modello dati del modulo (FDM) e la data di pubblicazione. Queste proprietà influenzano il comportamento del modulo e si integrano con i sistemi back-end.

  ![Modifica proprietà modulo](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **Impostazioni intestazione autenticazione**

  L&#39;opzione **Impostazioni intestazione autenticazione** consente di impostare intestazioni di autenticazione personalizzate per lo sviluppo locale. Questa opzione è particolarmente utile quando si esegue il test di moduli che richiedono credenziali di autenticazione.

  ![Intestazione autenticazione](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **Modalità reattiva**

  La funzionalità **Modalità reattiva** consente di verificare come il modulo verrà visualizzato su dispositivi diversi. Per impostazione predefinita, l’editor si apre in layout desktop, ma è possibile passare alla visualizzazione per dispositivi mobili per garantire che il modulo rimanga utilizzabile e interessante sugli schermi più piccoli.

  ![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **Modalità anteprima**

  **Modalità anteprima** mostra il modulo esattamente come apparirà quando verrà pubblicato. In questo modo è possibile interagire con il modulo facendo clic su collegamenti e pulsanti, esattamente come farebbero gli utenti. Questo è un passaggio essenziale prima della pubblicazione per verificare che tutto funzioni come previsto. Consente di passare dalla modalità di modifica alla modalità di anteprima utilizzando la scelta rapida da tastiera `p`.

  ![Anteprima](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **Apri pagina**

  Il pulsante **Apri pagina** apre il modulo in una nuova scheda del browser per l&#39;anteprima. In questo modo è possibile visualizzare il modulo a schermo intero senza l&#39;interfaccia dell&#39;editor. La scelta rapida da tastiera per questa azione è `o`.

  ![Apri pagina](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **Pubblica**

  Quando il modulo è pronto per gli utenti, il pulsante **Pubblica** lo rende disponibile al pubblico. Questo è il passaggio finale nel flusso di lavoro di creazione del modulo.

  ![Pubblica](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **Menu con puntini di sospensione**

  Facendo clic sui puntini di sospensione (...) vengono visualizzate ulteriori opzioni, inclusa la possibilità di **annullare la pubblicazione** di un modulo attualmente attivo. Questa opzione è utile quando è necessario rimuovere temporaneamente un modulo dall&#39;accesso pubblico o sostituirlo con una versione aggiornata.

  ![Puntini di sospensione](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### Pannello Proprietà

Il pannello **Proprietà** viene visualizzato sul lato destro dell&#39;interfaccia e visualizza informazioni contestuali in base a ciò che è stato selezionato nel modulo. Quando non è selezionato alcun componente, viene visualizzata la struttura generale del modulo.

![Pannello Proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

Esaminiamo i suoi componenti chiave:

- **Modalità proprietà**

  La modalità **Proprietà** visualizza le impostazioni e le opzioni per il componente attualmente selezionato. In questo modo è possibile personalizzare singoli elementi del modulo in base a esigenze specifiche. La scelta rapida da tastiera per aprire le proprietà di un componente selezionato è `d`.

  ![Proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **Struttura contenuto**

  La **Struttura contenuto** visualizza la struttura gerarchica del modulo. Questa rappresentazione visiva consente di comprendere il modo in cui i componenti sono nidificati l’uno nell’altro. Facendo clic su un elemento della struttura, questo viene selezionato nell&#39;editor e scorre fino alla posizione corrispondente. Questo è particolarmente utile nelle forme complesse. Attiva/disattiva la visualizzazione struttura contenuto con la scelta rapida da tastiera `f`.

  ![Struttura contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **Generare varianti**

  La funzionalità **Genera varianti** sfrutta l&#39;intelligenza artificiale per creare versioni diverse del modulo in base a prompt specifici. Questo consente di sperimentare diversi approcci e progettazioni senza creare manualmente ogni variante. Le richieste possono essere fornite da Adobe o personalizzate dall’utente.

  ![Generare varianti](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > Per istruzioni dettagliate sull&#39;utilizzo di Genera varianti per i moduli, consulta l&#39;articolo [Genera varianti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/generative-ai/generate-variations).

- **Sperimentazione**

  La funzionalità **Sperimentazione** consente di eseguire test controllati confrontando diversi layout e progettazioni di moduli. Analizzando il modo in cui gli utenti interagiscono con ogni variante, puoi prendere decisioni basate sui dati per ottimizzare i tassi di conversione e l’esperienza utente.

  ![Sperimentazione](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **Personalizzazione**

  Le impostazioni di **Personalization** consentono di connettere i moduli con Adobe Experience Platform (AEP) o applicazioni esterne. Questa connessione consente di creare esperienze di moduli personalizzate in base ai dati e ai comportamenti degli utenti, aumentandone la rilevanza e il coinvolgimento.

  ![Personalizzazione](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **Test A/B**

  **Test A/B** consente di confrontare varianti specifiche del modulo per determinare quali prestazioni sono migliori. A differenza di una sperimentazione più ampia, i test A/B si concentrano in genere sul confronto di elementi specifici o modifiche per identificare l’opzione più efficace.

  ![Test A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **Gestione attività**

  La funzionalità **Gestione attività** semplifica la collaborazione aiutando il team a organizzare, tenere traccia e completare le attività relative alla creazione e all&#39;ottimizzazione dei moduli. In questo modo i progetti progrediscono in modo efficiente con una chiara responsabilità.

  ![Gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **Bozze di contenuto**

  La funzionalità **Bozze di contenuto** consente di creare e salvare versioni preliminari di elementi di testo nel modulo. È possibile creare bozze utilizzando il testo del modulo esistente o iniziare da zero, quindi modificarle o eliminarle in base alle esigenze. Per impostazione predefinita, vengono visualizzate tre bozze, ma facendo clic su **Mostra tutto** vengono visualizzate altre bozze.

  ![Bozze di contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **Origine dati**

  L&#39;opzione **Data Source** consente di configurare e selezionare le origini dati per il modello dati del modulo (FDM). Questa integrazione rende disponibili per l’utilizzo nel modulo tutti gli oggetti, le proprietà e i servizi del modello dati provenienti dalle origini selezionate, consentendo il recupero e l’invio dinamici dei dati.

  ![Origine dati](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **Aggiungi**

  Il pulsante **Aggiungi** mostra un elenco a discesa di componenti che è possibile aggiungere al contenitore attualmente selezionato. Ad esempio, quando è selezionata una sezione Modulo adattivo, questo elenco mostra tutti i componenti che possono essere aggiunti a tale sezione. La scelta rapida da tastiera per aprire l&#39;elenco dei componenti è `a`.

  ![Aggiungi icona](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **Duplica**

  L&#39;opzione **Duplica** crea una copia esatta del componente selezionato. In questo modo si risparmia tempo quando sono necessari più elementi simili, poiché è possibile duplicare e quindi modificare invece di creare da zero.

  ![Icona duplicata](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **Elimina**

  L&#39;opzione **Elimina** rimuove il componente selezionato dal modulo. Presta attenzione quando utilizzi questa opzione, in quanto rimuove immediatamente l’elemento senza una richiesta di conferma.

  ![Elimina](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### Editor

L&#39;editor è l&#39;area di lavoro centrale in cui è possibile creare e modificare il modulo. Visualizza il modulo specificato nella barra delle posizioni e offre un&#39;esperienza WYSIWYG che mostra esattamente come il modulo verrà visualizzato agli utenti. In modalità anteprima, è possibile interagire con il modulo come farebbero gli utenti, testando la navigazione tramite pulsanti e collegamenti.

![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

Nell’editor viene dedicata la maggior parte del tuo tempo, aggiungendo componenti, configurandone le proprietà e disponendoli in modo da creare un’esperienza di modulo intuitiva ed efficace.

## Riepilogo scelte rapide da tastiera

Per aumentare la produttività, tenere presenti le scelte rapide da tastiera:

- `l` - Attiva la barra della posizione
- `p` - Passa dalla modalità di modifica a quella di anteprima
- `o` - Apri il modulo in una nuova scheda
- `d` - Apri proprietà del componente selezionato
- `f` - Attiva/disattiva la visualizzazione struttura contenuto
- `a` - Apre l&#39;elenco di componenti da aggiungere


