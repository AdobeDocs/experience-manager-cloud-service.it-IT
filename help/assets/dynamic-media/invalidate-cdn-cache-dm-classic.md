---
title: Annullare la validità della cache CDN (Content Delivery Network) tramite Dynamic Media Classic
description: Scopri come annullare la validità della rete CDN (Content Delivery Network) memorizzata nella cache per consentirti di aggiornare rapidamente le risorse consegnate da Dynamic Media, anziché attendere la scadenza della cache.
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: cf7d844acb0158b543d575368e35cd1c2fc72fba
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 15%

---

# Invalidare la cache CDN tramite Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Le risorse Dynamic Media sono memorizzate nella cache della rete CDN (Content Delivery Network) per velocizzarne la distribuzione. Tuttavia, quando apporti aggiornamenti a una risorsa, vuoi che tali modifiche abbiano effetto immediato. L’annullamento della validità del contenuto CDN memorizzato nella cache consente di aggiornare rapidamente le risorse consegnate da Dynamic Media, anziché attendere la scadenza della cache.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

>[!IMPORTANT]
>
>Questi passaggi si applicano solo a Dynamic Media in Adobe Experience Manager 6.5, Service Pack 5 o versioni precedenti. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Per annullare la validità della cache CDN tramite Dynamic Media Classic:**

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti.

1. Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.
1. Nella pagina Impostazioni generali applicazione, sotto l&#39;intestazione del gruppo Server, individuare il **[!UICONTROL Modello di annullamento validità CDN]** casella di testo.

1. Specifica il modello utilizzato per annullare la validità della cache CDN (Content Delivery Network).

   Ad esempio, supponiamo di inserire un URL immagine (inclusi predefiniti immagine o modificatori) che fa riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se il modello contiene solo `<ID>`, quindi Dynamic Media compila `https://<server>/is/image` dove `<server>` è il nome del server di pubblicazione definito in Impostazioni generali e &lt;id> è la risorsa selezionata per l’annullamento della validità.

1. Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Chiudi]**.
1. Nell’interfaccia utente di Dynamic Media Classic (Scene7), seleziona una o più risorse, quindi vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**. Viene visualizzato un elenco di uno o più URL generati dal modello creato e dalle risorse selezionate. Utilizza l&#39;URL del server elencato in &quot;Nome server pubblicato&quot; nelle Impostazioni generali dell&#39;applicazione.

   Ad esempio, con il modello di annullamento validità CDN impostato nel passaggio precedente, supponi di aver selezionato una singola immagine di risorsa immagine denominata `Backpack_B`. Quando vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, si traduce nel seguente URL generato nell’interfaccia utente di annullamento validità CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Nella casella di riepilogo URL, seleziona **[!UICONTROL Continua]** cancellare la cache per ogni URL specifico. È possibile modificare un URL o aggiungere un URL digitandolo o incollandolo nella casella di riepilogo URL; non è necessario impostare prima il modello di annullamento validità CDN.

   Dopo aver selezionato **[!UICONTROL Continua]**, viene visualizzato un indicatore che fornisce una stima del tempo necessario per cancellare la cache.

   Se hai selezionato più risorse, vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, a ogni risorsa viene fatto riferimento nel **[!UICONTROL URL modello]**. Pertanto, puoi definire un **[!UICONTROL Modello di annullamento validità CDN]** facendo riferimento a ogni predefinito immagine URL a cui viene fatto riferimento sul tuo sito web, ad esempio dettagli del prodotto e risultati della ricerca. Quindi, quando selezioni una o più immagini della cache di cui annullare la validità, gli URL compilano automaticamente l’interfaccia.

   >[!NOTE]
   >
   >Quando selezioni le risorse, vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, Dynamic Media utilizza un modello CDN non valido per creare automaticamente URL da annullare la validità dalla CDN. Se nella casella di testo **[!UICONTROL Modello di annullamento validità CDN]** non è presente alcun elemento, viene visualizzato un elenco URL vuoto. La memorizzazione nella cache della rete CDN non è basata su risorse, bensì su URL. Pertanto, è necessario conoscere gli URL completi presenti sul tuo sito web. Dopo aver determinato questi URL, puoi aggiungerli alla casella di testo **[!UICONTROL Invalidate CDN Template (Annulla validità modello CDN)]** descritta nei passaggi precedenti. A questo punto puoi selezionare queste risorse e annullare la validità degli URL, tutto in un unico passaggio.
   >
   >Un’altra opzione consiste nell’aggiungere URL completi al **[!UICONTROL Annulla validità CDN]** elenco. Se segui questo approccio, non è necessario selezionare le risorse in Dynamic Media Classic prima di passare alla **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]** opzione .
