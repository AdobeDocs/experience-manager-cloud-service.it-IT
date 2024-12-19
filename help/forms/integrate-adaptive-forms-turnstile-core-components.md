---
title: Come si utilizza Turnstile in un componente core modulo adattivo AEM?
description: Migliora la sicurezza dei moduli con il servizio Turnstile. Guida dettagliata all’interno!
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e9c13228-0857-4936-9c39-12ed2bddf429
source-git-commit: 709b3381eedefe7619cb961f345f202cadf512f3
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 14%

---

# Collegare l’ambiente AEM Forms con Turnstile {#connect-your-forms-environment-with-turnstile-service}

<span class="preview"> Questa funzione si trova nel programma per i primi utilizzatori. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms as a Cloud Service supporta le seguenti soluzioni CAPTCHA:


* [Turnstile](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Integrare l’ambiente AEM Forms con Turnstile Captcha

Il Turnstile Captcha di Cloudflare è una misura di sicurezza che mira a proteggere moduli e siti da bot automatizzati, attacchi dannosi, spam e traffico automatizzato indesiderato. Presenta una casella di controllo all’invio del modulo per verificare che sia umana, prima di consentire loro di inviare il modulo. AEM Forms as a Cloud Service supporta Turnstile Captcha nei componenti core di Forms adattivi.

### Prerequisiti per integrare l’ambiente AEM Forms con Turnstile Captcha {#prerequisite}

Per configurare Turnstile per i componenti core di AEM Forms, è necessario ottenere la [chiave del sito e la chiave segreta](https://developers.cloudflare.com/turnstile/get-started/) Turnstile dal sito Web Turnstile.

### Configura tornello {#steps-to-configure-hcaptcha}

Per integrare AEM Forms con il servizio Turnstile, effettuare le seguenti operazioni:

1. Crea un Contenitore di configurazione nell’ambiente AEM Forms as a Cloud Service. Un contenitore di configurazione contiene le configurazioni cloud utilizzate per collegare l’AEM a servizi esterni. Per creare e configurare un Contenitore di configurazione per collegare l’ambiente AEM Forms con Turnstile, segui i passaggi riportati di seguito:
   1. Apri la tua istanza di AEM Forms as a Cloud Service.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**.
   1. Nel browser configurazioni, crea una nuova cartella e abilita le relative configurazioni cloud, oppure abilita le configurazioni cloud per una cartella esistente come spiegato di seguito:

      * Per creare una **nuova cartella** e abilitare le relative configurazioni cloud, eseguire la procedura seguente:
         1. Nel browser configurazioni fare clic su **[!UICONTROL Crea]**.
         1. Nella finestra di dialogo Crea configurazione, specifica un nome e un titolo, quindi seleziona l&#39;opzione **[!UICONTROL Configurazioni cloud]**.
         1. Fai clic su **[!UICONTROL Crea]**.
      * Per abilitare l&#39;opzione Configurazioni cloud per una **cartella esistente**:
         1. Nel Browser configurazioni, seleziona la cartella esistente e fai clic su **[!UICONTROL Proprietà]**.
         1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
         1. Fai clic su **[!UICONTROL Salva e chiudi]** per salvare la configurazione ed uscire.

1. Configurare il Cloud Service:
   1. Nell&#39;istanza dell&#39;autore AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** e fai clic su **[!UICONTROL Turnstile]**.
      ![Turnstile nell&#39;interfaccia utente](assets/turnstile-in-ui.png)
   1. Seleziona un Contenitore di configurazione, creato o aggiornato, come descritto nella sezione precedente. Seleziona **[!UICONTROL Crea]**.
      ![Turnstile di configurazione](assets/config-hcaptcha.png)
   1. Specificare **[!UICONTROL Tipo widget]** come gestito, non interattivo o invisibile. Per ulteriori informazioni sul tipo di widget, visita [Widget tornstile](https://developers.cloudflare.com/turnstile/concepts/widget/).
   1. Specificare **[!UICONTROL Titolo]**, **[!UICONTROL Nome]**, **[!UICONTROL Chiave sito]** e **[!UICONTROL Chiave segreta]** per il servizio tornello [ottenuto nel prerequisito](#prerequisite).
   1. Fai clic su **[!UICONTROL Crea]**.

      ![Configura il Cloud Service per connettere l&#39;ambiente AEM Forms con Turnstile](assets/config-turntstile-cc.png)

   >[!NOTE]
   > Gli utenti non devono modificare l’URL di convalida JavaScript lato client e l’URL di convalida lato server, in quanto sono già precompilati per la convalida lato client.

   Una volta configurato, il servizio Captcha Turnstile è disponibile per l&#39;utilizzo in un [modulo adattivo basato su componenti core](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Utilizzare Turnstile in un modulo adattivo {#using-turnstile-core-components}

1. Apri la tua istanza di AEM Forms as a Cloud Service.
1. Vai a **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e fai clic su **[!UICONTROL Proprietà]**. Nella sezione **[!UICONTROL Contenitore configurazione]**, seleziona il Contenitore configurazione che contiene la configurazione cloud che connette AEM Forms a Turnstile.
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   Se non si dispone di un Contenitore di configurazione, vedere la sezione [Configurare il tornello](#steps-to-configure-hcaptcha) per informazioni sulla creazione di un Contenitore di configurazione.

   ![Seleziona contenitore configurazione](/help/forms/assets/captcha-properties.png)

1. Seleziona un modulo adattivo e fai clic su **[!UICONTROL Modifica]** per aprire un modulo nell&#39;editor.
1. Dal browser componenti, trascina o aggiungi il componente **[!UICONTROL Stile modulo adattivo]** al modulo adattivo.
   ![Aggiungi componente Captcha stile](/help/forms/assets/turnstile-v2.png)
1. Seleziona il componente **[!UICONTROL Stile modulo adattivo]** e fai clic sull&#39;icona ![Proprietà](assets/configure-icon.svg). Apre la finestra di dialogo delle proprietà. Specifica le seguenti proprietà:

   ![Turnstile v2](assets/turnstile-settings-for-v2.png)

   * **[!UICONTROL Nome]:** Specifica il nome per il componente Captcha. Puoi identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell&#39;editor di regole.
   * **[!UICONTROL Titolo]:** Specifica il titolo del componente Captcha. puoi consentire l’utilizzo del titolo in formato Rich Text e nascondere il titolo selezionando le caselle di controllo.
   * **[!UICONTROL Impostazioni configurazione]:** Seleziona una configurazione cloud configurata per il servizio Turnstile Captcha.
     >[!NOTE]
     >* Puoi avere più configurazioni cloud nell’ambiente per uno scopo simile. Quindi, scegli il servizio con attenzione. Se non è elencato alcun servizio, vedere la sezione [Configurazione di Turnstile](#steps-to-configure-hcaptcha) per informazioni sulla creazione di un contenitore di configurazione per la connessione dell&#39;ambiente AEM Forms al servizio Turnstile.

   * **[!UICONTROL Convalida]:** Fornisci la convalida Captcha sotto forma di messaggio di errore:

      * **Messaggio di errore:** Fornisci il messaggio di errore da visualizzare all&#39;utente quando l&#39;invio Captcha non riesce.
        >[!NOTE]
        >* Un messaggio di errore viene visualizzato solo se il CAPTCHA è compilato sul lato client.
1. Fai clic su **[!UICONTROL Fine]**.


Ora, solo le forme legittime, in cui il compilatore di moduli elimina con successo la sfida posta dal servizio Turnstile sono consentite per l&#39;invio del modulo.

![Sfida tornello](assets/turnstile-challenge.png)


## Domande frequenti

* **Q: posso utilizzare più di un componente Captcha in un modulo adattivo?**
* **Ans:** L&#39;utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare un componente Captcha in un frammento o in un pannello contrassegnato per il caricamento lento.

## Consulta anche {#see-also}

{{see-also}}
