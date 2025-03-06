---
title: Informazioni sull’editor universale - Modalità reattiva
description: Questo articolo spiega come visualizzare in anteprima i moduli utilizzando diversi emulatori nell’editor universale per verificarne l’aspetto durante l’authoring.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 7%

---


# Modalità reattiva nell’authoring WYSIWYG

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l&#39;accesso, invia un&#39;e-mail con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio dall&#39;indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Ad esempio, se l&#39;URL del repository è https://github.com/adobe/abc, il nome dell&#39;organizzazione è adobe e il nome del repository è abc.</span>

## Introduzione a Responsive Forms

Nel mondo odierno del multi-dispositivo, i moduli devono avere un aspetto elegante e funzionare bene su schermi di tutte le dimensioni, dai monitor desktop agli smartphone. La modalità reattiva in Universal Editor consente di ottenere questo risultato, consentendo di visualizzare in anteprima e testare i moduli su dispositivi di dimensioni diverse durante il processo di authoring.

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) consente di creare moduli che si adattano automaticamente a diverse dimensioni dello schermo, offrendo un&#39;esperienza utente ottimale indipendentemente dal dispositivo utilizzato.

## Visualizzare in anteprima i moduli in modalità reattiva per dispositivi diversi

Universal Editor fornisce un&#39;icona **Emulatore** situata nell&#39;angolo in alto a destra dello schermo che consente di visualizzare in anteprima le pagine su dispositivi di dimensioni diverse e di verificare il comportamento della progettazione reattiva per una migliore esperienza utente.

Per visualizzare l’anteprima di un modulo in modalità reattiva:

1. Apri un modulo nell’editor universale per la modifica.
2. Fai clic sull&#39;icona dell&#39;![emulatore che mostra un simbolo di anteprima del dispositivo](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} nella barra degli strumenti.
3. Seleziona un formato di dispositivo:
   - Desktop (predefinito)
   - Tablet
   - Dispositivi mobili
   - Personalizzato (specifica larghezza e altezza)

