---
title: Note sulla versione 2023.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2023.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 98%

---

# Note sulla versione 2023.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.10.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.10.0) è il 26 ottobre 2023. La prossima versione funzionale (2023.11.0) è pianificata per il 30 novembre 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video di panoramica sulla versione di ottobre 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni {#assets-features}

**Componente aggiuntivo AEM Assets per Adobe Express**: Experience Manager Assets fornisce ora un componente aggiuntivo, ad Adobe Express. Il componente aggiuntivo consente di accedere direttamente alle risorse memorizzate in Experience Manager Assets dall’interfaccia utente di Adobe Express. Il contenuto gestito in AEM Assets può essere inserito nell’area di lavoro di Express e quindi il contenuto nuovo o modificato può essere salvato in un archivio AEM Assets. Il componente aggiuntivo offre i seguenti vantaggi chiave:

* maggiore riutilizzo dei contenuti grazie alla modifica e al salvataggio di nuove risorse in AEM

* riduzione del tempo e dell’impegno necessari per creare nuove risorse o nuove versioni di risorse esistenti

  ![inclusione delle risorse dal componente aggiuntivo di Assets](/help/assets/assets/aem-assets-add-on-include-assets.png)

### Nuove funzioni nella Vista risorse {#assets-view-features}

* **Importazione in blocco delle risorse dall’origine dati di OneDrive**: gli amministratori possono ora [importare un numero elevato di risorse da OneDrive a AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). L’elenco aggiornato delle origini dati supportate per l’importazione in blocco include Azure, AWS, Google Cloud, Dropbox e OneDrive.

  ![assegnare il modulo metadati a una cartella](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **Supporto di diritti tra diverse organizzazioni per le librerie**: Experience Manager Assets ora consente di configurare l’accesso alle librerie Creative Cloud in un’organizzazione IMS diversa. Consente di accedere più facilmente ai flussi di lavoro di prodotti più recenti tra Creative Cloud e Experience Manager, riducendo i tempi e gli sforzi dei creativi.

### Funzioni pre-release disponibili in [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [supporto di tracce con più didascalie e multi-audio per video in Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): è ora possibile aggiungere facilmente più didascalie e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono gestire anche le didascalie e le tracce audio da una singola scheda nell’interfaccia utente.

  ![Scheda Didascalie e Tracce audio nella pagina Proprietà di una risorsa video selezionata.](/help/release-notes/assets/msma-aem-cs.png)*Scheda Didascalie e Tracce audio nella pagina delle Proprietà di una risorsa video selezionata.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Experience Manager Forms] {#forms-features}

* **[Proprietà personalizzate per Moduli adattivi](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**: è possibile associare attributi personalizzati (coppie valore-chiave) a un modello di modulo o a un componente di moduli adattivi per consentire agli sviluppatori di fornire comportamenti di modulo dinamico che si adattano in base ai valori di tali attributi personalizzati. Ad esempio, gli sviluppatori possono creare diverse rappresentazioni di un componente di moduli headless su piattaforme mobili, desktop o web, in base ai valori di attributi personalizzati, migliorando in modo significativo l’esperienza utente su un’ampia gamma di dispositivi.

* **Temi e modelli**: avvia il processo di creazione di moduli con nuovi temi e modelli, personalizzati per rendere autonomi professionisti esperti e nuovi autori di moduli. Creati in modo semplice utilizzando i Componenti core dei moduli adattivi, questi temi e modelli meticolosamente curati consentono di iniziare a creare moduli rapidamente per i casi d’uso comuni.

  ![Modelli predefiniti](/help/forms/assets/form-templates-ootb.png)


### Programma per i primi utilizzatori {#forms-early-adopter}

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Regole del filtro del traffico, incluse le regole WAF {#traffic-filter-rules-waf}

[Filtrare il traffico sulla rete CDN gestita da Adobe](/help/security/traffic-filter-rules-including-waf.md) dichiarando le regole che corrispondono al traffico del sito web in base alle proprietà, inclusi URL, indirizzo IP e agente utente, oppure impostando limiti di velocità di traffico personalizzati per evitare attacchi DoS. La clientela può inoltre autorizzare un set di regole WAF (Web Application Firewall) avanzate per una protezione aggiuntiva contro le minacce sofisticate dei siti Web.

Ti invitiamo a familiarizzare con le regole di filtro del traffico [provando un tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html?lang=it). Tale tutorial illustra i passaggi necessari per configurare una nuova pipeline di configurazione Cloud Manager, dichiarare le regole in un file di configurazione e analizzare i registri CDN per rilevare eventuale traffico dannoso.

Le regole di filtro del traffico sono disponibili ora negli ambienti di sviluppo, con un’implementazione graduale negli ambienti di staging e produzione a novembre. Puoi richiedere l’accesso anticipato all’ambiente di staging e produzione inviando una e-mail all’indirizzo **aemcs-waf-adopter@adobe.com**.

Le regole avanzate per il filtro del traffico WAF possono essere autorizzate entro la fine dell’anno tramite le offerte di sicurezza avanzata o protezione WAF-DDoS.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
