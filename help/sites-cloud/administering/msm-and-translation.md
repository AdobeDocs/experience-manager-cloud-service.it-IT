---
title: Gestione multisito e traduzione
description: Scopri come riutilizzare i contenuti all’interno del progetto e come gestire siti web multilingue in AEM.
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 45%

---

# Gestione multisito e traduzione {#msm-and-translation}

Gli strumenti di traduzione e gestione multisito integrati di Adobe Experience Manager semplificano la localizzazione dei contenuti.

* Multi Site Manager (MSM) e le sue funzioni Live Copy consentono di utilizzare lo stesso contenuto del sito in più posizioni, permettendo al contempo l’utilizzo di varianti:
   * [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](msm/overview.md)
* La traduzione consente di automatizzare la traduzione del contenuto della pagina per creare e gestire siti Web multilingue:
   * [Traduzione di contenuti per siti multilingue](translation/overview.md)

Queste due funzioni possono essere combinate per gestire i siti Web che sono [multinazionali e multilingue](#multinational-and-multilingual-sites).

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta [Percorso di traduzione siti](/help/journey-sites/translation/overview.md). Si tratta di un percorso guidato attraverso la traduzione dei contenuti AEM Sites utilizzando potenti strumenti di traduzione AEM; ideale se non hai esperienza di AEM o traduzione.

## Siti multinazionali e multilingue {#multinational-and-multilingual-sites}

Puoi creare contenuti per siti multinazionali e multilingue in modo efficiente tramite l’utilizzo combinato di Multi Site Manager e del flusso di lavoro di traduzione.

In genere, si crea un sito principale in una lingua e per un paese specifico, quindi si utilizza tale contenuto come base per gli altri siti, utilizzando la traduzione ove necessario.

1. [Traduci](translation/overview.md) il sito principale in diverse lingue.
1. Utilizza [Multi Site Manager](msm/overview.md) per:
   1. Riutilizzare i contenuti del sito principale e delle relative traduzioni per creare siti per altri paesi e culture.
   1. Se necessario, scollegare gli elementi delle Live Copy per aggiungere i dettagli di localizzazione.

>[!TIP]
>
>Limitare l’utilizzo di Multi Site Manager ai contenuti in una sola lingua.
>
>Ad esempio, utilizza l’inglese principale per creare la versione inglese delle pagine per le pagine USA, Canada e Regno Unito. Quindi, utilizza il francese principale per creare la versione francese delle pagine per Francia, Svizzera, Canada e così via.

Il diagramma seguente illustra l’intersezione dei concetti principali (ma non tutti i livelli/elementi coinvolti):

![Panoramica sulla localizzazione](assets/localization-overview.png)

In questo scenario, e in quelli simili, MSM non gestisce le diverse versioni linguistiche in quanto tali.

* [MSM](msm/overview.md) gestisce la distribuzione dei contenuti tradotti da una blueprint (ovvero, una pagina globale principale) alle Live Copy (ovvero, i siti locali), entro i limiti della lingua.
* Il [traduzione](translation/overview.md) capacità di integrazione dell’AEM, con servizi di gestione della traduzione di terze parti, gestisce le lingue e traduce i contenuti in diverse lingue.

Per casi d’uso più avanzati, MSM può essere utilizzato anche tra le lingue primarie.

>[!TIP]
>
>Per tutti i casi d’uso si consiglia di leggere le seguenti best practice:
>
>* [Best practice per MSM](msm/best-practices.md)
>* [Best practice per la traduzione](translation/best-practices.md)
