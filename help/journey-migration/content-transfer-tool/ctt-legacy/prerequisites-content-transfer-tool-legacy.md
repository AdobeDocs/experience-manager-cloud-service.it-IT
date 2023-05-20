---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti) (legacy)
description: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
hide: true
hidefromtoc: true
exl-id: 6b2878cb-6882-452b-8cab-e590316633f6
source-git-commit: eb633db8fe64a62661c094b88f0ce8d9950ed6d7
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti) (legacy) {#prerequisites}

Nella tabella seguente sono riepilogati i prerequisiti per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).

Leggere tutte le considerazioni riportate di seguito:

| Considerazioni | Cosa è attualmente supportato |
|--- |--- |
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo su AEM 6.3 o versioni successive. |
| Dimensione dell’archivio segmenti | Un archivio esistente con meno di 55 milioni di nodi JCR e fino a 83 GB (dimensione compressa online) su *Autore* e 31 GB su *Pubblica* sono attualmente supportati. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per le dimensioni dell’archivio segmenti al di sopra di questi limiti. |
| Dimensione totale dell’archivio dei contenuti <br>*(archivio segmenti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 20 TB per il tipo di archivio dati Archivio dati file. Al momento non sono supportati dati superiori a 20 TB. Crea un ticket di supporto con l’Assistenza clienti Adobe per discutere le opzioni per contenuti superiori a 20 TB. <br>Per accelerare notevolmente il processo di trasferimento dei contenuti per archivi di grandi dimensioni, è disponibile un [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) può essere utilizzato. Questo vale per i tipi di archivio dati File Data Store, Amazon S3 e Azure Data Store. Per Amazon S3 e Azure Data Store, sono supportate dimensioni dell’archivio superiori a 20 TB. |
| Dimensione totale indice Lucene | Attualmente è supportata una dimensione totale dell’indice Lucene massima di 25 GB. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per le dimensioni dell’indice superiori a questo limite. |
| Lunghezza nome nodo | La lunghezza del nome di un nodo deve essere inferiore o pari a 150 byte. I nomi dei nodi più lunghi di 150 byte devono essere ridotti a &lt;= 150 byte per poter essere supportati dall’archivio nodi Document in AEM as a Cloud Service. Le acquisizioni non riusciranno se questi nomi di nodo lunghi non sono corretti. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non può essere utilizzato per migrare il contenuto in percorsi immutabili. Per trasferire contenuti da `/etc` solo determinati `/etc` I percorsi possono essere selezionati ma solo per supportare [Da AEM Forms ad AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Per tutti gli altri casi d’uso, consulta [Ristrutturazione dell’archivio comune](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) per ulteriori informazioni sulla ristrutturazione dell’archivio. |
| Valore della proprietà del nodo in MongoDB | I valori delle proprietà del nodo memorizzati in MongoDB non possono superare i 16 MB. Questo è imposto da MongoDB. Le acquisizioni non riusciranno se i valori delle proprietà superano questo limite. Prima di eseguire un’estrazione, esegui questa [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Esamina tutti i valori delle proprietà di grandi dimensioni e, se necessario, esegui la convalida. Quelli che superano i 16 MB dovranno essere convertiti in valori binari. |

## Passaggio successivo {#whats-next}

Dopo aver esaminato i prerequisiti e stabilito se è possibile utilizzare lo strumento Content Transfer nel progetto di migrazione, consulta [Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
