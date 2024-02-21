---
title: Configura pagina di ringraziamento per EDS Forms
description: Configura pagina di ringraziamento per EDS Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 1%

---


# Configurare i reindirizzamenti dei blocchi di modulo

Puoi configurare il blocco di modulo in modo che venga reindirizzato a una pagina diversa del tuo sito web invece della pagina predefinita &quot;grazie&quot;. Per impostare un&#39;altra pagina come destinazione di reindirizzamento

1. Apri `[EDS Project]/blocks/form/form.js` file per la modifica.

   ![codice per il nodo grazie](/help/edge/assets/change-thankyou-node.png)

1. Modificare il `thankyou` nodo nella riga seguente al nodo desiderato:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Ad esempio:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > Se non è già stata creata, assicurati che nella cartella dei progetti del servizio di consegna Edge in Microsoft SharePoint o Google Sheets venga creata una pagina del documento con lo stesso nome.


1. Procedi con l’archiviazione della cartella &quot;form.js&quot; aggiornata e dei relativi file sottostanti nel progetto del servizio di consegna Edge su GitHub. Questo aggiornamento assicura che il modulo ora venga reindirizzato al nodo aggiornato come specificato.
