---
title: Riutilizzare le proprietà dei metadati di un modulo adattivo
seo-title: Reuse metadata properties of an Adaptive Form
description: Puoi riutilizzare un modulo adattivo esistente per creare un nuovo Forms adattivo.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: f7f30545b76afa6abd4f49316d0fb2245f5470c2
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 4%

---

# Riutilizzare le proprietà dei metadati di un modulo adattivo {#reusing-adaptive-forms}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/reusing-adaptive-forms.html) |
| AEM as a Cloud Service | Questo articolo |

Se desideri utilizzare alcune delle proprietà di un modulo adattivo esistente per generarne uno nuovo, puoi semplicemente utilizzare la funzionalità di copia e incolla. Inoltre, puoi incollare il nuovo modulo adattivo nel percorso di cartella desiderato. Tutte le proprietà dei metadati vengono replicate e vengono copiati anche XFA e XSD per Forms adattivo basato su XFA e XSD.

>[!NOTE]
>
>Lo stato e i dettagli della revisione non vengono copiati. Ad esempio, se il modulo adattivo è pubblicato e quindi lo copi, il modulo adattivo incollato si trova nello stato non pubblicato. Analogamente, se una risorsa copiata è in revisione, la risorsa incollata non è in revisione.

## Copiare un modulo adattivo {#copy-an-adaptive-form}

Copiare un modulo adattivo utilizzando uno dei seguenti approcci:

1. Fai clic su Copia ![aem6forms_copy](assets/aem6forms_copy.png) da Azioni rapide.

   >[!NOTE]
   >
   >Le azioni rapide sono le azioni che vengono visualizzate su una miniatura al passaggio del mouse.

1. Seleziona il modulo adattivo. Il processo di selezione è diverso per le diverse viste.

   Se ti trovi nella vista a schede, passa alla modalità di selezione facendo clic sulla selezione ![aem6forms_check-circle](assets/aem6forms_check-circle.png) e fai clic su tutto il Forms adattivo da copiare.

   Se ti trovi nella vista a elenco, fai clic sulle caselle di controllo di tutti i Forms adattivi per selezionarle.

   >[!NOTE]
   >
   >Tutte le risorse selezionate devono essere Forms adattivo perché la funzionalità di copia e incolla è supportata solo per Forms adattivo e tutte le risorse selezionate devono essere presenti nella stessa cartella.

   Dopo aver selezionato le risorse, fai clic sulla copia ![aem6forms_copy](assets/aem6forms_copy.png) presente nella barra degli strumenti per copiare il modulo adattivo selezionato.

## Incollare un modulo adattivo {#paste-an-adaptive-form}

Facendo clic sull&#39;azione di copia, si esce automaticamente dalla modalità di selezione e si esegue l&#39;operazione Incolla ![Incolla](assets/Smock_Paste_18_N.svg) visibile. Ora vai al percorso della cartella desiderato e fai clic sul pulsante Incolla ![Incolla](assets/Smock_Paste_18_N.svg) per incollare il modulo adattivo copiato.

Se si incolla nella stessa cartella o in questa cartella di destinazione esiste un altro file con lo stesso nome di nodo (con il quale è memorizzato nell&#39;archivio CRX), al suffisso viene aggiunto 1 (ad esempio, myaf diventa myaf1 e, se myaf1 esiste nella stessa posizione, myaf diventa myaf2. Tutte le altre proprietà rimangono invariate rispetto al modulo adattivo originale.

Dopo aver fatto clic sull’icona Incolla ![Incolla](assets/Smock_Paste_18_N.svg) icona, sarà di nuovo nascosto. È possibile incollare una sola volta. Per creare di nuovo una copia della stessa risorsa, copiala nuovamente.

## Modifica il contenuto del nuovo modulo adattivo {#change-contents-of-new-adaptive-form}

Il contenuto di un Forms adattivo incollato può essere modificato utilizzando i seguenti approcci per renderlo diverso dal modulo copiato:

1. **Modifica proprietà metadati:**

   Puoi modificare le proprietà dei metadati del modulo adattivo, ad esempio titolo e descrizione. Per ulteriori dettagli sulle proprietà dei metadati e su come modificarle, consulta [Gestione dei metadati del modulo](manage-form-metadata.md)

1. **Modifica XFA/XSD per Forms adattivo basato su XFA/XSD:**

   È possibile modificare l’XFA/XSD utilizzato in Adaptive Forms. Per sapere come è possibile modificare questi Forms adattivi, consulta [Gestione dei metadati del modulo](manage-form-metadata.md)

1. **Ripubblica:**

   La risorsa incollata è diversa da quella copiata. Puoi pubblicarla come nuova risorsa per renderla disponibile agli utenti finali. Per sapere come pubblicare una risorsa, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
