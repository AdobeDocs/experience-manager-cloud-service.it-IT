---
title: Configura Cloud Service Dynamic Medie
description: Scopri come configurare Dynamic Medie in Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '3794'
ht-degree: 3%

---

# Informazioni sulla configurazione del Cloud Service Dynamic Medie {#configuring-dynamic-media}

Se utilizzi Adobe Experience Manager per diversi ambienti, ad esempio sviluppo, staging e produzione live, configura i Cloud Service Dynamic Medie per ciascuno di questi ambienti.

Vedi anche [Configurare un account alias società Dynamic Medie](/help/assets/dynamic-media/dm-alias-account.md)

## Diagramma dell’architettura di Dynamic Medie {#architecture-diagram-of-dynamic-media}

Il diagramma seguente descrive l’architettura di Dynamic Medie.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primaria e si sincronizza con Dynamic Medie per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa di origine principale viene caricata in Adobe Experience Manager as a Cloud Service, viene replicata in Dynamic Medie. A questo punto, Dynamic Medie gestisce tutte le attività di elaborazione delle risorse e generazione del rendering, come la codifica video e le varianti dinamiche di un’immagine.
1. Dopo la generazione delle rappresentazioni, Experience Manager as a Cloud Service può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni remote di Dynamic Medie (nessun binario viene rimandato all’istanza Experience Manager as a Cloud Service).
1. Quando il contenuto è pronto per essere pubblicato e approvato, attiva il servizio Dynamic Medie per inviare contenuti ai server di distribuzione e memorizzarli nella cache della rete CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>Il seguente elenco di funzioni richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager - Dynamic Medie. Qualsiasi altra rete CDN personalizzata non è supportata con queste funzioni.
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

## Creare una configurazione Dynamic Medie in Cloud Service {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. In Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. A sinistra della console, seleziona l’icona Strumenti, quindi vai a **[!UICONTROL Cloud Service > Configurazione Dynamic Medie]**.
1. Nella pagina Browser configurazioni Dynamic Medie, nel riquadro a sinistra, selezionare **[!UICONTROL globale]** (non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL globale]**). Quindi seleziona **[!UICONTROL Crea]**.
1. Il giorno **[!UICONTROL Crea configurazione Dynamic Medie]** pagina, immetti il titolo, l’indirizzo e-mail dell’account Dynamic Medie e la password dell’amministratore aziendale dell’account Dynamic Medie, quindi seleziona la tua area geografica. Queste informazioni sono fornite da un Adobe nell’e-mail di provisioning. Se non hai ricevuto questa e-mail, contatta l’Assistenza clienti Adobe.
1. Seleziona **[!UICONTROL Connetti a Dynamic Medie]**.
1. In **[!UICONTROL Cambia password]** nella finestra di dialogo **[!UICONTROL Nuova password]** immettere una nuova password composta da 8-25 caratteri. La password deve contenere almeno uno dei seguenti elementi:

   * Lettera maiuscola
   * Lettera minuscola
   * Numero
   * Carattere speciale: `# $ & . - _ : { }`

   Il **[!UICONTROL Password corrente]** il campo è intenzionalmente precompilato e nascosto dall’interazione.

   Se necessario, è possibile controllare l&#39;ortografia di una password digitata o ridigitata selezionando l&#39;icona dell&#39;occhio della password per visualizzare la password. Seleziona nuovamente l’icona per nascondere la password.

