---
title: Aggiungere versioni, commenti e annotazioni a un modulo.
description: Utilizza i componenti core per moduli adattivi per aggiungere commenti, annotazioni e versioni a un modulo adattivo.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Adaptive Forms, Core Components
hidefromtoc: true
source-git-commit: e71e247f5b6de806b36c5c759b29e7273511f94e
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Controllo delle versioni, revisione e aggiunta di commenti in un modulo adattivo

<!--Before you can use versionings, comments, and annotations in an Adaptive Form, you must ensure you have [enabled Adaptive Form Core Components](
https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components).-->

<!--Adaptive Form Core Components facilitates to add versionings, comments, and annotations to a form. These features helps form authors and users to enhance the form development process where they can create multiple versions of a form, collaborate and add their comments to a form, and add annotations to form components.-->

<span class="preview"> Si tratta di una funzione pre-release accessibile tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>


I componenti core Moduli adattivi forniscono funzionalità che consentono agli autori dei moduli di incorporare nei moduli il controllo delle versioni, i commenti e le annotazioni. Queste funzioni semplificano il processo di sviluppo dei moduli consentendo agli utenti di creare e gestire più versioni di un modulo, avviare discussioni collaborative tramite commenti e allegare annotazioni a specifici componenti del modulo, migliorando in tal modo l’esperienza complessiva di creazione del modulo.


## Controllo delle versioni dei moduli adattivi {#adaptive-form-versioning}

Il controllo delle versioni adattive dei moduli consente di aggiungere versioni a un modulo. Gli autori dei moduli possono creare facilmente più versioni di un modulo e infine utilizzare quella adatta agli obiettivi aziendali. Gli utenti del modulo possono inoltre ripristinare le versioni precedenti del modulo. Consente inoltre agli autori di confrontare due versioni qualsiasi di un modulo visualizzandole in anteprima, consentendo loro di analizzare i moduli in modo migliore dal punto di vista dell’interfaccia utente. Passiamo ora ai dettagli per ogni funzionalità di controllo delle versioni dei moduli adattivi:

### Creare una versione del modulo {#create-a-form-version}

Per creare una versione di un modulo, effettuare le seguenti operazioni:

1. Creare un modulo o utilizzare un modulo esistente.
1. Nell’interfaccia utente dell’AEM, passa a **[!UICONTROL Modulo]**>>**[!UICONTROL Forms e documenti]** e seleziona il tuo **Modulo**.
1. Nel menu a discesa di selezione nel pannello a sinistra, seleziona **[!UICONTROL Versioni]**.
   ![Seleziona un modulo](select-a-form.png)
1. Fai clic su **tre punti** nel pannello inferiore a sinistra, fai clic su **[!UICONTROL Salva come versione]**.
1. A questo punto, assegnare un&#39;etichetta alla versione del modulo ed è possibile fornire informazioni sul modulo tramite il commento.
   ![Creare una versione del modulo](create-a-form-version.png)

### Aggiornare una versione del modulo {#update-a-form-version}

Quando modifichi e aggiorni il modulo adattivo, aggiungi una nuova versione al modulo. Per assegnare un nome a una nuova versione del modulo, come illustrato nell&#39;immagine, attenersi alla procedura descritta nell&#39;ultima sezione:

![Aggiornare una versione del modulo](update-a-form-version.png)

### Ripristinare una versione del modulo {#revert-a-form-version}

Per ripristinare una versione precedente di un modulo, selezionane una e fai clic su **[!UICONTROL Ripristina questa versione]**.

![Ripristina versione modulo](revert-form-version.png)

### Confronta versioni modulo {#compare-form-versions}

Gli autori dei moduli possono confrontare due versioni diverse di un modulo a scopo di anteprima. Per confrontare le versioni, seleziona una versione del modulo e fai clic su **[!UICONTROL Confronta con corrente]**. Vengono visualizzate due diverse versioni del modulo in modalità anteprima.

![Confronta versioni modulo](compare-form-versions.png)

## Aggiungi commenti {#add-comments}

Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti ai moduli. Qualsiasi utente di un modulo può aggiungere un commento a un modulo o esaminarlo tramite commenti. Per aggiungere un commento a un modulo, selezionare una **[!UICONTROL Modulo]**, e aggiungere una **[!UICONTROL Commento]** al modulo.

>[!NOTE]
> Quando utilizzi commenti nei componenti core per moduli adattivi come descritto in precedenza, la funzionalità del modulo [Creazione e gestione delle revisioni ai moduli](/help/forms/create-reviews-forms.md) è disabilitato.


![Aggiungere commenti in un modulo](form-comments.png)

## Aggiungi annotazioni {#adaptive-form-annotations}

In molti casi, agli utenti dei gruppi di moduli viene richiesto di aggiungere annotazioni a un modulo a scopo di revisione, ad esempio in una scheda specifica di un modulo o di componenti di un modulo. In questi casi, gli autori possono utilizzare le annotazioni. Per aggiungere annotazioni a un modulo, effettuare le seguenti operazioni:

1. Aprire un modulo in **[!UICONTROL Modifica]** modalità.

1. Fai clic su **icona aggiungi** si trova nella barra superiore destra, come indicato nell’immagine.
   ![Annotazione](annotation.png)

1. Fai clic su **icona aggiungi** si trova nella barra in alto a sinistra, come indicato nell’immagine, per aggiungere l’annotazione.
   ![Aggiungi annotazione](add-annotation.png)

1. Ora è possibile aggiungere commenti, disegnare schizzi con più colori per formare i componenti.

1. Per visualizzare tutte le annotazioni aggiunte a un modulo, selezionalo e visualizzerai le annotazioni aggiunte nel pannello sinistro, come illustrato nell’immagine.

   ![Vedi annotazioni aggiunte](see-annotations.png)

## Consulta anche {#see-also}

{{see-also}}
