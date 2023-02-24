---
title: Come migrare da un Forms Forms AEM 6.5 e AEM 6.4 a [!DNL AEM Forms] Ambiente as a Cloud Service?
description: Migrare da un [!DNL AEM Forms] Ambiente locale su [!DNL AEM Forms] Ambiente as a Cloud Service
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: b11979acc23efe5f1af690443180a6b456d589ed
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 5%

---

# Migrare a [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

Puoi eseguire la migrazione di Forms adattivo, temi, modelli e configurazioni cloud da <!-- AEM 6.3 Forms--> AEM 6.4 Forms su OSGi e AEM Forms 6.5 su OSGi a [!DNL AEM] as a Cloud Service. Prima di eseguire la migrazione di queste risorse, utilizza l&#39;utility di migrazione per convertire il formato utilizzato nelle versioni precedenti nel formato utilizzato in [!DNL AEM] as a Cloud Service. Quando esegui l&#39;utilità di migrazione, vengono aggiornate le risorse seguenti:

* Componenti personalizzati per Forms adattivo
* Modelli e temi per Forms adattivi
* Configurazioni cloud
* Gli script dell’editor di codice vengono convertiti in funzioni riutilizzabili e applicati alle regole visive.

## Considerazioni {#consideration}

* Il servizio consente di eseguire la migrazione del contenuto solo da [!DNL AEM Forms] negli ambienti OSGi. Migrazione dei contenuti da [!DNL AEM Forms] su JEE in un ambiente di Cloud Service non supportato.

* (Solo per AEM 6.3 Forms o un ambiente di versione precedente aggiornato a AEM 6.4 Forms o AEM 6.5 Forms) Forms adattivo basato su modelli e temi predefiniti disponibili in AEM 6.3 Forms o versione precedente non sono supportati in [!DNL AEM Forms] as a Cloud Service.

* Il passaggio Verifica non è disponibile. Rimuovi il passaggio di verifica dal Forms adattivo esistente prima di spostare tali moduli in un ambiente di Cloud Service.

* Il Passaggio firma per Adattivo Forms non è disponibile. Rimuovi il passaggio Firma da un modulo adattivo esistente. Configura il modulo adattivo per utilizzare l’esperienza di firma nel browser. All’invio di un modulo adattivo, mostra il consenso di Adobe Acrobat Sign alla firma del contratto all’interno del browser. L’esperienza di firma nel browser consente di rendere più rapida l’operazione e di far risparmiare tempo al firmatario.

## Differenza con AEM 6.5 Forms

| Funzione obsoleta | Differenza con AEM 6.5 Forms |
|--------------|-----------|
| HTML5 Forms (Mobile Forms) | Il servizio non supporta HTML5 Forms (Mobile Forms). Se esegui il rendering dei moduli basati su XDP come HTML5 Forms, puoi continuare a utilizzare la funzione su Forms 6.5. |
| Moduli adattivi | <li><b>Forms adattivo basato su XSD:</b> Il servizio non supporta HTML5 Forms (Mobile Forms). Se esegui il rendering dei moduli basati su XDP come HTML5 Forms, puoi continuare a utilizzare la funzione su Forms 6.5. </li> <li><b> Modelli di modulo adattivo:</b> Utilizza la pipeline di compilazione e l’archivio Git corrispondente del programma per importare i modelli di moduli adattivi esistenti. </li><li><b>Editor di regole:</b> AEM Forms as a Cloud Service fornisce un [Editor di regole](rule-editor.md#visual-rule-editor). L&#39;editor di codice non è disponibile su Forms as a Cloud Service. L’utility di migrazione consente di migrare i moduli con regole personalizzate (create nell’editor di codice). L&#39;utility converte tali regole in funzioni personalizzate supportate su Forms as a Cloud Service. È possibile utilizzare le funzioni riutilizzabili con l&#39;editor di regole per continuare a ottenere i risultati ottenuti con gli script di regole Il `onSubmitError` o `onSubmitSuccess` Le funzioni sono ora disponibili come azioni nell’editor di regole. </li> <li><b>Progetti e osservazioni:</b> Il servizio non conserva i metadati per le bozze e invia Adaptive Forms. </li> <li><b> Servizio di precompilazione:</b> Per impostazione predefinita, il servizio di precompilazione unisce i dati con un modulo adattivo sul client anziché con l’unione dei dati sul server in Forms 6.5 AEM. Questa funzione consente di migliorare il tempo necessario per precompilare un modulo adattivo. È sempre possibile configurare l&#39;esecuzione dell&#39;azione di unione sul server Adobe Experience Manager Forms. </li><li><b>Azioni di invio:</b> La **Invia e-mail come PDF** azione non disponibile. La **E-mail** l’azione di invio fornisce opzioni per l’invio di allegati e allega documento di record (DoR) con e-mail. </li> |
| Modello dati modulo | <li>Il modello dati Forms supporta solo endpoint HTTP e HTTP per l’invio dei dati. </li><li>Forms as a Cloud Service consente di utilizzare Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive e i servizi che supportano le operazioni CRUD generali (creazione, lettura, aggiornamento ed eliminazione) come archivi di dati. Il servizio non supporta il connettore JDBC, SSL reciproco per il connettore Rest e l’autenticazione basata su certificato x509 per le origini dati SOAP. </li> |
| Servizio automated forms conversion | Il servizio non fornisce un metamodello per il servizio di Automated forms conversion. È possibile [scaricarlo dalla documentazione di Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model). |
| Configurazioni | <li>Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) per abilitare le porte per l’invio di e-mail e per abilitare il protocollo SMTP per l’ambiente. </li> <li>Se utilizzi i bundle personalizzati, ricompila il codice con l&#39;ultima versione di adobe-aemfd-docmanager prima di utilizzare questi bundle con Forms as a Cloud Service.</li> |
| API di manipolazione documenti (servizio Assembler) | Il servizio non supporta operazioni dipendenti da altri servizi o applicazioni: <li>La conversione di documenti in formato non PDF in formato PDF non è supportata. Ad esempio, Microsoft Word in PDF, Microsoft Excel in PDF e HTML in PDF non sono supportati</li><li>Adobe Le conversioni basate su Distiller non sono supportate. Ad esempio, da PostScript(PS) a PDF</li><li>Le conversioni basate su servizi Forms non sono supportate. Ad esempio, da XDP a PDF forms.</li><li>Il servizio non supporta la conversione di un PDF o di un PDF trasparente con firma in un altro formato di PDF.</li> |

