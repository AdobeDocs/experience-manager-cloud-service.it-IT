---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
description: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
source-git-commit: 0d664997a66d790d5662e10ac0afd0dca7cc7fac
workflow-type: tm+mt
source-wordcount: '322'
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
| Dimensione dell’archivio segmenti | Lo strumento Content Transfer supporta attualmente fino a 83 GB su *Author* e fino a 31 GB su *Publish*. |
| Dimensione totale dell&#39;archivio dei contenuti <br>*(archivio segmenti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 10 TB. Attualmente non è supportato alcun valore superiore a 10 TB. Crea un ticket di assistenza con l’Assistenza clienti Adobe per discutere le opzioni per contenuti di dimensioni superiori a 10 TB. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non può essere utilizzato per migrare il contenuto in percorsi immutabili come `“/etc”`. Sono consentiti alcuni percorsi `"/etc"` da selezionare ma solo per supportare [AEM Forms in AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Per tutti gli altri casi d&#39;uso, fai riferimento a [Ristrutturazione del repository comune](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) per ulteriori informazioni sulla ristrutturazione dell&#39;archivio. |

## Novità {#whats-next}

Dopo aver esaminato i prerequisiti e aver determinato se è possibile utilizzare lo strumento Content Transfer (Trasferimento contenuti) nel progetto di migrazione, consulta [Best practice e considerazioni aggiuntive](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) durante l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).
