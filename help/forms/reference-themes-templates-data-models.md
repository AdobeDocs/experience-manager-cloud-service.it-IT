---
title: Temi di riferimento, modelli e modelli dati modulo
seo-title: Reference Themes, Templates, and Form Data models
description: AEM Forms fornisce temi, modelli e modelli di dati per moduli adattivi che è possibile ottenere da Software Distribution
seo-description: AEM Forms provides adaptive forms themes, templates, and form data models that you can get from Software Distribution
exl-id: 81588759-22da-4123-92fe-5ca97e97f1e4
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Temi di riferimento, modelli e modelli dati modulo {#reference-themes-templates-and-data-models}

AEM Forms as a Cloud Service fornisce più temi di riferimento, modelli e modelli di dati dei moduli per aiutarti a iniziare rapidamente a creare Adaptive Forms. È possibile scaricare [pacchetto di contenuti di riferimento dal portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) e utilizza [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) per installare [pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) nell’ambiente di produzione, sviluppo o sviluppo locale per trasferire queste risorse di riferimento all’ambiente.

I temi, i modelli e i modelli di dati dei moduli inclusi nel pacchetto di contenuti di riferimento sono:


| Temi | Modelli | Modelli dati modulo |
---------|----------|---------
| Area di lavoro 3.0 | Base | Microsoft Dynamics 365 |
| Tranquilla | Vuoto | Salesforce |
| Urbano |  |  |
| Ultramarina |  |  |
| Beryl |  |  |
| Assistenza sanitaria |  |  |
| FSI |  |  |

## Temi di riferimento {#reference-themes}

[Temi](/help/forms/themes.md) consente di applicare uno stile ai moduli senza una profonda conoscenza dei CSS. È possibile ottenere i seguenti temi installando [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Beryl
* Area di lavoro 3.0
* Tranquilla
* Urbano
* Ultramarina
* Assistenza sanitaria
* FSI (Servizi finanziari e assicurativi)

Ogni tema contiene uno stile univoco ed elegante che puoi utilizzare per creare moduli adattivi deliziosi per i tuoi utenti. Contiene uno stile univoco per selettori quali pannello, casella di testo, casella numerica, pulsante di scelta, tabella e interruttore. Gli stili in questi temi sono basati su requisiti. Ad esempio, in uno scenario particolare è necessario un tema minimalista con font puliti. Il tema Liberty ti permette di ottenere questo aspetto.

![Temi di riferimento](assets/ref-themes.png)

I temi inclusi in questo pacchetto sono reattivi e lo stile in questi temi è definito per i display mobili e desktop. La maggior parte dei browser moderni su diversi dispositivi può eseguire il rendering di moduli applicati con uno di questi temi senza alcun problema.

Per ulteriori informazioni sull’installazione del pacchetto, consulta [Come utilizzare i pacchetti](/help/implementing/developing/tools/package-manager.md).

## Beryl {#beryl}

Il tema Beryl enfatizza l&#39;uso di immagini di sfondo, trasparenza e icone grandi e piatte. Nella schermata seguente puoi vedere come si presenta il tema Beryl e come può migliorare lo stile del modulo.

![Tema Beryl](assets/beryl.png)

## Area di lavoro 3.0 {#canvas}

Canvas 3.0 è il tema predefinito per Adaptive Forms ed evidenzia l&#39;uso di colori di base, trasparenza e icone piatte. Nella schermata seguente puoi vedere come si presenta il tema Canvas 3.0.

![Tema Beryl](assets/canvas.png)


## Tranquilla {#tranquil}

Il tema Tranquilla fornisce sfumature chiare e scure della combinazione di colori Tranquil per evidenziare diversi componenti di una forma. Ad esempio, i pulsanti di scelta, i pannelli e le schede hanno una tonalità verde diversa.

![Tema Tranquilla](assets/tranquil.png)


## Urbano {#urbane}

Il tema Urbano enfatizza un aspetto minimalista e funzionale per la tua forma. Quando si applica il tema Urbane al modulo, è possibile vedere che i componenti sono piatti. I pannelli hanno contorni sottili per conferire un aspetto moderno.

![Tema Urbano](assets/urbane.png)


## Ultramarina {#ultramarine}

Il tema Ultramarine utilizza tonalità blu profonde per evidenziare componenti quali schede, pannelli, caselle di testo e pulsanti.

![Tema Ultramarino](assets/ultramarine.png)

## Assistenza sanitaria {#healthcare}

Il tema Healthcare utilizza tonalità verdi profonde per evidenziare componenti come schede, pannelli, caselle di testo e pulsanti.

![Tema FSI](assets/healthcare.png)


## FSI (Servizi finanziari e assicurativi)

Il tema FSI enfatizza un aspetto minimalista e funzionale per il modulo. Quando applichi il tema FSI al modulo, puoi vedere che i componenti del pannello sono gialli.

![Tema FSI](assets/fsi.png)

## Modelli di riferimento {#reference-templates}


[Modelli](/help/forms/themes.md) consente di definire la struttura iniziale del modulo, il contenuto e le azioni per i moduli. È possibile ottenere i seguenti modelli installando [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Base
* Vuoto

Il modello di base consente di creare rapidamente un modulo di iscrizione. Puoi utilizzarlo anche per visualizzare in anteprima la funzionalità dei componenti di Adaptive Forms Foundation. Fornisce un layout guidato per la presentazione sezione per sezione dei dati. Utilizza il modello vuoto per iniziare a creare un modulo adattivo da su un’area di lavoro vuota.


## Modelli dati modulo di riferimento {#reference-models}

Il Forms adattivo può quindi interagire con i server Microsoft Dynamics 365 e Salesforce per abilitare i flussi di lavoro aziendali. Ad esempio:

* Scrivere dati in Microsoft Dynamics 365 e Salesforce all’invio di moduli adattivi.
* Scrivi dati in Microsoft Dynamics 365 e Salesforce tramite entità personalizzate definite in Modello dati modulo e viceversa.
* Effettua query su Microsoft Dynamics 365 e server Salesforce per dati e precompila Forms adattivo.
* Leggi i dati da Microsoft Dynamics 365 e dal server Salesforce.

È possibile ottenere i seguenti modelli di dati del modulo installando [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

Per informazioni sull’utilizzo di questi modelli, consulta [Configurare Microsoft Dynamics 365 e i servizi cloud Salesforce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)
