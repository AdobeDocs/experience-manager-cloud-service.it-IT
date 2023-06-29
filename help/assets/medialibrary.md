---
title: Utilizza Media Library per la gestione di base delle risorse digitali
description: '"[!DNL Experience Manager Assets] e Media Library per la gestione degli asset".'
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 9%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Utilizza Media Library per la gestione di base delle risorse {#manage-assets-using-media-library}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager] Platform offre diverse funzionalità per la gestione delle risorse. Media Library consente agli utenti di caricare un numero limitato di risorse nell’archivio, cercare e utilizzare tali risorse nelle pagine web ed eseguire semplici attività di gestione delle risorse sulle risorse.

Media Library è una soluzione leggera di gestione delle risorse digitali (DAM) fornita con [!DNL Adobe Experience Manager Sites] licenza. [!DNL Sites] è un’offerta per la gestione dei contenuti web (WCM). Media Library funziona con tutte le funzionalità di Experience Manager.

[!DNL Adobe Experience Manager Assets] La licenza è disponibile separatamente per l&#39;acquisto. [!DNL Experience Manager Assets] consente di gestire in modo affidabile le risorse tramite casi d’uso aziendali, personalizzazioni per metadati, schemi, ricerche e interfacce utente e molte altre funzioni oltre a quelle fornite da Media Library.

## Requisiti delle licenze {#avail-media-library-license}

Clienti che hanno [!DNL Sites] La licenza di è autorizzata a utilizzare Media Library. Funziona con tutti i componenti di [!DNL Experience Manager].

Media Library viene installato come parte di Sites. Non è richiesta alcuna licenza o pacchetto aggiuntivo oltre alla licenza e all’installazione di Sites.

## [!DNL Assets] rispetto a Media Library {#assets-and-media-library}

Experience Manager Assets fornisce funzionalità DAM di livello enterprise. La funzionalità Assets viene fornita con [!DNL Experience Manager] in un&#39;unica confezione. Tuttavia, gli utenti che non hanno acquistato una licenza Assets non sono autorizzati a utilizzare le funzioni avanzate di DAM. Senza licenza Assets, solo [Funzioni di Media Library](#use-media-library) sono disponibili.

Se si desidera evitare l&#39;uso involontario di [!DNL Assets] funzioni per le quali non hai concesso la licenza, quindi rimuovi tutte le [!DNL Assets]specifici, componenti, tassonomie, opzioni e [!DNL Assets] amministratore da [!DNL Experience Manager]. In questo modo si evita che gli utenti utilizzino accidentalmente [!DNL Assets] funzionalità per le quali non si dispone della licenza.

## Usa Media Library {#use-media-library}

Media Library tratta in generale i seguenti casi d’uso:

* Fornisci funzioni DAM di base per le pagine web create con [!DNL Adobe Experience Manager Sites].
* Moduli adattivi e comunicazioni creati con [!DNL Adobe Experience Manager Forms].
* Esperienze di schermata digitale create con [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API REST HTTP per operazioni headless.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Per utilizzare la funzionalità Media Library, è possibile utilizzare il [!DNL Experience Manager] dell&#39;utente. Media Library fa parte di [!DNL Experience Manager Sites] e non è necessaria alcuna interfaccia o componente aggiuntivo separato. Utilizzando l’interfaccia esistente, gli utenti di Media Library sono autorizzati a eseguire le seguenti attività:

* Creare cartelle per organizzare le risorse.
* Caricare le risorse.
* Pubblicare le risorse.
* Modificare, spostare e copiare le risorse.
* Sfogliare, filtrare e cercare le risorse (inclusa la ricerca per similarità).
* Aggiungi e modifica i valori nei campi dei metadati, ad eccezione del campo Tag avanzati, disponibili in [!UICONTROL Base] scheda di una risorsa [!UICONTROL Proprietà] pagina per impostazione predefinita.
* Aggiungere ed eliminare rappresentazioni statiche.
* Scarica cartelle, risorse e rappresentazioni delle risorse.
* Creare le versioni delle risorse.
* Crea ed esegui attività di revisione sulle risorse.
* Annotare le risorse.
* Aggiungere risorse a [!DNL Sites] pagine tramite Content Finder.
* Utilizzo [!DNL Content Fragments].
* Utilizzare API REST e GraphQL HTTP per [!DNL Content Fragments] e risorse multimediali di riferimento, con licenza Sites.
* Integrazione del Marketing Cloud.
* Personalizzare ed estendere l’interfaccia utente per la gestione delle risorse.
* Accedi a Query Builder (API) per estendere la funzionalità di ricerca.
* Creare tag statici.
* Creare progetti e attività.
* Flusso di attività (timeline).
* Commenti e annotazioni.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Molti casi d’uso avanzati di DAM sono soddisfatti da [!DNL Experience Manager Assets]. La licenza di Media Library ti autorizza a soddisfare solo i casi d’uso elencati utilizzando Media Library. Se un caso d’uso non è elencato, non utilizzarlo con la licenza Media Library. Per eventuali domande, contatta l’Assistenza clienti.

Non è possibile utilizzare smart tag, [!DNL Asset] collegamento, [!DNL Asset] selettore, assegnazione di tag in blocco, modifica dei flussi di lavoro delle risorse o standard [!DNL Adobe Experience Manager] per accedere a Media Library senza [!DNL Assets] licenza.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Funzioni DAM in [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=it)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] descrizione del prodotto](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)
