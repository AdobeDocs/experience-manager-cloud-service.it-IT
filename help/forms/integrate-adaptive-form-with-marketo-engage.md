---
Title: How to integrate Marketo Engage with AEM Forms using Form wizard?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms using form wizard.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 7%

---

# Integrare un modulo adattivo con Marketo Engage

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

![Flusso di lavoro](/help/forms/assets/workflow-marketo-4.png)

Dopo aver creato la configurazione del servizio cloud per integrare Marketo Engage con AEM Forms, puoi configurare un modulo adattivo da integrare con [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home).

È possibile collegare Marketo Engage a un modulo adattivo utilizzando la procedura guidata del modulo, che semplifica il processo di configurazione guidando l’utente attraverso ogni passaggio. Include la selezione di modelli, stili e campi dati, nonché la configurazione della mappatura dei dati per garantire che il modulo sia pronto per la comunicazione con Marketo Engage dopo la creazione. Utilizzando la procedura guidata del modulo, puoi anche configurare il modulo adattivo in modo che invii i dati direttamente a Adobe Marketo Engage al momento dell’invio.

## Considerazioni sulla configurazione dell&#39;origine dati Marketo Engage per i moduli

Durante la configurazione dell’origine dati di Marketo Engage per i moduli si tiene conto dei seguenti fattori:

* Impossibile collegare Edge Delivery Services Forms a Marketo Engage.

## Prerequisito per la connessione di Marketo Engage con Forms

Prerequisito per la connessione di Marketo Engage ai moduli:

* Crea la configurazione del servizio cloud [per integrare Marketo Engage con forms](/help/forms/integrate-form-to-marketo-engage.md).

## Come configurare un nuovo modulo adattivo da integrare con Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442867/marketo-aem-marketo-engage-engage-aem-forms)

>[!BEGINTABS]

>[!TAB Componente di base]

Per configurare un nuovo modulo adattivo basato su componenti di base da integrare con Marketo Engage, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

   ![Seleziona Forms e documenti](/help/forms/assets/select-forms.png)

1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene visualizzata la procedura guidata di creazione del modulo.

   ![Seleziona AF](/help/forms/assets/select-create-forms.png)

1. Nella scheda **[!UICONTROL Source]**, seleziona un modello

   ![Seleziona modelli](/help/forms/assets/select-template-af1.png)

1. In **[!UICONTROL Stile]**, selezionare il tema.

   ![Seleziona tema](/help/forms/assets/select-form-theme-af1.png)
1. Nella scheda **[!UICONTROL Dati]**, seleziona un modello dati come **Marketo Engage**.
1. Selezionare la **[!UICONTROL Configurazione cloud]** dall&#39;elenco a discesa visualizzato nel riquadro di destra dello schermo.
Per impostazione predefinita, vengono visualizzati tutti i campi della configurazione associata. La procedura guidata consente di scegliere in modo selettivo i campi da includere nel modulo adattivo tramite l’utilizzo di caselle di controllo.

   ![Seleziona modello dati](/help/forms/assets/select-marketo-data-af1.png)

1. Nella scheda **[!UICONTROL Invio]**, seleziona l&#39;azione di invio come **[!UICONTROL Invia a Marketo]**.

   Quando selezioni il modello dati come **Marketo Engage**, l&#39;azione di invio come **Invia a Marketo** viene selezionata automaticamente. Puoi selezionare un&#39;azione di invio diversa dalla scheda **[!UICONTROL Invio]**. Nella scheda **[!UICONTROL Invio]** vengono visualizzate tutte le azioni di invio disponibili.

   ![Invia a Marketo engagement](/help/forms/assets/select-marketo-engage.png)

1. Seleziona **[!UICONTROL Crea]**. Specifica il titolo, il nome e il percorso per salvare il modulo adattivo.

   ![Crea modulo](/help/forms/assets/create-marketo-form.png)

1. Seleziona **[!UICONTROL Crea]**.

Il modulo adattivo è ora configurato per connettersi all’istanza di Marketo Engage. In alternativa, puoi anche modificare le proprietà del modulo adattivo per modificarne la configurazione associata

>[!TAB Componente core]

Per configurare un nuovo modulo adattivo basato su componenti core da integrare con Marketo Engage, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

   ![Seleziona Forms e documenti](/help/forms/assets/select-forms.png)

1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene visualizzata la procedura guidata di creazione del modulo.

   ![Seleziona AF](/help/forms/assets/select-create-forms.png)

1. Nella scheda **[!UICONTROL Source]**, seleziona un modello

   ![Seleziona modelli](/help/forms/assets/select-template.png)

1. In **[!UICONTROL Stile]**, selezionare il tema.

   ![Seleziona tema](/help/forms/assets/select-form-theme.png)


1. Nella scheda **[!UICONTROL Dati]**, seleziona un modello dati come **Marketo Engage**.

