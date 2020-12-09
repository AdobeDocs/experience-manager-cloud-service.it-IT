---
title: Configurazione del Cloud Service Dynamic Media
description: Informazioni su come configurare Dynamic Media in Adobe Experience Manager come Cloud Service.
translation-type: tm+mt
source-git-commit: fd75af0bf0c16e20c3b98703af14f329ea6c6371
workflow-type: tm+mt
source-wordcount: '3855'
ht-degree: 8%

---


# Informazioni sulla configurazione del Cloud Service Dynamic Media {#configuring-dynamic-media-scene-mode}

Se utilizzate la configurazione di Adobe Experience Manager per ambienti diversi, ad esempio uno per lo sviluppo, uno per la gestione temporanea e uno per la produzione live, dovete configurare i Cloud Services Dynamic Media per ciascuno di questi ambienti.

## Diagramma di architettura di Dynamic Media {#architecture-diagram-of-dynamic-media-scene-mode}

Nel diagramma di architettura seguente viene descritto il funzionamento di Dynamic Media.

Con la nuova architettura, AEM è responsabile delle risorse di origine primaria e delle sincronizzazioni con Dynamic Media per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa di origine principale viene caricata in AEM, viene replicata in Dynamic Media. A questo punto, Dynamic Media gestisce l’elaborazione delle risorse e la generazione di rappresentazioni, come la codifica video e le varianti dinamiche di un’immagine.
1. Una volta generate le rappresentazioni, AEM accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Media remote (i file binari non vengono inviati nuovamente all&#39;istanza AEM).
1. Quando il contenuto è pronto per essere pubblicato e approvato, attiva il servizio Dynamic Media per inviare contenuti ai server di distribuzione e memorizzare il contenuto nella cache del CDN.

![chlimage_1-550](assets/chlimage_1-550.png)

<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading AEM Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your AEM instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Creazione di una nuova configurazione Dynamic Media nei Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must [log in](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) to Dynamic Media Classic to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. In AEM, toccate il logo AEM per accedere alla console di navigazione globale.
1. Sul lato sinistro della console, toccate l&#39;icona Strumenti, quindi toccate **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. Nella pagina del Browser configurazioni Dynamic Media, seleziona il riquadro a sinistra e tocca **[!UICONTROL global (globale)]** (non toccare o selezionare l’icona della cartella a sinistra di **[!UICONTROL global]**), quindi tocca **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea configurazione Dynamic Media]**, immettete un titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Media, la password, quindi selezionate la vostra area geografica. Questi vengono forniti  Adobe nel messaggio e-mail di provisioning. Se non avete ricevuto questa richiesta, contattate l&#39;assistenza.
1. Fare clic su **[!UICONTROL Connetti ad Dynamic Media]**.
1. Nella finestra di dialogo **[!UICONTROL Cambia password]**, nel campo **[!UICONTROL Nuova password]** immettere una nuova password composta da 8-25 caratteri. La password deve contenere almeno uno dei seguenti elementi:

   * Lettera maiuscola
   * Lettera minuscola
   * Numero
   * Carattere speciale: `# $ & . - _ : { }`

   Il campo **[!UICONTROL Password corrente]** è intenzionalmente precompilato e nascosto dall&#39;interazione.

   Se necessario, potete eseguire il controllo dell&#39;ortografia di una password digitata o digitata nuovamente toccando l&#39;icona occhio password per visualizzare la password. Toccate di nuovo l&#39;icona per nascondere la password.

1. Nel campo **[!UICONTROL Ripeti password]**, digitare nuovamente la nuova password, quindi toccare **[!UICONTROL Fine.]**

   La nuova password viene salvata toccando **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Crea configurazione Dynamic Media]**.

   Se avete toccato **[!UICONTROL Annulla]** nella finestra di dialogo **[!UICONTROL Modifica password]**, dovete comunque immettere una nuova password quando toccate **[!UICONTROL Salva]** per salvare la configurazione di Dynamic Media appena creata.

   Vedere anche [Modifica della password in Dynamic Media](#change-dm-password).

1. Quando la connessione ha esito positivo, potete impostare quanto segue:

   | Proprietà | Descrizione |
   |---|---|
   | Azienda | Nome dell&#39;account Dynamic Media. È possibile che si disponga di più account Dynamic Media per diversi marchi secondari, divisioni o diversi ambienti di produzione e di staging. |
   | Percorso cartella principale della società | Percorso cartella principale della società. |
   | Pubblicazione delle risorse | Potete scegliere tra le seguenti tre opzioni:<br>**[!UICONTROL Immediatamente ]**: Quando le risorse vengono caricate, il sistema le acquisisce e fornisce immediatamente l’URL o l’incorporamento. Non è necessario alcun intervento da parte degli utenti per pubblicare le risorse.<br>**[!UICONTROL Al momento dell&#39;attivazione]**: Prima di fornire un collegamento URL/Incorpora, è necessario pubblicare esplicitamente la risorsa.<br>**[!UICONTROL Pubblicazione ]**selettiva: Le risorse vengono pubblicate automaticamente solo per la visualizzazione in anteprima protetta e possono essere pubblicate in modo esplicito su AEM senza la pubblicazione in DMS7 per la distribuzione nel dominio pubblico. In futuro,  Adobe migliorerà questa opzione per pubblicare le risorse per AEM e pubblicare le risorse in Dynamic Media, escludendovi a vicenda. In altre parole, potete pubblicare le risorse su DMS7 in modo da poter utilizzare funzioni quali SmartCrop o rappresentazioni dinamiche. Oppure potete pubblicare le risorse esclusivamente in AEM per la visualizzazione dell’anteprima; le stesse risorse non vengono pubblicate in DMS7 per la distribuzione nel dominio pubblico. |
   | Server di anteprima protetto | Consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, AEM accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Media remote (nessun file binario viene inviato nuovamente all&#39;istanza AEM).<br>A meno che non disponiate di una disposizione speciale per utilizzare il server della vostra società o un server speciale,  Adobe Systems consiglia di lasciare questa impostazione come specificato. |
   | Sincronizza tutti i contenuti | Selezionato per impostazione predefinita. Deselezionate questa opzione se desiderate includere o escludere selettivamente le risorse dalla sincronizzazione ad Dynamic Media. Deselezionando questa opzione è possibile scegliere tra le due seguenti modalità di sincronizzazione Dynamic Media:<br>**[!UICONTROL modalità di sincronizzazione Dynamic Media]**<br>**[!UICONTROL Attiva per impostazione predefinita ]**: Per impostazione predefinita, la configurazione è applicata a tutte le cartelle, a meno che non venga contrassegnata una cartella specifica per l’esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disattivato per impostazione predefinita]**: La configurazione non viene applicata ad alcuna cartella finché non viene esplicitamente contrassegnata una cartella selezionata per la sincronizzazione con Dynamic Media.<br>Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Media, selezionate una cartella di risorse, quindi toccate  **[!UICONTROL Proprietà]** sulla barra degli strumenti. Nella scheda **[!UICONTROL Dettagli]**, nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione Dynamic Media]**, scegliere tra le tre opzioni seguenti. Al termine, toccare **[!UICONTROL Save]**. *Ricorda: queste tre opzioni non sono disponibili se avete selezionato **Sincronizza tutto il**contenuto in precedenza.* Consultate anche  [Utilizzo della pubblicazione selettiva a livello di cartella in Dynamic Media.](/help/assets/dynamic-media/selective-publishing.md)<br>**[!UICONTROL Ereditato ]**: Nessun valore di sincronizzazione esplicito sulla cartella; al contrario, la cartella eredita il valore di sincronizzazione da una delle cartelle antenate o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per le presentazioni ereditate viene visualizzato tramite una descrizione comandi.<br>**[!UICONTROL Abilita per sottocartelle]**: Include tutti gli elementi di questo sottoalbero per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono la modalità predefinita nella configurazione cloud.<br>**[!UICONTROL Disattivato per le sottocartelle ]**: Escludere tutti gli elementi di questo sottoalbero dalla sincronizzazione ad Dynamic Media. |

   >[!NOTE]
   >
   >In Dynamic Media non è supportato il controllo delle versioni. Inoltre, l’attivazione ritardata si applica solo se l’opzione **[!UICONTROL Pubblica risorse]** della pagina Modifica configurazione Dynamic Media è impostata su **[!UICONTROL All’attivazione]** e soltanto fino alla prima attivazione della risorsa.
   >
   >
   >Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in diretta su S7 Delivery.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Toccate **[!UICONTROL Salva]**. Viene salvata la nuova password e la nuova configurazione Dynamic Media. Se invece avete toccato **[!UICONTROL Annulla]**, non si verifica alcun aggiornamento della password.
1. Nella finestra di dialogo **[!UICONTROL Configurazione di Dynamic Media]**, toccare **[!UICONTROL OK]** per iniziare la configurazione.

   >[!IMPORTANT]
   >
   >Al termine della nuova configurazione di Dynamic Media, riceverete una notifica di stato all&#39;interno AEM Inbox.
   >
   >Questa notifica Inbox informa se la configurazione ha avuto esito positivo o meno.
   > Per ulteriori informazioni, vedere [Risoluzione dei problemi relativi a una nuova configurazione Dynamic Media](#troubleshoot-dm-config) e [Posta in arrivo](/help/sites-cloud/authoring/getting-started/inbox.md).

1. Per visualizzare in modo sicuro l&#39;anteprima del contenuto Dynamic Media prima che venga pubblicato, è necessario &quot; inserire nell&#39;elenco Consentiti&quot; l&#39;istanza di creazione AEM per connettersi ad Dynamic Media. Per configurare questa impostazione, effettuate le seguenti operazioni:

   * Accedete al vostro account Dynamic Media Classic: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html). Le credenziali e l&#39;accesso sono stati forniti  Adobe al momento del provisioning. Se non disponete di tali informazioni, contattate il supporto tecnico.
   * Nella barra di navigazione in alto a destra della pagina, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server immagini]**.

   * Nella pagina Pubblica su Image Server, nell’elenco a discesa Contesto pubblicazione, selezionate **[!UICONTROL Test Image Server]**.
   * Per Filtro indirizzi client, toccate **[!UICONTROL Aggiungi]**.
   * Selezionate la casella di controllo per attivare l&#39;indirizzo, quindi immettete l&#39;indirizzo IP dell&#39;istanza di AEM Author (non l&#39;IP del dispatcher).
   * Fai clic su **[!UICONTROL Salva]**.

