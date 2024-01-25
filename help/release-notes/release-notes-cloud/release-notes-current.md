---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: fa106c2e3fec70971e2c54572199e35c24db0aa7
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 38%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.1.0) è il venerdì 25 gennaio 2024. La prossima versione funzionale (2024.2.0) è pianificata per il venerdì 29 febbraio 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Extension Manager in AEM Sites {#sites-extension-manager}

**Esplora il nuovo [Extension Manager in AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** per personalizzare la configurazione dell’AEM configurando le estensioni dell’interfaccia utente.

![Extension Manager in AEM Sites](/help/assets/sites/extension-manager/homepage.png)

L’Extension Manager di AEM Sites consente a sviluppatori e professionisti di accedere, gestire e personalizzare le estensioni dell’interfaccia utente create per migliorare le funzionalità di AEM Sites.
Con l’Extension Manager, puoi:

* Abilitare o disabilitare le estensioni per singole istanze;
* Configurare i parametri di estensione;
* Visualizzare l’anteprima delle estensioni e generare un collegamento di anteprima condivisibile;
* Scopri le funzioni di estensibilità dell’interfaccia utente tramite demo interattive;
* Accedi alle funzioni sperimentali di Adobe tramite estensioni di prime parti.

Stiamo attivamente cercando feedback e nuovi casi d’uso per le estensioni dell’interfaccia utente. Se desideri connetterti, invia un’e-mail a `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funzioni prerelease di visualizzazione amministrazione {#admin-view-prerelease}

**Anteprima rappresentazioni per tutti i tipi di video supportati**

Experience Manager Assets ora genera le rappresentazioni in anteprima di tutti i tipi di video supportati per impostazione predefinita senza richiedere una configurazione del profilo di elaborazione

### Visualizzazione risorse {#assets-view-features}

**Tag avanzati nell’elenco Bloccati**

Assets Essentials ora consente di definire l’elenco Bloccati per le parole che non devono essere aggiunte come tag avanzati alle risorse quando vengono caricate nell’archivio. Questa funzionalità consente di mantenere la conformità al marchio e di ridurre gli sforzi nella moderazione dei tag avanzati.

![Inserisce nell&#39;elenco Bloccati tag avanzati](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programma Early Adopter {#forms-early-adopter}

* **[Inviare un modulo adattivo allo scenario Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service offre opzioni pronte all’uso per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

* **[Supporto lingue da destra a sinistra](/help/forms/supporting-new-language-localization-core-components.md)**: il Forms adattivo basato sui Componenti core ora può essere presentato in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi in modo da soddisfare questi diversi tipi di pubblico e selezionarli in mercati RTL. In alcune regioni, è anche un mandato legale fornire moduli nella lingua locale. Accogliendo le lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

  ![Supporto lingue da destra a sinistra](/help/forms/assets/right-to-left-language-support.png)

* **[Protect i tuoi documenti con le API DocAssurance (parte delle API di comunicazione)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance ti consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite la crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo livello di protezione aumentato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Puoi scrivere a `aem-forms-early-adopter-program@adobe.com` dal tuo id e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto per Dynatrace {#dynatrace}

I clienti Dynatrace possono monitorare il loro utilizzo di AEM. [Scopri come](/help/implementing/cloud-manager/dynatrace.md) per richiedere la connettività con l&#39;ambiente Dynatrace per il monitoraggio delle prestazioni delle applicazioni. Tieni presente che New Relic APM, disponibile per tutti i clienti, interromperà la raccolta dei dati se Dynatrace è abilitato.

### Supporto RDE per il codice front-end tramite i temi del sito e i modelli del sito: programma Early Adopter {#rde-frontend-early-adopter}

[Ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ora supporta il codice front-end basato su [temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md), per i primi utilizzatori. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando, anziché una [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Rivolgiti a **aemcs-rde-support@adobe.com** per provarlo e fornire feedback.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
