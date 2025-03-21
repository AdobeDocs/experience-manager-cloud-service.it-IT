---
title: Invalidare la cache CDN (Content Delivery Network) tramite Dynamic Media Classic
description: Scopri come annullare la validità della rete CDN (Content Delivery Network) per aggiornare rapidamente le risorse distribuite da Dynamic Media, invece di attendere la scadenza della cache.
contentOwner: Rick Brough
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 17%

---

# Invalidare la cache CDN tramite Dynamic Media Classic {#invalidating-your-cdn-cached-content}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Le risorse Dynamic Media vengono memorizzate nella cache dalla rete CDN (Content Delivery Network) per velocizzarne la distribuzione. Tuttavia, quando apporti aggiornamenti a una risorsa, vuoi che tali modifiche diventino effettive immediatamente. L’annullamento della validità del contenuto CDN memorizzato nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, invece di attendere la scadenza della cache.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

>[!IMPORTANT]
>
>Questi passaggi si applicano solo a Dynamic Media in Adobe Experience Manager 6.5, Service Pack 5 o versioni precedenti. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Per annullare la validità della cache CDN tramite Dynamic Media Classic:**

1. Apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di queste informazioni, contatta l’Assistenza clienti.

1. Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**.
1. Nella pagina Impostazioni generali applicazione, sotto l&#39;intestazione del gruppo Server, individuare la casella di testo **[!UICONTROL Modello di annullamento validità CDN]**.

1. Specifica il modello utilizzato per annullare la validità della cache CDN (Content Delivery Network).

   Si supponga, ad esempio, di immettere un URL immagine (inclusi predefiniti immagine o modificatori) che fa riferimento a `<ID>`, anziché un ID immagine specifico come nell&#39;esempio seguente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se il modello contiene solo `<ID>`, Dynamic Media compila `https://<server>/is/image` dove `<server>` è il nome del server di pubblicazione definito nelle impostazioni generali e &lt;ID> è la risorsa selezionata per l&#39;annullamento della validità.

1. Nell&#39;angolo inferiore destro della pagina, seleziona **[!UICONTROL Chiudi]**.
1. Nell&#39;interfaccia utente di Dynamic Media Classic (Scene7), seleziona una o più risorse, quindi vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**. Viene visualizzato un elenco di uno o più URL generati dal modello creato e dalle risorse selezionate. Utilizza l’URL del server elencato in &quot;Published Server Name&quot; (Nome server pubblicato) nelle impostazioni generali dell’applicazione.

   Ad esempio, con il modello di annullamento della validità CDN impostato nel passaggio precedente, supponi di aver selezionato una singola immagine della risorsa immagine denominata `Backpack_B`. Quando si passa a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, nell&#39;interfaccia utente di annullamento validità CDN viene generato il seguente URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Nella casella di riepilogo URL selezionare **[!UICONTROL Continua]** per cancellare la cache per ogni URL specifico. Puoi modificare un URL oppure aggiungerlo digitandolo o incollandolo nella casella di riepilogo URL; non è necessario impostare in precedenza il modello di annullamento validità CDN.

   Dopo aver selezionato **[!UICONTROL Continua]**, viene visualizzato un indicatore che fornisce una stima del tempo necessario per cancellare la cache.

   Se hai selezionato più risorse e poi sei passato a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, a ciascuna risorsa viene fatto riferimento nell&#39;**[!UICONTROL URL modello]** salvato. Puoi quindi definire un **[!UICONTROL Modello di annullamento validità CDN]** facendo riferimento a ciascun predefinito dell&#39;URL immagine a cui viene fatto riferimento nel tuo sito Web, ad esempio i dettagli del prodotto e i risultati della ricerca. Quindi, quando selezioni una o più immagini della cache di cui annullare la validità, gli URL compilano automaticamente l’interfaccia.

   >[!NOTE]
   >
   >Quando selezioni le risorse e poi vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, Dynamic Media utilizza un modello CDN non valido per creare automaticamente gli URL da annullare la validità dalla CDN. Se nella casella di testo **[!UICONTROL Modello di annullamento validità CDN]** non è presente alcun elemento, viene visualizzato un elenco URL vuoto. La memorizzazione nella cache della rete CDN non è basata su risorse, bensì su URL. Pertanto, è necessario conoscere gli URL completi presenti sul tuo sito web. Dopo aver determinato questi URL, puoi aggiungerli alla casella di testo **[!UICONTROL Invalidate CDN Template (Annulla validità modello CDN)]** descritta nei passaggi precedenti. A questo punto puoi selezionare queste risorse e annullare la validità degli URL, tutto in un unico passaggio.
   >
   >Un&#39;altra opzione consiste nell&#39;aggiungere URL completi all&#39;elenco **[!UICONTROL Annulla validità CDN]**. Se si segue questo approccio, non è necessario selezionare le risorse in Dynamic Media Classic prima di passare all&#39;opzione **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**.