1. Selezionare la **[!UICONTROL Configurazione cloud]** dall&#39;elenco a discesa visualizzato nel riquadro di destra dello schermo.
Per impostazione predefinita, vengono visualizzati tutti i campi della configurazione associata. La procedura guidata consente di scegliere in modo selettivo i campi da includere nel modulo adattivo tramite l’utilizzo di caselle di controllo.

   ![Seleziona modello dati](/help/forms/assets/select-marketo-data.png)

1. Nella scheda **[!UICONTROL Invio]**, seleziona l&#39;azione di invio come **[!UICONTROL Invia a Marketo]**.

   Quando selezioni il modello dati come **Marketo Engage**, l&#39;azione di invio come **Invia a Marketo** viene selezionata automaticamente. Puoi selezionare un&#39;azione di invio diversa dalla scheda **[!UICONTROL Invio]**. Nella scheda **[!UICONTROL Invio]** vengono visualizzate tutte le azioni di invio disponibili.

   ![Invia a Marketo engagement](/help/forms/assets/select-marketo-engage.png)

1. Seleziona **[!UICONTROL Crea]**. Specifica il titolo, il nome e il percorso per salvare il modulo adattivo.

   ![Crea modulo](/help/forms/assets/create-marketo-form.png)

1. Seleziona **[!UICONTROL Crea]**.

Il modulo adattivo è ora configurato per connettersi all’istanza di Marketo Engage. In alternativa, puoi anche modificare le proprietà del modulo adattivo per modificarne la configurazione associata.

>[!TAB Editor universale]

Per configurare un nuovo modulo adattivo creato in Universal Editor per l’integrazione con Marketo Engage, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

   ![Seleziona Forms e documenti](/help/forms/assets/select-forms.png)

1. Seleziona **[!UICONTROL Crea]**  > **[!UICONTROL Moduli adattivi]**. Viene visualizzata la procedura guidata di creazione del modulo.

   ![Seleziona AF](/help/forms/assets/select-create-forms.png)

1. Nella scheda **[!UICONTROL Source]**, seleziona un modello

   ![Seleziona modelli](/help/forms/assets/select-template-ue.png)

1. Nella scheda **[!UICONTROL Dati]**, seleziona un modello dati come **Marketo Engage**.

1. Selezionare la **[!UICONTROL Configurazione cloud]** dall&#39;elenco a discesa visualizzato nel riquadro di destra dello schermo.
Per impostazione predefinita, vengono visualizzati tutti i campi della configurazione associata. La procedura guidata consente di scegliere in modo selettivo i campi da includere nel modulo adattivo tramite l’utilizzo di caselle di controllo.

   ![Seleziona modello dati](/help/forms/assets/select-marketo-data-ue.png)

1. Nella scheda **[!UICONTROL Invio]**, seleziona l&#39;azione di invio come **[!UICONTROL Invia a Marketo]**.

   Quando selezioni il modello dati come **Marketo Engage**, l&#39;azione di invio come **Invia a Marketo** viene selezionata automaticamente. Puoi selezionare un&#39;azione di invio diversa dalla scheda **[!UICONTROL Invio]**. Nella scheda **[!UICONTROL Invio]** vengono visualizzate tutte le azioni di invio disponibili.

   ![Invia a Marketo engagement](/help/forms/assets/select-marketo-engage-ue.png)

1. Seleziona **[!UICONTROL Crea]**. Specifica il titolo, il nome e il percorso per salvare il modulo adattivo.

   ![Crea modulo](/help/forms/assets/create-marketo-form.png)

1. Seleziona **[!UICONTROL Crea]**.

Il modulo adattivo è ora configurato per connettersi all’istanza di Marketo Engage. In alternativa, puoi anche modificare le proprietà del modulo adattivo per modificarne la configurazione associata.

>[!ENDTABS]

## Domande frequenti

**D: è possibile modificare l&#39;azione di invio per i moduli configurati per la connessione allo schema di Marketo Engage?**
**A:** Per impostazione predefinita, l&#39;azione **Invia a Marketo** è selezionata quando un modulo è configurato per la connessione allo schema di Marketo Engage. Tuttavia, se necessario, è possibile modificare l&#39;azione di invio per i moduli.


**D: cosa succede quando si modifica il connettore del modulo?**\
**A:** Se si modifica il connettore del modulo, le associazioni esistenti non saranno più valide.

**D: quali sono le tre operazioni disponibili nel servizio Invoke dell&#39;editor di regole per i moduli integrati con Marketo Engage?**\
**A:** Le tre operazioni predefinite disponibili in **Invoke Service** per i moduli integrati con Marketo Engage sono:

* Sincronizza lead
* Ottieni lead per ID
* Ottieni lead per tipo di filtro

## Passaggio successivo

È inoltre possibile collegare un modulo adattivo alla [libreria Munchkin](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) per tenere traccia del numero di visite, clic e invii di moduli.

## Articoli correlati

{{af-submit-action}}

## Consulta anche

{{marketo-engage-see-also}}
