---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
description: Acquisisci familiarità con i prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: aa032af2ed7ff877b4c9f9cb6d427c84e71c3874
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 11%

---

# Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti) {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Considerazioni importanti sull’utilizzo dello strumento Content Transfer"
>abstract="Esamina le considerazioni importanti per l’utilizzo dello strumento di trasferimento dei contenuti, tra cui le versioni di Java™ e AEM, i tipi di archivio dati supportati, considerazioni sui gruppi di utenti e altro ancora."
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=it" text="Considerazioni importanti sull’utilizzo dello strumento di trasferimento dei contenuti"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it#best-practices" text="Best practice e linee guida"

Nella tabella seguente sono riepilogati i prerequisiti per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).

Rivedi tutte le considerazioni elencate di seguito:

| Considerazioni | Cosa è attualmente supportato |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo su AEM 6.3 o versioni successive. |
| Dimensione dell’archivio segmenti | Un archivio esistente con meno di 750 milioni di nodi JCR e fino a 500 GB (dimensione compressa online) su *Autore* e 50 GB su *Pubblica* sono attualmente supportati. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per le dimensioni dell’archivio segmenti al di sopra di questi limiti. |
| Dimensione totale dell’archivio dei contenuti <br>*(archivio segmenti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 20 terabyte per il tipo di archivio dati Archivio dati file. Al momento non sono supportati dati superiori a 20 terabyte. Crea un ticket di supporto con l’Assistenza clienti Adobe per discutere le opzioni per contenuti superiori a 20 terabyte. <br>Per accelerare notevolmente il processo di trasferimento dei contenuti per archivi di grandi dimensioni, è disponibile un [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=it#setting-up-pre-copy-step) può essere utilizzato. Questo processo si applica ai tipi di archivio dati File Data Store, Amazon S3 e Azure Data Store. Per Amazon S3 e Azure Data Store, sono supportate dimensioni dell’archivio superiori a 20 terabyte. |
| Dimensione totale indice Lucene | Indice Lucene totale massimo di 25 GB, escluso `/oak:index/lucene` e `/oak:index/damAssetLucene` è supportato. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per la dimensione dell’indice oltre questo limite. |
| Lunghezza nome nodo | La lunghezza del nome di un nodo deve essere inferiore o uguale a 150 byte quando il percorso padre del nodo è maggiore o uguale a 350 byte. Per poter essere supportati dall’archivio nodi Document in AEM as a Cloud Service, questi nomi di nodo devono essere ridotti a &lt;= 150 byte. Le acquisizioni non riescono se questi nomi di nodo lunghi non sono corretti. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non può essere utilizzato per migrare il contenuto in percorsi immutabili. Per trasferire contenuti da `/etc`, puoi selezionare alcuni `/etc` percorsi, ma solo per supportare [Da AEM Forms ad AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). Per tutti gli altri casi d’uso, vedi [Ristrutturazione dell’archivio comune](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) per ulteriori informazioni sulla ristrutturazione dell’archivio. |
| Valore della proprietà del nodo in MongoDB | I valori delle proprietà del nodo memorizzati in MongoDB non possono superare i 16 MB. Questa regola viene applicata da MongoDB. Le acquisizioni non riescono se sono presenti valori di proprietà maggiori di questo limite. Prima di eseguire un’estrazione, esegui questa [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Esamina tutti i valori delle proprietà di grandi dimensioni e, se necessario, esegui la convalida. I valori superiori a 16 MB devono essere convertiti in valori binari. |

## Passaggio successivo {#whats-next}

Dopo aver esaminato i prerequisiti e stabilito se è possibile utilizzare lo strumento Content Transfer nel progetto di migrazione, consulta [Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it).
