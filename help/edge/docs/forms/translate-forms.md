---
title: Tradurre e localizzare un modulo di Edge Delivery Services AEM Forms
description: Tradurre e localizzare un modulo di Edge Delivery Services AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 6%

---


# Tradurre e localizzare un modulo di Edge Delivery Services AEM Forms

Nei Edge Delivery Services, la traduzione dei moduli comporta la conversione del contenuto dei moduli da una lingua all’altra, con particolare attenzione alla precisione, alla chiarezza e alla coerenza. I moduli tradotti o localizzati consentono una più ampia copertura del pubblico tra diverse posizioni geografiche, migliorando così l’esperienza utente e facilitando una migliore comunicazione tra le diverse preferenze linguistiche.


Alla fine dell’articolo imparerai a:

* [Traduzione di moduli in Google Drive](#translate-form-google-drive)
* [Traduzione di moduli nel sito SharePoint](#translate-form-sharepoint)

## Traduzione di moduli in Google Drive {#translate-form-google-drive}

Il `GOOGLETRANSLATE` funzione in fogli Google traduce i moduli toccando in strumento di traduzione incorporato, cambiando il testo da una lingua all&#39;altra direttamente all&#39;interno di un foglio Google. Per tradurre i moduli in Google Drive:

1. Vai alla cartella dei progetti AEM su Google Drive e apri il foglio Google.
2. Rinomina il foglio esistente (`shared-default`) a `shared-en`.
3. Aggiungi un foglio denominato `shared-default`. Il `shared-default` contiene il contenuto per la localizzazione in una lingua specifica.
4. Aggiungere il contenuto localizzato in `shared-default` foglio con `GOOGLETRANSLATE` funzione.
È possibile utilizzare una formula per tradurre il contenuto della cella D2 dal `shared-en` in francese entro il `shared-default` foglio. Di seguito è riportata la formula da utilizzare:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Interrogazione Traduci foglio di calcolo](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Visualizzare in anteprima e pubblicare il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

È possibile fare riferimento a [foglio di calcolo](/help/forms/assets/enquirytranslate.xlsx) contenente la definizione del modulo per un `enquiry` modulo tradotto dall&#39;inglese al francese.

![Modulo interrogazione tradotto](/help/forms/assets/translate-form-french.png)

Fai riferimento all&#39;URL seguente, dove è possibile visualizzare il modulo con la sua traduzione in lingua francese: https://main--portal--wkndforms.hlx.live/enquirytranslate

## Traduzione di moduli nel sito SharePoint{#translate-form-sharepoint}

Per tradurre i moduli sul sito Microsoft® SharePoint, è necessario modificare manualmente le etichette dei campi utilizzando qualsiasi servizio di traduzione. Per tradurre i moduli nel sito SharePoint:

1. Vai alla cartella dei progetti AEM su Microsoft® SharePoint e apri il foglio di calcolo.
2. Rinomina il foglio esistente (`shared-default`) a `shared-en`.
3. Aggiungi un foglio denominato `shared-default`. Il `shared-default` contiene il contenuto per la localizzazione in una lingua specifica.
4. Aggiungere il contenuto localizzato in `shared-default` foglio manualmente.

   ![Interrogazione Traduci foglio di calcolo](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Visualizzare in anteprima e pubblicare il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Consulta la sezione [foglio di calcolo](/help/forms/assets/enquirytranslate-sp.xlsx) contenente la definizione del modulo per un `enquiry` modulo tradotto dall&#39;inglese al francese.

![Modulo interrogazione tradotto](/help/forms/assets/translate-form-french.png)

Fai riferimento all&#39;URL seguente, dove è possibile visualizzare il modulo con la sua traduzione in lingua francese: https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## Problemi noti {#known-issues}

* Le etichette del modulo vengono tradotte nella lingua localizzata specificata in `shared-default` , ma i messaggi di errore vengono visualizzati nella lingua predefinita del browser.

  ![Messaggio di errore](/help/forms/assets/translate-error-message.png)

* Quando apri il calendario, l’elenco a discesa del calendario viene visualizzato nella lingua predefinita del browser.

  ![Messaggio di errore](/help/forms/assets/translate-calender-display.png)


## Domande frequenti {#faq}

**Q**: come si digita l’input nella lingua localizzata specificata in un modulo?

**A**: per inserire testo in una lingua localizzata specifica, regola le impostazioni della tastiera sul dispositivo. Per istruzioni su come eseguire questa operazione, fai riferimento ai seguenti collegamenti:

* [Configura il Mac per ricevere input in un&#39;altra lingua](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [Configurare Windows per immettere dati in un&#39;altra lingua](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [Configura i tuoi Android o iPhone/iPad per ricevere input in un’altra lingua](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**: come posso recuperare un elenco di impostazioni internazionali utilizzate nella `GOOGLETRANSLATE` funzione?

**A**: puoi fare riferimento a [documentazione ufficiale di Google](https://cloud.google.com/translate/docs/languages) per un elenco completo delle lingue utilizzate nel GOOGLETRANSLATE.

## Consulta anche

{{see-more-forms-eds}}

