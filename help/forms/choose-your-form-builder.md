---
title: 'Generatore di moduli: scegli il tuo approccio'
description: Confronta i generatori di moduli e individua l’approccio corretto per la creazione di moduli adattivi. Per i creatori di moduli che necessitano di modelli o per la creazione di moduli complessi, scegliere il generatore di moduli più adatto alle proprie esigenze.
keywords: Forms Builder, AEM forms, creatore di moduli, creazione di moduli, creatore di moduli, moduli adattivi, componenti core, componenti di base, servizi di distribuzione edge, creazione di moduli
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: choose-form-builder-guide
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 8%

---


# Generatore di moduli: scegli il tuo approccio {#choose-your-form-builder}

Adobe Experience Manager (AEM) Forms offre tre potenti approcci per la creazione di moduli, ciascuno progettato per diversi casi d’uso, requisiti tecnici e destinazioni di pubblicazione. Che tu sia un creatore di moduli alla ricerca di modelli o uno sviluppatore che crea moduli complessi, questa guida ti aiuta a scegliere il generatore di moduli adatto al tuo progetto.

## Guida rapida alle decisioni

Utilizza questo riferimento rapido per identificare il generatore di moduli migliore per le tue esigenze:

| **Se hai bisogno di...** | **Scegli** |
|-------------------|------------|
| **Moduli moderni e scalabili con funzioni più recenti** | Componenti core |
| **Moduli veloci per siti Web a traffico elevato** | Editor universale |
| **Gestisci moduli esistenti o integrazioni legacy** | Componenti di base |
| **Authoring visivo con trascinamento** | Componenti core o editor universale |
| **Creazione di moduli basati su fogli di calcolo** | Authoring basato su documenti |
| **Consegna omni-channel (web, dispositivi mobili, chioschi)** | Componenti core (con API headless) |
| **Applicazioni front-end personalizzate (React, Angular)** | Componenti core (con API headless) |
| **Controllo completo del rendering dei moduli** | Componenti core (con API headless) |

## Informazioni sulle opzioni del generatore di moduli

AEM Forms offre tre approcci principali per la creazione di moduli, ciascuno progettato per diversi tipi di creatori di moduli e casi di utilizzo. Che tu abbia bisogno di un semplice creatore di moduli per attività rapide o di funzionalità avanzate di generazione moduli per progetti complessi, esiste un approccio che si adatta alle tue esigenze:

### Generatore di moduli per componenti Foundation

I componenti di base rappresentano la classica esperienza di authoring di AEM Forms. Anche se ancora supportati, sono principalmente consigliati per mantenere i moduli esistenti piuttosto che crearne di nuovi.

**Caratteristiche chiave:**

- Interfaccia di authoring tradizionale di AEM
- Stabilità comprovata per i flussi di lavoro esistenti
- Pubblicazione limitata a AEM
- Libreria dei componenti di base

### Generatore di moduli per componenti core

I Componenti core forniscono le funzionalità AEM Forms più recenti con prestazioni, accessibilità e flessibilità migliorate. Questo generatore di moduli è ideale per i creatori di moduli che necessitano di risultati professionali con funzioni moderne. Supporta la pubblicazione sia in AEM che in Edge Delivery Services e produce automaticamente moduli headless per la distribuzione basata su API su più piattaforme.

**Caratteristiche chiave:**

- Componenti moderni e standard
- Prestazioni e accessibilità migliorate
- Opzioni di pubblicazione flessibili (AEM + Edge Delivery)
- Funzionalità di personalizzazione avanzate
- Architettura scalabile
- Generazione automatica di moduli headless per la distribuzione omnicanale

### Editor universale (Edge Delivery Services)

Universal Editor fornisce due potenti approcci di authoring per Edge Delivery Services: l’authoring visivo WYSIWYG e l’authoring basato su documenti utilizzando fogli di calcolo. Questo approccio da creatore di moduli è perfetto per gli utenti che desiderano creare moduli rapidamente con prestazioni eccezionali.

**Caratteristiche chiave:**

- Prestazioni eccezionali (punteggi elevati per Lighthouse)
- Due metodi di authoring: WYSIWYG e basato su documenti
- Ottimizzato per Edge Delivery Services
- Prestazioni eccezionali e SEO
- Sviluppo e implementazione rapidi


## Confronto dettagliato

### Capacità tecniche

| **Funzionalità** | **Foundation** | **Core** | **Editor universale** | **Basato Su Documenti** |
|----------------|----------------|----------|---------------------|-------------------|
| **Complessità modulo** | Base | Avanzate | Avanzate | Da semplice a moderato |
| **Motore regole** | Avanzate | Avanzate | Avanzate | Limitata |
| **Componenti personalizzati** | ✅ | ✅ | ✅ | ✅ |
| **Temi** | ✅ | ✅ | A livello di progetto | A livello di progetto |
| **Modelli** | ✅ | ✅ | Solo contenuto iniziale |  |
| **Frammenti** | ✅ | ✅ | ✅ | ✅ |
| **Localizzazione** | ✅ | ✅ | Tramite AEM Sites | Manuale/Funzioni |

### Integrazione e invio

