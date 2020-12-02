---
title: Norme sulla protezione dei dati e sulla privacy dei dati - Adobe Experience Manager come Cloud Service di prontezza
description: 'Scopri Adobe Experience Manager come supporto Cloud Service per le varie normative sulla protezione dei dati e la privacy dei dati; incluso il Regolamento generale sulla protezione dei dati (GDPR) dell''UE, il California sulla privacy Act e le modalità per conformarsi all''implementazione di una nuova AEM come progetto di Cloud Service. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---


# Adobe Experience Manager come Cloud Service di preparazione per le normative sulla protezione dei dati e la privacy dei dati {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto del presente documento non costituisce consulenza giuridica e non è inteso come sostituto della consulenza legale.
>
>Consulta l&#39;ufficio legale della tua azienda per consigli in merito alle normative sulla protezione dei dati e sulla privacy dei dati.

>[!NOTE]
>
>Per ulteriori informazioni  risposta  Adobe ai problemi di privacy e ciò che ciò significa per voi in quanto clienti  Adobe, vedere [ Adobe Centro per la privacy](https://www.adobe.com/privacy.html).

 Adobe fornisce documentazione e procedure (con API quando disponibili), affinché l&#39;amministratore della privacy del cliente o l&#39;amministratore AEM possa gestire le richieste di protezione dei dati e privacy dei dati e aiutare i nostri clienti a rispettare queste normative. Le procedure documentate consentiranno ai clienti di eseguire le richieste normative manualmente o chiamando le API, se disponibili, da un portale o servizio esterno.

>[!CAUTION]
>
>I dettagli qui documentati sono limitati ad Adobe Experience Manager come Cloud Service.
>
>I dati provenienti da un altro servizio on-demand  Adobe, insieme a tutte le relative richieste di privacy, richiederanno l&#39;adozione di misure per tale servizio.
>
>Per ulteriori informazioni, vedere [ Adobe  Centro per la privacy](https://www.adobe.com/privacy.html).

## Introduzione {#introduction}

Le istanze di Adobe Experience Manager come Cloud Service, e le applicazioni che vi vengono eseguite, sono di proprietà e gestite dai nostri clienti.

Di conseguenza, le normative sulla protezione dei dati, come il GDPR, l&#39;CCPA e altri, sono in gran parte responsabilità dei clienti.

Per una breve introduzione, le norme sulla privacy e la protezione dei dati comprendono nuove regole da seguire per:

* Entità commerciali (CCPA) e/o controllori dati (GDPR)

* Fornitori di servizi (CCPA) e/o processori di dati (GDPR)

Le disposizioni principali di tali regolamenti sono:

1. Definizione estesa di dati personali per includere tutti gli ID univoci; come in dati direttamente e indirettamente identificabili.

2. Requisiti di consenso rafforzati.

3. Maggiore attenzione ai diritti di eliminazione (Data Erasure).

4. Rifiuto della vendita di dati.

Per Adobe Experience Manager come Cloud Service:

* Le istanze e le applicazioni che vengono eseguite su di esse sono di proprietà e gestite dal cliente.

   * Ciò significa che il cliente gestisce efficacemente i ruoli normativi, tra cui Business Entities e Service Provider, Data Controller e Data Processor, tra gli altri.

   * L&#39;Adobe Experience Platform Privacy Service  non farà parte del flusso di lavoro per AEM, come illustrato nel diagramma seguente.

* AEM include la documentazione e le procedure per l&#39;amministratore della privacy del cliente e/o l&#39;amministratore AEM per l&#39;esecuzione delle richieste relative alla normativa sulla privacy; manualmente o tramite API, se disponibili.

* Non è stato aggiunto alcun nuovo servizio o interfaccia utente.

   * Le procedure e le API sono invece documentate per l&#39;utilizzo da parte dell&#39;interfaccia utente/portali del cliente che gestisce le richieste di informativa sulla privacy.

* AEM non includerà alcuno strumento out-of-the-box per supportare il flusso di lavoro delle richieste di privacy.

   *  Adobe fornirà la documentazione e le procedure per l&#39;amministratore della privacy del cliente e/o l&#39;amministratore AEM, consentendo loro di eseguire manualmente le richieste relative alle normative sulla privacy.

 Adobe fornisce procedure per la gestione delle richieste di privacy relative a Access, Delete e Opt-Out per Adobe Experience Manager come Cloud Service. In alcuni casi, sono disponibili delle API che possono essere richiamate da un portale sviluppato dal cliente o da script per facilitare l&#39;automazione.

Nel diagramma seguente è illustrato l’aspetto di un flusso di lavoro per la richiesta di privacy (illustrato con Adobe Experience Manager 6.5):

![Protezione dei dati e privacy](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager come Cloud Service e preparazione normativa {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulta le sezioni seguenti per la documentazione regolamentare per le aree di prodotto di AEM come Cloud Service.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#aem-foundation}

Vedere [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

Vedere [ AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager come integrazione Cloud Service con  Adobe Target e  Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Queste integrazioni Adobe Experience Manager come Cloud Service si integrano con la protezione dei dati e con i servizi GDPR (es. Nessun dato personale  Adobe Target o  Adobe Analytics viene memorizzato in AEM in relazione alle integrazioni.
Per ulteriori informazioni, consulta:

* [ Adobe Target - Panoramica sulla privacy](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [ Adobe Analytics Data Privacy Workflow](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
