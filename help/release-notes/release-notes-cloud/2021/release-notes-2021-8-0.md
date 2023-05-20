---
title: Note sulla versione 2021.8.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.8.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 33%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] (2021.8.0) è l’26 agosto 2021.
La seguente versione (2021.9.0) è del 6 ottobre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di agosto 2021](https://video.tv.adobe.com/v/336277) video per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Quando si condividono risorse digitali come collegamento, gli utenti possono copiare immediatamente l’URL negli Appunti. Questo miglioramento consente di condividere le risorse in modo più rapido e conveniente. Questa funzionalità consente una condivisione delle risorse più rapida e conveniente.

   ![Opzione Copia URL quando si condivide una risorsa come collegamento](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Quando condividi una risorsa come collegamento, ora puoi copiare l’URL per condividerlo separatamente.*

* Quando carichi i file TXT, i microservizi per le risorse generano automaticamente una miniatura. La miniatura PNG è una rappresentazione del file TXT che aiuta gli utenti a identificare il contenuto o i file in una certa misura, senza aprire i file. Questa funzionalità non richiede alcuna configurazione e funziona per impostazione predefinita.

   ![Una rappresentazione di un file TXT viene generata automaticamente da [!DNL Assets] in formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Viene generata automaticamente una rappresentazione di un file TXT per aiutarti a identificare il file senza aprirlo.*

### Nuova funzione in [!DNL Assets] canale prerelease {#assets-prerelease-features}

* Ora gli utenti possono ordinare le risorse visualizzate nei risultati di ricerca nelle viste Colonna e Scheda. L’ordinamento funziona sulle colonne Nome, Creato, Modificato o Nessuno.

   ![Ordinare i risultati della ricerca in [!DNL Assets] nelle viste Colonna e Scheda](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordinare i risultati della ricerca in [!DNL Assets] nelle viste Colonna e Scheda.*

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

* Quando un membro del gruppo di collaboratori passa al [!DNL Assets] Console, un altro `POST` viene generata una richiesta per provare a creare una raccolta. Questa richiesta non è necessaria, ha esito negativo a causa di problemi di autorizzazioni e crea molti errori nei registri. (CQ-4328856)
* Quando gli utenti visualizzano una risorsa e selezionano [!UICONTROL Timeline] dal menu a comparsa nel pannello a sinistra, viene visualizzato un errore. Nei registri vengono registrati molti avvisi a causa di una query non valida. (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* Il servizio di automated forms conversion può [convertire PDF forms in italiano e portoghese](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) su Adaptive Forms.

* **Documento di record basato su Acroform**: AEM Forms as a Cloud Service supporta l’utilizzo di [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) come modello per documento record oltre al modello di modulo basato su XFA.

* **Connettore per l’archivio dati di Microsoft Azure**: ora è possibile [connettere il modello dati modulo al sistema di archiviazione Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare i dati dei moduli adattivi come BLOB nell’archiviazione di Microsoft Azure.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

* **Utilizzare i ruoli di Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere i ruoli dei destinatari del contratto, oltre a Firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Ora è possibile abilitare ogni destinatario dell’accordo a configurare il proprio ruolo in un modulo adattivo, con Firmatario come ruolo predefinito.

* **Analytics per Forms adattivo**: ora puoi acquisire e tenere traccia del comportamento degli utenti finali tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni approfondite sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Connettere facilmente AEM Forms con Microsoft Dynamics e Salesforce.com**: il servizio fornisce la configurazione dell’origine dati predefinita e i modelli dati per Microsoft Dynamics e Salesforce.com, rendendo più rapido e semplice per gli sviluppatori configurare Microsoft Dynamics e Salesforce.com come origini dati per un modulo adattivo.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuova interfaccia utente per il selettore delle categorie per migliorare l’esperienza utente, l’efficienza e il supporto per cataloghi di prodotti complessi

   ![Nuovo selettore categorie](/help/assets/CIF/category-picker.png)

* Migliore supporto A11Y per i componenti core CIF

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data di pubblicazione {#release-date-cm-aug}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.8.0 è il 12 agosto 2021.
La prossima versione è pianificata per il 9 settembre 2021.

### Novità {#what-is-new-aug}

* Ora chi usa Cloud Service può visualizzare i rapporti SLA (Service Level Agreement) in Cloud Manager. La funzione sarà progressivamente resa disponibile nei prossimi mesi.
Per ulteriori informazioni, consulta [Generazione rapporti SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=it).

* Il tipo e la gravità di IndexType e delle regole di qualità `IndexDamAssetLucene` sono stati modificati. Ora entrambi i bug sono di *gravità* bloccante.

* Sono state introdotte nuove regole per la qualità dell’indice Oak che riguardano le configurazioni asincrone e tika.

* Il numero massimo di certificati SSL per programma è aumentato a 50.

* È stata aggiunta la funzionalità self-service per consentire agli utenti di creare e gestire più archivi tramite l’interfaccia utente di Cloud Manager.

* SonarQube leggeva inutilmente i dati della cronologia Git. Su basi di codice di grandi dimensioni, ciò poteva comportare un’immotivata riduzione delle prestazioni della build.

* Ora è disponibile un’API per rendere non valida la cache di dipendenza Maven per ogni pipeline.

* L’archetipo del progetto AEM utilizzato da Cloud Manager è stato aggiornato alla versione 29.

### Correzioni di bug {#bug-fixes-aug}

* Lo stato Aggiornamento disponibile non doveva essere visualizzato quando l’ultima versione era precedente alla versione corrente.

* L’onboarding iniziale non veniva avviato correttamente per le nuove organizzazioni con nomi molto lunghi.

* Talvolta, quando una pipeline veniva attivata due volte per qualche motivo, si verificava un errore in una delle esecuzioni riportante il messaggio *Impossibile aggiornare lo stato di esecuzione della pipeline*.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.5.6 è l’11 agosto 2021.

### Correzioni di bug {#bug-fixes-ctt}

* In alcuni casi non tutti gli utenti sono stati trasferiti all’istanza di destinazione. Per ottenere questa correzione è necessario CTT v1.5.6 insieme a aem-ethos-tools 1.2.354 o versione successiva sull’istanza AEM as a Cloud Service di destinazione.

* Il **Interrompi acquisizione** durante l’acquisizione nell’istanza Publish. Questo non è necessario perché non è presente alcun passaggio di ripristino mongo durante l’acquisizione di Publish.

* CTT non ha pulito il `/tmp` dopo un’estrazione riuscita. Questo a volte causava problemi di spazio su disco.