| **Funzione** | **Foundation** | **Core** | **Editor universale** | **Basato Su Documenti** |
|-------------|----------------|----------|---------------------|-------------------|
| **Modelli dati** | FDM, personalizzato | FDM, personalizzato | FDM, personalizzato | Personalizzato |
| **Invia azioni** | Più opzioni | Più opzioni | Più opzioni | Solo foglio di calcolo |
| **Precompilazione** | ✅ | ✅ | Tramite procedura guidata | ✅ |
| **CAPTCHA** | Più tipi | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise | reCAPTCHA Enterprise |
| **Allegati** | ✅ | ✅ | ✅ | Accesso anticipato |
| **Firme digitali** | ✅ |  |  |  |

### Pubblicazione e prestazioni

| **Aspetto** | **Foundation** | **Core** | **Editor universale** | **Basato Su Documenti** |
|------------|----------------|----------|---------------------|-------------------|
| **Pubblicazione** | Solo AEM | AEM + Edge Delivery + API headless | Edge Delivery | Edge Delivery |
| **Prestazioni** | Standard | Migliorato | Punteggi elevati di Lighthouse | Punteggi elevati di Lighthouse |
| **Ottimizzazione SEO** | Base | Buona | Eccellente | Eccellente |
| **Velocità di risposta mobile** | Buona | Eccellente | Eccellente | Eccellente |

## Scelta del generatore corretto

### Scegli i componenti di base se:

- Stai mantenendo i moduli basati su Foundation esistenti
- È necessaria l’integrazione della firma digitale
- Il flusso di lavoro dipende dalle funzioni di Foundation stabilite
- Stai lavorando secondo i requisiti di pubblicazione di sola AEM

**Ideale per:** manutenzione moduli, integrazione di sistemi legacy, flussi di lavoro stabiliti

### Scegli i Componenti core se:

- State costruendo nuove forme moderne
- È necessaria flessibilità per pubblicare su AEM o Edge Delivery Services
- Desideri le funzioni più recenti
- Sono necessari personalizzazione e temi avanzati
- Accessibilità e prestazioni sono priorità
- Desideri una tecnologia a prova di futuro

**Ideale per:** nuovi progetti, soluzioni scalabili, esperienze web moderne

### Scegli l&#39;editor universale se:

- Prestazioni eccezionali e SEO
- Stai creando per i siti Edge Delivery Services
- Sono necessari moduli complessi con azioni personalizzate
- È necessaria l&#39;integrazione con sistemi esterni

**Ideale per:** siti ad alte prestazioni, Edge Delivery Services, flussi di lavoro di authoring visivo

### Scegliere l&#39;authoring basato su documenti se:

- Gli utenti aziendali preferiscono l&#39;authoring basato su foglio di calcolo
- Necessità di eseguire rapidamente la prototipazione e l&#39;implementazione
- Forms sono relativamente semplici (sondaggi, registrazioni, feedback)
- La raccolta dei dati nei fogli di calcolo soddisfa le tue esigenze
- Non è richiesto alcun flusso di lavoro di invio avanzato

**Ideale per:** Distribuzione rapida, creazione di utenti aziendali, raccolta dati semplice


## Considerazioni sulla migrazione

### Dalla base ai componenti core

- **Approccio consigliato:** Utilizzare lo strumento [utilità di migrazione](/help/forms/migration-utility-tool-for-af-core-components.md)
- **Vantaggi:** funzioni moderne, prestazioni migliori, funzionalità di doppia pubblicazione
- **Impegno:** da moderato a elevato, a seconda della complessità del modulo

### Dall&#39;editor tradizionale all&#39;editor universale

- **Approccio:** rigenerare i moduli utilizzando WYSIWYG o l&#39;authoring basato su documenti in Universal Editor
- **Vantaggi:** Prestazioni eccezionali, esperienza di sviluppo moderna, punteggi SEO elevati
- **Impegno:** elevato per moduli complessi, basso per moduli semplici

## Guida introduttiva

Dopo aver scelto il generatore di moduli:

### Componenti di base

1. [Creare un modulo adattivo (componenti di base)](/help/forms/creating-adaptive-form.md)
2. [Guida all’authoring di Componenti Foundation](/help/forms/introduction-forms-authoring.md)

### Componenti core

1. [Creare un modulo adattivo (componenti core)](/help/forms/creating-adaptive-form-core-components.md)
2. [Panoramica delle funzioni dei Componenti core](/help/forms/adaptive-form-core-components-json-schema-form-model.md)

### Editor universale (Edge Delivery Services)

1. **Authoring di WYSIWYG:** [Guida introduttiva all&#39;editor universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
2. **Authoring basato su documenti:** [Crea il primo modulo con fogli di calcolo](/help/edge/docs/forms/tutorial.md)


## Hai bisogno di aiuto per decidere?

Non sei ancora sicuro di quale generatore di moduli scegliere? Considera questi fattori:

- **Esperienza del team:** Qual è il livello di abilità tecnica del tuo team?
- **Timeline del progetto:** Con quale rapidità è necessario eseguire la distribuzione?
- **Requisiti prestazionali:** Velocità e SEO sono fondamentali?
- **Scalabilità futura:** Sarà necessario espandere o modificare frequentemente i moduli?
- **Destinazione pubblicazione:** Dove verranno pubblicati i moduli?

Per assistenza personalizzata, consulta il team di implementazione di AEM Forms o il supporto Adobe.

## Articoli correlati

- [Confronto dettagliato dell’authoring dei moduli](/help/edge/docs/forms/authoring-a-form.md)
- [Panoramica dei componenti core di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it)
- [Panoramica di Edge Delivery Services per Forms](/help/edge/docs/forms/overview.md)
- [Forms adattivo headless con componenti core](https://experienceleague.adobe.com/it/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)
