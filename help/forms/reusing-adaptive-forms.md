---
title: Come si riutilizzano le proprietà dei metadati di un modulo adattivo?
description: Scopri come riutilizzare in modo efficiente un modulo adattivo esistente per crearne uno nuovo.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
feature: Adaptive Forms, Foundation Components
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 3%

---

# Riutilizzare le proprietà dei metadati di un modulo adattivo {#reusing-adaptive-forms}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/reusing-adaptive-forms.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Se desideri utilizzare alcune delle proprietà di un modulo adattivo esistente per generarne uno nuovo, puoi semplicemente utilizzare la funzionalità di copia e incolla. Inoltre, puoi incollare il nuovo modulo adattivo nel percorso di cartella desiderato. Tutte le proprietà dei metadati vengono replicate e vengono copiati anche XFA e XSD per Forms adattivo basato su XFA e XSD.

>[!NOTE]
>
>Lo stato e i dettagli della revisione non vengono copiati. Ad esempio, se il modulo adattivo è pubblicato e quindi lo copi, il modulo adattivo incollato si trova nello stato non pubblicato. Analogamente, se una risorsa copiata è in revisione, la risorsa incollata non è in revisione.

## Copiare un modulo adattivo {#copy-an-adaptive-form}

Copiare un modulo adattivo utilizzando uno dei seguenti approcci:

1. Fai clic sull&#39;icona Copia ![aem6forms_copy](assets/aem6forms_copy.png) da Azioni rapide.

   >[!NOTE]
   >
   >Le azioni rapide sono le azioni che vengono visualizzate su una miniatura al passaggio del mouse.

1. Seleziona il modulo adattivo. Il processo di selezione è diverso per le diverse viste.

   Se ti trovi nella vista a schede, passa alla modalità di selezione facendo clic sull&#39;icona della selezione ![aem6forms_check-circle](assets/aem6forms_check-circle.png) e fai clic su tutti i Forms adattivi da copiare.

   Se ti trovi nella vista a elenco, fai clic sulle caselle di controllo di tutti i Forms adattivi per selezionarle.

   >[!NOTE]
   >
   >Tutte le risorse selezionate devono essere Forms adattivo perché la funzionalità di copia e incolla è supportata solo per Forms adattivo e tutte le risorse selezionate devono essere presenti nella stessa cartella.

   Dopo aver selezionato le risorse, fai clic sull&#39;icona Copia ![aem6forms_copy](assets/aem6forms_copy.png) presente nella barra degli strumenti per copiare il modulo adattivo selezionato.

## Incollare un modulo adattivo {#paste-an-adaptive-form}

Facendo clic sull&#39;azione di copia si esce automaticamente dalla modalità di selezione e si rende visibile l&#39;icona Incolla ![Incolla](assets/Smock_Paste_18_N.svg). Vai al percorso della cartella desiderato e fai clic sull&#39;icona Incolla ![Incolla](assets/Smock_Paste_18_N.svg) per incollare il modulo adattivo copiato.

Se si sta incollando nella stessa cartella o un altro file con lo stesso nome di nodo (con cui è memorizzato nell&#39;archivio di CRX) esiste in questa cartella di destinazione, 1 viene aggiunto al suffisso (ad esempio, myaf diventa myaf1 e se myaf1 esiste nella stessa posizione, myaf diventa myaf2. Tutte le altre proprietà rimangono invariate rispetto al modulo adattivo originale.

Dopo aver fatto clic sull&#39;icona Incolla ![Incolla](assets/Smock_Paste_18_N.svg), questa verrà nuovamente nascosta. È possibile incollare una sola volta. Per creare di nuovo una copia della stessa risorsa, copiala nuovamente.

## Modifica il contenuto del nuovo modulo adattivo {#change-contents-of-new-adaptive-form}

Il contenuto di un Forms adattivo incollato può essere modificato utilizzando i seguenti approcci per renderlo diverso dal modulo copiato:

1. **Modifica proprietà metadati:**

   Puoi modificare le proprietà dei metadati del modulo adattivo, ad esempio titolo e descrizione. Per ulteriori dettagli sulle proprietà dei metadati e su come modificarle, vedi [Gestione dei metadati del modulo](manage-form-metadata.md)

1. **Modifica XFA/XSD per Forms adattivo basato su XFA/XSD:**

   È possibile modificare l’XFA/XSD utilizzato in Adaptive Forms. Per sapere come è possibile modificare questi Forms adattivi, consulta [Gestione dei metadati del modulo](manage-form-metadata.md)

1. **Ripubblica:**

   La risorsa incollata è diversa da quella copiata. Puoi pubblicarla come nuova risorsa per renderla disponibile agli utenti finali. Per sapere come pubblicare una risorsa, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->


## Consulta anche {#see-also}

{{see-also}}