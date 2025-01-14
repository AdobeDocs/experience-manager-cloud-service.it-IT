---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 8%

---

# Configurare l’origine dati di Marketo Engage per moduli adattivi esistente

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

![Flusso di lavoro](/help/forms/assets/workflow-marketo-2.png)

Dopo aver creato la configurazione del servizio cloud per integrare il Marketo Engage con AEM Forms esistente, puoi configurare l’origine dati per i moduli.

La configurazione dell’integrazione dei dati consente agli utenti di connettersi a varie origini dati o schemi. L’integrazione con l’origine dati di Marketo Engage e il suo utilizzo in diversi moduli facilitano le operazioni su tali dati. Per esplorare le origini dati predefinite supportate per un modulo adattivo, consulta l&#39;articolo [Configurare le origini dati](/help/forms/configure-data-sources.md).

## Considerazione per la configurazione dell&#39;origine dati di Marketo Engage per i moduli

Durante la configurazione dell’origine dati di Marketo Engage per i moduli si tiene conto dei seguenti fattori:

* Non è possibile collegare Edge Delivery Services Forms al Marketo Engage.

## Prerequisito per l&#39;utilizzo dell&#39;origine dati di Marketo Engage per i moduli

Prerequisito per l&#39;utilizzo dell&#39;origine dati di Marketo Engage con i moduli:

* Crea la configurazione del servizio cloud [per integrare il Marketo Engage con forms](/help/forms/integrate-form-to-marketo-engage.md).

## Come configurare un modulo adattivo esistente per l’origine dati di Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

Per configurare un modulo adattivo con l’origine dati di Marketo Engage, effettua le seguenti operazioni:
1. Accedi all&#39;istanza Autore [!DNL Experience Manager Forms].

2. Apri il modulo adattivo per la modifica.
3. Aprire la Struttura contenuto e selezionare il **[!UICONTROL Contenitore guida]**.
4. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare l’origine dati.
5. Apri la scheda **[!UICONTROL Modello dati]** e seleziona un modello di modulo come **Connettore**.
6. Selezionare **[!UICONTROL Connettore]** dall&#39;elenco a discesa.

7. Dopo aver selezionato il **[!UICONTROL connettore]**, puoi selezionare la configurazione cloud.

   ![Seleziona Connettore Marketo](/help/forms/assets/select-marketo-connector.png)

   In base alla configurazione di Marketo Engage selezionata, gli elementi del modulo vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** di **[!UICONTROL Browser contenuto]** nella barra laterale. Puoi trascinare questi elementi per creare il modulo adattivo.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png)

8. Fai clic su **[!UICONTROL Fine]**.

In alternativa, puoi anche modificare le proprietà del modulo adattivo per modificarne la configurazione associata.

Il modulo adattivo è ora configurato con l’origine dati dell’istanza del Marketo Engage connesso. Ora configuralo per inviare dati a Adobe Marketo Engage.

## Domande frequenti

**D: cosa succede quando si modifica il connettore del modulo?**\
**A:** Se si modifica il connettore del modulo, le associazioni esistenti non saranno più valide.

**D: quali sono le tre operazioni disponibili nel servizio Invoke dell&#39;editor di regole per i moduli integrati nel Marketo Engage?**\
**A:** Le tre operazioni predefinite disponibili in **Invoke Service** per i moduli integrati con il Marketo Engage sono:
* Sincronizza lead
* Ottieni lead per ID
* Ottieni lead per tipo di filtro

## Passaggio successivo

Ora hai configurato l’origine dati di Marketo Engage per Adaptive Forms. Successivamente, puoi [configurare un modulo adattivo per inviare dati al Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Articoli correlati

{{af-submit-action}}

## Consulta anche

{{marketo-engage-see-also}}
