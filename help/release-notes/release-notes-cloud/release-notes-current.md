---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 6277325b80f1cdb8735f88b5ad856e405572bffe
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 2%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] come Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Per informazioni sugli aggiornamenti della documentazione non direttamente correlati a una versione, consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) .

## Data di rilascio {#release-date}

La data di rilascio di [!DNL Adobe Experience Manager] come versione corrente [!DNL Cloud Service] (2021.8.0) è il 26 agosto 2021.
La versione seguente (2021.9.0) è del 30 settembre 2021.

## Video sulla versione {#release-video}

Per un riepilogo delle funzioni aggiunte, guarda il video [Panoramica sulla versione di agosto 2021](https://video.tv.adobe.com/v/336277) .

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Quando condividi risorse digitali come collegamento, gli utenti possono copiare l’URL negli Appunti immediatamente. Questo miglioramento consente di condividere le risorse in modo più rapido e conveniente. Questa funzionalità consente una condivisione delle risorse più rapida e conveniente.

   ![Opzione Copia URL quando condividi una risorsa come collegamento](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Quando condividi una risorsa come collegamento, ora puoi copiare l’URL per condividerlo separatamente.*

* Quando carichi file TXT, i microservizi per le risorse generano automaticamente una miniatura. La miniatura PNG è una rappresentazione del file TXT che aiuta gli utenti a identificare il contenuto o i file in una certa misura, senza aprire i file. Questa funzionalità non richiede alcuna configurazione e funziona per impostazione predefinita.

   ![Un rendering di un file TXT viene generato automaticamente da  [!DNL Assets] in formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Viene generato automaticamente un rendering di un file TXT per identificare il file senza aprirlo.*

### Nuova funzione nel canale pre-rilascio [!DNL Assets] {#assets-prerelease-features}

* Gli utenti possono ora ordinare le risorse visualizzate nei risultati della ricerca nelle viste a colonne e a schede. L’ordinamento viene eseguito sulle colonne Nome, Creato, Modificato o Nessuno.

   ![Ordinare i risultati della ricerca  [!DNL Assets] nelle viste a colonne e a schede](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordina i risultati della ricerca  [!DNL Assets] nelle viste a colonne e a schede.*

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

* Quando un membro del gruppo di collaboratori accede alla console [!DNL Assets], viene generata una richiesta aggiuntiva `POST` per cercare di creare una raccolta. Questa richiesta non è necessaria, non riesce a causa di problemi di autorizzazioni e crea molti errori nei log. (CQ-4328856)
* Quando gli utenti visualizzano una risorsa e selezionano [!UICONTROL Timeline] dal menu a comparsa nel pannello a sinistra, viene visualizzato un errore. Nei registri, molti avvisi vengono registrati a causa di una query non valida. (CQ-4328919)

## [!DNL Experience Manager Forms] come  [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* AEM progetto Archetype per Forms as a Cloud Service ora include [modelli di tema e dati modulo Canvas 3.0 per Microsoft Dynamics e Salesforce.com](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment).

* **Documento di registrazione** basato su Acroform: AEM Forms as a Cloud Service supporta l’utilizzo del formato PDF  [Adobe Acrobat (PDF Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html)  come modello per il documento di record oltre al modello di modulo basato su XFA.

* **Connettore** archivio dati di Microsoft Azure: È ora possibile  [collegare il modello dati modulo a Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare dati adattivi del modulo in Microsoft Azure Storage as a BLOB.

### Funzione beta di [!DNL Forms] {#aug-what-is-new-forms-prerelease}

* **Connettore di storage unificato:** utilizza il connettore di archiviazione unificato per esternalizzare i dati in-process negli archivi gestiti dai clienti. Ad esempio
   * Abilita la funzionalità di salvataggio e ripresa di Forms Portal e archivia le bozze dei moduli adattivi in un archivio dati gestito dal cliente.
   * Archiviare i dati dei flussi di lavoro AEM in-process (AEM dati variabili di flusso di lavoro) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [Communication ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) APIshelp combina modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che consentono di:
   * Genera i documenti compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare file PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere su [!DNL formscsbeta@adobe.com] per iscriverti al programma beta.

### Nuove funzioni disponibili nel canale pre-rilascio [!DNL Forms] {#prerelease-features-forms}

* **Utilizzare i ruoli Adobe Sign in un modulo** adattivo: Adobe Sign per i livelli di servizio aziendali e aziendali ha la possibilità di espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, in modo da soddisfare meglio i requisiti del flusso di lavoro. Ora è possibile [abilitare ogni destinatario dell&#39;accordo a configurare il proprio ruolo in un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform), con il firmatario come ruolo predefinito.

* **Analytics per Forms** adattivo: È ora possibile acquisire e tenere traccia del comportamento dell’utente finale tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sull’utente finale. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Collega facilmente AEM Forms con Microsoft Dynamics e Salesforce.com**: Il servizio fornisce modelli di dati e configurazione dell’origine dati preconfigurati per Microsoft Dynamics e Salesforce.com, consentendo agli sviluppatori di configurare Microsoft Dynamics e Salesforce.com come origini dati per un modulo [ adattivo in modo ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html)più rapido e semplice.

## [!DNL Screens] come  [!DNL Cloud Service] {#screens}

### Novità {#what-is-new-screens}

* In qualità di autore del contenuto, ora puoi definire una miniatura per i video in modo da poter utilizzare l’immagine come segnaposto e testare correttamente la riproduzione e il targeting del contenuto, mentre il video effettivo è in fase di finalizzazione da parte del team appropriato.
Per ulteriori informazioni, consulta [Monitoraggio di base della riproduzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) .

* Supporto delle miniature per i video in ora supportato in Screens come Cloud Service. Un autore di contenuti può definire una miniatura per i video in modo che l’immagine possa essere utilizzata come segnaposto e possa testare correttamente la riproduzione e il targeting del contenuto, mentre il video effettivo viene finalizzato dal team appropriato. L&#39;immagine può anche essere utilizzata, nel caso in cui la riproduzione del video non riesca.

### Correzioni di bug {#bug-fixes-screens}

* Impossibile visualizzare il contenuto dalla pagina incorporata. Il problema è stato risolto.

* Dopo l&#39;accesso, passare alla pagina (canali) predefinita è finita in una pagina di errore del server interno.

* Le voci di tag associate non sono state rimosse durante la rimozione delle playlist.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuova interfaccia utente del selettore categorie per migliorare l’esperienza utente, aumentare l’efficienza e migliorare il supporto per cataloghi di prodotti complessi

   ![Selezione nuova categoria](/help/assets/CIF/category-picker.png)

* Supporto migliorato per A11Y per i componenti core CIF

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data di rilascio {#release-date-cm-aug}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.8.0 è il 12 agosto 2021.
La prossima versione è prevista per il 9 settembre 2021.

### Novità {#what-is-new-aug}

* I clienti del Cloud Service ora possono visualizzare i rapporti SLA (Service Level Agreement) in Cloud Manager. Ciò sarà progressivamente reso disponibile nei prossimi mesi.
Per ulteriori informazioni, consulta [Generazione di rapporti SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) .

* Il tipo e la gravità delle regole di qualità IndexType e `IndexDamAssetLucene` sono stati modificati. Questi sono ora due bug di Blocker *serverity*.

* Sono state introdotte nuove regole sulla qualità dell&#39;indice Oak per coprire configurazioni asincrone e tika.

* Aumenta il numero massimo di certificati SSL per programma a 50.

* Funzionalità self-service per consentire agli utenti di creare e gestire più archivi tramite l’interfaccia utente di Cloud Manager.

* SonarQube leggeva inutilmente i dati della cronologia Git. Su basi di codice di grandi dimensioni, ciò potrebbe comportare una multa non necessaria per le prestazioni della build.

* È ora disponibile un’API per annullare la validità della cache di dipendenza Maven per pipeline.

* La versione di AEM Project Archetype utilizzata da Cloud Manager è stata aggiornata alla versione 29.

### Correzioni di bug {#bug-fixes-aug}

* Lo stato Aggiorna disponibile non deve essere visualizzato quando l&#39;ultima versione è inferiore alla versione corrente.

* L&#39;onboarding iniziale non riusciva per le nuove organizzazioni con nomi molto lunghi.

* Talvolta, quando una pipeline viene attivata due volte per qualche motivo, si verifica un errore di una delle esecuzioni che non riesce con *non è in grado di aggiornare lo stato di esecuzione della pipeline*.

## Strumento Content Transfer (Trasferimento contenuti)  {#content-transfer-tool}

### Data di rilascio {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.5.6 è l’11 agosto 2021.

### Correzioni di bug {#bug-fixes-ctt}

* In alcuni casi non tutti gli utenti sono stati migrati all’istanza di destinazione. Per ottenere questa correzione è necessario CTT v1.5.6 insieme alla versione aem-ethos-tools 1.2.354 o successiva sul AEM di destinazione come istanza di Cloud Service.

* Il pulsante **Interrompi acquisizione** veniva disattivato durante l’acquisizione nell’istanza Publish. Questo non è necessario perché non esiste un passaggio di ripristino mongo durante l’acquisizione di Publish.

* Il CTT non ha ripulito la directory `/tmp` dopo un’estrazione riuscita. Ciò a volte ha causato problemi di spazio su disco.

