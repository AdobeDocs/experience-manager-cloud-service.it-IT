---
title: Modifica in blocco dei metadati nella vista Assets
description: Scopri come modificare simultaneamente i metadati di più risorse disponibili nella visualizzazione Assets.
source-git-commit: 5778d0dac141174c1b950625057f920af0301a8b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Modifica in blocco dei metadati nella vista Assets{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

Utilizzando **Modifica in blocco dei metadati** nell&#39;interfaccia utente di Assets View, puoi modificare i metadati per più file di risorse contemporaneamente. Invece di modificare i metadati di ogni singola risorsa, puoi applicare le modifiche a un gruppo di risorse più ampio alla volta. Questa funzione migliora l’efficienza, la coerenza e la precisione delle proprietà dei metadati in un’ampia serie di risorse, migliorando la ricercabilità delle risorse e l’organizzazione.

## Modificare in blocco i metadati delle risorse {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Per modificare in blocco i metadati di più risorse contemporaneamente, esegui i passaggi seguenti:

1. Nella visualizzazione Assets, fare clic su **Assets**.
1. Sfoglia le risorse o immetti le parole chiave pertinenti nella barra di ricerca per individuare risorse specifiche.
1. Seleziona più risorse e fai clic su **Modifica in blocco metadati** dal menu principale.
   ![modifica in blocco dei metadati](/help/assets/assets/bulk-metadata-edit.png)
1. Nella pagina Modifica metadati, modifica i campi seguenti nel pannello **Proprietà**:
   * **Stato:** seleziona uno stato per definire l&#39;usabilità delle risorse selezionate.
   * **Data di scadenza:** Imposta una data dopo la quale le risorse non sono più valide o necessarie.
   * **Autore:** Specificare il nome dell&#39;autore.
   * **Parole chiave:** Aggiungi termini o stringhe di testo che forniscano informazioni di alto livello sulle risorse per migliorarne la reperibilità. Aggiungete una parola chiave e premete Invio o Ritorna per aggiungerne un&#39;altra all&#39;elenco.
     <!-- * **Tags:** Click ![tags icon](/help/assets/assets/tags-icon.svg) to select tags from the available options. Tags provide more specific information about the assets and enhances their discoverability. Tags already applied to the selected assets are only displayed in the **Properties** panel. If you cannot find the relevant tags, create the tags and assign them to the selected assets. See [Manage tags in Assets view](/help/assets/tagging-management-assets-view.md) for details.-->
   * Fai clic su **Salva** per aggiungere parole chiave e <!-- Tags while--> sovrascrive i dettagli esistenti per Stato, Data di scadenza e Autore.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties1.png)

     >[!NOTE]
     >
     >Puoi modificare i metadati di 100 risorse alla volta.

Per visualizzare le modifiche ai metadati applicate a una risorsa, passa alla pagina dei dettagli della risorsa (seleziona la risorsa e fai clic su **Dettagli**) e fai clic su ![](/help/assets/assets/info-icon-solid-black.svg) per visualizzare i metadati della risorsa nel pannello **Informazioni**.

>[!NOTE]
>
>Stato, Data di scadenza, Autore e Parole chiave <!-- and Tags--> sono proprietà di metadati standard disponibili per la modifica in blocco di metadati, indipendentemente dai metadati specifici della cartella. Queste proprietà di metadati vengono visualizzate nella pagina dei dettagli della risorsa solo se sono incluse nel modulo metadati applicato alla cartella della risorsa.  Se non riesci a visualizzare queste proprietà di metadati nella pagina dei dettagli della risorsa, modifica il modulo di metadati della cartella risorse per includerle. Per informazioni su come creare o modificare un modulo di metadati e applicarlo a una cartella, consulta [Metadati in Assets View](/help/assets/metadata-assets-view.md).


