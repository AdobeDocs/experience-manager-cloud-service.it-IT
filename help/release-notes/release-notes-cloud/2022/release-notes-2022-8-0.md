---
title: Note sulla versione 2022.8.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2022.8.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
source-git-commit: 599f924465552b2ef43827da8e139c239e47baed
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 61%

---

# Note sulla versione 2022.8.0 per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione della funzione per la versione 2022.8.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.8.0) è il 1° settembre 2022.
La prossima versione (2022.10.0) è prevista per il 10 novembre 2022.

## Video sulla versione {#release-video}

Guarda il video Panoramica sulla versione di agosto 2022 per un riepilogo delle funzioni aggiunte nella versione 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* Il componente E-mail consente di creare contenuti in AEM che vengono quindi inviati come e-mail tramite Campaign Classic. Il componente e-mail di base:
   * è basato su [Componente WCM core](https://github.com/adobe/aem-core-wcm-components) che supporta i modelli modificabili e il sistema di stili.
   * fornisce 10 componenti pronti per la produzione ottimizzati per e-mail (Pagina, Contenitore, Titolo, Testo, Immagine, Pulsante, Teaser, Frammento esperienza, Frammento di contenuto, Segmentazione).
   * offre personalizzazione e segmentazione avanzate, grazie alla funzione [Inserimento di variabili di Campaign](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) nella maggior parte dei campi di dialogo e nella flessibilità [Componente Segmentation](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * fornisce un output HTML di facile utilizzo e-mail ottimale, grazie alla [Inliner stili CSS](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), [Inliner attributi di HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)e [Sanitari HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * consente la creazione delle e-mail ovunque.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Sites] {#prerelease-features-sites}

* La [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) fornisce agli utenti un’opzione per visualizzare il numero totale di copie della lingua associate a un frammento di contenuto. Inoltre, è possibile accedere con 1 solo clic per visualizzare tutte le copie delle varie lingue. Gli utenti possono anche filtrare la visualizzazione a tabella in base alla lingua che desiderano.

![Lingue dei frammenti di contenuto](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#features-assets}

* Ora puoi configurare Adobe Experience Manager Assets in modo da [limitare il tipo di risorse che gli utenti possono caricare in base al tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

   ![Restrizioni al caricamento delle risorse](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

* [Procedura guidata per moduli adattivi](/help/forms/creating-adaptive-form.md): AEM Forms fornisce una procedura guidata intuitiva che consente agli utenti aziendali di creare rapidamente Adaptive Forms. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per creare un modulo adattivo. Con questa versione sono stati introdotti i seguenti miglioramenti alla procedura guidata:

   * Selezionare o deselezionare i campi: la procedura guidata consente di creare un modulo adattivo basato su schemi JSON e Form Data Model. È ora possibile selezionare un sottoinsieme di campi all’interno di uno schema da includere in un modulo adattivo. I campi selezionati vengono convertiti nei corrispondenti componenti di acquisizione dati per moduli adattivi, per creare rapidamente i moduli adattivi desiderati.

   * Usare modelli statici: i clienti che dispongono già di modelli statici legacy possono continuare il loro percorso di adozione cloud utilizzando modelli statici nella procedura guidata per la creazione di moduli adattivi. Questo offre ai clienti più tempo per completare la migrazione dai vecchi modelli statici ai nuovi modelli modificabili.

* [Rimuovere i campi nascosti da un documento di record (DoR) durante l’elaborazione lato server](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): è possibile generare il PDF del documento di record in modo che contenga solo i campi che erano visibili agli utenti finali durante la loro esperienza di acquisizione dei dati. Dopo l’invio del modulo, il server rileva quali campi erano nascosti all’utente finale in base ai dati inviati e quindi li esclude dal documento di record, per coerenza.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Associazione di pagine AEM a prodotti e categorie tramite le proprietà di pagina AEM più panoramica in cockpit prodotto
   ![associazione pagina cockpit prodotto](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
