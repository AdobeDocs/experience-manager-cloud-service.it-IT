---
title: Temi di riferimento, modelli e modelli di dati dei moduli
seo-title: Reference Themes, Templates, and Form Data models
description: AEM Forms fornisce temi, modelli e modelli di moduli adattivi per i moduli che è possibile ottenere dalla Distribuzione di software
seo-description: AEM Forms provides adaptive forms themes, templates, and form data models that you can get from Software Distribution
source-git-commit: 196a2f221c637d58ea6642177f530f158888efe0
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Temi di riferimento, modelli e modelli di dati dei moduli {#reference-themes-templates-and-data-models}

AEM Forms as a Cloud Service fornisce diversi temi di riferimento, modelli e modelli di dati per moduli per iniziare rapidamente a creare Forms adattivo. È possibile scaricare [pacchetto di contenuti di riferimento dal portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) e utilizza [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) per installare [pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) nell’ambiente di produzione, sviluppo o sviluppo locale, per ottenere queste risorse di riferimento nell’ambiente.

I temi, i modelli e i modelli di dati modulo inclusi nel pacchetto di contenuti di riferimento sono:


| Temi | Modelli | Modelli dati modulo |
---------|----------|---------
| Area di lavoro 3.0 | Base | Microsoft Dynamics 365 |
| Tranquillo | Vuoto | Salesforce |
| Urbane |  |  |
| Ultramarina |  |  |
| Berile |  |  |
| Sanità |  |  |
| FSI |  |  |

## Temi di riferimento {#reference-themes}

[Temi](/help/forms/themes.md) consente di personalizzare lo stile dei moduli senza conoscere a fondo i CSS. È possibile ottenere i seguenti temi installando il [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Berile
* Area di lavoro 3.0
* Tranquillo
* Urbane
* Ultramarina
* Sanità
* FSI (servizi finanziari e assicurazioni)

Ogni tema contiene uno stile unico ed elegante che può essere utilizzato per creare deliziosi moduli adattivi per i vostri utenti. Contiene uno stile univoco per selettori quali pannello, casella di testo, casella numerica, pulsante di scelta, tabella e switch. Gli stili in questi temi sono basati sui requisiti. Ad esempio, in uno scenario particolare è necessario un tema minimalista con caratteri puliti. Il tema Liberty ti permette di ottenere quel look.

![Temi di riferimento](assets/ref-themes.png)

I temi inclusi in questo pacchetto sono reattivi e lo stile in questi temi è definito per i display mobili e desktop. La maggior parte dei browser moderni su una varietà di dispositivi può eseguire il rendering dei moduli applicati con uno di questi temi senza problemi.

Per ulteriori informazioni sull&#39;installazione del pacchetto, vedi [Come lavorare con i pacchetti](/help/implementing/developing/tools/package-manager.md).

## Berile {#beryl}

Il tema beryl enfatizza l&#39;uso dell&#39;immagine di sfondo, la trasparenza, e grandi icone piatte. Nella schermata seguente è possibile vedere l’aspetto del tema Beryl e come può migliorare lo stile del modulo.

![Tema di berile](assets/beryl.png)

## Area di lavoro 3.0 {#canvas}

Canvas 3.0 è il tema predefinito per Adaptive Forms e enfatizza l&#39;uso di colori di base, trasparenza e icone piatte. Nella schermata seguente, puoi vedere come si presenta il tema Canvas 3.0.

![Tema di berile](assets/canvas.png)


## Tranquillo {#tranquil}

Il tema Tranquil fornisce sfumature chiare e scure della combinazione di colori Tranquillo per evidenziare diversi componenti di un modulo. Ad esempio, i pulsanti di scelta, i pannelli e le schede presentano una tonalità di verde diversa.

![Tema tranqual](assets/tranquil.png)


## Urbane {#urbane}

Tema urbano enfatizza un aspetto minimalista e funzionale della vostra forma. Quando si applica il tema Urbane al modulo, è possibile vedere che i componenti sono piatti. I pannelli ottengono contorni sottili per creare un look moderno.

![Tema urbano](assets/urbane.png)


## Ultramarina {#ultramarine}

Il tema ultramarino utilizza tonalità blu profonde per evidenziare componenti quali schede, pannelli, caselle di testo e pulsanti.

![Tema ultramarino](assets/ultramarine.png)

## Sanità {#healthcare}

Il tema medicale utilizza sfumature di verde intenso per evidenziare componenti quali schede, pannelli, caselle di testo e pulsanti.

![Tema FSI](assets/healthcare.png)


## FSI (servizi finanziari e assicurazioni)

Il tema FSI enfatizza un aspetto minimalista e funzionale del modulo. Quando si applica il tema FSI al modulo, è possibile notare che i componenti del pannello sono gialli.

![Tema FSI](assets/fsi.png)

## Modelli di riferimento {#reference-templates}


[Modelli](/help/forms/themes.md) consente di definire la struttura, il contenuto e le azioni iniziali del modulo per i moduli. È possibile ottenere i seguenti modelli installando il [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Base
* Vuoto

Il modello di base consente di creare rapidamente un modulo di iscrizione. È inoltre possibile utilizzarlo per visualizzare in anteprima le funzionalità dei componenti Adaptive Forms Foundation. Fornisce un layout guidato per la presentazione dei dati, sezione per sezione. Utilizza il modello vuoto per iniziare a creare un modulo adattivo da un’area di lavoro vuota.


## Modelli di dati dei moduli di riferimento {#reference-models}

L’Adaptive Forms può quindi interagire con i server Microsoft Dynamics 365 e Salesforce per abilitare i flussi di lavoro aziendali. Esempio:

* Inserire dati in Microsoft Dynamics 365 e Salesforce durante l’invio di moduli adattivi.
* Scrivere dati in Microsoft Dynamics 365 e Salesforce tramite entità personalizzate definite in Form Data Model e viceversa.
* Esegui una query sul server Microsoft Dynamics 365 e Salesforce per i dati e precompila Adaptive Forms.
* Leggi i dati da Microsoft Dynamics 365 e dal server Salesforce.

È possibile ottenere i seguenti modelli di dati modulo installando il [Pacchetto di contenuti di riferimento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

Per informazioni sull&#39;utilizzo di questi modelli, vedi [Configurare Microsoft Dynamics 365 e i servizi cloud Salesforce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)






