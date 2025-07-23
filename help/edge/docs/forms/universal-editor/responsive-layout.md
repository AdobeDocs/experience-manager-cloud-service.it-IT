---
title: Informazioni sull’editor universale - Modalità reattiva
description: Questo articolo spiega come visualizzare in anteprima i moduli utilizzando diversi emulatori nell’editor universale per verificarne l’aspetto durante l’authoring.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: ht
source-wordcount: '1248'
ht-degree: 100%

---


# Modalità reattiva nell’authoring WYSIWYG

<span class="preview">Si tratta di una funzione pre-release accessibile tramite il <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale pre-release</a>. </span>

## Introduzione ai moduli reattivi

Nel mondo “multi-dispositivo” odierno, i moduli devono essere attraenti esteticamente e funzionare bene su schermi di tutte le dimensioni, dai monitor desktop agli smartphone. La modalità reattiva nell’editor universale ti aiuta a raggiungere questo risultato, consentendoti di visualizzare in anteprima e di testare i moduli su dispositivi di dimensioni diverse durante il processo di authoring.

L’[editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) consente di creare moduli che si adattano automaticamente a diverse dimensioni dello schermo, offrendo un’esperienza utente ottimale indipendentemente dal dispositivo utilizzato.

## Visualizzare in anteprima i moduli in modalità reattiva su dispositivi diversi

Nell’editor universale, un’icona **Emulatore** situata nell’angolo in alto a destra della schermata consente di visualizzare in anteprima le pagine su dispositivi di dimensioni diverse e di testare il comportamento della progettazione reattiva per una migliore esperienza utente.

Per visualizzare l’anteprima di un modulo in modalità reattiva:

1. Apri un modulo nell’editor universale per la modifica.
2. Fai clic sull’![icona dell’emulatore che mostra un simbolo di anteprima del dispositivo](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} nella barra degli strumenti.
3. Seleziona un formato di dispositivo:
   - Desktop (predefinito)
   - Tablet
   - Dispositivo mobile
   - Personalizzato (specifica larghezza e altezza)