1. In **[!UICONTROL Ripeti password]** , ridigitare la nuova password, quindi selezionare **[!UICONTROL Fine]**.

   La nuova password viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro del **[!UICONTROL Crea configurazione Dynamic Medie]** pagina.

   Se hai selezionato **[!UICONTROL Annulla]** nel **[!UICONTROL Cambia password]** , è comunque necessario immettere una nuova password quando si salva la configurazione di Dynamic Medie appena creata.

   Vedi anche [Cambia la password in Dynamic Medie](#change-dm-password).

1. Quando la connessione ha esito positivo, puoi impostare quanto segue:

   | Proprietà | Descrizione |
   |---|---|
   | Azienda | Nome dell’account Dynamic Medie.<br>**Importante**: in un’istanza di Experience Manager è supportata una sola configurazione Dynamic Medie nei Cloud Service; non aggiungere più di una configurazione. Più configurazioni Dynamic Medie in un’istanza Experience Manager sono _non_ supportati o consigliati dall’Adobe.<!-- CQDOC-19579 and CQDOC-19612 --><br>Vedi anche [Configurare un account alias società Dynamic Medie](/help/assets/dynamic-media/dm-alias-account.md). |
   | Percorso cartella principale della società | Percorso della cartella principale della società. |
   | Pubblicazione delle risorse | Puoi scegliere tra le tre opzioni seguenti:<br>**[!UICONTROL Immediatamente ]**- Quando le risorse vengono caricate, il sistema le acquisisce e fornisce immediatamente l’URL/Incorpora. Non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.<br>**[!UICONTROL Al momento dell’attivazione]** : devi pubblicare esplicitamente la risorsa prima di fornire un URL/collegamento di incorporamento.<br>**[!UICONTROL Pubblicazione selettiva ]**: le risorse vengono pubblicate automaticamente solo per l’anteprima protetta. Possono anche essere pubblicati in modo esplicito in Experience Manager as a Cloud Service senza dover essere pubblicati in DMS7 per la distribuzione nel dominio pubblico. In futuro, questa opzione prevede di pubblicare le risorse su Experience Manager as a Cloud Service e di pubblicare le risorse su Dynamic Medie, escludendosi a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. In alternativa, puoi pubblicare le risorse esclusivamente in Experience Manager as a Cloud Service per la visualizzazione in anteprima; le stesse risorse non vengono pubblicate in DMS7 per la distribuzione nel dominio pubblico. |
   | Server di anteprima protetto | Consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, Experience Manager as a Cloud Service può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni remote di Dynamic Medie (nessun binario viene rimandato all’istanza Experience Manager as a Cloud Service).<br>Adobe A meno che non si disponga di una disposizione speciale per utilizzare il server della propria società o un server speciale, si consiglia di lasciare questa impostazione come specificato. |
   | Sincronizza tutti i contenuti | Selezionata per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere selettivamente le risorse dalla sincronizzazione con Dynamic Medie. Deselezionando questa opzione è possibile scegliere tra le due seguenti modalità di sincronizzazione di Dynamic Medie:<br>**[!UICONTROL Modalità di sincronizzazione Dynamic Medie]**<br>**[!UICONTROL Attiva per impostazione predefinita ]**: la configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non contrassegni una cartella specificamente per l’esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabilitata per impostazione predefinita]** - La configurazione non viene applicata ad alcuna cartella finché non contrassegni esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Medie.<br>Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Medie, seleziona una cartella di risorse, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**. Il giorno **[!UICONTROL Dettagli]** , nella scheda **[!UICONTROL Modalità di sincronizzazione Dynamic Medie]** scegliere tra le tre opzioni seguenti. Al termine, seleziona **[!UICONTROL Salva]**. _Ricorda: queste tre opzioni non sono disponibili se hai selezionato **Sincronizza tutto il contenuto**prima._ Vedi anche [Utilizzare la pubblicazione selettiva a livello di cartella in Dynamic Medie](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Ereditato ]**- Nessun valore di sincronizzazione esplicito nella cartella. Al contrario, la cartella eredita il valore di sincronizzazione da una delle sue cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per ereditato viene visualizzato tramite una descrizione comando.<br>**[!UICONTROL Attiva per sottocartelle]** : include tutto il contenuto di questo sottoalbero per la sincronizzazione con Dynamic Medie. Le impostazioni specifiche della cartella sovrascrivono la modalità predefinita nella configurazione cloud.<br>**[!UICONTROL Disattivato per le sottocartelle ]**: escludi tutti gli elementi di questo sottoalbero dalla sincronizzazione con Dynamic Medie. |

   >[!NOTE]
   >
   >In Dynamic Media non è supportato il controllo delle versioni. Inoltre, l&#39;attivazione ritardata si applica solo se **[!UICONTROL Pubblicare le risorse]** nella pagina Modifica configurazione Dynamic Medie è impostato su **[!UICONTROL All&#39;attivazione]**. E poi, solo fino alla prima volta che la risorsa viene attivata.
   >
   >
   >Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale in S7 Delivery.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Seleziona **[!UICONTROL Salva]**. La nuova password e la nuova configurazione di Dynamic Medie vengono salvate. Se hai selezionato **[!UICONTROL Annulla]** non si verifica alcun aggiornamento della password.
