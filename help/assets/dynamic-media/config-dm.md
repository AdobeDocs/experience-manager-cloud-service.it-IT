---
title: Configurazione di Dynamic Media Cloud Service
description: Scopri come configurare Dynamic Media in Adobe Experience Manager come Cloud Service.
role: Administrator,Business Practitioner
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '4053'
ht-degree: 4%

---

# Informazioni sulla configurazione del Cloud Service Dynamic Media {#configuring-dynamic-media}

Se utilizzi Adobe Experience Manager per ambienti diversi, ad esempio sviluppo, staging e produzione live, configura i Cloud Services Dynamic Media per ciascuno di tali ambienti.

## Diagramma dell&#39;architettura di Dynamic Media {#architecture-diagram-of-dynamic-media}

Il diagramma di architettura seguente descrive il funzionamento di Dynamic Media.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primaria e delle sincronizzazioni con Dynamic Media per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa sorgente principale viene caricata in Adobe Experience Manager come Cloud Service, viene replicata in Dynamic Media. A questo punto, Dynamic Media gestisce l’elaborazione e la generazione di rendering delle risorse, ad esempio la codifica video e le varianti dinamiche di un’immagine.
1. Dopo la generazione dei rendering, ad Experience Manager come Cloud Service è possibile accedere in modo sicuro e visualizzare in anteprima i rendering remoti di Dynamic Media (nessun file binario viene inviato nuovamente all&#39;Experience Manager come istanza di Cloud Service).
1. Quando il contenuto è pronto per la pubblicazione e l’approvazione, attiva il servizio Dynamic Media per inviare contenuti push ai server di consegna e memorizzare in cache il contenuto nella rete CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>Il seguente elenco di funzioni richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager - Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con queste funzioni.
>
>* [Imaging avanzato](/help/assets/dynamic-media/imaging-faq.md)
>* [Annullamento della validità della cache](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [Protezione del collegamento ipertestuale](/help/assets/dynamic-media/hotlink-protection.md)
>* [Distribuzione HTTP/2 dei contenuti](/help/assets/dynamic-media/http2faq.md)
>* Reindirizzamento URL a livello CDN
>* Akamai ChinaCDN (per una consegna ottimale in Cina)


<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Creazione di una configurazione Dynamic Media nei Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. In Experience Manager come Cloud Service, tocca l’Experience Manager come logo di Cloud Service per accedere alla console di navigazione globale.
1. A sinistra della console, tocca l’icona Strumenti , quindi tocca **[!UICONTROL Cloud Services > Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazione Dynamic Media, nel riquadro a sinistra, tocca **[!UICONTROL global]** (non toccare o selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**). Quindi tocca **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea configurazione Dynamic Media]**, immetti un titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Media, la password, quindi seleziona la tua area geografica. Queste informazioni vengono fornite per Adobe nell’e-mail di provisioning. Se non hai ricevuto questa e-mail, contatta l’Assistenza clienti di Adobe.
1. Fare clic su **[!UICONTROL Connetti a Dynamic Media]**.
1. Nella finestra di dialogo **[!UICONTROL Cambia password]**, immettere una nuova password costituita da 8-25 caratteri nel campo **[!UICONTROL Nuova password]**. La password deve contenere almeno uno dei seguenti elementi:

   * Lettera maiuscola
   * Lettera minuscola
   * Numero
   * Carattere speciale: `# $ & . - _ : { }`

   Il campo **[!UICONTROL Password corrente]** è precompilato intenzionalmente e nascosto dall&#39;interazione.

   Se necessario, per controllare l&#39;ortografia di una password digitata o digitata, tocca l&#39;icona occhio password per visualizzare la password. Toccare nuovamente l’icona per nascondere la password.

1. Nel campo **[!UICONTROL Ripeti password]**, digita nuovamente la nuova password, quindi tocca **[!UICONTROL Fine]**.

   La nuova password viene salvata quando tocchi **[!UICONTROL Salva]** nell&#39;angolo in alto a destra della pagina **[!UICONTROL Crea configurazione Dynamic Media]**.

   Se hai toccato **[!UICONTROL Annulla]** nella finestra di dialogo **[!UICONTROL Cambia password]**, devi comunque immettere una nuova password quando salvi la configurazione di Dynamic Media appena creata.

   Vedere anche [Modifica della password in Dynamic Media](#change-dm-password).

1. Quando la connessione ha esito positivo, è possibile impostare quanto segue:

   | Proprietà | Descrizione |
   |---|---|
   | Azienda | Nome dell&#39;account Dynamic Media. È possibile avere più account Dynamic Media per diversi marchi secondari, divisioni o ambienti di staging/produzione. |
   | Percorso cartella principale della società | Percorso cartella principale della tua azienda. |
   | Pubblicazione delle risorse | Puoi scegliere tra le tre opzioni seguenti:<br>**[!UICONTROL Immediatamente ]**: Quando le risorse vengono caricate, il sistema le acquisisce e fornisce l’URL/da incorporare immediatamente. Non è necessario alcun intervento degli utenti per pubblicare le risorse.<br>**[!UICONTROL All’attivazione]**: Devi pubblicare esplicitamente la risorsa prima prima di fornire un collegamento URL/Incorpora .<br>**[!UICONTROL Pubblicazione ]**selettiva: Le risorse vengono pubblicate automaticamente solo per l’anteprima protetta. Possono anche essere pubblicati esplicitamente in Experience Manager come Cloud Service senza pubblicare in DMS7 per la distribuzione nel dominio pubblico. In futuro, questa opzione intende pubblicare le risorse in Experience Manager as a Cloud Service e pubblicarle in Dynamic Media, escludendovi a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 in modo da poter utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. Oppure puoi pubblicare le risorse esclusivamente in Experience Manager come Cloud Service per l’anteprima; le stesse risorse non vengono pubblicate in DMS7 per la distribuzione nel dominio pubblico. |
   | Server di anteprima protetto | Consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, un Cloud Service come può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Media remote (nessun file binario viene inviato all’Experience Manager come istanza di Cloud Service).<br>A meno che non si disponga di una disposizione speciale per utilizzare il server della propria azienda o un server speciale, Adobe consiglia di lasciare questa impostazione come specificato. |
   | Sincronizza tutti i contenuti | Selezionato per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere in modo selettivo le risorse dalla sincronizzazione con Dynamic Media. Deselezionando questa opzione puoi scegliere tra le due seguenti modalità di sincronizzazione Dynamic Media:<br>**[!UICONTROL Modalità di sincronizzazione Dynamic Media]**<br>**[!UICONTROL Abilita per impostazione predefinita ]**: La configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non si contrassegni una cartella specifica per l’esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabilitata per impostazione predefinita]**: La configurazione non viene applicata ad alcuna cartella finché non contrassegni esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Media.<br>Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Media, seleziona una cartella di risorse, quindi tocca  **[!UICONTROL Proprietà]** nella barra degli strumenti. Nella scheda **[!UICONTROL Dettagli]**, nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione Dynamic Media]** , scegli una delle tre opzioni seguenti. Al termine, tocca **[!UICONTROL Salva]**. *Ricorda: queste tre opzioni non sono disponibili se hai selezionato **Sincronizza tutto il contenuto**in precedenza.* Consulta anche  [Utilizzo della pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Ereditato ]**: Nessun valore di sincronizzazione esplicito nella cartella. La cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per le visualizzazioni ereditate viene visualizzato tramite una descrizione comandi.<br>**[!UICONTROL Abilita per le sottocartelle]**: Includi tutti gli elementi in questa sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono la modalità predefinita nella configurazione cloud.<br>**[!UICONTROL Disabilitata per le sottocartelle ]**: Escludere tutti gli elementi di questa sottostruttura dalla sincronizzazione con Dynamic Media. |

   >[!NOTE]
   >
   >In Dynamic Media non è supportato il controllo delle versioni. Inoltre, l&#39;attivazione ritardata si applica solo se **[!UICONTROL Pubblica risorse]** nella pagina Modifica configurazione Dynamic Media è impostato su **[!UICONTROL All&#39;attivazione]**. E poi, solo fino alla prima attivazione della risorsa.
   >
   >
   >Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale su S7 Delivery.

   ![dynamic icmediaconfiguration2update](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Tocca **[!UICONTROL Salva]**. La nuova password e la nuova configurazione di Dynamic Media viene salvata. Se invece hai toccato **[!UICONTROL Annulla]** , non si verifica alcun aggiornamento della password.
1. Nella finestra di dialogo **[!UICONTROL Configurazione di Dynamic Media]**, tocca **[!UICONTROL OK]** per iniziare la configurazione.

   >[!IMPORTANT]
   >
   >Al termine della nuova configurazione di Dynamic Media, riceverai una notifica di stato all’interno di Experience Manager as a Cloud Service Inbox.
   >
   >Questa notifica della casella in entrata informa se la configurazione ha avuto esito positivo o meno.
   > Per ulteriori informazioni, consulta [Risoluzione dei problemi relativi a una nuova configurazione di Dynamic Media](#troubleshoot-dm-config) e [La tua casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md) .

1. Per visualizzare in anteprima in modo sicuro il contenuto Dynamic Media prima della pubblicazione, per impostazione predefinita, Experience Manager as a Cloud Service utilizza l’autenticazione basata sui token. Tuttavia, puoi anche &quot;inserire nell&#39;elenco Consentiti&quot; più IP per fornire agli utenti l’accesso per visualizzare in anteprima i contenuti in modo sicuro. Per impostare questa azione, procedi come segue: <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

   * Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account. Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti Adobe.
   * Nella barra di navigazione vicino all&#39;angolo superiore destro della pagina, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni pubblicazione]** > **[!UICONTROL Server immagini]**.
   * Nella pagina Pubblica su Image Server, nell&#39;elenco a discesa **[!UICONTROL Contesto pubblicazione]**, selezionare **[!UICONTROL Test Image Serving]**.
   * Per il filtro indirizzi client, tocca **[!UICONTROL Aggiungi]**.
   * Per abilitare (attivare) l’indirizzo, seleziona la casella di controllo, quindi immetti l’indirizzo IP dell’istanza di authoring di Experience Manager (non l’IP di Dispatcher).
   * Fai clic su **[!UICONTROL Salva]**.

La configurazione di base è terminata. sei pronto per utilizzare Dynamic Media.

Se desideri personalizzare ulteriormente la configurazione, puoi eventualmente completare una qualsiasi delle attività descritte in [Configurazione delle impostazioni avanzate in Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Risoluzione dei problemi relativi alla nuova configurazione Dynamic Media {#troubleshoot-dm-config}

Al termine della configurazione di una nuova configurazione di Dynamic Media, riceverai una notifica di stato all’interno di Experience Manager as a Cloud Service Inbox. Questa notifica informa se la configurazione ha avuto esito positivo o meno, come illustrato nelle immagini seguenti dalla casella in entrata.

![Experience Manager Casella in entrata - Completata](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Errore della casella in entrata Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Vedere anche [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md).

**Per risolvere i problemi relativi alla nuova configurazione di Dynamic Media**

1. Nell&#39;angolo in alto a destra dell&#39;Experience Manager come pagina di Cloud Service, tocca l&#39;icona della campana, quindi tocca **[!UICONTROL Visualizza tutto]**.
1. Nella pagina Posta in arrivo, tocca la notifica di successo per leggere una panoramica dello stato e dei registri della configurazione.

   Se la configurazione non è riuscita, tocca la notifica di errore simile alla schermata seguente.

   ![Configurazione Dynamic Media non riuscita](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Nella pagina **[!UICONTROL DMSETUP]**, controlla i dettagli di configurazione che descrivono l&#39;errore. In particolare, prendere nota di eventuali messaggi di errore o codici di errore. Contatta l’Assistenza clienti Adobe con queste informazioni.

   ![Pagina Configurazione Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Modifica della password in Dynamic Media {#change-dm-password}

La scadenza della password in Dynamic Media è impostata a 100 anni dalla data di sistema corrente.

La password deve contenere almeno uno dei seguenti elementi:

* Lettera maiuscola
* Lettera minuscola
* Numero
* Carattere speciale: `# $ & . - _ : { }`

Se necessario, per controllare l&#39;ortografia di una password digitata o digitata, tocca l&#39;icona occhio password per visualizzare la password. Toccare nuovamente l’icona per nascondere la password.

La password modificata viene salvata quando tocchi **[!UICONTROL Salva]** nell&#39;angolo in alto a destra della pagina **[!UICONTROL Modifica configurazione Dynamic Media]**.

1. In Experience Manager come Cloud Service, tocca l’Experience Manager come logo di Cloud Service per accedere alla console di navigazione globale.
1. A sinistra della console, tocca l’icona Strumenti , quindi tocca **[!UICONTROL Cloud Services > Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazione Dynamic Media, nel riquadro a sinistra, tocca **[!UICONTROL global]**. Non toccare o selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**. Quindi, tocca **[!UICONTROL Modifica]**.
1. Nella pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, direttamente sotto il campo **[!UICONTROL Password]**, tocca **[!UICONTROL Modifica password]**.
1. Nella finestra di dialogo **[!UICONTROL Cambia password]**, procedi come segue:

   * Nel campo **[!UICONTROL Nuova password]**, immetti una nuova password.

      Il campo **[!UICONTROL Password corrente]** è precompilato intenzionalmente e nascosto dall&#39;interazione.

   * Nel campo **[!UICONTROL Ripeti password]**, digita nuovamente la nuova password, quindi tocca **[!UICONTROL Fine]**.

1. Nell&#39;angolo in alto a destra della pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, tocca **[!UICONTROL Salva]**, quindi tocca **[!UICONTROL OK]**.

## (Facoltativo) Configurazione delle impostazioni avanzate in Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Per personalizzare ulteriormente la configurazione e la configurazione di Dynamic Media o ottimizzarne le prestazioni, è possibile completare una o più delle seguenti attività *facoltative*:

* [Configurazione e configurazione delle impostazioni di Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Facoltativo) Configurazione e configurazione delle impostazioni Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilizza l’interfaccia utente di Dynamic Media Classic per modificare le impostazioni di Dynamic Media.

Alcune delle attività di cui sopra richiedono l&#39;apertura dell&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi l&#39;accesso al tuo account.

Le attività di configurazione e configurazione includono:

* [Configurazione pubblicazione per Image Server](#publishing-setup-for-image-server)
* [Configurazione delle impostazioni generali dell&#39;applicazione](#configuring-application-general-settings)
* [Configurazione della gestione del colore](#configuring-color-management)
* [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiunta di tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configurazione pubblicazione per Image Server {#publishing-setup-for-image-server}

Le impostazioni di Configurazione pubblicazione determinano il modo in cui le risorse vengono distribuite per impostazione predefinita da Dynamic Media. Se non viene specificata alcuna impostazione, Dynamic Media distribuisce una risorsa in base alle impostazioni predefinite definite in Configurazione pubblicazione. Ad esempio, una richiesta di fornire un’immagine che non include un attributo di risoluzione genera un’immagine con l’impostazione Risoluzione oggetto predefinita.

Per configurare l&#39;impostazione di pubblicazione: in Dynamic Media Classic, fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni pubblicazione > Image Server]**.

La schermata Image Server stabilisce le impostazioni predefinite per la distribuzione delle immagini. Per una descrizione di ciascuna impostazione, consulta la schermata dell’interfaccia utente .

**[!UICONTROL Richiedi attributi]** : queste impostazioni impongono limiti alle immagini che possono essere consegnate dal server.
**[!UICONTROL Attributi richiesta predefiniti]** : queste impostazioni si riferiscono all&#39;aspetto predefinito delle immagini.
**[!UICONTROL Attributi comuni delle miniature]** : queste impostazioni si riferiscono all&#39;aspetto predefinito delle immagini in miniatura.
**[!UICONTROL Valori predefiniti per i campi del catalogo]**: queste impostazioni si riferiscono alla risoluzione e al tipo di miniatura predefinito delle immagini.
**[!UICONTROL Attributi di gestione del colore]** : queste impostazioni determinano quali profili di colore ICC vengono utilizzati.
**[!UICONTROL Attributi di compatibilità]** : questa impostazione consente ai paragrafi iniziali e finali nei livelli di testo di essere trattati come nella versione 3.6 per la compatibilità con le versioni precedenti.
**[!UICONTROL Supporto per la localizzazione]** : queste impostazioni consentono di gestire più attributi di impostazione internazionale. Consente inoltre di specificare una stringa di mappa delle impostazioni internazionali in modo da definire le lingue che si desidera supportare per le varie descrizioni a comparsa nei visualizzatori. Per ulteriori informazioni sulla configurazione del **[!UICONTROL supporto per la localizzazione]**, consulta [Considerazioni sulla configurazione della localizzazione delle risorse](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Configurazione delle impostazioni generali dell&#39;applicazione {#configuring-application-general-settings}

Per aprire la pagina Impostazioni generali applicazione, nella barra di navigazione globale di Dynamic Media Classic fare clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

**[!UICONTROL Server]**  - Al momento del provisioning dell’account, Dynamic Media fornisce automaticamente i server assegnati alla tua azienda. Questi server vengono utilizzati per creare stringhe URL per il sito web e le applicazioni. Queste chiamate URL sono specifiche del tuo account. Non modificare nessuno dei nomi dei server, a meno che non venga esplicitamente richiesto da Experience Manager come supporto Cloud Service.
**[!UICONTROL Sovrascrivi immagini]** : Dynamic Media non consente a due file di avere lo stesso nome. L&#39;ID URL di ogni elemento (il nome del file meno l&#39;estensione) deve essere univoco. Queste opzioni specificano come vengono caricate le risorse sostitutive: se sostituiscono l&#39;originale o diventano duplicati. Le risorse duplicate vengono rinominate con un &quot;-1&quot; (ad esempio, chair.tif viene rinominato chair-1.tif). Queste opzioni interessano le risorse caricate in una cartella diversa dall’originale o le risorse con un’estensione di file diversa dall’originale.
**[!UICONTROL Sovrascrivi nella cartella corrente, nome/estensione]**  immagine di base - Questa opzione è la regola più rigida per la sostituzione. Richiede di caricare l&#39;immagine di sostituzione nella stessa cartella dell&#39;originale e che abbia la stessa estensione di file dell&#39;originale. Se tali requisiti non sono soddisfatti, viene creato un duplicato. Per mantenere la coerenza con l&#39;Experience Manager come Cloud Service, scegli sempre **[!UICONTROL Sovrascrivi nella cartella corrente, stesso nome/estensione dell&#39;immagine di base]**.
**[!UICONTROL Sovrascrivi in qualsiasi cartella, stesso nome/estensione]**  della risorsa base - Richiede che l&#39;immagine sostitutiva abbia la stessa estensione del file dell&#39;immagine originale. Ad esempio, sedia.jpg deve sostituire sedia.jpg, non sedia.tif. Tuttavia, puoi caricare l’immagine di sostituzione in una cartella diversa dall’originale. L&#39;immagine aggiornata si trova nella nuova cartella; non è più possibile trovare il file nella posizione originale.
**[!UICONTROL Sovrascrivi in qualsiasi cartella, lo stesso nome della risorsa di base indipendentemente dall&#39;estensione]**  - Questa opzione è la regola di sostituzione più inclusiva. Puoi caricare un’immagine sostitutiva in una cartella diversa dall’originale, caricare un file con un’estensione di file diversa e sostituire il file originale. Se il file originale si trova in una cartella diversa, l&#39;immagine sostitutiva si trova nella nuova cartella in cui è stata caricata.
**[!UICONTROL Profili colore predefiniti]**  - Per ulteriori informazioni, consulta  [Configurazione della ](#configuring-color-management) gestione colore . Per impostazione predefinita, il sistema mostra 15 rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** e 15 predefiniti visualizzatore quando fai clic su **[!UICONTROL Visualizzatori]** nella vista Dettaglio della risorsa. Puoi aumentare questo limite. Consulta la sezione [Aumento o riduzione del numero di predefiniti immagine da visualizzare](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumento o riduzione del numero di predefiniti visualizzatore da mostrare](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Configurazione della gestione del colore {#configuring-color-management}

La gestione del colore di Dynamic Media consente di colorare le risorse corrette. Con la correzione del colore, le risorse acquisite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede un rendering dinamico, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio. Consulta [Configurazione dei predefiniti per immagini](/help/assets/dynamic-media/managing-image-presets.md).

Per configurare le proprietà colore predefinite per l’abilitazione della correzione colore durante la richiesta delle immagini:

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account utilizzando le credenziali fornite durante il provisioning.
1. Passa a **[!UICONTROL Configurazione > Impostazione applicazione]**.
1. Espandi l’area **[!UICONTROL Publish Setup (Impostazione pubblicazione)]** e seleziona **[!UICONTROL Image Server]**. Per le istanze di pubblicazione, imposta **[!UICONTROL Contesto di pubblicazione]** su **[!UICONTROL Image Server]**.
1. Scorri fino alla proprietà da modificare, ad esempio una proprietà nell&#39;area **[!UICONTROL Attributi di gestione del colore]**.
È possibile impostare le seguenti proprietà di correzione del colore:

   | Proprietà | Descrizione |
   |---|---|
   | Spazio colore predefinito CMYK | Nome del profilo colore CMYK predefinito. |
   | Spazio colore predefinito in scala di grigi | Nome del profilo colore grigio predefinito. |
   | Spazio colore predefinito RGB | Nome del profilo colore RGB predefinito. |
   | Intento di rendering della conversione del colore | Specifica l&#39;intento di rendering. I valori accettabili sono: **[!UICONTROL percettivo]**, **[!UICONTROL colometrico relativo]**, **[!UICONTROL saturazione]**, **[!UICONTROL colometrico assoluto]**. L&#39;Adobe consiglia **[!UICONTROL relativo]** come impostazione predefinita. |

1. Tocca **[!UICONTROL Salva]**.

Ad esempio, puoi impostare **[!UICONTROL Spazio colore predefinito RGB]** su *sRGB* e **[!UICONTROL Spazio colore predefinito CMYK]** su *WebCoated*.

In questo modo si effettua quanto segue:

* Abilita la correzione del colore per le immagini RGB e CMYK.
* Le immagini RGB che non hanno un profilo colore sono considerate nello spazio colore *sRGB*.
* Le immagini CMYK prive di un profilo colore sono considerate nello spazio colore *WebCoated*.
* Rendering dinamici che restituiscono l’output RGB, restituiscilo nello spazio colore *sRGB*.
* Rendering dinamici che restituiscono l&#39;output CMYK, restituiscilo nello spazio colore *WebCoated*.

#### Modifica dei tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Media e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Converti un Adobe PDF in una risorsa eCatalog.
* Converti un documento Adobe Photoshop (.PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file di PostScript® incapsulato Adobe Photoshop (.EPS).
* [I ](/help/assets/dynamic-media/video-profiles.md) profili video e i profili  [ ](/help/assets/dynamic-media/image-profiles.md) di imaging possono essere utilizzati rispettivamente per definire l’elaborazione di video e immagini.

Consulta [Caricamento delle risorse](/help/assets/add-assets.md).

**Per modificare i tipi MIME per i formati supportati**

1. In Experience Manager come Cloud Service, fai clic sul logo Experience Manager come Cloud Service per accedere alla console di navigazione globale, quindi fai clic su **[!UICONTROL Generale > CRXDE Lite]**.
1. Nella barra a sinistra, passa a quanto segue:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes , seleziona un tipo MIME.
1. Sul lato destro della pagina CRXDE Lite, nella parte inferiore:

   * Fare doppio clic sul campo **[!UICONTROL abilitato]**. Per impostazione predefinita, tutti i tipi MIME delle risorse sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse sono sincronizzate in Dynamic Media per l’elaborazione. Se desideri escludere l’elaborazione di questo tipo MIME della risorsa, modifica questa impostazione in **[!UICONTROL false]**.

   * Fare doppio clic su **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Consulta [Tipi MIME supportati](/help/assets/file-format-support.md) per un elenco dei valori dei parametri di elaborazione consentiti che puoi utilizzare per un determinato tipo MIME.

1. Effettua una delle operazioni seguenti:
   * Ripeti i passaggi 3-4 per modificare altri tipi MIME.
   * Nella barra dei menu della pagina CRXDE Lite, fai clic su **[!UICONTROL Salva tutto]**.

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL CRXDE Lite]** per tornare ad Experience Manager come Cloud Service.

#### Aggiunta di tipi MIME per i formati non supportati {#adding-mime-types-for-unsupported-formats}

In Experience Manager Assets puoi aggiungere tipi MIME personalizzati per i formati non supportati. Per fare in modo che qualsiasi nuovo nodo aggiunto in CRXDE Lite non venga eliminato ad Experience Manager, sposta il tipo MIME prima di `image_`. Inoltre, assicurati che il suo valore abilitato sia impostato su **[!UICONTROL false]**.

**Aggiunta di tipi MIME per i formati non supportati**

1. Ad Experience Manager, come Cloud Service, tocca **[!UICONTROL Strumenti > Operazioni > Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser alla pagina **[!UICONTROL Configurazione della console Web Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, tocca **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Nella pagina **Adobe CQ Scene7 Asset MIME type Service** , fai clic sull’icona a forma di segno più &lt;+>. La posizione nella tabella in cui fai clic sul segno più per aggiungere il nuovo tipo MIME è insignificante.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digita `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   L’esempio `DWG=image/vnd.dwg` è solo a scopo illustrativo. Il tipo MIME che aggiungi qui può essere qualsiasi altro formato non supportato.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Nell’angolo in basso a destra della pagina, tocca **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser con la pagina di configurazione della console Web di Adobe Experience Manager aperta.

1. Torna alla scheda del browser con l’Experience Manager aperto come console di Cloud Service.
1. Dall’Experience Manager come Cloud Service, tocca **[!UICONTROL Strumenti > Generale > CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, passa a quanto segue:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo MIME `image_vnd.dwg` e rilascialo direttamente sopra `image_` nell’albero come mostrato nella schermata seguente.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo MIME `image_vnd.dwg` ancora selezionato, dalla scheda **[!UICONTROL Proprietà]**, nella riga **[!UICONTROL abilitato]**, nell&#39;intestazione di colonna **[!UICONTROL Valore]** fai doppio clic sul valore. Viene aperto l’elenco a discesa **[!UICONTROL Valore]** .
1. Digita `false` nel campo (oppure seleziona **[!UICONTROL false]** dall’elenco a discesa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Fai clic su **[!UICONTROL Salva tutto]** nell’angolo in alto a sinistra della pagina CRXDE Lite.



### (Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per garantire il corretto funzionamento di Dynamic Media <!--(with `dynamicmedia_scene7` run mode)-->, l&#39;Adobe consiglia i seguenti suggerimenti per l&#39;ottimizzazione delle prestazioni/della scalabilità di sincronizzazione:

* Aggiornamento dei parametri di processo predefiniti per l&#39;elaborazione di diversi formati di file.
* Aggiornamento dei thread di lavoro predefiniti del flusso di lavoro Granite (risorse video) in coda.
* Aggiornamento dei thread di lavoro temporanei di coda predefiniti del flusso di lavoro Granite (immagini e risorse non video).
* Aggiornamento delle connessioni di caricamento massime nel server Dynamic Media Classic.

#### Aggiornamento dei parametri di processo predefiniti per l&#39;elaborazione di diversi formati di file

Puoi ottimizzare i parametri dei processi per velocizzarne l’elaborazione quando carichi i file. Ad esempio, se carichi i file PSD ma non desideri elaborarli come modelli, puoi impostare l’estrazione del livello su false (disattivato). In questo caso, il parametro del processo di sintonizzazione viene visualizzato come segue: `process=None&createTemplate=false`.

Se desideri attivare la creazione di modelli, utilizza i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

L&#39;Adobe consiglia di utilizzare i seguenti parametri di processo &quot;sintonizzati&quot; per i file PDF, PostScript® e PSD:

| Tipo di file | Parametri di lavoro consigliati |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno di questi parametri, consulta [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats).

Vedi anche [Aggiunta di tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats).

#### Aggiornamento della coda del flusso di lavoro transitorio di Granite {#updating-the-granite-transient-workflow-queue}

La coda del flusso di lavoro di transito Granite viene utilizzata per il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** . In Dynamic Media viene utilizzato per l’acquisizione e l’elaborazione delle immagini.

**Per aggiornare la coda del flusso di lavoro transitorio di Granite**

1. Vai su [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) e cerca **Coda: Coda flusso di lavoro transitorio Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Processi paralleli massimi]** , modifica il numero nel valore desiderato.

   Puoi aumentare **[!UICONTROL Processi paralleli massimi]** per supportare in modo adeguato il caricamento di file pesanti in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ad esempio una migrazione iniziale o un caricamento in serie una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (come il doppio del numero di core) può avere effetti negativi su altre attività simultanee. Di conseguenza, verifica e regola il valore in base al tuo caso d’uso specifico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Tocca **[!UICONTROL Salva]**.

#### Aggiornamento della coda del flusso di lavoro Granite {#updating-the-granite-workflow-queue}

La coda del flusso di lavoro Granite viene utilizzata per i flussi di lavoro non transitori. In Dynamic Media, veniva utilizzato per elaborare i video con il flusso di lavoro **[!UICONTROL Codifica video Dynamic Media]** .

Per aggiornare la coda del flusso di lavoro Granite:

1. Passa a `https://<server>/system/console/configMgr` e cerca **Coda: Coda flusso di lavoro Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Processi paralleli massimi]** , modifica il numero nel valore desiderato.

   Per impostazione predefinita, il numero massimo di processi paralleli dipende dal numero di core della CPU disponibili. Ad esempio, su un server di base 4, assegna due thread di lavoro. Un valore compreso tra 0,0 e 1,0 è basato sul rapporto o qualsiasi numero maggiore di uno assegna il numero di thread di lavoro.

   Per la maggior parte dei casi d’uso, è sufficiente l’impostazione predefinita 0,5.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Tocca **[!UICONTROL Salva]**.

#### Aggiornamento della connessione di caricamento Scene7 {#updating-the-scene-upload-connection}

L’impostazione Scene7 Upload Connection sincronizza le risorse di Experience Manager con i server Dynamic Media Classic.

Per aggiornare la connessione di caricamento Scene7:

1. Accedi a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. Nel campo **[!UICONTROL Numero di connessioni]** o nel campo **[!UICONTROL Timeout processo attivo]**, o in entrambi, modificare il numero come desiderato.

   L&#39;impostazione **[!UICONTROL Number of connections]** controlla il numero massimo di connessioni HTTP consentite, ad Experience Manager per il caricamento in Dynamic Media. In genere, il valore predefinito di dieci connessioni è sufficiente.

   L’impostazione **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per la pubblicazione delle risorse Dynamic Media caricate nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

   Per la maggior parte dei casi d’uso, è sufficiente impostare 2100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Tocca **[!UICONTROL Salva]**.

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, tap the Experience Manager as a Cloud Service logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
