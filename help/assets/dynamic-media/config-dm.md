---
title: Configura Cloud Service Dynamic Media
description: Scopri come configurare Dynamic Media in Adobe Experience Manager as a Cloud Service.
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: fc07b12f7a35b4f772a0ac4f9e6b09a1287eec8b
workflow-type: tm+mt
source-wordcount: '3574'
ht-degree: 3%

---

# Informazioni sulla configurazione del Cloud Service Dynamic Media {#configuring-dynamic-media}

Se utilizzi Adobe Experience Manager per ambienti diversi, ad esempio sviluppo, staging e produzione live, configura i Cloud Services Dynamic Media per ciascuno di tali ambienti.

Vedi anche [Configurare un account alias società Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md)

## Diagramma dell&#39;architettura di Dynamic Media {#architecture-diagram-of-dynamic-media}

Il diagramma di architettura seguente descrive il funzionamento di Dynamic Media.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primaria e delle sincronizzazioni con Dynamic Media per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa sorgente principale viene caricata in Adobe Experience Manager as a Cloud Service, viene replicata in Dynamic Media. A questo punto, Dynamic Media gestisce l’elaborazione e la generazione di rendering delle risorse, ad esempio la codifica video e le varianti dinamiche di un’immagine.
1. Dopo la generazione dei rendering, Experience Manager as a Cloud Service può accedere in modo sicuro e visualizzare in anteprima i rendering remoti di Dynamic Media (nessun file binario viene inviato nuovamente all&#39;istanza as a Cloud Service di Experience Manager).
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

## Creare una configurazione Dynamic Media nei Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. In Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. Nella parte sinistra della console, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Cloud Services > Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazione Dynamic Media, seleziona nel riquadro a sinistra **[!UICONTROL globale]** (non selezionare l’icona della cartella a sinistra di **[!UICONTROL globale]**). Quindi seleziona **[!UICONTROL Crea]**.
1. Sulla **[!UICONTROL Crea configurazione Dynamic Media]** , inserisci il titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Media e la password dell&#39;amministratore aziendale dell&#39;account Dynamic Media, quindi seleziona la tua area geografica. Queste informazioni vengono fornite per Adobe nell’e-mail di provisioning. Se non hai ricevuto questa e-mail, contatta l’Assistenza clienti di Adobe.
1. Seleziona **[!UICONTROL Connessione a Dynamic Media]**.
1. In **[!UICONTROL Modifica password]** nella finestra di dialogo **[!UICONTROL Nuova password]** immetti una nuova password composta da 8-25 caratteri. La password deve contenere almeno uno dei seguenti elementi:

   * Lettera maiuscola
   * Lettera minuscola
   * Numero
   * Carattere speciale: `# $ & . - _ : { }`

   La **[!UICONTROL Password corrente]** Il campo è precompilato intenzionalmente e nascosto dall’interazione.

   Se necessario, è possibile controllare l&#39;ortografia di una password digitata o digitata nuovamente selezionando l&#39;icona occhio password per visualizzare la password. Seleziona nuovamente l&#39;icona per nascondere la password.

1. In **[!UICONTROL Ripeti password]** campo , digita nuovamente la nuova password, quindi seleziona **[!UICONTROL Fine]**.

   La nuova password viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro del **[!UICONTROL Crea configurazione Dynamic Media]** pagina.

   Se hai selezionato **[!UICONTROL Annulla]** in **[!UICONTROL Modifica password]** quando salvi la configurazione di Dynamic Media appena creata, è comunque necessario immettere una nuova password.

   Vedi anche [Modificare la password in Dynamic Media](#change-dm-password).

1. Quando la connessione ha esito positivo, è possibile impostare quanto segue:

   | Proprietà | Descrizione |
   |---|---|
   | Azienda | Nome dell&#39;account Dynamic Media. È possibile avere più account Dynamic Media per diversi marchi secondari, divisioni o ambienti di staging/produzione.<br>Vedi anche [Configurare un account alias società Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md). |
   | Percorso cartella principale della società | Percorso cartella principale della tua azienda. |
   | Pubblicazione delle risorse | Puoi scegliere tra le tre opzioni seguenti:<br>**[!UICONTROL Immediatamente ]**- Quando le risorse vengono caricate, il sistema le acquisisce e fornisce l’URL/da incorporare immediatamente. Non è necessario alcun intervento degli utenti per pubblicare le risorse.<br>**[!UICONTROL All&#39;attivazione]** - È necessario pubblicare esplicitamente la risorsa prima prima di fornire un collegamento URL/Incorpora .<br>**[!UICONTROL Pubblicazione selettiva ]**- Le risorse vengono pubblicate automaticamente solo per l’anteprima protetta. Possono anche essere pubblicati esplicitamente in Experience Manager as a Cloud Service senza pubblicare in DMS7 per la distribuzione nel dominio pubblico. In futuro, questa opzione intende pubblicare le risorse in Experience Manager as a Cloud Service e pubblicarle in Dynamic Media, che si escludono a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 in modo da poter utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. Oppure, puoi pubblicare le risorse esclusivamente nell’Experience Manager as a Cloud Service per la visualizzazione dell’anteprima; le stesse risorse non vengono pubblicate in DMS7 per la distribuzione nel dominio pubblico. |
   | Server di anteprima protetto | Consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, Experience Manager as a Cloud Service può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Media remote (non vengono inviati binari all’istanza as a Cloud Service di Experience Manager).<br>A meno che non si disponga di una disposizione speciale per utilizzare il server della propria azienda o un server speciale, Adobe consiglia di lasciare questa impostazione come specificato. |
   | Sincronizza tutti i contenuti | Selezionato per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere in modo selettivo le risorse dalla sincronizzazione con Dynamic Media. Deselezionando questa opzione puoi scegliere tra le due seguenti modalità di sincronizzazione Dynamic Media:<br>**[!UICONTROL Modalità di sincronizzazione Dynamic Media]**<br>**[!UICONTROL Abilita per impostazione predefinita ]**- La configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non si contrassegni una cartella specifica per l&#39;esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabilitata per impostazione predefinita]** - La configurazione non viene applicata ad alcuna cartella finché non si contrassegna esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Media.<br>Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Media, seleziona una cartella di risorse, quindi seleziona nella barra degli strumenti **[!UICONTROL Proprietà]**. Sulla **[!UICONTROL Dettagli]** nella scheda **[!UICONTROL Modalità di sincronizzazione Dynamic Media]** dall’elenco a discesa, scegli una delle tre opzioni seguenti. Al termine, seleziona **[!UICONTROL Salva]**. *Ricorda: queste tre opzioni non sono disponibili se selezionate **Sincronizza tutti i contenuti**prima.* Vedi anche [Utilizzo di Pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Ereditato ]**- Nessun valore di sincronizzazione esplicito sulla cartella. La cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per le visualizzazioni ereditate viene visualizzato tramite una descrizione comandi.<br>**[!UICONTROL Abilita per sottocartelle]** - Includi tutto ciò che si trova in questa sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono la modalità predefinita nella configurazione cloud.<br>**[!UICONTROL Disabilitato per le sottocartelle ]**- Escludere tutti gli elementi di questo sottoalbero dalla sincronizzazione con Dynamic Media. |

   >[!NOTE]
   >
   >In Dynamic Media non è supportato il controllo delle versioni. Inoltre, l&#39;attivazione ritardata si applica solo se **[!UICONTROL Pubblicare le risorse]** nella pagina Modifica configurazione Dynamic Media è impostato su **[!UICONTROL All&#39;attivazione]**. E poi, solo fino alla prima attivazione della risorsa.
   >
   >
   >Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale su S7 Delivery.

   ![dynamic icmediaconfiguration2update](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Seleziona **[!UICONTROL Salva]**. La nuova password e la nuova configurazione di Dynamic Media viene salvata. Se hai selezionato **[!UICONTROL Annulla]** non viene invece eseguito alcun aggiornamento della password.
1. In **[!UICONTROL Configurazione di Dynamic Media]** finestra di dialogo, seleziona **[!UICONTROL OK]** per iniziare la configurazione.

   >[!IMPORTANT]
   >
   >Al termine della nuova configurazione di Dynamic Media, riceverai una notifica di stato nella casella in entrata di Experience Manager as a Cloud Service.
   >
   >Questa notifica della casella in entrata informa se la configurazione ha avuto esito positivo o meno.
   > Vedi [Risolvere i problemi relativi alla nuova configurazione di Dynamic Media](#troubleshoot-dm-config) e [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md) per ulteriori informazioni.

1. Per visualizzare in modo sicuro l’anteprima del contenuto Dynamic Media prima della pubblicazione, Experience Manager as a Cloud Service utilizza la convalida basata su token, quindi Experience Manager Author visualizza in anteprima il contenuto Dynamic Media per impostazione predefinita. Tuttavia, puoi *inserire nell&#39;elenco Consentiti* più IP per consentire agli utenti di visualizzare un’anteprima sicura dei contenuti. Per impostare questa azione nell&#39;Experience Manager as a Cloud Service, vedi [Configurazione di Dynamic Media Publish Setup per Image Server - Scheda Sicurezza](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

La configurazione di base è terminata. sei pronto per utilizzare Dynamic Media.

Se desideri personalizzare ulteriormente la configurazione, puoi facoltativamente completare una qualsiasi delle attività in [Configurare le impostazioni avanzate in Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Risolvere i problemi relativi alla nuova configurazione di Dynamic Media {#troubleshoot-dm-config}

Al termine della configurazione di una nuova configurazione di Dynamic Media, riceverai una notifica di stato nella casella in entrata di Experience Manager as a Cloud Service. Questa notifica informa se la configurazione ha avuto esito positivo o meno, come illustrato nelle immagini seguenti dalla casella in entrata.

![Experience Manager Casella in entrata - Completata](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Errore della casella in entrata Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Vedi anche [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md).

**Per risolvere i problemi relativi a una nuova configurazione di Dynamic Media:**

1. Nell’angolo in alto a destra della pagina as a Cloud Service dell’Experience Manager, seleziona l’icona della campana, quindi seleziona **[!UICONTROL Visualizza tutto]**.
1. Nella pagina Posta in arrivo, seleziona la notifica di successo per leggere una panoramica dello stato e dei registri della configurazione.

   Se la configurazione non è riuscita, seleziona la notifica di errore simile alla schermata seguente.

   ![Configurazione Dynamic Media non riuscita](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Sulla **[!UICONTROL DMSETUP]** controlla i dettagli di configurazione che descrivono l’errore. In particolare, prendere nota di eventuali messaggi di errore o codici di errore. Contatta l’Assistenza clienti di Adobe con queste informazioni.

   ![Pagina Configurazione Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Modificare la password in Dynamic Media {#change-dm-password}

La scadenza della password in Dynamic Media è impostata a 100 anni dalla data di sistema corrente.

La password deve contenere almeno uno dei seguenti elementi:

* Lettera maiuscola
* Lettera minuscola
* Numero
* Carattere speciale: `# $ & . - _ : { }`

Se necessario, è possibile controllare l&#39;ortografia di una password digitata o digitata nuovamente selezionando l&#39;icona occhio password per visualizzare la password. Seleziona nuovamente l&#39;icona per nascondere la password.

La password modificata viene salvata quando selezioni **[!UICONTROL Salva]** nell&#39;angolo superiore destro del **[!UICONTROL Modifica configurazione Dynamic Media]** pagina.

1. In Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. Nella parte sinistra della console, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Cloud Services > Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazione Dynamic Media, seleziona nel riquadro a sinistra **[!UICONTROL globale]**. Non selezionare l’icona della cartella a sinistra di **[!UICONTROL globale]**. Quindi, seleziona **[!UICONTROL Modifica]**.
1. Sulla **[!UICONTROL Modifica configurazione Dynamic Media]** direttamente sotto la pagina **[!UICONTROL Password]** campo , seleziona **[!UICONTROL Modifica password]**.
1. In **[!UICONTROL Modifica password]** effettuare le seguenti operazioni:

   * In **[!UICONTROL Nuova password]** immettere una nuova password.

      La **[!UICONTROL Password corrente]** Il campo è precompilato intenzionalmente e nascosto dall’interazione.

   * In **[!UICONTROL Ripeti password]** campo , digita nuovamente la nuova password, quindi seleziona **[!UICONTROL Fine]**.

1. Nell&#39;angolo in alto a destra del **[!UICONTROL Modifica configurazione Dynamic Media]** pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]**.

## (Facoltativo) Configurare le impostazioni avanzate in Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Per personalizzare ulteriormente la configurazione e la configurazione di Dynamic Media o ottimizzarne le prestazioni, puoi completare una o più delle seguenti operazioni *facoltativo* attività:

* [(Facoltativo) Configurazione e configurazione delle impostazioni di Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Facoltativo) Ottimizzare le prestazioni di Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Facoltativo) Configurazione e configurazione delle impostazioni di Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilizza l’interfaccia utente di Dynamic Media Classic per modificare le impostazioni di Dynamic Media.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

Le attività di configurazione e configurazione includono:

* [Configurare l’impostazione di pubblicazione Dynamic Media per il server immagini](#publishing-setup-for-image-server)
* [Configurare le impostazioni generali di Dynamic Media](#configuring-application-general-settings)
* [Configurare la gestione del colore](#configuring-color-management)
* [Modifica tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiungi tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats)

<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configurare l’impostazione di pubblicazione Dynamic Media per il server immagini {#publishing-setup-for-image-server}

La pagina Configurazione pubblicazione di Dynamic Media stabilisce le impostazioni predefinite che determinano come le risorse vengono distribuite dai server Dynamic Media di Adobe ai siti web o alle applicazioni.

Vedi [Configurare l’impostazione di pubblicazione Dynamic Media per il server immagini](/help/assets/dynamic-media/dm-publish-settings.md).

#### Configurare le impostazioni generali di Dynamic Media {#configuring-application-general-settings}

Configurare Dynamic Media **[!UICONTROL Nome server di pubblicazione]** e **[!UICONTROL Nome server di origine]** URL. Puoi inoltre specificare **[!UICONTROL Carica nell’applicazione]** impostazioni e **[!UICONTROL Opzioni di caricamento predefinite]** tutto in base al tuo caso d&#39;uso specifico.

Vedi [Configurare le impostazioni generali di Dynamic Media](/help/assets/dynamic-media/dm-general-settings.md).

#### Configurare la gestione del colore {#configuring-color-management}

La gestione del colore di Dynamic Media consente di colorare le risorse corrette. Con la correzione del colore, le risorse acquisite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede un rendering dinamico, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio.

Vedi [Configurare i predefiniti per immagini](/help/assets/dynamic-media/managing-image-presets.md).

Per configurare le proprietà colore predefinite per l’abilitazione della correzione colore durante la richiesta delle immagini:

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account utilizzando le credenziali fornite durante il provisioning.
1. Vai a **[!UICONTROL Configurazione > Impostazione applicazione]**.
1. Espandi l’area **[!UICONTROL Publish Setup (Impostazione pubblicazione)]** e seleziona **[!UICONTROL Image Server]**. Per le istanze di pubblicazione, imposta **[!UICONTROL Contesto di pubblicazione]** su **[!UICONTROL Image Server]**.
1. Scorri fino alla proprietà da modificare, ad esempio una proprietà nel **[!UICONTROL Attributi di gestione del colore]** area.
È possibile impostare le seguenti proprietà di correzione del colore:

   | Proprietà | Descrizione |
   |---|---|
   | Spazio colore predefinito CMYK | Nome del profilo colore CMYK predefinito. |
   | Spazio colore predefinito in scala di grigi | Nome del profilo colore grigio predefinito. |
   | Spazio colore predefinito di RGB | Nome del profilo colore predefinito di RGB. |
   | Intento di rendering per conversione colore | Specifica l&#39;intento di rendering. I valori accettabili sono: **[!UICONTROL percettivo]**, **[!UICONTROL colometrico relativo]**, **[!UICONTROL saturazione]**, **[!UICONTROL colometrico assoluto]**. L&#39;Adobe raccomanda **[!UICONTROL relativo]** come impostazione predefinita. |

1. Seleziona **[!UICONTROL Salva]**.

Ad esempio, puoi impostare **[!UICONTROL Spazio colore predefinito RGB]** su *sRGB* e **[!UICONTROL Spazio colore predefinito CMYK]** su *WebCoated*.

In questo modo si effettua quanto segue:

* Abilita la correzione del colore per le immagini RGB e CMYK.
* Si presume che le immagini di RGB prive di un profilo colore siano presenti nel *sRGB* spazio colore.
* Si presume che le immagini CMYK prive di un profilo colore siano in *WebCoated* spazio colore.
* Rendering dinamici che restituiscono l’output di RGB, restituiscilo nel *sRGB* spazio colore.
* Rendering dinamici che restituiscono l’output CMYK, restituiscilo nel *WebCoated* spazio colore.

#### Modifica tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Media e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Converti un Adobe PDF in una risorsa eCatalog.
* Converti un documento Adobe Photoshop (.PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file di PostScript® incapsulato Adobe Photoshop (.EPS).
* [Profili video](/help/assets/dynamic-media/video-profiles.md) e [Profili immagine](/help/assets/dynamic-media/image-profiles.md) può essere utilizzato rispettivamente per definire l’elaborazione di video e immagini.

Vedi [Caricare le risorse](/help/assets/add-assets.md).

**Per modificare i tipi MIME per i formati supportati:**

1. Accedi al tuo Experience Manager as a Cloud Service come amministratore del prodotto.
1. In Experience Manager as a Cloud Service , seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Generale > CRXDE Lite]**.

   Se non hai accesso ad CRXDE Lite, consulta [Utilizzo di CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. Nella barra a sinistra, passa a quanto segue:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes , seleziona un tipo MIME.
1. Sul lato destro della pagina CRXDE Lite, nella parte inferiore:

   * Tocca due volte il **[!UICONTROL abilitato]** campo . Per impostazione predefinita, tutti i tipi MIME delle risorse sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse vengono sincronizzate in Dynamic Media per l’elaborazione. Se desideri escludere l’elaborazione di questo tipo MIME della risorsa, modifica questa impostazione in **[!UICONTROL false]**.

   * Doppio tocco **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Vedi [Tipi MIME supportati](/help/assets/file-format-support.md) per un elenco dei valori dei parametri di elaborazione consentiti che è possibile utilizzare per un determinato tipo MIME.

1. Effettua una delle operazioni seguenti:
   * Ripeti i passaggi 3-4 per modificare altri tipi MIME.
   * Nella barra dei menu della pagina CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

1. Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL CRXDE Lite]** per tornare all&#39;Experience Manager as a Cloud Service.

#### Aggiungi tipi MIME per i formati non supportati {#adding-mime-types-for-unsupported-formats}

In Experience Manager Assets puoi aggiungere tipi MIME personalizzati per i formati non supportati. Per evitare che un nuovo nodo aggiunto in CRXDE Lite venga eliminato ad Experience Manager, sposta il tipo MIME prima di `image_`. Inoltre, assicurati che il valore abilitato sia impostato su **[!UICONTROL false]**.

**Per aggiungere tipi MIME per i formati non supportati:**

1. Accedi al tuo Experience Manager as a Cloud Service come amministratore del prodotto.
1. Dall’Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti > Operazioni > Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser **[!UICONTROL Configurazione della console Web di Adobe Experience Manager]** pagina.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, tocca **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![Modifica i valori di configurazione](assets/2019-08-02_16-44-56.png)

1. Sulla **Servizio Adobe CQ Scene7 Asset MIME type** , selezionare un&#39;icona del segno più &lt;+>. La posizione nella tabella in cui selezioni il segno più per aggiungere il nuovo tipo MIME è insignificante.

   ![Servizio Adobe CQ Scene7 Asset Mime Type](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   La `DWG=image/vnd.dwg` Il tipo MIME è solo a scopo di esempio. Il tipo MIME che aggiungi qui può essere qualsiasi altro formato non supportato.

   ![Aggiunta di un tipo di MIME DWG](assets/2019-08-02_16-36-36.png)

1. Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser con la pagina di configurazione della console Web di Adobe Experience Manager aperta.

1. Torna alla scheda del browser con la console as a Cloud Service aperta Experience Manager.
1. Dall’Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti > Generale > CRXDE Lite]**.

   Se non hai accesso ad CRXDE Lite, consulta [Utilizzo di CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![Strumenti > Generale > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, passa a quanto segue:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo MIME `image_vnd.dwg` e rilasciarlo direttamente sopra `image_` nell&#39;albero come visto nella schermata seguente.

   ![Modifica di un file DWG in CRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo MIME `image_vnd.dwg` ancora selezionato, dal **[!UICONTROL Proprietà]** nella scheda **[!UICONTROL abilitato]** riga, sotto **[!UICONTROL Valore]** intestazione di colonna, tocca due volte il valore. La **[!UICONTROL Valore]** l’elenco a discesa viene aperto.
1. Tipo `false` nel campo (o seleziona **[!UICONTROL false]** dall’elenco a discesa).

   ![Modifica dei tipi di mime in CRXDE Lite](assets/2019-08-02_16-60-30.png)

1. Nell’angolo in alto a sinistra della pagina CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

### (Facoltativo) Ottimizzare le prestazioni di Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per mantenere Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> in modo scorrevole, Adobe consiglia i seguenti suggerimenti per l’ottimizzazione delle prestazioni/della scalabilità di sincronizzazione:

* [Aggiornare i parametri di processo predefiniti per l’elaborazione di diversi formati di file](#update-job-para).
* [Aggiorna i thread di lavoro predefiniti della coda di lavoro Granite (risorse video)](#update-granite-workflow-queue-worker-threads-video)
* [Aggiorna i thread di lavoro predefiniti della coda di lavoro transitoria di Granite (immagini e risorse non video)](#update-granite-transient-workflow-queue-worker-threads-images).
* [Aggiorna le connessioni di caricamento massime sul server Dynamic Media Classic (Scene7)](#update-max-s7-upload-connections).

#### Aggiornare i parametri di processo predefiniti per l’elaborazione di diversi formati di file {#update-job-para}

Puoi ottimizzare i parametri dei processi per velocizzarne l’elaborazione quando carichi i file. Ad esempio, se carichi i file PSD ma non desideri elaborarli come modelli, puoi impostare l’estrazione del livello su false (disattivato). In questo caso, il parametro del processo di sintonizzazione viene visualizzato come segue: `process=None&createTemplate=false`.

Se desideri attivare la creazione di modelli, utilizza i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe consiglia di utilizzare i seguenti parametri di processo &quot;ottimizzati&quot; per i file PDF, PostScript® e PSD:

| Tipo di file | Parametri di lavoro consigliati |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno qualsiasi di questi parametri, vedi [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats).

Vedi anche [Aggiunta di tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats).

#### Aggiorna i thread di lavoro predefiniti della coda di lavoro Granite (risorse video) {#update-granite-workflow-queue-worker-threads-video}

La coda del flusso di lavoro Granite viene utilizzata per i flussi di lavoro non transitori. In Dynamic Media, elaborava i video con il **[!UICONTROL Codifica video Dynamic Media]** workflow.

>[!NOTE]
>
>Per completare questa attività, devi accedere ad Experience Manager as a Cloud Service come amministratore del prodotto.

Se non hai accesso a OSGi, vedi [Configurazione OSGi](/help/implementing/developing/components/overview.md#osgi-configuration).

**Per aggiornare i thread di lavoro predefiniti della coda di lavoro Granite (risorse video):**

1. Passa a `https://<server>/system/console/configMgr` e cerca **Coda: Coda flusso di lavoro Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. In **[!UICONTROL Processi paralleli massimi]** modifica il numero nel valore desiderato.

   Per impostazione predefinita, il numero massimo di processi paralleli dipende dal numero di core della CPU disponibili. Ad esempio, su un server di base 4, assegna due thread di lavoro. Un valore compreso tra 0,0 e 1,0 è basato sul rapporto o qualsiasi numero maggiore di uno assegna il numero di thread di lavoro.

   Per la maggior parte dei casi d’uso, è sufficiente l’impostazione predefinita 0,5.

   ![Configurazione di una coda di elaborazione del processo](assets/chlimage_1-1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiorna i thread di lavoro predefiniti della coda di lavoro transitoria di Granite {#update-granite-transient-workflow-queue-worker-threads-images}

La coda del flusso di lavoro di transito Granite viene utilizzata per **[!UICONTROL Risorsa di aggiornamento DAM]** workflow. In Dynamic Media viene utilizzato per l’acquisizione e l’elaborazione di immagini e risorse non video.

>[!NOTE]
>
>Per completare questa attività, devi accedere ad Experience Manager as a Cloud Service come amministratore del prodotto.

**Per aggiornare i thread di lavoro della coda del flusso di lavoro transitorio di Granite:**

1. Passa a **Configurazione della console Web di Adobe Experience Manager** a `http://<host>:<port>/system/console/configMgr`
1. Cerca **Coda: Coda flusso di lavoro transitorio di Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. In **[!UICONTROL Processi paralleli massimi]** modifica il numero nel valore desiderato.

   È possibile aumentare **[!UICONTROL Processi paralleli massimi]** per supportare adeguatamente il caricamento di file pesanti in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ad esempio una migrazione iniziale o un caricamento in serie una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (come il doppio del numero di core) può avere effetti negativi su altre attività simultanee. Di conseguenza, verifica e regola il valore in base al tuo caso d’uso specifico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiorna le connessioni di caricamento massime sul server Dynamic Media Classic (Scene7) {#update-max-s7-upload-connections}

L’impostazione Dynamic Media Classic (Scene7) Upload Connection sincronizza le risorse di Experience Manager sui server Dynamic Media Classic.

>[!NOTE]
>
>Per completare questa attività, devi accedere ad Experience Manager as a Cloud Service come amministratore del prodotto.

**Per aggiornare il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7):**

1. Accedi a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. In **[!UICONTROL Numero di connessioni]** o **[!UICONTROL Timeout processo attivo]** o entrambi, modificare il numero come desiderato.

   La **[!UICONTROL Numero di connessioni]** controlla il numero massimo di connessioni HTTP consentite, ad Experience Manager per il caricamento su Dynamic Media. In genere, il valore predefinito di dieci connessioni è sufficiente.

   La **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per le risorse Dynamic Media caricate da pubblicare nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

   Per la maggior parte dei casi d’uso, è sufficiente impostare 2100.

   ![Servizio di caricamento Adobe Scene7](assets/chlimage_1-2.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

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

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
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
