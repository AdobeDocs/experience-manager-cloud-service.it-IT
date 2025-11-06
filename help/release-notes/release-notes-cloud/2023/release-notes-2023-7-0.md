---
title: Note sulla versione 2023.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2023.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 7866d94c-e54c-4bb2-aaa6-66c019e46336
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 100%

---

# Note sulla versione 2023.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.7.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.7.0) è il 27 luglio 2023. La successiva versione funzionale (2023.8.0) è pianificata per il 31 agosto 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di luglio 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* MSM per frammenti di contenuto. AEM Multisite Manager è ora disponibile per i frammenti di contenuto, che consentono di creare Live Copy dei frammenti di contenuto per la distribuzione in blocco dei contenuti. I controlli di ereditarietà granulari sono disponibili fino al livello Elemento frammento di contenuto e Variante.

### Nuove funzioni nella versione pre-release di [!DNL Experience Manager Sites] {#prerelease-sites}

* La [Console Frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=it) ora consente agli utenti di visualizzare i tag e di effettuare ricerche per tag applicati come metadati ai frammenti di contenuto. Per usufruire di questa funzionalità, gli utenti non dovranno più passare all’interfaccia utente Assets, riducendo così i passaggi da un contesto all’altro e migliorando l’efficienza.

![Assegnazione di tag nella console Frammenti di contenuto](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Risorse {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**Framework di intelligenza artificiale migliorato per i tag avanzati delle immagini**

Experience Manager Assets ora utilizza un framework di intelligenza artificiale migliorato per i tag avanzati delle immagini. Offre un livello di intelligence sui contenuti che migliora la pertinenza e la precisione dei tag avanzati per tutte le risorse di tipo immagine al momento della loro acquisizione.

**Configurare la visualizzazione delle colonne per la vista Elenco risorse**

Assets Essentials ora consente di selezionare le colonne da visualizzare nella vista Elenco risorse, ad esempio Stato, Formato, Dimensioni, Dimensione file e così via.

![Colonne configurabili](/help/release-notes/assets/configure-columns.png)

**Ordinare i risultati della ricerca in base alla rilevanza**

Per impostazione predefinita, Assets Essentials ora ordina i risultati della ricerca in base alla rilevanza. Puoi ordinare le risorse trovate in ordine crescente o decrescente per `Name`, `Relevance`, `Size`, `Modified` e `Created`.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Temi predefiniti**](/help/forms/using-themes-in-core-components.md) **e modelli**: velocizza il processo di creazione dei moduli con i nostri temi e modelli pronti all’uso, personalizzati per consentirne l’utilizzo da parte sia di professionisti esperti che di nuovi autori di moduli. Creati direttamente utilizzando i componenti core per moduli adattivi, questi temi e modelli meticolosamente curati consentono di iniziare a creare moduli rapidamente per i casi d’uso più comuni.

* **[Componenti React per moduli headless](https://github.com/adobe/aem-forms-headless-components/tree/main/packages/react-vanilla-components)**: ora puoi visualizzare in anteprima e personalizzare le rappresentazioni di moduli adattivi headless con i componenti React pronti all’uso. Questi componenti utilizzano le classi BEM dei componenti core per moduli adattivi per la creazione di stili, semplificandone la personalizzazione dell’aspetto in base a requisiti specifici.

* [**Crea moduli adattivi con sezioni ripetibili**](/help/forms/create-forms-repeatable-sections.md): ora puoi realizzare un modello adattivo basato su componenti [Pannello a soffietto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=it), [Procedura guidata](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=it), [Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) e [Schede orizzontali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=it) ripetibili per l’acquisizione di più record di dati.  Queste sezioni ripetibili consentono di fornire facilmente più immissioni di dati. È utile quando le istanze di dati richieste non sono note in anticipo. Un compilatore può aggiungere o rimuovere facilmente le sezioni, rendendo i moduli adattabili a scenari di immissione dati diversi e semplificando la raccolta di più occorrenze degli stessi record di dati.


### Funzioni pre-release disponibili in [!DNL Forms]  {#pre-release-features-available-in-forms-channel}

* [**Supporto Google reCAPTCHA Enterprise**](/help/forms/captcha-adaptive-forms.md): utilizza Google reCAPTCHA Enterprise in un modulo adattivo per fornire maggiore protezione contro attività fraudolente e spam, per un’esperienza utente più sicura. Grazie all’analisi avanzata dei rischi e all’integrazione diretta, gli utenti autentici possono inviare facilmente i moduli mentre i bot vengono bloccati in modo efficace.

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i [moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) per consentire a chi sviluppa di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfruttare la potenza di Adobe Experience Manager Forms

È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Centro azioni {#actions-center}

Iscriviti per ricevere notifiche e-mail in caso di incidenti critici che richiedono un intervento immediato, e consigli personalizzati per ottimizzare il tuo sito. [Centro azioni](/help/operations/actions-center.md) funge da hub in cui è possibile esaminare questi avvisi, ad esempio le code di replica bloccate o le credenziali in scadenza, e contrassegnarli come risolti.

![Schermata Centro azioni](/help/assets/assets/actions-center.png)

### Programma per i primi utilizzatori delle regole CDN e WAF {#waf-early-adopter}

Filtra il traffico sulla rete CDN in base a:

* intestazioni e proprietà delle richieste (ad esempio, indirizzo IP)
* modelli di traffico noti associati a traffico dannoso

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma per i primi utilizzatori. Lo spazio è limitato.

Ulteriori informazioni su questa funzione sono disponibili in [questo articolo](/help/security/traffic-filter-rules-including-waf.md).

### Altre modifiche di base {#other-foundation-changes}

* Durante la settimana del 7 agosto, quando le richieste alle istanze AEM superavano un livello valido, AEM restituiva il codice di errore 429 invece del codice di errore 503. [Ulteriori informazioni](/help/implementing/developing/introduction/development-guidelines.md).

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
