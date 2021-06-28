---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
description: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: 87fa7079388e7a125ed62577123959524390486c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti) {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)"
>abstract="Esamina considerazioni importanti per utilizzare lo strumento Content Transfer (Trasferimento contenuti) tra cui versioni Java e AEM, tipi di datastore supportati, considerazioni sui gruppi di utenti e altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Valutazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti) "
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="Best practice e linee guida"

Nella tabella seguente sono riepilogati i prerequisiti per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).

Rivedi tutte le considerazioni elencate di seguito:

| Considerazioni | Cosa è attualmente supportato |
|--- |--- |
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo nelle versioni AEM 6.3 o successive. Per poter utilizzare lo strumento Content Transfer (Trasferimento contenuti) con AEM 6.2 o versioni precedenti, è necessario un aggiornamento locale dell’archivio dei contenuti a AEM 6.5. Non è necessario aggiornare il codice a AEM 6.5 per questo. |
| Dimensione dell’archivio segmenti | Sono attualmente supportati fino a 83 GB su *Author* e 31 GB su *Publish*. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per la dimensione dell’archivio segmenti al di sopra di questi limiti. |
| Dimensione totale dell&#39;archivio dei contenuti <br>*(archivio segmenti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 10 TB per il tipo di archivio dati file. Attualmente non è supportato alcun valore superiore a 10 TB. Crea un ticket di assistenza con l’Assistenza clienti Adobe per discutere le opzioni per contenuti di dimensioni superiori a 10 TB. <br>Per i tipi di archivio dati di Amazon S3 e Azure, è possibile utilizzare un passaggio di pre-copia opzionale per velocizzare in modo significativo il processo di trasferimento dei contenuti e supporta dimensioni superiori a 10 TB di dati archiviati. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non può essere utilizzato per migrare il contenuto in percorsi immutabili. Per trasferire il contenuto da `/etc` è possibile selezionare solo alcuni percorsi `"/etc"`, ma solo supportare [AEM Forms in AEM Forms come Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Per tutti gli altri casi d&#39;uso, fai riferimento a [Ristrutturazione del repository comune](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) per ulteriori informazioni sulla ristrutturazione dell&#39;archivio. |

## Novità {#whats-next}

Dopo aver esaminato i prerequisiti e aver determinato se è possibile utilizzare lo strumento Content Transfer (Trasferimento contenuti) nel progetto di migrazione, consulta [Best practice e considerazioni aggiuntive](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) durante l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).
