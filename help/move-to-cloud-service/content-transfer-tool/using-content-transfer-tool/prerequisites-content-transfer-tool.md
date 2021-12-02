---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
description: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: 3b1ef6eef7249a33908102b287ee4b373d7e843b
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

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
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo nelle versioni AEM 6.3 o successive. |
| Dimensione dell’archivio segmenti | Un archivio esistente con meno di 55 milioni di nodi JCR e fino a 83 GB (dimensione compatta online) su *Autore* e 31 GB su *Pubblica* sono attualmente supportate. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per la dimensione dell’archivio segmenti al di sopra di questi limiti. |
| Dimensione totale dell’archivio dei contenuti <br>*(archivio segmenti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 20 TB per il tipo di archivio dati file. Attualmente non è supportato alcun valore superiore a 20 TB. Crea un ticket di assistenza con l’Assistenza clienti Adobe per discutere le opzioni per contenuti di dimensioni superiori a 20 TB. <br>Per accelerare notevolmente il processo di trasferimento dei contenuti per archivi di grandi dimensioni, è possibile [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) è possibile utilizzare il passaggio . Questo vale per i tipi di archivio dati file, Amazon S3 e Azure Data Store dell’archivio dati. Per Amazon S3 e Azure Data Store, è supportato un archivio con dimensioni superiori a 20 TB. |
| Dimensione totale indice Lucene | È attualmente supportata la dimensione totale dell&#39;indice Lucene massima di 25 GB. Crea un ticket di supporto con l’Assistenza clienti di Adobe per discutere le opzioni per la dimensione dell’indice al di sopra di questo limite. |
| Lunghezza nome nodo | La lunghezza del nome di un nodo deve essere uguale o inferiore a 150 byte. Per essere supportati dall&#39;archivio dei nodi del documento in AEM as a Cloud Service, i nomi dei nodi di lunghezza superiore a 150 byte devono essere abbreviati per essere &lt;= 150 byte. Gli input avranno esito negativo se questi nomi di nodo lunghi non sono fissi. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non può essere utilizzato per migrare il contenuto in percorsi immutabili. Per trasferire il contenuto da `/etc` solo certi `/etc` i percorsi possono essere selezionati ma solo per supportare [AEM Forms in AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Per tutti gli altri casi d’uso, consulta [Ristrutturazione dell’archivio comune](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) per ulteriori informazioni sulla ristrutturazione dell’archivio. |
| Valore della proprietà del nodo in MongoDB | I valori delle proprietà del nodo memorizzati in MongoDB non possono superare i 16 MB. Questo viene applicato da MongoDB. Gli input avranno esito negativo se i valori di proprietà sono maggiori di questo limite. Prima di eseguire un’estrazione, esegui questa [corsa di oak](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Esamina tutti i valori delle proprietà di grandi dimensioni e convalida se necessari. Quelli che superano i 16 MB dovranno essere convertiti in valori binari. |

## Novità {#whats-next}

Dopo aver esaminato i prerequisiti e aver determinato se è possibile utilizzare lo strumento Content Transfer (Trasferimento contenuti) nel progetto di migrazione, consulta [Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
