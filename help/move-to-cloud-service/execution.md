---
title: Fase di esecuzione
description: Fase di esecuzione
exl-id: 176dd79d-0d72-443c-87db-dab24fb48b96
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 87%

---

# Esecuzione {#execution-phase}

Prima di avviare la fase di esecuzione, devi aver effettuato l’onboarding in Cloud Service. È inoltre necessario acquisire familiarità con Cloud Manager, in quanto è l’unico meccanismo per l’implementazione del codice in AEM Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente AEM nel cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

Per ulteriori informazioni, consulta le seguenti risorse:

* [Onboarding per Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) per comprendere le risorse disponibili sull’onboarding per Experience Manager as a Cloud Service.

* [Integrazione di Git con Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) per informazioni sull’utilizzo di un archivio Git singolo per implementare il codice.

* [Configurazione di Adobe Experience as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#aem-configuration) per informazioni sulla gestione dei prodotti e dell’accesso degli utenti in Admin Console.


## Introduzione {#introduction}

I passaggi esatti della transizione verso Cloud Service dipendono dai sistemi acquistati e dalle procedure di sviluppo software seguite.

La figura seguente mostra i passaggi principali della fase di esecuzione:

![immagine](/help/move-to-cloud-service/assets/exec-image1.png)

## Trasferimento dei contenuti {#content-transfer}

Per trasferire contenuti dall’istanza AEM corrente all’istanza Cloud Service, puoi utilizzare lo strumento Content Transfer (Trasferimento contenuti) di Adobe.

Con questo strumento, puoi specificare il sottoinsieme di contenuti che desideri trasferire dall’istanza AEM sorgente all’istanza AEM Cloud Service.

>[!NOTE]
>Si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Per ulteriori informazioni, consulta [Strumento Content Transfer (Trasferimento contenuti](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md).

>[!IMPORTANT]
>l requisiti di sistema minimi per lo strumento Content Transfer (Trasferimento contenuti) sono AEM 6.3 o versione successiva e JAVA 8. Se utilizzi una precedente versione di AEM, dovrai aggiornare l’archivio dei contenuti ad AEM 6.5 per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

## Refactoring del codice {#code-refactor}

Lo sviluppo e l’esecuzione del codice in AEM as a Cloud Service richiedono un approccio diverso. Il codice deve essere resiliente, soprattutto poiché un’istanza potrebbe essere arrestata in qualsiasi momento. Il codice in esecuzione in Cloud Service deve tener conto di essere sempre in esecuzione in un cluster. Ciò significa che ci sono sempre in esecuzione più di un’istanza.

Alcune modifiche devono essere apportate ai progetti AEM Maven per renderli compatibili con AEM as a Cloud Service. AEM as a Cloud Service richiede una separazione di *contenuto* e *codice* in pacchetti distinti per l’implementazione in AEM.

* `/apps` e `/libs` sono considerate aree immutabili di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime). Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

* Tutte le altre aree all’interno dell’archivio (`/content`, `/conf`, `/var`, `/home`, `/etc`, `/oak:index`, `/system`, `/tmp` ecc.) sono mutabili, ovvero possono essere modificate in fase di runtime.

Per ulteriori dettagli, consulta [Struttura consigliata dei pacchetti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure).

Durante lo sviluppo su AEM as a Cloud Service, considera anche alcune linee guida di sviluppo aggiuntive. Per ulteriori informazioni, consulta [Linee guida per lo sviluppo per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html).

Nella fase di pianificazione, avrai stilato un elenco di aree che richiedono il refactoring affinché siano compatibili con Cloud Service. È inoltre necessario esaminare le [Linee guida per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html) per ulteriori dettagli su come effettuare il refactoring del codice e ottimizzarlo per il passaggio a Cloud Service.

Per accelerare alcune delle attività di refactoring del codice, puoi utilizzare i seguenti strumenti:

* [Asset Workflow Migration (Migrazione flussi di lavoro per risorse) ](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Strumenti di modernizzazione](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

Si consiglia di effettuare il refactoring del codice e testarlo localmente prima di inviarlo a un ambiente Cloud Service tramite Cloud Manager Git.

Leggi la documentazione [AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) per ulteriori informazioni.

Di seguito sono elencate alcune risorse aggiuntive:

* Guarda Install Dispatcher SDK per informazioni su come installare Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Guarda Configure Dispatcher SDK per informazioni su come configurare Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* Consulta la documentazione [Local Development Setup](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) per configurare un ambiente di sviluppo locale


Per gestire lo sviluppo del codice in corso sul tuo AEM attivo insieme all’attività di refactoring del codice come parte del percorso di transizione, è consigliabile pianificare un periodo di blocco del codice fino a quando non avrai completato la ristrutturazione del progetto Maven per renderlo compatibile con AEM as a Cloud Service.

Una volta completata la ristrutturazione del progetto, puoi riprendere lo sviluppo del nuovo codice in base a questa nuova struttura. Questo ridurrà gli errori della pipeline di Cloud Manager durante l’implementazione e il test del codice.

>[!NOTE]
>Le attività di trasferimento dei contenuti e refactoring del codice non devono necessariamente essere eseguite in sequenza. Queste attività possono essere svolte l’una indipendentemente dall’altra. Tuttavia, è necessaria la giusta struttura di progetto per garantire il corretto rendering del contenuto nell’ambiente Cloud Service.

## Best practice per l’implementazione e il test del codice {#best-practices}

Le esecuzioni della pipeline di Cloud Manager per Cloud Services supportano l’esecuzione di test sull’ambiente stage.

Per informazioni sulla scrittura di script di test e sulla copertura consigliata di almeno il 50%, consulta l’articolo sul [testing della qualità del codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing).

Inoltre, consulta [Regole per la qualità del codice personalizzato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) per ulteriori informazioni sulle regole per la qualità del codice personalizzato eseguite da Cloud Manager e create in base alle best practice di AEM Engineering.

L’utilizzo di Cloud Manager è l’unico meccanismo per implementare il codice negli ambienti di Cloud Service.

Consulta le risorse elencate di seguito per scoprire come utilizzare Cloud Manager per gestire e implementare il codice.

* [Gestione degli ambienti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Configurazione della pipeline CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Implementazione del codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Best practice per la preparazione alla pubblicazione {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparazione Go-Live"
>abstract="Per garantire un&#39;esperienza di AEM fluida e di successo come Cloud Service, è necessario pianificare periodi di blocco del codice e dei contenuti, iterazioni di test, integrazioni di contenuto, test delle prestazioni, test di sicurezza e altro ancora."

Per garantire una pubblicazione corretta e priva di problemi in AEM as a Cloud Service, valuta l’esecuzione dei seguenti passaggi:

* Pianificare un periodo di blocco del codice e dei contenuti
* Eseguire l’integrazione del contenuto finale
* Completare le iterazioni di test
* Eseguire test di prestazioni e sicurezza
* Cutover
