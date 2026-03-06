---
title: Incorporare un tema Forms adattivo in un tema AEM Sites
description: Scopri come integrare un tema Forms adattivo (ad esempio, Canvas) in un tema AEM Sites in modo che le pagine Sites e Forms adattivo incorporato condividano un tema e una distribuzione unificati.
keywords: tema per moduli adattivi, tema del sito, tema di AEM Sites, integrazione del tema dei moduli, pipeline front-end, incorporamento del tema
feature: Adaptive Forms, Core Components
role: Developer
exl-id: 0607e11c-84d2-42cb-be9f-acd7c328a342
source-git-commit: 343fc4fdc9b2947ff7771e3b74e77c679cf5c204
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Incorporare un tema Forms adattivo in un tema AEM Sites

Puoi incorporare un tema Forms adattivo (ad esempio [tema AEM Forms Canvas](https://github.com/adobe/aem-forms-theme-canvas)) nel tema AEM Sites. In questo modo, un singolo tema guida sia le pagine del sito che qualsiasi Forms adattivo incorporato in tali pagine, con una build e una distribuzione tramite la [pipeline front-end di AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html).

Questo articolo è destinato agli sviluppatori che mantengono o personalizzano il tema AEM Sites standard (o personalizzato) e desiderano includere lo stile Moduli adattivi senza gestire una distribuzione separata del tema Forms.

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di disporre di:

* **AEM as a Cloud Service** con [pipeline front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html) configurata per il tema del sito.
* **Origini tema sito**, ad esempio [tema modello sito standard](https://github.com/adobe/aem-site-template-standard) (l&#39;archivio che contiene `theme/` con `src/theme.scss`, `src/components/` e così via).
* **Origini tema Forms** - il [tema AEM Forms Canvas](https://github.com/adobe/aem-forms-theme-canvas) (o un altro tema Adaptive Forms compatibile) è stato clonato o scaricato localmente.
* **Node.js e npm**: per generare il tema del sito, vedere il file README del tema per le versioni supportate.
* **Maven** - se si genera il pacchetto del modello di sito completo (facoltativo per il lavoro solo tema).

>[!NOTE]
>
>**Nome tema:** Quando incorpori un tema Forms nel tema del sito e distribuisci tramite la pipeline front-end, **non devi modificare alcun nome tema**. Gli stili di modulo diventano parte del tema del sito esistente, che viene creato e distribuito con il nome corrente. La modifica del nome del tema (ad esempio in `package.json`) è necessaria solo quando si distribuisce un tema di Forms **autonomo** da un archivio tema dedicato; tale scenario è descritto in [Utilizzare i temi per assegnare uno stile a Forms adattivo basato su Componenti core](/help/forms/using-themes-in-core-components.md).

## Passaggio 1: creare la cartella dei componenti del modulo adattivo {#step-1-create-folder}

Nell’archivio dei temi del sito, crea la cartella in cui risiederà il tema Forms:

```text
theme/src/components/adaptiveform/
```

Tutte le risorse tema di Forms si troveranno in questa cartella, in modo che rimangano separate dai componenti del sito esistenti.

## Passaggio 2: copiare componenti e immagini del tema di Forms {#step-2-copy-components-and-images}

Utilizzo del **tema Forms** (ad esempio, `aem-forms-theme-canvas`) e dei percorsi del **tema del sito**:

1. **Copia cartelle componenti**\
   Dal tema Forms, copiare l&#39;intero contenuto di `src/components/` nel tema del sito come:

   ```text
   theme/src/components/adaptiveform/
   ```

   In questo modo si ottengono percorsi come:

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

   ![aggiungi componenti modulo adattivo](/help/forms/assets/theme-add-adaptiveform-component.png)

2. **Copia immagini**\
   Copia le immagini del tema Forms nel tema del sito:

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   Creare `theme/src/components/adaptiveform/resources/images/` se non esiste, quindi copiare tutte le risorse immagine (ad esempio `question.svg`, `Chevron-Left.svg`, `busy-state.gif` e così via).

   ![aggiungi immagini](/help/forms/assets/theme-add-images.png)

## Passaggio 3: copiare variabili e mixin {#step-3-copy-variables-and-mixins}

Il tema Forms utilizza variabili e mixin condivisi in `src/site/`. Copia solo questi due file nella **radice** di `adaptiveform/` (non all&#39;interno di una sottocartella `site`):

| Source (tema Forms) | Destinazione (tema del sito) |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

**non** copia il resto della cartella `src/site/` del tema Forms; per gli stili di modulo incorporati sono necessari solo questi due file.

![aggiungi variabili e mixin](/help/forms/assets/theme-add-mixin-variable.png)

## Passaggio 4: correggere i percorsi delle immagini in SCSS {#step-4-fix-image-paths}

Nel tema Forms, i file SCSS dei componenti spesso fanno riferimento a immagini con percorsi come `./resources/` o `url(resources/`. Dopo aver copiato nel tema del sito, tali percorsi devono puntare a `theme/src/components/adaptiveform/resources/images/`.

Il tema **del modello di sito standard** utilizza Parcel, che risolve `url()` percorsi da `theme/src/`. Pertanto, quando le immagini si trovano in `theme/src/components/adaptiveform/resources/images/`, utilizzare il percorso **`components/adaptiveform/resources/images/`** (relativo a `theme/src/`).

**Trova e sostituisci** in ogni `.scss` in `theme/src/components/adaptiveform/`:

| Trova | Sostituisci con |
|------|------------------|
| `./resources/` | `components/adaptiveform/resources/` |
| `url(resources/` | `url(components/adaptiveform/resources/` |
| `url('resources/` | `url('components/adaptiveform/resources/` |
| `url(../resources/` | `url(components/adaptiveform/resources/` |

**Esempio** - prima (tema Forms):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**Dopo** (tema del sito, immagini in `adaptiveform/resources/images/`):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(components/adaptiveform/resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

![Cambia URL immagini](/help/forms/assets/theme-change-url.png)

Ripetere l&#39;operazione per ogni file SCSS in `adaptiveform/` che fa riferimento a immagini (pulsante, pannello a soffietto, procedura guidata, contenitore, scarabocchio e altri). Si consiglia di eseguire una ricerca/sostituzione a livello di progetto nell&#39;IDE su `theme/src/components/adaptiveform/`.

## Passaggio 5: creare il modulo adattivo SCSS dal punto di ingresso {#step-5-create-adaptiveform-scss}

Crea **`theme/src/components/adaptiveform/_adaptiveform.scss`** nel tema del sito. Questo file deve:

1. Importa le variabili e i mixin condivisi.
2. Importa il file SCSS principale di ciascun componente Modulo adattivo.

Utilizza quanto segue come punto di ingresso completo (corrisponde all’integrazione standard con tutti i componenti modulo basati su Componenti core):

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

![scss modulo adattivo](/help/forms/assets/theme-adaptive-form-scss.png)

Se il tema Forms omette alcuni componenti (ad esempio, senza scarabocchio o captcha), rimuovi o commenta le righe `@import` corrispondenti per evitare errori di compilazione. L&#39;elenco precedente corrisponde alla struttura [Tema area di lavoro](https://github.com/adobe/aem-forms-theme-canvas).

## Passaggio 6: importare il tema del modulo adattivo nel tema del sito {#step-6-import-in-theme-scss}

In **`theme/src/theme.scss`**, aggiungi una singola importazione alla **fine** del file (dopo le importazioni di altri componenti):

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**Esempio** - fine di `theme.scss`:

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

![aggiungi scss modulo adattivo](/help/forms/assets/theme-add-adaptive-form-scss-theme.png)

Questa è l&#39;unica modifica necessaria nella struttura del tema del sito esistente; tutto il codice specifico del modulo rimane in `src/components/adaptiveform/`.

## Passaggio 7: generare e distribuire {#step-7-build-and-deploy}

1. Crea il tema del sito dalla directory principale del tema:

   ```bash
   cd theme
   npm install
   npm run build
   ```

   ![esegui compilazione](/help/forms/assets/theme-mpm-run-build.png)

2. Distribuisci tramite la [pipeline front-end esistente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html). Dopo la distribuzione, lo stesso CSS tema verrà applicato sia alle pagine del sito che al Forms adattivo incorporato.

## Risoluzione dei problemi {#troubleshooting}

| Problema | Cosa controllare |
|-------|-------------------------------|
| Build non riuscita: &quot;file non trovato&quot; per un’immagine | Verificare che tutte le immagini del modulo siano in `theme/src/components/adaptiveform/resources/images/`. In ogni `.scss` in `adaptiveform/`, utilizzare `url(components/adaptiveform/resources/images/...)` in modo che il percorso venga risolto da `theme/src/` (richiesto per la compilazione del tema del sito standard con pacchetto). Non utilizzare `../resources/` o `resources/` da solo a meno che il bundler non risolva percorsi per file; quindi utilizza il percorso che corrisponde alla cartella di immagini. |
| Build non riuscita: &quot;file non trovato&quot; per `_variables.scss` o `_mixin.scss` | Copiare entrambi i file dal tema di Forms `src/site/` in `theme/src/components/adaptiveform/` (radice adaptiveform), non all&#39;interno di una sottocartella `site`. |
| Build non riuscita: &quot;file non trovato&quot; per un componente (esempio: `_scribble.scss`) | Il tema Forms potrebbe non includere tale componente. In `theme/src/components/adaptiveform/_adaptiveform.scss`, rimuovere o commentare la riga `@import` per quel componente. |
| Il modulo viene riprodotto ma non presenta stili | Verificare che la pagina utilizzi la libreria client che include il CSS del tema generato e che `theme.scss` contenga la riga `@import './components/adaptiveform/_adaptiveform.scss';` e che il tema sia stato ricompilato e distribuito. |
| Conflitto di stili tra i componenti del sito e del modulo | Le classi dei componenti del modulo hanno namespace (ad esempio `cmp-adaptiveform-button`). In caso di conflitti, controlla se il CSS del sito personalizzato sostituisce tali classi e regola la specificità o l’ordine. |

## Consulta anche {#see-also}

* [Utilizzare i temi per assegnare uno stile al Forms adattivo basato su Componenti core](/help/forms/using-themes-in-core-components.md)
* [Sviluppa con pipeline front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)
