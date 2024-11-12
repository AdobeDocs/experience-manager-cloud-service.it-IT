---
title: Creazione delle pagine
description: Scopri come creare nuove pagine per il sito web utilizzando la console Sites.
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: dbe4cd619f4dc680e6fc4826f6a4fea92bab9707
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 27%

---


# Creazione delle pagine {#creating-pages}

Scopri come creare nuove pagine per il tuo sito web utilizzando la console **Sites**.

>[!TIP]
>
>Prima di iniziare la creazione di nuove pagine, conoscere [l&#39;organizzazione delle pagine in AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## Privilegi di accesso {#access-privileges}

Il tuo account necessita dei diritti di accesso e delle autorizzazioni appropriati per creare le pagine.

In caso di problemi, contattare l&#39;amministratore di sistema.

## Creazione di una nuova pagina {#creating-a-new-page}

A meno che le pagine non siano già state create tutte, prima di poter iniziare a creare il contenuto dovrai creare una pagina:

1. Apri [la console **Sites**.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Passa alla posizione in cui desideri creare la nuova pagina.
1. Apri il selettore a discesa utilizzando l’opzione **Crea** nella barra degli strumenti, quindi seleziona **Pagina** dall’elenco:

   ![Creazione di una pagina](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. Dal primo passaggio della procedura guidata, puoi effettuare le seguenti operazioni:

   * Seleziona il modello da utilizzare per creare la nuova pagina, quindi seleziona **Successivo** per procedere o **Annulla** per interrompere il processo.
   * I modelli sono supportati sia per l&#39;[Editor pagine](/help/sites-cloud/authoring/page-editor/introduction.md) che per l&#39;[Editor universale.](/help/sites-cloud/authoring/universal-editor/templates.md)

   ![Selezione di un modello per una nuova pagina](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Dalla fase finale della procedura guidata, puoi effettuare le seguenti operazioni:

   * Utilizza le tre schede per immettere le [proprietà di pagina](/help/sites-cloud/authoring/sites-console/page-properties.md) da assegnare alla nuova pagina, quindi seleziona **Crea** per creare effettivamente la pagina.

   * Utilizza **Indietro** per tornare alla selezione del modello.

   I campi chiave sono:

   * **Titolo**:

      * Questo viene presentato all’utente ed è obbligatorio.

   * **Nome**:

      * Viene utilizzato per generare l’URI. Se non viene specificato, il nome viene derivato dal titolo.
      * Se durante la creazione di una pagina si specifica il nome **Name**, l&#39;AEM [convalida il nome in base alle convenzioni](/help/implementing/developing/introduction/naming-conventions.md) imposte da AEM e JCR.
      * **Non è possibile utilizzare caratteri non validi** nel campo **Nome**. Quando l’AEM rileva caratteri non validi, il campo viene evidenziato e viene visualizzato un messaggio esplicativo per indicare i caratteri da rimuovere o sostituire.

   >[!TIP]
   >
   >Consulta [Convenzioni di denominazione delle pagine](#page-naming-conventions).

   Le informazioni minime necessarie per creare una pagina sono il **Titolo**.

   ![Fornire il titolo della pagina](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Tocca o fai clic su **Crea** per completare il processo e creare la nuova pagina. Nella finestra di dialogo di conferma viene richiesto se si desidera **aprire** la pagina immediatamente o tornare alla console (**Fine**). Selezionane uno per terminare il processo di creazione della pagina.

   ![Creazione pagina completata](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * Se scegli **Apri**, la console **Sites** apre l&#39;editor appropriato in base al modello della nuova pagina:
      * [Editor pagina](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md)

Se torni alla console, puoi visualizzare la nuova pagina:

![Nuova pagina risultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>Se crei una pagina utilizzando un nome che esiste già nella stessa posizione, AEM crea la pagina con una variante del nome specificato aggiungendo un numero. Ad esempio, se `beach` esiste già, la nuova pagina diventa `beach1`.

>[!CAUTION]
>
>Una volta creata una pagina, il relativo modello non può essere modificato a meno che non si [crei un lancio con un nuovo modello](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), anche se questo determinerà la perdita di eventuali contenuti esistenti.
