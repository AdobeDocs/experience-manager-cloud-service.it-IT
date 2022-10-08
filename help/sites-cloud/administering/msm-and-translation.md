---
title: Gestione multisito e traduzione
description: Scopri come riutilizzare i contenuti all’interno del progetto e come gestire siti web multilingue in AEM.
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 95%

---

# Gestione multisito e traduzione {#msm-and-translation}

Gli strumenti di traduzione e gestione multisito integrati di Adobe Experience Manager semplificano la localizzazione dei contenuti.

* Multi Site Manager (MSM) e le sue funzioni Live Copy consentono di utilizzare lo stesso contenuto del sito in più posizioni, permettendo al contempo l’utilizzo di varianti:
   * [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](msm/overview.md)
* La traduzione consente di automatizzare la localizzazione dei contenuti della pagina per creare e gestire siti Web multilingue:
   * [Traduzione di contenuti per siti multilingue](translation/overview.md)

Queste due funzioni possono essere combinate per gestire i siti Web che sono [multinazionali e multilingue](#multinational-and-multilingual-sites).

>[!TIP]
>
>Se sei alle prime armi con la traduzione di contenuti, consulta il nostro [Percorso di traduzione siti,](/help/journey-sites/translation/overview.md) che è un processo guidato attraverso la traduzione dei contenuti dei tuoi siti AEM utilizzando i potenti strumenti di traduzione di AEM, ideale per chi non ha esperienza di AEM o di traduzione.

## Siti multinazionali e multilingue {#multinational-and-multilingual-sites}

Puoi creare contenuti per siti multinazionali e multilingue in modo efficiente tramite l’utilizzo combinato di Multi Site Manager e del flusso di lavoro di traduzione.

In genere, si crea un sito master in una lingua e per un paese specifico, quindi si utilizza tale contenuto come base per gli altri siti, utilizzando la traduzione, se necessario.

1. [Tradurre](translation/overview.md) il sito master in lingue diverse.
1. Utilizza [Multi Site Manager](msm/overview.md) per:
   1. Riutilizzare i contenuti del sito master e delle sue traduzioni per creare siti per diversi paesi e culture.
   1. Se necessario, scollegare gli elementi delle Live Copy per aggiungere i dettagli di localizzazione.

>[!TIP]
>
>Limitare l’utilizzo di Multi Site Manager ai contenuti in una sola lingua.
>
>Ad esempio, utilizza il master inglese per creare la versione inglese delle pagine per gli Stati Uniti, il Canada, il Regno Unito, ecc. e utilizza il master francese per creare la versione francese delle pagine per Francia, Svizzera, Canada, ecc.

Il diagramma seguente illustra l’intersezione dei concetti principali (ma non tutti i livelli/elementi coinvolti):

![Panoramica sulla localizzazione](assets/localization-overview.png)

In questo scenario (e simili) MSM non gestisce le diverse versioni linguistiche in quanto tali.

* [MSM](msm/overview.md) gestisce la distribuzione dei contenuti tradotti da un blueprint (cioè un master globale) alle Live Copy (ossia i siti locali), entro i limiti della lingua.
* Le capacità di integrazione delle [traduzioni](translation/overview.md) di AEM, in collaborazione con servizi di gestione della localizzazione di terze parti, gestiscono le lingue e traducono i contenuti in diverse lingue.

Per casi di utilizzo più avanzati, MSM può essere utilizzato anche tra le lingue master.

>[!TIP]
>
>Per tutti i casi d’uso si consiglia di leggere le seguenti best practice:
>
>* [Best practice per MSM](msm/best-practices.md)
>* [Best practice per la traduzione](translation/best-practices.md)

