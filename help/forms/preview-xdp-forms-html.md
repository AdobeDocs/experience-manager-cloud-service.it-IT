---
title: Generare l’anteprima HTML5 di un modulo XDP
description: La scheda Anteprima HTML in LiveCycle Designer può essere utilizzata per visualizzare in anteprima i moduli così come vengono visualizzati in un browser.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# Generare l’anteprima HTML5 di un modulo XDP{#generate-html-preview-of-an-xdp-form}

<span class="preview"> La funzionalità HTML5 Forms è disponibile come parte del programma di accesso anticipato. Per richiedere l’accesso, invia un’e-mail dal tuo ID e-mail ufficiale (di lavoro) a aem-forms-ea@adobe.com.
</span>

Durante la progettazione di un modulo in AEM Forms Designer, oltre a visualizzare in anteprima il rendering PDF di un modulo, puoi anche visualizzarne un rendering HTML5. È possibile utilizzare la scheda **Anteprima HTML** per visualizzare in anteprima un modulo come apparirebbe in un browser.

## Abilitare l’anteprima di HTML per i moduli XDP in Designer {#html-preview-of-forms-in-forms-designer}

Per consentire a Designer di generare l’anteprima HTML dei moduli XDP, esegui le seguenti configurazioni:

* Configurare il servizio di autenticazione Apache Sling
* Disattiva modalità protetta
* Fornisci i dettagli del server AEM Forms

### Configurare il servizio di autenticazione Apache Sling {#configure-apache-sling-authentication-service}

1. Vai a `https://'[server]:[port]'/system/console/configMgr` su AEM Forms in esecuzione su OSGi o
   `https://'[server]:[port]'/lc/system/console/configMgr` su AEM Forms in esecuzione su JEE.
1. Individua e fai clic sulla configurazione **Apache Sling Authentication Service** per aprirla in modalità di modifica.

1. A seconda che AEM Forms sia in esecuzione su OSGi o JEE, aggiungi quanto segue nel campo **Requisiti di autenticazione**:

   * AEM Forms su JEE

      * -/content/xfaforms
      * -/etc/clientlibs

   * AEM Forms su OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >Non copiare e incollare il valore specificato nel campo Requisiti di autenticazione in quanto potrebbe danneggiare i caratteri speciali nel valore. Digita invece il valore specificato nel campo.

1. Specificare un nome utente e una password rispettivamente nei campi **[!UICONTROL Nome utente anonimo]** e **[!UICONTROL Password utente anonimo]**. Le credenziali specificate vengono utilizzate per gestire l&#39;autenticazione anonima e consentire l&#39;accesso agli utenti anonimi.
1. Fai clic su **Salva** per salvare la configurazione.

### Disattiva modalità protetta {#disable-protected-mode}

La **modalità protetta** è attivata per impostazione predefinita. Tienilo abilitato per gli ambienti di produzione. È possibile disattivarlo per un ambiente di sviluppo per visualizzare in anteprima HTML5 Forms in desinger. Per disattivarla, effettua le seguenti operazioni:

1. Accedi ad AEM Web Console come amministratore.

   * L&#39;URL per AEM Forms su OSGi è `https://'[server]:[port]'/system/console/configMgr`
   * L&#39;URL per AEM Forms su JEE è `https://'[server]:[port]'/lc/system/console/configMgr`

1. Apri **[!UICONTROL Configurazioni Forms mobile]** per la modifica.
1. Deseleziona l&#39;opzione **[!UICONTROL Modalità protetta]** e fai clic su **[!UICONTROL Salva]**.

### Fornisci i dettagli del server AEM Forms {#provide-details-of-aem-forms-server}

1. In Designer, vai a **Strumenti** > **Opzioni**.
1. Nella finestra Opzioni, selezionare la pagina **Opzioni server**, fornire i dettagli seguenti e fare clic su **OK**.

   * **URL server**: URL server AEM Forms.

   * **Numero porta HTTP**: porta del server AEM. Il valore predefinito è 4502.
   * **Contesto anteprima HTML:** Percorso del profilo per il rendering dei moduli XFA. I seguenti profili predefiniti vengono utilizzati per visualizzare in anteprima il modulo in Designer. Tuttavia, puoi anche specificare il percorso di un profilo personalizzato.

      * `/content/xfaforms/profiles/default.html` (AEM Forms su OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms su JEE)

   * **Contesto di Forms Manager:** Percorso contestuale in cui viene distribuita l&#39;interfaccia utente di Forms Manager. I valori predefiniti sono:

      * `/aem/forms` (AEM Forms su OSGi)
      * `/lc/forms` (AEM Forms su JEE)

   >[!NOTE]
   >
   >Verifica che il server AEM Forms sia in esecuzione. L&#39;anteprima HTML si connette al server CRX per *generare* un&#39;anteprima.

   ![Opzioni AEM Forms Designer &#x200B;](assets/server_options.png)

   Opzioni AEM Forms Designer

1. Per visualizzare in anteprima un modulo in HTML, fare clic sulla scheda **Anteprima HTML**.

   >[!NOTE]
   >
   >
   >
   >
   >    * Se la scheda Anteprima HTML è chiusa, premere F4 per aprire la scheda Anteprima HTML. Per aprire la scheda Anteprima HTML, è anche possibile selezionare Anteprima HTML dal menu Visualizza.
   >    * L&#39;anteprima HTML non supporta i documenti PDF, l&#39;anteprima HTML è solo per i documenti XDP.
   >
   >

   >[!CAUTION]
   >
   >Per testare la reale esperienza dell’utente finale, puoi anche visualizzare in anteprima i moduli in browser esterni (Google Chrome, Microsoft Edge, Mozilla Firefox e altro). Ogni browser utilizza un motore separato per eseguire il rendering di HTML, quindi ci potrebbero essere alcune differenze nel modo in cui un modulo viene visualizzato in anteprima in Designer e nel browser esterno.

## Per visualizzare in anteprima un modulo utilizzando dati di esempio {#to-preview-a-form-using-sample-data}

Designer consente di visualizzare in anteprima e verificare il modulo utilizzando dati XML di esempio. Si consiglia di verificare frequentemente il modulo con dati di esempio per verificare che venga eseguito correttamente il rendering.

Se non disponi di dati di esempio, puoi crearli direttamente in Designer. (Vedi [Per generare automaticamente i dati di esempio per l&#39;anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) e [Per creare i dati di esempio per l&#39;anteprima del modulo](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Il test del modulo tramite un&#39;origine dati di esempio assicura che i dati e i campi siano mappati e che le sottomaschere ripetute vengano ripetute come previsto. È possibile creare un layout di modulo bilanciato che fornisca lo spazio appropriato per ogni oggetto per visualizzare i dati uniti.

1. Selezionare **File > Proprietà modulo**.

1. Fare clic sulla scheda **Anteprima** e nella casella File di dati digitare il percorso completo del file di dati di prova. È inoltre possibile utilizzare il pulsante Sfoglia per passare al file.

1. Fare clic su **OK**. Alla successiva anteprima del modulo nella scheda **Anteprima HTML**, i valori dei dati del file XML di esempio verranno visualizzati nei rispettivi oggetti.

## Anteprima dei moduli in un archivio {#html-preview-of-forms-in-forms-manager}

In AEM Forms è possibile visualizzare in anteprima moduli e documenti in un repository. L’anteprima consente di sapere esattamente come si presentano e si comportano i moduli per gli utenti finali.
