---
title: Informazioni sull’editor universale - Modalità reattiva
description: Questo articolo spiega come visualizzare in anteprima i moduli utilizzando diversi emulatori nell’editor universale per verificarne l’aspetto durante l’authoring.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 33%

---

# Modalità reattiva nell’authoring WYSIWYG

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l&#39;accesso, invia un&#39;e-mail dal tuo indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio. Ad esempio, se l&#39;URL del repository è https://github.com/adobe/abc, il nome dell&#39;organizzazione è adobe e il nome del repository è abc.</span>


L’[editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) consente di visualizzare in anteprima i moduli Edge Delivery Services con emulatori diversi per visualizzare l’aspetto del modulo durante l’authoring.

La modalità reattiva (o responsive) consente agli sviluppatori di progettare layout che si adattano automaticamente a diverse dimensioni di schermo, inclusi desktop, tablet e dispositivi mobili. L’editor universale supporta emulatori per desktop, tablet e dispositivi mobili. È possibile impostare l’altezza e la larghezza in base alle dimensioni dello schermo ed eseguire le azioni seguenti:

* Impostare l’orientamento
* Definire la larghezza e l’altezza
* Modificare l’orientamento

## Visualizzare in anteprima i moduli in modalità reattiva per dispositivi diversi

Universal Editor fornisce un&#39;icona **Emulatore** situata nell&#39;angolo in alto a destra dello schermo che consente di visualizzare in anteprima le pagine su dispositivi di dimensioni diverse e di verificare il comportamento della progettazione reattiva per una migliore esperienza utente.

Per vedere in che modo l’editor universale presenta i moduli per schermi di dimensioni diverse, effettua le seguenti operazioni:

1. Apri un modulo nell’editor universale per la modifica.
1. Selezionare l&#39;![icona Emulatore](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} disponibile sulla barra degli strumenti di Universal Editor e fare clic sull&#39;icona dell&#39;emulatore per visualizzare l&#39;opzione.

   ![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. Selezionare un&#39;opzione per emulare un modulo nell&#39;Editor universale su un dispositivo selezionato: Desktop, Tablet, Dispositivi mobili.

   ![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%,height=40%}

   Per impostazione predefinita, l’editor si apre in layout desktop, con altezza e larghezza definite automaticamente dal browser. In alternativa, è possibile emulare un modulo come verrebbe visualizzato su un dispositivo mobile o tablet. Puoi anche personalizzare la larghezza e l’altezza dello schermo per dispositivi personalizzati.

L’editor universale fornisce emulatori diversi per l’anteprima dei moduli su vari dispositivi. La tabella seguente elenca i tipi di emulatore disponibili e le relative rappresentazioni dei dispositivi:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo di emulatore</th>
        <th style="width: 80%">Immagine in base al dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Desktop</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Emulatore desktop" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tablet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Emulatore tablet" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivi mobili</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Emulatore mobile" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizzato</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Emulatore dispositivo personalizzato" style="width: auto; height: auto"></td>
    </tr>
</table>

Puoi utilizzare l’icona **Rotazione schermo** per passare all’orientamento orizzontale o verticale durante l’anteprima di un modulo su dispositivi diversi. Questo consente agli sviluppatori di testare il modo in cui la il design responsive si adatta alla rotazione dello schermo su vari dispositivi.

Universal Editor supporta i vari layout di modulo. Per esplorare il layout diverso, consulta la sezione [Funzionalità di layout](#layout-capabilities).

## Funzionalità di layout

Universal Editor consente di creare moduli di facile utilizzo che offrono esperienze dinamiche agli utenti finali. Il layout del modulo controlla la modalità di visualizzazione degli elementi o dei componenti in un modulo.

Universal Editor supporta i seguenti tipi di layout per i moduli:
* [Layout pannello](#panel-layout)
* [Layout procedura guidata](#wizard-layout)
* [Layout Accordion](#accordion-layout)

### Layout pannello

Il layout del pannello è utile per organizzare i campi correlati in modo da semplificare la navigazione e la ricerca del contenuto corrispondente. Il layout del pannello dispone i componenti del modulo all’interno di sezioni o pannelli distinti nei moduli.

![Layout pannello](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

È possibile utilizzare il [componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) per aggiungere il layout del pannello in un modulo. Per istruzioni dettagliate su come configurare varie proprietà del componente Pannello, consulta l&#39;articolo [componente Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Layout procedura guidata


Il layout della procedura guidata semplifica un modulo complesso suddividendolo in passaggi distinti. Ogni passaggio rappresenta una parte diversa del processo e gli utenti si spostano in sequenza, spesso con i pulsanti **Successivo** e **Indietro**. È possibile utilizzare il layout della procedura guidata per creare un modulo che comprenda più sezioni o passaggi.

![Layout guidato](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

È possibile utilizzare il [componente procedura guidata](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) per aggiungere il layout della procedura guidata in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente della procedura guidata, fare riferimento all&#39;articolo [componente della procedura guidata](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Layout Accordion

Il layout del Pannello a soffietto mostra il contenuto in sezioni o pannelli comprimibili in un Modulo adattivo. Quando una sezione viene espansa, il contenuto viene visualizzato all’interno di, mentre le altre sezioni rimangono compresse. Questo layout è ideale per visualizzare grandi quantità di informazioni in un formato compatto.

![Layout Accordion](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

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

## Consulta anche

{{universal-editor-see-also}}
