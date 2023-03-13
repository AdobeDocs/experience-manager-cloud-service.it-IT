---
title: Come configurare una pagina di reindirizzamento?
description: Scopri come gli utenti possono essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Configurazione della pagina di reindirizzamento {#configuring-redirect-page}

Gli autori dei moduli possono configurare una pagina per ogni modulo, alla quale gli utenti vengono reindirizzati dopo l&#39;invio di un modulo.

1. In modalità di modifica, seleziona un componente, quindi fai clic su ![a livello di campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenitore modulo adattivo]** e quindi fare clic su ![cmppr](assets/configure-icon.svg).

1. Nella barra laterale, fai clic su **[!UICONTROL Invio]**.

1. Immetti l’URL della pagina di reindirizzamento in **[!UICONTROL URL/percorso di reindirizzamento]** nel **[!UICONTROL Invio]** sezione.
1. Facoltativamente, in Azione di invio, per l’azione Invia a endpoint REST, puoi configurare il parametro da passare alla pagina di reindirizzamento.

   ![Configurazione pagina di reindirizzamento](assets/redirect-url.png)

   Configurazione pagina di reindirizzamento

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, `status` e `owner` i parametri vengono passati. Oltre a questi due parametri, vengono passati alcuni parametri aggiuntivi per le seguenti azioni di invio:

* **[!UICONTROL Invia all’endpoint REST]**: vengono passati i parametri aggiunti per la mappatura in-field ai parametri. `status` e `owner` I parametri non vengono passati in questa azione di invio. Per ulteriori informazioni, consulta [Configurazione dell’azione di invio Invia all’endpoint REST](configuring-submit-actions.md).
