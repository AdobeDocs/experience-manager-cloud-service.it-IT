---
title: Utilità di migrazione Strumenti/Strumenti di modernizzazione AEM per convertire Forms adattivo basato su componenti di base in moduli basati su componenti di base
description: Scopri come installare e utilizzare l’utilità di migrazione e gli strumenti di modernizzazione AEM per convertire i Forms adattivi basati su componenti di base in moduli basati su componenti di base.
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 5%

---

# Introduzione

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

L&#39;utilità di conversione di Forms, parte della suite dello strumento di modernizzazione [AEM](https://opensource.adobe.com/aem-modernize-tools/), consente di convertire facilmente Forms adattivo creato con i componenti Foundation legacy in moduli che sfruttano le funzionalità moderne e supportate dei componenti core.

## Cos’è AEM Modernize Tools?

[Strumenti di modernizzazione di AEM](https://opensource.adobe.com/aem-modernize-tools/) fa riferimento a un insieme di utilità o applicazioni software progettate per facilitare il processo di modernizzazione o aggiornamento dei progetti Adobe Experience Manager (AEM). Questi strumenti in genere aiutano a convertire i componenti o le funzionalità meno recenti di AEM in alternative più recenti, più efficienti e supportate. Forms Conversion Utility viene installato in Strumenti di modernizzazione AEM per convertire i Forms adattivi basati su componenti di base in moduli basati su componenti di base.

Forms Conversion Utility converte i Forms adattivi basati su componenti Foundation precedenti in moduli basati su componenti core più recenti. Questo processo di conversione garantisce l’allineamento dei moduli agli standard e alle funzionalità più recenti, migliorando potenzialmente le prestazioni, la compatibilità e la facilità di manutenzione all’interno dell’ambiente AEM.

![Strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>Si consiglia di installare gli Strumenti di modernizzazione AEM nella configurazione AEM locale. Migrare il Forms adattivo basato su componenti di base ai moduli basati su componenti di base. Scarica il modulo e le relative risorse. Quindi, carica il modulo e le relative risorse nell’ambiente richiesto.

## Considerazioni durante l’utilizzo degli strumenti AEM di modernizzazione {#considerations}

* In caso di conversioni corrette, tutte le regole applicate al modulo vengono rimosse. Le regole non vengono migrate automaticamente. È necessario ricreare e applicare manualmente queste regole al modulo convertito.
* Le impostazioni di traduzione utilizzate nel modulo originale non vengono riportate. Riconfigura la traduzione per il modulo convertito.
* Se il modulo basato su Componenti Foundation contiene script o regole di funzione personalizzate, è necessario riscriverli per il modulo convertito basato su Componenti core.
* I seguenti componenti di base OOTB non sono ancora supportati nei Componenti core e vengono quindi eliminati nel modulo convertito:

   * Blocco Adobe Sign
   * Grafico
   * Elenco allegato file
   * Segnaposto Nota a piè di pagina
   * Scelta immagine
   * Pulsante Avanti
   * Pulsante precedente
   * Firma scarabocchio
   * Passaggio di riepilogo
   * Barra degli strumenti

## Prerequisiti per utilizzare gli strumenti di modernizzazione AEM

* [Configura l&#39;ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md).
* Installa la versione più recente per abilitare i componenti core Adaptive Forms per il tuo ambiente AEM Cloud Service.
* Aggiungi gli utenti al gruppo [!DNL forms-users]. I membri del gruppo [!DNL forms-users] dispongono delle autorizzazioni per creare un modulo adattivo.
* Gli utenti con i seguenti ruoli dispongono delle autorizzazioni per installare gli strumenti di modernizzazione AEM all’interno di un ambiente AEM:

   * Ruolo Sviluppatore
   * Ruolo amministratore

Per un elenco dettagliato dei gruppi di utenti specifici per i moduli, vedere [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

## Installare e configurare gli strumenti di modernizzazione AEM

Per installare e configurare gli strumenti di modernizzazione AEM:

1. [Installare gli strumenti di modernizzazione AEM nell’ambiente AEM Forms locale](#install-aem-modernize-Tools)
1. [Abilitare gli strumenti di modernizzazione AEM per il tuo ambiente AEM Forms locale](#enable-aem-modernize-Tools)

### Installare gli strumenti di modernizzazione AEM nell’ambiente AEM Forms locale {#install-aem-modernize-Tools}

Per installare gli strumenti di modernizzazione AEM nell’ambiente AEM Forms locale, effettua le seguenti operazioni:

1. Apri il prompt dei comandi o il terminale.
1. Avvia il servizio AEM Author locale. Ad esempio, esegui il seguente codice da per avviare l’istanza AEM Author locale:

   `java -jar aem-author-p4502.jar`

1. Clona l&#39;archivio dello strumento di modernizzazione [AEM](https://github.com/adobe/forms-modernizer) nel sistema locale.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   Dopo aver eseguito correttamente il comando, nel computer è disponibile una copia locale dell’archivio dello strumento AEM Modernize Tool.

1. Passare a `[AEM Modernize Tool Repository]` nel sistema locale.
1. Esegui il comando seguente:

   ```Shell
       mvn clean install 
   ```

![Immagine di installazione completata](/help/forms/assets/aem-modernize-install-steps.png)

Dopo l’installazione, gli strumenti AEM di modernizzazione diventano disponibili per il tuo ambiente.

![Abilita Utilità di migrazione AEM](/help/forms/assets/enable-aem-modernizer-tools.png)


### Abilitare gli strumenti di modernizzazione AEM per il tuo ambiente AEM Forms locale{#enable-aem-modernize-Tools}

Per abilitare e utilizzare gli strumenti di modernizzazione AEM per il tuo ambiente AEM, è importante mappare le regole per la migrazione dei Componenti di base ai Componenti core:

1. Accedi all’istanza di authoring.
1. Passa a `http://[host]:[port]/system/console/configMgr`
1. Trova e modifica `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Aggiungi `Component Rule Paths` come `/apps/forms-modernizer/rules`.
1. Fai clic su **Salva** per salvare le modifiche.

![Regola componente di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Esegui l’utility di conversione moduli per convertire i moduli basati su Componenti Foundation in moduli basati su Componenti core

1. Vai a **[!UICONTROL Strumenti > Strumenti di modernizzazione AEM > Conversione Forms]**.

   ![Seleziona strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Selezionare l&#39;opzione **[!UICONTROL Conversione Forms]**.

   ![Seleziona opzione di conversione Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Fai clic su **Crea** per creare un nuovo processo.

   ![Processo di creazione strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Specifica il **[!UICONTROL nome processo]**.
1. Nella scheda **[!UICONTROL Modulo]** è possibile selezionare una delle opzioni seguenti:

   * **Nessuno**: selezionare l&#39;opzione se non si desidera creare una copia dei moduli basati sul componente Foundation prima di avviare la conversione del modulo.
   * **Ripristina**: selezionare l&#39;opzione per ripristinare lo stato del modulo prima di avviare la conversione.
   * **Copia in Target**: selezionare l&#39;opzione per creare una copia dei moduli basati sul componente di base prima di avviare la conversione del modulo.

   Nel nostro caso, l&#39;opzione **Copia in Target** è selezionata. Se l&#39;opzione **Copia in Target** è selezionata, le opzioni **[!UICONTROL Percorso Source]** e **[!UICONTROL Percorso Target]** diventano visibili.

1. Specificare il nome `source folder` nel **[!UICONTROL percorso Source]**.
1. Specificare il nome `target folder` nel **[!UICONTROL percorso di destinazione]**.
1. Seleziona **[!UICONTROL Avanti]**.
1. Fai clic su **[!UICONTROL Aggiungi Forms]**. Tutti i moduli in `source folder` vengono visualizzati sullo schermo.
1. Seleziona il Forms adattivo basato su componenti di base per convertirlo in moduli basati su componenti di base. È inoltre possibile selezionare più moduli.

   ![Modulo di selezione strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Fai clic su **[!UICONTROL Seleziona]**.
1. Fai clic su **[!UICONTROL Pianifica processo]** per avviare il processo di conversione.
1. Fare clic su **[!UICONTROL Converti]** nella finestra di dialogo **[!UICONTROL Converti pagine]**.

   ![Strumenti di modernizzazione AEM per la conversione delle pagine](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Quando lo stato del processo viene modificato in `success`. Passare a `target folder` per visualizzare il modulo convertito.

   ![Strumenti di modernizzazione AEM completati](/help/forms/assets/aem-modernize-tools-success.png)

1. Seleziona il modulo adattivo e seleziona > **[!UICONTROL Proprietà]**. Viene visualizzata la pagina Proprietà modulo.

   ![Cartella di destinazione degli strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Selezionare **[!UICONTROL Salva e chiudi]** per salvare nuovamente le proprietà del modulo convertito.
   ![Proprietà modulo adattivo per strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-af-properties.png)

Ora puoi vedere che il modulo adattivo basato su componenti di base si trasforma nel modulo adattivo basato su componenti di base.

## Best practice {#best-practices}

* Assicurati che i moduli basati su Componenti di base utilizzino solo i componenti con un [Componenti core](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) equivalente disponibile. Nei casi in cui utilizzi componenti di base che non hanno un componente core equivalente, il componente di base non viene convertito. Di conseguenza, non funziona correttamente durante la creazione di un modulo
* Assicurati che le regole per convertire i Componenti di base in Componenti core siano formattate in XML.
