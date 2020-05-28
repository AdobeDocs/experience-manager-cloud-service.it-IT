---
title: Fase di esecuzione
description: Fase di esecuzione
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 7%

---


# Esecuzione {#execution-phase}

Prima di avviare la fase di esecuzione, è necessario essere collegati a Cloud Service. È inoltre necessario acquisire familiarità con Cloud Manager, in quanto è l&#39;unico meccanismo per distribuire il codice al servizio AEM Cloud.

Cloud Manager consente alle organizzazioni di gestire autonomamente AEM in Cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

Per ulteriori informazioni, consultate le seguenti risorse:

* [Accesso a Experience Manager come servizio](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/onboarding/home.html) cloud per comprendere le risorse di supporto autonomo sull&#39;onboarding per Experience Manager come servizio Cloud.

* [Integrazione di Git con Adobe Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) per informazioni sull’utilizzo di un repository Git singolo per distribuire il codice.

* [Adobe Experience as a Cloud Service Configuration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) (Configurazione di servizi cloud) per informazioni sulla gestione di prodotti e accesso utente in Admin Console.


## Introduzione {#introduction}

I passaggi esatti della transizione a Cloud Service dipendono dai sistemi acquistati e dalle procedure di sviluppo software seguite.

La figura seguente mostra le fasi principali della fase di esecuzione:

![image](/help/move-to-cloud-service/assets/exec-image1.png)

## Trasferimento dei contenuti {#content-transfer}

Per trasferire il contenuto dall’istanza AEM corrente all’istanza del servizio cloud, potete utilizzare lo strumento di trasferimento dei contenuti di Adobe.

Con questo strumento, potete specificare il sottoinsieme di contenuti desiderato da trasferire dall’istanza AEM di origine all’istanza del servizio AEM Cloud.

>[!NOTE]
>Si consiglia di eseguire frequenti aggiunte differenziali ai contenuti per ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali prima di iniziare a utilizzare il servizio Cloud.

Per ulteriori informazioni, consultate Strumento [di trasferimento](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) dei contenuti.

>[!IMPORTANT]
>Il requisito minimo per lo strumento di trasferimento dei contenuti è AEM 6.3 + e JAVA 8. Se si utilizza una versione di AEM inferiore, sarà necessario aggiornare l’archivio dei contenuti ad AEM 6.5 per utilizzare lo strumento di trasferimento dei contenuti.

## Refactoring del codice {#code-refactor}

Lo sviluppo e l’esecuzione del codice in AEM come servizio cloud richiedono una modifica del set di idee. Va notato che il codice deve essere resiliente, soprattutto perché un&#39;istanza potrebbe essere arrestata in qualsiasi momento. Il codice in esecuzione nel servizio cloud deve essere consapevole del fatto che è sempre in esecuzione in un cluster. Ciò significa che è sempre in esecuzione più di un&#39;istanza.

Alcune modifiche sono necessarie affinché i progetti AEM Maven siano compatibili con AEM come servizio cloud. AEM come servizio cloud richiede una separazione di *contenuto* e *codice* in pacchetti discreti per la distribuzione in AEM.

* `/apps` e `/libs` sono considerate aree immutabili di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime). Qualsiasi tentativo di modifica di un’area immutabile in fase di runtime avrà esito negativo.

* Tutto il resto nella directory archivio, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` , ecc. sono tutte aree mutabili, ovvero possono essere modificate in fase di esecuzione.

Per ulteriori dettagli, consultate [Struttura](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) pacchetto consigliata.

Durante lo sviluppo di AEM come servizio cloud, è necessario essere consapevoli di alcune linee guida di sviluppo aggiuntive. Per ulteriori informazioni, consulta [AEM come guida](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) allo sviluppo di servizi cloud.

Dalla fase di pianificazione, è necessario disporre di un elenco di aree da rendere compatibili con il servizio Cloud. È inoltre necessario consultare le Linee guida [per](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) lo sviluppo per ulteriori dettagli su come reimpostare e ottimizzare il codice per passare al servizio Cloud.

Per accelerare alcune delle attività di refactoring del codice, potete utilizzare i seguenti strumenti:

* [Migrazione al flusso di lavoro delle risorse](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Strumenti di modernizzazione](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

Si consiglia di rifattorizzare e testare il codice localmente prima di inviarlo a un ambiente di servizio Cloud tramite Cloud Manager Git.

Leggi la documentazione [AEM SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) per saperne di più.

Di seguito sono elencate alcune risorse aggiuntive:

* Per informazioni su come installare Dispatcher SDK, consulta Installare Dispatcher:

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* Per informazioni su come configurare Dispatcher SDK, consulta Configurare il dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* Consulta la documentazione di Impostazione [sviluppo](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) locale per configurare un ambiente di sviluppo locale


Per gestire lo sviluppo del codice in corso sul tuo AEM attivo insieme all’attività di refactoring del codice come parte del percorso di transizione, è consigliabile pianificare un periodo di blocco del codice fino a quando non avrai completato la ristrutturazione del progetto Maven per renderlo compatibile con AEM come servizio cloud.

Una volta completata la ristrutturazione del progetto, potete riprendere lo sviluppo del codice in base a questa nuova struttura. Questo ridurrà gli errori della pipeline di Cloud Manager durante la distribuzione e il test del codice.

>[!NOTE]
>Le attività di trasferimento dei contenuti e di refactoring dei codici non devono essere eseguite in sequenza. Questi compiti possono essere svolti indipendentemente l&#39;uno dall&#39;altro. Tuttavia, è necessaria la struttura di progetto corretta per garantire il corretto rendering del contenuto nell&#39;ambiente Cloud Service.

## Best practice per la distribuzione e il test del codice {#best-practices}

Le esecuzioni della pipeline di Cloud Manager for Cloud Services supporteranno l&#39;esecuzione di test eseguiti nell&#39;ambiente del passaggio.

Per informazioni sulla scrittura di script di test e sulla copertura consigliata di almeno il 50%, fare riferimento a Test [qualità](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) codice.

Inoltre, fate riferimento a [Informazioni sulle regole](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) di qualità del codice personalizzate per ulteriori informazioni sulle regole di qualità del codice eseguite da Cloud Manager create in base alle best practice di AEM Engineering.

L&#39;utilizzo di Cloud Manager è l&#39;unico meccanismo per distribuire il codice agli ambienti del servizio Cloud.

Segui le risorse riportate di seguito per apprendere come utilizzare Cloud Manager per gestire e distribuire il codice.

* [Gestione degli ambienti](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Configurazione della pipeline CI-CD](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Implementazione del codice](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Best practice per la preparazione Go-Live {#go-live}

Per garantire un accesso diretto e corretto ad AEM come servizio cloud, prendi in considerazione l&#39;esecuzione dei seguenti passaggi:

* Pianificazione del periodo di blocco del codice e del contenuto
* Eseguire l&#39;integrazione del contenuto finale
* Completare le iterazioni di test
* Esecuzione di test di prestazioni e sicurezza
* Taglia
