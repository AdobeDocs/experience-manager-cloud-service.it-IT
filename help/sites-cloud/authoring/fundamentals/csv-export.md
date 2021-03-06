---
title: Esportazione in formato CSV
description: Esporta informazioni sulle pagine in un file CSV sul sistema locale
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '199'
ht-degree: 100%

---

# Esportazione in formato CSV   {#export-to-csv}

**Crea rapporto CSV** consente di esportare le informazioni contenute nelle pagine in un file CSV nel sistema locale.

* Il nome del file scaricato è `export.csv`
* Il contenuto dipende dalle proprietà selezionate.
* Puoi definire il percorso e il livello di profondità dell’esportazione.

>[!NOTE]
>
>Vengono utilizzate la funzione di download e la destinazione predefinita del browser in uso.

La procedura guidata **Crea esportazione CSV** permette di selezionare:

* Proprietà da esportare
   * Metadati
      * Nome
      * Modificato
      * Pubblicato
      * Modello
      * Flusso di lavoro
   * Traduzione
      * Tradotto
   * Analytics
      * Visualizzazioni pagina
      * Visitatori univoci
      * Tempo sulla pagina
* Profondità
   * Percorso principale
   * Solo elementi figlio diretti
   * Livelli aggiuntivi di elementi figlio
   * Livelli

Il file `export.csv` risultante può essere aperto in Excel o in un’altra applicazione compatibile.

Per creare un’esportazione CSV:

1. Apri la console **Sites** e passa alla posizione desiderata, se necessario.
   * L’opzione **Crea rapporto CSV** è disponibile nella vista a elenco della console **Sites**.
   * Si tratta di un’opzione del menu a discesa **Crea**:

      ![Opzione Crea CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. Dalla barra degli strumenti, seleziona **Crea**, quindi **Rapporto CSV** per aprire la procedura guidata:

   ![Opzioni di esportazione CSV](/help/sites-cloud/authoring/assets/csv-options.png)

1. Seleziona le proprietà da esportare.
1. Seleziona **Crea**.
   ![Esportazione CSV risultante in Excel](/help/sites-cloud/authoring/assets/csv-example.png)
