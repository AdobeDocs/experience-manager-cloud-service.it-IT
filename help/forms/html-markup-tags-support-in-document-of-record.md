---
title: Tag di markup HTML supportati nel PDF di invio (precedentemente Document of Record)
description: Guida di riferimento per i tag di markup HTML supportati durante la generazione di un PDF di invio (precedentemente Document of Record), incluse considerazioni sul comportamento di rendering e sull’accessibilità.
feature: Adaptive Forms
role: Developer, User
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 6%

---


# Tag di markup HTML supportati nel PDF di invio (precedentemente Document of Record)

## Quali sono le implicazioni di questo riferimento?

AEM Forms ora supporta i tag di markup HTML nei campi Rich Text durante la generazione di un PDF Submission PDF (precedentemente Document of Record). Questa guida spiega quali tag di markup HTML puoi utilizzare in modo sicuro in Adaptive Forms e come vengono riprodotti nel PDF di invio generato.

Se ai moduli si aggiungono contenuti in formato Rich Text (ad esempio in grassetto, elenchi o collegamenti), è importante capire quali tag sono supportati e quali limitazioni possono avere. Questo riferimento consente di scegliere i tag appropriati per garantire la corretta visualizzazione e l’accessibilità del contenuto nel PDF di invio.

## Prima di iniziare

### Prerequisiti

Dovresti conoscere:

- Sintassi di markup HTML di base
- [Nozioni di base su PDF (in precedenza Documento di record)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- Principi di accessibilità e linee guida WCAG
- Requisiti di accessibilità di PDF
- Componenti del modulo adattivo che accettano il markup HTML

### Considerazioni

Il PDF di invio (precedentemente Document of Record) può essere un PDF con tag che garantisce l’accessibilità e la struttura corretta delle tecnologie per l’accessibilità. Per abilitare l&#39;output di PDF con tag, [impostare la proprietà XCI `config/present/pdf/tagged` su `true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Dopo aver generato il PDF, è importante verificare che i tag di accessibilità siano applicati correttamente. È possibile utilizzare [Adobe Acrobat per verificare i tag di accessibilità](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html) e assicurarsi che il documento soddisfi gli standard di accessibilità.

### Novità

Il supporto per testo RTF in Submission PDF è stato recentemente migliorato. In precedenza, il contenuto in formato Rich Text veniva visualizzato come testo normale nei documenti generati. Questa nuova funzionalità consente il corretto rendering del contenuto formattato negli output PDF.

## Riferimento per il supporto dei tag di HTML

### Tag completamente supportati

Questi tag sono completamente supportati con la corretta creazione dei nodi di accessibilità:

| Tag HTML | Descrizione | Invio supporto PDF | Accessibilità | Esempio |
|----------|-------------|-------------|---------------|---------|
| `<p>` | Paragrafo | Sì | Completamente supportato - Correzione nodo `<P>` | `<p>This is a paragraph.</p>` |
| `<br/>` | Interruzione di riga | Sì | Completamente supportato - entro `<P>` nodo | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | Testo grassetto | Sì | Completamente supportato - entro `<P>` nodo | `<b>bold text</b>` |
| `<i>` | Testo corsivo | Sì | Completamente supportato - entro `<P>` nodo | `<i>italic text</i>` |
| `<span>` | Contenitore in linea generico | Sì | all’interno di elementi di blocco | `<span>styled text</span>` |
| `<sub>` | Pedice | Sì | Completamente supportato - all’interno di elementi di blocco | `H<sub>2</sub>O` |
| `<sup>` | Apice | Sì | Completamente supportato - All’interno di elementi blocco | `E=mc<sup>2</sup>` |
| `<a>` | Collegamento ipertestuale | Sì | Supporto limitato: è necessaria una nidificazione corretta | `<a href="url">link text</a>` |


#### Elencare problemi di accessibilità

Il rendering elenco corrente crea `<P>` nodi invece della struttura elenco corretta:

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### Tag non supportati

Questi tag non sono supportati e non verranno visualizzati correttamente:

| Tag HTML | Descrizione | Soluzione alternativa |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | Tag di intestazione | Utilizza tag con stile `<p>` o intestazioni a livello di progettazione |
| `<img>` | Immagini | Utilizzare campi immagine o modelli struttura separati |
| `<code>` | Blocchi di codice | Usa caratteri monospazio con `<span>` stile |
| `<blockquote>` | Blocca offerte | Usa tag `<p>` con rientro |
| `<table>` | Tabelle | Utilizzare i componenti della tabella del modulo adattivo |

## Esempi di codice

### Formattazione testo di base

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### Elenchi

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### Collegamenti

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### Notazione scientifica

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## Contenuto correlato


- [Genera PDF di invio (precedentemente documento di record) per Forms adattivo](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [Genera PDF di invio per i componenti core](/help/forms/generate-document-of-record-core-components.md)
- [Personalizzazione del modello PDF di invio](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

