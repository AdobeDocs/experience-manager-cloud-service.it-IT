---
title: Come personalizzare il modello del documento di record generato automaticamente per Adaptive Forms?
description: Scopri come scaricare, personalizzare e ricaricare il modello DoR (Document of Record) generato automaticamente per Adaptive Forms utilizzando Adobe Forms Designer.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer
source-git-commit: 51ec9ef76a8f3f9b7bf2cdc25b03f72e286f586f
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---


# Personalizzare il modello del documento di record generato automaticamente

<span class="preview"> Questo articolo si applica sia a **Componenti core** che a **Componenti Foundation** basati su Adaptive Forms.</span>

Quando generi automaticamente un documento di record (DoR) per un modulo adattivo, AEM Forms crea un modello predefinito basato sulla struttura del modulo. Puoi personalizzare questo modello generato automaticamente in base ai requisiti di branding e layout della tua organizzazione.

Il flusso di lavoro di personalizzazione prevede tre passaggi:

1. Scarica il modello DoR generato automaticamente da Forms Manager.
1. Modifica il modello utilizzando Adobe Forms Designer.
1. Ricarica il modello personalizzato in AEM Forms e configuralo come modello personalizzato.

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di avere i seguenti elementi:

* Accesso ad AEM Forms Manager con autorizzazioni per scaricare e caricare modelli.
* Adobe Forms Designer installato nel computer locale.
* Modulo adattivo con **[!UICONTROL Genera documento record]** abilitato.

## Passaggio 1: scarica il modello DoR generato automaticamente {#download-auto-generated-dor-template}

Per scaricare il modello DoR generato automaticamente (file XDP) per il modulo adattivo:

1. Accedi all’istanza Autore di AEM Forms.
1. Passa a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo per il quale desideri scaricare il modello DoR.
1. Apri le proprietà del modulo adattivo selezionato.
1. Nel pannello delle proprietà, seleziona l&#39;opzione **[!UICONTROL Scarica documento di record]** per scaricare il modello DoR generato automaticamente (file XDP).
1. Salva il file XDP scaricato nel computer locale.


## Passaggio 2: personalizzare il modello utilizzando Adobe Forms Designer {#customize-template-using-designer}

Apri il modello XDP scaricato in Adobe Forms Designer e modificalo in base alle esigenze della tua organizzazione.

1. Apri il file XDP scaricato in **Adobe Forms Designer**.
1. Personalizza il modello come richiesto. Esempi di personalizzazioni includono:

   * **Più pagine master**: aggiungi ulteriori pagine master per definire layout diversi per pagine specifiche del documento record. Ad esempio, utilizza una prima pagina distinta con un&#39;intestazione aziendale e le pagine successive con un layout più semplice.
   * **Colori e famiglie di tipi di carattere**: modifica il colore, la dimensione e la famiglia dei tipi di carattere in base alle linee guida aziendali per il marchio.
   * **Elementi personalizzati**: aggiungi elementi quali logo aziendali, intestazioni, piè di pagina e testo della liberatoria per stabilire un&#39;identità del brand coerente.
   * **Layout e stile pagina**: regola i margini, la spaziatura e la struttura generale della pagina per migliorarne la leggibilità.
   * **Stile e posizionamento dei campi**: modifica l&#39;aspetto e la posizione dei campi modulo in base al layout preferito.

1. Salva il modello XDP personalizzato.

>[!NOTE]
>
> Non rimuovere o modificare gli script presenti nel modello. La modifica degli script può influire sull&#39;associazione dei dati e sulla generazione del documento di record.

## Passaggio 3: ricarica il modello personalizzato in AEM {#reupload-customized-template}

Dopo aver personalizzato il modello, caricalo su AEM Forms e configura il modulo adattivo per utilizzarlo.

1. Carica il modello XDP personalizzato nella tua istanza di AEM Forms:
   * Passa a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
   * Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]** e carica il file XDP personalizzato.

Quindi configura il modulo per utilizzare il modello personalizzato. I passaggi variano a seconda che il modulo sia basato su Componenti core o Componenti di base.

>[!BEGINTABS]

>[!TAB Componenti core]

Per Forms adattivo basato su componenti core:

1. Apri il modulo adattivo nell’editor per il quale desideri applicare il modello personalizzato.
1. Nella struttura del contenuto, selezionare **[!UICONTROL Contenitore guida]** (pannello radice).
1. Apri **[!UICONTROL Proprietà]** e fai clic sull&#39;icona **[!UICONTROL Documento di record]** (DoR) per aprire le proprietà del documento di record.
1. Nella scheda **[!UICONTROL Base]**, apri il menu a discesa **[!UICONTROL Modello]** e seleziona **[!UICONTROL Personalizzato]**.
1. Sfoglia e seleziona il modello XDP personalizzato caricato.
1. Seleziona il segno di spunta da salvare.

   ![Proprietà del documento record - Modello impostato su Personalizzato (Componenti core)](/help/forms/assets/submission-pdf-dor-custom-template.png)

>[!TAB Componenti di base]

Per Forms adattivo basato su componenti di base:

1. Apri il modulo adattivo nell’editor per il quale desideri applicare il modello personalizzato.
1. Seleziona il pannello principale (contenitore modulo).
1. Apri **[!UICONTROL Proprietà documento record]** (dal pannello delle proprietà o dalla scheda DoR).
1. Nella scheda **[!UICONTROL Base]**, apri il menu a discesa **[!UICONTROL Modello]** e seleziona **[!UICONTROL Personalizzato]**.
1. Sfoglia e seleziona il modello XDP personalizzato caricato.
1. Seleziona **[!UICONTROL Fine]** per salvare.

   ![Proprietà del documento record - Modello impostato su Personalizzato (Componenti di base)](/help/forms/assets/dor-custom-template-foundation-components.png)

>[!ENDTABS]

Il modulo adattivo ora utilizza il modello personalizzato durante la generazione del documento di record.

## Verifica il modello personalizzato {#verify-customized-template}

Per verificare che il modello personalizzato sia applicato correttamente:

1. Invia una voce di test per il modulo adattivo.
1. Genera il documento di record.
1. Verifica che il PDF generato rifletta le tue personalizzazioni, inclusi loghi, font, modifiche al layout e altri elementi di branding.

## Risoluzione dei problemi {#troubleshooting}

| Problema | Risoluzione |
|---|---|
| Il modello personalizzato non viene caricato. | Verificare che il file XDP sia valido e non danneggiato. Verifica di disporre delle autorizzazioni necessarie per caricare i file in AEM Forms. |
| Le personalizzazioni non vengono visualizzate nel documento di record generato. | Conferma di aver selezionato il modello personalizzato corretto nella sezione **[!UICONTROL Configurazione del modello del documento record]** delle proprietà del modulo. |
| Problemi di layout o formattazione nel PDF generato. | Verificare che le personalizzazioni in Adobe Forms Designer rispettino le [convenzioni di base del modello](/help/forms/generate-document-of-record-core-components.md#base-template-conventions). Assicurati che tutti gli elementi siano posizionati correttamente all’interno della struttura del modello. |

## Consulta anche {#see-also}

* [Generare documenti di record per Forms adattivo (componenti core)](/help/forms/generate-document-of-record-core-components.md)
* [Genera documento di record per Forms adattivo (componenti di base)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Modello base di un documento record](/help/forms/generate-document-of-record-core-components.md#base-template-of-a-document-of-record)
* [Personalizzare le informazioni di branding nel documento record](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record)

