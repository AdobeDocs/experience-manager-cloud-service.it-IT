---
title: Utilità di migrazione per convertire Forms adattivo basato su componenti di base in moduli basati su componenti di base
description: Scopri come installare e utilizzare l’utility di migrazione per convertire Forms adattivo basato su componenti Foundation in moduli basati su componenti core.
Keywords: Migration Utility tool, Convert Adaptive Forms based on foundation components to core component based forms, Convert Foundation forms to Core components forms, Using Modernizer tool to convert Foundation Components to Core components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 1%

---


# Introduzione

È possibile utilizzare l’utility di migrazione per convertire Forms adattivo basato su componenti di base in moduli basati su componenti di base. È possibile utilizzare [Strumento di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/) come strumento di utilità di migrazione. Il [Strumenti di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/) fornisce una suite di utility utilizzate per convertire Forms adattivo basato su componenti di base in funzionalità moderne e supportate dei componenti di base.

## Cos’è l’AEM Modernize Tools?

[Strumenti di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/) si riferisce a un insieme di utility o applicazioni software progettate per facilitare il processo di modernizzazione o aggiornamento dei progetti Adobe Experience Manager (AEM). Questi strumenti in genere aiutano a convertire i vecchi componenti o funzionalità all’interno dell’AEM in alternative più recenti, più efficienti e supportate.

Gli strumenti di modernizzazione AEM convertono i Forms adattivi basati su componenti di base meno recenti in nuovi moduli basati su componenti di base più recenti. Questo processo di conversione garantisce l’allineamento dei moduli agli standard e alle funzionalità più recenti, migliorando potenzialmente le prestazioni, la compatibilità e la facilità di manutenzione all’interno dell’ambiente AEM.

![Strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> Si consiglia di installare gli strumenti di modernizzazione AEM nell’installazione locale dell’AEM. Migrare i moduli basati su Foundation ai moduli basati su componenti di base. Scarica il modulo e le relative risorse. Quindi, carica il modulo e le relative risorse nell’ambiente richiesto.

## Prerequisiti per utilizzare gli strumenti di modernizzazione AEM

* [Configurare l’ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md)
* [Abilita i componenti core Adaptive Forms per il tuo ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Aggiungi i tuoi utenti al [!DNL forms-users] gruppo. I membri della [!DNL forms-users] dispongono delle autorizzazioni per creare un modulo adattivo.

* Gli utenti con i seguenti ruoli dispongono delle autorizzazioni per installare gli strumenti di modernizzazione AEM in un ambiente AEM:
   * Ruolo Sviluppatore
   * Ruolo amministratore Per un elenco dettagliato dei gruppi di utenti specifici per i moduli, consulta [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

## Installare e configurare gli strumenti di modernizzazione AEM

Passaggi per installare e configurare gli strumenti di modernizzazione AEM:

1. [Installare gli strumenti di modernizzazione AEM nell’ambiente AEM Forms locale](#install-aem-modernize-tools)
2. [Abilitare gli strumenti di modernizzazione AEM per l’ambiente AEM Forms locale](#enable-aem-modernize-tools)

### Installare gli strumenti di modernizzazione AEM nell’ambiente AEM Forms locale {#install-aem-modernize-tools}

Per installare gli strumenti di modernizzazione AEM nell’ambiente AEM Forms locale, effettua le seguenti operazioni:

1. Avvia il servizio di authoring AEM locale eseguendo quanto segue dalla riga di comando:

   `java -jar aem-author-p4502.jar`

   >[!NOTE]
   >
   > Immetti la password amministratore come `admin`. Qualsiasi password amministratore è accettabile, tuttavia si consiglia di utilizzare l’impostazione predefinita per lo sviluppo locale per ridurre la necessità di riconfigurare.

1. Clona il [Strumenti di modernizzazione AEM](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) nel sistema locale.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tools]
   ```
   Sostituisci il [Percorso dell’archivio Git degli strumenti di modernizzazione AEM] con l’URL effettivo dell’archivio Git corrispondente degli strumenti di modernizzazione AEM.
Dopo aver eseguito correttamente il comando, nel computer è disponibile una copia locale dell’archivio degli strumenti di modernizzazione AEM.

1. Accedi a`[AEM Modernize Tools Repository]`  nel sistema locale.
1. Esegui il comando seguente:

   ```Shell
       mvn clean install 
   ```
![Immagine di installazione completata](/help/forms/assets/aem-modernize-install-steps.png)

Una volta completata l’installazione, gli strumenti di modernizzazione AEM diventano disponibili per il tuo ambiente.

![Abilita strumenti di modernizzazione AEM](/help/forms/assets/enable-aem-modernizer-tools.png)


### Abilitare gli strumenti di modernizzazione AEM per l’ambiente AEM Forms locale{#enable-aem-modernize-tools}

Per abilitare e utilizzare gli strumenti di modernizzazione AEM per l’ambiente AEM in uso, è importante mappare le regole per la migrazione dei componenti di base ai componenti core:

1. Accedi all’istanza di authoring.
1. Accedi a `http://[host]:[port]/system/console/configMgr`
1. Trova e modifica il `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Aggiungi il `Component Rule Paths` as `/apps/forms-modernizer/rules`.
1. Clic **Salva** per salvare le modifiche.

![Regola componente di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Eseguire gli strumenti di modernizzazione AEM per convertire i moduli basati su componenti di base in moduli basati su componenti di base

1. Vai a **[!UICONTROL Strumenti > Strumenti di modernizzazione AEM > Conversione Forms]**.

   ![Seleziona strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-select.png)

1. Seleziona la **[!UICONTROL Conversione Forms]** opzione.

   ![Seleziona opzione di conversione Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Clic **Crea** per creare un nuovo processo.

   ![Processo di creazione strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Specifica la **[!UICONTROL Nome processo]**.
1. In **[!UICONTROL Modulo]** , è possibile selezionare una delle seguenti opzioni:
   * **Nessuno** : seleziona questa opzione se la gestione dei moduli non è richiesta.
   * **Ripristina** : seleziona questa opzione per ripristinare lo stato del modulo precedente all’ultima conversione.
   * **Copia in Target**: seleziona questa opzione per copiare il modulo prima di eseguire la conversione.
Nel nostro caso, il **Copia in Target** è selezionata. Se il **Copia in Target** è selezionata, la **[!UICONTROL Percorso di origine]** e **[!UICONTROL Percorso di destinazione]** diventano visibili.

1. Specifica la `source folder` nome in **[!UICONTROL Percorso di origine]**.
1. Specifica la `target folder` nome in **[!UICONTROL Percorso di destinazione]**.
1. Seleziona **[!UICONTROL Avanti]**.
1. Fai clic su **[!UICONTROL Aggiungi Forms]**. Tutti i moduli in `source folder` viene visualizzato sullo schermo.
1. Seleziona il modulo basato su componenti di base per convertirlo in modulo basato su componenti di base. È inoltre possibile selezionare più moduli.

   ![Modulo di selezione strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Clic **[!UICONTROL Seleziona]**.
1. Clic **[!UICONTROL Pianifica processo]** per avviare il processo di conversione.
1. Clic **[!UICONTROL Converti]** dal **[!UICONTROL Converti pagine]** .

   ![Strumenti di modernizzazione AEM per convertire le pagine](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Quando lo stato del processo viene modificato in `success`. Accedi a `target folder` per visualizzare il modulo convertito.

   ![Strumenti di modernizzazione AEM riusciti](/help/forms/assets/aem-modernize-tools-success.png)

1. Seleziona il modulo adattivo e fai clic su > **[!UICONTROL Proprietà]**. Viene visualizzata la pagina Proprietà modulo.
   ![Cartella di destinazione degli strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare nuovamente le proprietà del modulo convertito.
   ![Proprietà modulo adattivo degli strumenti di modernizzazione AEM](/help/forms/assets/aem-modernize-tools-af-properties.png)

Ora puoi vedere che il Modulo adattivo basato su componenti di base si trasforma nel Modulo adattivo basato su componenti di base.

## Considerazioni durante l&#39;utilizzo dello strumento Utilità di migrazione {#considerations}

* Se il modulo basato su componenti di base contiene regole di funzioni personalizzate, è necessario riscrivere tali regole per il modulo convertito basato su componenti di base.
* Il modulo convertito non include regole nell’editor di regole, che richiedono la riscrittura delle regole per il modulo convertito.
* È necessario ricreare il processo di traduzione per il modulo convertito.

## Best practice {#best-practices}

* Il modulo basato su componenti di base include solo i componenti presenti nei componenti basati su componenti di base.
* Verificare che le regole siano formattate in XML.


