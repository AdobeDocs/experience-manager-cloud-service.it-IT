---
title: Come configurare una pagina di reindirizzamento?
description: Scopri come gli utenti possono essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 6%

---

# Configurazione della pagina di reindirizzamento {#configuring-redirect-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Gli autori dei moduli possono configurare una pagina per ogni modulo, alla quale gli utenti vengono reindirizzati dopo l&#39;invio di un modulo.

1. In modalità di modifica, seleziona un componente, quindi fai clic su ![livello campo](assets/select_parent_icon.svg) > **[!UICONTROL Contenitore modulo adattivo]**, quindi fai clic su ![cmppr](assets/configure-icon.svg).

1. Nella barra laterale fare clic su **[!UICONTROL Invio]**.

1. Fornisci l&#39;URL della pagina di reindirizzamento in **[!UICONTROL URL/percorso di reindirizzamento]** nella sezione **[!UICONTROL Invio]**.
1. Facoltativamente, in Azione di invio, per l’azione Invia a endpoint REST, puoi configurare il parametro da passare alla pagina di reindirizzamento.

   ![Configurazione pagina di reindirizzamento](assets/redirect-url.png)

   Configurazione pagina di reindirizzamento

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, vengono passati `status` e `owner` parametri. Oltre a questi due parametri, vengono passati alcuni parametri aggiuntivi per le seguenti azioni di invio:

* **[!UICONTROL Invia all&#39;endpoint REST]**: i parametri aggiunti per la mappatura interna al campo al parametro vengono passati. Parametri `status` e `owner` non passati in questa azione di invio. Per ulteriori informazioni, vedere [Configurazione dell&#39;azione di invio Invia all&#39;endpoint REST](configuring-submit-actions.md).

>[!MORELIKETHIS]
>
>* [Configurare una pagina di reindirizzamento o inviare un messaggio di ringraziamento](/help/forms/configure-redirect-page-or-thank-you-message.md)
