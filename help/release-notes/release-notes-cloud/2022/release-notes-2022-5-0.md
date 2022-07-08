---
title: Note sulla versione 2022.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2022.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: d6038920a5866c19a94980cc14fa46dec48daf51
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 18%

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

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.5.0) è il 9 giugno 2022.
La prossima versione (2022.6.0) è prevista per il 30 giugno 2022.

## Video sulla versione {#release-video}

Per un riepilogo delle funzioni aggiunte nella versione 2022.5.0, guarda il video Panoramica sulla versione di maggio 2022:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Sites] {#prerelease-features-sites}

* Varie funzionalità di GraphQL
* A [nuova console](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) Ottimizzato per l’utilizzo headless di frammenti di contenuto

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [Imaging avanzato Dynamic Media](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) ora supporta il formato di file AVIF - migliora ulteriormente Google Core Web Vital (Largest Contentful Paint), con AVIF che fornisce una riduzione del 20% in più rispetto a WebP. In totale, AVIF fornisce una riduzione delle dimensioni media fino al 41% rispetto a JPEG (in alcune immagini anche fino al 76%).

* [!UICONTROL Experience Manager Assets Brand Portal] ora esegue processi automatici ogni dodici ore per eliminare tutte le risorse Brand Portal pubblicate in AEM. Di conseguenza, non è necessario eliminare manualmente le risorse nella cartella Contribution per mantenere la dimensione della cartella al di sotto del limite di soglia. Vedi [Novità di Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

### Nuove funzioni disponibili nel canale prerelease di [!DNL Assets] {#prerelease-features-assets}

Experience Manager Assets utilizza le funzionalità di Adobe Sensei AI per [distinguere i colori in un’immagine e applicarli automaticamente come tag al momento dell’acquisizione](/help/assets/color-tag-images.md). Questi tag consentono un’esperienza di ricerca avanzata, in base alla composizione del colore dell’immagine. È possibile configurare il numero di colori, compresi tra uno e quaranta, che vengono assegnati a un’immagine in modo da poter cercare le immagini in base a tali colori in un secondo momento.


## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

* **Integrare Forms adattivo con Microsoft® Power Automate**: È ora possibile configurare un modulo adattivo per eseguire un flusso cloud Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record a Power Automate Cloud Flow per l&#39;elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche aziendali intorno ai dati acquisiti e automatizzare i flussi di lavoro dei clienti.

* **Creazione guidata di un modulo adattivo**: Puoi utilizzare la procedura guidata di facile utilizzo per creare rapidamente Adaptive Forms. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per creare un modulo adattivo.

   ![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Accesso rapido al cockpit del prodotto: Accesso semplice e dettagliato alle informazioni di prodotto con un solo clic in Sites Editor

   ![Abilita elenco dei desideri](/help/assets/CIF/enable-wishlist.png)

* Supporto per componenti di marketing aggiuntivi: I componenti possono essere configurati per mostrare una chiamata all’azione del componente aggiuntivo al carrello e del componente aggiuntivo all’elenco dei desideri

   ![Collegamento all’editor di siti per il cockpit di prodotto](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* L&#39;opzione &quot;Aggiungi albero&quot; nella schermata di amministrazione dell&#39;agente di replica **Scheda Distribuisci**, precedentemente dichiarato obsoleto, verrà rimosso il 20 giugno 2022 o poco dopo. I pacchetti con una gerarchia ad albero del contenuto devono essere replicati utilizzando [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [Flusso di lavoro Pubblica albero del contenuto](/help/operations/replication.md#publish-content-tree-workflow).

* L’utilizzo della schermata di amministrazione dell’agente di replica o dell’API di replica per la distribuzione di pacchetti di contenuto di dimensioni superiori a 10 MB (nodi con proprietà, esclusi i binari) è obsoleto e verrà applicato il 12 settembre 2022 o subito dopo. Invece, [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [Flusso di lavoro Pubblica albero del contenuto](/help/operations/replication.md#publish-content-tree-workflow) deve essere utilizzato per replicare questi pacchetti di contenuti di grandi dimensioni. A luglio verrà visualizzato un messaggio di avviso nella schermata di amministrazione dell’agente di replica **Scheda Distribuisci** se si tenta di replicare questi pacchetti di contenuti di grandi dimensioni e anche nel registro di errore AEM ogni volta che l&#39;API di replica viene utilizzata per replicare questi pacchetti di contenuti di grandi dimensioni. A settembre, gli avvisi saranno sostituiti da errori. Adeguare i processi di conseguenza.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service è ora integrato con Unified Shell per migliorare l’esperienza utente e unificarla a tutte le altre applicazioni di Experience Cloud. Fai riferimento a [AEM as a Cloud Service sulla shell unificata](/help/overview/aem-cloud-service-on-unified-shell.md) per ulteriori dettagli.

## [!DNL Experience Manager] come [!DNL Cloud Service] Sicurezza di base {#foundation-security}

### Obsolescenza di TLS 1.0, 1.1

A partire dal 30 giugno 2022, Experience Manager as a Cloud Service richiederà una comunicazione di rete e uno scambio di dati più sicuri con i sistemi degli utenti. AEM utilizzerà esclusivamente il protocollo TLS (Transport Layer Security) 1.2. Le versioni precedenti di TLS 1.0 e 1.1 diventeranno obsolete.

Se continui a utilizzare versioni precedenti di TLS come 1.0, 1.1, potresti perdere l’accesso ad Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Strumenti di migrazione {#migration-tools}

È possibile trovare un elenco completo delle versioni degli strumenti di migrazione [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
