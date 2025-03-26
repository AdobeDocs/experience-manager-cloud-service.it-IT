---
title: Configurare Dynamic Media Cloud Service
description: Scopri come configurare Dynamic Media in Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Configuration,Dynamic Media
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3625'
ht-degree: 3%

---

# Informazioni sulla configurazione di Dynamic Media Cloud Service {#configuring-dynamic-media}

{{work-with-dynamic-media}}

Se utilizzi Adobe Experience Manager as a Cloud Service per diversi ambienti, ad esempio sviluppo, staging e produzione live, configura i servizi cloud per elementi multimediali dinamici per ciascuno di questi ambienti.

Vedi anche [Configurare un account alias società Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md)

## Diagramma dell’architettura di Dynamic Media {#architecture-diagram-of-dynamic-media}

Il seguente diagramma dell’architettura descrive il funzionamento di Dynamic Media.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primarie e si sincronizza con Dynamic Media per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa di origine primaria viene caricata in Adobe Experience Manager as a Cloud Service, viene replicata in Dynamic Media. A questo punto, Dynamic Media gestisce tutte le attività di elaborazione delle risorse e generazione del rendering, come la codifica video e le varianti dinamiche di un’immagine.
1. Dopo la generazione delle rappresentazioni, Experience Manager as a Cloud Service può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni remote di Dynamic Media (nessun binario viene inviato all’istanza di Experience Manager as a Cloud Service).
1. Quando il contenuto è pronto per essere pubblicato e approvato, attiva il servizio Dynamic Media per inviare contenuti ai server di distribuzione e memorizzarli nella cache della rete CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>Il seguente elenco di funzioni richiede l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager - Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con queste funzioni.
>
>* [Imaging avanzato](/help/assets/dynamic-media/imaging-faq.md)
>* [Annullamento validità cache](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [Protezione hotlink](/help/assets/dynamic-media/hotlink-protection.md)
>* [Distribuzione HTTP/2 dei contenuti](/help/assets/dynamic-media/http2faq.md)
>* Reindirizzamento URL a livello di CDN
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

## Creare una configurazione Dynamic Media in Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. In Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. Sulla sinistra della console, seleziona l&#39;icona Strumenti, quindi vai a **[!UICONTROL Cloud Services > Configurazione elemento multimediale dinamico]**.
1. Nel riquadro sinistro della pagina Browser configurazioni Dynamic Media selezionare **[!UICONTROL global]** (non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**). Quindi seleziona **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea configurazione Dynamic Media]**, immetti il titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Media e la password dell&#39;amministratore aziendale dell&#39;account Dynamic Media, quindi seleziona la tua area geografica. Queste informazioni vengono fornite da Adobe nell’e-mail di provisioning. Se non hai ricevuto questa e-mail, contatta l’Assistenza clienti Adobe.
1. Seleziona **[!UICONTROL Connetti a Dynamic Media]**.
1. Nella finestra di dialogo **[!UICONTROL Cambia password]** immettere una nuova password composta da 8-25 caratteri nel campo **[!UICONTROL Nuova password]**. La password deve contenere almeno uno dei seguenti elementi:

   * Lettera maiuscola
   * Lettera minuscola
   * Numero
   * Carattere speciale: `# $ & . - _ : { }`

   Il campo **[!UICONTROL Password corrente]** è stato precompilato intenzionalmente e nascosto dall&#39;interazione.

   Se necessario, è possibile controllare l&#39;ortografia di una password digitata o ridigitata selezionando l&#39;icona dell&#39;occhio della password per visualizzare la password. Seleziona nuovamente l’icona per nascondere la password.