1. In **[!UICONTROL Configurazione di Dynamic Medie]** finestra di dialogo, seleziona **[!UICONTROL OK]** per iniziare la configurazione.

   >[!IMPORTANT]
   >
   >Al termine dell’installazione della nuova configurazione di Dynamic Medie, verrà inviata una notifica nella casella in entrata di Experience Manager as a Cloud Service.
   >
   >Questa notifica della casella in entrata ti informa se la configurazione è stata eseguita correttamente o meno.
   > Consulta [Risoluzione dei problemi relativi a una nuova configurazione di Dynamic Medie](#troubleshoot-dm-config) e [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md) per ulteriori informazioni.

1. Per visualizzare in anteprima in modo sicuro il contenuto Dynamic Medie prima che venga pubblicato, Experience Manager as a Cloud Service utilizza la convalida basata su token e quindi per impostazione predefinita Dynamic Medie viene visualizzata in anteprima da Experience Manager Author. Tuttavia, è possibile *INSERISCO NELL&#39;ELENCO CONSENTITI DI* più IP per consentire agli utenti di accedere ai contenuti in anteprima in modo sicuro. Per impostare questa azione in Experience Manager as a Cloud Service, consulta [Configurazione di Dynamic Medie Publish Setup per il server immagini: scheda Sicurezza](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

La configurazione di base è stata completata; è possibile utilizzare Dynamic Medie.

Se si desidera personalizzare ulteriormente la configurazione, ad esempio abilitando le autorizzazioni ACL (Access Control List), è possibile completare una qualsiasi delle operazioni descritte in [Configurare le impostazioni avanzate in Dynamic Medie](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Risoluzione dei problemi relativi a una nuova configurazione di Dynamic Medie {#troubleshoot-dm-config}

Al termine dell’installazione di una nuova configurazione di Dynamic Medie, viene inviata una notifica nella casella in entrata di Experience Manager as a Cloud Service. Questa notifica ti informa se la configurazione è avvenuta con successo o meno, come mostrato nelle rispettive immagini seguenti provenienti dalla casella in entrata.

![Casella in entrata Experience Manager completata](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Errore casella in entrata Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Vedi anche [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md).

**Per risolvere i problemi relativi a una nuova configurazione di Dynamic Medie:**

1. Seleziona l’icona a forma di campana nell’angolo in alto a destra della pagina di Experience Manager as a Cloud Service, quindi fai clic su **[!UICONTROL Visualizza tutto]**.
1. Nella pagina Casella in entrata, seleziona la notifica di successo per leggere una panoramica dello stato e dei registri della configurazione.

   Se la configurazione non è riuscita, seleziona la notifica di errore simile alla schermata seguente.

   ![Installazione di Dynamic Medie non riuscita](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Il giorno **[!UICONTROL DMSETUP]** , rivedere i dettagli di configurazione che descrivono l&#39;errore. In particolare, prendi nota di eventuali messaggi di errore o codici di errore. Contatta l’Assistenza clienti Adobe con queste informazioni.

   ![Pagina di configurazione Dynamic Medie](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Cambia la password in Dynamic Medie {#change-dm-password}

La scadenza della password in Dynamic Medie è impostata su 100 anni dalla data di sistema corrente.

La password deve contenere almeno uno dei seguenti elementi:

* Lettera maiuscola
* Lettera minuscola
* Numero
* Carattere speciale: `# $ & . - _ : { }`

Se necessario, è possibile controllare l&#39;ortografia di una password digitata o ridigitata selezionando l&#39;icona dell&#39;occhio della password per visualizzare la password. Seleziona nuovamente l’icona per nascondere la password.

La password modificata viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro del **[!UICONTROL Modifica configurazione Dynamic Medie]** pagina.

1. In Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. A sinistra della console, seleziona l’icona Strumenti, quindi vai a **[!UICONTROL Cloud Service > Configurazione Dynamic Medie]**.
1. Nella pagina Browser configurazioni Dynamic Medie, nel riquadro a sinistra, selezionare **[!UICONTROL globale]**. Non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL globale]**. Quindi, seleziona **[!UICONTROL Modifica]**.
1. Il giorno **[!UICONTROL Modifica configurazione Dynamic Medie]** direttamente sotto il **[!UICONTROL Password]** campo, seleziona **[!UICONTROL Cambia password]**.
1. In **[!UICONTROL Cambia password]** eseguire le operazioni seguenti:

   * In **[!UICONTROL Nuova password]** , immettere una nuova password.

     Il **[!UICONTROL Password corrente]** il campo è intenzionalmente precompilato e nascosto dall’interazione.

   * In **[!UICONTROL Ripeti password]** , ridigitare la nuova password, quindi selezionare **[!UICONTROL Fine]**.

1. Nell&#39;angolo superiore destro del **[!UICONTROL Modifica configurazione Dynamic Medie]** pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]**.

## (Facoltativo) Configurazione delle impostazioni avanzate in Dynamic Medie{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Per personalizzare ulteriormente la configurazione e la configurazione di Dynamic Medie o ottimizzarne le prestazioni, è possibile completare una o più delle operazioni seguenti _facoltativo_ attività:

* [Abilitare le autorizzazioni ACL in Dynamic Medie (facoltativo)](#optional-enable-acl)
* [(Facoltativo) Configurazione delle impostazioni di Dynamic Medie](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Facoltativo) Ottimizzazione delle prestazioni di Dynamic Medie](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Facoltativo) Abilitare le autorizzazioni dell’elenco di controllo di accesso in Dynamic Medie {#optional-enable-acl}

Quando esegui Dynamic Medie su AEM, attualmente inoltra `/is/image` Richieste a Secure Preview Image Server senza verificare le autorizzazioni ACL (Access Control List) in Platform ServerServlet. Tuttavia, puoi: _abilita_ autorizzazioni ACL. In tal modo, il `/is/image` richieste. Se un utente non è autorizzato ad accedere alla risorsa, viene visualizzato un errore &quot;403 - Non consentito&quot;.

**Per abilitare le autorizzazioni ACL in Dynamic Medie:**

1. Da Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser **[!UICONTROL Configurazione console Web Adobe Experience Manager]** pagina.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri fino al nome _Adobe CQ Scene7 Platform Server_.

1. A destra del nome, seleziona l’icona della matita (**[!UICONTROL Modificare i valori di configurazione]**).

1. Il giorno **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** , selezionare la casella di controllo per le due impostazioni seguenti:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` - Se attivata, questa impostazione memorizza in cache i risultati delle autorizzazioni per due minuti (impostazione predefinita) per il salvataggio.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` : se selezionata, questa impostazione convalida l’accesso di un utente che visualizza l’anteprima delle risorse tramite Dynamic Medie Image Server.

   ![Abilitare le impostazioni dell’elenco di controllo degli accessi in modalità Dynamic Medie - Scene7](/help/assets/dynamic-media/assets/acl.png)

1. Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Salva]**.

### (Facoltativo) Configurazione delle impostazioni di Dynamic Medie {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilizza l’interfaccia utente di Dynamic Media Classic per modificare le impostazioni del Dynamic Medie.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

Le attività di configurazione e configurazione includono:

* [Configurare Impostazione pubblicazione Dynamic Medie per il server immagini](#publishing-setup-for-image-server)
* [Configurazione impostazioni generali di Dynamic Medie](#configuring-application-general-settings)
* [Configura gestione colore](#configuring-color-management)
* [Modifica tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiungere tipi MIME per formati non supportati](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configurare Impostazione pubblicazione Dynamic Medie per il server immagini {#publishing-setup-for-image-server}

La pagina Impostazione pubblicazione di Dynamic Medie stabilisce le impostazioni predefinite che determinano il modo in cui le risorse vengono consegnate dai server Adobe Dynamic Medie ai siti web o alle applicazioni.

Consulta [Configurare Impostazione pubblicazione Dynamic Medie per il server immagini](/help/assets/dynamic-media/dm-publish-settings.md).

#### Configurazione impostazioni generali di Dynamic Medie {#configuring-application-general-settings}

Configurare Dynamic Medie **[!UICONTROL Nome server di pubblicazione]** URL e **[!UICONTROL Nome server di origine]** URL. Puoi anche specificare **[!UICONTROL Carica nell&#39;applicazione]** impostazioni e **[!UICONTROL Opzioni di caricamento predefinite]** tutto in base al tuo caso d’uso particolare.

Consulta [Configurazione impostazioni generali di Dynamic Medie](/help/assets/dynamic-media/dm-general-settings.md).

#### Configura gestione colore {#configuring-color-management}

La gestione del colore di Dynamic Medie consente di correggere il colore delle risorse. Con la correzione del colore, le risorse acquisite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede una rappresentazione dinamica, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio.

Consulta [Configura predefiniti immagine](/help/assets/dynamic-media/managing-image-presets.md).

Per configurare le proprietà di colore predefinite per l&#39;abilitazione della correzione del colore durante la richiesta delle immagini:

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account utilizzando le credenziali fornite durante il provisioning.
1. Vai a **[!UICONTROL Configurazione > Impostazione applicazione]**.
1. Espandi l’area **[!UICONTROL Publish Setup (Impostazione pubblicazione)]** e seleziona **[!UICONTROL Image Server]**. Per le istanze di pubblicazione, imposta **[!UICONTROL Contesto di pubblicazione]** su **[!UICONTROL Image Server]**.
1. Scorri fino alla proprietà da modificare, ad esempio una proprietà in **[!UICONTROL Attributi gestione colore]** area.
È possibile impostare le seguenti proprietà di correzione del colore:

   | Proprietà | Descrizione |
   |---|---|
   | Spazio colore predefinito CMYK | Nome del profilo colore CMYK predefinito. |
   | Spazio colore predefinito scala di grigi | Nome del profilo colore grigio predefinito. |
   | Spazio colore predefinito RGB | Nome del profilo colore RGB predefinito. |
   | Intento di rendering per conversione colore | Specifica l&#39;intento di rendering. I valori accettabili sono: **[!UICONTROL percettivo]**, **[!UICONTROL colorimetrico relativo]**, **[!UICONTROL saturazione]**, **[!UICONTROL colorimetrico assoluto]**. Adobe di consigli **[!UICONTROL relativo]** come impostazione predefinita. |

1. Seleziona **[!UICONTROL Salva]**.

Ad esempio, puoi impostare **[!UICONTROL Spazio colore predefinito RGB]** su *sRGB* e **[!UICONTROL Spazio colore predefinito CMYK]** su *WebCoated*.

In questo caso, effettua le seguenti operazioni:

* Abilita la correzione del colore per le immagini RGB e CMYK.
* Le immagini RGB che non hanno un profilo colore sono considerate nel *sRGB* spazio colore.
* Le immagini CMYK che non hanno un profilo colore sono considerate *WebCoated* spazio colore.
* Le rappresentazioni dinamiche che restituiscono l’output di RGB lo restituiscono nella *sRGB* spazio colore.
* Le rappresentazioni dinamiche che restituiscono l’output CMYK, lo restituiscono nella *WebCoated* spazio colore.

#### Modifica tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Medie e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Convertire un’Adobe PDF in una risorsa eCatalog.
* Converti un documento di Adobe Photoshop (con estensione PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file Adobe Photoshop Encapsulated PostScript® (.EPS).
* [Profili video](/help/assets/dynamic-media/video-profiles.md) e [Profili immagine](/help/assets/dynamic-media/image-profiles.md) può essere utilizzato rispettivamente per definire l’elaborazione di video e immagini.

Consulta [Caricare le risorse](/help/assets/add-assets.md).

**Per modificare i tipi MIME per i formati supportati:**

1. Accedi al tuo Experience Manager as a Cloud Service come amministratore del prodotto.
1. In Experience Manager as a Cloud Service , seleziona il logo di Experience Manager as a Cloud Service per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Generale > CRXDE Lite]**.

   Se non hai accesso a CRXDE Liti, consulta [Utilizzo di CRXDE Liti](/help/implementing/developing/tools/crxde.md).

1. Nella barra a sinistra, accedi a:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes, seleziona un tipo MIME.
1. Nella parte inferiore, sul lato destro della pagina CRXDE Liti:

   * Tocca due volte il **[!UICONTROL abilitato]** campo. Per impostazione predefinita, tutti i tipi MIME di risorse sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse vengono sincronizzate in Dynamic Medie per l’elaborazione. Se desideri escludere questo tipo di risorsa MIME dall’elaborazione, modifica questa impostazione in **[!UICONTROL false]**.

   * Doppio tocco **[!UICONTROL jobParam]** per aprire il campo di testo associato. Consulta [Tipi MIME supportati](/help/assets/file-format-support.md) per un elenco dei valori dei parametri di elaborazione consentiti che è possibile utilizzare per un determinato tipo MIME.

1. Effettua una delle operazioni seguenti:
   * Ripeti i passaggi 3-4 per modificare più tipi MIME.
   * Nella barra dei menu della pagina CRXDE Liti, seleziona **[!UICONTROL Salva tutto]**.

1. Nell’angolo superiore sinistro della pagina, seleziona **[!UICONTROL CRXDE Liti]** per tornare a Experience Manager as a Cloud Service.

#### Aggiungere tipi MIME per formati non supportati {#adding-mime-types-for-unsupported-formats}

In Experience Manager Assets è possibile aggiungere tipi MIME personalizzati per formati non supportati. Per evitare che un nuovo nodo aggiunto in CRXDE Liti venga eliminato da Experience Manager, sposta il tipo MIME prima di `image_`. Inoltre, assicurati che il relativo valore abilitato sia impostato su **[!UICONTROL false]**.

**Per aggiungere tipi MIME per formati non supportati:**

1. Accedi al tuo Experience Manager as a Cloud Service come amministratore del prodotto.
1. Da Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti > Operazioni > Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser **[!UICONTROL Configurazione console Web Adobe Experience Manager]** pagina.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, tocca **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![Modificare i valori di configurazione](assets/2019-08-02_16-44-56.png)

1. Il giorno **Servizio di tipo MIME risorse Scene7 di Adobe CQ** , selezionare un&#39;icona del segno più &lt;+>. La posizione nella tabella in cui si seleziona il segno più per aggiungere il nuovo tipo MIME è insignificante.

   ![Servizio Adobe CQ Scene7 Asset Mime Type](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   Il `DWG=image/vnd.dwg` Il tipo MIME è solo a scopo di esempio. Il tipo MIME aggiunto qui può essere qualsiasi altro formato non supportato.

   ![Aggiunta del tipo MIME DWG](assets/2019-08-02_16-36-36.png)

1. Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser che include la pagina Apri configurazione console Web Adobe Experience Manager.

1. Torna alla scheda del browser che presenta la console aperta as a Cloud Service in Experience Manager.
1. Da Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti > Generale > CRXDE Lite]**.

   Se non hai accesso a CRXDE Liti, consulta [Utilizzo di CRXDE Liti](/help/implementing/developing/tools/crxde.md).

   ![Strumenti > Generale > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, accedi a:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo MIME `image_vnd.dwg` e rilascialo direttamente sopra `image_` nell&#39;albero come mostrato nella schermata seguente.

   ![Modifica di un file DWG in CRXDE Liti](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo MIME `image_vnd.dwg` ancora selezionato, da **[!UICONTROL Proprietà]** , nella scheda **[!UICONTROL abilitato]** riga, sotto **[!UICONTROL Valore]** , toccare due volte il valore. Il **[!UICONTROL Valore]** viene aperto l’elenco a discesa.
1. Tipo `false` nel campo (o seleziona **[!UICONTROL false]** dall’elenco a discesa).

   ![Modifica dei tipi MIME in CRXDE Liti](assets/2019-08-02_16-60-30.png)

1. Nell&#39;angolo superiore sinistro della pagina CRXDE Liti, seleziona **[!UICONTROL Salva tutto]**.

### (Facoltativo) Ottimizzazione delle prestazioni di Dynamic Medie {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per mantenere Dynamic Medie <!--(with `dynamicmedia_scene7` run mode)--> senza problemi, Adobe consiglia i seguenti suggerimenti per l’ottimizzazione delle prestazioni e della scalabilità della sincronizzazione:

* [Aggiornare i parametri predefiniti del job per l&#39;elaborazione di diversi formati di file](#update-job-para).
* [Aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro di Granite (risorse video)](#update-granite-workflow-queue-worker-threads-video)
* [Aggiorna i thread di lavoro predefiniti della coda di flusso di lavoro transitorio di Granite (immagini e risorse non video)](#update-granite-transient-workflow-queue-worker-threads-images).
* [Aggiornare il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7)](#update-max-s7-upload-connections).

#### Aggiornare i parametri predefiniti del job per l&#39;elaborazione di diversi formati di file {#update-job-para}

Puoi regolare i parametri dei processi per velocizzare l’elaborazione quando carichi i file. Ad esempio, se caricate i file PSD ma non desiderate elaborarli come modelli, potete impostare l&#39;estrazione del livello su false (off). In tal caso, il parametro del processo ottimizzato viene visualizzato come segue: `process=None&createTemplate=false`.

Se desideri attivare la creazione di modelli, utilizza i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

L’Adobe consiglia di utilizzare i seguenti parametri di processo &quot;ottimizzati&quot; per i file PDF, PostScript® e PSD:

| Tipo di file | Parametri di processo consigliati |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno di questi parametri, vedi [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats).

Vedi anche [Aggiunta di tipi MIME per formati non supportati](#adding-mime-types-for-unsupported-formats).

#### Aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro di Granite (risorse video) {#update-granite-workflow-queue-worker-threads-video}

La coda del flusso di lavoro Granite viene utilizzata per flussi di lavoro non transitori. In Dynamic Medie, utilizzava per elaborare i video con **[!UICONTROL Codifica video Dynamic Medie]** flusso di lavoro.

>[!NOTE]
>
>Per completare questa attività, devi aver effettuato l’accesso ad Experience Manager as a Cloud Service come amministratore del prodotto.

Se non hai accesso a OSGi, consulta [Configurazione OSGi](/help/implementing/developing/components/overview.md#osgi-configuration).

**Per aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro di Granite (risorse video):**

1. Accedi a `https://<server>/system/console/configMgr` e cerca **Coda: coda del flusso di lavoro Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. In **[!UICONTROL Numero massimo processi paralleli]** , modificare il numero nel valore desiderato.

   Per impostazione predefinita, il numero massimo di processi paralleli dipende dal numero di core CPU disponibili. Ad esempio, in un server a 4 core, vengono assegnati due thread di lavoro. (Un valore compreso tra 0,0 e 1,0 è basato sul rapporto oppure qualsiasi numero maggiore di uno assegna il numero di thread di lavoro.)

   Per la maggior parte dei casi d’uso è sufficiente l’impostazione predefinita 0.5.

   ![Configurazione di una coda di elaborazione del processo](assets/chlimage_1-1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiorna i thread di lavoro predefiniti della coda del flusso di lavoro transitorio di Granite {#update-granite-transient-workflow-queue-worker-threads-images}

La coda del flusso di lavoro di Granite Transit viene utilizzata per **[!UICONTROL Aggiorna risorsa DAM]** flusso di lavoro. In Dynamic Medie, viene utilizzato per l’acquisizione e l’elaborazione di risorse immagini e non video.

>[!NOTE]
>
>Per completare questa attività, devi aver effettuato l’accesso ad Experience Manager as a Cloud Service come amministratore del prodotto.

**Per aggiornare i thread di lavoro predefiniti della coda del flusso di lavoro transitorio di Granite:**

1. Accedi a **Configurazione console Web Adobe Experience Manager** a `http://<host>:<port>/system/console/configMgr`
1. Cerca **Coda: coda del flusso di lavoro transitorio Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. In **[!UICONTROL Numero massimo processi paralleli]** , modificare il numero nel valore desiderato.

   Puoi aumentare **[!UICONTROL Numero massimo processi paralleli]** per supportare adeguatamente il caricamento di file in Dynamic Medie. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ad esempio una migrazione iniziale o un caricamento in blocco una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (ad esempio due volte il numero di core) può avere effetti negativi su altre attività simultanee. In questo modo, testa e regola il valore in base al tuo caso d’uso particolare.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiornare il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7) {#update-max-s7-upload-connections}

L’impostazione Carica connessione di Dynamic Media Classic (Scene7) sincronizza le risorse Experience Manager con i server Dynamic Media Classic.

>[!NOTE]
>
>Per completare questa attività, devi aver effettuato l’accesso ad Experience Manager as a Cloud Service come amministratore del prodotto.

**Per aggiornare il numero massimo di connessioni di caricamento al server Dynamic Media Classic (Scene7):**

1. Accedi a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. In **[!UICONTROL Numero di connessioni]** o il **[!UICONTROL Timeout processo attivo]** o entrambi, modificare il numero come desiderato.

   Il **[!UICONTROL Numero di connessioni]** l&#39;impostazione controlla il numero massimo di connessioni HTTP consentite, ad Experience Manager al caricamento Dynamic Medie. In genere, il valore predefinito di dieci connessioni è sufficiente.

   Il **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per la pubblicazione delle risorse Dynamic Medie caricate nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

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
