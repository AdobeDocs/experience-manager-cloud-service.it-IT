---
title: Abilitare AEM Screens per il tuo sito demo
description: Scopri i passaggi per abilitare l’esperienza completa di AEM Screens as a Cloud Service sul tuo sito demo.
exl-id: 369eea9f-2e81-4b87-841c-188b67657bab
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 96%

---

# Abilitare AEM Screens per il tuo sito demo {#enable-screens}

Scopri i passaggi per abilitare l’esperienza completa di AEM Screens as a Cloud Service sul tuo sito demo.

>[!NOTE]
>
>AEM Screens Demo richiede l’aggiunta del componente aggiuntivo Screens al programma Cloud Manager. Scopri [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/adding-screens-addon/add-on-new-program-screens-cloud.html) come aggiungerlo.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di AEM Reference Demos Add-On, con [Crea sito demo,](create-site.md) hai creato un nuovo sito demo basato sui modelli di Reference Demo Add-On. Ora dovresti:

* Comprendere come accedere all’ambiente di authoring AEM.
* Conoscere come creare un sito basato su un modello.
* Comprendere le nozioni di base per navigare nella struttura del sito e modificare una pagina.

Adesso che disponi di un sito demo per esplorare e comprendere gli strumenti disponibili per aiutarti a gestirlo, puoi abilitare l’esperienza completa di AEM Screens as a Cloud Service per i siti demo.

## Obiettivo {#objective}

AEM Reference Demos Add-On contiene i contenuti AEM Screens per We.Cafe, una caffetteria verticale. Questo documento spiega come eseguire la configurazione demo di We.Cafe nel contesto di AEM Screens. Dopo la lettura dovresti:

* Conoscere le nozioni di base di AEM Screens.
* Comprendere il contenuto demo di We.Cafe.
* Sapere come configurare AEM Screens per We.Cafe.
   * Conoscere come creare un progetto Screens per We.Cafe.
   * Essere in grado di configurare un servizio meteo simulato utilizzando i fogli e gli API di Google.
   * Simulare la modifica dinamica del contenuto di Screens in base al “servizio meteo“.
   * Installare e utilizzare il lettore Screens.

## Comprendere Screens {#understand-screens}

AEM Screens as a Cloud Service è una soluzione di segnaletica digitale che consente ai professionisti del marketing di creare e gestire esperienze digitali dinamiche su larga scala. Con AEM Screens as a Cloud Service, puoi creare esperienze di segnaletica digitale coinvolgenti e dinamiche destinate a essere utilizzate negli spazi pubblici.

>[!TIP]
>
>Per informazioni complete su AEM Screens as a Cloud Service, consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine del presente documento.

