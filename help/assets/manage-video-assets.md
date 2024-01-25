---
title: Gestire le risorse video
description: Caricare, visualizzare in anteprima, annotare e pubblicare risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 4b05e8f8ae554e7c0881134ef24ca8ce35e3e2bf
workflow-type: tm+mt
source-wordcount: '4976'
ht-degree: 6%

---

# Gestire le risorse video {#manage-video-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Il formato video è una parte fondamentale delle risorse digitali di un’organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzioni mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, sono possibili utilizzando Profili di elaborazione e utilizzando [!DNL Dynamic Media] integrazione. Senza [!DNL Dynamic Media] licenza, [!DNL Experience Manager] fornisce il supporto di base per i video, ad esempio la transcodifica tramite FFmpeg, l’estrazione delle miniature di anteprima per i formati di file supportati e l’anteprima nell’interfaccia utente per i formati supportati per la riproduzione diretta nel browser.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

Puoi caricare e visualizzare in anteprima le risorse video nel formato supportato in [!DNL Experience Manager Assets].
<!-- It generates previews for video assets with the extension MP4. -->

### Caricare risorse video

Per caricare una risorsa video, effettua le seguenti operazioni:

1. Nella cartella o nelle sottocartelle delle risorse digitali, individua il percorso in cui devi aggiungere la risorsa.
1. Clic **[!UICONTROL Crea]** dalla barra degli strumenti e scegli **[!UICONTROL File]**. <br>In alternativa, trascina un file sull’interfaccia utente.
Ulteriori informazioni su [caricamento delle risorse](manage-digital-assets.md#uploading-assets) in [!DNL Experience Manager Assets].

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### Visualizzare in anteprima le risorse video

Puoi visualizzare in anteprima i video nelle rappresentazioni supportate in [!DNL Assets] dell&#39;utente. Per visualizzare in anteprima una risorsa video, effettua le seguenti operazioni:

1. Carica una risorsa video di un formato supportato in [!DNL Experience Manager Assets]. Ulteriori informazioni su [formati video supportati](file-format-support.md#video-formats). <br>Una volta caricata, la risorsa video viene elaborata e viene generata una rappresentazione di anteprima.
1. Fai clic sulla risorsa e seleziona ![opzione dettagli](assets/do-not-localize/details_icon.svg) **[!UICONTROL Dettagli]**  dalla barra degli strumenti superiore. La risorsa video si apre nel visualizzatore video.
1. Fai clic su ![opzione di riproduzione](assets/do-not-localize/play.png) sulla miniatura del video. <br>È possibile riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

Per le risorse video esistenti in [!DNL Experience Manager Assets], è necessario **[!UICONTROL Rielabora]** le risorse in [!DNL Experience Manager] per attivare la funzione di anteprima video. Scopri come [rielaborare le risorse digitali](reprocessing.md) in [!DNL Experience Manager].

### Limitazioni dell’anteprima video

* I file MXF non mostrano le anteprime video anche se viene generata la rappresentazione.
* I file WebM non generano copie trasformate di anteprima in quanto possono essere riprodotti in modalità nativa dai browser Web.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, puoi includere le risorse video in una pagina web come URL o incorporarle direttamente. Per ulteriori informazioni, consulta [pubblicare [!DNL Dynamic Media] risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Pubblicare video su YouTube {#publishing-videos-to-youtube}

Puoi pubblicare le risorse video gestite in Experience Manager Assets direttamente su un canale YouTube creato in precedenza.

Per pubblicare risorse video in YouTube, devi assegnare tag alle risorse video in Experience Manager Assets. Associa questi tag a un canale YouTube. Se il tag di una risorsa video corrisponde a quello di un canale YouTube, il video viene pubblicato in YouTube. La pubblicazione su YouTube viene eseguita insieme alla normale pubblicazione del video, purché venga utilizzato un tag associato.

YouTube esegue la propria codifica. Di conseguenza, il file video originale caricato in Experience Manager viene pubblicato in YouTube invece di qualsiasi rendering video creato con la codifica Dynamic Medie. Anche se non è necessario per elaborare i video utilizzando Dynamic Medie, è previsto che lo facciano nel caso in cui sia necessario un predefinito visualizzatore per la riproduzione.

Quando salti il profilo di elaborazione video e pubblichi direttamente in YouTube, significa semplicemente che la risorsa video in Experience Manager Asset non riceve una miniatura visualizzabile. Significa anche che i video non codificati non funzionano con nessuno dei tipi di risorse Dynamic Medie.

La pubblicazione di risorse video sui server YouTube prevede il completamento delle seguenti attività per garantire una verifica server-to-server sicura con YouTube:

1. [Configurare le impostazioni di Google Cloud](#configuring-google-cloud-settings)
1. [Creare un canale YouTube](#creating-a-youtube-channel)
1. [Aggiungi tag per la pubblicazione](#adding-tags-for-publishing)
1. [Configurare YouTube in Experience Manager](#setting-up-youtube-in-aem)
1. [(Facoltativo) Automatizza l&#39;impostazione delle proprietà predefinite di YouTube per i video caricati](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Pubblicare video sul canale YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Facoltativo) Verifica il video pubblicato su YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Collegare gli URL di YouTube all’applicazione web](#linking-youtube-urls-to-your-web-application)

È inoltre possibile [annullare la pubblicazione dei video per rimuoverli da YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Configurare le impostazioni di Google Cloud {#configuring-google-cloud-settings}

Per pubblicare su YouTube, è necessario un account Google. Se si dispone di un account GMAIL, si dispone già di un account Google; se non si dispone di un account Google, è possibile crearne facilmente uno. L’account è necessario perché sono necessarie credenziali per pubblicare risorse video in YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

Non è necessario che l’account utilizzato con Google Cloud e l’account Google utilizzato per YouTube siano gli stessi.

Google modifica periodicamente l’interfaccia utente. Di conseguenza, i passaggi per pubblicare video in YouTube possono variare leggermente rispetto a quanto documentato di seguito. Questa avvertenza si applica anche ad YouTube quando tenti di verificare se i video sono stati caricati su di esso.

>[!NOTE]
>
>I seguenti passaggi erano accurati al momento della scrittura. Tuttavia, Google aggiorna periodicamente le pagine web cloud senza preavviso. Di conseguenza, alcune opzioni di configurazione nell’interfaccia utente di Google potrebbero essere denominate in modo leggermente diverso rispetto al nome utilizzato nei passaggi.

**Per configurare le impostazioni di Google Cloud:**

1. Crea un account Google.

   Se disponi già di un account Google, puoi passare al passaggio successivo.

1. Vai a [https://cloud.google.com/](https://cloud.google.com/).
1. Il giorno **[!UICONTROL Google Cloud]** nell&#39;angolo superiore destro, seleziona **[!UICONTROL Console]**.

   Se necessario, **[!UICONTROL Accedi]** utilizzo delle credenziali dell&#39;account Google per visualizzare **[!UICONTROL Console]** opzione.

1. Il giorno **[!UICONTROL Dashboard]** a destra di **[!UICONTROL Piattaforma Google Cloud]**, seleziona la **[!UICONTROL Progetto]** elenco a discesa per aprire **[!UICONTROL Seleziona un progetto]** .
1. In **[!UICONTROL Seleziona un progetto]** finestra di dialogo, seleziona **[!UICONTROL Nuovo progetto]**.
1. In **[!UICONTROL Nuovo progetto]** nella finestra di dialogo **[!UICONTROL Nome progetto]** digitare il nome del nuovo progetto.

   L&#39;ID progetto si basa sul nome del progetto. Pertanto, scegli attentamente il nome del progetto, che non può essere modificato dopo la creazione. Inoltre, devi immettere nuovamente lo stesso ID progetto quando configuri YouTube in Experience Manager in un secondo momento. Pertanto, trascrivilo.

1. Seleziona **[!UICONTROL Crea]**.

1. Effettuare una delle seguenti operazioni:

   * Nel dashboard del progetto, nella sezione **[!UICONTROL Guida introduttiva]** , seleziona **[!UICONTROL Esplora e abilita API]**.
   * Nel dashboard del progetto, nella sezione **[!UICONTROL API]** , seleziona **[!UICONTROL Vai alla panoramica delle API]**.

1. Vicino alla parte superiore centrale del **[!UICONTROL API e servizi]** pagina, seleziona **[!UICONTROL ABILITA API E SERVIZI]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. Il giorno **[!UICONTROL Libreria API]** pagina, a sinistra, sotto **[!UICONTROL Categoria]**, seleziona **[!UICONTROL YouTube]**. Sul lato destro della pagina, seleziona **[!UICONTROL YouTube]**.
1. Il giorno **[!UICONTROL YouTube]** pagina, seleziona **[!UICONTROL API dati YouTube v3]**.
1. Il giorno **[!UICONTROL API dati YouTube v3]** pagina, seleziona **[!UICONTROL GESTISCI]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. Per utilizzare l’API, sono necessarie le credenziali. Se necessario, sul lato sinistro del **[!UICONTROL API e servizi]** pagina, seleziona **[!UICONTROL Credenziali]**.
1. Il giorno **[!UICONTROL Credenziali]** nella parte superiore, seleziona **[!UICONTROL CREA CREDENZIALI]**, quindi seleziona **[!UICONTROL ID client OAuth]**.
1. Il giorno **[!UICONTROL Crea ID client OAuth]** pagina, nella **[!UICONTROL Tipo di applicazione]** elenco a discesa, seleziona **[!UICONTROL Applicazione web]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Effettua una delle operazioni seguenti:

   * In **[!UICONTROL Nome]** immetti un nome univoco per il client OAuth 2.0.
   * Utilizza il nome predefinito già fornito da Google nel **[!UICONTROL Nome]** campo.

1. Sotto **[!UICONTROL Origini JavaScript autorizzate]** intestazione, seleziona **[!UICONTROL AGGIUNGI URI]**.

   ![6_5_googleaccount-apis-namepermissions](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. In **[!UICONTROL URI]** immettere il seguente percorso, sostituendo il proprio dominio e il proprio numero di porta nel percorso, quindi premere **[!UICONTROL Invio]** per aggiungere il percorso all&#39;elenco:

   `https://<servername.domain>:<port_number>`

   Ad esempio `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >L’esempio del percorso URI riportato sopra è ipotetico e solo a scopo illustrativo.

1. Sotto **[!UICONTROL URI di reindirizzamento autorizzati]** , selezionare ADD URI.
1. In **[!UICONTROL URI]** immettere il seguente percorso, sostituendo il proprio dominio e il proprio numero di porta nel percorso, quindi premere **[!UICONTROL Invio]** per aggiungere il percorso all&#39;elenco:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Ad esempio `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >L’esempio del percorso URI riportato sopra è ipotetico e solo a scopo illustrativo.

1. Vicino alla parte inferiore del **[!UICONTROL Crea ID client OAuth]** pagina, seleziona **[!UICONTROL Crea]**.
1. Il giorno **[!UICONTROL Client OAuth creato]** eseguire le operazioni seguenti:

   * (Facoltativo) Copia i valori in **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** e salvare.
   * Seleziona **[!UICONTROL SCARICA JSON]**, quindi salva il file JSON.

   Questo file JSON scaricato è necessario per la configurazione di YouTube in Adobe Experience Manager in un secondo momento.

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. Il giorno **[!UICONTROL Client OAuth creato]** finestra di dialogo, seleziona **[!UICONTROL OK]**.
1. Esci dal tuo account Google. Ora crea un canale YouTube.

### Creare un canale YouTube {#creating-a-youtube-channel}

La pubblicazione di video in YouTube richiede la presenza di uno o più canali. Se hai già creato un canale YouTube, puoi saltare questa attività e passare a [Aggiungi tag per la pubblicazione](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Verifica di aver già configurato uno o più canali in YouTube *prima di* aggiungi canali in Impostazioni YouTube in Experience Manager (consulta [Configurare YouTube in Experience Manager](#setting-up-youtube-in-aem) di seguito). Se non si esegue la configurazione del canale, non viene visualizzato alcun avviso relativo all&#39;assenza di canali esistenti. Tuttavia, la verifica Google si verifica ancora quando si aggiunge un canale, ma non è possibile scegliere quale canale inviare il video.

**Per creare un canale YouTube:**

1. Vai a [https://www.youtube.com](https://www.youtube.com/) e accedi utilizzando le credenziali del tuo account Google.
1. Nell’angolo in alto a destra della pagina YouTube, seleziona l’immagine del profilo (può anche apparire come lettera all’interno di un cerchio di colore uniforme), quindi seleziona **[!UICONTROL Impostazioni di YouTube]** (icona a forma di ingranaggio circolare).
1. Nella pagina Overview (Panoramica), sotto l’intestazione Additional Features (Caratteristiche aggiuntive), seleziona **[!UICONTROL Visualizza tutti i miei canali o crea un canale]**.
1. Nella pagina Canali, seleziona **[!UICONTROL Crea un nuovo canale]**.
1. Nella pagina Account marchio, immetti il nome di una società o di qualsiasi altro nome di canale scelto per la pubblicazione delle risorse video nel campo Nome account marchio, quindi seleziona **[!UICONTROL Crea]**.

   Ricorda il nome che immetti qui; devi immetterlo nuovamente quando devi impostare YouTube in Experience Manager.

1. Se necessario, aggiungi altri canali.

   Ora puoi aggiungere tag per la pubblicazione.

### Aggiungi tag per la pubblicazione {#adding-tags-for-publishing}

Per pubblicare i video in YouTube, Experience Manager associa i tag a uno o più canali di YouTube. Per aggiungere tag per la pubblicazione, consulta [Amministrare i tag](/help/sites-cloud/authoring/features/tags.md).

Oppure, se desideri utilizzare i tag predefiniti in Experience Manager, puoi saltare questa attività e passare a [Configurare YouTube in Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>Una volta configurato il Cloud Service, non è necessaria un’altra configurazione per abilitare l’agente di replica YouTube Publish in questo momento. Il motivo è che è stato abilitato quando è stata salvata la configurazione del Cloud Service.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Configurare YouTube in Experience Manager {#setting-up-youtube-in-aem}

A partire dall’Experience Manager 6.4, è stato introdotto un nuovo metodo di interfaccia utente touch per configurare la pubblicazione YouTube in Experience Manager. In base all&#39;istanza installata di Experience Manager in uso, eseguire una delle operazioni seguenti:

* Per configurare YouTube in Experience Manager prima della versione 6.4, consulta [Configurare YouTube in Experience Manager prima della versione 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Per configurare YouTube nell’Experience Manager 6.4 o versione successiva, consulta [Configurare YouTube all’Experience Manager 6.4 e versioni successive](#setting-up-youtube-in-aem-and-later).

#### Configurare YouTube all’Experience Manager 6.4 e versioni successive {#setting-up-youtube-in-aem-and-later}

1. Accertati di accedere alla tua istanza di Dynamic Medie come amministratore.
1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]**(icona a forma di martello) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione pubblicazione YouTube]**.
1. Seleziona **[!UICONTROL globale]** (non selezionarlo).

1. Nell’angolo superiore destro della pagina globale, seleziona **[!UICONTROL Crea]**.
1. Nella pagina Crea configurazione YouTube, seleziona Impostazioni piattaforma Google Cloud, quindi immetti l’ID progetto Google nel campo **[!UICONTROL Nome applicazione]**.

   Hai specificato l’ID del progetto al momento della configurazione iniziale delle impostazioni di Google Cloud.
Lascia aperta la pagina Crea configurazione di YouTube; tornerai tra un attimo.

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Utilizzando un editor di testo normale, apri il file JSON scaricato e salvato in precedenza nell’attività [Configurare le impostazioni di Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. Seleziona e copia l’intero testo JSON.
1. Torna alla finestra di dialogo Impostazioni account YouTube. Nel campo **[!UICONTROL Configurazione JSON]**, incolla il testo JSON.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   Ora imposta i canali YouTube in Experience Manager.

1. Seleziona **[!UICONTROL Aggiungi canale]**.
1. Nel campo Nome canale, inserisci il nome del canale creato nell’attività **[!UICONTROL Aggiunta di uno o più canali ad YouTube]** prima.

   Facoltativamente, puoi aggiungere una descrizione, se necessario.

1. Seleziona **[!UICONTROL Aggiungi]**.
1. Viene visualizzata la verifica YouTube/Google. Se non hai già effettuato l’accesso all’account Google Cloud, salta questo passaggio.

   * Inserisci il nome utente e la password di Google associati all’ID progetto Google e al testo JSON qui sopra.
   * A seconda di quanti canali dispone il tuo account, puoi visualizzare due o più elementi. Seleziona un canale. Non selezionare l&#39;indirizzo di posta elettronica, non è un canale.
   * Nella pagina successiva, seleziona **[!UICONTROL Accetta]** per consentire l’accesso a questo canale.

1. Seleziona **[!UICONTROL Consenti]**.

   Ora imposta i tag per la pubblicazione.

1. **[!UICONTROL Impostazione dei tag per la pubblicazione]** - Nella pagina Cloud Service > YouTube, seleziona l’icona a forma di matita per modificare l’elenco di tag che desideri utilizzare.
1. Per visualizzare l’elenco dei tag disponibili in Experience Manager, seleziona l’icona a discesa dell’elenco (cursore a discesa).
1. Per aggiungerli, seleziona uno o più tag.

   Per eliminare un tag aggiunto, selezionalo e seleziona **[!UICONTROL X]**.

1. Dopo aver aggiunto i tag desiderati, seleziona **[!UICONTROL Salva]**.

   Ora pubblichi i video sul tuo canale YouTube.

#### Configurare YouTube in Experience Manager prima della versione 6.4 {#setting-up-youtube-in-aem-before}

1. Accertati di accedere alla tua istanza di Dynamic Medie come amministratore.

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Service]**.
1. Nell’intestazione Servizi di terze parti, in YouTube, seleziona **[!UICONTROL Configura ora]**.
1. Nella finestra di dialogo Crea configurazione, immetti un titolo (obbligatorio) e un nome (facoltativo) nei rispettivi campi.
1. Seleziona **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Impostazioni account di YouTube, immetti l’ID progetto Google nel campo **[!UICONTROL Nome applicazione]**.

   Hai specificato l’ID del progetto al momento della [impostazioni configurate di Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) prima.
Lascia aperta la finestra di dialogo YouTube Account Setting (Impostazioni account di Adobe Experience Cloud). Tornerai tra poco.

1. Utilizzando un editor di testo normale, apri il file JSON scaricato e salvato in precedenza nell’attività Configurazione delle impostazioni di Google Cloud.
1. Seleziona e copia l’intero testo JSON.
1. Torna alla finestra di dialogo Impostazioni account YouTube. Nel campo **[!UICONTROL Configurazione JSON]**, incolla il testo JSON.
1. Seleziona **[!UICONTROL OK]**.

   Ora imposta i canali YouTube in Experience Manager.

1. A destra di **[!UICONTROL Canali disponibili]**, seleziona **+** (icona del segno più).
1. Nella finestra di dialogo Impostazioni canale YouTube, fai clic sul campo Titolo e immetti il nome del canale creato nell’attività precedente **[!UICONTROL Aggiunta di uno o più canali a YouTube]**.

   Facoltativamente, puoi aggiungere una descrizione, se necessario.

1. Seleziona **[!UICONTROL OK]**.
1. Viene visualizzata la verifica YouTube/Google. Se non hai già effettuato l’accesso all’account Google Cloud, salta questo passaggio.

   * Inserisci il nome utente e la password di Google associati all’ID progetto Google e al testo JSON qui sopra.
   * A seconda di quanti canali dispone il tuo account, puoi visualizzare due o più elementi. Seleziona un canale. Non selezionare l&#39;indirizzo di posta elettronica, non è un canale.
   * Nella pagina successiva, seleziona **[!UICONTROL Accetta]** per consentire l’accesso a questo canale.

1. Seleziona **[!UICONTROL Consenti]**.

   Ora imposta i tag per la pubblicazione.

1. **[!UICONTROL Impostazione dei tag per la pubblicazione]** - Nella pagina Cloud Service > YouTube, seleziona l’icona a forma di matita per modificare l’elenco di tag che desideri utilizzare.
1. Per visualizzare l’elenco dei tag disponibili in Experience Manager, seleziona l’icona a discesa dell’elenco (cursore a discesa).
1. Per aggiungerli, seleziona uno o più tag.

   Per eliminare un tag aggiunto, selezionalo e seleziona **X**.

1. Dopo aver aggiunto i tag desiderati, seleziona **[!UICONTROL OK]**.

   Ora pubblichi i video sul tuo canale YouTube.

### (Facoltativo) Automatizza l&#39;impostazione delle proprietà predefinite di YouTube per i video caricati {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Facoltativamente, puoi automatizzare l’impostazione delle proprietà di YouTube al caricamento dei video. Crea un profilo di elaborazione metadati in Experience Manager.

Per creare il profilo di elaborazione dei metadati, devi prima copiare i valori dai campi **[!UICONTROL Etichetta campo]**, **[!UICONTROL Mappa su proprietà]** e **[!UICONTROL Scelte]**, tutti disponibili in Schemi metadati per i video. Quindi, aggiungi questi valori al profilo di elaborazione dei metadati video di YouTube.

**Per automatizzare l’impostazione delle proprietà predefinite di YouTube per i video caricati:**

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona **[!UICONTROL predefinito]**. (Non aggiungere un segno di spunta alla casella di selezione a sinistra di &quot;default&quot;).
1. Il giorno **[!UICONTROL predefinito]** , seleziona la casella a sinistra di **[!UICONTROL video]**, quindi seleziona **[!UICONTROL Modifica]**.
1. Nella pagina Editor schema metadati, seleziona la **[!UICONTROL Avanzate]** scheda.
1. Sotto l’intestazione Pubblicazione YouTube, seleziona **[!UICONTROL Categoria YouTube]**.
1. Sul lato destro della pagina, sotto **[!UICONTROL Impostazioni]** , eseguire le operazioni seguenti:

   * In **[!UICONTROL Mappa su proprietà]** testo, seleziona e copia il valore.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

   * Sotto **[!UICONTROL Scelte]**, seleziona e copia il valore predefinito che desideri utilizzare (ad esempio Persone e blog o Scienza e tecnologia).
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

1. Sotto l’intestazione Pubblicazione YouTube, seleziona **[!UICONTROL Privacy di YouTube]**.
1. Sul lato destro della pagina, sotto **[!UICONTROL Impostazioni]** , eseguire le operazioni seguenti:

   * In **[!UICONTROL Mappa su proprietà]** testo, seleziona e copia il valore.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

   * Sotto **[!UICONTROL Scelte]**, seleziona e copia il valore predefinito che desideri utilizzare. Notate che le scelte sono raggruppate in coppie di due. Il campo inferiore della coppia è il valore predefinito che si desidera copiare, ad esempio public, unlisted o private.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

1. Nell’angolo superiore destro della pagina Editor schema metadati, seleziona **[!UICONTROL Annulla]**.
1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]**.

1. Nella pagina Profili metadati, nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Aggiungi profilo metadati, nel **[!UICONTROL Titolo profilo]** testo, immettere il nome `YouTube Video` quindi seleziona **[!UICONTROL Crea]**.
1. Nella pagina Editor profilo metadati, seleziona la **[!UICONTROL Avanza]** scheda.
1. Aggiungi al profilo i valori di pubblicazione di YouTube copiati effettuando le seguenti operazioni:

   * Sul lato destro della pagina, seleziona la **[!UICONTROL Genera modulo]** scheda.
   * (Facoltativo) Trascina il componente etichettato **[!UICONTROL Intestazione sezione]** a sinistra e rilasciarlo nell&#39;area del modulo.
   * (Facoltativo) Seleziona **[!UICONTROL Etichetta campo]** per selezionare il componente.
   * (Facoltativo) Nella parte destra della pagina, nella scheda Impostazioni, nel campo di testo Etichetta campo, immetti `YouTube Publishing`.
   * Seleziona la **[!UICONTROL Genera modulo]** , quindi trascina il componente con l’etichetta **[!UICONTROL Testo con più valori]** e rilascialo sotto il **[!UICONTROL Pubblicazione YouTube]** intestazione creata.

   * Per selezionare il componente, seleziona **[!UICONTROL Etichetta campo]**.
   * Nella parte destra della pagina, nella scheda Impostazioni, incolla i valori di pubblicazione di YouTube (valore Etichetta campo e Mappa su valore proprietà) copiati in precedenza nei rispettivi campi del modulo. Incolla il valore Scelte nel campo Valore predefinito.

1. Aggiungi i valori di YouTube Privacy copiati al profilo effettuando le seguenti operazioni:

   * Sul lato destro della pagina, seleziona la **[!UICONTROL Genera modulo]** scheda.
   * (Facoltativo) Trascina il componente etichettato **[!UICONTROL Intestazione sezione]** a sinistra e rilasciarlo nell&#39;area del modulo.
   * (Facoltativo) Seleziona **[!UICONTROL Etichetta campo]** per selezionare il componente.
   * (Facoltativo) Nella parte destra della pagina, nella scheda Impostazioni, nel campo di testo Etichetta campo, immetti `YouTube Privacy`.
   * Seleziona la **[!UICONTROL Genera modulo]** , quindi trascina il componente con l’etichetta **[!UICONTROL Testo con più valori]** e rilascialo sotto il **[!UICONTROL Privacy di YouTube]** intestazione creata.

   * Per selezionare il componente, seleziona **[!UICONTROL Etichetta campo]**.
   * Nella parte destra della pagina, nella scheda Impostazioni, incolla i valori di pubblicazione di YouTube (valore Etichetta campo e Mappa su valore proprietà) copiati in precedenza nei rispettivi campi del modulo. Incolla il valore Scelte nel campo Valore predefinito.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.
1. Applica il profilo di metadati Pubblicazione YouTube alle cartelle in cui stai per caricare i video. Devi avere sia il Profilo metadati che il Profilo video impostati.

   Consulta le sezioni [Profili di metadati](/help/assets/metadata-profiles.md) e [Profili video](/help/assets/dynamic-media/video-profiles.md).

### Pubblicare video sul canale YouTube {#publishing-videos-to-your-youtube-channel}

Ora associ alle risorse video i tag aggiunti in precedenza. Questo consente agli Experienci Manager di sapere quali risorse pubblicare nel canale YouTube.

>[!NOTE]
>
>La pubblicazione immediata non viene automaticamente pubblicata in YouTube. Quando si imposta Dynamic Media, è possibile scegliere tra due opzioni di pubblicazione: **[!UICONTROL Immediatamente]** o **[!UICONTROL All’attivazione]**.
>
>**[!UICONTROL Pubblica immediatamente]** significa che la risorsa caricata, dopo essere stata sincronizzata con IPS, viene pubblicata automaticamente nel sistema di consegna. Anche se questo è vero per Dynamic Medie, non lo è per YouTube. Per pubblicare in YouTube, devi utilizzare l’Autore Experience Manager.

>[!NOTE]
>
Per pubblicare contenuti da YouTube, Experience Manager utilizza **[!UICONTROL Pubblica su YouTube]** che consente di monitorare l’avanzamento e visualizzare eventuali informazioni sull’errore.
>
Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
Per informazioni più dettagliate sullo stato di avanzamento, puoi monitorare il registro di YouTube in replica. Tenere presente, tuttavia, che tale monitoraggio richiede l&#39;accesso dell&#39;amministratore.

**Per pubblicare video sul canale YouTube:**

1. Ad Experience Manager, individua la risorsa video da pubblicare sul tuo canale YouTube.
1. Seleziona la risorsa video (il set di video adattivi).
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda Base, seleziona l’intestazione Metadati **[!UICONTROL Apri finestra di dialogo per selezione]** a destra del campo Tag.
1. Nella pagina Seleziona tag passare ai tag che si desidera utilizzare e quindi selezionare uno o più tag.

   Ricorda che i tag devono essere associati al canale YouTube.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.
1. Nell’angolo superiore destro della pagina delle proprietà del video, seleziona **[!UICONTROL Salva e chiudi]**.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

   Vedi anche [Utilizzare Gestione delle pubblicazioni con Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   Facoltativamente, puoi verificare il video pubblicato sul tuo canale YouTube.

### (Facoltativo) Verifica il video pubblicato su YouTube {#optional-verifying-the-published-video-on-youtube}

Facoltativamente, puoi monitorare lo stato della pubblicazione (o dell’annullamento della pubblicazione) in YouTube.

Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

I tempi di pubblicazione possono variare notevolmente a seconda di numerosi fattori, tra cui il formato del video sorgente principale, la dimensione del file e il traffico di caricamento. Il processo di pubblicazione può richiedere da pochi minuti a diverse ore. Inoltre, i formati a risoluzione più elevata vengono riprodotti molto più lentamente. Ad esempio, le modalità 720p e 1080p richiedono più tempo rispetto alla modalità 480p.

Dopo otto ore, se ricevi ancora un messaggio di stato che indica **[!UICONTROL Caricato (elaborazione, attendere)]**, prova a rimuovere il video dal sito e a caricarlo di nuovo.

### Collegare gli URL di YouTube all’applicazione web {#linking-youtube-urls-to-your-web-application}

Dopo la pubblicazione del video, puoi ottenere una stringa URL di YouTube generata da Dynamic Medie. Quando copi l’URL di YouTube, questo viene inserito negli Appunti, in modo da poterlo incollare nelle pagine del sito web o dell’applicazione.

>[!NOTE]
>
L’URL di YouTube non è disponibile per la copia finché non hai pubblicato la risorsa video in YouTube.

Per collegare gli URL di YouTube alla tua applicazione web:

1. Accedi a *YouTube pubblicato* risorsa video di cui desideri copiare l’URL, quindi selezionala.

   Gli URL di YouTube sono disponibili solo per la copia *dopo* hai prima *pubblicato* le risorse video in YouTube.

1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Avanzate]** scheda.
1. Nell’elenco URL di YouTube Publishing, seleziona e copia il testo dell’URL nel browser Web per visualizzare in anteprima la risorsa o aggiungerlo alla pagina di contenuto Web, sotto l’intestazione Pubblicazione di YouTube.

### Annullare la pubblicazione dei video per rimuoverli da YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Quando annulli la pubblicazione di una risorsa video in Experience Manager, il video viene rimosso da YouTube.

>[!CAUTION]
>
Se rimuovi un video direttamente da YouTube, Experience Manager non ne è a conoscenza e continua a comportarsi come se il video fosse ancora pubblicato in YouTube. Per Experience Manager, annulla sempre la pubblicazione di una risorsa video da YouTube.

>[!NOTE]
>
Per rimuovere il contenuto da YouTube, Experience Manager utilizza **[!UICONTROL Annulla pubblicazione da YouTube]** che consente di monitorare l’avanzamento e visualizzare eventuali informazioni sull’errore.
>
Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Per annullare la pubblicazione dei video e rimuoverli da YouTube:**

1. Passa alle risorse video di cui vuoi annullare la pubblicazione dal tuo canale YouTube.
1. In modalità di selezione delle risorse, seleziona una o più risorse video pubblicate.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Se necessario, seleziona l’icona dei tre punti (`. . .`) sulla barra degli strumenti per visualizzare **[!UICONTROL Gestisci pubblicazione]**.
1. Nella pagina Gestisci pubblicazione, seleziona **[!UICONTROL Annulla pubblicazione]**.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Successivo]**.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Annulla pubblicazione]**.

## Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Quando carichi un nuovo video in una cartella a cui è applicata la codifica video o, pubblichi il video in YouTube, monitori l’avanzamento (o l’errore) della codifica video/pubblicazione su Youtube. L’avanzamento effettivo della pubblicazione in YouTube è disponibile solo tramite i registri. Ma se fallisce o ha successo, viene elencato in altri modi descritti nella procedura seguente. Inoltre, ricevi notifiche e-mail quando un flusso di lavoro o una codifica video di YouTube Publish viene completato o interrotto.

### Monitorare l’avanzamento {#monitoring-progress}

Puoi monitorare l’avanzamento, inclusa la codifica non riuscita/pubblicazione YouTube.

1. Visualizza l’avanzamento della codifica video nella cartella delle risorse:

   * Nella vista a schede, l’avanzamento della codifica video viene visualizzato sulla risorsa in percentuale. In caso di errore, queste informazioni vengono visualizzate anche sulla risorsa.

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * Nella vista a elenco, l’avanzamento della codifica video viene visualizzato nel **[!UICONTROL Stato elaborazione]** colonna. In caso di errore, il messaggio viene visualizzato nella stessa colonna.

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   Questa colonna non viene visualizzata per impostazione predefinita. Per abilitare la colonna, seleziona **[!UICONTROL Impostazioni vista]** dal menu a discesa viste e aggiungi **[!UICONTROL Stato elaborazione]** e seleziona **[!UICONTROL Aggiorna]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Visualizza l’avanzamento nei dettagli della risorsa. Quando selezioni una risorsa, apri il menu a discesa e seleziona **[!UICONTROL Timeline]**. Per limitarla alle attività del flusso di lavoro come la codifica o la pubblicazione YouTube, seleziona **[!UICONTROL Flussi di lavoro]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   Tutte le informazioni sul flusso di lavoro, ad esempio la codifica, vengono visualizzate nella timeline. Per YouTube Publish, la timeline del flusso di lavoro include anche il nome del canale YouTube e l’URL del video YouTube. Inoltre, una volta completata la pubblicazione, nella timeline del flusso di lavoro vengono visualizzate tutte le notifiche di errore.

   >[!NOTE]
   >
   Potrebbero essere necessari tempi lunghi per la registrazione dei messaggi di errore/guasto, a causa della presenza di più configurazioni di workflow **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** da [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), ad esempio:
   >
   * Configurazione coda processi Apache Sling
   * Adobe Granite Workflow External Process Job Handler
   * Coda di timeout del flusso di lavoro Granite
   >
   È possibile regolare **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** proprietà in queste configurazioni.

1. Per i flussi di lavoro in corso, vedi l’opzione Istanze flusso di lavoro accedendo a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Istanze]**.

   >[!NOTE]
   >
   Sono necessari diritti di amministratore per accedere a **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   Seleziona l’istanza e seleziona **[!UICONTROL Cronologia elementi aperti]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   Dall’area Istanze flusso di lavoro, puoi anche sospendere, terminare o rinominare i flussi di lavoro. Consulta [Amministrare i flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md) per ulteriori informazioni.

1. Per i processi non riusciti, consulta l’opzione Errori di flusso di lavoro, accessibile da **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Errori]**. In **[!UICONTROL Errore flusso di lavoro]** sono elencate tutte le attività del flusso di lavoro che hanno generato errori.

   >[!NOTE]
   >
   Sono necessari diritti di amministratore per accedere a **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   Potrebbero essere necessari tempi lunghi per la registrazione del messaggio di errore, a causa della presenza di più configurazioni di workflow in **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** da [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), ad esempio:
   >
   * Configurazione coda processi Apache Sling
   * Adobe Granite Workflow External Process Job Handler
   * Coda di timeout del flusso di lavoro Granite
   >
   È possibile regolare **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** proprietà in queste configurazioni.

1. Per i flussi di lavoro completati, consulta Archivio flussi di lavoro, accessibile da **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Archivio]**. **[!UICONTROL Archivio flussi di lavoro]** elenca tutte le attività del flusso di lavoro che sono state completate.

   >[!NOTE]
   >
   Sono necessari diritti di amministratore per accedere a **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. Ricevi notifiche e-mail sui processi del flusso di lavoro interrotti o non riusciti. Queste notifiche e-mail possono essere configurate da un amministratore. Consulta [Configurare le notifiche e-mail](#configuring-e-mail-notifications).

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

## Trascodifica tramite profilo di elaborazione {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] consente di eseguire la transcodifica di base dei file video MP4 utilizzando Profili di elaborazione. Questa funzionalità consente non solo di caricare ma anche di visualizzare in anteprima e ridimensionare un file video MP4.

![Creare un profilo di elaborazione per la transcodifica video in [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Profilo di elaborazione per la transcodifica video in [!DNL Experience Manager].*

Se fornisci solo la larghezza o solo l’altezza e lasci vuoto l’altro campo, le rappresentazioni manterranno le proporzioni. È disponibile il codec video H.264 per la transcodifica.

Per elaborare le risorse utilizzando un profilo di elaborazione, aggiungi un profilo a una cartella. Consulta [utilizzare i profili di elaborazione per elaborare le risorse](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Annotare risorse video {#annotate-video-assets}

Puoi aggiungere annotazioni alle risorse video. Durante l’annotazione dei video, il lettore si interrompe per consentire l’annotazione su un fotogramma. Per ulteriori informazioni, consulta [gestione delle risorse video](manage-video-assets.md).

>[!NOTE]
>
Il formato video MXF non è ancora supportato con le annotazioni delle risorse video.

1. Dalla sezione [!DNL Assets] console, seleziona **[!UICONTROL Modifica]** nella scheda delle risorse per visualizzare la pagina dettagli risorsa.
1. Per riprodurre il video, fai clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fai clic su **[!UICONTROL Annota]**. Nel video viene aggiunta un’annotazione in corrispondenza del momento specifico (fotogramma). Durante l&#39;annotazione, è possibile disegnare sull&#39;area di lavoro e includere un commento con il disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata di annotazione, fare clic su **[!UICONTROL Chiudi]**.
1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.
1. Per visualizzarlo nella timeline, fai clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fai clic su **[!UICONTROL Elimina]**.

## Best practice e limitazioni {#tips-limitations}

* Senza [!DNL Dynamic Media] licenza, è possibile elaborare solo file MP4 utilizzando profili di elaborazione.
* Quando si transcodificano file MP4 utilizzando Profili di elaborazione, si applicano le seguenti linee guida e limitazioni:

   * I file Apple ProRes possono essere transcodificati solo con una risoluzione massima di 1080p.
   * Se il file di origine ha un bitrate > 200 Mbps, è possibile eseguire la trascodifica solo con una risoluzione massima di 1080p.
   * Se la frequenza di fotogrammi di origine è >=60 fps, la dimensione massima del file di origine utilizzabile è,

      * 400 MB per la transcodifica 4k.
      * 800 MB per la transcodifica 1080p.
      * 8 GB per transcodifica 720p.

   * La dimensione massima del file trascodificabile a una risoluzione 4k è di 2,55 GB di file MP4 con risoluzione 4k, bitrate di 12 Mbps e 23 fps.

  **Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
* [Documentazione video di Dynamic Medie](/help/assets/dynamic-media/video.md).
* [Ulteriori informazioni su utilizzo, tipi e configurazione dei profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).
