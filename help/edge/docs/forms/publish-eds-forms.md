---
title: Pubblicare un modulo Edge Delivery Services di AEM Forms
description: Pubblicare un modulo Edge Delivery Services di AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Pubblicare il modulo

Quando si è pronti a condividere il modulo con i clienti per la raccolta o l&#39;invio dei dati, è sufficiente pubblicarlo, rendendolo facilmente disponibile per l&#39;utilizzo da parte dei clienti.

## Prerequisiti

* Il [Il blocco del modulo è abilitato per il progetto EDS su Github](/help/edge/docs/forms/create-forms.md).
* Il modulo è stato testato e pronto per l&#39;uso.
* Il tuo [il foglio di calcolo è configurato](/help/edge/docs/forms/submit-forms.md) per accettare i dati.

## Pubblicare il modulo

Per pubblicare il modulo:

1. Accedere al proprio account Microsoft SharePoint o Google Drive e passare al `[AEM Edge Delivery project directory]`.

1. Aprire un file di documento in cui si desidera incorporare il modulo. Ad esempio, è possibile aprire il file di indice o, in alternativa, creare un nuovo documento.

1. Identificare la sezione desiderata all&#39;interno del documento in cui si desidera inserire il modulo e passare di conseguenza.

1. Aggiungi al file un blocco denominato &quot;Modulo&quot;, simile all’esempio fornito di seguito:

   | Modulo |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Questo blocco funge da segnaposto in cui è incorporato il modulo. Nella seconda riga del blocco, aggiungi l’URL del `<form>.json` come collegamento ipertestuale.

   >[!IMPORTANT]
   >
   >
   > Verificare che l&#39;URL sia formattato come collegamento ipertestuale anziché come testo normale.

   Utilizza l’URL di anteprima (.page URL) a scopo di sviluppo o test oppure l’URL di pubblicazione (.live) per la produzione. Di seguito sono riportati alcuni esempi con URL di anteprima e pubblicazione:

   **URL di anteprima**
| Modulo | |—| | [https://main--portal--wkndforms.hlx.page/enquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **URL di pubblicazione**
| Modulo | |—| | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l&#39;anteprima della pagina. Nella pagina viene ora visualizzato il modulo. Ad esempio, questo è il modulo basato su [foglio di calcolo interrogazione](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Un esempio di modulo EDS](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Ora i tuoi clienti possono compilare il modulo e inviarlo.

## Risoluzione dei problemi

+++ Impossibile inviare i dati al modulo

Se si verifica un errore simile al seguente messaggio, il foglio di calcolo non è ancora configurato per accettare i dati inviati.

![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

+++


## Vedi altro

* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)