![Schermata di Universal Editor che mostra le opzioni della modalità reattiva per diversi dispositivi](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

È inoltre possibile utilizzare l&#39;icona **Rotatore schermo** per passare da orientamento verticale a orientamento orizzontale durante l&#39;anteprima su dispositivi mobili o tablet.

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
        <td style="width: 20%">Dispositivi mobili</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Visualizzazione mobile di un modulo che mostra un layout stretto con componenti sovrapposti" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizzato</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Visualizzazione dispositivo personalizzata di un modulo con dimensioni specificate dall'utente" style="width: auto; height: auto"></td>
    </tr>
</table>

## Funzionalità di layout

Universal Editor consente di creare moduli di facile utilizzo che offrono esperienze dinamiche agli utenti finali. Il layout del modulo controlla la modalità di visualizzazione degli elementi o dei componenti in un modulo.

Universal Editor supporta i seguenti tipi di layout per i moduli:

- [Layout pannello](#panel-layout)
- [Layout procedura guidata](#wizard-layout)
- [Layout Accordion](#accordion-layout)

### Layout pannello

Il layout del pannello è utile per organizzare i campi correlati in modo da semplificare la navigazione e la ricerca del contenuto corrispondente. Il layout del pannello dispone i componenti del modulo all’interno di sezioni o pannelli distinti nei moduli.

![Layout del pannello che mostra più sezioni distinte all&#39;interno di un modulo](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Esempio:** Un modulo di candidatura per un processo può utilizzare pannelli per separare &quot;Informazioni personali&quot;, &quot;Istruzione&quot;, &quot;Esperienza di lavoro&quot; e &quot;Riferimenti&quot; in sezioni distinte.

**Comportamento reattivo:** Negli schermi più piccoli, i pannelli si sovrappongono in genere verticalmente, mantenendo i raggruppamenti distinti e regolando la larghezza su un valore più basso.

È possibile utilizzare il [componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) per aggiungere il layout del pannello in un modulo. Per istruzioni dettagliate su come configurare varie proprietà del componente Pannello, consulta l&#39;articolo [componente Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Layout procedura guidata

Il layout della procedura guidata semplifica un modulo complesso suddividendolo in passaggi distinti. Ogni passaggio rappresenta una parte diversa del processo e gli utenti si spostano in sequenza, spesso con i pulsanti **Successivo** e **Indietro**. È possibile utilizzare il layout della procedura guidata per creare un modulo che comprenda più sezioni o passaggi.

![Layout della procedura guidata che mostra un modulo con più passaggi con controlli di spostamento](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Esempio:** un modulo di richiesta di risarcimento potrebbe utilizzare una procedura guidata per guidare gli utenti fornendo dettagli sull&#39;incidente, caricando le prove, immettendo informazioni personali e rivedendo l&#39;invio.

**Comportamento reattivo:** Nei dispositivi mobili, la procedura guidata mantiene il proprio approccio graduale ma regola il contenuto all&#39;interno di ogni passaggio per adattarlo allo schermo più stretto, spesso impilando elementi che apparirebbero affiancati su schermi più grandi.

È possibile utilizzare il [componente procedura guidata](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) per aggiungere il layout della procedura guidata in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente della procedura guidata, fare riferimento all&#39;articolo [componente della procedura guidata](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Layout Accordion

Il layout del Pannello a soffietto mostra il contenuto in sezioni o pannelli comprimibili in un Modulo adattivo. Quando una sezione viene espansa, il contenuto viene visualizzato all’interno di, mentre le altre sezioni rimangono compresse. Questo layout è ideale per visualizzare grandi quantità di informazioni in un formato compatto.

![Layout Pannello a soffietto con sezioni espandibili in un modulo](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Esempio:** un modulo di configurazione del prodotto potrebbe utilizzare sezioni del Pannello a soffietto per &quot;Opzioni di base&quot;, &quot;Funzioni avanzate&quot;, &quot;Accessori&quot; e &quot;Piani di pagamento&quot;, consentendo agli utenti di concentrarsi su un aspetto alla volta.

**Comportamento reattivo:** Le fisarmoniche funzionano particolarmente bene sui dispositivi mobili in quanto conservano naturalmente lo spazio verticale mostrando solo la sezione di contenuto espansa, rendendole ideali per gli schermi più piccoli.

È possibile utilizzare il [componente Pannello a soffietto](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) per aggiungere il layout Pannello a soffietto in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente Pannello a soffietto, consulta l&#39;articolo [Componente Pannello a soffietto](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### Come scegliere il layout giusto?

È importante selezionare il layout giusto per ottimizzare l’esperienza utente e la funzionalità dei moduli. La tabella ti aiuta a comprendere le diverse opzioni di layout disponibili e ti guida nella selezione del layout più adatto in base alle tue esigenze e ai tuoi casi d’uso specifici:

| Funzione obsoleta | Layout pannello | Layout procedura guidata | Layout Accordion |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Scopo** | Raggruppa il contenuto correlato in sezioni distinte | Guida gli utenti attraverso un processo o un modulo in più fasi | Organizza il contenuto in sezioni comprimibili |
| **Struttura** | Sezioni distinte | Passaggi/pagine sequenziali | Pannelli/sezioni comprimibili |
| **Navigazione** | Fai clic sulle intestazioni del pannello per navigare | - Avanti: pulsante &quot;Avanti&quot;<br>- Indietro: pulsante &quot;Indietro&quot;<br>- Passaggi facoltativi ignorati | Fai clic sulle intestazioni per espandere/comprimere le sezioni |
| **Esperienza utente** | Organizza grandi quantità di contenuti in modo gestibile | Guida passo passo, riduzione del sovraccarico | Vista compatta con sezioni espanse/compresse |
| **Caso d’uso** | Moduli complessi con sezioni suddivise in categorie | Processi di configurazione, moduli complessi | Domande frequenti, menu delle impostazioni e sezioni del contenuto dettagliato |
| **Ottimo per dispositivi mobili** | Modera: i pannelli si sovrappongono in verticale | Corretto: consente di concentrarsi solo sul passaggio corrente | Eccellente: consente di risparmiare spazio con sezioni comprimibili |

## Best practice per Forms reattivo

Per garantire che i moduli forniscano la migliore esperienza su tutti i dispositivi, segui queste best practice:

1. **Progetta prima per dispositivi mobili:** Inizia progettando il modulo per dispositivi mobili, quindi migliora per schermi più grandi. Questo approccio garantisce che le funzionalità di base funzionino sugli schermi più piccoli.

2. **Utilizza i tipi di campo appropriati:** Scegli i tipi di campo che funzionano correttamente sui dispositivi touch:
   - Utilizza i menu a discesa invece dei pulsanti di scelta quando sono presenti molte opzioni
   - Utilizza selettori data progettati per l’input tocco
   - Assicurarsi che i pulsanti e le destinazioni touch siano almeno 44px x 44px

3. **Semplifica per schermi più piccoli:**
   - Visualizza un numero inferiore di campi per riga sui dispositivi mobili
   - Considera di nascondere i campi opzionali dietro un’opzione &quot;Mostra altro&quot;
   - Suddividi i moduli complessi in più passaggi su dispositivi mobili

4. **Verifica approfondita:** verifica sempre i moduli su dispositivi effettivi o utilizzando la modalità emulatore in Universal Editor per assicurarne il corretto funzionamento su schermi di dimensioni diverse.

5. **Valuta i tempi di caricamento:** Ottimizza le dimensioni delle immagini e riduci al minimo le risorse necessarie, in particolare per gli utenti mobili che potrebbero avere connessioni più lente.

## Risoluzione dei problemi di Responsive Forms

| Problema   | Possibile causa | Soluzione |
|-------|---------------|----------|
| Il modulo appare tagliato sui dispositivi mobili | Problemi di overflow o impostazioni di larghezza fisse | Usate le unità relative (%, rem) invece dei pixel e verificate la presenza di overflow:proprietà nascoste |
| Elementi touch difficili da interagire con | Toccare i target troppo piccoli o troppo vicini tra loro | Aumenta le dimensioni del pulsante/ingresso ad almeno 44 px x 44 px e aumenta lo spazio tra gli elementi interattivi |
| Overflow dei contenuti su schermi di piccole dimensioni | Nessuna regola reattiva per i riquadri di visualizzazione più piccoli | Aggiungi query multimediali o classi reattive per regolare il layout per diverse dimensioni di schermo |
| Modulo troppo lento su dispositivi mobili | Immagini di grandi dimensioni o script eccessivi | Ottimizza le immagini, riduci al minimo JavaScript e prendi in considerazione il caricamento lento per gli elementi non critici |
| Aspetto diverso tra emulatore e dispositivi reali | Rendering specifico del browser o varianti di dispositivo | Se possibile, prova sui dispositivi effettivi, non solo sugli emulatori |

## Consulta anche

{#see-more-eds-forms}
