---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 9%

---

# Configurare l’azione di invio a Marketo Engage per i moduli esistenti

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

![Flusso di lavoro](/help/forms/assets/workflow-marketo-3.png)

L&#39;editor di Forms adattivo fornisce l&#39;azione di invio **Invia al Marketo Engage** per inviare dati di Forms adattivo a Adobe Marketo Engage per l&#39;elaborazione. È possibile configurare un modulo adattivo esistente per inviare dati a [Adobe Marketo Engage](https://experienceleague.adobe.com/it/docs/marketo/using/home) all&#39;invio.

Sono disponibili varie azioni di invio predefinite per la gestione degli invii dei moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

## Considerazione durante la configurazione dell’azione di invio al Marketo Engage per il modulo

* Assicurati che il modulo adattivo sia configurato con l’origine dati di Marketo Engage per inviare dati al Marketo Engage al momento dell’invio del modulo. È tuttavia possibile modificare l&#39;azione di invio in alternativa, ad esempio **Invia a OneDrive** o **Invia a SharePoint**, anche se il modulo è configurato con lo schema dati del Marketo Engage.

## Prerequisito per configurare l’azione di invio al Marketo Engage per il modulo esistente

Prerequisito per configurare l’azione di invio per il Marketo Engage:

* Configura l&#39;origine dati [Marketo Engage per il modulo adattivo](/help/forms/use-marketo-engage-data-source-in-form.md) e associa gli elementi del modulo ai campi Marketo Engage.

## Come si configura l’azione di invio al Marketo Engage per i moduli esistenti?

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

È possibile configurare l’azione di invio di un modulo adattivo per inviare dati a Adobe Marketo Engage. Per configurare l&#39;azione di invio al Marketo Engage, effettuare le seguenti operazioni:

1. Apri il modulo adattivo per la modifica.
2. Aprire la Struttura contenuto e selezionare il **[!UICONTROL Contenitore guida]**.
3. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo con cui configurare l’azione di invio.
4. Apri la scheda **[!UICONTROL Invio]** e seleziona un&#39;azione di invio come **Invia al Marketo Engage**.
5. Fai clic su **[!UICONTROL Fine]**.

![Azione di invio Marketo](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}


Dopo aver configurato l&#39;azione di invio per il modulo adattivo come **Invia al Marketo Engage**, puoi inviare dati a Adobe Marketo Engage per l&#39;elaborazione. I dati possono essere utilizzati per analizzare e ottimizzare campagne di marketing, automatizzare le e-mail di follow-up e attivare flussi di lavoro in base all’invio di moduli.

## Domande frequenti

**D: è possibile modificare l&#39;azione di invio per i moduli configurati per la connessione allo schema di Marketo Engage?**
**A:** Per impostazione predefinita, l&#39;azione **Invia a Marketo** è selezionata quando un modulo è configurato per la connessione allo schema del Marketo Engage. Tuttavia, se necessario, è possibile modificare l&#39;azione di invio per i moduli.

## Passaggio successivo

È inoltre possibile collegare un modulo adattivo alla [libreria Munchkin](https://experienceleague.adobe.com/it/docs/marketo/using/product-docs/administration/setup/munchkin) per tenere traccia del numero di visite, clic e invii di moduli.

## Articoli correlati

{{af-submit-action}}

## Consulta anche

{{marketo-engage-see-also}}
