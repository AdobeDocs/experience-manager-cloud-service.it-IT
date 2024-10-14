---
title: Rapporti SLA
description: Scopri come visualizzare le prestazioni dell’ambiente AEM di produzione rispetto al contratto del livello di servizio.
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 13%

---


# Rapporti SLA {#sla-reporting}

Scopri come visualizzare le prestazioni dell’ambiente AEM di produzione rispetto al contratto SLA (Service Level Agreement).

## Visualizzare un rapporto di SLA {#introduction}

I dati dei rapporti di SLA tengono traccia delle metriche delle prestazioni per due livelli di produzione: livello di authoring e livello di Publish.

Il grafico a linee di un anno selezionato include punti dati per ogni mese da gennaio a dicembre. Vengono tracciate le metriche seguenti.

| Metrica tracciata | Colore linea | Descrizione |
| --- | --- | --- |
| Autore livello effettivo | Verde chiaro | Tempo di attività misurato per gli incidenti di factoring del livello di authoring in produzione causati da fornitori Adobe o Adobe. |
| Autore livello contratto | Blu scuro | Il SLA definito nel contratto con Adobe per il livello di authoring. |
| Pubblica livello effettivo | Arancione | Tempo di attività misurato del livello Publish di produzione, tenendo conto degli incidenti causati da fornitori di Adobi o Adobi. |
| Pubblica livello contratto | Rosso | Il SLA definito nel contratto con Adobe per il livello Publish. |

**Per visualizzare un report di SLA:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nella pagina **Panoramica programma**, nel menu a sinistra, fare clic su **Report**.

1. Fai clic su **Rapporti SLA**.

   ![Grafico a linee del report di SLA](/help/implementing/cloud-manager/assets/cm-sla-report.png)

1. Fai clic sull’anno desiderato per visualizzare un grafico a linee dei dati di SLA.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Sposta il cursore su un punto dati nel grafico a linee per visualizzare i valori specifici per quel punto.
   * Al di sotto dell’anno del grafico a linee, fai clic sull’icona Scarica per salvare un file di immagine PNG del grafico a linee.
   * Fai clic sul nome di una metrica per visualizzarne solo i dati. In alternativa, premere `Shift` sulla tastiera durante la selezione o deselezione di uno o più nomi di metriche.

   ![Visualizzazione dei dati dettagliati](/help/implementing/cloud-manager/assets/cm-sla-download.png)

## Analisi degli eventi {#event-analysis}

La sezione **Analisi degli eventi** sotto il grafico mostra il set di incidenti che si sono verificati per il programma durante l&#39;anno selezionato.

Ogni problema presenta un intervallo di tempo, una causa e una serie di commenti.

![Esempio di analisi degli eventi](assets/sla-reporting-c.png)

## Intervallo di aggiornamento dei rapporti di SLA {#refresh}

Il reporting di SLA fornisce informazioni approfondite sulle prestazioni dell’ambiente di produzione dell’AEM ed è aggiornato, ma non istantaneo. La generazione di rapporti di SLA viene eseguita mensilmente e viene generata per i nuovi programmi contrassegnati come `Production previous month`. Non è istantaneo. A causa di questo ritardo, tieni presente quanto segue durante la revisione del rapporto SLA:

* Il SLA segnalato è quello esistente all’inizio del mese, anche se SLA è cambiato durante quel mese.
* Se all&#39;inizio del mese non era presente alcun SLA perché il programma non esisteva, verrà applicato il SLA esistente alla data di creazione del programma.

## Ambienti di anteprima {#preview}

L’ambiente di anteprima è uno strumento che consente agli autori dei contenuti di verificare l’esperienza finale del contenuto prima della pubblicazione. A causa di questa funzionalità, gli ambienti di anteprima non sono progettati per l’elevata disponibilità e non dispongono di un SLA associato.
