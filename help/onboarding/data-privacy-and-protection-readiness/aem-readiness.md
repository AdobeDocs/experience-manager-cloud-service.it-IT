---
title: Normative sulla protezione dei dati e la privacy dei dati - Adobe Experience Manager come preparazione al Cloud Service
description: Scopri Adobe Experience Manager come supporto Cloud Service per le varie normative su privacy e protezione dei dati; incluso il Regolamento generale sulla protezione dei dati (RGPD) dell’UE, il California Consumer Privacy Act e le modalità per conformarsi all’implementazione di un nuovo AEM come progetto di Cloud Service.
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# Adobe Experience Manager come Cloud Service di preparazione alle normative su privacy e protezione dei dati {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende sostituirsi a una consulenza legale.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative su privacy e protezione dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta del Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta [Centro per la privacy di Adobe](https://www.adobe.com/privacy.html).

Adobe fornisce documentazione e procedure (con API se disponibili) per l’amministratore della privacy del cliente o AEM amministratore per gestire le richieste di protezione dei dati e privacy dei dati e aiutare i nostri clienti a rispettare queste normative. Le procedure documentate consentiranno ai clienti di eseguire le richieste normative manualmente o chiamando nelle API, se disponibili, da un portale o servizio esterno.

>[!CAUTION]
>
>I dettagli qui documentati sono limitati ad Adobe Experience Manager come Cloud Service.
>
>I dati provenienti da un altro servizio Adobe on-demand, insieme a eventuali richieste di accesso a dati personali correlate, richiederanno azioni su tale servizio.
>
>Per ulteriori informazioni, consulta [Centro per la privacy di Adobe](https://www.adobe.com/privacy.html).

## Introduzione {#introduction}

Le istanze di Adobe Experience Manager as a Cloud Service e le applicazioni che le eseguono sono di proprietà e gestite dai nostri clienti.

Di conseguenza, le normative sulla protezione dei dati, come RGPD, CCPA e altri, sono in gran parte responsabilità dei clienti.

Come breve introduzione, le norme sulla privacy e la protezione dei dati includono nuove regole che devono essere seguite dai ruoli di:

* Entità commerciali (CCPA) e/o titolari del trattamento dei dati (RGPD)

* Fornitori di servizi (CCPA) e/o responsabili del trattamento dei dati (RGPD)

Le principali disposizioni di tali regolamenti sono le seguenti:

1. Definizione ampliata dei dati personali per includere tutti gli ID univoci; come in dati direttamente e indirettamente identificabili.

2. Requisiti più severi in materia di consenso.

3. Maggiore attenzione ai diritti di eliminazione (Cancellazione dati).

4. Rinuncia alla vendita di dati.

Per Adobe Experience Manager as a Cloud Service:

* Le istanze e le applicazioni che le eseguono sono di proprietà e gestite dal cliente.

   * Ciò significa in modo efficace che il cliente gestisce i ruoli normativi, tra cui Business Entities e Service Provider, Data Controller e Data Processor, tra gli altri.

   * Adobe Experience Platform Privacy Service non farà parte del flusso di lavoro per AEM, come illustrato nel diagramma seguente.

* AEM include la documentazione e le procedure per l&#39;amministratore della privacy del cliente e/o l&#39;amministratore AEM per eseguire le richieste relative alla normativa sulla privacy; manualmente o tramite API, se disponibili.

* Nessun nuovo servizio o interfaccia utente aggiunto.

   * Le procedure e le API sono invece documentate per l’utilizzo da parte dell’interfaccia utente/dei portali dei clienti che gestiscono le richieste di normativa sulla privacy.

* AEM non includerà alcun strumento predefinito per supportare il flusso di lavoro delle richieste di privacy.

   * L’Adobe fornisce documentazione e procedure per l’amministratore della privacy del cliente e/o per l’amministratore AEM, consentendo loro di eseguire manualmente le richieste relative alle normative sulla privacy.

Adobe fornisce procedure per la gestione delle richieste di accesso, cancellazione e rinuncia alla privacy relative ad Adobe Experience Manager as a Cloud Service. In alcuni casi, sono disponibili API che possono essere richiamate da un portale sviluppato dal cliente o da script per facilitare l&#39;automazione.

Il diagramma seguente illustra l’aspetto di un flusso di lavoro per la richiesta di accesso a dati personali (illustrato con Adobe Experience Manager 6.5):

![Protezione dei dati e privacy](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service e preparazione alle normative {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulta le sezioni seguenti per la documentazione regolamentare per le aree di prodotto di AEM come Cloud Service.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#aem-foundation}

Consulta [AEM Preparazione di base per le normative su privacy e protezione dei dati](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager Sites as a Cloud Service {#aem-sites}

Consulta [Preparazione di AEM Sites per le normative su privacy e protezione dei dati.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Integrazione di Adobe Experience Manager as a Cloud Service con Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Queste integrazioni di Adobe Experience Manager as a Cloud Service si basano sulla protezione dei dati e sulla privacy (ad esempio, il RGPD) dei servizi pronti. Nessun dato personale da Adobe Target o Adobe Analytics viene memorizzato in AEM in relazione alle integrazioni.
Per ulteriori informazioni, consulta:

* [Adobe Target - Panoramica sulla privacy](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flusso di lavoro sulla privacy dei dati di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
