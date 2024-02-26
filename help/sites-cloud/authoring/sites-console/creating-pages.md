---
title: Creazione di pagine
description: Scopri come creare nuove pagine per il sito web utilizzando la console Sites.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 64%

---


# Creazione di pagine {#creating-pages}

Scopri come creare nuove pagine per il sito web utilizzando **Sites** console.

>[!TIP]
>
>Prima di iniziare a creare nuove pagine, acquisisci familiarità con [organizzazione delle pagine in AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## Privilegi di accesso {#access-privileges}

Il tuo account necessita dei diritti di accesso e delle autorizzazioni appropriati per creare le pagine.

Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

## Creazione di una nuova pagina {#creating-a-new-page}

A meno che le pagine non siano già state create tutte, prima di poter iniziare a creare il contenuto dovrai creare una pagina:

1. Apri [il **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Passa alla posizione in cui desideri creare la nuova pagina.
1. Apri il selettore a discesa utilizzando l’opzione **Crea** nella barra degli strumenti, quindi seleziona **Pagina** dall’elenco:

   ![Creazione di una pagina](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. Nel primo passaggio della creazione guidata puoi effettuare le seguenti operazioni:

   * Seleziona il modello da utilizzare per creare la nuova pagina, quindi seleziona **Successivo** per procedere.

   * Seleziona **Annulla** per interrompere la procedura.

   ![Selezione di un modello per una nuova pagina](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Nell’ultimo passaggio della creazione guidata puoi effettuare le seguenti operazioni:

   * Utilizza le tre schede per inserire [proprietà pagina](/help/sites-cloud/authoring/sites-console/page-properties.md) vuoi assegnarlo alla nuova pagina, quindi seleziona **Crea** per creare effettivamente la pagina.

   * Utilizza **Indietro** per tornare alla selezione del modello.

   I campi chiave sono:

   * **Titolo**:

      * Questo viene presentato all’utente ed è obbligatorio.

   * **Nome**:

      * Viene utilizzato per generare l’URI. Se non viene specificato, il nome viene derivato dal titolo.
      * Se si specifica una pagina **Nome** durante la creazione di una pagina, AEM [convalida il nome in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposto dall&#39;AEM e dal JCR.
      * **Non è possibile utilizzare caratteri non validi** nel campo **Nome**. Quando AEM rileva caratteri non validi, il campo viene evidenziato e viene visualizzato un messaggio esplicativo per indicare i caratteri da rimuovere o sostituire.

   >[!TIP]
   >
   >Consulta [Convenzioni di denominazione delle pagine](#page-naming-conventions).

   Le informazioni minime necessarie per creare una pagina sono **Titolo**.

   ![Fornire il titolo della pagina](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Tocca o fai clic su **Crea** per completare il processo e creare la nuova pagina. Viene visualizzata una finestra di dialogo di conferma in cui viene richiesto se desideri **aprire** subito la pagina o ritornare alla console (selezionando **Fine**):

   ![Creazione pagina completata](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Se per la pagina creata hai specificato un nome già esistente nello stesso percorso, viene automaticamente generata una variante del nome aggiungendo un numero. Se, ad esempio, esiste già `beach`, la nuova pagina diventa `beach1`.

1. Se ritorni alla console puoi visualizzare la nuova pagina:

   ![Nuova pagina risultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Una volta creata una pagina, il relativo modello non può essere modificato, a meno di [creare un lancio con un nuovo modello](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), anche se questo determinerà la perdita di eventuali contenuti esistenti.