## Prerequisiti {#prerequisites}

* [Abilita Forms - Registrazione digitale](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) opzione attivata per il programma di Cloud Service Forms e [eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   ![Risultato esecuzione di prova](assets/enable-add-on.png)

* In un ambiente di Cloud Service, l&#39;utility Migration funziona insieme allo strumento User Mapping e allo strumento Content Transfer (Trasferimento contenuti). L&#39;utilità di migrazione rende [!DNL AEM Forms] le risorse compatibili con il Cloud Service e lo strumento di trasferimento dei contenuti migrano il contenuto dal [!DNL AEM Forms] ambiente a un [!DNL AEM] Ambiente as a Cloud Service. Prima di utilizzare l&#39;utility di migrazione, scopri il processo di [spostamento a AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). Il processo prevede due strumenti:
   * [Strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): Lo strumento di mappatura utente consente di mappare i tuoi utenti con gli account utente Adobe IMS corrispondenti.
   * [Strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): Lo strumento Content Transfer (Trasferimento contenuti) consente di preparare e trasferire i contenuti dall’ambiente esistente a un ambiente di Cloud Service.
* Account con privilegi di amministratore su [!DNL AEM Forms] as a Cloud Service e locale [!DNL AEM Forms] ambiente.
* Scaricare e installare Best Practice Analyzer, Content Transfer Tool e [!DNL AEM Forms] Utilità di migrazione da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)

* Esegui il [Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) e risolvi il problema segnalato.

<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## Migrare [!DNL AEM Forms] assets  {#use-the-migration-utility}

Esegui i seguenti passaggi per effettuare [!DNL AEM Forms] risorse compatibili con il Cloud Service e trasferirle in un [!DNL AEM] Ambiente as a Cloud Service.

1. Crea un [clone](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) della tua [!DNL AEM Forms] ambiente.

   Utilizza sempre l’ambiente clonato per eseguire lo strumento Content Transfer (Trasferimento contenuti) e l’utility Migration (Migrazione). Lo strumento Content Transfer (Trasferimento contenuti) e l’utility Migration (Migrazione) apportano alcune modifiche al contenuto e alle risorse. Pertanto, non eseguire lo strumento Content Transfer (Trasferimento contenuti) e l&#39;utility Migration (Migrazione) in un ambiente di produzione.

1. Accedi all’ambiente clonato con privilegi amministrativi.

1. Esegui il [Strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) per mappare i tuoi utenti con gli account utente Adobe IMS corrispondenti. È necessario che gli account utente Adobe IMS effettuino l’accesso a un [!DNL AEM Forms] Istanza as a Cloud Service.

1. Scarica e installa la [Strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) e [!DNL AEM Forms] Utilità di migrazione as a Cloud Service da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) sull’ambiente clonato. È possibile utilizzare Gestione pacchetti AEM per installare lo strumento e l&#39;utility.

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Migrazione dei contenuti]**.

1. Apri **[!UICONTROL Preparare Forms per la migrazione]** il Card. Il browser visualizza cinque opzioni:
   * **[!UICONTROL Migrazione risorse AEM Forms]**
   * **[!UICONTROL Migrazione adattata dei componenti personalizzati Forms]**
   * **[!UICONTROL Migrazione dei modelli Forms adattivi]**
   * **[!UICONTROL Migrazione configurazioni AEM Forms Cloud]**
   * **[!UICONTROL Migrazione script dell’Editor di codice]**

