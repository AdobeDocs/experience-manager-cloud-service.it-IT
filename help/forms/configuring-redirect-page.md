---
title: Come si configura una pagina di reindirizzamento?
description: Scopri come reindirizzare gli utenti a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
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

Gli autori dei moduli possono configurare una pagina per ciascun modulo, a cui verranno reindirizzati gli utenti dopo l’invio.

1. In modalità di modifica, seleziona un componente, quindi fai clic su ![a livello di campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenitore di moduli adattivi]**, quindi fai clic su ![cmppr](assets/configure-icon.svg).

1. Nella barra laterale, fai clic su **[!UICONTROL Invio]**.

1. Fornisci l&#39;URL della pagina di reindirizzamento in **[!UICONTROL URL/percorso di reindirizzamento]** in **[!UICONTROL Invio]** sezione .
1. Facoltativamente, in Azione di invio per l’azione Invia a endpoint REST è possibile configurare il parametro da passare alla pagina di reindirizzamento.

   ![Reindirizza la configurazione della pagina](assets/redirect-url.png)

   Reindirizza la configurazione della pagina

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, `status` e `owner` vengono passati i parametri . Oltre a questi due parametri, alcuni parametri aggiuntivi vengono passati per le seguenti azioni di invio:

* **[!UICONTROL Invia all’endpoint REST]**: I parametri aggiunti per la mappatura in-field ai parametri vengono passati. `status` e `owner` i parametri non vengono passati in questa azione di invio. Per ulteriori informazioni, consulta [Configurazione dell’azione di invio all’endpoint REST](configuring-submit-actions.md).
