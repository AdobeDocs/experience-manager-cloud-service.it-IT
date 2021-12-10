---
title: Riutilizzare le proprietà dei metadati di un modulo adattivo
seo-title: Reuse metadata properties of an Adaptive Form
description: È possibile riutilizzare un modulo adattivo esistente per creare un nuovo Forms adattivo.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Riutilizzare le proprietà dei metadati di un modulo adattivo {#reusing-adaptive-forms}

Se si desidera utilizzare alcune delle proprietà di un modulo adattivo esistente per generarne una nuova, è sufficiente utilizzare la funzionalità di copia e incolla. Inoltre, puoi incollare il nuovo modulo adattivo nel percorso della cartella desiderato. Vengono replicate tutte le proprietà dei metadati e vengono copiati anche i file XFA e XSD per i Forms adattivi basati su XFA e XSD.

>[!NOTE]
>
>Lo stato e i dettagli della revisione non vengono copiati. Ad esempio, se il modulo adattivo viene pubblicato e successivamente lo si copia, lo stato del modulo adattivo incollato non viene pubblicato. Analogamente, se una risorsa copiata è in fase di revisione, la risorsa incollata non è sotto la stessa revisione.

## Copiare un modulo adattivo {#copy-an-adaptive-form}

Copiare un modulo adattivo utilizzando uno dei seguenti approcci:

1. Fai clic su Copia ![aem6forms_copy](assets/aem6forms_copy.png) da Azioni rapide.

   >[!NOTE]
   >
   >Le azioni rapide sono gli elementi che vengono visualizzati su una miniatura al passaggio del mouse.

1. Selezionare il modulo adattivo. Il processo di selezione è diverso per le diverse viste.

   Se siete nella vista a schede, passate alla modalità di selezione facendo clic sulla selezione ![aem6forms_check-cerchio](assets/aem6forms_check-circle.png) e fai clic su tutti i Forms adattivi da copiare.

   Se ti trovi nella vista a elenco, fai clic sulle caselle di controllo di tutti gli Adaptive Forms per selezionarli.

   >[!NOTE]
   >
   >Tutte le risorse selezionate devono essere Adaptive Forms perché la funzionalità di copia e incolla è supportata solo per Adaptive Forms e tutte le risorse selezionate devono essere presenti nella stessa cartella.

   Dopo aver selezionato le risorse, fai clic sulla copia ![aem6forms_copy](assets/aem6forms_copy.png) presente nella barra degli strumenti per copiare il modulo adattivo selezionato.

## Incolla un modulo adattivo {#paste-an-adaptive-form}

Quando si fa clic sull’azione di copia, la modalità di selezione viene automaticamente chiusa e l’opzione incolla ![Incolla](assets/Smock_Paste_18_N.svg) icona visibile. Ora vai al percorso della cartella desiderato e fai clic su incolla ![Incolla](assets/Smock_Paste_18_N.svg) per incollare il modulo adattivo copiato.

Se si incolla nella stessa cartella o in un altro file con lo stesso nome di nodo (con il quale è memorizzato nell&#39;archivio CRX) esiste in questa cartella di destinazione, viene aggiunto 1 al suffisso (ad esempio, myaf diventa myaf1 e se myaf1 esiste nella stessa posizione, myaf diventa myaf2. Tutte le altre proprietà rimangono invariate rispetto al modulo adattivo originale.

Dopo aver fatto clic sul pulsante Incolla ![Incolla](assets/Smock_Paste_18_N.svg) icona, si nasconderà di nuovo. È possibile incollare una sola volta. Per creare nuovamente una copia della stessa risorsa, copiala nuovamente.

## Modificare il contenuto del nuovo modulo adattivo {#change-contents-of-new-adaptive-form}

Il contenuto di un Forms adattivo incollato può essere modificato utilizzando i seguenti approcci per renderlo diverso dal modulo copiato:

1. **Modificare le proprietà dei metadati:**

   È possibile modificare le proprietà dei metadati del modulo adattivo, ad esempio titolo e descrizione. Per ulteriori dettagli sulle proprietà dei metadati e su come modificarle, consulta [Gestione dei metadati dei moduli](manage-form-metadata.md)

1. **Modificare XFA/XSD per Forms adattivo basato su XFA/XSD:**

   È possibile modificare XFA/XSD utilizzato in Forms adattivo. Per sapere come è possibile modificare questi Forms adattivi, vedi [Gestione dei metadati dei moduli](manage-form-metadata.md)

1. **Ripubblica:**

   La risorsa incollata è diversa da quella copiata. Puoi pubblicarlo come nuova risorsa per renderlo disponibile agli utenti finali. Per sapere come pubblicare una risorsa, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
