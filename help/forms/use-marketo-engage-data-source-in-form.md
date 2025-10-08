---
title: Come si configurano i dati di Marketo Engage per Adaptive Forms?
description: Scopri come utilizzare lo schema Marketo Engage in Adaptive Forms.
keywords: 'Utilizzare l’origine dati Marketo Engage in Adaptive Forms: come collegare un’origine dati dell’istanza Marketo con un modulo? , Connettere un modulo a Marketo.'
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: 4bb63932a658cf01cc493b9e5e68b96984cce49c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 8%

---

# Configurare l’origine dati di Marketo Engage per moduli adattivi esistente

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

![Flusso di lavoro](/help/forms/assets/workflow-marketo-2.png)

Dopo aver creato la configurazione del servizio cloud per integrare Marketo Engage con AEM Forms esistente, puoi configurare l’origine dati per i moduli.

La configurazione dell’integrazione dei dati consente agli utenti di connettersi a varie origini dati o schemi. L’integrazione con l’origine dati Marketo Engage e il suo utilizzo in diversi moduli facilita le operazioni su tali dati. Per esplorare le origini dati predefinite supportate per un modulo adattivo, consulta l&#39;articolo [Configurare le origini dati](/help/forms/configure-data-sources.md).

## Prerequisito per l’utilizzo dell’origine dati Marketo Engage per i moduli

Prerequisito per utilizzare l’origine dati Marketo Engage con i moduli:

* Crea la configurazione del servizio cloud [per integrare Marketo Engage con forms](/help/forms/integrate-form-to-marketo-engage.md).

## Come si configura un modulo adattivo esistente per l’origine dati Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span> Questo video è applicabile solo ai Componenti core. Per i componenti UE/Foundation, fare riferimento all&#39;articolo.</span>

>[!BEGINTABS]

>[!TAB Componente di base]

Per configurare un modulo adattivo basato su componenti di base con l’origine dati Marketo Engage, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring [!DNL Experience Manager Forms].
1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Modello dati]** delle proprietà Contenitore modulo adattivo e seleziona un modello di modulo come **Connettore**.
1. Selezionare **[!UICONTROL Connettore]** dall&#39;elenco a discesa.
1. Dopo aver selezionato il **[!UICONTROL connettore]**, puoi selezionare la configurazione cloud.

   ![Seleziona Connettore Marketo](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   In base alla configurazione di Marketo Engage selezionata, gli elementi del modulo vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** di **[!UICONTROL Browser contenuto]** nella barra laterale. Puoi trascinare questi elementi per creare il modulo adattivo.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. Fai clic su **[!UICONTROL Fine]**.

In alternativa, puoi anche modificare le proprietà del modulo adattivo per modificarne la configurazione associata.

Il modulo adattivo è ora configurato con l’origine dati dell’istanza di Marketo Engage connessa. Ora configuralo per inviare dati a Adobe Marketo Engage.

>[!TAB Componente core]

Per configurare un modulo adattivo basato su componenti core con l’origine dati Marketo Engage, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring [!DNL Experience Manager Forms].

1. Apri il modulo adattivo per la modifica.
1. Aprire la Struttura contenuto e selezionare il **[!UICONTROL Contenitore guida]**.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare l’origine dati.
1. Apri la scheda **[!UICONTROL Modello dati]** e seleziona un modello di modulo come **Connettore**.
1. Selezionare **[!UICONTROL Connettore]** dall&#39;elenco a discesa.

1. Dopo aver selezionato il **[!UICONTROL connettore]**, puoi selezionare la configurazione cloud.

   ![Seleziona Connettore Marketo](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   In base alla configurazione di Marketo Engage selezionata, gli elementi del modulo vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** di **[!UICONTROL Browser contenuto]** nella barra laterale. Puoi trascinare questi elementi per creare il modulo adattivo.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. Fai clic su **[!UICONTROL Fine]**.

In alternativa, puoi anche modificare le proprietà del modulo adattivo per modificarne la configurazione associata.

Il modulo adattivo è ora configurato con l’origine dati dell’istanza di Marketo Engage connessa. Ora configuralo per inviare dati a Adobe Marketo Engage.

>[!TAB Editor universale]

Per configurare un modulo adattivo creato in Universal Editor con l’origine dati Marketo Engage, effettua le seguenti operazioni:

1. Apri le proprietà del modulo per la modifica.
1. Selezionare il **[!UICONTROL modello modulo]**.
1. Seleziona **Connettore** dal **[!UICONTROL Modello modulo]**.
1. Dopo aver selezionato il **[!UICONTROL connettore]**, puoi selezionare la configurazione cloud.

   ![Seleziona Connettore Marketo](/help/forms/assets/select-marketo-connector-ue.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**.

In base alla configurazione di Marketo Engage selezionata, gli elementi del modulo vengono visualizzati nella scheda **[!UICONTROL Origine dati]** del browser Contenuto nel pannello Proprietà. Puoi trascinare questi elementi per creare il modulo adattivo.

![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-ue.png)

Il modulo è ora configurato con l’origine dati dell’istanza di Marketo Engage connessa. Ora configuralo per inviare dati a Adobe Marketo Engage.

>[!ENDTABS]

## Domande frequenti

**D: cosa succede quando si modifica il connettore del modulo?**\
**A:** Se si modifica il connettore del modulo, le associazioni esistenti non saranno più valide.

**D: quali sono le tre operazioni disponibili nel servizio Invoke dell&#39;editor di regole per i moduli integrati con Marketo Engage?**\
**A:** Le tre operazioni predefinite disponibili in **Invoke Service** per i moduli integrati con Marketo Engage sono:
* Sincronizza lead
* Ottieni lead per ID
* Ottieni lead per tipo di filtro

## Passaggio successivo

Ora hai configurato l’origine dati Marketo Engage per Adaptive Forms. Successivamente, puoi [configurare un modulo adattivo per inviare dati a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Articoli correlati

{{af-submit-action}}

## Consulta anche

{{marketo-engage-see-also}}
