---
title: Riutilizzare i frammenti di contenuto con MSM e Live Copy
description: Scopri come utilizzare la funzionalità Live Copy di MSM per utilizzare lo stesso contenuto di frammenti di contenuto, o simile, in più posizioni, durante la sincronizzazione con il contenuto sorgente.
exl-id: f050b2d1-856c-4cdb-ac74-bc78016f144a
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# Riutilizzare frammenti di contenuto con MSM {#reuse-content-fragments-using-msm}

Multi Site Manager (MSM) e la funzionalità Live Copy consentono di utilizzare lo stesso contenuto in più posizioni, sincronizzandolo con il contenuto sorgente.

* Con MSM Live Copy puoi:
   * Creare contenuto una volta e poi
   * Riutilizzare questo contenuto in altre aree dello stesso sito o di altri siti o applicazioni.
* MSM mantiene quindi le relazioni in tempo reale tra il contenuto sorgente e le relative Live Copy in modo che:
   * Quando modifichi il contenuto sorgente, la sorgente e le Live Copy vengono sincronizzate.
   * Puoi apportare modifiche solo al contenuto delle Live Copy scollegando la relazione in tempo reale per le singole sottopagine e/o componenti.

Per una panoramica dettagliata dei concetti di MSM, vedi [Riutilizzo del contenuto: Multi Site Manager e Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>La funzionalità [Gestione multisito (MSM)](/help/sites-cloud/administering/msm/overview.md) in Adobe Experience Manager consente agli utenti di riutilizzare il contenuto creato una volta e quindi riutilizzato in più percorsi Web.

Utilizzando MSM per frammenti di contenuto puoi:

* Crea frammenti di contenuto una volta e quindi crea copie (collegate) di questi frammenti da riutilizzare in altre aree del sito o dell’applicazione.
* Mantieni più copie sincronizzate aggiornando la copia sorgente una sola volta, quindi inviando le modifiche alle copie (live).
* Apporta modifiche locali sospendendo temporaneamente o definitivamente il collegamento tra i frammenti padre e figlio, completamente o per le relative varianti o campi.

MSM per frammenti di contenuto, combinato con la funzionalità nell’Editor frammenti di contenuto, consente di interrompere e ripristinare l’ereditarietà a livello di campo.

>[!CAUTION]
>
>MSM per frammenti di contenuto è disponibile solo quando si utilizzano frammenti di contenuto tramite la console **Assets**.
>
>La funzionalità MSM è *non* disponibile quando si utilizza la console **Frammenti di contenuto**.

## Procedura {#how-to}

Consulta la seguente documentazione per informazioni dettagliate sull’utilizzo di MSM per Frammenti di contenuto (applicabile anche ad Assets):

* Come utilizzare [MSM per frammenti di contenuto (e Assets)](/help/assets/reuse-assets-using-msm.md)

* [Creare una Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >Se desideri utilizzare MSM per creare copie di frammenti di contenuto, tutti i vincoli **Unique** devono essere rimossi da qualsiasi tipo di dati utilizzato nei rispettivi [modelli di frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md).

* [Visualizzare le proprietà e lo stato dell’origine e della Live Copy](/help/assets/reuse-assets-using-msm.md#properties)
* [Propaga le modifiche dall’origine alla Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* Annulla e ripristina l&#39;ereditarietà per:
   * campi e varianti nell&#39;[Editor frammento di contenuto](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [metadati delle risorse correlate](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [Sospendere e riprendere la relazione](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [Rimuovi la relazione live](/help/assets/reuse-assets-using-msm.md#detach)
* [Confrontare MSM per Frammenti di contenuto (e Assets) con MSM per Sites](/help/assets/reuse-assets-using-msm.md#comparison)

## Limitazioni {#limitations}

* I trigger durante la modifica e la configurazione di rollout associata non esistono per i frammenti di contenuto.
