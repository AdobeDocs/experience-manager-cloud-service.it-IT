---
title: Gestire le risorse video
description: Caricare, visualizzare in anteprima, annotare e pubblicare risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '4938'
ht-degree: 6%

---

# Gestire le risorse video {#manage-video-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Il formato video è una parte fondamentale delle risorse digitali di un&#39;organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzionalità mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, è possibile utilizzando i Profili di elaborazione e utilizzando [!DNL Dynamic Media] integrazione. Senza [!DNL Dynamic Media] licenza, [!DNL Experience Manager] fornisce supporto di base per i video, ad esempio la transcodifica tramite FFmpeg, l’estrazione delle miniature di anteprima per i formati di file supportati e l’anteprima nell’interfaccia utente per i formati supportati per la riproduzione direttamente nel browser.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera le anteprime per le risorse video con l’estensione MP4. È possibile visualizzare in anteprima le rappresentazioni nel [!DNL Assets] interfaccia utente.

1. Nella cartella o nelle sottocartelle delle risorse digitali, individua il percorso in cui desideri aggiungere le risorse digitali.
1. Per caricare la risorsa, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti e scegli **[!UICONTROL File]**. In alternativa, trascinare un file sull’interfaccia utente. Vedi [caricare le risorse](manage-digital-assets.md#uploading-assets) per i dettagli.
1. Per visualizzare un video in anteprima nella vista a schede, fai clic sul pulsante **[!UICONTROL Play]** ![opzione di riproduzione](assets/do-not-localize/play.png) sulla risorsa video. È possibile mettere in pausa o riprodurre video solo nella vista a schede. La [!UICONTROL Play] e [!UICONTROL Pausa] le opzioni non sono disponibili nella vista a elenco.
1. Per visualizzare l’anteprima del video nella pagina dei dettagli della risorsa, seleziona **[!UICONTROL Modifica]** sulla carta. Il video viene riprodotto nel lettore video nativo del browser. È possibile riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, puoi includere le risorse video in una pagina web come URL o incorporarle direttamente. Per maggiori dettagli, vedi [pubblicare [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Pubblicare video in YouTube {#publishing-videos-to-youtube}

Puoi pubblicare risorse video gestite in Experience Manager Assets direttamente su un canale YouTube creato in precedenza.

Per pubblicare le risorse video in YouTube, taggate le risorse video in Experience Manager Assets con i tag . Puoi associare questi tag a un canale YouTube. Se il tag di una risorsa video corrisponde al tag di un canale YouTube, il video viene pubblicato in YouTube. La pubblicazione in YouTube avviene insieme a una normale pubblicazione del video, purché venga utilizzato un tag associato.

YouTube esegue la propria codifica. Pertanto, il file video originale caricato in Experience Manager viene pubblicato in YouTube invece di qualsiasi rendering video creato dalla codifica di Dynamic Media. Sebbene non sia necessario elaborare i video con Dynamic Media, è previsto che lo facciano nel caso in cui sia necessario un predefinito visualizzatore per la riproduzione.

Quando bypassi il profilo di elaborazione video e lo pubblichi direttamente in YouTube, significa semplicemente che la risorsa video in Experience Manager Asset non riceve una miniatura visibile. Significa anche che i video non codificati non funzionano con nessuno dei tipi di risorse Dynamic Media.

La pubblicazione delle risorse video sui server YouTube comporta il completamento delle seguenti attività per garantire una verifica server-to-server sicura con YouTube:

1. [Configurare le impostazioni Google Cloud](#configuring-google-cloud-settings)
1. [Creare un canale YouTube](#creating-a-youtube-channel)
1. [Aggiungi tag per la pubblicazione](#adding-tags-for-publishing)
1. [Configurare YouTube nell’Experience Manager](#setting-up-youtube-in-aem)
1. [(Facoltativo) Automatizza l&#39;impostazione delle proprietà predefinite di YouTube per i video caricati](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Pubblicare video sul canale YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Facoltativo) Verifica il video pubblicato su YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Collegare gli URL di YouTube all’applicazione Web](#linking-youtube-urls-to-your-web-application)

È inoltre possibile [annullare la pubblicazione dei video per rimuoverli da YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Configurare le impostazioni Google Cloud {#configuring-google-cloud-settings}

Per pubblicare su YouTube, è necessario un account Google. Se disponi di un account GMAIL, disponi già di un account Google; se non disponi di un account Google, puoi facilmente crearne uno. È necessario l’account perché sono necessarie le credenziali per pubblicare le risorse video in YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

L’account utilizzato con Google Cloud e l’account Google utilizzato per YouTube non deve essere lo stesso.

Google cambia periodicamente la propria interfaccia utente. Di conseguenza, i passaggi per pubblicare i video in YouTube possono variare leggermente rispetto a quanto descritto di seguito. Questa avvertenza si applica anche ad YouTube quando tenti di verificare se i video sono caricati su di esso.

>[!NOTE]
>
>I seguenti passaggi erano accurati al momento della scrittura. Tuttavia, Google aggiorna periodicamente le proprie pagine web cloud senza preavviso. Di conseguenza, alcune opzioni di configurazione possono essere denominate in modo leggermente diverso nell’interfaccia utente di Google rispetto al nome utilizzato nei passaggi.

**Per configurare le impostazioni Google Cloud:**

1. Crea un account Google.
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   Se disponi già di un account Google, puoi passare al passaggio successivo.

1. Vai a [https://cloud.google.com/](https://cloud.google.com/).
1. Sulla **[!UICONTROL Google Cloud]** nell’angolo in alto a destra, seleziona **[!UICONTROL Console]**.

   Se necessario, **[!UICONTROL Accedere]** utilizzo delle credenziali del tuo account Google per visualizzare **[!UICONTROL Console]** opzione .

1. Sulla **[!UICONTROL Dashboard]** a destra di **[!UICONTROL Piattaforma Google Cloud]**, seleziona **[!UICONTROL Progetto]** elenco a discesa per aprire **[!UICONTROL Selezionare un progetto]** finestra di dialogo.
1. In **[!UICONTROL Selezionare un progetto]** finestra di dialogo, seleziona **[!UICONTROL Nuovo progetto]**.
1. In **[!UICONTROL Nuovo progetto]** nella finestra di dialogo **[!UICONTROL Nome del progetto]** digitare il nome del nuovo progetto.

   L&#39;ID progetto si basa sul nome del progetto. Scegliere con attenzione il nome del progetto; non può essere modificato dopo la creazione. Inoltre, devi immettere nuovamente lo stesso ID progetto quando configuri YouTube in Experience Manager successivo. Quindi, annotalo.

1. Seleziona **[!UICONTROL Crea]**.

1. Effettua una delle seguenti operazioni:

   * Nella dashboard del progetto, nella sezione **[!UICONTROL Introduzione]** scheda, seleziona **[!UICONTROL Esplorare e abilitare le API]**.
   * Nella dashboard del progetto, nella sezione **[!UICONTROL API]** scheda, seleziona **[!UICONTROL Panoramica su API]**.

1. Vicino al centro superiore del **[!UICONTROL API e servizi]** pagina, seleziona **[!UICONTROL ABILITARE API E SERVIZI]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. Sulla **[!UICONTROL Libreria API]** pagina, a sinistra, sotto **[!UICONTROL Categoria]**, seleziona **[!UICONTROL YouTube]**. Sul lato destro della pagina, seleziona **[!UICONTROL YouTube]**.
1. Sulla **[!UICONTROL YouTube]** pagina, seleziona **[!UICONTROL API dati YouTube v3]**.
1. Sulla **[!UICONTROL API dati YouTube v3]** pagina, seleziona **[!UICONTROL GESTIONE]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. Per utilizzare l’API, sono necessarie le credenziali. Se necessario, sul lato sinistro del **[!UICONTROL API e servizi]** pagina, seleziona **[!UICONTROL Credenziali]**.
1. Sulla **[!UICONTROL Credenziali]** nella parte superiore della pagina, seleziona **[!UICONTROL CREDENZIALI]**, quindi seleziona **[!UICONTROL ID client OAuth]**.
1. Sulla **[!UICONTROL Crea ID client OAuth]** nella pagina **[!UICONTROL Tipo di applicazione]** elenco a discesa, seleziona **[!UICONTROL Applicazione Web]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Effettua una delle operazioni seguenti:

   * In **[!UICONTROL Nome]** immetti un nome univoco per il client OAuth 2.0.
   * Usa il nome predefinito già fornito da Google nel **[!UICONTROL Nome]** campo .

1. Sotto la **[!UICONTROL Origini JavaScript autorizzate]** intestazione, selezionare **[!UICONTROL AGGIUNGI URI]**.

   ![6_5_googleaccount-apis-namepermissions](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. In **[!UICONTROL URI]** campo di testo, immettere il seguente percorso, sostituendo il proprio dominio e il proprio numero di porta nel percorso, quindi premere **[!UICONTROL Invio]** per aggiungere il percorso all’elenco:

   `https://<servername.domain>:<port_number>`

   Ad esempio `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >L’esempio di percorso URI riportato sopra è ipotetico e solo a scopo di spiegazione.

1. Sotto la **[!UICONTROL URI di reindirizzamento autorizzati]** selezionare ADD URI.
1. In **[!UICONTROL URI]** campo di testo, immettere il seguente percorso, sostituendo il proprio dominio e il proprio numero di porta nel percorso, quindi premere **[!UICONTROL Invio]** per aggiungere il percorso all’elenco:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Ad esempio `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >L’esempio di percorso URI riportato sopra è ipotetico e solo a scopo di spiegazione.

1. Vicino al fondo del **[!UICONTROL Crea ID client OAuth]** pagina, seleziona **[!UICONTROL Crea]**.
1. Sulla **[!UICONTROL Client OAuth creato]** effettuare le seguenti operazioni:

   * (Facoltativo) Copia i valori nella **[!UICONTROL ID cliente]** e **[!UICONTROL Segreto client]** e salvare.
   * Seleziona **[!UICONTROL SCARICA JSON]**, quindi salva il file JSON.

   È necessario scaricare questo file JSON quando si configura YouTube in Adobe Experience Manager in un secondo momento.

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. Sulla **[!UICONTROL Client OAuth creato]** finestra di dialogo, seleziona **[!UICONTROL OK]**.
1. Esci dal tuo account Google. Ora crea un canale YouTube.

### Creare un canale YouTube {#creating-a-youtube-channel}

Per pubblicare video in YouTube è necessario disporre di uno o più canali. Se hai già creato un canale YouTube, puoi saltare questa attività e passare a [Aggiungi tag per la pubblicazione](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Assicurati di aver già configurato uno o più canali in YouTube *prima* aggiungi canali in Impostazioni YouTube in Experience Manager (vedi [Configurare YouTube nell’Experience Manager](#setting-up-youtube-in-aem) qui sotto). Se non riesci a eseguire la configurazione del canale, non riceverai alcun avviso di canali esistenti. Tuttavia, la verifica Google si verifica ancora quando aggiungi un canale, ma non è possibile scegliere quale canale viene inviato il video.

**Per creare un canale YouTube:**

1. Vai a [https://www.youtube.com](https://www.youtube.com/) e accedi utilizzando le credenziali del tuo account Google.
1. Nell’angolo in alto a destra della pagina YouTube, seleziona l’immagine del profilo (può anche essere visualizzata come lettera all’interno di un cerchio colorato), quindi seleziona **[!UICONTROL Impostazioni di YouTube]** (icona a forma di ingranaggio circolare).
1. Nella pagina Panoramica , seleziona l’intestazione Altre funzioni . **[!UICONTROL Visualizza tutti i miei canali o crea un canale]**.
1. Nella pagina Canali, seleziona **[!UICONTROL Crea un nuovo canale]**.
1. Nella pagina Account marchio , immetti il nome di un’azienda o un altro nome di canale scelto per la pubblicazione delle risorse video nel campo Nome account marchio , quindi seleziona **[!UICONTROL Crea]**.

   Ricordare il nome che si immette qui; è necessario immetterlo nuovamente quando è necessario configurare YouTube in Experience Manager.

1. (Facoltativo) Se necessario, aggiungi altri canali.

   Ora è possibile aggiungere tag per la pubblicazione.

### Aggiungi tag per la pubblicazione {#adding-tags-for-publishing}

Per pubblicare nei video in YouTube, Experience Manager associa i tag a uno o più canali YouTube. Per aggiungere tag per la pubblicazione, consulta [Amministrare i tag](/help/sites-cloud/authoring/features/tags.md).

Oppure, se si desidera utilizzare i tag predefiniti in Experience Manager, è possibile saltare questa attività e passare a [Configurare YouTube nell’Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>Una volta configurato il Cloud Service, non è necessaria un’altra configurazione per abilitare l’agente di replica di YouTube Publish a questo punto. Il motivo è che è stato attivato al momento del salvataggio della configurazione del Cloud Service.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Configurare YouTube nell’Experience Manager {#setting-up-youtube-in-aem}

A partire da Experience Manager 6.4, è stato introdotto un nuovo metodo di interfaccia utente touch per configurare la pubblicazione YouTube in Experience Manager. In base all’istanza installata dell’Experience Manager in uso, effettua una delle seguenti operazioni:

* Per configurare YouTube in Experience Manager prima della versione 6.4, vedi [Configurare YouTube in Experience Manager prima della versione 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Per configurare YouTube in Experience Manager 6.4 o versione successiva, vedi [Configurare YouTube in Experience Manager 6.4 e versioni successive](#setting-up-youtube-in-aem-and-later).

#### Configurare YouTube in Experience Manager 6.4 e versioni successive {#setting-up-youtube-in-aem-and-later}

1. Assicurati di accedere alla tua istanza di Dynamic Media come amministratore.
1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra individua **[!UICONTROL Strumenti]**(icona a forma di martello) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione pubblicazione YouTube]**.
1. Seleziona **[!UICONTROL globale]** (non selezionarlo).

1. Nell’angolo in alto a destra della pagina globale, seleziona **[!UICONTROL Crea]**.
1. Nella pagina Crea configurazione YouTube, seleziona Impostazioni piattaforma Google Cloud, quindi immetti l’ID progetto Google nel campo **[!UICONTROL Nome applicazione]**.

   Hai specificato l’ID del progetto quando hai inizialmente configurato le impostazioni di Google Cloud in precedenza.
Lascia aperta la pagina Crea configurazione YouTube; ci ritornate tra un momento.

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Utilizzando un editor di testo normale, apri il file JSON scaricato e salvato in precedenza nell’attività [Configurare le impostazioni Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. Seleziona e copia l’intero testo JSON.
1. Torna alla finestra di dialogo Impostazioni account YouTube. Nel campo **[!UICONTROL Configurazione JSON]**, incolla il testo JSON.
1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva]**.

   Ora configura i canali YouTube nell’Experience Manager.

1. Seleziona **[!UICONTROL Aggiungi canale]**.
1. Nel campo Nome canale , immetti il nome del canale creato nell’attività **[!UICONTROL Aggiunta di uno o più canali ad YouTube]** prima.

   Facoltativamente, puoi aggiungere una descrizione.

1. Seleziona **[!UICONTROL Aggiungi]**.
1. Viene visualizzata la verifica YouTube/Google. Se non hai già effettuato l’accesso all’account Google Cloud, salta questo passaggio.

   * Immetti il nome utente e la password Google associati all’ID progetto Google e al testo JSON sopra riportato.
   * A seconda del numero di canali di cui dispone l’account, vengono visualizzati due o più elementi. Seleziona un canale. Non selezionare l&#39;indirizzo di posta elettronica; non è un canale.
   * Nella pagina successiva, seleziona **[!UICONTROL Accetta]** per consentire l&#39;accesso a questo canale.

1. Seleziona **[!UICONTROL Consenti]**.

   Ora imposta i tag per la pubblicazione.

1. **[!UICONTROL Impostazione dei tag per la pubblicazione]** - Nella pagina Cloud Services > YouTube , seleziona l’icona a forma di matita per modificare l’elenco dei tag da utilizzare.
1. Per visualizzare l’elenco dei tag disponibili in Experience Manager, seleziona l’icona dell’elenco a discesa (cursore verso il basso).
1. Per aggiungerli, selezionare uno o più tag.

   Per eliminare un tag aggiunto, selezionalo e seleziona **[!UICONTROL X]**.

1. Dopo aver aggiunto i tag desiderati, seleziona **[!UICONTROL Salva]**.

   Ora pubblichi i video sul tuo canale YouTube.

#### Configurare YouTube in Experience Manager prima della versione 6.4 {#setting-up-youtube-in-aem-before}

1. Assicurati di accedere alla tua istanza di Dynamic Media come amministratore.

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra individua **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Services]**.
1. Nell’intestazione Servizi di terze parti, in YouTube, seleziona **[!UICONTROL Configura ora]**.
1. Nella finestra di dialogo Crea configurazione, immetti un titolo (obbligatorio) e un nome (facoltativo) nei rispettivi campi.
1. Seleziona **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Impostazioni account di YouTube, immetti l’ID progetto Google nel campo **[!UICONTROL Nome applicazione]**.

   Hai specificato l&#39;ID progetto all&#39;inizio [impostazioni Google Cloud configurate](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) prima.
Lascia aperta la finestra di dialogo Impostazione account YouTube; ci ritornate tra un momento.

1. Utilizzando un editor di testo normale, apri il file JSON scaricato e salvato in precedenza nell’attività Configurazione delle impostazioni di Google Cloud .
1. Seleziona e copia l’intero testo JSON.
1. Torna alla finestra di dialogo Impostazioni account YouTube. Nel campo **[!UICONTROL Configurazione JSON]**, incolla il testo JSON.
1. Seleziona **[!UICONTROL OK]**.

   Ora configura i canali YouTube nell’Experience Manager.

1. A destra di **[!UICONTROL Canali disponibili]**, seleziona **+** (icona del segno più).
1. Nella finestra di dialogo Impostazioni canale YouTube, fai clic sul campo Titolo e immetti il nome del canale creato nell’attività precedente **[!UICONTROL Aggiunta di uno o più canali a YouTube]**.

   Facoltativamente, puoi aggiungere una descrizione.

1. Seleziona **[!UICONTROL OK]**.
1. Viene visualizzata la verifica YouTube/Google. Se non hai già effettuato l’accesso all’account Google Cloud, salta questo passaggio.

   * Immetti il nome utente e la password Google associati all’ID progetto Google e al testo JSON sopra riportato.
   * A seconda del numero di canali di cui dispone l’account, vengono visualizzati due o più elementi. Seleziona un canale. Non selezionare l&#39;indirizzo di posta elettronica; non è un canale.
   * Nella pagina successiva, seleziona **[!UICONTROL Accetta]** per consentire l&#39;accesso a questo canale.

1. Seleziona **[!UICONTROL Consenti]**.

   Ora imposta i tag per la pubblicazione.

1. **[!UICONTROL Impostazione dei tag per la pubblicazione]** - Nella pagina Cloud Services > YouTube , seleziona l’icona a forma di matita per modificare l’elenco dei tag da utilizzare.
1. Per visualizzare l’elenco dei tag disponibili in Experience Manager, seleziona l’icona dell’elenco a discesa (cursore verso il basso).
1. Per aggiungerli, selezionare uno o più tag.

   Per eliminare un tag aggiunto, selezionalo e seleziona **X**.

1. Dopo aver aggiunto i tag desiderati, seleziona **[!UICONTROL OK]**.

   Ora pubblichi i video sul tuo canale YouTube.

### (Facoltativo) Automatizza l&#39;impostazione delle proprietà predefinite di YouTube per i video caricati {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Facoltativamente, puoi automatizzare l’impostazione delle proprietà di YouTube al caricamento dei video. Crea un profilo di elaborazione dei metadati in Experience Manager.

Per creare il profilo di elaborazione dei metadati, devi prima copiare i valori dai campi **[!UICONTROL Etichetta campo]**, **[!UICONTROL Mappa su proprietà]** e **[!UICONTROL Scelte]**, tutti disponibili in Schemi metadati per i video. Quindi, puoi creare il tuo profilo di elaborazione dei metadati video YouTube aggiungendo tali valori a esso.

**Per automatizzare l’impostazione delle proprietà predefinite di YouTube per i video caricati:**

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra individua **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona **[!UICONTROL default]**. (Non aggiungere un segno di spunta alla casella di selezione a sinistra di &quot;default&quot;.)
1. Sulla **[!UICONTROL default]** , seleziona la casella a sinistra di **[!UICONTROL video]**, quindi seleziona **[!UICONTROL Modifica]**.
1. Nella pagina Editor schema metadati , seleziona la **[!UICONTROL Avanzate]** scheda .
1. Nell’intestazione Pubblicazione YouTube, seleziona **[!UICONTROL Categoria YouTube]**.
1. Sul lato destro della pagina, sotto il **[!UICONTROL Impostazioni]** esegui le seguenti operazioni:

   * In **[!UICONTROL Mappa su proprietà]** campo di testo, selezionare e copiare il valore.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando crei il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

   * Sotto **[!UICONTROL Scelte]**, seleziona e copia il valore predefinito da utilizzare (ad esempio Persone e blog o Scienza e tecnologia).
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando crei il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

1. Nell’intestazione Pubblicazione YouTube, seleziona **[!UICONTROL Privacy di YouTube]**.
1. Sul lato destro della pagina, sotto il **[!UICONTROL Impostazioni]** esegui le seguenti operazioni:

   * In **[!UICONTROL Mappa su proprietà]** campo di testo, selezionare e copiare il valore.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando crei il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

   * Sotto **[!UICONTROL Scelte]**, seleziona e copia il valore predefinito da utilizzare. Le scelte sono raggruppate in coppie di due. Il campo inferiore della coppia è il valore predefinito che si desidera copiare, ad esempio pubblico, non elencato o privato.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando crei il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

1. Nell’angolo in alto a destra della pagina Editor schema metadati, seleziona **[!UICONTROL Annulla]**.
1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi seleziona nella barra a sinistra **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]**.

1. Nella pagina Profili metadati , seleziona nell’angolo superiore destro della pagina **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Aggiungi profilo metadati, nella finestra di dialogo **[!UICONTROL Titolo del profilo]** campo di testo, immettere il nome `YouTube Video` quindi seleziona **[!UICONTROL Crea]**.
1. Nella pagina Editor profilo metadati , seleziona la **[!UICONTROL Avanzamento]** scheda .
1. Aggiungi i valori di pubblicazione YouTube copiati al profilo facendo quanto segue:

   * Sul lato destro della pagina, seleziona la **[!UICONTROL Crea modulo]** scheda .
   * (Facoltativo) Trascina il componente con etichetta **[!UICONTROL Intestazione sezione]** a sinistra e rilasciarla nell’area del modulo.
   * (Facoltativo) Seleziona **[!UICONTROL Etichetta campo]** per selezionare il componente.
   * (Facoltativo) Sul lato destro della pagina, sotto la scheda Impostazioni, nel campo di testo Etichetta campo, immetti . `YouTube Publishing`.
   * Seleziona la **[!UICONTROL Crea modulo]** , quindi trascina il componente etichettato **[!UICONTROL Testo con più valori]** e rilasciarlo sotto il **[!UICONTROL Pubblicazione YouTube]** intestazione creata.

   * Per selezionare il componente, seleziona **[!UICONTROL Etichetta campo]**.
   * Sul lato destro della pagina, nella scheda Impostazioni , incolla i valori di Pubblicazione YouTube (Valore etichetta campo e Mappa su valore proprietà) copiati in precedenza, nei rispettivi campi del modulo. Incolla il valore di Scelte nel campo Valore predefinito .

1. Aggiungi i valori di YouTube Privacy copiati al profilo facendo quanto segue:

   * Sul lato destro della pagina, seleziona la **[!UICONTROL Crea modulo]** scheda .
   * (Facoltativo) Trascina il componente con etichetta **[!UICONTROL Intestazione sezione]** a sinistra e rilasciarla nell’area del modulo.
   * (Facoltativo) Seleziona **[!UICONTROL Etichetta campo]** per selezionare il componente.
   * (Facoltativo) Sul lato destro della pagina, sotto la scheda Impostazioni, nel campo di testo Etichetta campo, immetti . `YouTube Privacy`.
   * Seleziona la **[!UICONTROL Crea modulo]** , quindi trascina il componente etichettato **[!UICONTROL Testo con più valori]** e rilasciarlo sotto il **[!UICONTROL Privacy di YouTube]** intestazione creata.

   * Per selezionare il componente, seleziona **[!UICONTROL Etichetta campo]**.
   * Sul lato destro della pagina, nella scheda Impostazioni , incolla i valori di Pubblicazione YouTube (Valore etichetta campo e Mappa su valore proprietà) copiati in precedenza, nei rispettivi campi del modulo. Incolla il valore di Scelte nel campo Valore predefinito .

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva]**.
1. Applica il profilo metadati Pubblicazione YouTube alle cartelle in cui stai per caricare i video. È necessario disporre sia del profilo metadati che del profilo video impostato.

   Consulta le sezioni [Profili di metadati](/help/assets/metadata-profiles.md) e [Profili video](/help/assets/dynamic-media/video-profiles.md).

### Pubblicare video sul canale YouTube {#publishing-videos-to-your-youtube-channel}

Ora puoi associare i tag aggiunti in precedenza alle risorse video. Questo processo consente ad Experience Manager di sapere quali risorse pubblicare sul tuo canale YouTube.

>[!NOTE]
>
>La pubblicazione immediata non viene pubblicata automaticamente in YouTube. Quando si imposta Dynamic Media, è possibile scegliere tra due opzioni di pubblicazione: **[!UICONTROL Immediatamente]** o **[!UICONTROL All’attivazione]**.
>
>**[!UICONTROL Pubblica immediatamente]** significa che la risorsa caricata dopo la sincronizzazione con IPS viene pubblicata automaticamente nel sistema di consegna. Anche se questo vale per Dynamic Media, non è vero per YouTube. Per pubblicare in YouTube, devi pubblicarlo tramite Experience Manager Author.

>[!NOTE]
Per pubblicare contenuti da YouTube, Experience Manager utilizza la funzione **[!UICONTROL Pubblicare su YouTube]** , che consente di monitorare l’avanzamento e visualizzare eventuali informazioni di errore.
Vedi [Monitorare la codifica video e lo stato di pubblicazione di YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
Per informazioni più dettagliate sullo stato, è possibile monitorare il log YouTube sotto replica. Tuttavia, tale monitoraggio richiede l’accesso dell’amministratore.

**Per pubblicare i video sul tuo canale YouTube:**

1. Ad Experience Manager, accedi a una risorsa video da pubblicare sul tuo canale YouTube.
1. Seleziona la risorsa video (il set video adattivo).
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda Base, sotto l’intestazione Metadati, selezionare **[!UICONTROL Finestra di dialogo Apri selezione]** a destra del campo Tag .
1. Nella pagina Seleziona tag individua i tag da utilizzare, quindi seleziona uno o più tag.

   I tag devono essere associati al canale YouTube.

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Seleziona]**.
1. Nell’angolo in alto a destra della pagina delle proprietà del video, seleziona **[!UICONTROL Salva e chiudi]**.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

   Vedi anche [Utilizzare la gestione della pubblicazione con Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   Facoltativamente, puoi verificare il video pubblicato sul tuo canale YouTube.

### (Facoltativo) Verifica il video pubblicato su YouTube {#optional-verifying-the-published-video-on-youtube}

Facoltativamente, puoi monitorare l’avanzamento della pubblicazione di YouTube (o l’annullamento della pubblicazione).

Vedi [Monitorare la codifica video e lo stato di pubblicazione di YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

I tempi di pubblicazione possono variare notevolmente a seconda di numerosi fattori che includono il formato del video sorgente principale, la dimensione del file e il traffico di caricamento. Il processo di pubblicazione può richiedere da qualche minuto a diverse ore. Inoltre, i formati a risoluzione più elevata vengono resi molto più lentamente. Ad esempio, 720p e 1080p richiedono più tempo per apparire di 480p.

Dopo otto ore, se vedi ancora un messaggio di stato che dice **[!UICONTROL Caricato (elaborazione, attendi)]**, prova a rimuovere il video dal sito e caricarlo di nuovo.

### Collegare gli URL di YouTube all’applicazione Web {#linking-youtube-urls-to-your-web-application}

Puoi ottenere una stringa URL YouTube generata da Dynamic Media dopo la pubblicazione del video. Quando copi l’URL di YouTube, questo viene inserito negli Appunti, in modo da poterlo incollare come necessario nelle pagine del sito web o dell’applicazione.

>[!NOTE]
L’URL di YouTube non è disponibile per la copia finché non avrai pubblicato la risorsa video in YouTube.

Per collegare gli URL YouTube alla tua applicazione web:

1. Passa a *YouTube pubblicato* risorsa video di cui desideri copiare l’URL, quindi selezionalo.

   Gli URL di YouTube sono disponibili solo per la copia *dopo* hai il primo *pubblicato* le risorse video in YouTube.

1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Avanzate]** scheda .
1. Sotto l’intestazione Pubblicazione YouTube, nell’elenco URL di YouTube, seleziona e copia il testo dell’URL nel browser web per visualizzare l’anteprima della risorsa o per aggiungerla alla pagina del contenuto web.

### Annullare la pubblicazione di video in modo da poterli rimuovere da YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Quando si annulla la pubblicazione di una risorsa video in Experience Manager, il video viene rimosso da YouTube.

>[!CAUTION]
Se rimuovi un video direttamente da YouTube, Experience Manager ignora e continua a comportarsi come se il video fosse ancora pubblicato in YouTube. Per Experience Manager, annulla sempre la pubblicazione di una risorsa video da YouTube.

>[!NOTE]
Per rimuovere contenuti da YouTube, Experience Manager utilizza la funzione **[!UICONTROL Annullare la pubblicazione da YouTube]** , che consente di monitorare l’avanzamento e visualizzare eventuali informazioni di errore.
Vedi [Monitorare la codifica video e lo stato di pubblicazione di YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Per annullare la pubblicazione dei video e rimuoverli da YouTube:**

1. Passa alle risorse video da cui desideri annullare la pubblicazione dal canale YouTube.
1. In una modalità di selezione delle risorse, seleziona una o più risorse video pubblicate.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Se necessario, seleziona l’icona dei tre punti (`. . .`) sulla barra degli strumenti da visualizzare **[!UICONTROL Gestisci pubblicazione]**.
1. Nella pagina Gestisci pubblicazione, seleziona **[!UICONTROL Annulla pubblicazione]**.
1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Successivo]**.
1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Annulla pubblicazione]**.

## Monitorare la codifica video e lo stato di pubblicazione di YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Quando carichi un nuovo video in una cartella a cui è stata applicata la codifica video o, pubblichi il video in YouTube, monitora l’avanzamento (o il mancato funzionamento) della codifica video/pubblicazione su Youtube. L’avanzamento effettivo della pubblicazione in YouTube è disponibile solo tramite i registri. Tuttavia, indipendentemente dal suo esito positivo o negativo, viene elencato in altri modi descritti nella procedura seguente. Inoltre, ricevi notifiche e-mail quando un flusso di lavoro o una codifica video di pubblicazione di YouTube viene completata o interrotta.

### Avanzamento monitor {#monitoring-progress}

Puoi monitorare l’avanzamento, inclusa la codifica non riuscita/pubblicazione YouTube.

1. Visualizza l’avanzamento della codifica video nella cartella delle risorse:

   * Nella vista a schede, l’avanzamento della codifica video viene visualizzato per percentuale sulla risorsa. In caso di errore, queste informazioni vengono visualizzate anche sulla risorsa.

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * Nella vista a elenco, l’avanzamento della codifica video viene visualizzato nella **[!UICONTROL Stato di elaborazione]** colonna. In caso di errore, il messaggio viene visualizzato nella stessa colonna.

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   Questa colonna non viene visualizzata per impostazione predefinita. Per abilitare la colonna, seleziona **[!UICONTROL Visualizza impostazioni]** dal menu a discesa delle viste e aggiungi il **[!UICONTROL Stato di elaborazione]** e seleziona **[!UICONTROL Aggiorna]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Visualizza l’avanzamento nei dettagli della risorsa. Quando selezioni una risorsa, apri il menu a discesa e seleziona **[!UICONTROL Timeline]**. Per limitare l’attività al flusso di lavoro, ad esempio la codifica o la pubblicazione in YouTube, seleziona **[!UICONTROL Flussi di lavoro]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   Tutte le informazioni sul flusso di lavoro, ad esempio la codifica, vengono visualizzate nella timeline. Per la pubblicazione in YouTube, la timeline del flusso di lavoro include anche il nome del canale YouTube e l’URL video YouTube. Inoltre, puoi visualizzare eventuali notifiche di errore nella timeline del flusso di lavoro al termine della pubblicazione.

   >[!NOTE]
   Potrebbero essere necessari tempi lunghi per la registrazione dei messaggi di errore o di errore a causa di più configurazioni del flusso di lavoro in **[!UICONTROL tentativi]**, **[!UICONTROL ritardo]** e **[!UICONTROL timeout]** da [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)ad esempio:
   * Configurazione della coda dei processi Sling Apache
   * Adobe Granite Workflow External Process Job Handler
   * Coda timeout flusso di lavoro Granite

   È possibile regolare le **[!UICONTROL tentativi]**, **[!UICONTROL ritardo]** e **[!UICONTROL timeout]** in queste configurazioni.

1. Per i flussi di lavoro in corso, vedi l’opzione Istanze flusso di lavoro accedendo a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Istanze]**.

   >[!NOTE]
   Per accedere al **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   Seleziona l’istanza e seleziona **[!UICONTROL Cronologia aperta]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   Dall’area Istanze flusso di lavoro puoi anche sospendere, terminare o rinominare i flussi di lavoro. Vedi [Amministrare i flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md) per ulteriori informazioni.

1. Per i processi non riusciti, consulta l’opzione Errori di flusso di lavoro, accessibile da **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Errori]**. In **[!UICONTROL Errore flusso di lavoro]** sono elencate tutte le attività del flusso di lavoro che hanno generato errori.

   >[!NOTE]
   Per accedere al **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   Potrebbero essere necessari tempi lunghi per la registrazione del messaggio di errore a causa di più configurazioni del flusso di lavoro nelle **[!UICONTROL tentativi]**, **[!UICONTROL ritardo]** e **[!UICONTROL timeout]** da [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)ad esempio:
   * Configurazione della coda dei processi Sling Apache
   * Adobe Granite Workflow External Process Job Handler
   * Coda timeout flusso di lavoro Granite

   È possibile regolare le **[!UICONTROL tentativi]**, **[!UICONTROL ritardo]** e **[!UICONTROL timeout]** in queste configurazioni.

1. Per i flussi di lavoro completati, consulta Archivio flussi di lavoro, accessibile da **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Archivio]**. **[!UICONTROL Archivio flussi di lavoro]** elenca tutte le attività del flusso di lavoro che sono state completate.

   >[!NOTE]
   Per accedere al **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. Ricevi notifiche e-mail sui processi del flusso di lavoro interrotti o non riusciti. Queste notifiche e-mail sono configurabili da un amministratore. Vedi [Configurare le notifiche e-mail](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## Transcodifica tramite il profilo di elaborazione {#transcode-video}

[!DNL Experience Manager] come [!DNL Cloud Service] consente di eseguire la transcodifica di base dei file video MP4 utilizzando Profili di elaborazione. La funzionalità ti consente non solo di caricare, ma anche di visualizzare in anteprima e scalare un file video MP4.

![Crea profilo di elaborazione per la transcodifica video in [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Un profilo di elaborazione per la transcodifica video in [!DNL Experience Manager].*

Se specifichi solo la larghezza o solo l’altezza e lasci vuoto l’altro campo, le rappresentazioni mantengono le proporzioni. Il codec video H.264 è disponibile per la transcodifica.

Per elaborare le risorse utilizzando un profilo di elaborazione, aggiungi un profilo a una cartella. Vedi [utilizzare i profili di elaborazione per elaborare le risorse](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Annotare risorse video {#annotate-video-assets}

Puoi aggiungere annotazioni alle risorse video. Durante l&#39;annotazione dei video, il lettore si mette in pausa per consentirvi di annotare un fotogramma. Per maggiori dettagli, vedi [gestione delle risorse video](manage-video-assets.md).

>[!NOTE]
Il formato video MXF non è ancora supportato con le annotazioni delle risorse video.

1. Da [!DNL Assets] console, seleziona **[!UICONTROL Modifica]** nella scheda della risorsa per visualizzare la pagina dei dettagli della risorsa.
1. Per riprodurre il video, fai clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fai clic su **[!UICONTROL Annota]**. Viene aggiunta un’annotazione alla data e all’ora specifiche (fotogramma) del video. Durante l&#39;annotazione, potete disegnare sull&#39;area di lavoro e includere un commento nel disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata dell’annotazione, fai clic su **[!UICONTROL Chiudi]**.
1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.
1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fai clic su **[!UICONTROL Elimina]**.

## Best practice e limitazioni {#tips-limitations}

* Senza [!DNL Dynamic Media] è possibile elaborare solo file MP4 utilizzando i profili di elaborazione.
* Quando si transcodificano file MP4 utilizzando i Profili di elaborazione, si applicano le seguenti linee guida e limitazioni:

   * I file ProRes di Apple possono solo transcodificare ad una risoluzione massima di 1080p.
   * Se il file di origine ha un bitrate >200 Mbps, è possibile eseguire la transcodifica solo a una risoluzione massima di 1080p.
   * Se il framerate di origine >=60 fps allora, la dimensione massima del file di origine che è possibile utilizzare è,

      * 400 MB per transcodifica 4k.
      * 800 MB per transcodifica 1080p.
      * 8 GB per transcodifica 720p.
   * La dimensione massima del file che è possibile transcodificare in risoluzione 4k è un file MP4 da 2,55 GB con risoluzione 4k, bitrate da 12 Mbps e 23 fps.

   **Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

>[!MORELIKETHIS]
* [Documentazione video Dynamic Media](/help/assets/dynamic-media/video.md).
* [Scopri di più su utilizzo, tipi e configurazione dei profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).

