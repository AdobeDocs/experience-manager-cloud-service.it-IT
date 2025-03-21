---
title: Modifica in blocco dei metadati nella vista Risorse
description: Scopri come aggiornare un set predefinito di campi di metadati standard per più risorse disponibili contemporaneamente nella vista Assets.
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# Modifica in blocco dei metadati nella vista Risorse{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

La funzionalità **Modifica in blocco dei metadati** nella visualizzazione Assets consente agli utenti di modificare contemporaneamente un set predefinito di campi di metadati standard per più file di risorse. Seleziona più risorse e aggiorna contemporaneamente in blocco il set predefinito di metadati standard, anziché aggiornare singolarmente i metadati standard di ogni risorsa. Questa funzione migliora l’efficienza, la coerenza e la precisione delle proprietà di metadati standard in un’ampia serie di risorse, migliorando la ricercabilità delle risorse e l’organizzazione.

## Modificare in blocco i metadati delle risorse {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Per modificare in blocco i metadati di più risorse contemporaneamente, esegui i passaggi seguenti:

1. Nella visualizzazione Assets, fare clic su **Assets**.
1. Cerca risorse specifiche o esegui la ricerca utilizzando le parole chiave nella barra di ricerca.
1. Seleziona le risorse e fai clic su **Modifica in blocco metadati** nel menu principale.
   ![modifica in blocco dei metadati](/help/assets/assets/bulk-metadata-edit1.png)
1. Nella pagina Modifica metadati, modifica i campi seguenti nel pannello **Proprietà**:
   * **Stato:** Selezionare uno stato per le risorse selezionate.
   * **Data di scadenza:** Imposta una data dopo la quale le risorse non sono più valide o necessarie.
   * **Autore:** Specificare il nome dell&#39;autore.
   * **Parole chiave:** Aggiungi termini o stringhe di testo specifici che forniscano informazioni di alto livello sulle risorse per migliorarne la reperibilità. Aggiungete una parola chiave e premete Invio o Ritorna per aggiungerne un&#39;altra all&#39;elenco.
   * **Tag:** Fai clic sull&#39;icona ![tag](/help/assets/assets/tags-icon.svg) per selezionare i tag tra le opzioni disponibili. I tag forniscono informazioni più specifiche sulle risorse e ne migliorano la reperibilità. I tag già applicati alle risorse selezionate vengono visualizzati nel pannello **Proprietà**. Se non riesci a trovare i tag rilevanti, creali e assegnali alle risorse selezionate. Consulta [Gestire i tag nella vista Assets](/help/assets/tagging-management-assets-view.md) per informazioni dettagliate sulla creazione e l&#39;assegnazione di tag alle risorse.
   * Fai clic su **Salva** per applicare gli aggiornamenti dei metadati di cui sopra alle risorse selezionate. Una volta salvati, le parole chiave e i tag vengono aggiunti, mentre i dettagli aggiornati per Stato, Data di scadenza e Autore sostituiscono quelli esistenti.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >Puoi modificare i metadati di 100 risorse alla volta.

Per visualizzare gli aggiornamenti dei metadati applicati a una risorsa, passa alla pagina dei dettagli della risorsa (seleziona la risorsa e fai clic su **Dettagli**) e fai clic su ![](/help/assets/assets/info-icon-solid-black.svg) per visualizzare i metadati della risorsa nel pannello **Informazioni**.

>[!NOTE]
>
>**Stato**, **Data di scadenza**, **Autore**, **Parole chiave** e **Tag** sono proprietà di metadati standard disponibili per la modifica in blocco dei metadati, indipendentemente dai metadati specifici della cartella. Queste proprietà di metadati vengono visualizzate nella pagina dei dettagli della risorsa solo se sono incluse nel modulo metadati applicato alla cartella della risorsa. Se non riesci a trovare queste proprietà di metadati standard nella pagina dei dettagli della risorsa, modifica il modulo di metadati della cartella risorse per includerle. Per informazioni su come creare o modificare un modulo di metadati e applicarlo a una cartella, consulta [Metadati in Assets View](/help/assets/metadata-assets-view.md).