Installando AEM Reference Demos Add-On, il contenuto We.Cafe per AEM Screens sarà disponibile automaticamente nell’ambiente di authoring demo. I passaggi descritti in [Distribuzione di un progetto Screens demo](#deploy-project) ti consentono di abilitare l’esperienza AEM Screens completa pubblicando tale contenuto e distribuendolo ai lettori multimediali, ecc.

## Comprendere il contenuto della demo {#demo-content}

La caffetteria We.Cafe è composta da tre negozi che si trovano in tre sedi negli Stati Uniti. I tre negozi hanno tre esperienze simili:

* Una bacheca del menu sopra il bancone con due o tre pannelli verticali
* Un espositore all’ingresso rivolto verso la strada con un pannello orizzontale o verticale che invita i clienti a entrare nel negozio
* Una postazione chiosco per ordinazioni fai da te rapide per evitare la coda con un tablet verticale

>[!NOTE]
>
>Nella versione corrente della demo può essere testato solamente l’espositore all’ingresso. Gli altri espositori lo saranno in una versione futura.
>
>Nella versione corrente della demo il chiosco non è incluso. Sarà incluso in una versione futura.

Si presume che la sede di New York sia in un negozio più piccolo che non ha molto spazio, e come tale:

* La bacheca del menu ha solo due pannelli verticali invece di tre come per San Francisco e San Jose
* L’espositore all’ingresso è posizionato verticalmente anziché orizzontalmente

>[!NOTE]
>
>Se decidi di connetterti a Screens Cloud Service nella sezione [Connessione a Screens as a Cloud Service](#connect-screens), crea le sedi come cartelle in visualizzazioni. Per ulteriori informazioni sulle visualizzazioni, consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine del presente documento.

### Layout delle caffetterie {#care-layouts}

Le sedi di We.Cafe hanno i seguenti layout.

![Layout di We.Cafe](assets/cafe-layouts.png)

>[!NOTE]
>
>Le misurazioni delle schermate sono in pollici.

### Ingresso {#entrance}

L’ingresso è suddiviso in base al giorno e la prima immagine verrà cambiata dal mattino al pomeriggio. Su ogni passaggio della sequenza, verrà pubblicizzata anche una preparazione speciale del caffè diversa, utilizzando una sequenza incorporata controllata per riprodurre un elemento diverso ogni volta.

Anche sull’ultima immagine sui canali dell’ingresso viene eseguito il targeting (cioè viene modificata dinamicamente) in base alla temperatura esterna che può essere simulata nel modo descritto nella [Crea un’origine dati simulata](#data-source).

## Distribuire un progetto Screens demo {#deploy-project}

Per utilizzare il contenuto demo nella sandbox creata in [Crea programma](create-program.md) passaggio, un sito deve essere creato in base a un modello.

Se non hai già creato un sito demo We.Cafe, segui semplicemente gli stessi passaggi della sezione [Crea un sito demo](create-site.md). Quando selezioni il modello, scegli semplicemente il **Modello del sito web We.Cafe**.

![Modello We.Cafe](assets/wecafe-template.png)

Al termine della procedura guidata, troverai il contenuto distribuito in Sites e potrai navigare ed esplorare come qualsiasi altro contenuto.

![Contenuto We.Cafe](assets/wecafe-content.png)

Ora che disponi di contenuti dimostrativi We.Cafe, puoi scegliere come testare AEM Screens:

* Per esplorare solo i contenuti della console AEM Sites, è sufficiente iniziare a esplorare e scoprire di più nella sezione [Risorse aggiuntive](#additional-resources) non è richiesta alcuna ulteriore azione.
* Se desideri utilizzare le funzioni dinamiche complete di AEM Screens, continua con la sezione successiva, [Modifica dinamica del contenuto di Screens.](#dynamically-change)

## Modifica dinamica del contenuto di Screens {#dynamically-change}

Proprio come AEM Sites, AEM Screens può modificare i contenuti in modo dinamico in base al contesto. La demo We.Cafe ha canali configurati per mostrare contenuti diversi a seconda della temperatura corrente. Per simulare ciò, è necessario creare il semplice servizio meteo.

### Creare origine dati simulata {#data-source}

Dato che è molto difficile cambiare il tempo durante una demo o durante la prova, i cambiamenti di temperatura devono essere simulati. Simuleremo un servizio meteo memorizzando un valore di temperatura in un foglio di calcolo di Google Sheet che ContextHub di AEM chiamerà per recuperare la temperatura.

#### Creare chiave API Google {#create-api-key}

Innanzitutto, è necessario creare una chiave API Google per facilitare lo scambio di dati.

1. Accedi a un account Google.
1. Apri la Cloud Console con questo collegamento `https://console.cloud.google.com`.
1. Crea un nuovo progetto facendo clic sul nome del progetto corrente in alto a sinistra nella barra degli strumenti, dopo l’etichetta **Piattaforma Google Cloud**.

   ![Console Google Cloud](assets/google-cloud-console.png)

1. Nella finestra di dialogo del selettore del progetto, fai clic su **NUOVO PROGETTO**.

   ![Nuovo progetto](assets/new-project.png)

1. Assegna un nome al progetto e fai clic su **CREA**.

   ![Crea progetto](assets/create-project.png)

1. Accertati che il nuovo progetto sia selezionato, quindi seleziona **API e servizi** dal menu hamburger della dashboard di Cloud Console.

   ![API e servizi](assets/apis-services.png)

1. Nel pannello a sinistra della finestra API e servizi, fai clic su **Credenziali** nella parte superiore della finestra, quindi fai clic su **CREA CREDENZIALI** e **Chiave API**.

   ![Credenziali](assets/credentials.png)

1. Nella finestra di dialogo, copia la nuova chiave API e salva per un utilizzo successivo. Fai clic su **CHIUDI** per chiudere la finestra di dialogo.

#### Abilita API dei fogli di Google {#enable-sheets}

Per consentire lo scambio di dati dei fogli Google utilizzando la chiave API, devi abilitare l’API Google Sheets.

1. Torna alla console Google Cloud all’indirizzo `https://console.cloud.google.com` per il progetto, quindi utilizza il menu hamburger per selezionare **API e servizi -> Libreria**.

   ![Libreria API](assets/api-library.png)

1. Nella schermata Libreria API, scorri per trovare la ricerca **API dei fogli di Google**. Fai clic su di esso.

   ![Ricerca nella libreria API](assets/api-library-search.png)

1. Nella finestra **API dei fogli di Google** fai clic su **ABILITA**.

   ![API dei fogli di Google](assets/sheets-api.png)

#### Creare un foglio di calcolo Google {#create-spreadsheet}

Ora puoi creare un foglio di calcolo Google Sheets per memorizzare i dati meteo.

1. Vai a `https://docs.google.com` e crea un nuovo foglio di calcolo Google Sheets.
1. Definire la temperatura immettendo `32` nella cella A2.
1. Condividi il documento facendo clic su **Condividi** in alto a destra nella finestra e sotto **Ottieni collegamento** fai click su **Modifica**.

   ![Condividi foglio](assets/share-sheet.png)

1. Copia il collegamento per il passaggio successivo.

   ![Condividi collegamento](assets/share-link.png)

1. Individua l’ID del foglio.

   * L&#39;ID foglio è la stringa casuale di caratteri nel collegamento del foglio copiato dopo `d/` e prima `/edit`.
   * Esempio:
      * Se l’URL è `https://docs.google.com/spreadsheets/d/1cNM7j1B52HgMdsjf8frCQrXpnypIb8NkJ98YcxqaEP30/edit#gid=0`
      * L’ID del foglio è `1cNM7j1B52HgMdsjf8frCQrXpnypIb8NkJ98YcxqaEP30`.

1. Copia l’ID del foglio per utilizzi futuri.

#### Verifica servizio meteo {#test-weather-service}

Dopo aver creato l’origine dati come foglio di calcolo Google Sheets e aver abilitato l’accesso tramite API, testala per assicurarti che il “servizio meteo” sia accessibile.

1. Apri un browser web.

1. Immetti la seguente richiesta, sostituendo l’ID foglio e i valori chiave API salvati in precedenza.

   ```
   https://sheets.googleapis.com/v4/spreadsheets/<yourSheetID>/values/Sheet1?key=<yourAPIKey>
   ```

1. Se ricevi dati JSON simili ai seguenti, impostali correttamente.

   ```json
   {
     "range": "Sheet1!A1:Z1000",
     "majorDimension": "ROWS",
     "values": [
       [],
       [
         "32"
       ]
     ]
   }
   ```

AEM Screens può utilizzare lo stesso servizio per accedere ai dati meteo simulati configurati nel passaggio successivo.

### Configurare ContextHub {#configure-contexthub}

AEM Screens può modificare il contenuto in modo dinamico in base al contesto. La demo We.Cafe dispone di canali configurati per mostrare contenuti diversi a seconda della temperatura corrente sfruttando ContextHub di AEM.

>[!TIP]
>
>Per informazioni complete su ContextHub, consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine del documento.

Quando viene visualizzato il contenuto dello schermo, ContextHub richiamerà il servizio meteo per trovare la temperatura corrente per determinare quale contenuto visualizzare.

A scopo dimostrativo, i valori nel foglio possono essere modificati. ContextHub lo riconoscerà e il contenuto verrà regolato nel canale in base alla temperatura aggiornata.

1. Nell’istanza di authoring di AEMaaCS, vai a **Navigazione globale -> Strumenti -> Siti -> ContextHub**.
1. Seleziona il contenitore di configurazione con lo stesso nome assegnato al progetto quando hai creato il progetto Screens dal **modello del sito web We.Cafe**.
1. Seleziona **Configurazione -> Configurazione ContextHub -> Fogli Google** quindi fai clic su **Successivo** in alto a destra.
1. La configurazione deve avere già dati JSON preconfigurati. È necessario modificare due valori:
   1. Sostituisci `[your Google Sheets id]` con l’ID foglio [che hai salvato in precedenza.](#create-spreadsheet)
   1. Sostituisci `[your Google API Key]` con la chiave API [che hai salvato in precedenza.](#create-api-key)
1. Fai clic su **Salva**.

Ora è possibile modificare il valore della temperatura nel foglio di calcolo di Google Sheet e ContextHub aggiornerà dinamicamente Screens in quanto “vede il cambiamento del tempo”.

### Verifica dati dinamici {#test-dynamic}

Ora che AEM Screens e ContextHub sono connessi al servizio meteo, puoi testarlo per vedere come Screens può aggiornare i contenuti in modo dinamico.

1. Accedi all’istanza di authoring della sandbox.
1. Passa alla console Sites tramite **Navigazione globale -> Sites** e seleziona la pagina seguente **Screens -> &lt;nome progetto> -> Canali -> Ingresso Mattina (Verticale)**.

   ![Selezionare il contenuto del progetto demo](assets/project-content.png)

1. Fai clic su Modifica nella barra degli strumenti o digita il tasto di scelta rapida `e` per modificare la pagina.

1. Nell’editor, puoi visualizzare il contenuto. Tieni presente che un’immagine è evidenziata in blu con un’icona di targeting nell’angolo.

   ![Contenuto di Screens nell’editor](assets/screens-content-editor.png)

1. Modifica la temperatura immessa nel foglio di calcolo da 32 a 70 e osserva come cambia il contenuto.

   ![Contenuto di Screens nell’editor](assets/screens-content-editor-2.png)

In base alla variazione della temperatura da 0°C (32°F) a 21°C (70°F), l’immagine in primo piano cambia da una tazza di tè calda a un caffè freddo.

>[!IMPORTANT]
>
>Utilizza solo la soluzione Google Sheets descritta a scopo dimostrativo. Adobe non supporta l’utilizzo di Google Sheets per ambienti di produzione.

## Connetti Screens as a Cloud Service {#connect-screens}

Se desideri anche configurare un’esperienza di segnaletica digitale reale, incluso un lettore che viene eseguito su un dispositivo di segnaletica digitale o sul computer, segui i passaggi successivi.

In alternativa, è possibile visualizzare in anteprima la demo semplicemente nell’Editor canali su AEMaaCS.

>[!TIP]
>
>Per informazioni dettagliate sull’editor canali, consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine del documento.

### Configurare AEM Screens as a Cloud Service {#configure-screens}

Innanzitutto devi pubblicare il contenuto demo di Screens in AEM Screens as a Cloud Service e configurare il servizio.

1. Pubblica il contenuto del progetto Screens demo.
1. Passa a Screens as a Cloud Service in `https://experience.adobe.com/screens` e accedi.
1. Controlla in alto a destra nella schermata di trovarti nell’organizzazione corretta.

   ![Controlla la tua organizzazione Screens](assets/screens-org.png)

1. In alto a sinistra, fai clic sull’icona a forma di ingranaggio **Modifica impostazioni**.

   ![Modifica impostazioni](assets/screens-edit-settings.png)

1. Fornisci gli URL delle istanze di authoring e pubblicazione di AEMaaCS in cui hai creato il tuo sito demo e fai clic su **Salva**.

   ![Impostazione di Screens](assets/screens-settings.png)

1. Una volta connessi alle istanze demo, Screens estrae il contenuto del canale. Fai clic su **Canali** nel pannello a sinistra per visualizzare i canali pubblicati. La compilazione delle informazioni potrebbe richiedere del tempo. Puoi fare clic sul pulsante blu **Sincronizzazione** in alto a destra dello schermo per aggiornare le informazioni.

   ![Informazioni sul canale demo](assets/screens-channels.png)

1. Fai clic su **Visualizzazioni** nel pannello a sinistra. Al momento non hai ancora creato alcuna visualizzazione per la tua demo. Ciascuna località di We.Cafe verrà simulata creando la rispettiva cartella. Fai clic su **Crea** in alto a destra dello schermo e seleziona **Cartella**.

   ![Crea visualizzazione](assets/screens-displays.png)

1. Nella finestra di dialogo, specifica un nome di cartella come **San Jose** e fai clic su **Crea**.

1. Apri la cartella facendo clic su di essa, fai clic su **Crea** in alto a destra e infine seleziona **Visualizzazione**.

1. Assegna un nome alla visualizzazione e fai clic su **Crea**.

   ![Crea visualizzazione](assets/create-display.png)

1. Dopo aver creato la visualizzazione, fai clic sul nome per aprire la schermata dei dettagli della visualizzazione. È necessario assegnare alla visualizzazione un canale sincronizzato dal sito demo. Fai clic su **Assegna canale** in alto a destra dello schermo.

   ![Dettaglio canale](assets/channel-detail.png)

1. Nella finestra di dialogo, seleziona il canale e fai clic su **Assegna**.

   ![Assegna canale](assets/assign-channel.png)

Puoi ripetere questi passaggi per le località e le visualizzazioni aggiuntive. Una volta completato, hai collegato il tuo sito demo ad AEM Screens e definito la configurazione necessaria.

Puoi visualizzare l’anteprima della demo semplicemente nell’Editor canale su AEMaaCS.

### Utilizzo di Screens Player {#screens-player}

Per visualizzare il contenuto come su un vero schermo, puoi scaricare il lettore e configurarlo localmente. AEM Screens as a Cloud Service in seguito distribuirà il contenuto al lettore

#### Generare un codice di registrazione {#registration-code}

Innanzitutto, devi creare un codice di registrazione per collegare in modo sicuro il lettore ad AEM Screens as a Cloud Service.

1. Passa a Screens as a Cloud Service all’indirizzo `https://experience.adobe.com/screens` ed effettua l’accesso.
1. Controlla in alto a destra nella schermata di trovarti nell’organizzazione corretta.

   ![Controlla la tua organizzazione Screens](assets/screens-org.png)

1. Nel pannello a sinistra, fai clic su **Gestione lettore -> Codici di registrazione** quindi fai clic su **Crea codice** in alto a destra dello schermo.

![Codici di registrazione](assets/registration-codes.png)

1. Immetti un nome per il codice e fai clic su **Crea**.

   ![Crea codice](assets/create-code.png)

1. Una volta creato, il codice viene visualizzato nell’elenco. Fai clic su per copiare il codice.

   ![Codice di registrazione](assets/registration-code.png)

#### Installazione e configurazione lettore {#install-player}

1. Scarica il lettore idoneo per la tua piattaforma da `https://download.macromedia.com/screens/` e installalo.
1. Esegui il lettore e passa alla scheda **Configurazione**, scorri verso il basso per fare clic e confermare sia **Ripristina impostazioni di fabbrica** che **Cambia in modalità cloud**.

   ![Impostazioni lettore](assets/player-configuration.png)

1. Il lettore passa automaticamente alla scheda **Registrazione lettore**. Immetti il codice generato in precedenza e fai clic su **Registra**.

   ![Registrazione lettore](assets/player-registration-code.png)

1. Passa alla scheda **Informazioni di sistema** per verificare l’avvenuta registrazione del lettore.

   ![Lettore registrato](assets/player-registered.png)

#### Assegnare un lettore a un display {#assign-player}

1. Passa a Screens as a Cloud Service alla pagina `https://experience.adobe.com/screens` e accedi.
1. Controlla in alto a destra nella schermata di trovarti nell’organizzazione corretta.

   ![Controlla la tua organizzazione Screens](assets/screens-org.png)

1. Nel pannello a sinistra, fai clic su **Gestione lettore -> Lettori** e vedrai il lettore installato e registrato in precedenza.

   ![Lettori](assets/players.png)

1. Fai clic sul nome del lettore per aprirne i dettagli e quindi su **Assegna visualizzazione** in alto a destra dello schermo.

   ![Assegnare il lettore alla visualizzazione](assets/assign-to-display.png)

1. Nella finestra di dialogo, seleziona la visualizzazione creata in precedenza e fai clic su **Seleziona**.

   ![Assegnare una visualizzazione](assets/assign-a-display.png)

#### Riproduzione! {#playback}

Una volta che hai assegnato una visualizzazione a un lettore, AEM Screens as a Cloud Service distribuisce il contenuto al lettore affinché sia visibile.

![Ingresso verticale](assets/entrance-portrait.jpg)

![Ingresso orizzontale](assets/entrance-landscape.jpg)

## Novità {#what-is-next}

Adesso che hai completato questa parte del percorso di AEM Reference Demo Add-On, dovresti:

* Conoscere le nozioni di base di AEM Screens.
* Comprendere il contenuto demo di We.Cafe.
* Sapere come configurare AEM Screens per We.Cafe.

Adesso sei pronto per esplorare le funzionalità di AEM Screens utilizzando i tuoi siti demo. Prosegui alla sezione successiva del percorso, [Gestire i siti demo,](manage.md) in cui scoprirai gli strumenti disponibili per aiutarti a gestire i siti demo e come rimuoverli.

Puoi consultare alcune delle risorse aggiuntive disponibili nella [Sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Documentazione di ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md): scopri come ContextHub può essere utilizzato per personalizzare il contenuto in base al contesto dell’utente oltre le condizioni meteo.
* [Utilizzo delle chiavi API - Documentazione di Google](https://developers.google.com/maps/documentation/javascript/get-api-key): un riferimento utile per i dettagli sull’utilizzo delle chiavi API di Google.
* [Visualizzazioni](/help/screens-cloud/creating-content/creating-displays-screens-cloud.md): ulteriori informazioni su cosa è una visualizzazione in AEM Screens e cosa è in grado di fare.
* [Scaricare il lettore](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md): scopri come accedere a Screens Player e come installarlo.
* [Registrare il lettore](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md): scopri come configurare e registrare un lettore con il tuo progetto AEM Screens.
* [Assegnazione del lettore a una visualizzazione](/help/screens-cloud/managing-players-registration/assigning-player-display.md): configura un lettore per visualizzare il contenuto.
