---
title: Scaricare risorse da AEM
description: Scoprite come scaricare risorse da AEM e abilitare o disabilitare la funzionalità di download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12575cd2f046d3a382786811dd28fec8df3be8bd
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 4%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Potete scaricare le risorse incluse le rappresentazioni statiche e dinamiche. In alternativa, potete inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate vengono raggruppate in un file ZIP. Il file ZIP compresso ha una dimensione massima di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>I destinatari delle e-mail devono essere membri del `dam-users` gruppo per accedere al collegamento di download ZIP nel messaggio e-mail. Per poter scaricare le risorse, i membri devono disporre delle autorizzazioni necessarie per avviare flussi di lavoro che attivano il download delle risorse.

Impossibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set file multimediali diversi e Set caroselli.

**Per scaricare le risorse,**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Navigation]** (Compass icon).
1. Nella pagina di navigazione, tocca **[!UICONTROL Risorse > File]**.
1. Individuate una cartella contenente le risorse da scaricare.
1. Selezionate la cartella o selezionate una o più risorse all’interno della cartella.
1. Nella barra degli strumenti, toccate **[!UICONTROL Scarica]**.

   ![Opzioni disponibili durante il download delle risorse da  Experience Manager Assets](/help/assets/assets/asset-download1.png)

   *Opzioni della finestra di dialogo Download.*

1. Nella finestra di dialogo Download, selezionate le opzioni di download desiderate.

   | Opzione di download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Selezionate questa opzione per includere tutte le risorse scaricate, incluse quelle nelle cartelle figlie nidificate sotto la cartella padre della risorsa in una cartella sul computer locale. Se questa opzione *non* è selezionata, per impostazione predefinita la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella del computer locale. |
   | **[!UICONTROL E-mail]** | Selezionate questa opzione per far sì che venga inviata una notifica e-mail al destinatario. I modelli standard per le e-mail sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Potete memorizzare i modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Selezionate questa opzione per scaricare la risorsa nel modulo originale senza alcuna rappresentazione.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale contiene risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione, potete selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
   | **[!UICONTROL Ritagli avanzati]** | Selezionate questa opzione per scaricare da AEM tutte le rappresentazioni di ritaglio avanzato della risorsa selezionata. Viene creato e scaricato nel computer locale un file zip con le rappresentazioni SmartCrop. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Selezionate questa opzione per generare una serie di rappresentazioni alternative in tempo reale. Quando selezionate questa opzione, potete anche selezionare i rendering che desiderate creare in modo dinamico selezionando dall’elenco Predefiniti [](/help/assets/dynamic-media/image-presets.md) immagine. <br>Potete inoltre selezionare le dimensioni e l’unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine opzionale, ad esempio l’inversione dell’immagine. L’opzione è disponibile solo se è stata [!DNL Dynamic Media] attivata. |

1. Nella finestra di dialogo, toccate **[!UICONTROL Scarica]**.


## Abilita servlet download risorse {#enable-asset-download-servlet}

Il servlet predefinito in AEM consente agli utenti autenticati di emettere richieste di download simultanei di grandi dimensioni per la creazione di file ZIP di risorse visibili agli utenti che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, il componente `AssetDownloadServlet` OSGi è disabilitato per impostazione predefinita per le istanze di pubblicazione.

Per consentire il download delle risorse da DAM, ad esempio quando si utilizza un sistema simile a Asset Share Commons o ad altre implementazioni di tipo portale, è necessario abilitare manualmente il servlet tramite una configurazione OSGi. Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Create una cartella con una convenzione di denominazione per la modalità di esecuzione della pubblicazione, vale a dire `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Nella cartella di configurazione, create un nuovo file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Compilate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con le seguenti opzioni. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattivazione del servlet di download delle risorse {#disable-asset-download-servlet}

È `Asset Download Servlet` possibile disattivare le istanze di un AEM Publish aggiornando la configurazione del dispatcher per bloccare qualsiasi richiesta di download di risorse. Il servlet può anche essere disattivato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione dispatcher, modifica la `dispatcher.any` configurazione e aggiungi una nuova regola alla sezione [](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtro.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Scaricare risorse protette DRM](drm.md)
>* [Scaricare risorse dall’app desktop AEM su Windows o Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Scaricare risorse tramite il collegamento Adobe Assets dall&#39;interno delle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)