1. Nel campo **[!UICONTROL Ripeti password]**, digita nuovamente la nuova password, quindi seleziona **[!UICONTROL Fine]**.

   La nuova password viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Crea configurazione Dynamic Media]**.

   Se hai selezionato **[!UICONTROL Annulla]** nella finestra di dialogo **[!UICONTROL Modifica password]**, devi comunque immettere una nuova password quando salvi la configurazione di Dynamic Media creata.

   Vedi anche [Modificare la password in Dynamic Media](#change-dm-password).

1. Quando la connessione ha esito positivo, puoi impostare quanto segue:

   | Proprietà | Descrizione |
   |---|---|
   | Azienda | Nome dell’account Dynamic Media.<br>**Importante**: in un&#39;istanza di Experience Manager è supportata una sola configurazione Dynamic Media in Cloud Services; non aggiungere più di una configurazione. Più configurazioni Dynamic Media in un&#39;istanza Experience Manager sono _non_ supportate o consigliate da Adobe.<!-- CQDOC-19579 and CQDOC-19612 --><br>Vedere anche [Configurare un account alias società Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md). |
   | Percorso cartella principale della società | Percorso della cartella principale della società. |
   | Pubblicazione di Assets | Puoi scegliere tra le tre opzioni seguenti:<br>**[!UICONTROL Immediatamente ]**- Quando le risorse vengono caricate, il sistema le acquisisce e fornisce immediatamente l&#39;URL/Incorpora. Non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.<br>**[!UICONTROL Al momento dell&#39;attivazione]** - Prima di fornire un URL o un collegamento di incorporamento, devi pubblicare esplicitamente la risorsa.<br>**[!UICONTROL Pubblicazione selettiva ]**- Assets viene pubblicato automaticamente solo per l&#39;anteprima protetta. Possono anche essere pubblicati in modo esplicito in Experience Manager as a Cloud Service senza dover essere pubblicati in DMS7 per la distribuzione nel dominio pubblico. In futuro, questa opzione pubblicherà le risorse in Experience Manager as a Cloud Service e le pubblicherà in Dynamic Media, escludendosi a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. In alternativa, puoi pubblicare le risorse esclusivamente in Experience Manager as a Cloud Service per la visualizzazione in anteprima; le stesse risorse non vengono pubblicate in DMS7 per la distribuzione nel dominio pubblico. |
   | Server di anteprima protetto | Consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, Experience Manager as a Cloud Service può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni remote di Dynamic Media (nessun binario viene rimandato all’istanza di Experience Manager as a Cloud Service).<br>A meno che non si disponga di una disposizione speciale per utilizzare il server della propria società o un server speciale, Adobe consiglia di lasciare questa impostazione come specificato. |
   | Sincronizza tutti i contenuti | Selezionata per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere selettivamente le risorse dalla sincronizzazione con Dynamic Media. Deselezionando questa opzione è possibile scegliere tra le due modalità di sincronizzazione di Dynamic Media seguenti:<br>**[!UICONTROL Modalità di sincronizzazione di Dynamic Media]**<br>**[!UICONTROL Attiva per impostazione predefinita ]**- La configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non si contrassegni una cartella specificamente per l&#39;esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabilitata per impostazione predefinita]** - La configurazione non viene applicata ad alcuna cartella fino a quando non contrassegni esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Media.<br>Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Media, seleziona una cartella di risorse, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**. Nella scheda **[!UICONTROL Dettagli]**, nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione Dynamic Media]**, scegliere una delle tre opzioni seguenti. Al termine, seleziona **[!UICONTROL Salva]**. _Ricorda: queste tre opzioni non sono disponibili se hai selezionato **Sincronizza tutto il contenuto**in precedenza._ Vedi anche [Utilizzare la pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Ereditato ]**- Nessun valore di sincronizzazione esplicito nella cartella. Al contrario, la cartella eredita il valore di sincronizzazione da una delle sue cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per ereditato viene visualizzato tramite una descrizione comando.<br>**[!UICONTROL Abilita per le sottocartelle]** - Includi tutto in questa sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche della cartella sovrascrivono la modalità predefinita nella configurazione cloud.<br>**[!UICONTROL Disattivato per le sottocartelle ]**- Escludi tutto ciò che si trova in questa struttura secondaria dalla sincronizzazione in Dynamic Media. |

   >[!NOTE]
   >
   >In Dynamic Media non è supportato il controllo delle versioni. Inoltre, l&#39;attivazione ritardata si applica solo se **[!UICONTROL Pubblica Assets]** nella pagina Modifica configurazione Dynamic Media è impostato su **[!UICONTROL All&#39;attivazione]**. E poi, solo fino alla prima volta che la risorsa viene attivata.
   >
   >
   >Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale in S7 Delivery.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Seleziona **[!UICONTROL Salva]**. Vengono salvate la nuova password e la nuova configurazione di Dynamic Media. Se invece hai selezionato **[!UICONTROL Annulla]**, non si verifica alcun aggiornamento della password.
1. Nella finestra di dialogo **[!UICONTROL Configurazione di Dynamic Media]**, seleziona **[!UICONTROL OK]** per avviare la configurazione.

   >[!IMPORTANT]
   >
   >Al termine dell’installazione della nuova configurazione di Dynamic Media, verrà inviata una notifica nella casella in entrata di Experience Manager as a Cloud Service.
   >
   >Questa notifica della casella in entrata ti informa se la configurazione è stata eseguita correttamente o meno.
   > Per ulteriori informazioni, vedere [Risoluzione dei problemi relativi a una nuova configurazione di Dynamic Media](#troubleshoot-dm-config) e [Posta in arrivo](/help/sites-cloud/authoring/inbox.md).

1. Per visualizzare in anteprima in modo sicuro il contenuto Dynamic Media prima che venga pubblicato, Experience Manager as a Cloud Service utilizza la convalida basata su token e quindi Experience Manager Author visualizza in anteprima il contenuto Dynamic Media per impostazione predefinita. Tuttavia, puoi *inserire nell&#39;elenco Consentiti* ulteriori IP per consentire agli utenti di accedere in modo sicuro all&#39;anteprima del contenuto. Per configurare questa azione in Experience Manager as a Cloud Service, vedi [Configurare l&#39;installazione della pubblicazione Dynamic Media per il server immagini - Scheda Sicurezza](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

Ora hai completato la configurazione di base; puoi utilizzare Dynamic Media.

Se desideri personalizzare ulteriormente la configurazione, ad esempio abilitando le autorizzazioni ACL (Access Control List), puoi facoltativamente completare qualsiasi attività in [Configura impostazioni avanzate in Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Risolvere i problemi relativi a una nuova configurazione di Dynamic Media {#troubleshoot-dm-config}

Al termine dell’installazione di una nuova configurazione di Dynamic Media, viene inviata una notifica nella casella in entrata di Experience Manager as a Cloud Service. Questa notifica ti informa se la configurazione è avvenuta con successo o meno, come mostrato nelle rispettive immagini seguenti provenienti dalla casella in entrata.

![Casella in entrata Experience Manager completata](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Errore della casella in entrata di Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Vedi anche [Posta in arrivo](/help/sites-cloud/authoring/inbox.md).

**Per risolvere i problemi relativi a una nuova configurazione di Dynamic Media:**

1. Fai clic sull&#39;icona del campanello nell&#39;angolo superiore destro della pagina Experience Manager as a Cloud Service, quindi seleziona **[!UICONTROL Visualizza tutto]**.
1. Nella pagina Casella in entrata, seleziona la notifica di successo per leggere una panoramica dello stato e dei registri della configurazione.

   Se la configurazione non è riuscita, seleziona la notifica di errore simile alla schermata seguente.

   ![Installazione di Dynamic Media non riuscita](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Nella pagina **[!UICONTROL DMSETUP]**, esaminare i dettagli di configurazione che descrivono l&#39;errore. In particolare, prendi nota di eventuali messaggi di errore o codici di errore. Contatta l’Assistenza clienti di Adobe con queste informazioni.

   ![Pagina di configurazione di Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Cambia la password in Dynamic Media {#change-dm-password}

La scadenza della password in Dynamic Media è impostata su 100 anni dalla data di sistema corrente.

La password deve contenere almeno uno dei seguenti elementi:

* Lettera maiuscola
* Lettera minuscola
* Numero
* Carattere speciale: `# $ & . - _ : { }`

Se necessario, è possibile controllare l&#39;ortografia di una password digitata o ridigitata selezionando l&#39;icona dell&#39;occhio della password per visualizzare la password. Seleziona nuovamente l’icona per nascondere la password.

La password modificata viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Modifica configurazione Dynamic Media]**.

1. In Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. Sulla sinistra della console, seleziona l&#39;icona Strumenti, quindi vai a **[!UICONTROL Cloud Services > Configurazione elemento multimediale dinamico]**.
1. Nella pagina Browser configurazioni Dynamic Media, nel riquadro a sinistra, selezionare **[!UICONTROL global]**. Non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**. Quindi, seleziona **[!UICONTROL Modifica]**.
1. Nella pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, sotto il campo **[!UICONTROL Password]**, selezionare **[!UICONTROL Modifica password]**.
1. Nella finestra di dialogo **[!UICONTROL Modifica password]** eseguire le operazioni seguenti:

   * Nel campo **[!UICONTROL Nuova password]** immettere una nuova password.

     Il campo **[!UICONTROL Password corrente]** è stato precompilato intenzionalmente e nascosto dall&#39;interazione.

   * Nel campo **[!UICONTROL Ripeti password]**, digita nuovamente la nuova password, quindi seleziona **[!UICONTROL Fine]**.

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]**.

## (Facoltativo) Configurazione delle impostazioni avanzate in Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Per personalizzare ulteriormente la configurazione e l&#39;installazione di Dynamic Media o ottimizzarne le prestazioni, è possibile completare una o più delle seguenti _attività facoltative_:

* [Abilitare le autorizzazioni ACL in Dynamic Media (facoltativo)](#optional-enable-acl)
* [Impostazione e configurazione delle impostazioni di Dynamic Media (facoltativo)](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

<!-- Removed as per CQDOC-20701 - May need to revisit and update. In Adobe Experience Manager (AEM) as a Cloud Service, enabling Access Control List (ACL) permissions for Dynamic Media requires a different approach compared to on-premise versions (which was described below), as direct editing of OSGi configurations via the UI is not supported. Not sure how this is done now. For example, you can manage ACLs using tools like the Netcentric Access Control Tool (AC Tool), which simplifies the specification and deployment of complex ACLs in AEM but I doubt that's the recommended method.

### (Optional) Enable Access Control List permissions in Dynamic Media {#optional-enable-acl}

When you run Dynamic Media on AEM as a Cloud Service, it currently forwards `/is/image` requests to Secure Preview Image Serving without checking ACL (Access Control List) permissions on the PlatformServerServlet. You can, however, _enable_ ACL permissions. Doing so forwards the authorized `/is/image` requests. If a user is not authorized to access the asset, a "403 - Forbidden" error is displayed.

**To enable Access Control List permissions in Dynamic Media on AEM as a Cloud Service:**

1. From Adobe Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. A new browser tab opens to the **[!UICONTROL Adobe Experience Manager Web Console Configuration]** page.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. On the page, scroll to the name _Adobe CQ Scene7 PlatformServer_.

1. To the right of the name, select the pencil icon (**[!UICONTROL Edit the configuration values]**).

1. On the **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** page, select the check box for the following two settings:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` &ndash; When enabled, this setting caches permission results for two minutes (default) to save.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` &ndash; When enabled, this setting validates a user's access while they preview assets by way of Dynamic Media Image Server.

   ![Enable Access Control List settings in Dynamic Media - Scene7 mode](/help/assets/dynamic-media/assets/acl.png)

1. Near the lower-right corner of the page, select **[!UICONTROL Save]**.
-->

### Impostazione e configurazione delle impostazioni di Dynamic Media (facoltativo) {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilizza l’interfaccia utente di Dynamic Media Classic per modificare le impostazioni di Dynamic Media.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

Le attività di configurazione e configurazione includono:

* [Configurare Impostazione pubblicazione Dynamic Media per il server immagini](#publishing-setup-for-image-server)
* [Configurare le impostazioni generali di Dynamic Media](#configuring-application-general-settings)
* [Configura gestione colore](#configuring-color-management)
* [Modifica tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiungere tipi MIME per formati non supportati](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configurare Impostazione pubblicazione Dynamic Media per il server immagini {#publishing-setup-for-image-server}

La pagina Impostazione pubblicazione Dynamic Media stabilisce le impostazioni predefinite che determinano il modo in cui le risorse vengono distribuite dai server Adobe Dynamic Media ai siti web o alle applicazioni.

Consulta [Configurare l&#39;installazione della pubblicazione Dynamic Media per il server immagini](/help/assets/dynamic-media/dm-publish-settings.md).

#### Configurare le impostazioni generali di Dynamic Media {#configuring-application-general-settings}

Configura l&#39;URL **[!UICONTROL Nome server di pubblicazione]** di Dynamic Media e l&#39;URL **[!UICONTROL Nome server di origine]**. Puoi anche specificare **[!UICONTROL Impostazioni di caricamento nell&#39;applicazione]** e **[!UICONTROL Opzioni di caricamento predefinite]** in base al tuo caso d&#39;uso specifico.

Consulta [Configurare le impostazioni generali di Dynamic Media](/help/assets/dynamic-media/dm-general-settings.md).

#### Configura gestione colore {#configuring-color-management}

La gestione del colore di Dynamic Media consente di correggere il colore delle risorse. Con la correzione del colore, le risorse acquisite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede una rappresentazione dinamica, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio.

Consulta [Configurare i predefiniti immagine](/help/assets/dynamic-media/managing-image-presets.md).

Per configurare le proprietà di colore predefinite per l&#39;abilitazione della correzione del colore durante la richiesta delle immagini:

1. Apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account utilizzando le credenziali fornite durante il provisioning.
1. Vai a **[!UICONTROL Configurazione > Impostazione applicazione]**.
1. Espandi l’area **[!UICONTROL Publish Setup (Impostazione pubblicazione)]** e seleziona **[!UICONTROL Image Server]**. Per le istanze di pubblicazione, imposta **[!UICONTROL Contesto di pubblicazione]** su **[!UICONTROL Image Server]**.
1. Scorri fino alla proprietà che devi modificare, ad esempio una proprietà nell&#39;area **[!UICONTROL Attributi gestione colore]**.
È possibile impostare le seguenti proprietà di correzione del colore:

   | Proprietà | Descrizione |
   |---|---|
   | Spazio colore predefinito CMYK | Nome del profilo colore CMYK predefinito. |
   | Spazio colore predefinito scala di grigi | Nome del profilo colore grigio predefinito. |
   | Spazio colore predefinito RGB | Nome del profilo colore predefinito di RGB. |
   | Intento di rendering per conversione colore | Specifica l&#39;intento di rendering. I valori accettabili sono: **[!UICONTROL percettivo]**, **[!UICONTROL colorimetrico relativo]**, **[!UICONTROL saturazione]**, **[!UICONTROL colorimetrico assoluto]**. Per impostazione predefinita, Adobe consiglia **[!UICONTROL relativo]**. |

1. Seleziona **[!UICONTROL Salva]**.

Ad esempio, puoi impostare **[!UICONTROL Spazio colore predefinito RGB]** su *sRGB* e **[!UICONTROL Spazio colore predefinito CMYK]** su *WebCoated*.

In questo caso, effettua le seguenti operazioni:

* Abilita la correzione del colore per le immagini RGB e CMYK.
* Si presume che le immagini RGB prive di un profilo colore siano nello spazio colore *sRGB*.
* Si presume che le immagini CMYK prive di un profilo colore si trovino nello spazio colore *WebCoated*.
* Le rappresentazioni dinamiche che restituiscono l&#39;output di RGB lo restituiscono nello spazio colore *sRGB*.
* Le rappresentazioni dinamiche che restituiscono l&#39;output CMYK restituiscono tale output nello spazio colore *WebCoated*.

#### Modifica tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Media e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Convertire un’Adobe PDF in una risorsa eCatalog.
* Convertire un documento di Adobe Photoshop (con estensione PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file Adobe Photoshop Encapsulated PostScript® (.EPS).
* È possibile utilizzare [Profili video](/help/assets/dynamic-media/video-profiles.md) e [Profili immagine](/help/assets/dynamic-media/image-profiles.md) per definire rispettivamente l&#39;elaborazione di video e immagini.

Consulta [Caricare risorse](/help/assets/add-assets.md).

**Per modificare i tipi MIME per i formati supportati:**

1. Accedi al tuo as a Cloud Service di Experience Manager come amministratore del prodotto.
1. In Experience Manager as a Cloud Service , seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale, quindi passa a **[!UICONTROL Generale > CRXDE Lite]**.

   Se non hai accesso a CRXDE Lite, vedi [Utilizzo di CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. Nella barra a sinistra, accedi a:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes, seleziona un tipo MIME.
1. Nella parte inferiore, sul lato destro della pagina CRXDE Lite:

   * Selezionare due volte il campo **[!UICONTROL enabled]**. Per impostazione predefinita, tutti i tipi MIME di risorse sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse vengono sincronizzate in Dynamic Media per l&#39;elaborazione. Se vuoi escludere questo tipo di risorsa MIME dall&#39;elaborazione, modifica questa impostazione in **[!UICONTROL false]**.

   * Selezionare **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Per un elenco dei valori dei parametri di elaborazione consentiti che è possibile utilizzare per un determinato tipo MIME, vedere [Tipi MIME supportati](/help/assets/file-format-support.md).

1. Effettua una delle seguenti operazioni:
   * Ripeti i passaggi 3-4 per modificare più tipi MIME.
   * Nella barra dei menu della pagina CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

1. Nell&#39;angolo superiore sinistro della pagina, seleziona **[!UICONTROL CRXDE Lite]** per tornare ad Experience Manager as a Cloud Service.

#### Aggiungere tipi MIME per formati non supportati {#adding-mime-types-for-unsupported-formats}

In Experience Manager Assets è possibile aggiungere tipi MIME personalizzati per formati non supportati. Per garantire che Experience Manager non elimini eventuali nuovi nodi aggiunti in CRXDE Lite, sposta il tipo MIME prima di `image_`. Inoltre, assicurati che il relativo valore abilitato sia impostato su **[!UICONTROL false]**.

**Per aggiungere tipi MIME per formati non supportati:**

1. Accedi al tuo as a Cloud Service di Experience Manager come amministratore del prodotto.
1. Da Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti > Operazioni > Console Web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser alla pagina **[!UICONTROL Configurazione console Web Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, selezionare **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![Modifica i valori di configurazione](assets/2019-08-02_16-44-56.png)

1. Nella pagina **Adobe CQ Scene7 Asset MIME type Service**, seleziona un&#39;icona con il segno più &lt;+>. La posizione nella tabella in cui si seleziona il segno più per aggiungere il nuovo tipo MIME è insignificante.

   ![Servizio tipo MIME risorse Adobe CQ Scene7](assets/2019-08-02_16-27-27.png)

1. Digitare `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   Il tipo MIME `DWG=image/vnd.dwg` è solo a scopo di esempio. Il tipo MIME aggiunto qui può essere qualsiasi altro formato non supportato.

   ![Aggiunta tipo MIME DWG](assets/2019-08-02_16-36-36.png)

1. Nell&#39;angolo inferiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser che include la pagina Apri configurazione console Web Adobe Experience Manager.

1. Torna alla scheda del browser che presenta la console as a Cloud Service di Experience Manager aperta.
1. Da Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti > Generale > CRXDE Lite]**.

   Se non hai accesso a CRXDE Lite, vedi [Utilizzo di CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![Strumenti > Generale > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, accedi a:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo MIME `image_vnd.dwg` e rilascialo direttamente sopra `image_` nella struttura, come illustrato nella schermata seguente.

   ![Modifica di un file DWG in CRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo MIME `image_vnd.dwg` ancora selezionato, dalla scheda **[!UICONTROL Proprietà]**, nella riga **[!UICONTROL enabled]**, nell&#39;intestazione della colonna **[!UICONTROL Valore]**, selezionare due volte il valore. L&#39;elenco a discesa **[!UICONTROL Value]** è aperto.
1. Digita `false` nel campo (oppure seleziona **[!UICONTROL false]** dall&#39;elenco a discesa).

   ![Modifica dei tipi MIME in CRXDE Lite](assets/2019-08-02_16-60-30.png)

1. Selezionare **[!UICONTROL Salva tutto]** nell&#39;angolo superiore sinistro della pagina CRXDE Lite.

### (Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per garantire il corretto funzionamento di Dynamic Media <!--(with `dynamicmedia_scene7` run mode)-->, Adobe consiglia i seguenti suggerimenti per l&#39;ottimizzazione delle prestazioni e della scalabilità della sincronizzazione:

* [Aggiorna i parametri predefiniti del processo per l&#39;elaborazione di diversi formati di file](#update-job-para).
* [Aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro di Granite (risorse video)](#update-granite-workflow-queue-worker-threads-video)
* [Aggiorna i thread di lavoro predefiniti della coda del flusso di lavoro transitorio di Granite (immagini e risorse non video)](#update-granite-transient-workflow-queue-worker-threads-images).
* [Aggiorna il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7)](#update-max-s7-upload-connections).

#### Aggiornare i parametri predefiniti del job per l&#39;elaborazione di diversi formati di file {#update-job-para}

Puoi regolare i parametri dei processi per velocizzare l’elaborazione quando carichi i file. Ad esempio, se caricate i file PSD ma non desiderate elaborarli come modelli, potete impostare l&#39;estrazione dei livelli su false (off). In questo caso, il parametro del processo ottimizzato viene visualizzato come segue: `process=None&createTemplate=false`.

Se si desidera attivare la creazione del modello, utilizzare i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe consiglia di utilizzare i seguenti parametri di processo &quot;ottimizzati&quot; per i file PDF, PostScript® e PSD:

| Tipo di file | Parametri di processo consigliati |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno di questi parametri, vedere [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats).

Vedi anche [Aggiunta di tipi MIME per formati non supportati](#adding-mime-types-for-unsupported-formats).

#### Aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro di Granite (risorse video) {#update-granite-workflow-queue-worker-threads-video}

La coda del flusso di lavoro Granite viene utilizzata per flussi di lavoro non transitori. In Dynamic Media veniva utilizzato per elaborare video con il flusso di lavoro **[!UICONTROL Codifica video elementi multimediali dinamici]**.

>[!NOTE]
>
>Per completare questa attività, devi aver effettuato l’accesso ad Experience Manager as a Cloud Service in qualità di amministratore del prodotto.

Se non hai accesso a OSGi, consulta [Configurazione OSGi](/help/implementing/developing/components/overview.md#osgi-configuration).

**Per aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro di Granite (risorse video):**

1. Passare a `https://<server>/system/console/configMgr` e cercare **Coda: coda flusso di lavoro Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Maximum Parallel Jobs]** (Numero massimo processi paralleli), modifica il numero impostando il valore desiderato.

   Per impostazione predefinita, il numero massimo di processi paralleli dipende dal numero di core CPU disponibili. Ad esempio, in un server a 4 core, vengono assegnati due thread di lavoro. (Un valore compreso tra 0,0 e 1,0 è basato sul rapporto oppure qualsiasi numero maggiore di uno assegna il numero di thread di lavoro.)

   Per la maggior parte dei casi d’uso è sufficiente l’impostazione predefinita 0.5.

   ![Configurazione di una coda di elaborazione del processo](assets/chlimage_1-1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiorna i thread di lavoro predefiniti della coda del flusso di lavoro transitorio di Granite {#update-granite-transient-workflow-queue-worker-threads-images}

La coda del flusso di lavoro di transito Granite è utilizzata per il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**. In Dynamic Media, viene utilizzato per l’acquisizione e l’elaborazione di risorse video e non.

>[!NOTE]
>
>Per completare questa attività, devi aver effettuato l’accesso ad Experience Manager as a Cloud Service in qualità di amministratore del prodotto.

**Per aggiornare i thread di lavoro della coda del flusso di lavoro transitorio di Granite predefiniti:**

1. Passa alla **configurazione console Web Adobe Experience Manager** in `http://<host>:<port>/system/console/configMgr`
1. Cerca **Coda: coda flusso di lavoro transitorio Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Maximum Parallel Jobs]** (Numero massimo processi paralleli), modifica il numero impostando il valore desiderato.

   Puoi aumentare il numero massimo di **[!UICONTROL processi paralleli]** per supportare adeguatamente il caricamento di file in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ad esempio una migrazione iniziale o un caricamento in blocco una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (ad esempio due volte il numero di core) può avere effetti negativi su altre attività simultanee. In questo modo, testa e regola il valore in base al tuo caso d’uso particolare.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiornare il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7) {#update-max-s7-upload-connections}

L’impostazione Dynamic Media Classic (Scene7) Upload Connection sincronizza le risorse Experience Manager con i server Dynamic Media Classic.

>[!NOTE]
>
>Per completare questa attività, devi aver effettuato l’accesso ad Experience Manager as a Cloud Service in qualità di amministratore del prodotto.

**Per aggiornare il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7):**

1. Passa a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. Nel campo **[!UICONTROL Numero di connessioni]**, nel campo **[!UICONTROL Timeout processo attivo]** o in entrambi, modificare il numero come desiderato.

   L&#39;impostazione **[!UICONTROL Numero di connessioni]** controlla il numero massimo di connessioni HTTP consentite per il caricamento da Experience Manager a Dynamic Media. In genere, il valore predefinito di dieci connessioni è sufficiente.

   L&#39;impostazione **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per la pubblicazione delle risorse Dynamic Media caricate nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

   Per la maggior parte dei casi d’uso è sufficiente impostare 2100.

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
