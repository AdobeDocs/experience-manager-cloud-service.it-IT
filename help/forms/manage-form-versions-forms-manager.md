---
title: Gestire le versioni dei moduli in Forms Manager
description: Scopri come creare e gestire versioni di Adaptive Forms, frammenti di moduli, temi e altre risorse nell’interfaccia utente di Forms Manager.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
source-git-commit: 52d6e8163ef24d362287cbedf54c2977fff9c87b
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 4%

---


# Gestire le versioni delle risorse modulo nell’interfaccia utente di Forms Manager

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l&#39;accesso, invia un&#39;e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). </span>

Forms Manager ora supporta il controllo delle versioni per le risorse dei moduli. Puoi creare versioni, visualizzare la cronologia delle versioni e ripristinare le versioni precedenti delle risorse dall&#39;interfaccia utente di Forms Manager.

## Tipi di risorse supportati {#supported-asset-types}

Puoi creare e gestire le versioni per i seguenti tipi di risorse:

| Tipo risorsa | Descrizione |
|---|---|
| Forms adattivo (componenti core) | Forms adattivo creato utilizzando i Componenti core |
| Forms adattivo (componenti di base) | Forms adattivo creato utilizzando i componenti di base |
| Frammenti di modulo | Sezioni di moduli riutilizzabili condivise in più moduli |
| Temi | Definizioni di stile visivo applicate a Forms adattivo |
| Modelli XDP | Modelli di modulo basati su XFA |
| Risorse binarie | Altri file archiviati nei moduli archivio DAM |

## Crea una versione {#create-version-forms-manager}

Per creare una versione di una risorsa modulo:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona il modulo o la risorsa.
1. Nel pannello a sinistra, seleziona **[!UICONTROL Timeline]**.
1. Fai clic su **[!UICONTROL Salva come versione]** nella barra degli strumenti della timeline.
   ![Salva come versione](/help/forms/assets/create-version.png)
1. Immettere un **[!UICONTROL etichetta]** e un **[!UICONTROL commento]** facoltativo per descrivere le modifiche.
1. Fai clic su **[!UICONTROL Crea]**.
   ![Salva come versione 2](/help/forms/assets/create-version1.png)

La versione viene visualizzata nel pannello timeline con la relativa etichetta, commento e marca temporale.

## Versione di una risorsa durante il caricamento {#version-on-upload}

Quando carichi una risorsa con lo stesso nome di una risorsa esistente, Forms Manager visualizza una finestra di dialogo **Caricamento file** in cui sono elencate le risorse da aggiornare. La finestra di dialogo mostra il nome, la sezione e il percorso della risorsa.

Quando esiste già una risorsa con lo stesso nome, il caricamento sostituisce la risorsa esistente e crea automaticamente una nuova versione. Puoi visualizzare la versione creata nella timeline.

![Finestra di dialogo Caricamento file con caricamento con versione](/help/forms/assets/version-upload.png)

## Visualizza cronologia versioni {#view-version-history}

Per visualizzare la cronologia delle versioni di una risorsa:

1. Seleziona la risorsa in Forms Manager.
1. Nel pannello a sinistra, seleziona **[!UICONTROL Timeline]**.
   ![Cronologia versioni](/help/forms/assets/version-history.png)

La sequenza temporale mostra tutte le voci di versione insieme agli eventi di attività. Ogni voce mostra l’etichetta, il commento, l’autore e la marca temporale.

## Ripristinare una versione precedente {#restore-version}

Per ripristinare una risorsa a una versione precedente:

1. Seleziona la risorsa in Forms Manager.
1. Nel pannello a sinistra, seleziona **[!UICONTROL Timeline]**.
1. Selezionare la versione da ripristinare.
1. Fai clic su **[!UICONTROL Ripristina questa versione]**.
   ![Ripristina versione](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>Le immagini non possono essere ripristinate a una versione precedente. Tutti gli altri tipi di risorse, inclusi Forms adattivo, frammenti di modulo, temi e modelli XDP, supportano il ripristino delle versioni.

## Consulta anche {#see-also}

* [Controllo delle versioni, revisione e aggiunta di commenti in un modulo adattivo](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [Importare ed esportare moduli e risorse correlate](/help/forms/import-export-forms-templates.md)
* [Pubblicazione e annullamento della pubblicazione dei moduli](/help/forms/publishing-unpublishing-forms.md)
