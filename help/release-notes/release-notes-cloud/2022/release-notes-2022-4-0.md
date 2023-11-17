---
title: Note sulla versione 2022.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2022.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 86%

---

# Note sulla versione 2022.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione 2022.4.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.4.0) è il 5 maggio 2022.
La prossima versione (2022.5.0) è prevista per il 9 giugno 2022.

## Video sulla versione {#release-video}

Dai un’occhiata al video [Panoramica sulla versione di aprile 2022](https://video.tv.adobe.com/v/342612?quality=12) per un riepilogo delle funzioni aggiunte alla versione 2022.4.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* I tipi di dati del modello di contenuto possono ora essere definiti come [traducibili](/help/assets/content-fragments/content-fragments-models.md#properties) utilizzando una semplice casella di controllo nell’editor dei modelli di contenuto. Inoltre, le regole di traduzione e le configurazioni dell’AEM vengono aggiornate automaticamente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Ora puoi [ordinare i tag](/help/assets/organize-assets.md#use-tags-to-organize-assets) nella finestra del selettore dei tag in ordine crescente o decrescente in base al nome, alla data di creazione o alla data di modifica.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Supporto delle API di comunizazione/manipolazione dei documenti nell’SDK di Forms as a Cloud Service**: le [API per la manipolazione dei documenti](/help/forms/aem-forms-cloud-service-communications.md) consentono di combinare, ridisporre e convalidare i documenti PDF. Ora puoi utilizzare le API di comunicazione e generazione di documenti in un ambiente di sviluppo locale grazie all’SDK di AEM Forms as a Cloud Service.

* **Utilizzare XCI personalizzato per generare un documento Record**: ora puoi [utilizzare un file XCI personalizzato per impostare varie proprietà di un documento Record](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Sostituisce l’XCI principale con le modifiche personalizzate. Offre un maggiore controllo sulla generazione di documenti di record, aumentando le opportunità di personalizzazione e customizzazione.

* **Utilizzare il CAPTCHA invisibile in un modulo adattivo**: puoi usare il [CAPTCHA invisibile per mostrare la richiesta CAPTCHA solo nel caso di attività sospetta](/help/forms/captcha-adaptive-forms.md). Se non viene trovata alcuna attività sospetta, la richiesta CAPTCHA non viene visualizzata. Consente di valutare il completamento manuale dei moduli senza bisogno di caselle di controllo, ridurre le operazioni di personalizzazione e migliorare l’esperienza dell’utente finale.

* **Configurazioni del modello dati del modulo**: ora puoi [riutilizzare le configurazioni del modello dati modulo in ambienti diversi](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), semplificando le integrazioni di dati e riducendo i costi IT.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### SDK Build Analyzer {#sdk-build-analyzers}

Il plug-in Maven SDK Build Analyzer per AEM as a Cloud Service rileva i problemi in un progetto Maven, incluse eventuali dipendenze mancanti. Offre agli sviluppatori l’opportunità di individuare i problemi durante lo sviluppo locale, molto prima che vengano distribuiti in ambienti Cloud con Cloud Manager.

È stato aggiunto di recente un nuovo analizzatore:

* `content-packages-validation` : convalida la sintassi e la struttura del formato dei contenuti dei pacchetti installati durante la distribuzione

Consigliamo vivamente di aggiornare il progetto Maven con l’ultima versione dell’analizzatore o di includerlo, se non lo hai ancora fatto. Per ulteriori informazioni, consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it).

## Elementi di base per la sicurezza di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation-security}

### Obsolescenza di TLS 1.0, 1.1

A partire dal 30 giugno 2022, Experience Manager as a Cloud Service richiederà una comunicazione di rete e uno scambio di dati più sicuri con i sistemi degli utenti. L’AEM intende utilizzare esclusivamente il protocollo TLS (Transport Layer Security) 1.2. Le versioni precedenti di TLS 1.0 e 1.1 ora sono obsolete.

Se continui a utilizzare versioni precedenti di TLS come 1.0 o 1.1, potresti perdere l’accesso ad Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