Ora hai finito con la configurazione di base; è possibile utilizzare Dynamic Media.

Se desiderate personalizzare ulteriormente la configurazione, potete eventualmente completare una qualsiasi delle attività in [Configurazione delle impostazioni avanzate in Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Risoluzione dei problemi relativi a una nuova configurazione Dynamic Media {#troubleshoot-dm-config}

Al termine dell&#39;installazione di una nuova configurazione Dynamic Media, riceverai una notifica di stato in AEM Posta in arrivo. Questa notifica informa se la configurazione ha avuto esito positivo o meno, come mostrato nelle immagini riportate di seguito dalla Casella in entrata.

![aeminboxsuccess](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![aeminbossottaggio](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Vedere anche [Posta in arrivo](/help/sites-cloud/authoring/getting-started/inbox.md).

**Risoluzione di problemi relativi a una nuova configurazione Dynamic Media**

1. Vicino all&#39;angolo superiore destro della pagina AEM, toccare l&#39;icona della campana, quindi toccare **[!UICONTROL Visualizza tutto]**.
1. Nella pagina Posta in arrivo, toccate la notifica di riuscita per visualizzare una panoramica dello stato e dei registri della configurazione.

   Se la configurazione non è riuscita, toccate la notifica di errore simile alla schermata seguente.

   ![dmsetupFailed](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Nella pagina **[!UICONTROL DMSETUP]**, controlla i dettagli di configurazione che descrivono l&#39;errore. In particolare, prendere nota di eventuali messaggi di errore o codici di errore. Dovrai contattare &#39;Assistenza Adobe con queste informazioni.

   ![dmsetuppage](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Modifica della password in Dynamic Media {#change-dm-password}

La scadenza della password in Dynamic Media è impostata su 100 anni dalla data corrente del sistema.

La password deve contenere almeno uno dei seguenti elementi:

* Lettera maiuscola
* Lettera minuscola
* Numero
* Carattere speciale: `# $ & . - _ : { }`

Se necessario, potete eseguire il controllo dell&#39;ortografia di una password digitata o digitata nuovamente toccando l&#39;icona occhio password per visualizzare la password. Toccate di nuovo l&#39;icona per nascondere la password.

La password modificata viene salvata quando toccate **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Modifica configurazione Dynamic Media]**.

1. In AEM, toccate il logo AEM per accedere alla console di navigazione globale.
1. Sul lato sinistro della console, toccare l&#39;icona Strumenti, quindi toccare **[!UICONTROL Cloud Services > Configurazione Dynamic Media.]**
1. Nella pagina del browser Configurazione Dynamic Media, nel riquadro a sinistra, toccare **[!UICONTROL globale]** (non toccare o selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL globale]**), quindi toccare **[!UICONTROL Modifica.]**
1. Nella pagina **[!UICONTROL Edit Dynamic Media Configuration]**, direttamente sotto il campo **[!UICONTROL Password]**, toccare **[!UICONTROL Change Password.]**
1. Nella finestra di dialogo **[!UICONTROL Cambia password]**, effettuare le seguenti operazioni:

   * Nel campo **[!UICONTROL Nuova password]**, immettere una nuova password.

      Il campo **[!UICONTROL Password corrente]** è intenzionalmente precompilato e nascosto dall&#39;interazione.

   * Nel campo **[!UICONTROL Ripeti password]**, digitare nuovamente la nuova password, quindi toccare **[!UICONTROL Fine.]**

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, toccare **[!UICONTROL Salva]**, quindi toccare **[!UICONTROL OK.]**

## (Facoltativo) Configurazione delle impostazioni avanzate in Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Per personalizzare ulteriormente la configurazione e l&#39;impostazione di Dynamic Media o ottimizzarne le prestazioni, è possibile completare una o più delle seguenti *attività facoltative*:

* [Configurazione e configurazione delle impostazioni Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Facoltativo) Configurazione e configurazione delle impostazioni Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilizzate l&#39;interfaccia utente Dynamic Media Classic (Scene7) per apportare modifiche alle impostazioni Dynamic Media.

Per alcune delle attività di cui sopra è necessario accedere ad Dynamic Media Classic (Scene7) qui: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

Le attività di configurazione e configurazione includono:

* [Configurazione pubblicazione per Image Server](#publishing-setup-for-image-server)
* [Configurazione delle impostazioni generali dell’applicazione](#configuring-application-general-settings)
* [Configurazione della gestione del colore](#configuring-color-management)
* [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiunta di tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configurazione pubblicazione per Image Server {#publishing-setup-for-image-server}

Le impostazioni Impostazione pubblicazione specificano il modo in cui le risorse vengono distribuite per impostazione predefinita da Dynamic Media. Se non viene specificata alcuna impostazione, Dynamic Media distribuisce una risorsa in base alle impostazioni predefinite definite in Impostazione pubblicazione. Ad esempio, una richiesta di invio di un&#39;immagine che non include un attributo di risoluzione produce un&#39;immagine con l&#39;impostazione Risoluzione oggetto predefinita.

Per configurare Impostazione pubblicazione: in Dynamic Media Classic, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server immagini]**.

La schermata Server immagini stabilisce le impostazioni predefinite per la distribuzione delle immagini. Consultate la schermata dell’interfaccia utente per una descrizione di ciascuna impostazione.

**[!UICONTROL Attributi]**  richiesta - Queste impostazioni impongono limiti alle immagini che possono essere distribuite dal server.
**[!UICONTROL Attributi]**  richiesta predefiniti: queste impostazioni interessano l&#39;aspetto predefinito delle immagini.
**[!UICONTROL Attributi]**  comuni delle miniature: queste impostazioni interessano l’aspetto predefinito delle miniature.
**[!UICONTROL Valori predefiniti per i campi]** catalogo: queste impostazioni interessano la risoluzione e il tipo predefinito di miniatura delle immagini.
**[!UICONTROL Attributi]**  di gestione del colore: queste impostazioni determinano quali profili colore ICC vengono utilizzati.
**[!UICONTROL Attributi]**  di compatibilità: questa impostazione consente ai paragrafi iniziali e finali nei livelli di testo di essere trattati come nella versione 3.6 per garantire la compatibilità con le versioni precedenti.
**[!UICONTROL Supporto]**  per la localizzazione: queste impostazioni consentono di gestire più attributi della lingua. Consente inoltre di specificare una stringa di mappa lingua in modo da definire le lingue da supportare per le varie descrizioni comandi nei visualizzatori. Per ulteriori informazioni sull&#39;impostazione di **[!UICONTROL Supporto per la localizzazione]**, vedere [Considerazioni per l&#39;impostazione della localizzazione delle risorse](https://experienceleague.corp.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Configurazione delle impostazioni generali dell&#39;applicazione {#configuring-application-general-settings}

Per aprire la pagina Impostazioni generali applicazione, nella barra di navigazione globale di Dynamic Media Classic fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali.]**

**[!UICONTROL Server]**  - Al provisioning dell&#39;account, Dynamic Media fornisce automaticamente i server assegnati alla società. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche per il vostro account. Non modificate i nomi dei server, a meno che non sia espressamente richiesto dal supporto AEM.
**[!UICONTROL Sovrascrivi immagini]**  - Dynamic Media non consente a due file di avere lo stesso nome. L’ID URL di ogni elemento (il nome del file senza l’estensione) deve essere univoco. Queste opzioni specificano la modalità di caricamento delle risorse sostitutive: se sostituiscono l’originale o diventano duplicati. Le risorse duplicate vengono rinominate con il suffisso &quot;-1&quot; (ad esempio, sedia.tif viene rinominato sedia-1.tif). Queste opzioni interessano le risorse caricate in una cartella diversa dall’originale o le risorse con un’estensione file diversa dall’originale (ad esempio, JPG, TIF o PNG).
**[!UICONTROL Sovrascrivi in cartella corrente, nome/estensione]**  stessa immagine base: questa opzione rappresenta la regola di sostituzione più restrittiva. Richiede che l’immagine sostitutiva venga caricata nella stessa cartella dell’originale e che abbia la stessa estensione del nome file dell’originale. Se questi requisiti non sono soddisfatti, viene creato un duplicato. Per mantenere la coerenza con le AEM, scegliete sempre **[!UICONTROL Sovrascrivi nella cartella corrente, nome/estensione base uguale]**.
**[!UICONTROL Sovrascrivi in qualsiasi cartella, nome/estensione]**  della risorsa base - Richiede che l’immagine sostitutiva abbia la stessa estensione del nome file dell’immagine originale (ad esempio, sedia.jpg deve sostituire sedia.jpg, non sedia.tif). Tuttavia, potete caricare l’immagine sostitutiva in una cartella diversa da quella dell’originale. L’immagine aggiornata si trova nella nuova cartella; il file non può più essere trovato nella posizione originale.
**[!UICONTROL Sovrascrivi in qualsiasi cartella, nome della stessa risorsa di base, indipendentemente dall’estensione]** . Questa opzione è la regola di sostituzione più inclusiva. Potete caricare un’immagine sostitutiva in una cartella diversa da quella dell’originale, caricare un file con un’estensione diversa e sostituire il file originale. Se il file originale si trova in un’altra cartella, l’immagine sostitutiva si trova nella nuova cartella in cui è stata caricata.
**[!UICONTROL Profili]**  colore predefiniti - Per ulteriori informazioni, consultate  [Configurazione della ](#configuring-color-management) gestione del colore. Per impostazione predefinita, il sistema mostra 15 rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** e 15 predefiniti visualizzatore quando fai clic su **[!UICONTROL Visualizzatori]** nella vista Dettaglio della risorsa. Puoi aumentare questo limite. Consulta la sezione [Aumento o riduzione del numero di predefiniti immagine da visualizzare](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumento o riduzione del numero di predefiniti visualizzatore da mostrare](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Configurazione della gestione del colore {#configuring-color-management}

La gestione dinamica del colore dei contenuti multimediali consente di colorare le risorse corrette. Con la correzione del colore, le risorse inserite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede una rappresentazione dinamica, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio. Consultate [Configurazione dei predefiniti per immagini](/help/assets/dynamic-media/managing-image-presets.md).

Per configurare le proprietà colore predefinite per attivare la correzione colore durante la richiesta delle immagini:

1. [Effettuate l&#39;accesso ad Dynamic Media ](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) Classic utilizzando le credenziali fornite durante il provisioning. Passare a **[!UICONTROL Configurazione > Impostazione applicazione]**.
1. Espandi l’area **[!UICONTROL Publish Setup (Impostazione pubblicazione)]** e seleziona **[!UICONTROL Image Server]**. Per le istanze di pubblicazione, imposta **[!UICONTROL Contesto di pubblicazione]** su **[!UICONTROL Image Server]**.
1. Scorrete fino alla proprietà da modificare, ad esempio una proprietà nell&#39;area **[!UICONTROL Attributi di gestione del colore]**.
Potete impostare le seguenti proprietà di correzione del colore:

   | Proprietà | Descrizione |
   |---|---|
   | Spazio colore predefinito CMYK | Nome del profilo colore CMYK predefinito. |
   | Scala di grigio Spazio colore predefinito | Nome del profilo colore grigio predefinito. |
   | Spazio colore predefinito RGB | Nome del profilo colore RGB predefinito. |
   | Intento di rendering conversione colore | Specifica l’intento di rendering. I valori accettabili sono: **[!UICONTROL percettivo]**, **[!UICONTROL colometrico relativo]**, **[!UICONTROL saturazione]**, **[!UICONTROL colometrico assoluto.]**  Adobe consiglia  **** i parenti come impostazione predefinita. |

1. Toccate **[!UICONTROL Salva]**.

Ad esempio, puoi impostare **[!UICONTROL Spazio colore predefinito RGB]** su *sRGB* e **[!UICONTROL Spazio colore predefinito CMYK]** su *WebCoated*.

In questo modo si effettua quanto segue:

* Attiva la correzione del colore per le immagini RGB e CMYK.
* Si presume che le immagini RGB che non hanno un profilo colore siano nello spazio colore *sRGB*.
* Si presume che le immagini CMYK che non hanno un profilo colore siano nello spazio colore *WebCoated*.
* Le rappresentazioni dinamiche che restituiscono l&#39;output RGB lo restituiranno nello spazio colore *sRGB*.
* Rappresentazioni dinamiche che restituiscono l&#39;output CMYK, lo restituiranno nello spazio colore *WebCoated*.

#### Modifica dei tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Potete definire quali tipi di risorse vengono elaborati da Dynamic Media e personalizzare i parametri di elaborazione avanzata delle risorse. Ad esempio, potete specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Convertite un Adobe PDF  in una risorsa eCatalog.
* Convertite un documento Adobe Photoshop  (.PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizzare un file Adobe Illustrator  (.AI) o un file  Encapsulated Postscript di Adobe Photoshop (.EPS).
* [I ](/help/assets/dynamic-media/video-profiles.md) profili video e i  [profili ](/help/assets/dynamic-media/image-profiles.md) immagine possono essere utilizzati rispettivamente per definire l’elaborazione di video e immagini.

Consulta [Caricamento delle risorse](/help/assets/add-assets.md).

**Per modificare i tipi MIME per i formati supportati**

1. In AEM, fare clic sul logo AEM per accedere alla console di navigazione globale, quindi fare clic su **[!UICONTROL Generale > CRXDE Lite]**.
1. Nella barra a sinistra, andate a:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![mimetypes](assets/mimetypes.png)

1. Sotto la cartella mimeTypes, selezionate un tipo mime.
1. Sul lato destro della pagina CRXDE Lite, nella parte inferiore:

   * Fare doppio clic sul campo **[!UICONTROL enabled]**. Per impostazione predefinita, tutti i tipi di mime delle risorse sono attivati (impostati su **[!UICONTROL true]**), il che significa che le risorse verranno sincronizzate in Dynamic Media per l&#39;elaborazione. Se desiderate escludere l&#39;elaborazione di questo tipo di mime della risorsa, modificate questa impostazione in **[!UICONTROL false]**.

   * Fare doppio clic su **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Consultate [Tipi mime supportati](/help/assets/file-format-support.md) per un elenco dei valori di parametro di elaborazione consentiti che potete utilizzare per un determinato tipo mime.

1. Effettua una delle operazioni seguenti:
   * Ripetete i passaggi da 3 a 4 per modificare altri tipi di mime.
   * Nella barra dei menu della pagina dei CRXDE Lite, fare clic su **[!UICONTROL Salva tutto.]**

1. Nell&#39;angolo superiore sinistro della pagina, toccare **[!UICONTROL CRXDE Lite]** per tornare alla AEM.

#### Aggiunta di tipi MIME per i formati non supportati {#adding-mime-types-for-unsupported-formats}

All’interno di AEM Assets puoi aggiungere tipi MIME personalizzati per i formati non supportati. Per assicurarti che AEM non elimini eventuali nuovi nodi che aggiungi in CRXDE Lite, devi accertarti di spostare il tipo MIME prima di `image_` e che il suo valore abilitato sia impostato su **[!UICONTROL false]**.

**Aggiunta di tipi MIME per i formati non supportati**

1. Da AEM, toccare **[!UICONTROL Strumenti > Operazioni > Console Web.]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser nella pagina **[!UICONTROL Configurazione della console Web Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, tocca **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Nella pagina **Adobe CQ Scene7 Asset MIME type Service** fare clic sull&#39;icona con il segno più &lt;+>. La posizione nella tabella in cui si fa clic sul segno più per aggiungere il nuovo tipo mime è insignificante.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digitare `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   L&#39;esempio `DWG=image/vnd.dwg` è solo a scopo illustrativo. Il tipo MIME aggiunto qui può essere qualsiasi altro formato non supportato.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Nell&#39;angolo inferiore destro della pagina, toccare **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser con la pagina di configurazione della console Web di Adobe Experience Manager aperta.

1. Tornate alla scheda del browser con la console AEM aperta.
1. Da AEM, toccare **[!UICONTROL Strumenti > Generale > CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, andate a:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascinate il tipo mime `image_vnd.dwg` e rilasciatelo direttamente sopra `image_` nella struttura ad albero, come mostrato nella schermata seguente.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo mime `image_vnd.dwg` ancora selezionato, nella scheda **[!UICONTROL Proprietà]** della riga **[!UICONTROL abilitata]**, seleziona l’intestazione della colonna **[!UICONTROL Valore]** e fai doppio clic sul valore per aprire l’elenco a discesa **[!UICONTROL Valore]**.
1. Digitare `false` nel campo (oppure selezionare **[!UICONTROL false]** dall&#39;elenco a discesa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Nell&#39;angolo superiore sinistro della pagina dei CRXDE Lite, fare clic su **[!UICONTROL Salva tutto]**.



### (Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per mantenere Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> in esecuzione senza problemi,  Adobe consiglia i seguenti suggerimenti per l&#39;ottimizzazione delle prestazioni di sincronizzazione/scalabilità:

* Aggiornamento dei parametri di processo predefiniti per l’elaborazione di diversi formati di file.
* Aggiornamento dei thread di lavoro predefiniti per il flusso di lavoro Granite (risorse video) in coda.
* Aggiornamento dei thread di lavoro transitori Granite (immagini e risorse non video) predefiniti per il flusso di lavoro in coda.
* Aggiornamento delle connessioni di caricamento massime nel server Dynamic Media Classic.

#### Aggiornamento dei parametri di processo predefiniti per l’elaborazione di diversi formati di file

Potete ottimizzare i parametri di processo per velocizzare l’elaborazione quando caricate i file. Ad esempio, se caricate file PSD ma non desiderate elaborarli come modelli, potete impostare l’estrazione dei livelli su false (disattivato). In tal caso, il parametro del processo sintonizzato apparirebbe come `process=None&createTemplate=false`.

 Adobe consiglia di utilizzare i seguenti parametri di processo &quot;sintonizzati&quot; per i file PDF, Postscript e PSD:

| Tipo di file | Parametri di processo consigliati |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- To update any of these parameters, follow the steps in [Enabling MIME type-based Assets/Dynamic Media Classic upload job parameter support](#enabling-mime-type-based-assets-scene-upload-job-parameter-support). -->

#### Aggiornamento della coda del flusso di lavoro transitorio Granite {#updating-the-granite-transient-workflow-queue}

La coda del flusso di lavoro di transito Granite viene utilizzata per il flusso di lavoro **[!UICONTROL DAM Update Asset]**. In Dynamic Media, viene utilizzata per l’assimilazione e l’elaborazione delle immagini.

**Per aggiornare la coda del flusso di lavoro transitorio Granite**

1. Andate su [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) e cercate **Coda: Granite Transient Workflow Queue**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Processi paralleli massimi]**, impostate il numero sul valore desiderato.

   È possibile aumentare il numero massimo di **[!UICONTROL processi paralleli]** per supportare in modo adeguato il caricamento di file in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ad esempio una migrazione iniziale o un caricamento in blocco una tantum, potete usare un valore elevato. Tenete presente, tuttavia, che l&#39;utilizzo di un valore elevato (ad esempio, due volte il numero di core) può avere effetti negativi su altre attività simultanee. È quindi necessario verificare e regolare il valore in base al caso di utilizzo specifico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Toccate **[!UICONTROL Salva]**.

#### Aggiornamento della coda del flusso di lavoro Granite {#updating-the-granite-workflow-queue}

La coda Flusso di lavoro Granite viene utilizzata per i flussi di lavoro non transitori. In Dynamic Media, veniva utilizzato per elaborare i video con il flusso di lavoro **[!UICONTROL Dynamic Media Encode Video]**.

Per aggiornare la coda del flusso di lavoro Granite:

1. Andate su `https://<server>/system/console/configMgr` e cercate **Coda: Granite Workflow Queue**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Processi paralleli massimi]**, impostate il numero sul valore desiderato.

   Per impostazione predefinita, il numero massimo di processi paralleli dipende dal numero di core CPU disponibili. Ad esempio, su un server di 4 core assegna 2 thread di lavoro. (Un valore compreso tra 0,0 e 1,0 è basato sul rapporto, altrimenti qualsiasi numero maggiore di 1 assegnerà il numero di thread di lavoro.)

   Per la maggior parte dei casi di utilizzo, l&#39;impostazione predefinita 0.5 è sufficiente.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Toccate **[!UICONTROL Salva]**.

#### Aggiornamento della connessione di caricamento Scene7 {#updating-the-scene-upload-connection}

L&#39;impostazione di Scene7 Upload Connection sincronizza AEM risorse sui server Dynamic Media Classic.

Per aggiornare la connessione di caricamento Scene7:

1. Accedi a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. Nel campo **[!UICONTROL Numero di connessioni]** e/o nel campo **[!UICONTROL Timeout processo attivo]**, modificare il numero come desiderato.

   L&#39;impostazione **[!UICONTROL Numero di connessioni]** controlla il numero massimo di connessioni HTTP consentite per il caricamento di AEM su Dynamic Media; in genere, il valore predefinito di 10 connessioni è sufficiente.

   L&#39;impostazione **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per la pubblicazione delle risorse Dynamic Media caricate nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

   Per la maggior parte dei casi di utilizzo, è sufficiente impostare 2100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Toccate **[!UICONTROL Salva.]**

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your AEM author environment to the AEM publish node. This workflow is necessary because the AEM publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to AEM publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the AEM publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the AEM publish node.

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

1. In AEM, tap the AEM logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
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

