---
title: Note sulla versione 2021.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 12%

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

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2021.8.0) è il 26 agosto 2021.
La versione seguente (2021.9.0) è del 6 ottobre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di agosto 2021](https://video.tv.adobe.com/v/336277) video per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Quando condividi risorse digitali come collegamento, gli utenti possono copiare l’URL negli Appunti immediatamente. Questo miglioramento consente di condividere le risorse in modo più rapido e conveniente. Questa funzionalità consente una condivisione delle risorse più rapida e conveniente.

   ![Opzione Copia URL quando condividi una risorsa come collegamento](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Quando condividi una risorsa come collegamento, ora puoi copiare l’URL per condividerlo separatamente.*

* Quando carichi file TXT, i microservizi per le risorse generano automaticamente una miniatura. La miniatura PNG è una rappresentazione del file TXT che aiuta gli utenti a identificare il contenuto o i file in una certa misura, senza aprire i file. Questa funzionalità non richiede alcuna configurazione e funziona per impostazione predefinita.

   ![Il rendering di un file TXT viene generato automaticamente da [!DNL Assets] in formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Viene generato automaticamente un rendering di un file TXT per identificare il file senza aprirlo.*

### Nuova funzione nel [!DNL Assets] canale prerelease {#assets-prerelease-features}

* Gli utenti possono ora ordinare le risorse visualizzate nei risultati della ricerca nelle viste a colonne e a schede. L’ordinamento viene eseguito sulle colonne Nome, Creato, Modificato o Nessuno.

   ![Ordina i risultati della ricerca in [!DNL Assets] nelle viste a colonne e a schede](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordina i risultati della ricerca in [!DNL Assets] nelle viste a colonne e a schede.*

### Bug fissati in [!DNL Assets] {#assets-bugs-fixed}

* Quando un membro del gruppo di collaboratori accede alla pagina [!DNL Assets] Console, un `POST` viene generata la richiesta per cercare di creare una raccolta. Questa richiesta non è necessaria, non riesce a causa di problemi di autorizzazioni e crea molti errori nei log. (CQ-4328856)
* Quando gli utenti visualizzano una risorsa e selezionano la [!UICONTROL Timeline] dal menu a comparsa nel pannello a sinistra viene visualizzato un errore. Nei registri, molti avvisi vengono registrati a causa di una query non valida. (CQ-4328919)

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* Il servizio di automated forms conversion può [convertire PDF forms in italiano e portoghese](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) su Forms adattivo.

* **Documento di record basato su Acroform**: AEM Forms as a Cloud Service supporta l’utilizzo di [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) come modello per il modello di modulo Document of Record oltre a basato su XFA.

* **Connettore dell’archivio dati di Microsoft Azure**: Ora puoi [collega il modello dati del modulo all’archiviazione di Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare dati adattivi del modulo in Microsoft Azure Storage as a BLOB.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms}

* **Utilizzare i ruoli Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio aziendali e aziendali ha la possibilità di espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, in modo da soddisfare meglio i requisiti del flusso di lavoro. Ora puoi abilitare ogni destinatario dell’accordo a configurare il proprio ruolo in un modulo adattivo, con il ruolo predefinito Firma .

* **Analytics per Forms adattivo**: È ora possibile acquisire e tenere traccia del comportamento dell’utente finale tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sull’utente finale. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce.com**: Il servizio fornisce modelli di dati e configurazione dell’origine dati preconfigurati per Microsoft Dynamics e Salesforce.com, consentendo agli sviluppatori di configurare Microsoft Dynamics e Salesforce.com come origini dati per un modulo adattivo in modo più rapido e semplice.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuova interfaccia utente del selettore categorie per migliorare l’esperienza utente, aumentare l’efficienza e migliorare il supporto per cataloghi di prodotti complessi

   ![Selezione nuova categoria](/help/assets/CIF/category-picker.png)

* Supporto migliorato per A11Y per i componenti core CIF

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM 2021.8.0 e 2021.7.0.

## Data di pubblicazione {#release-date-cm-aug}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.8.0 è il 12 agosto 2021.
La prossima versione è prevista per il 9 settembre 2021.

### Novità {#what-is-new-aug}

* I clienti del Cloud Service ora possono visualizzare i rapporti SLA (Service Level Agreement) in Cloud Manager. Ciò sarà progressivamente reso disponibile nei prossimi mesi.
Vedi [Generazione rapporti SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) per saperne di più.

* Tipo e gravità dell&#39;IndexType e `IndexDamAssetLucene` le regole di qualità sono state modificate. Questi sono ora entrambi Bugs of Blocker *serenità*.

* Sono state introdotte nuove regole sulla qualità dell&#39;indice Oak per coprire configurazioni asincrone e tika.

* Aumenta il numero massimo di certificati SSL per programma a 50.

* Funzionalità self-service per consentire agli utenti di creare e gestire più archivi tramite l’interfaccia utente di Cloud Manager.

* SonarQube leggeva inutilmente i dati della cronologia Git. Su basi di codice di grandi dimensioni, ciò potrebbe comportare una multa non necessaria per le prestazioni della build.

* È ora disponibile un’API per annullare la validità della cache di dipendenza Maven per pipeline.

* La versione di AEM Project Archetype utilizzata da Cloud Manager è stata aggiornata alla versione 29.

### Correzioni di bug {#bug-fixes-aug}

* Lo stato Aggiorna disponibile non deve essere visualizzato quando l&#39;ultima versione è inferiore alla versione corrente.

* L&#39;onboarding iniziale non riusciva per le nuove organizzazioni con nomi molto lunghi.

* Talvolta, quando una pipeline viene attivata due volte per qualche motivo, si verifica un errore in una delle esecuzioni con *impossibile aggiornare lo stato di esecuzione della pipeline* errore.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.5.6 è l’11 agosto 2021.

### Correzioni di bug {#bug-fixes-ctt}

* In alcuni casi non tutti gli utenti sono stati migrati all’istanza di destinazione. Per ottenere questa correzione è necessario CTT v1.5.6 insieme alla versione aem-ethos-tools 1.2.354 o successiva sull&#39;istanza di destinazione AEM as a Cloud Service.

* La **Interrompi acquisizione** Il pulsante veniva disattivato durante l’acquisizione nell’istanza Publish. Questo non è necessario perché non esiste un passaggio di ripristino mongo durante l’acquisizione di Publish.

* Il CTT non ha ripulito il `/tmp` dopo un’estrazione riuscita. Ciò a volte ha causato problemi di spazio su disco.
