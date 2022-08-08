---
title: Note sulla versione 2022.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2022.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: c2cd11b806f0cb961fc5ea0d8469f57b04e4aafa
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 20%

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

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.6.0) è il 30 giugno 2022.

La prossima versione (2022.7.0) è prevista per l’8 agosto 2022.

## Video sulla versione {#release-video}

Guarda il video Panoramica sulla versione di giugno 2022 per un riepilogo delle funzioni aggiunte nella versione 2022.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* Nuovo [interfaccia utente](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) è ora disponibile per gli amministratori di contenuti e gli autori di contenuti per gestire in modo efficiente (eseguire azioni quali pubblicare, annullare la pubblicazione, copiare, spostare ecc.), cercare/filtrare e creare frammenti di contenuto per casi d’uso headless.

   ![Console Frammenti di contenuto](/help/release-notes/assets/cf-ui.png)

* Il nuovo [Componente Sommario](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) funziona non solo con i componenti core, ma con tutti i componenti, eseguendo il rendering automatico di ToCs sulle pagine di contenuto. Inoltre, poiché è reso lato server e completamente memorizzato nella cache dal dispatcher, è anche efficiente da caricare.

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

Experience Manager Assets utilizza le funzionalità di Adobe Sensei AI per [distinguere i colori in un’immagine e applicarli automaticamente come tag al momento dell’acquisizione](/help/assets/color-tag-images.md). Questi tag consentono un’esperienza di ricerca avanzata, in base alla composizione del colore dell’immagine. È possibile configurare il numero di colori, compresi tra uno e quaranta, che vengono assegnati a un’immagine in modo da poter cercare le immagini in base a tali colori in un secondo momento.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Forms] {#forms-features}

* **[Integrare Forms adattivo con Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: È ora possibile configurare un modulo adattivo per eseguire un flusso cloud Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record a Power Automate Cloud Flow per l&#39;elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche aziendali intorno ai dati acquisiti e automatizzare i flussi di lavoro dei clienti.

* **Creazione guidata di un modulo adattivo**: Puoi utilizzare la procedura guidata di facile utilizzo per creare rapidamente Adaptive Forms. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati per creare un modulo adattivo.

   ![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuova pagina delle proprietà del cockpit prodotto per una panoramica migliore e semplificata

![panoramica delle proprietà del cockpit prodotto](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilità e robustezza migliorate per i connettori di terze parti su I/O Runtime

* Supporto migliorato per le sovrascritture della configurazione client GQL (ad esempio, impostazione di un comportamento di caching personalizzato)

* Più endpoint di e-commerce sono ora supportati come predefiniti e possono essere configurati tramite Cloud Manager. Puoi trovare i dettagli nel blog CIF [qui](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Correzioni di bug {#bug-fixes-cif}

* Il campo del selettore prodotti con più valori mostra il secondo e prodotti aggiuntivi come non validi

* Il selettore dei prodotti viene talvolta nascosto dietro i componenti

## Componente aggiuntivo Demos di riferimento {#cloud-services-demos}

### Novità {#what-is-new-demos}

* Nuovo modello WKND Content &amp; Commerce che estende WKND con un’esperienza di acquisto E2E che include catalogo dei prodotti, carrello acquisti, checkout e myAccount. Questo modello utilizza CIF e i suoi componenti core CIF, pertanto è necessario installare anche il componente aggiuntivo CIF. Puoi trovare i dettagli nel blog CIF [qui](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![Negozio WKND](/help/assets/CIF/wknd_shop.png)

![pdp WKND](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* Come indicato nelle note sulla versione di maggio (2022.5.0), l’opzione &quot;Aggiungi albero&quot; nella schermata di amministrazione dell’agente di replica **Distribuisci** è stata rimossa la scheda . I pacchetti con una gerarchia ad albero del contenuto devono essere replicati utilizzando [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [Pubblica struttura contenuto](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) workflow.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Strumenti di migrazione {#migration-tools}

È possibile trovare un elenco completo delle versioni degli strumenti di migrazione [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
