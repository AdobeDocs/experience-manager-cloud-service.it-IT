---
title: Come migrare da un Forms Forms AEM 6.5 e AEM 6.4 a [!DNL AEM Forms] Ambiente as a Cloud Service?
description: Migrare da un [!DNL AEM Forms] Ambiente locale su [!DNL AEM Forms] Ambiente as a Cloud Service
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 8e28cff5b964005278858b6c8dd8a0f5f8156eaa
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 3%

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

1. Scarica e installa la [Strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) e [!DNL AEM Forms] Utilità di migrazione as a Cloud Service da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) sull’ambiente clonato. È possibile utilizzare Gestione pacchetti AEM per installare lo strumento e l&#39;utility.

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
