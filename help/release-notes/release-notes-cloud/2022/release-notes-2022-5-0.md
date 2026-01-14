---
title: Note sulla versione 2022.5.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2022.5.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 64%

---

# Note sulla versione 2022.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione 2022.5.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.5.0) è il 9 giugno 2022.
La prossima versione (2022.6.0) è prevista per il 30 giugno 2022.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica della versione di maggio 2022 per un riepilogo delle funzioni aggiunte alla versione 2022.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni disponibili nel canale pre-release di [!DNL Sites] {#prerelease-features-sites}

* Varie funzionalità di GraphQL
* Una [nuova console](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) ottimizzata per l’utilizzo headless di frammenti di contenuto

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [Imaging avanzato Dynamic Media](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) ora supporta il formato di file AVIF; migliora ulteriormente Google Core Web Vital (Largest Contentful Paint), con AVIF che fornisce una riduzione delle dimensioni del 20% in più rispetto a WebP. In totale, AVIF fornisce una riduzione media delle dimensioni fino al 41% rispetto a JPEG (in alcune immagini anche fino al 76%).

* [!UICONTROL Experience Manager Assets Brand Portal] ora esegue processi automatici ogni 12 ore per eliminare tutte le risorse Brand Portal pubblicate in AEM. Di conseguenza, non è necessario eliminare manualmente le risorse nella cartella Contributo per mantenere la dimensione della cartella al di sotto del limite di soglia. Consulta [Novità di Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=it).

### Nuove funzioni disponibili nel canale pre-release di [!DNL Assets] {#prerelease-features-assets}

Experience Manager Assets utilizza le funzionalità di intelligenza artificiale di Adobe per [distinguere i colori in un&#39;immagine e applicarli automaticamente come tag al momento dell&#39;acquisizione](/help/assets/color-tag-images.md). Questi tag consentono un’esperienza di ricerca avanzata, in base alla composizione del colore dell’immagine. È possibile configurare il numero di colori, compresi tra uno e 40, con cui un&#39;immagine viene taggata in modo da poter cercare le immagini in base a tali colori in un secondo momento.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili nel canale pre-release di [!DNL Forms] {#prerelease-features-forms}

* **Integrare moduli adattivi con Microsoft® Power Automate**: ora è possibile configurare un modulo adattivo per eseguire un flusso cloud Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record al flusso cloud Power Automate per l’elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche di business sulla base dei dati acquisiti e automatizzare i flussi di lavoro dei clienti.

* **Procedura guidata per la creazione di un modulo adattivo**: puoi usare la procedura guidata di facile utilizzo per gli utenti aziendali per creare rapidamente Forms adattivo. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati e creare un modulo adattivo.

  ![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Accesso rapido alla cabina di comando del prodotto: accesso semplice e dettagliato alle informazioni di prodotto con un solo clic nell’editor di Sites

<!-- Image was not found during PR validation despite correct path   ![Enable wantlist](/help/assets/CIF/enable-wishlist.png) -->

* Supporto per ulteriori componenti di marketing commerce: i componenti possono essere configurati per mostrare un componente aggiuntivo al carrello e un componente aggiuntivo all’elenco dei desideri call-to-action

  ![Collegamento all’editor di Sites per la cabina di comando del prodotto](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* L&#39;opzione &quot;Aggiungi albero&quot; nella scheda **Distribuisci** della schermata di amministrazione dell&#39;agente di replica, precedentemente dichiarata obsoleta, è stata rimossa il 20 giugno 2022 o poco dopo. I pacchetti con una gerarchia di struttura dei contenuti devono essere replicati utilizzando [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o il [flusso di lavoro Pubblica struttura dei contenuti](/help/operations/replication.md#publish-content-tree-workflow).

* L’utilizzo della schermata di amministrazione dell’agente di replica o dell’API di replica per la distribuzione di pacchetti di contenuti di dimensioni superiori a 10 MB (nodi con proprietà, esclusi i binari) è diventato obsoleto e applicato il 12 settembre 2022 o poco dopo. Per replicare pacchetti di contenuti di grandi dimensioni, è necessario utilizzare [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o il [flusso di lavoro Pubblica struttura dei contenuti](/help/operations/replication.md#publish-content-tree-workflow). A luglio verrà visualizzato un messaggio di avvertenza se si tenta di replicare pacchetti di contenuti di grandi dimensioni nella **scheda Distribuisci** della schermata di amministrazione dell&#39;agente di replica, nonché nel registro degli errori di AEM ogni volta che l&#39;API di replica viene utilizzata per replicare tali pacchetti di contenuti di grandi dimensioni. A settembre, le avvertenze sono state sostituite da errori. Regola i processi di conseguenza.

### Nuove funzioni disponibili nel canale pre-release di [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service è ora integrato con Unified Shell per migliorare l’esperienza utente e per coerenza con tutte le altre applicazioni di Experience Cloud. Per ulteriori dettagli, vedi [AEM as a Cloud Service su Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md).

## Elementi di base per la sicurezza di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation-security}

### Obsolescenza di TLS 1.0, 1.1

A partire dal 30 giugno 2022, Experience Manager as a Cloud Service richiederà una comunicazione di rete e uno scambio di dati più sicuri con i sistemi degli utenti. AEM utilizzerà esclusivamente il protocollo TLS (Transport Layer Security) 1.2. Le versioni precedenti di TLS 1.0 e 1.1 ora sono obsolete.

Se continui a utilizzare versioni precedenti di TLS come 1.0 o 1.1, potresti perdere l’accesso ad Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
