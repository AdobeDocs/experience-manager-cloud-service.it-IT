---
title: Utilizzare Media Library per la gestione di base delle risorse digitali
description: '"[!DNL Experience Manager Assets] e Media Library per la gestione delle risorse."'
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Utilizzare Media Library per la gestione delle risorse di base {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] Platform offre diverse funzionalità per la gestione delle risorse. Media Library consente agli utenti di caricare nell’archivio un numero limitato di risorse, di eseguire ricerche e utilizzarle nelle pagine web e di eseguire semplici attività di gestione delle risorse.

Media Library è una soluzione leggera per la gestione delle risorse digitali (DAM), [!DNL Adobe Experience Manager Sites] licenza. [!DNL Sites] è un’offerta WCM (Web Content Management). Media Library funziona con tutte le funzionalità di Experience Manager.

[!DNL Adobe Experience Manager Assets] licenza disponibile separatamente per l&#39;acquisto. [!DNL Experience Manager Assets] consente una gestione affidabile delle risorse tramite casi d’uso aziendali, personalizzazioni per metadati, schemi, ricerca e interfaccia utente e molte altre funzionalità oltre a quelle offerte da Media Library.

## Requisiti di licenza {#avail-media-library-license}

Clienti che hanno [!DNL Sites] Le licenze sono autorizzate a utilizzare Media Library. Funziona con tutti i componenti di [!DNL Experience Manager].

Media Library viene installato come parte di Sites. Non è richiesta alcuna licenza o pacchetto aggiuntivo oltre alla licenza e all’installazione di Sites.

## [!DNL Assets] rispetto a Media Library {#assets-and-media-library}

Experience Manager Assets fornisce funzionalità DAM di livello enterprise. La funzionalità Assets viene fornita con [!DNL Experience Manager] in un unico pacchetto. Tuttavia, gli utenti che non hanno acquistato una licenza di Assets non hanno il diritto di utilizzare le funzioni avanzate di DAM. Senza licenza Assets, solo [Funzioni di Media Library](#use-media-library) sono disponibili.

Per evitare l&#39;uso non intenzionale di [!DNL Assets] funzionalità per le quali non si dispone di una licenza, quindi rimuovere tutte le [!DNL Assets]: flussi di lavoro, componenti, tassonomie, opzioni e [!DNL Assets] amministratore da [!DNL Experience Manager]. In questo modo si evita che gli utenti utilizzino accidentalmente [!DNL Assets] funzionalità per le quali non hai concesso la licenza.

## Utilizza Media Library {#use-media-library}

Media Library copre ampiamente i seguenti casi di utilizzo:

* Fornire le funzioni DAM di base per le pagine web create utilizzando [!DNL Adobe Experience Manager Sites].
* Moduli adattivi e comunicazioni create utilizzando [!DNL Adobe Experience Manager Forms].
* Esperienze a schermo digitale create utilizzando [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API REST HTTP per operazioni headless.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Per utilizzare la funzionalità Media Library, è possibile utilizzare la [!DNL Experience Manager] interfaccia utente. Media Library fa parte del [!DNL Experience Manager Sites] installazione e non è necessaria alcuna interfaccia o componente aggiuntivo separata. Utilizzando l’interfaccia esistente, gli utenti di Media Library possono eseguire le seguenti attività:

* Crea cartelle per organizzare le risorse.
* Carica le risorse.
* Pubblicare le risorse.
* Modificare, spostare e copiare le risorse.
* Sfogliare, filtrare e cercare (include la ricerca per similarità) le risorse.
* Aggiungi valori a e modifica i valori nei campi di metadati, ad eccezione del campo Tag avanzati, disponibili nella variabile [!UICONTROL Base] scheda di una risorsa [!UICONTROL Proprietà] per impostazione predefinita.
* Aggiungi ed elimina rappresentazioni statiche.
* Scaricare cartelle, risorse e rappresentazioni di risorse.
* Creare versioni delle risorse.
* Crea ed esegui attività di revisione sulle risorse.
* Annotare le risorse.
* Aggiungi risorse a [!DNL Sites] tramite Content Finder.
* Utilizzo [!DNL Content Fragments].
* Utilizza le API REST HTTP e GraphQL per [!DNL Content Fragments] e risorse multimediali di riferimento, in licenza Sites.
* Integrazione del Marketing Cloud.
* Personalizza ed espandi l’interfaccia utente per la gestione delle risorse.
* Accedi all’API di Query Builder per estendere la funzionalità di ricerca.
* Creare tag statici.
* Progetti e attività di authoring.
* Flusso di attività (timeline).
* Commenti e annotazioni.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Molti casi d’uso avanzati di DAM sono soddisfatti da [!DNL Experience Manager Assets]. La licenza Media Library ti consente di soddisfare solo i casi d’uso elencati utilizzando Media Library. Se non è presente un caso d’uso, non utilizzarlo con una licenza Media Library. In caso di domande, contatta l’Assistenza clienti.

Non è possibile utilizzare tag avanzati, [!DNL Asset] collegamento, [!DNL Asset] selettore, assegnazione tag in blocco, modifica flussi di lavoro delle risorse o standard [!DNL Adobe Experience Manager] interfaccia utente per accedere a Media Library senza [!DNL Assets] licenza.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Funzioni di DAM in [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=it)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] descrizione del prodotto](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

