---
title: Tradurre e localizzare un modulo Edge Delivery Services di AEM Forms
description: Tradurre e localizzare un modulo Edge Delivery Services di AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 100%

---


# Tradurre e localizzare un modulo Edge Delivery Services di AEM Forms

In Edge Delivery Services, la traduzione dei moduli comporta la conversione del contenuto dei moduli da una lingua all’altra, con particolare attenzione alla precisione, alla chiarezza e alla coerenza. I moduli tradotti o localizzati consentono una più ampia copertura del pubblico tra diverse posizioni geografiche, migliorando così l’esperienza utente e facilitando una migliore comunicazione tra le diverse preferenze linguistiche.


Alla fine di questo articolo imparerai a:

- [Tradurre moduli in Google Drive](#translate-form-google-drive)
- [Tradurre moduli nel sito SharePoint](#translate-form-sharepoint)

## Tradurre moduli in Google Drive {#translate-form-google-drive}

La funzione `GOOGLETRANSLATE` in fogli Google traduce i moduli toccando lo strumento di traduzione incorporato, cambiando il testo da una lingua all’altra direttamente all’interno di un foglio Google. Per tradurre i moduli in Google Drive:

1. Passa alla cartella dei progetti AEM su Google Drive e apri il foglio Google.
2. Rinomina il foglio esistente (`shared-default`) in `shared-en`.
3. Aggiungi un foglio denominato `shared-default`. Il foglio `shared-default` contiene il contenuto per la localizzazione in una lingua specifica.
4. Aggiungi il contenuto localizzato nel foglio `shared-default` con la funzione `GOOGLETRANSLATE`.
È possibile utilizzare una formula per tradurre il contenuto della cella D2 dal foglio `shared-en` in francese all’interno del foglio `shared-default`. Di seguito è riportata la formula da utilizzare:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Traduci foglio di calcolo “enquiry”](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Visualizza in anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

È possibile fare riferimento al [foglio di calcolo](/help/forms/assets/enquirytranslate.xlsx) contenente la definizione del modulo per un modulo `enquiry` tradotto dall’inglese al francese.

![Modulo “enquiry” tradotto](/help/forms/assets/translate-form-french.png)

Fai riferimento all’URL seguente, dove è possibile visualizzare il modulo con la sua traduzione in lingua francese:
https://main--portal--wkndforms.hlx.live/enquirytranslate

## Tradurre moduli nel sito SharePoint{#translate-form-sharepoint}

Per tradurre i moduli sul sito Microsoft® SharePoint, è necessario modificare manualmente le etichette dei campi utilizzando qualsiasi servizio di traduzione. Per tradurre i moduli nel sito SharePoint:

1. Vai alla cartella dei progetti AEM su Microsoft® SharePoint e apri il foglio di calcolo.
2. Rinomina il foglio esistente (`shared-default`) in `shared-en`.
3. Aggiungi un foglio denominato `shared-default`. Il foglio `shared-default` raccoglie il contenuto per la localizzazione in una lingua specifica.
4. Aggiungere il contenuto localizzato nel foglio `shared-default` manualmente.

   ![Traduci foglio di calcolo “enquiry”](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Visualizza in anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Fai riferimento al [foglio di calcolo](/help/forms/assets/enquirytranslate-sp.xlsx) contenente la definizione del modulo per un modulo `enquiry` tradotto dall’inglese al francese.

![Modulo “enquiry” tradotto](/help/forms/assets/translate-form-french.png)

Fai riferimento all’URL seguente, dove puoi visualizzare il modulo con la sua traduzione in lingua francese:
https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## Problemi noti {#known-issues}

- Le etichette del modulo vengono tradotte nella lingua localizzata specificata nel foglio `shared-default`, ma i messaggi di errore vengono visualizzati nella lingua predefinita del browser.

  ![Messaggio di errore](/help/forms/assets/translate-error-message.png)

- Quando apri il calendario, viene visualizzato in elenco a discesa nella lingua predefinita del browser.

  ![Messaggio di errore](/help/forms/assets/translate-calender-display.png)


## Domande frequenti {#faq}

**D**: come si digita l’input nella lingua localizzata specificata in un modulo?

**R**: per inserire testo in una lingua localizzata specifica, regola le impostazioni della tastiera sul dispositivo. Per istruzioni su come eseguire questa operazione, fai riferimento ai seguenti collegamenti:

- [Configurare il Mac per ricevere input in un’altra lingua](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
- [Configurare Windows per ricevere input in un’altra lingua](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
- [Configurare dispositivi Android o iPhone/iPad per ricevere input in un’altra lingua](https://support.google.com/gboard/answer/7068494?hl=en&co=GENIE.Platform%3DAndroid)


**D**: come posso recuperare un elenco di lingue utilizzate nella funzione `GOOGLETRANSLATE`?

**R**: puoi fare riferimento alla [documentazione ufficiale di Google](https://cloud.google.com/translate/docs/languages) per un elenco completo delle lingue utilizzate in GOOGLETRANSLATE.


