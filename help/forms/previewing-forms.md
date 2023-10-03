---
title: Visualizzare in anteprima un modulo adattivo
description: Gli utenti possono visualizzare in anteprima i moduli prima di pubblicarli o attivarli, per assicurarsi che soddisfino le aspettative. Le opzioni di anteprima possono variare tra i tipi di modulo supportati.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
source-git-commit: 92f89243b79c6c2377db3ca2b8ea244957416626
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 3%

---


# Anteprima di un modulo {#previewing-a-form}

## Panoramica {#overview}

In entrata [!DNL AEM Forms], è possibile visualizzare in anteprima i moduli e i documenti presenti nel repository. L&#39;anteprima consente di conoscere esattamente l&#39;aspetto e il comportamento dei moduli quando vengono rilasciati agli utenti finali.

Quando si visualizza l’anteprima dei moduli, questi vengono riprodotti in un’interfaccia interattiva e l’utente può riempirli di dati. Quando si visualizza l’anteprima di un documento, questo viene riprodotto in modalità non interattiva e l’utente può solo visualizzarlo. Per i moduli è disponibile un’ulteriore opzione di Anteprima personalizzata. Questa opzione consente di visualizzare in anteprima il modulo utilizzando i dati di un file XML. I dati riempiono alcuni o tutti i campi del modulo visualizzato in anteprima.

Nella tabella seguente sono elencate le opzioni di anteprima disponibili per i diversi tipi di moduli supportati:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo risorsa</strong><br /> </td>
   <td><strong>Opzioni di anteprima disponibili</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Anteprima PDF</td>
  </tr>
  <tr>
   <td>Modulo PDF</td>
   <td>Anteprima e anteprima PDF con i dati<br /> </td>
  </tr>
  <tr>
   <td>Modulo adattivo</td>
   <td>Anteprima HTML e Anteprima HTML con dati</td>
  </tr>
  <tr>
   <td>Modello modulo</td>
   <td>Anteprima PDF, Anteprima PDF con dati, Anteprima HTML, Anteprima HTML con dati<br /> </td>
  </tr>
 </tbody>
</table>

## Anteprima di un modulo {#previewing-a-form-1}

1. Seleziona una risorsa da visualizzare in anteprima e fai clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png) nella barra delle azioni.

   >[!NOTE]
   >
   >Per selezionare una risorsa, passa alla vista a elenco dalla vista a schede predefinita. Clic ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) per cambiare visualizzazione.

1. Facendo clic su Anteprima vengono elencate le possibili opzioni di anteprima applicabili al tipo di risorsa selezionato. Fai clic sull’opzione desiderata per eseguire il rendering della risorsa selezionata in una nuova scheda.

   Le opzioni disponibili sono:

   * Anteprima come HTML
   * Anteprima con i dati
   * Anteprima come PDF (disponibile per i modelli di modulo)

## Anteprima con i dati {#preview-with-data}

Quando selezioni **Anteprima con dati**, è possibile visualizzare l&#39;aspetto del modulo con i dati reali immessi. L’opzione Anteprima con dati consente di caricare un XML che contiene dati utente di esempio. I dati utente di esempio vengono utilizzati per compilare il modulo di anteprima nel formato scelto.

1. Seleziona una risorsa e fai clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png), e seleziona **Anteprima con dati**.
1. Nella finestra di dialogo Anteprima modulo, specificare FormData come file XML. Fare clic su Anteprima per eseguire il rendering del modulo con i dati uniti da XML.

