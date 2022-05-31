---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 8c432f8902d005918c4fd4432d23c3140967c773
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 30%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.4.0) è il 5 maggio 2022.
La prossima versione (2022.5.0) è prevista per il 9 giugno 2022.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di aprile 2022](https://video.tv.adobe.com/v/342612?quality=12) video per un riepilogo delle funzioni aggiunte nella versione 2022.4.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* I tipi di dati del modello di contenuto possono ora essere definiti come [traducibile](/help/assets/content-fragments/content-fragments-models.md#properties) utilizzando una semplice casella di controllo nell’editor del modello di contenuto. Inoltre, AEM regole di traduzione e configurazioni vengono aggiornate automaticamente.

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Ora puoi [ordinare tag](/help/assets/organize-assets.md#use-tags-to-organize-assets) nella finestra del selettore tag in ordine crescente o decrescente in base al nome del tag, alla data di creazione o alla data di modifica.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Comunicazioni - Supporto delle API di manipolazione documenti nell’SDK as a Cloud Service di Forms**: [API di manipolazione documenti](/help/forms/aem-forms-cloud-service-communications.md) combinare, ridisporre e convalidare i documenti PDF. Ora puoi utilizzare le API Communications - Document Generation in un ambiente di sviluppo locale con l’aiuto dell’SDK as a Cloud Service di AEM Forms.

* **Utilizzare XCI personalizzato per generare un documento Record**[: ora puoi utilizzare un file XCI personalizzato per impostare varie proprietà di un documento Record](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Sostituisce l’XCI principale con le modifiche personalizzate. Offre un maggiore controllo sulla generazione di documenti di record, aumentando le opportunità di personalizzazione e personalizzazione.

* **Utilizzare il CAPTCHA invisibile in un modulo adattivo**[: puoi usare il CAPTCHA invisibile per mostrare la richiesta CAPTCHA solo nel caso di attività sospetta](/help/forms/captcha-adaptive-forms.md). Se non viene trovata alcuna attività sospetta, la richiesta CAPTCHA non viene visualizzata. Consente di valutare il completamento dei moduli senza bisogno di caselle di controllo, ridurre le operazioni di personalizzazione e migliorare l’esperienza dell’utente finale.

* **Configurazioni del modello dati del modulo**: Ora puoi [riutilizzo delle configurazioni del modello dati modulo in ambienti diversi](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), semplificando le integrazioni di dati e riducendo i costi IT.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Accesso rapido al cockpit del prodotto: Accesso semplice e dettagliato alle informazioni di prodotto con un solo clic in Sites Editor

   ![Abilita elenco dei desideri](/help/assets/CIF/enable-wishlist.png)

* Supporto per componenti di marketing aggiuntivi: I componenti possono essere configurati per mostrare una chiamata all’azione del componente aggiuntivo al carrello e del componente aggiuntivo all’elenco dei desideri

   ![Collegamento all’editor di siti per il cockpit di prodotto](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### SDK Build Analytics {#sdk-build-analyzers}

Il plug-in Maven di AEM SDK Build Analyzer as a Cloud Service rileva i problemi in un progetto Maven, incluse le dipendenze mancanti. Offre agli sviluppatori l’opportunità di scoprire i problemi durante lo sviluppo locale, molto prima di distribuirli in ambienti Cloud con Cloud Manager.

È stato aggiunto di recente un nuovo analizzatore:

* `content-packages-validation` - convalida la sintassi e la struttura dei contenuti di formato corretto per i pacchetti che verranno installati durante la distribuzione

Si consiglia vivamente di aggiornare il progetto maven con l’ultima versione dell’analizzatore o di includere l’analizzatore, se non lo hai ancora fatto. Per ulteriori informazioni, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] come [!DNL Cloud Service] Sicurezza di base {#foundation-security}

### Obsolescenza di TLS 1.0, 1.1

A partire dal 30 giugno 2022, Experience Manager as a Cloud Service richiederà una comunicazione di rete e uno scambio di dati più sicuri con i sistemi degli utenti. AEM utilizzerà esclusivamente il protocollo TLS (Transport Layer Security) 1.2. Le versioni precedenti di TLS 1.0 e 1.1 diventeranno obsolete.

Se continui a utilizzare versioni precedenti di TLS come 1.0, 1.1, potresti perdere l’accesso ad Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

È possibile trovare un elenco completo delle versioni mensili di Cloud Manager [qui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Strumenti di migrazione {#migration-tools}

È possibile trovare un elenco completo delle versioni degli strumenti di migrazione [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