![Schermata dell’editor universale che mostra le opzioni della modalità reattiva per diversi dispositivi](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

Puoi anche utilizzare l’icona **Rotazione schermo** per passare all’orientamento verticale o orizzontale durante l’anteprima su tablet o dispositivi mobili.

L’editor universale fornisce emulatori diversi per l’anteprima dei moduli su vari dispositivi. La tabella seguente elenca i tipi di emulatore disponibili e le relative rappresentazioni dei dispositivi:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo di emulatore</th>
        <th style="width: 80%">Immagine in base al dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Desktop</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Visualizzazione desktop di un modulo con layout a larghezza intera" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tablet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Visualizzazione Tablet di un modulo che mostra un layout di larghezza media con componenti regolati" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo mobile</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Visualizzazione per dispositivo mobile di un modulo che mostra un layout stretto con componenti sovrapposti" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizzato</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Visualizzazione per dispositivo personalizzato di un modulo con dimensioni specificate dall’utente" style="width: auto; height: auto"></td>
    </tr>
</table>

## Funzionalità di layout

L’editor universale consente di creare moduli di facile utilizzo che offrono esperienze dinamiche agli utenti finali. Il layout del modulo controlla il modo in cui gli elementi o i componenti vengono visualizzati in un modulo.

L’editor universale supporta i seguenti tipi di layout per i moduli:

- [Layout pannello](#panel-layout)
- [Layout procedura guidata](#wizard-layout)
- [Layout pannello a soffietto](#accordion-layout)

### Layout pannello

Il layout pannello è utile per organizzare i campi correlati in modo da semplificare la navigazione e la ricerca del contenuto corrispondente. Il layout pannello dispone i componenti del modulo all’interno di sezioni o pannelli distinti nei moduli.

![Layout pannello che mostra più sezioni distinte all’interno di un modulo](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Esempio:** un modulo di candidatura può utilizzare pannelli per separare “Informazioni personali”, ”Istruzione”, “Esperienza lavorativa” e “Referenze” in sezioni distinte.

**Comportamento reattivo:** negli schermi più piccoli, in genere i pannelli si sovrappongono verticalmente, mantenendo distinti i raggruppamenti e adattandosi a una larghezza ridotta.

È possibile utilizzare il [componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) per aggiungere il layout pannello in un modulo. Per istruzioni dettagliate su come configurare varie proprietà del componente pannello, consulta l’articolo [Componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Layout procedura guidata

Il layout procedura guidata semplifica un modulo complesso suddividendolo in passaggi distinti. Ogni passaggio rappresenta una parte diversa del processo e gli utenti si spostano attraverso di essi in sequenza, spesso con i pulsanti **Successivo** e **Indietro**. È possibile utilizzare il layout procedura guidata per creare un modulo che comprende più sezioni o passaggi.

![Layout procedura guidata che mostra un modulo con più passaggi con controlli di navigazione](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Esempio:** un modulo di richiesta di risarcimento potrebbe utilizzare una procedura guidata per orientare gli utenti nella fornitura dei dettagli sull’incidente, caricando le prove, immettendo informazioni personali e revisionando l’invio di tale richiesta.

**Comportamento reattivo:** nei dispositivi mobili la procedura guidata mantiene il proprio approccio dettagliato, ma regola il contenuto di ciascun passaggio per adattarsi allo schermo più stretto, spesso sovrapponendo elementi che su schermi più grandi apparirebbero affiancati.

È possibile utilizzare il [componente procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) per aggiungere il layout procedura guidata in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente procedura guidata, consulta l’articolo [Componente procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Layout pannello a soffietto

Il layout pannello a soffietto mostra il contenuto in sezioni o pannelli comprimibili in un modulo adattivo. Quando una sezione viene espansa, viene mostrato il contenuto all’interno, mentre le altre sezioni rimangono compresse. Questo layout è ideale per visualizzare grandi quantità di informazioni in un formato compatto.

![Layout pannello a soffietto con sezioni espandibili in un modulo](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Esempio:** un modulo per la configurazione di un prodotto potrebbe utilizzare sezioni a soffietto per “Opzioni di base”, “Funzioni avanzate”, “Accessori” e “Piani di pagamento”, consentendo agli utenti di concentrarsi su un aspetto alla volta.

**Comportamento reattivo:** i pannelli a soffietto funzionano particolarmente bene sui dispositivi mobili, in quanto conservano naturalmente lo spazio verticale mostrando solo la sezione di contenuto espansa, rendendoli ideali per gli schermi più piccoli.

È possibile utilizzare il [componente pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) per aggiungere il layout pannello a soffietto in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente pannello a soffietto, consulta l’articolo [Componente pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### Come scegliere il layout giusto?

È importante selezionare il layout giusto per ottimizzare l’esperienza utente e la funzionalità dei moduli. La tabella consente di comprendere le diverse opzioni di layout disponibili e ti aiuta nella selezione del layout più adatto in base alle tue esigenze e ai tuoi casi d’uso specifici:

| Funzione | Layout pannello | Layout procedura guidata | Layout pannello a soffietto |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Scopo** | Raggruppa il contenuto correlato in sezioni distinte | Guida gli utenti attraverso un processo o un modulo in più fasi | Organizza il contenuto in sezioni comprimibili |
| **Struttura** | Sezioni distinte | Passaggi/pagine sequenziali | Pannelli/sezioni comprimibili |
| **Navigazione** | Fai clic sulle intestazioni del pannello per spostarti | - In avanti: pulsante “Avanti”<br>- All’indietro: pulsante “Indietro”<br>- Salto dei passaggi facoltativo | Fai clic sulle intestazioni per espandere/comprimere le sezioni |
| **Esperienza utente** | Organizza grandi quantità di contenuti in modo gestibile | Guida dettagliata, riduzione del sovraccarico | Vista compatta con sezioni espanse/compresse |
| **Caso d’uso** | Moduli complessi con sezioni suddivise in categorie | Processi di configurazione, moduli complessi | Domande frequenti, menu delle impostazioni e sezioni contenuto dettagliate |
| **Ideale per dispositivi mobili** | Medio: i pannelli si sovrappongono in verticale | Buono: consente di concentrarsi solo sul passaggio corrente | Eccellente: consente di risparmiare spazio con sezioni comprimibili |

## Best practice per moduli reattivi

Per garantire che i moduli forniscano la migliore esperienza su tutti i dispositivi, segui queste best practice:

1. **Progettazione prima per dispositivi mobili:** iniziare progettando il modulo per dispositivi mobili, in un secondo momento apportare miglioramenti per schermi più grandi. Questo approccio garantisce che le funzionalità di base funzionino sugli schermi più piccoli.

2. **Utilizzo di tipi di campo appropriati:** scegliere i tipi di campo che funzionano correttamente sui dispositivi touch:
   - Utilizzare i menu a discesa invece dei pulsanti di scelta quando sono presenti molte opzioni
   - Utilizzare selettori di data progettati per l’input touch
   - Assicurarsi che i pulsanti e le destinazioni touch siano almeno 44 px x 44 px

3. **Semplificazione per schermi più piccoli:**
   - Visualizzare un numero inferiore di campi per riga sui dispositivi mobili
   - Prendere in considerazione di nascondere i campi opzionali dietro un’opzione “Mostra altro”
   - Suddividere i moduli complessi in più passaggi su dispositivi mobili

4. **Verifica approfondita:** verificare sempre i moduli su dispositivi reali o utilizzando la modalità emulatore nell’editor universale per assicurarne il corretto funzionamento su schermi di dimensioni diverse.

5. **Valutazione dei tempi di caricamento:** ottimizzare le dimensioni delle immagini e ridurre al minimo le risorse necessarie, in particolare per gli utenti di dispositivi mobili che potrebbero avere connessioni più lente.

## Risoluzione dei problemi dei moduli reattivi

| Problema   | Causa possibile | Soluzione |
|-------|---------------|----------|
| Sui dispositivi mobili il modulo appare tagliato | Problemi di overflow o impostazioni di larghezza risolti | Utilizzare le unità relative (%, rem) invece dei pixel e verificare le proprietà overflow:hidden |
| Elementi touch con cui è difficile interagire | Destinazioni touch troppo piccole o troppo vicine tra loro | Aumentare le dimensioni del pulsante/input ad almeno 44p x x 44 px e aumentare lo spazio tra gli elementi interattivi |
| Overflow del contenuto su schermi di piccole dimensioni | Nessuna regola reattiva per visualizzazioni più piccole | Aggiungere query multimediali o classi reattive per regolare il layout per diverse dimensioni dello schermo |
| Modulo troppo lento su dispositivi mobili | Immagini di grandi dimensioni o script eccessivi | Ottimizzare le immagini, ridurre al minimo JavaScript e prendere in considerazione il caricamento lento per gli elementi non critici |
| Aspetto diverso tra emulatore e dispositivi reali | Rendering specifico del browser o varianti di dispositivo | Se possibile, testare sui dispositivi reali, non solo sugli emulatori |

## Consulta anche

{#see-more-eds-forms}
