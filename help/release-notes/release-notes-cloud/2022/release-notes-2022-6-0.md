---
title: Note sulla versione 2022.6.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2022.6.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 75%

---

# Note sulla versione 2022.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione 2022.6.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.6.0) è il 30 giugno 2022.

La prossima versione (2022.7.0) è prevista per l&#39;8 agosto 2022.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di giugno 2022 per un riepilogo delle funzioni aggiunte alla versione 2022.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* Una nuova [interfaccia utente](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) è ora disponibile per gli amministratori di contenuti e gli autori di contenuti per gestire in modo efficiente (ad esempio pubblicare, annullare la pubblicazione, copiare, spostare e così via), cercare/filtrare e creare frammenti di contenuto per casi d&#39;uso headless.

  ![Console Frammenti di contenuto](/help/release-notes/assets/cf-ui.png)

* Il nuovo [componente Sommario](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html?lang=it) funziona non solo con i componenti core, ma con tutti i componenti, riproducendo automaticamente il sommario sulle pagine dei contenuti. Inoltre, poiché è gestito lato server e completamente memorizzato nella cache dal dispatcher, viene anche caricato in modo efficiente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

Experience Manager Assets utilizza le funzionalità di intelligenza artificiale di Adobe per [distinguere i colori in un&#39;immagine e applicarli automaticamente come tag al momento dell&#39;acquisizione](/help/assets/color-tag-images.md). Questi tag consentono un’esperienza di ricerca avanzata, in base alla composizione del colore dell’immagine. È possibile configurare il numero di colori, compresi tra uno e 40, con cui un&#39;immagine viene taggata in modo da poter cercare le immagini in base a tali colori in un secondo momento.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Forms] {#forms-features}

* **[Integrare moduli adattivi con Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: ora è possibile configurare un modulo adattivo in modo che all’invio venga eseguito un flusso cloud Microsoft® Power Automate. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record al flusso cloud Power Automate per l’elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche di business sulla base dei dati acquisiti e automatizzare i flussi di lavoro dei clienti.

* **Creazione guidata di un modulo adattivo**: puoi utilizzare la procedura guidata per utenti aziendali per creare moduli adattivi in modo facile e veloce. La procedura guidata fornisce una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati e creare un modulo adattivo.

  ![Creazione guidata di un modulo adattivo](/help/release-notes/assets/wizard.png)

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuova pagina delle proprietà del pannello di comando del prodotto, per una panoramica migliore e semplificata

![panoramica delle proprietà del pannello di comando del prodotto](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilità e robustezza migliorate per i connettori di terze parti su I/O Runtime

* È stato migliorato il supporto per le sovrascritture della configurazione client GQL (ad esempio, impostare un comportamento di caching personalizzato)

* Ora per impostazione predefinita sono supportati più endpoint commerce che possono essere configurati tramite Cloud Manager. Puoi trovare i dettagli nel blog CIF, disponibile [qui](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Correzioni di bug {#bug-fixes-cif}

* Il campo del selettore prodotti con più valori mostra il secondo e gli ulteriori prodotti come non validi

* Il selettore prodotti viene talvolta nascosto dietro i componenti

## Componente aggiuntivo demo di riferimento {#cloud-services-demos}

### Novità {#what-is-new-demos}

* Nuovo modello WKND Content and Commerce che estende WKND con un’esperienza di acquisto E2E che include catalogo dei prodotti, carrello acquisti, pagamento e myAccount. Questo modello utilizza CIF e i suoi componenti core CIF, pertanto è necessario installare anche il componente aggiuntivo CIF. Puoi trovare i dettagli nel blog CIF, disponibile [qui](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![Negozio WKND](/help/assets/CIF/wknd_shop.png)

![pdp WKND](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* Come indicato nelle note sulla versione di maggio (2022.5.0), l&#39;opzione &quot;Aggiungi albero&quot; nella scheda **Distribuisci** della schermata di amministrazione dell&#39;agente di replica è stata rimossa. I pacchetti con una struttura gerarchica del contenuto devono essere replicati utilizzando il flusso di lavoro [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [Pubblica struttura contenuto](/help/operations/replication.md#manage-publication#publish-content-tree-workflow).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
