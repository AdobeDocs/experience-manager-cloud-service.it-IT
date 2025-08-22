---
title: Note sulla versione 2023.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2023.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: 0845447c1c4f47b77debd179f24eac95a0d2c2db
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 41%

---

# Note sulla versione 2023.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.11.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.11.0) è il venerdì 30 novembre 2023. La prossima versione funzionale (2023.12.0) è pianificata per il venerdì 14 dicembre 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di giugno 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programma per i primi utilizzatori {#sites-early-adopter}

**[Trova e sostituisci stringhe nei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: la console Frammenti di contenuto offre agli utenti un modo semplice e intuitivo per sostituire una stringa che appare in più frammenti di contenuto contemporaneamente, per velocizzare la velocità del contenuto.

![Trova e sostituisci](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Invia un&#39;e-mail a **aemcs-headless-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma early adopter.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Assets {#assets-view-features}

* **Editor Adobe Express integrato in AEM Assets**: gli utenti con accesso a Express ora dispongono di strumenti integrati di modifica e creazione delle immagini da Adobe Express e Adobe Firefly disponibili direttamente in AEM Assets per migliorare il riutilizzo dei contenuti e velocizzarne la realizzazione.

  ![assegnare il modulo metadati a una cartella](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Report sull&#39;utilizzo dello spazio di archiviazione in Insights**: gli amministratori ora possono visualizzare i report sull&#39;utilizzo dello spazio di archiviazione disponibili come parte di Insights.

  ![insight sull’utilizzo dell’archiviazione](/help/assets/assets/storage-usage-insights.png)

* **Ricerca nella prima configurazione della home page**: Experience Manager Assets ora consente di configurare l&#39;esperienza della home page per l&#39;organizzazione. Se, per la pagina Home, selezioni l’opzione Cerca prima, puoi configurare l’allineamento della barra di ricerca, l’immagine di sfondo e il logo della tua organizzazione.

  ![configurazione di Cerca prima](/help/assets/assets/search-first-configuration.png)

### Nuove funzioni nella versione prerelease per la visualizzazione Amministratore {#admin-view-features-prerelease}

**Anteprima video**: AEM Assets ora genera le rappresentazioni di anteprima di tutti i formati video supportati per impostazione predefinita, senza la necessità di configurare un profilo di elaborazione.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzionalità in [!DNL Experience Manager Forms] {#forms-features}

* **[Componente casella di controllo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: Forms adattivo basato su componenti core ora può includere un componente casella di controllo. Consente agli utenti di effettuare scelte binarie, selezionando o deselezionando una particolare opzione. In genere viene visualizzata come una piccola casella su cui è possibile fare clic o toccare per alternare due stati: selezionato e deselezionato. La casella di controllo è un elemento modulo comune utilizzato per presentare una scelta sì/no o vero/falso.

* **[Componente termini e condizioni](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Forms adattivo basato su componenti core può ora includere un componente termini e condizioni. Consente agli autori dei moduli di introdurre una sezione specifica all’interno del modulo in cui vengono presentati agli utenti i termini, le condizioni o gli accordi legali associati all’utilizzo di un servizio, un prodotto o una piattaforma. Questo componente è progettato per informare gli utenti sulle regole, le normative e gli obblighi che si impegnano a rispettare inviando il modulo.

  ![Casella di controllo, termini e condizioni e schede verticali](/help/forms/assets/forms-components.png)

* **[Componente schede verticali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Forms adattivo basato su componenti core ora può organizzare il contenuto del modulo in un elenco verticale di schede, fornendo un layout strutturato e navigabile. L’utilizzo di schede verticali in un modulo può migliorare l’esperienza utente complessiva semplificando la navigazione e migliorando l’organizzazione del contenuto del modulo, soprattutto nelle situazioni in cui un modulo contiene più sezioni o informazioni complesse.



### Nuove funzionalità in [!DNL Forms] versione prerelease {#prerelease-features-forms}

* **[Collegare un Forms adattivo all&#39;elenco Microsoft® SharePoint](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms fornisce un&#39;integrazione OOTB per inviare i dati dei moduli direttamente all&#39;elenco SharePoint, consentendo di sfruttare le funzionalità degli elenchi SharePoint. È possibile configurare Microsoft SharePoint List come origine dati per un modello dati modulo e utilizzare l&#39;azione di invio **Invia utilizzando il modello dati modulo** per connettere un modulo adattivo a SharePoint List.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programma per i primi utilizzatori {#forms-early-adopter}

* **Inviare un modulo adattivo allo scenario Adobe Workfront Fusion**: Forms as a Cloud Service offre opzioni pronte all’uso per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario di Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

* **Supporto lingue da destra a sinistra**: i moduli adattivi basati sui Componenti core ora possono essere presentati in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi per soddisfare questi diversi tipi di pubblico e per accedere ai mercati RTL. In alcune aree geografiche, fornire moduli nella lingua locale, è anche obbligatorio dal punto di vista legale. Adattandosi alle lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

  ![Supporto lingue da destra a sinistra](/help/forms/assets/right-to-left-language-support.png)

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### È Ora Possibile Concedere La Licenza Per Le Regole Del Filtro Del Traffico Di WAF {#cdn-waf-license}

Le Regole per il filtro del traffico sono state rilasciate a ottobre e includevano una nota relativa alla speciale categoria di regole del firewall per l’applicazione web (WAF) che sarebbero state disponibili più avanti nel corso dell’anno per integrare le regole già disponibili per i clienti di Sites e Forms. Come aggiornamento, è ora possibile concedere in licenza l&#39;offerta di protezione WAF-DDoS.

Una volta ottenuta la licenza, queste regole WAF avanzate possono essere distribuite alla rete CDN utilizzando la pipeline di configurazione di Cloud Manager per aggiungere un ulteriore livello di protezione contro gli attacchi web.

Leggi le [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md), incluso WAF. Rivolgiti al team del tuo account AEM per informazioni sulle licenze di WAF-DDoS Protection o Enhanced Security.

### Mappatura dei domini - Programma di adozione anticipata {#cdn-config-early-adopter}

Oltre alle [Regole filtro del traffico (incluso WAF)](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, è possibile utilizzare la pipeline di configurazione per dichiarare e distribuire altri tipi di configurazione CDN. Ci piacerebbe conoscere i tuoi casi d’uso, tra cui:
* 301/302 reindirizzamenti lato client
* proxy di richieste al server Edge di origini arbitrarie
* trasformazioni URL
* impostazione o modifica delle intestazioni di risposta o richiesta
* pagine di errore personalizzate quando la rete CDN non può raggiungere AEM
* autenticazione tramite nome utente/password
* qualsiasi altra configurazione CDN utile

Invia un&#39;e-mail a **aemcs-cdn-config-adopter@adobe.com** dal tuo ID e-mail ufficiale con il tuo feedback.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Problemi noti {#known-issues}

* Impossibile inviare il Forms adattivo basato sui componenti core. Il problema si verifica per Forms adattivo creato utilizzando i Componenti core versioni 2.0.38 - 2.0.60.

  Per risolvere il problema. puoi passare alla versione 2.0.62 o successiva dei componenti core del modulo adattivo. Per impostare una versione dei componenti core adattivi di Forms per il tuo ambiente, imposta le versioni delle dipendenze `core.forms.components.version`, `core.forms.components.af.version` e `core.wcm.components.version component` nel tuo archivio Forms as a Cloud Service o progetto basato su Archetipo AEM e distribuisci le modifiche nel tuo ambiente Forms as a Cloud Service. La versione più recente delle dipendenze dei Componenti core Forms adattivi è disponibile all&#39;indirizzo [Archivio Git dei Componenti core Forms adattivi](https://github.com/adobe/aem-core-forms-components#system-requirements).
