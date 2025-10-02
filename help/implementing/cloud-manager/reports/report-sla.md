---
title: Rapporti SLA
description: Scopri come visualizzare le prestazioni dell’ambiente AEM di produzione rispetto al Service level agreement contrattuale.
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---


# Rapporti di SLA {#sla-reporting}

Scopri come visualizzare le prestazioni dell’ambiente AEM di produzione rispetto al SLA (Service level agreement) previsto dal contratto.

## Visualizzare un rapporto di SLA {#introduction}

I dati dei rapporti di SLA tengono traccia delle metriche delle prestazioni per due livelli di produzione: livello di authoring e livello di pubblicazione.

Il grafico a linee di un anno selezionato include punti dati per ogni mese da gennaio a dicembre. Vengono tracciate le metriche seguenti.

| Metrica tracciata | Colore linea | Descrizione |
| --- | --- | --- |
| Autore livello effettivo | Verde chiaro | Il tempo di attività misurato relativo al livello di authoring della produzione, che tiene conto dei problemi attribuibili a Adobe o ai fornitori Adobe. |
| Autore livello contratto | Blu scuro | Il SLA definito nel contratto con Adobe per il livello di authoring. |
| Pubblica livello effettivo | Arancione | Il tempo di attività misurato per il livello di pubblicazione della produzione, tenendo conto degli incidenti causati da Adobe o dai fornitori di Adobe. |
| Pubblica livello contratto | Rosso | Il SLA definito nel contratto con Adobe per il livello di pubblicazione. |

**Per visualizzare un report di SLA:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nella pagina **Panoramica programma**, nel menu a sinistra, fare clic su **Report**.

1. Fai clic su **Rapporti SLA**.

   ![Grafico a linee del report di SLA](/help/implementing/cloud-manager/reports/assets/cm-sla-report2.png)

1. Fai clic sull’anno desiderato per visualizzare un grafico a linee dei dati di SLA.

1. (Facoltativo) Effettua una delle seguenti operazioni:

   * Sposta il cursore su un punto dati nel grafico a linee per visualizzare i valori specifici per quel punto.
   * Sotto l&#39;anno del grafico a linee, fare clic sull&#39;icona **Scarica** per salvare un file di immagine PNG del grafico a linee.
   * Fai clic sul nome di una metrica per visualizzarne solo i dati. In alternativa, premere `Shift` sulla tastiera durante la selezione o deselezione di uno o più nomi di metriche.

## Analisi degli eventi {#event-analysis}

La sezione **Analisi degli eventi** sotto il grafico mostra il set di incidenti che si sono verificati per il programma durante l&#39;anno selezionato.

Ogni problema presenta un intervallo di tempo, una causa e una serie di commenti.

![Esempio di analisi degli eventi](/help/implementing/cloud-manager/reports/assets/sla-reporting-c.png)

## Intervallo di aggiornamento dei rapporti di SLA {#refresh}

Il reporting di SLA offre ad insight le prestazioni dell’ambiente di produzione AEM ed è aggiornato, ma non istantaneo. La generazione di rapporti di SLA viene eseguita mensilmente e viene generata per i nuovi programmi contrassegnati come `Production previous month`. Non è istantaneo. A causa di questo ritardo, tieni presente quanto segue durante la revisione del rapporto SLA:

* Il SLA segnalato è quello esistente all’inizio del mese, anche se SLA è cambiato durante quel mese.
* Se all&#39;inizio del mese non era presente alcun SLA perché il programma non esisteva, verrà applicato il SLA esistente alla data di creazione del programma.

## Ambienti di anteprima {#preview}

L’ambiente di anteprima è uno strumento che consente agli autori dei contenuti di verificare l’esperienza finale del contenuto prima della pubblicazione. A causa di questa funzionalità, gli ambienti di anteprima non sono progettati per l’elevata disponibilità e non dispongono di un SLA associato.

