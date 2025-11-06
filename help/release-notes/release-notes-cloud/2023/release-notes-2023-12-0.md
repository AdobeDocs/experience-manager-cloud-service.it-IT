---
title: Note sulla versione 2023.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2023.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: b36add58-a2ba-4299-94be-e0026e9c553c
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 72%

---

# Note sulla versione 2023.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.12.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.12.0) è il venerdì 14 dicembre 2023. La prossima versione funzionale (2024.1.0) è pianificata per il giovedì 25 gennaio 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programma per i primi utilizzatori {#sites-early-adopter}

**Puoi sfruttare il [servizio di telemetria operativa](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** per abilitare la raccolta lato client per AEM as a Cloud Service.

Il servizio dati di telemetria operativa offre una riflessione più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Inoltre, per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a `aemcs-rum-adopter@adobe.com` insieme al nome di dominio per l&#39;ambiente di produzione, stage e sviluppo dal tuo indirizzo e-mail associato al tuo Adobe ID. Il team di prodotto di Adobe abiliterà quindi il servizio dati di telemetria operativa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Assets {#assets-view-features}

**Creare immagini basate su IA generativa con Adobe Firefly**

Creazione di nuove immagini basate su query di ricerca con integrazione della funzione testo-immagine di Adobe Firefly (richiede una licenza Adobe Firefly).

![Integrazione Firefly per Assets](/help/assets/assets/assets-firefly-integration.png)

**Trovare immagini simili**

Ora è possibile trovare facilmente il contenuto selezionando un’immagine e visualizzando immagini simili nell’archivio di Experience Manager Assets.

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzionalità in [!DNL Experience Manager Forms] {#forms-features}

* **[Connessione di un Forms adattivo all&#39;elenco Microsoft® SharePoint](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms fornisce un&#39;integrazione OOTB per inviare i dati dei moduli direttamente all&#39;elenco SharePoint, consentendo l&#39;utilizzo delle funzionalità degli elenchi di SharePoint. È possibile configurare Microsoft SharePoint List come origine dati per un modello dati modulo e utilizzare l&#39;azione di invio **Invia utilizzando il modello dati modulo** per connettere un modulo adattivo a SharePoint List.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programma per i primi utilizzatori {#forms-early-adopter}

* **[Inviare un modulo adattivo allo scenario Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service offre opzioni pronte all’uso per collegare facilmente un modulo adattivo ad Adobe Workfront. Questo semplifica il processo di invio di un modulo adattivo a uno scenario di Adobe Workfront, consentendoti di attivare uno scenario Workfront Fusion all’invio di un modulo adattivo.

* **[Supporto lingue da destra a sinistra](/help/forms/supporting-new-language-localization-core-components.md)**: i moduli adattivi basati sui Componenti core ora possono essere presentati in una lingua da destra a sinistra (RTL) come l’arabo, il persiano e l’urdu. Le lingue RTL sono parlate da oltre 2 miliardi di persone in tutto il mondo. L’utilizzo di un modulo in linguaggio RTL consente di estendere la portata dei moduli adattivi in modo da soddisfare questi diversi tipi di pubblico e selezionarli in mercati RTL. In alcune aree geografiche, fornire moduli nella lingua locale, è anche obbligatorio dal punto di vista legale. Adattandosi alle lingue locali, non solo si aprono le porte a un pubblico più ampio, ma si garantisce anche la conformità con le leggi e i regolamenti pertinenti.

  ![Supporto lingue da destra a sinistra](/help/forms/assets/right-to-left-language-support.png)

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Mappatura dei domini - Programma di adozione anticipata {#cdn-config-early-adopter}

Oltre alle [Regole filtro del traffico](/help/security/traffic-filter-rules-including-waf.md) rilasciate di recente, che includono le regole del firewall dell&#39;applicazione Web (WAF) facoltativamente consentite, è possibile utilizzare la pipeline di configurazione per dichiarare e distribuire altri tipi di configurazione CDN. Ci piacerebbe conoscere i tuoi casi d’uso, tra cui:

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
