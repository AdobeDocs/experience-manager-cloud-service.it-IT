---
title: Connetti a Microsoft Translator
description: Scopri come collegare AEM a Microsoft Translator out-of-the-box per automatizzare il flusso di lavoro di traduzione.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# Connetti a Microsoft Translator {#connecting-to-microsoft-translator}

Crea una configurazione per [Traduttore Microsoft](https://hub.microsofttranslator.com) servizio cloud per utilizzare il tuo account di traduzione Microsoft per tradurre AEM contenuto di pagina o risorse.

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta la nostra [Percorso di traduzione dei siti,](/help/journey-sites/translation/overview.md) percorso guidato attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione di AEM, ideali per chi non ha esperienza di AEM o traduzione.

>[!NOTE]
>
>AEM fornisce un account di traduzione Microsoft di prova che consente un massimo di 2 000 000 caratteri tradotti gratuiti al mese. Per ottenere un abbonamento a un account adeguato per i sistemi di produzione, vedi [Aggiornamento della configurazione della licenza di prova di Microsoft Translator](#upgrading-the-microsoft-translator-trial-license-configuration).

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Nome visualizzato del servizio di traduzione |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall’utente, l’attribuzione visualizzata accanto al testo tradotto, ad esempio `Translations by Microsoft` |
| ID area di lavoro | (Facoltativo) L&#39;ID del motore di traduzione Microsoft personalizzato da utilizzare |
| Chiave di sottoscrizione | Chiave di abbonamento a Microsoft per Microsoft Translator |

Dopo aver creato la configurazione, devi [attivare](#activating-the-translator-service-configurations).

La procedura seguente crea una configurazione di Microsoft Translator.

1. In [pannello di navigazione,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) tocca o fai clic su **Strumenti** -> **Cloud Services** -> **Cloud Services di traduzione**.
1. Passa alla posizione in cui desideri creare la configurazione. Normalmente si trova nella directory principale del sito o può essere una configurazione globale predefinita.
1. Tocca o fai clic sul pulsante **Crea** pulsante .
1. Definisci la configurazione.
   1. Seleziona **Traduttore Microsoft** nel menu a discesa .
   1. Digita un titolo per la configurazione. Il titolo identifica la configurazione sia nella console Cloud Services che negli elenchi a discesa delle proprietà della pagina.
   1. Facoltativamente, digita un nome da utilizzare per il nodo del repository che memorizza la configurazione.

   ![Creare una configurazione di traduzione](../assets/create-translation-config.png)

1. Fai clic su **Crea**.
1. In **Modifica configurazione** fornire i valori per il servizio di traduzione descritto nella tabella precedente.

   ![Modificare la configurazione della traduzione](../assets/edit-translation-config.png)

1. Tocca o fai clic su **Connetti** per verificare la connessione.
1. Tocca o fai clic su **Salva e chiudi**.

## Aggiornamento della configurazione della licenza di prova di Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito web Microsoft per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. In [pannello di navigazione,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) tocca o fai clic **Strumenti** -> **Cloud Services** -> **Cloud Services di traduzione**.
1. Tocca o fai clic sulla configurazione di Microsoft Translator esistente.
1. Tocca o fai clic su **Modifica**.
1. In **Modifica configurazione** finestra, tocca o fai clic **Iscrizione all&#39;aggiornamento**. Viene visualizzata una pagina web Microsoft con ulteriori dettagli sul servizio.

## Personalizzazione del motore di traduzione Microsoft {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito web Microsoft per personalizzare il motore di traduzione Microsoft.

1. In [pannello di navigazione,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) tocca o fai clic **Strumenti** -> **Cloud Services** -> **Cloud Services di traduzione**.
1. Tocca o fai clic sulla configurazione di Microsoft Translator esistente.
1. Tocca o fai clic su **Modifica**.
1. In **Modifica configurazione** finestra, tocca o fai clic **Personalizza traduttore**. Utilizza la pagina web Microsoft che si apre per personalizzare il tuo servizio.

## Attivazione delle configurazioni del servizio di traduzione {#activating-the-translator-service-configurations}

Devi attivare le configurazioni del servizio cloud per supportare i contenuti tradotti replicati nell’istanza di pubblicazione. Utilizzare il metodo [pubblicazione di una struttura](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) per attivare i nodi del repository che memorizzano le configurazioni di Microsoft Translator. I nodi si trovano sotto i seguenti nodi padre:

* `/libs/settings/cloudconfigs/translation/msft-translation`
