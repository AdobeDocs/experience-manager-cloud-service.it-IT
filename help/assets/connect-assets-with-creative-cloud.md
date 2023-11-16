---
title: Connettere AEM Assets a Creative Cloud
description: Scopri come configurare e collegare AEM Assets a Creative Cloud. Connettiti a una licenza Creative Cloud fornita a un’altra organizzazione IMS per utilizzare facilmente le integrazioni Creative Cloud più recenti in AEM Assets, incluse le librerie Express e Creative Cloud.
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Connettere AEM Assets a Creative Cloud  {#cross-org-entitlements}

Experience Manager Assets è in grado di connettersi a una licenza Creative Cloud fornita a un’altra organizzazione IMS per utilizzare facilmente le più recenti integrazioni Creative Cloud in AEM Assets, incluse le librerie Express e Creative Cloud.

Se per i prodotti Creative Cloud e AEM Assets è stato eseguito il provisioning per organizzazioni IMS separate, è possibile connettersi a un’organizzazione Creative Cloud diversa per eseguire flussi di lavoro integrati tra le due soluzioni.

## Prerequisiti {#prerequisites}

* Diritti di amministratore su Experience Manager Assets

* Diritto attivo a Creative Cloud per lo stesso ID utente utilizzato in Creative Cloud e Experience Manager. I diritti agli ID personali e federati con lo stesso indirizzo e-mail vengono trattati come ID utente diversi.

## Connettersi a una nuova organizzazione Creative Cloud {#connect-to-creative-cloud-org}

Per connettersi a una nuova organizzazione Creative Cloud, effettuare le seguenti operazioni:

1. Accedi a **[!UICONTROL Impostazioni]** > **[!UICONTROL Creative Cloud]**.

1. Seleziona la nuova organizzazione Creative Cloud utilizzando **[!UICONTROL Seleziona nuovo ID organizzazione Creative Cloud]** elenco a discesa. Nell&#39;elenco vengono visualizzate tutte le organizzazioni a cui si ha accesso. Selezionare l&#39;organizzazione con diritti di Creative Cloud attivi.

1. Clic **[!UICONTROL Cambiare organizzazione]** per passare alla nuova organizzazione.

   ![Diritti per più organizzazioni](assets/cross-org-entitlements.png)

## Limitazioni {#limitations}

* Puoi collegare AEM Assets a un’organizzazione Creative Cloud alla volta. La connessione a più organizzazioni Creative Cloud alla volta non è supportata.

* L’organizzazione Creative Cloud a cui ti connetti in AEM Assets è applicabile a tutti gli utenti all’interno dell’organizzazione.

