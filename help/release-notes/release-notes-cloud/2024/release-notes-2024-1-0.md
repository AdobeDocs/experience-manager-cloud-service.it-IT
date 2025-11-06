---
title: Note sulla versione 2024.1.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.1.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 9f5d97c6-6536-4593-acbf-cbe8bf9b5eeb
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 89%

---

# Note sulla versione 2024.1.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.1.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.1.0) è il 25 gennaio 2024. La prossima versione funzionale (2024.3.0) è pianificata per l’11 aprile 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di gennaio 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Extension Manager in AEM Sites {#sites-extension-manager}

**Esplora il nuovo [Extension Manager in AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** per personalizzare la configurazione di AEM configurando le estensioni dell’interfaccia utente.

![Extension Manager in AEM Sites](/help/assets/sites/extension-manager/homepage.png)

Extension Manager in AEM Sites consente a sviluppatori e professionisti di accedere, gestire e personalizzare le [estensioni dell’interfaccia utente](https://developer.adobe.com/uix/docs/) create con [Adobe App Builder](https://developer.adobe.com/app-builder/) per migliorare le funzionalità di AEM Sites.
Con Extension Manager, puoi:

* abilitare o disabilitare le estensioni in base all’istanza;
* configurare i parametri di estensione;
* visualizzare l’anteprima delle estensioni e generare un collegamento di anteprima condivisibile;
* scoprire le funzioni di estensibilità dell’interfaccia utente tramite demo interattive;
* accedere alle funzioni sperimentali di Adobe tramite estensioni di prime parti.

Stiamo attivamente richiedendo un feedback e nuovi casi d’uso per le estensioni dell’interfaccia utente. Se desideri connetterti, invia un’e-mail all’indirizzo `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funzioni pre-release della vista Amministrazione {#admin-view-prerelease}

**Anteprima rappresentazioni per tutti i tipi di video supportati**

Experience Manager Assets ora genera le rappresentazioni in anteprima di tutti i tipi di video supportati per impostazione predefinita senza richiedere una configurazione del profilo di elaborazione

### Vista risorse {#assets-view-features}

**Tag avanzati nell’elenco Bloccati**

Assets Essentials ora consente di definire un elenco Bloccati per le parole che non devono essere aggiunte come tag avanzati alle risorse che vengono caricate nell’archivio. Questa funzionalità consente di mantenere la conformità al marchio e di ridurre il lavoro associato alla moderazione dei tag avanzati.

![Tag avanzati nell’elenco Bloccati](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programma per i primi utilizzatori {#forms-early-adopter}

* **[Inviare un modulo adattivo allo scenario Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service offre opzioni pronte all’uso per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario di Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

* **[Supporto lingue da destra a sinistra](/help/forms/supporting-new-language-localization-core-components.md)**: i moduli adattivi basati sui Componenti core ora possono essere presentati in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi in modo da soddisfare questi diversi tipi di pubblico e selezionarli in mercati RTL. In alcune aree geografiche, fornire moduli nella lingua locale, è anche obbligatorio dal punto di vista legale. Adattandosi alle lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

  ![Supporto lingue da destra a sinistra](/help/forms/assets/right-to-left-language-support.png)

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-early-adopter-program@adobe.com` dal proprio ID e-mail ufficiale.

* **[Puoi sfruttare il servizio di telemetria operativa](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** per abilitare la raccolta lato client per AEM as a Cloud Service.
Il servizio di telemetria operativa offre una riflessione più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Inoltre, per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

  Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a `aemcs-rum-adopter@adobe.com` insieme al tuo nome di dominio per ciascuno degli ambienti per i quali vuoi abilitare la telemetria operativa dal tuo indirizzo e-mail associato al tuo Adobe ID. Il team di prodotto di Adobe abiliterà quindi il servizio di telemetria operativa.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto per Dynatrace {#dynatrace}

I clienti Dynatrace possono monitorare il loro utilizzo di AEM. [Scopri come](/help/implementing/cloud-manager/dynatrace.md) richiedere la connettività con l’ambiente Dynatrace per il monitoraggio delle prestazioni delle applicazioni. Tieni presente che New Relic APM, disponibile per tutti i clienti, interromperà la raccolta dei dati se è abilitato Dynatrace.

### Supporto RDE per il codice front-end tramite i temi e i modelli del sito: programma per i primi utilizzatori {#rde-frontend-early-adopter}

Gli [ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ora supportano il codice front-end basato su [temi del sito](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelli di sito](/help/sites-cloud/administering/site-creation/site-templates.md), per i primi utilizzatori. Con gli RDE, questa operazione viene eseguita utilizzando una direttiva della riga di comando, anziché una [pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Invia un’e-mail all’indirizzo **aemcs-rde-support@adobe.com** per provarlo e fornire un feedback.

### Mappatura dei domini - Programma di adozione anticipata {#cdn-config-early-adopter}

Oltre alle [Regole del filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole WAF (Web Application Firewall) facoltative, esiste l’opportunità di utilizzare la pipeline di configurazione per specificare e distribuire [altri tipi di configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md). Partecipa al programma early adopter inviando un&#39;e-mail a **`aemcs-cdn-config-adopter@adobe.com`** per accedere a:

* 301/302 reindirizzamenti lato client
* proxy di richieste al server Edge di origini arbitrarie
* trasformazioni URL
* impostazione o modifica delle intestazioni di risposta o richiesta
* pagine di errore personalizzate quando la rete CDN non può raggiungere AEM

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