1. Utilizza l&#39;opzione una dopo l&#39;altra per rendere il tuo [!DNL AEM Forms] risorse compatibili con [!DNL AEM] as a Cloud Service:

   1. Tocca **[!UICONTROL Migrazione di AEM Forms Assets]** e nella schermata successiva, tocca **[!UICONTROL Avvia migrazione]**. Rende Adattivo Forms e temi sui vostri [!DNL AEM Forms] compatibile con [!DNL AEM] as a Cloud Service .

   1. Tocca **[!UICONTROL Migrazione adattata dei componenti personalizzati Forms]** e nella pagina Migrazione componenti personalizzati , tocca **[!UICONTROL Avvia migrazione]**. Rende qualsiasi componente personalizzato sviluppato per le sovrapposizioni di componenti e Forms adattivi sul tuo [!DNL AEM Forms] compatibile con [!DNL AEM] as a Cloud Service .

   1. Tocca **[!UICONTROL Migrazione adattata dei modelli Forms]** e nella pagina Migrazione componenti personalizzati , tocca **[!UICONTROL Avvia migrazione]**. Rende i modelli di moduli adattivi in /apps o /conf e creati utilizzando AEM Editor modelli compatibili con [!DNL AEM] as a Cloud Service .

   1. Tocca **[!UICONTROL Migrazione delle configurazioni di AEM Forms Cloud]** quindi nella pagina Migrazione configurazione, tocca **[!UICONTROL Avvia migrazione]**. Aggiorna e sposta i seguenti Cloud Services in una nuova posizione:

      * Cloud Service Modello dati modulo
      * Cloud Service Google reCAPTCHA
      * [!DNL Adobe Sign] Servizio cloud
      * Cloud Service Adobe Fonts
   1. Tocca **[!UICONTROL Migrazione script dell’Editor di codice]**, specifica una posizione in cui salvare le funzioni riutilizzabili e tocca **[!UICONTROL Avvia migrazione].

   Il Cloud Service non supporta gli script dell&#39;editor di regole. La **[!UICONTROL Migrazione degli script dell’editor di codice]** lo strumento converte tutti gli script di regole nell’ambiente in funzioni riutilizzabili e applica le funzioni riutilizzabili all’editor visivo nella posizione appropriata. Queste funzioni riutilizzabili vengono salvate sotto forma di librerie client e consentono di mantenere intatte le funzionalità esistenti. Lo strumento applica automaticamente le funzioni riutilizzabili generate al corrispondente Forms adattivo.

   Utilizza la [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) per esportare le funzioni riutilizzabili (librerie client) in un pacchetto.

1. [Distribuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) il pacchetto funzioni riutilizzabili (librerie client), [codice personalizzato, componenti, configurazioni](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), librerie personalizzate specifiche per le impostazioni internazionali [!DNL AEM] Ambiente as a Cloud Service.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Esegui il [Strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). Quando si specificano i parametri in **[!UICONTROL Crea set di migrazione]** specifica il percorso di Forms adattivo, temi, modelli, modelli di dati dei moduli, Cloud Services, componenti personalizzati e altre risorse specifiche di AEM Forms per **[!UICONTROL Percorsi da includere]** opzione . Aggiunge specificato [!DNL AEM Forms] risorse da impostare per la migrazione.

## Percorsi di varie risorse specifiche di AEM Forms

* **Forms adattivo**: Puoi trovare i moduli adattivi all’indirizzo `/content/dam/formsanddocuments/`e /content/forms/af. Ad esempio, per un modulo adattivo denominato WKND Registration, aggiungere percorsi `/content/dam/formsanddocuments/wknd-registration` e `/content/forms/af/wknd-registration`.
* **Modalità dati modulo**: Puoi trovare tutti i modelli di dati modulo in `/content/dam/formsanddocuments-fdm`. Esempio: `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Librerie client**: Il percorso predefinito delle librerie client è `/etc/clientlibs/fd/theme`.

* **Modelli di modulo adattivi**: Il percorso predefinito dei modelli è `/conf/<template folder>`. Ad esempio, per un modello denominato percorso di aggiunta di base `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temi di moduli adattivi e librerie client**: Il percorso predefinito dei temi è ` /content/dam/formsanddocuments-themes/` e il percorso predefinito delle librerie client è `/etc/clientlibs/fd/theme`. Ad esempio, per un modello denominato Tema WKND aggiungi percorso ` /content/dam/formsanddocuments-themes/wkndtheme` e le librerie client per il tema in `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Puoi anche avere temi e librerie client in altri percorsi personalizzati.

* **Configurazioni cloud**: Puoi trovare Configurazioni cloud in `/conf/`. Ad esempio, la configurazione cloud del modello dati modulo è disponibile in `/conf/global/settings/cloudconfigs/fdm`.

* **Modello di flusso di lavoro**: Puoi trovare AEM modelli di flussi di lavoro in `/conf/global/settings/workflow/models/`. Ad esempio, per un modello di flusso di lavoro denominato WKND Registration aggiungi percorso `/conf/global/settings/workflow/models/wknd-registration`

Puoi aggiungere percorsi di cartelle di livello superiore elencati di seguito o percorsi di cartelle specifici come descritto di seguito. Ti consente di migrare una determinata risorsa e tutte le risorse e i moduli contemporaneamente.

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/theme
* /content/forms/af
* /etc/clientlibs/fd/theme

Per migrare AEM modelli di flussi di lavoro, specifica i percorsi seguenti:

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
