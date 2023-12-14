---
title: Note sulla versione 2023.11.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.11.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
source-git-commit: c33874869bccae1e9837b30827a655e70636dd56
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 13%

---


# Note sulla versione 2023.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.11.0) è il venerdì 30 novembre 2023. La successiva versione funzionale (2023.12.0) è pianificata per il venerdì 14 dicembre 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di novembre 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programma Early Adopter {#sites-early-adopter}

**[Trovare e sostituire stringhe nei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: la console Frammenti di contenuto offre agli utenti un modo semplice e intuitivo di sostituire una stringa che appare contemporaneamente in più frammenti di contenuto per accelerare la velocità dei contenuti.

![Trova e sostituisci](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

Ti interessa provare questa funzione e condividere feedback? Invia un messaggio e-mail a **aemcs-headless-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma early adopter.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Risorse {#assets-view-features}

* **Editor Adobe Express incorporato in AEM Assets**: gli utenti con accesso a Express ora dispongono di strumenti integrati di modifica e creazione delle immagini da Adobi Express e Adobe Firefly disponibili direttamente in AEM Assets per migliorare il riutilizzo dei contenuti e accelerarne la velocità.

  ![assegnare il modulo metadati a una cartella](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Rapporti sull’utilizzo dello spazio di archiviazione in Insights**: gli amministratori ora possono visualizzare i rapporti sull’utilizzo dello storage disponibili come parte di Insights.

  ![informazioni sull&#39;utilizzo dello storage](/help/assets/assets/storage-usage-insights.png)

* **Cerca la prima configurazione della homepage**: Experience Manager Assets ora consente di configurare l’esperienza della pagina home per la tua organizzazione. Se si seleziona Cerca come pagina iniziale, è possibile configurare l&#39;allineamento della barra di ricerca, l&#39;immagine di sfondo e il logo per l&#39;organizzazione.

  ![cerca prima configurazione](/help/assets/assets/search-first-configuration.png)

### Nuove funzioni nella versione prerelease per la visualizzazione Amministratore {#admin-view-features-prerelease}

**Anteprima video**: AEM Assets ora genera per impostazione predefinita le rappresentazioni in anteprima di tutti i formati video supportati, senza la necessità di configurare un profilo di elaborazione.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Experience Manager Forms] {#forms-features}

* **[Componente casella di controllo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: il Forms adattivo basato sui Componenti core ora può includere un componente casella di controllo. Consente agli utenti di effettuare scelte binarie, selezionando o deselezionando una particolare opzione. In genere viene visualizzata come una piccola casella su cui è possibile fare clic o toccare per alternare due stati: selezionato e deselezionato. La casella di controllo è un elemento modulo comune utilizzato per presentare una scelta sì/no o vero/falso.

* **[Componente termini e condizioni](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Forms adattivo basato su componenti core ora può includere un componente Termini e condizioni. Consente agli autori dei moduli di introdurre una sezione specifica all’interno del modulo in cui vengono presentati agli utenti i termini, le condizioni o gli accordi legali associati all’utilizzo di un servizio, un prodotto o una piattaforma. Questo componente è progettato per informare gli utenti sulle regole, le normative e gli obblighi che si impegnano a rispettare inviando il modulo.

  ![Casella di controllo, Termini e condizioni e scheda Verticale](/help/forms/assets/forms-components.png)

* **[Componente Schede verticali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Forms adattivo basato su Componenti core ora può organizzare il contenuto del modulo in un elenco verticale di schede, fornendo un layout strutturato e navigabile. L’utilizzo di schede verticali in un modulo può migliorare l’esperienza utente complessiva semplificando la navigazione e migliorando l’organizzazione del contenuto del modulo, soprattutto nelle situazioni in cui un modulo contiene più sezioni o informazioni complesse.



### Nuove funzioni in [!DNL Forms] Versione prerelease {#prerelease-features-forms}

* **[Collegare un Forms adattivo all’elenco di Microsoft® SharePoint](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms fornisce un’integrazione OOTB per inviare i dati dei moduli direttamente a SharePoint List, consentendoti di sfruttare le funzionalità di SharePoint Lists. È possibile configurare Microsoft SharePoint List come origine dati per un modello dati modulo e utilizzare **Invia utilizzando il modello dati modulo** azione di invio per collegare un modulo adattivo a Elenco SharePoint.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programma Early Adopter {#forms-early-adopter}

* **Inviare un modulo adattivo allo scenario Adobe Workfront Fusion**: Forms as a Cloud Service offre opzioni pronte all’uso per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

* **Supporto lingue da destra a sinistra**: il Forms adattivo basato sui Componenti core ora può essere presentato in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi per soddisfare questi diversi tipi di pubblico e per accedere ai mercati RTL. In alcune regioni, è anche un mandato legale fornire moduli nella lingua locale. Accogliendo le lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

  ![Supporto lingue da destra a sinistra](/help/forms/assets/right-to-left-language-support.png)

* **[Protect i tuoi documenti con le API DocAssurance (parte delle API di comunicazione)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance ti consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite la crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da occhi non autorizzati, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Puoi scrivere a `aem-forms-early-adopter-program@adobe.com` dal tuo id e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### È ora possibile concedere la licenza alle regole del filtro del traffico WAF {#cdn-waf-license}

Le regole per il filtro del traffico sono state rilasciate a ottobre e includevano una nota sulla disponibilità della categoria speciale di regole WAF (Web Application Firewall) nel corso di quest’anno, per integrare le regole già disponibili per i clienti Sites e Forms. Come aggiornamento, è ora possibile concedere in licenza l&#39;offerta di protezione WAF-DDoS.

Una volta ottenuta la licenza, queste regole WAF avanzate possono essere distribuite alla rete CDN utilizzando la pipeline di configurazione di Cloud Manager per aggiungere un ulteriore livello di protezione contro gli attacchi web.

Ulteriori informazioni [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md), incluso WAF. Rivolgiti al tuo account team AEM per informazioni sulla concessione di licenze per la protezione WAF-DDoS o la sicurezza avanzata.

### Programma di adozione anticipata configurazione CDN {#cdn-config-early-adopter}

Oltre agli ultimi [Regole filtro traffico (incluso WAF)](/help/security/traffic-filter-rules-including-waf.md)Inoltre, esiste l’opportunità di utilizzare la pipeline di configurazione per dichiarare e distribuire altri tipi di configurazione CDN. Ci piacerebbe conoscere i tuoi casi d’uso, tra cui:
* 301/302 reindirizzamenti lato client
* trasferimento di richieste al server Edge di a origini arbitrarie
* Trasformazioni URL
* impostazione o modifica delle intestazioni di richiesta o risposta
* pagine di errore personalizzate quando la rete CDN non può raggiungere l’AEM
* autenticazione tramite nome utente/password
* qualsiasi altra configurazione CDN utile

Invia un messaggio e-mail a **aemcs-cdn-config-adopter@adobe.com** dal tuo ID e-mail ufficiale con il tuo feedback.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Problemi noti {#known-issues}

* Impossibile inviare il Forms adattivo basato sui componenti core. Il problema si verifica per Forms adattivo creato utilizzando i Componenti core versioni 2.0.38 - 2.0.60.

  Per risolvere il problema. puoi passare alla versione 2.0.62 o successiva dei componenti core del modulo adattivo. Per impostare una versione dei Componenti core Forms adattivi per il tuo ambiente: [impostare le versioni dei componenti core.forms.components.version, core.forms.components.af.version e core.wcm.components.version](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository) dipendenze nell’archivio Forms as a Cloud Service o nel progetto basato su AEM Archetipo e [implementare le modifiche nell’ambiente as a Cloud Service Forms](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment). La versione più recente delle dipendenze dei Componenti core adattivi di Forms è disponibile all’indirizzo [Archivio Git dei Componenti core di Forms adattivi](https://github.com/adobe/aem-core-forms-components#system-requirements).
