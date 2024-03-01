---
title: Riutilizzare i frammenti di contenuto utilizzando MSM e Live Copy
description: Scopri sull'utilizzo della funzionalità Live Copy di MSM per utilizzare lo stesso contenuto frammento di contenuto o simile in più posizioni, durante la sincronizzazione con il contenuto di origine.
source-git-commit: 3ce1a982055c2f9c900edbd88e079deb6d3a036a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# Riutilizzare i frammenti di contenuto utilizzando MSM {#reuse-content-fragments-using-msm}

Multi Site Manager (MSM) e la funzionalità Live Copy consentono di utilizzare lo stesso contenuto in più posizioni, durante la sincronizzazione con il contenuto di origine.

* Con MSM Live Copy puoi:
   * Creare contenuto una volta e poi
   * Riutilizzare questo contenuto in altre aree dello stesso o di altri siti o applicazioni.
* MSM mantiene quindi le relazioni in tempo reale tra il contenuto sorgente e le relative Live Copy in modo che:
   * Quando modifichi il contenuto di origine, l&#39;origine e le Live Copy vengono sincronizzate.
   * Puoi apportare modifiche solo al contenuto delle Live Copy scollegando la relazione in tempo reale per le singole sottopagine e/o componenti.

Per una panoramica dettagliata dei concetti MSM, vedere [Riutilizzo del contenuto: Multi Site Manager e Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[La funzionalità Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) in Adobe Experience Manager consente agli utenti di riutilizzare contenuto creata una volta e quindi riutilizzata in più posizioni Web.

Utilizzando MSM per i frammenti di contenuto è possibile:

* Crea frammenti di contenuto una volta e quindi creare copie (collegate) di questi frammenti per riutilizzarli in altre aree del sito o applicazione.
* Mantieni più copie sincronizzate aggiornando la copia sorgente una sola volta, quindi inviando le modifiche alle copie (live).
* Apporta modifiche locali sospendendo temporaneamente o definitivamente il collegamento tra i frammenti padre e figlio, completamente o per le relative varianti o campi.

MSM per frammenti di contenuto, combinato con la funzionalità dell&#39;editor dei frammenti di contenuto, consente di interrompere e ripristinare l&#39;ereditarietà a livello di campo.

>[!CAUTION]
>
>MSM per frammenti di contenuto è disponibile solo quando si utilizzano frammenti di contenuto tramite la **console Assets** .
>
>La funzionalità MSM non *è* disponibile quando si utilizza la **console Frammenti di** contenuto.

## Come si fa {#how-to}

Per i dettagli sull&#39;utilizzo di MSM per i frammenti di contenuto (applicabile anche a Assets, consulta la seguente documentazione):

* Come utilizzare [MSM per frammenti di contenuto (e Assets)](/help/assets/reuse-assets-using-msm.md)

* [Crea una Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >Se si desidera utilizzare MSM per creare copie di frammenti di contenuto), qualsiasi **vincolo univoco** deve essere rimosso da tutti i tipi di dati utilizzati nei rispettivi [modelli](/help/assets/content-fragments/content-fragments-models.md) di frammenti di contenuto.

* [Visualizza proprietà e stato dell&#39;origine e del Live Copy](/help/assets/reuse-assets-using-msm.md#properties)
* [Propaga le modifiche dall’origine alla Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* Annulla e ripristina l&#39;ereditarietà per:
   * campi e varianti nel frammento di [contenuto editor](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [metadati dei relativi risorse](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [Sospendi e riprendi la relazione](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [Rimuovi la relazione dal vivo](/help/assets/reuse-assets-using-msm.md#detach)
* [Confronta MSM per frammenti di contenuto (e Assets) con MSM per Sites](/help/assets/reuse-assets-using-msm.md#comparison)

## Limitazioni {#limitations}

* I trigger di modifica e la configurazione del rollout associato non esistono per i frammenti di contenuto.