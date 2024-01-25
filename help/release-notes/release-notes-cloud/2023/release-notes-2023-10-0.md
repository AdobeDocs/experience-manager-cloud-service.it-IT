---
title: Note sulla versione 2023.10.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.10.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
source-git-commit: 811a8f4d83a1034737c23b1707a24b52742fef55
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 50%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.10.0) è il venerdì 26 ottobre 2023. La prossima versione funzionale (2023.11.0) è pianificata per il venerdì 30 novembre 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video di panoramica sulla versione di ottobre 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni {#assets-features}

**Componente aggiuntivo AEM Assets per Adobe Express**: Experience Manager Assets ora fornisce un’ [componente aggiuntivo per Adobe Express](/help/assets/addon-adobe-express.md). Il componente aggiuntivo consente di accedere direttamente alle risorse memorizzate in Experience Manager Assets dall’interfaccia utente di Adobi Express. Puoi inserire il contenuto gestito in AEM Assets nell’area di lavoro di Express e quindi salvare il contenuto nuovo o modificato in un archivio AEM Assets. Il componente aggiuntivo offre i seguenti vantaggi chiave:

* Maggiore riutilizzo dei contenuti grazie alla modifica e al salvataggio di nuove risorse in AEM

* Riduzione del tempo e dell&#39;impegno necessari per creare nuove risorse o nuove versioni di risorse esistenti

  ![Includi risorse dal componente aggiuntivo Risorse](/help/assets/assets/aem-assets-add-on-include-assets.png)

### Nuove funzioni nella Vista risorse {#assets-view-features}

* **Importa risorse in blocco dall&#39;origine dati di OneDrive**: gli amministratori possono ora: [importa un numero elevato di risorse da OneDrive ad AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). L&#39;elenco aggiornato delle origini dati supportate per l&#39;importazione in blocco include Azure, AWS, Google Cloud, Dropbox e OneDrive.

  ![assegnare un modulo di metadati a una cartella](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **Supporto di diritti per più organizzazioni per le librerie**: Experience Manager Assets ora consente di configurare l’accesso alle librerie Creative Cloud in un’organizzazione IMS diversa. Questo consente di accedere più facilmente ai flussi di lavoro di prodotti più recenti tra Creative Cloud e Experience Manager, riducendo i tempi e agevolando il lavoro dei creativi.

### Funzioni pre-release disponibili in [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [supporto di tracce con più sottotitoli e multi-audio per video in Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): è ora possibile aggiungere facilmente più sottotitoli e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono gestire anche i sottotitoli e le tracce audio da una singola scheda nell’interfaccia utente.

  ![Scheda Sottotitoli e tracce audio nella pagina Proprietà di una risorsa video selezionata.](/help/release-notes/assets/msma-aem-cs.png)*Scheda Sottotitoli e tracce audio nella pagina Proprietà di una risorsa video selezionata.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Experience Manager Forms] {#forms-features}

* **[Proprietà personalizzate per Adaptive Forms](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**: è possibile associare attributi personalizzati (coppie chiave-valore) a un modello di modulo o a un componente moduli adattivi per consentire agli sviluppatori di moduli di fornire comportamenti di moduli dinamici che si adattano in base ai valori di tali attributi personalizzati. Ad esempio, gli sviluppatori possono creare diverse rappresentazioni di un componente Forms headless su piattaforme mobili, desktop o web, in base ai valori degli attributi personalizzati, migliorando in modo significativo l’esperienza utente su un’ampia gamma di dispositivi.

* **Temi e modelli**: avvia il processo di creazione dei moduli con nuovi temi e modelli, personalizzati per abilitare professionisti esperti e nuovi autori di moduli. Creati direttamente utilizzando i componenti core per moduli adattivi, questi temi e modelli meticolosamente curati consentono di iniziare a creare moduli rapidamente per i casi d’uso più comuni.

  ![Modelli pronti all’uso](/help/forms/assets/form-templates-ootb.png)


### Programma di adozione anticipata {#forms-early-adopter}

* **[Protect i tuoi documenti con le API DocAssurance (parte delle API di comunicazione)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance ti consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite la crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo livello di protezione aumentato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Puoi scrivere a `aem-forms-early-adopter-program@adobe.com` dal tuo id e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Regole filtro del traffico, incluso WAF {#traffic-filter-rules-waf}

[Filtra il traffico sulla rete CDN gestita dell’Adobe](/help/security/traffic-filter-rules-including-waf.md) dichiarando le regole che corrispondono al traffico del sito web in base alle proprietà, inclusi URL, indirizzo IP e agente utente, oppure impostando limiti di velocità di traffico personalizzati per evitare attacchi DoS. I clienti possono inoltre concedere in licenza un set di regole WAF (Web Application Firewall) avanzate per una protezione aggiuntiva contro le minacce sofisticate dei siti Web.

Ti invitiamo a familiarizzare con le regole del filtro del traffico [prova di un tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html?lang=it)! Illustra i passaggi necessari per configurare una nuova pipeline di configurazione di Cloud Manager, dichiarare le regole in un file di configurazione e analizzare i registri CDN per rilevare eventuale traffico dannoso.

Le regole del filtro del traffico sono ora disponibili sugli ambienti di sviluppo, con un rollout graduale negli ambienti di staging e produzione a novembre. Puoi richiedere l’accesso anticipato all’ambiente di staging e produzione inviando una e-mail all’indirizzo **aemcs-waf-adopter@adobe.com**.

Le regole avanzate del filtro del traffico WAF possono essere concesse in licenza entro la fine dell&#39;anno tramite le offerte di sicurezza avanzata o protezione WAF-DDoS.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
