---
title: Prerequisiti per lo strumento di trasferimento contenuti
description: Acquisisci familiarità con i prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
feature: Migration
role: Admin
source-git-commit: 3e3d018dfd4babce9abef858e487bf1c116ed3a6
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 13%

---


# Prerequisiti per lo strumento di trasferimento contenuti {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerazioni importanti sull’utilizzo dello strumento di trasferimento contenuti"
>abstract="Esamina le considerazioni importanti per l’utilizzo dello strumento di trasferimento contenuti, tra cui le versioni di Java™ e AEM, i tipi di archivio dati supportati, considerazioni sui gruppi di utenti e altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=it" text="Considerazioni importanti sull’utilizzo dello strumento di trasferimento contenuti"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it#best-practices" text="Best practice e linee guida"

Nella tabella seguente sono riepilogati i prerequisiti per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).

Rivedi tutte le considerazioni elencate di seguito:

| Considerazioni | Cosa è attualmente supportato |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo su AEM 6.3 o versioni successive. |
| Dimensione dell’archivio segmenti | Un archivio esistente con meno di 750 milioni di nodi JCR e fino a 500 GB (dimensione compressa online) in *Author* e 50 GB in *Publish* è attualmente supportato. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per le dimensioni dell’archivio segmenti al di sopra di questi limiti. |
| Dimensione totale dell&#39;archivio dei contenuti <br>*(archivio segmenti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 20 terabyte per il tipo di archivio dati Archivio dati file. Al momento non sono supportati dati superiori a 20 terabyte. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per contenuti superiori a 20 terabyte. <br>Per accelerare significativamente il processo di trasferimento dei contenuti per archivi di grandi dimensioni, è possibile utilizzare un passaggio facoltativo di [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=it#setting-up-pre-copy-step). Questo processo si applica ai tipi di archivio dati File Data Store, Amazon S3 e Azure Data Store. Per Amazon S3 e Azure Data Store, sono supportate dimensioni dell’archivio superiori a 20 terabyte. |
| Dimensione totale indice Lucene | È supportata una dimensione totale dell&#39;indice Lucene massima di 25 GB, esclusi `/oak:index/lucene` e `/oak:index/damAssetLucene`. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per la dimensione dell’indice oltre questo limite. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non può essere utilizzato per migrare il contenuto in percorsi immutabili. Per trasferire il contenuto da `/etc`, è possibile selezionare alcuni percorsi `/etc`, ma solo per supportare [AEM Forms in AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). Per tutti gli altri casi d&#39;uso, vedere [Ristrutturazione del repository](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) per ulteriori informazioni sulla ristrutturazione del repository. |
| Valore della proprietà del nodo in MongoDB | I valori delle proprietà del nodo memorizzati in MongoDB non possono superare i 16 MB. Questa regola viene applicata da MongoDB. Le acquisizioni non riescono se sono presenti valori di proprietà maggiori di questo limite. Prima di eseguire un&#39;estrazione, eseguire lo script [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar). Esamina tutti i valori delle proprietà di grandi dimensioni e, se necessario, esegui la convalida. I valori superiori a 16 MB devono essere convertiti in valori binari. |

## Passaggio successivo {#whats-next}

Dopo aver esaminato i prerequisiti e stabilito se è possibile utilizzare lo strumento Content Transfer nel progetto di migrazione, consulta [Linee guida e best practice per l&#39;utilizzo dello strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it).