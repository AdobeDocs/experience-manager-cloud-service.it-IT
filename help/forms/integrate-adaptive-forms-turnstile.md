---
title: Come si utilizza Turnstile in un modulo adattivo per AEM?
description: Migliora la sicurezza dei moduli con il servizio Turnstile. Guida passo passo all'interno!
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: 54914728ee892f14ab8d669051504a52942a6c01
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# Collegare l’ambiente AEM Forms con Turnstile {#connect-your-forms-environment-with-turnstile-service}

<span class="preview"> Questa funzione è disponibile nel programma di adozione anticipata. Puoi scrivere a aem-forms-ea@adobe.com dal tuo ID e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità. </span>


Il Turnstile Captcha di Cloudflare è una misura di sicurezza che mira a proteggere moduli e siti da bot automatizzati, attacchi dannosi, spam e traffico automatizzato indesiderato. Presenta una casella di controllo all’invio del modulo per verificare che sia umana, prima di consentire loro di inviare il modulo. AEM Forms as a Cloud Service supporta Turnstile Captcha in Adaptive Forms.

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Prerequisiti per integrare l’ambiente AEM Forms con Turnstile {#prerequisite}

Per configurare Turnstile per i componenti core di AEM Forms, è necessario ottenere [Chiave del sito e chiave segreta](https://developers.cloudflare.com/turnstile/get-started/) dal sito web Turnstile.

## Passaggi per configurare Turnstile per AEM Forms{#steps-to-configure-turnstile}

1. Crea un Contenitore di configurazione nell’ambiente as a Cloud Service AEM Forms. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un Contenitore di configurazione per collegare il tuo ambiente AEM Forms con Turnstile:
   1. Apri l’istanza as a Cloud Service di AEM Forms.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Nel Browser configurazioni, puoi selezionare una cartella esistente o crearne una. Puoi creare una cartella e abilitare per essa l’opzione Configurazioni cloud oppure abilitare l’opzione Configurazioni cloud per una cartella esistente:

      * **Per creare una cartella e abilitare l’opzione Configurazioni cloud**:
         1. Nel browser configurazioni, fai clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica un nome e un titolo, quindi seleziona la **[!UICONTROL Configurazioni cloud]** opzione.
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare l’opzione Configurazioni cloud per una cartella esistente:
         1. Nel browser configurazioni, seleziona la cartella e fai clic su **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

1. Configurare il Cloud Service:
   1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e seleziona **[!UICONTROL Tornello]**.
      ![Turnstile nell’interfaccia utente](assets/turnstile-in-ui.png)
   1. Seleziona un Contenitore di configurazione, creato o aggiornato, come descritto nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
      ![Tornello di configurazione](assets/config-hcaptcha.png)
   1. Specifica **[!UICONTROL Tipo di widget]** come gestito, il tipo di widget può cambiare che dipende dalla chiave ottenuta nel prerequisito, **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]**, e **[!UICONTROL Chiave segreta]** per servizio tornello [ottenuto come prerequisito](#prerequisite). Seleziona **[!UICONTROL Crea]**.

      ![Configurare il Cloud Service per collegare l’ambiente AEM Forms con Turnstile](assets/config-turntstile.png)

>[!NOTE]
> Gli utenti non devono modificare l’URL di convalida JavaScript lato client e l’URL di convalida lato server, in quanto sono già precompilati per la convalida lato client.

Una volta configurato, il servizio Turnstile Captcha è disponibile per l’utilizzo in un modulo adattivo.

## Utilizzare il tornello in un modulo adattivo{#using-turnstile-foundation-components}

1. Apri l’istanza as a Cloud Service di AEM Forms.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Proprietà]**. Per **[!UICONTROL Contenitore configurazione]** , seleziona il Contenitore di configurazione contenente la Configurazione cloud che connette AEM Forms a Turnstile e fai clic su **[!UICONTROL Salva e chiudi]**.

   Se non disponi di un contenitore di configurazione di questo tipo, consulta la sezione [Collegare l’ambiente AEM Forms con Turnstile](#connect-your-forms-environment-with-turnstile-service) per scoprire come creare un contenitore di configurazione.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un modulo adattivo e seleziona **[!UICONTROL Modifica]**. Il modulo adattivo si apre nell’editor di Forms adattivo.
1. Dal browser Componenti, trascina **[!UICONTROL Captcha]** nel modulo adattivo.
1. Seleziona la **[!UICONTROL Captcha]** e fai clic su proprietà ![Icona Proprietà](assets/configure-icon.svg) icona. Apre la finestra di dialogo delle proprietà.

   ![Impostazioni](assets/turnstile-setting-v1.png)

   Specifica le seguenti proprietà:

   * **[!UICONTROL Titolo]:** Specificando il titolo del componente Captcha, puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell’editor di regole.
   * **[!UICONTROL Messaggio di convalida]:** Fornisci un messaggio di convalida per la convalida Captcha all’invio del modulo.
   * **[!UICONTROL Convalida Captcha]:** Puoi selezionare una delle opzioni, per convalidare Captcha:
      * All’invio del modulo
      * Su un’azione dell’utente.
   * **[!UICONTROL Servizio Captcha]:** Seleziona il servizio Captcha, qui selezioni il servizio Cloudfare Turnstile Captcha.
   * **[!UICONTROL Configurazione Captcha]:** Seleziona una configurazione cloud configurata per Turnstile. ad esempio, qui puoi selezionare il **chiave gestita**.
     >[!NOTE]
     >Puoi avere più configurazioni cloud nell’ambiente per uno scopo simile. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, consulta [Collegare l’ambiente AEM Forms con Turnstile](#connect-your-forms-environment-with-turnstile-service) per scoprire come creare un Cloud Service che colleghi il tuo ambiente AEM Forms con il servizio Turnstile.

   * **Messaggio di errore:** Fornisci il messaggio di errore da visualizzare all’utente quando l’invio del Captcha non riesce.
   * **Dimensione Captcha:** Selezionate la dimensione di visualizzazione della finestra di dialogo Sfida tornello (Turnstile Challenge). Utilizza il **[!UICONTROL Compatto]** per visualizzare una dimensione ridotta e il **[!UICONTROL Normale]** per visualizzare una finestra di dialogo di sfida di tipo Turnstile di dimensioni relativamente grandi.


     >[!NOTE]
     >Questo è applicabile per il tipo di widget Gestito e Non interattivo. Se il tipo di widget è invisibile, la proprietà size non è obbligatoria ed è disabilitata.

1. Seleziona **[!UICONTROL Fine]**.

Ora, solo le forme legittime, in cui il compilatore di moduli elimina con successo la sfida posta dal servizio Turnstile sono consentite per l&#39;invio del modulo.

![Sfida tornello](assets/turnstile-challenge.png)

## Domande frequenti

* **D: Posso utilizzare più di un componente Captcha in un modulo adattivo?**
* **Ans:** L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare un componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}