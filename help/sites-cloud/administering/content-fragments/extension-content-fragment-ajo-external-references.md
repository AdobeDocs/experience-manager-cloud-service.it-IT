---
title: Utilizzo dell’estensione Content Fragments AJO External References
description: Scopri l’estensione per riferimenti esterni AJO per frammenti di contenuto
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 79c90e6b-91da-4f5a-ac96-a98ef7f8d4cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# Estensione dei riferimenti esterni AJO per frammenti di contenuto {#content-fragment-external-references-extension}

Per visualizzare in anteprima le esperienze da AEM su un altro prodotto Adobe, puoi abilitare l’estensione dell’interfaccia utente:

* **Riferimenti esterni AJO**

L’estensione AJO External References funziona recuperando i riferimenti al frammento di contenuto da tutte le organizzazioni e sandbox associate a tag predefiniti. L&#39;estensione mostra quindi i dettagli.

Ad esempio, per un’integrazione con Adobe Journey Optimizer (AJO) i dettagli dipendono dal fatto che il riferimento sia una campagna, un Percorso o un modello.

>[!NOTE]
>
>Per informazioni dettagliate su come abilitare l&#39;estensione, vedere [Extension Manager in AEM Experience Manager.](https://developer.adobe.com/uix/docs/extension-manager/)

Ad esempio, per utilizzare l’estensione con AJO:

>[!NOTE]
>
>Vedi anche [Integrazione AJO](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/integrations/aem-fragments).

1. Apri [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

1. Passa al frammento di contenuto, il frammento creato e utilizzato nei vari canali di AJO.

1. Apri il frammento di contenuto nell&#39;[editor](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment).

1. L’estensione AJO External References è disponibile come scheda nel pannello di destra. Seleziona la scheda per aprire l&#39;estensione:

   ![Estensione riferimenti esterni AJO](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   Una volta selezionato un tipo di riferimento, l&#39;estensione visualizza i riferimenti esterni corrispondenti sotto forma di tabella con le colonne:

   * **Nome**: il nome del riferimento in cui viene utilizzato il frammento di contenuto
   * **Anteprima** seleziona questo collegamento per avviare l&#39;anteprima
   * **Stato**: lo stato del riferimento

1. È possibile selezionare il **Tipo di riferimento** dal menu a discesa per passare da un tipo di riferimento all&#39;altro:

   * **Campagna**
      * Visualizza un elenco di tutte le campagne con collegamenti al frammento di contenuto corrente.
      * Puoi quindi visualizzare in anteprima una campagna selezionata.
      * Predefiniti
   * **Percorso**
      * Visualizza il Percorso più recente.
      * È quindi possibile selezionare e visualizzare in anteprima un Percorso selezionato.
   * **Modello**
      * Visualizza i modelli relativi al frammento di contenuto.
      * È quindi possibile selezionare e visualizzare in anteprima un modello selezionato.
