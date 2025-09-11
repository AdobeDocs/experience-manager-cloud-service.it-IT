---
title: Ereditarietà di contenuti nell’editor universale
description: Scopri in che modo Universal Editor supporta l’ereditarietà dei contenuti per la gestione multisito e i lanci per supportare il riutilizzo e la localizzazione dei contenuti.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 2a1b87c2-29b9-4689-9a15-e17942439160
source-git-commit: 2099a1aecd30eaa2ca3ca33a13729817a30b6c3f
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# Ereditarietà di contenuti nell’editor universale {#inheritance}

Scopri in che modo Universal Editor supporta l’ereditarietà dei contenuti per la gestione multisito e i lanci per supportare il riutilizzo e la localizzazione dei contenuti.

>[!NOTE]
>
>Questa funzione è disponibile solo per il contenuto archiviato nell’archivio AEM.

## Caso d’uso {#use-case}

Per molti utenti di AEM, la creazione di una pagina è solo l’inizio. Per ridimensionare il contenuto in modo efficace, in genere dopo la creazione della pagina sono necessari i seguenti passaggi:

1. **Traduci la pagina** utilizzando copie per lingua e flussi di lavoro di traduzione.
1. **Localizzare la pagina** utilizzando Gestione multisito per distribuire la pagina tradotta in mercati diversi.
1. **Crea nuove versioni** utilizzando i lanci per preparare le iterazioni future della pagina e attivare tali modifiche.

Questi passaggi possono accelerare la velocità dei contenuti e garantirne la coerenza. L’editor universale supporta l’ereditarietà dei contenuti, ovvero il meccanismo su cui si basano le copie per lingua, la gestione multisito e i lanci.

## Ereditarietà {#what-is-inheritance}

L’ereditarietà è il meccanismo in cui il contenuto può essere collegato in modo che la modifica di un elemento cambia automaticamente l’altro.

MSM e Launches sono strumenti potenti per aiutarti a riutilizzare i contenuti utilizzando l&#39;ereditarietà. Le pagine possono essere copiate da una sorgente centrale (la blueprint) per consentire agli autori di apportare modifiche specifiche al contesto di tali copie, mentre il resto del contenuto rimane ereditato dalla blueprint. Questa funzione è estremamente utile per la localizzazione dei siti.

Per modificare parte del contenuto delle copie, gli autori interrompono l’ereditarietà sui componenti interessati in modo da garantire che le modifiche locali non vengano sovrascritte quando le copie vengono sincronizzate dalla blueprint.

## Ereditarietà dei contenuti e Editor universale {#universal-editor}

Quando una pagina fa parte di MSM o di un lancio e il contenuto viene modificato con l&#39;Editor universale, l&#39;editor disabilita automaticamente l&#39;ereditarietà per tutte le modifiche apportate dagli autori sulla pagina, garantendo che il contenuto modificato venga mantenuto quando gli aggiornamenti vengono sincronizzati dalla blueprint.

L’autore non deve fare clic su un pulsante o adottare altri passaggi per disabilitare l’ereditarietà prima di apportare modifiche locali. Non appena viene apportata una modifica, l’ereditarietà viene implicitamente annullata. Questo flusso di lavoro è in contrasto con [Editor pagina](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components).

L’ereditarietà può essere ripristinata per l’intera pagina tramite:

* [Console Panoramica Live Copy](/help/sites-cloud/administering/msm/live-copy-overview.md)
* [Console dei lanci](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* Utilizzo del pulsante **Reimposta** nella scheda **Live Copy** della finestra [proprietà pagina](/help/sites-cloud/authoring/sites-console/page-properties.md).

L’editor universale non influisce sul meccanismo di ereditarietà sottostante. Per ulteriori dettagli sul funzionamento dell’ereditarietà, consulta la seguente documentazione.

* [Gestione multisito (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)

### Estensione AEM Multi-Site-Management (MSM) {#msm-extension}

Se installata, l&#39;estensione **AEM Multi-Site-Management (MSM)** visualizza lo stato di ereditarietà corrente del componente selezionato e consente di interrompere o ripristinare l&#39;ereditarietà a livello di componente.

Per ulteriori informazioni su come utilizzare questa estensione, consulta la documentazione per l&#39;authoring di [.](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)

Per informazioni su come abilitare questa estensione, [consulta la documentazione di Extension Manager.](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## Limitazioni {#limitations}

* Per ripristinare l&#39;ereditarietà per i singoli componenti, è necessario abilitare l&#39;estensione **AEM Multi-Site-Management (MSM)**.
* Per visualizzare il feedback visivo per vedere quali componenti hanno la loro ereditarietà disabilitata e quali ancora la mantengono, è necessario abilitare l&#39;estensione **AEM Multi-Site-Management (MSM)**.
