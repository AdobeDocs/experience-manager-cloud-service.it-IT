---
title: Connetti a Microsoft Translator
description: Scopri come collegare AEM a Microsoft Translator predefinito per automatizzare il flusso di lavoro di traduzione.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
solution: Experience Manager Sites
source-git-commit: 2314ad30ea31b49d832ce0fdf729420e0ee70e0c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 65%

---

# Connetti a Microsoft Translator {#connecting-to-microsoft-translator}

AEM fornisce un connettore integrato per [Microsoft Translator](https://www.microsoft.com/it-it/translator/business/) per tradurre il contenuto o le risorse della pagina. Dopo aver ottenuto una licenza da Microsoft per utilizzare Microsoft Translator, configura il connettore seguendo le istruzioni riportate in questa pagina.

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta il [Percorso di traduzione Sites](/help/journey-sites/translation/overview.md), per una guida attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideali per chi non ha esperienza di AEM o di traduzione.

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Il nome visualizzato per il servizio di traduzione |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall&#39;utente, l&#39;attribuzione visualizzata accanto al testo tradotto, ad esempio `Translations by Microsoft` |
| ID area di lavoro | (Facoltativo) L’ID del motore di Microsoft Translator personalizzato da utilizzare |
| Chiave di sottoscrizione | La chiave di abbonamento a Microsoft per Microsoft Translator |

La procedura seguente crea una configurazione di Microsoft Translator.

1. Nel pannello di navigazione [,](/help/sites-cloud/authoring/basic-handling.md#first-steps) seleziona **Strumenti** > **Cloud Service** > **Cloud Service di traduzione**.
1. Passa alla posizione in cui desideri creare la configurazione. Normalmente si trova nel sito principale oppure può essere una configurazione globale predefinita.
1. Seleziona il pulante **Crea**.
1. Definisci la configurazione.
   1. Seleziona **Microsoft Translator** nel menu a discesa.
   1. Digita un titolo per la configurazione. Il titolo identifica la configurazione sia nella console Cloud Services che negli elenchi a discesa delle proprietà della pagina.
   1. Facoltativamente, digita un nome da utilizzare per il nodo dell’archivio che memorizza la configurazione.

   ![Creare una configurazione di traduzione](../assets/create-translation-config.png)

1. Fai clic su **Crea**.
1. Nella finestra **Modifica configurazione**, indica i valori per il servizio di traduzione descritto nella tabella precedente.

   ![Modificare la configurazione della traduzione](../assets/msft-config-ui.png)

1. Seleziona **Connetti** per verificare la connessione.
1. Seleziona **Salva e chiudi**.

## Pubblicazione delle configurazioni del servizio Translator {#publishing-the-translator-service-configurations}

Come ultimo passaggio, pubblica le configurazioni di Microsoft Translator per supportare i contenuti tradotti pubblicati, utilizzando l&#39;azione [pubblicazione di una struttura](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-and-unpublishing-a-tree).
