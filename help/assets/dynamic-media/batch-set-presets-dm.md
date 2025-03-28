---
title: Predefiniti set di batch
description: Scopri come automatizzare la creazione di set di immagini e set 360 gradi utilizzando i predefiniti set di batch in Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3434'
ht-degree: 0%

---

# Predefiniti per set di batch {#about-bsp}

Utilizza **[!UICONTROL Predefiniti set di batch]** per creare e organizzare più risorse in un set di immagini o set 360 gradi al momento del caricamento dei file di risorse in una cartella singolarmente o mediante l&#39;acquisizione in blocco. Il predefinito può essere eseguito insieme ai processi di importazione risorse pianificati in [!DNL Dynamic Media]. Ogni predefinito è un set di istruzioni indipendente con nome univoco che definisce come creare il set di immagini o il set 360 gradi utilizzando immagini che corrispondono alle convenzioni di denominazione definite nella ricetta predefinita.

>[!IMPORTANT]
>
>Si utilizzano i predefiniti per set di batch in [!DNL Dynamic Media Classic] e si esegue la migrazione da [!DNL Dynamic Media Classic] ad Adobe Experience Manager as a Cloud Service? In tal caso, è necessario ricreare manualmente le definizioni dei predefiniti per set di batch in [!DNL Adobe Experience Manager as a Cloud Service].

**Best Practice** - Quando si lavora con i predefiniti per set di batch, Adobe consiglia il seguente flusso di lavoro:

1. Crea un predefinito per set di batch. Vedi [Creare un predefinito per set di batch per un set di immagini o un set 360 gradi](#creating-bsp).
1. Creare una cartella di risorse o utilizzare una cartella di risorse esistente e assicurarsi che sia sincronizzata in [!DNL Dynamic Media]. Consulta [Creare cartelle](/help/assets/manage-digital-assets.md#creating-folders).
1. Applica il predefinito per set di batch alla cartella delle risorse. Vedere [Informazioni sull&#39;applicazione di predefiniti set di batch alle cartelle](#apply-bsp).
1. Carica le immagini nella cartella delle risorse. Consulta [Caricare risorse per set di immagini](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Caricare risorse per set 360 gradi](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) o [Aggiungere risorse digitali a Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. Il set di immagini o il set 360 gradi viene generato automaticamente nella cartella desiderata.
1. Pubblica il set di immagini o il set 360 gradi. Consulta [Pubblicare Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Creare un predefinito per set di batch per set di immagini o set 360 gradi {#creating-bsp}

Per creare predefiniti per set di batch, è opportuno conoscere e comprendere le espressioni regolari.

Idealmente, la tua azienda ha già definito una convenzione di denominazione per il modo in cui le risorse vengono raggruppate in un set.
Per comprendere l&#39;importanza di utilizzare una convenzione di denominazione, si supponga che la convenzione di denominazione definita della società sia `<style>-<color>-<view>`. Il nome di base del set deve essere sempre `<style>-<color>` e l&#39;estensione del nome del set `-SET`. Se carichi un&#39;immagine denominata `0123-RED-01`, verrà creato un set denominato `0123-RED-SET`. Se in seguito si caricano le immagini `0123-RED-03` e `0123-BLUE-01`, l&#39;immagine `RED-03` verrà aggiunta al set nella seconda posizione perché è ordinata inferiore a `01`. L&#39;immagine `BLUE-01` farebbe parte di un nuovo set denominato `0123-BLUE-SET`. Per il successivo caricamento della risorsa, aggiungi i file `0123-RED-02` e `0123-BLUE-02`. Ogni risorsa viene aggiunta al rispettivo set. L&#39;immagine `RED-02` verrebbe automaticamente ordinata tra le immagini esistenti `01` e `03`, a causa dell&#39;ordinamento.

La pagina **[!UICONTROL Predefinito per set di batch]** in [!DNL Dynamic Media] consente di creare, modificare o eliminare i predefiniti per set di batch e di applicare o rimuovere i predefiniti per set di batch da o verso le cartelle di risorse. Puoi utilizzare gli elenchi a discesa dei campi modulo per definire un predefinito per set di batch oppure il campo **[!UICONTROL Codice non elaborato]**, che consente di digitare la sintassi delle espressioni regolari.

Puoi creare molti predefiniti per set di batch in modo da coprire tutti i processi di acquisizione risorse necessari.

### Informazioni sulla convenzione di denominazione delle risorse

L&#39;area **[!UICONTROL Convenzione per la denominazione delle risorse]** nella pagina **[!UICONTROL Predefinito set di batch]** include due elementi che è possibile utilizzare per definire il predefinito set di batch: **[!UICONTROL Corrispondenza]** e **[!UICONTROL Nome base]**. Questi elementi ti consentono di definire una convenzione di denominazione e di identificare la parte della convenzione utilizzata per denominare il set in cui sono contenuti. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convenzione di denominazione individuale di un’azienda spesso utilizza una o più righe di definizione da ciascuno di questi due elementi. È possibile utilizzare un numero illimitato di righe per la definizione univoca e raggrupparle in elementi distinti, ad esempio per l&#39;immagine principale, l&#39;elemento Colore, l&#39;elemento Visualizzazione alternativa e l&#39;elemento Campione.

Ad esempio, la sintassi per un’espressione regolare di corrispondenza letterale potrebbe essere simile alla seguente:

`(\w+)-\w+-\w+`

### Informazioni sull&#39;ordinamento delle sequenze

Facoltativamente, è possibile definire l&#39;ordine di visualizzazione delle immagini dopo il raggruppamento del set di immagini o del set 360 gradi in [!DNL Dynamic Media]. Per impostazione predefinita, le risorse sono ordinate in ordine alfanumerico. Tuttavia, puoi utilizzare un elenco separato da virgole di espressioni regolari per definire l’ordine.

Per quanto riguarda l’automazione dell’ordinamento di sequenze, se necessario, specifica delle regole per forzare l’ordinamento delle risorse in un determinato modo. Si supponga, ad esempio, che la prima risorsa sia sempre denominata `_main` e si desideri che sia seguita da `_alt1`, `_alt2`, `_alt3` e così via. In questi casi, puoi creare una regola di ordinamento di sequenza con la seguente sintassi:

`.*_main,.*_alt[0-9]`

Anche se una sequenza di ordinamento forzato è possibile, è meglio basarsi il più possibile sulla numerazione alfanumerica per l’ordinamento delle sequenze. Inoltre, è possibile utilizzare gli strumenti editor set di immagini o set 360 gradi in [!DNL Dynamic Media] per riorganizzare l&#39;ordine di sequenza delle risorse oppure aggiungere ed eliminare nuove risorse nel set mediante un&#39;operazione di trascinamento della selezione.

Al termine della creazione di un predefinito per set di batch, lo si applica a una o più cartelle create. Vedere [Informazioni sull&#39;applicazione di predefiniti set di batch alle cartelle](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Per creare un predefinito per set di batch per un set di immagini o un set 360 gradi:**

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti set di batch]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, nell&#39;angolo superiore destro, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea predefinito per set di batch]** immettere un nome descrittivo nel campo di testo **[!UICONTROL Nome predefinito]**. Il nome del predefinito non può essere modificato se successivamente decidete di modificarlo.

1. Nell&#39;elenco a discesa **[!UICONTROL Tipo di predefinito]**, selezionare **[!UICONTROL Set di immagini]** o **[!UICONTROL Set360 gradi]**. Accertatevi di scegliere il tipo di predefinito corretto; non sarà più possibile modificarlo.
1. Seleziona **[!UICONTROL Crea]**.
1. Sulla destra della pagina **[!UICONTROL Modifica predefinito per set di batch]**, imposta le opzioni modificabili desiderate nelle intestazioni **[!UICONTROL Dettagli predefinito]** e **[!UICONTROL Imposta convenzione di denominazione]**.
Per ulteriori informazioni sulle opzioni modificabili disponibili, vedere [Dettagli predefinito, Imposta convenzione di denominazione e Risultati regola - Opzioni RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Crea uno o più gruppi di espressioni regolari.

   * Nella pagina **[!UICONTROL Modifica predefinito per set di batch]**, alla voce **[!UICONTROL Corrispondenza]**, **[!UICONTROL Nome base]** o **[!UICONTROL Ordinamento sequenza]**, selezionare **[!UICONTROL Aggiungi gruppo]**.
   * Il campo **[!UICONTROL Corrispondenza]** è obbligatorio. **[!UICONTROL Nome base]** è obbligatorio solo se il campo **[!UICONTROL Corrispondenza]** non specifica già un nome base utilizzando un raggruppamento di parentesi quadre. **[!UICONTROL L&#39;ordinamento delle sequenze]** è facoltativo.
   * Utilizzando gli elenchi a discesa e le caselle di testo nel modulo del gruppo, specifica un gruppo di espressioni da utilizzare per definire i criteri di denominazione per i membri della risorsa set di immagini o set 360 gradi.
      * Quando selezioni e specifichi le espressioni per un gruppo, tieni presente che la sintassi delle espressioni regolari effettive si riflette vicino alla parte inferiore destra della pagina, sotto l&#39;intestazione **[!UICONTROL Risultati regola - RegX]**. Per visualizzare la stringa di espressione regolare aggiornata in basso a destra, selezionare un punto qualsiasi al di fuori dell&#39;area del modulo. Queste stringhe di espressioni regolari rappresentano il pattern che si desidera associare in una ricerca di [!DNL Dynamic Media] risorse per creare il set di immagini o il set 360 gradi.
      * Se hai aggiunto un gruppo e vuoi rimuoverlo, seleziona **[!UICONTROL X]**.
   * Quando si aggiungono due o più gruppi, nell&#39;elenco a discesa **[!UICONTROL And]** selezionare **[!UICONTROL And]** per unire un gruppo appena aggiunto a qualsiasi gruppo di espressioni precedente aggiunto. In alternativa, selezionare **[!UICONTROL Or]** per aggiungere un&#39;alternanza tra il gruppo di espressioni precedente e il nuovo gruppo creato. L&#39;operando **[!UICONTROL Or]** è definito dall&#39;utilizzo di un carattere di riga verticale `|` nella sintassi stessa dell&#39;espressione regolare.

1. Effettua una delle seguenti operazioni:

   * Per aggiungere un altro nuovo gruppo, in **[!UICONTROL Corrispondenza]**, **[!UICONTROL Nome base]** o **[!UICONTROL Ordine di sequenza]**, selezionare **[!UICONTROL Aggiungi gruppo]**. Creare un altro gruppo di espressioni regolari come nel passaggio precedente.
   * Verificare la sintassi delle espressioni regolari nell&#39;area **[!UICONTROL Risultati regola - RegX]**. Se devi modificare la sintassi, apporta le modifiche nel rispettivo gruppo a sinistra della pagina.
   * Se la creazione dei gruppi di espressioni è stata completata, procedere al passaggio successivo.

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.

Ora puoi applicare il predefinito per set di batch a una cartella di risorse. Quindi carica le risorse in tale cartella. Questo flusso di lavoro determina la generazione automatica del set di immagini o del set 360 gradi. Consulta [Informazioni sull&#39;applicazione di predefiniti per set di batch alle cartelle di risorse](#apply-bsp).

### Dettagli del predefinito, Imposta convenzione di denominazione e Risultati regola - Opzioni RegX {#features-options-bsp}

Queste opzioni sono disponibili nella pagina **[!UICONTROL Modifica predefinito per set di batch]** quando si crea o si modifica un predefinito per set di batch.

Consulta [Creare un predefinito per set di batch per un set di immagini o un set 360 gradi](#creating-bsp) o [Modificare un predefinito per set di batch](#edit-bsp).

| **[!UICONTROL Dettagli predefinito]** | Descrizione |
| --- | --- |
| Nome predefinito | Sola lettura. Il nome specificato al momento della creazione del set di batch. Se è necessario rinominare il predefinito, è possibile copiare il predefinito per set di batch esistente e specificare un nuovo nome. Vedi [Copiare un predefinito per set di batch esistente](#copy-bsp). |
| Tipo | Sola lettura. Tipo specificato al momento della creazione del set di batch. La copia di un predefinito per set di batch esistente non consente di modificarne il [!UICONTROL tipo]; è necessario creare un predefinito. |
| Includi risorse derivate | Facoltativo. Per fare in modo che l&#39;IPS (Image Production System) di [!DNL Dynamic Media] includa immagini generate o &quot;derivate&quot; con il set 360 gradi o il set di immagini, selezionare **[!UICONTROL Sì]** (impostazione predefinita). Una risorsa derivata è un’immagine che non è stata caricata direttamente da un utente. Al contrario, la risorsa è stata prodotta da IPS al caricamento di una risorsa principale. Ad esempio, una risorsa immagine generata da IPS da una pagina in un PDF al momento del caricamento di PDF in [!DNL Dynamic Media] è considerata una risorsa derivata. |
| Cartella di destinazione | Facoltativo. Se definisci un numero elevato di set di immagini o set 360 gradi, Adobe consiglia di mantenere questi set separati dalle cartelle che contengono le risorse stesse. Pertanto, è consigliabile creare una cartella Set di immagini o Set 360 gradi e reindirizzare l&#39;applicazione per inserire qui i set di batch generati.<br>In questo caso, specificare la cartella all&#39;interno della struttura di cartelle di Experience Manager Assets (`/content/dam`) in cui è attivo il predefinito per set di batch. Assicurarsi che la cartella sia abilitata per la sincronizzazione [!DNL Dynamic Media] per consentirla come cartella di destinazione. Vedi [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>È possibile assegnare un predefinito per set di batch a più cartelle, se si applica il predefinito tramite le **[!UICONTROL proprietà]** della cartella. Vedere [Applica predefiniti set di batch dalla pagina Proprietà di una cartella di risorse](#apply-bsp-to-folders-via-properties).<br>Se non specifichi una cartella, il set di immagini o il set 360 gradi generato dal predefinito per set di batch viene creato nella stessa cartella in cui è stata caricata la cartella risorse. |
| **[!UICONTROL Imposta convenzione di denominazione]** |  |
| Prefisso<br>o<br>Suffisso | Facoltativo. Immettere un prefisso, un suffisso o entrambi nei rispettivi campi.<br>I campi prefisso e suffisso consentono di creare molti predefiniti per set di batch utilizzando una convenzione di denominazione file personalizzata alternativa per un particolare set di contenuti. Questo metodo è particolarmente utile nei casi in cui esiste un’eccezione allo schema di denominazione predefinito definito da un’azienda.<br>Il prefisso o il suffisso viene aggiunto al **[!UICONTROL Nome base]** definito nell&#39;area **[!UICONTROL Convenzione di denominazione risorse]**. Aggiungendo un prefisso o un suffisso, assicurati che il set di immagini o il set 360 gradi venga creato in modo esclusivo e indipendente da altre risorse. Può anche essere utile per aiutare altri utenti a identificare i tipi di file. Ad esempio, per determinare una modalità colore utilizzata, è possibile aggiungere come prefisso o suffisso `rgb` o `cmyk`.<br>Sebbene non sia necessario specificare una convenzione per la denominazione dei set per utilizzare la funzionalità dei set di batch predefiniti, è consigliabile utilizzare la convenzione per la denominazione dei set. Questa procedura consente di definire tutti gli elementi della convenzione di denominazione che si desidera raggruppare in un set per semplificare la creazione di set di batch. |
| **[!UICONTROL Risultati regola - RegX]** |  |
| Convenzione di denominazione risorse - Corrispondenza | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni della maschera Corrispondenza selezionate o al codice non elaborato immesso. |
| Convenzione di denominazione risorse - Nome base | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni del modulo Nome base selezionate o al codice non elaborato immesso. |
| Ordinamento sequenza - Corrispondenza | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni di modulo selezionate o al codice non elaborato immesso. |

## Informazioni sull’applicazione di predefiniti per set di batch alle cartelle di risorse {#apply-bsp}

Quando assegnate dei predefiniti per set di batch a una o più cartelle di risorse, tutte le sottocartelle ereditano automaticamente i predefiniti dalla relativa cartella principale.

È possibile applicare più predefiniti set di batch a una cartella di risorse.

Le cartelle a cui è assegnato un predefinito batch sono indicate nell&#39;interfaccia utente con il nome del predefinito visualizzato nella cartella, nella visualizzazione **[!UICONTROL Scheda]**.

Per applicare i predefiniti per set di batch alle cartelle di risorse, utilizza uno dei due metodi seguenti:

* [Applica predefiniti set di batch alle cartelle di risorse dalla pagina Predefinito set di batch](#apply-bsp-to-folders-via-bsp-page) - Questo metodo offre la massima flessibilità. Potete applicare uno o più predefiniti a una o più cartelle.
* [Applica predefiniti set di batch dalla pagina Proprietà di una cartella di risorse](#apply-bsp-to-folders-via-properties). Questo metodo consente di applicare uno o più predefiniti set di batch a una singola cartella.

Come best practice, assicurati che le cartelle di risorse siano sincronizzate [!DNL Dynamic Media], quindi applica i predefiniti desiderati.

Rielabora le risorse in una cartella se si verifica uno dei due scenari seguenti:

* Desideri eseguire un predefinito per set di batch in una cartella di risorse esistente in cui sono già caricate risorse.
* In seguito puoi modificare un predefinito per set di batch esistente precedentemente applicato a una cartella di risorse.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Applicare i predefiniti per set di batch alle cartelle di risorse dalla pagina Predefinito per set di batch {#apply-bsp-to-folders-via-bsp-page}

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionare la casella di controllo di ogni predefinito set di batch che si desidera applicare alle cartelle.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Applica predefinito batch alle cartelle]**.
1. Nella pagina **[!UICONTROL Seleziona cartelle]** selezionare la casella di controllo di ogni cartella a cui si desidera applicare i predefiniti del set di batch.
1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Seleziona cartelle]**, selezionare **[!UICONTROL Applica]**.

### Applicare predefiniti set di batch dalla pagina Proprietà di una cartella di risorse {#apply-bsp-to-folders-via-properties}

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Passare a una cartella in cui si desidera applicare uno o più predefiniti per set di batch.
1. Nella pagina, a sinistra della colonna **[!UICONTROL Name]**, selezionare la casella di controllo di una cartella.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Nella pagina Proprietà della cartella selezionare la scheda **[!UICONTROL Elaborazione elemento multimediale dinamico]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. In **[!UICONTROL Predefiniti set di batch]**, dalla casella di riepilogo a discesa **[!UICONTROL Nome predefinito]**, selezionare il nome di un predefinito set di batch che si desidera applicare. La schermata precedente mostra due predefiniti per set di batch selezionati che vengono applicati alla cartella delle risorse.

   Se nella casella di riepilogo a discesa **[!UICONTROL Nome predefinito]** non sono presenti nomi di predefinito per set di batch, significa che non sono ancora stati creati predefiniti per set di batch. Vedi [Creare un predefinito per set di batch per un set di immagini o un set 360 gradi](#creating-bsp).

   Per rimuovere un predefinito per set di batch applicato, selezionare **[!UICONTROL X]** a destra del tipo di predefinito.

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Salva e chiudi]**.

## Modificare un predefinito per set di batch {#edit-bsp}

È possibile modificare un predefinito per set di batch esistente creato. Puoi modificare qualsiasi gruppo di espressioni creato per la convenzione di denominazione delle risorse o l’ordine di sequenza. Se necessario, puoi anche aggiornare la cartella di destinazione e impostare le convenzioni di denominazione.

Tuttavia, non potete modificare il nome o il tipo di predefinito (Set di immagini o Set 360 gradi). Se è necessario modificare il nome di un predefinito, copiate il predefinito esistente e specificate un nuovo nome. Vedere [Copiare un predefinito per set di batch](#copy-bsp).

Se modifichi un predefinito per set di batch precedentemente applicato a una cartella, il nuovo predefinito per set di batch modificato viene applicato solo alle nuove risorse caricate in tale cartella.

Se desiderate che il predefinito appena modificato venga riapplicato alle risorse esistenti nella cartella, dovete rielaborare la cartella. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->In questo modo, le risorse esistenti diventerebbero parte di un set di immagini o di un set 360 gradi e verrebbero aggiunte. Inoltre, le risorse esistenti già incluse nel set di immagini o nel set 360 gradi, in base al precedente predefinito per set di batch utilizzato, non vengono rimosse e visualizzate così come sono. Questo scenario presuppone che non siano più qualificati in base al predefinito appena modificato.

**Per modificare un predefinito per set di batch:**

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, controllare il predefinito set di batch che si desidera modificare.
1. Nella barra degli strumenti, selezionare **[!UICONTROL Modifica predefinito per set di batch]**.
1. Se necessario, modificate il predefinito.
1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Predefinito set di batch]**, selezionare **[!UICONTROL Salva]**.

## Copiare un predefinito per set di batch esistente {#copy-bsp}

È possibile copiare un predefinito per set di batch esistente per evitare di dover ricreare manualmente un predefinito complesso o se si desidera semplicemente rinominare un predefinito. Non è tuttavia possibile modificare il tipo di predefinito utilizzato (Set di immagini o Set 360 gradi).

Se copi un predefinito esistente a cui fanno riferimento le cartelle di risorse, questo non influisce su tali cartelle.

**Copia un predefinito per set di batch esistente:**

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionare la casella di controllo del predefinito set di batch da copiare.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Copia]**.
1. Nella finestra di dialogo **[!UICONTROL Copia predefinito per set di batch]** digitare un nuovo nome per il predefinito nella casella di testo **[!UICONTROL Titolo]**.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Seleziona **[!UICONTROL Copia]**.

## Informazioni sulla rimozione di predefiniti set di batch dalle cartelle {#remove-bsp-from-folder}

Quando rimuovi i predefiniti set di batch dalle cartelle, a tutte le nuove risorse caricate in queste cartelle non viene applicato il predefinito set di batch. Le risorse esistenti nella cartella già aggiunte al set di immagini o al set 360 gradi in base al predefinito per set di batch applicato alla cartella continuano a essere visualizzate così come sono.

Se invece desideri *eliminare* predefiniti dalle cartelle, consulta [Eliminare predefiniti set di batch](#delete-bsp).

Esistono due metodi per rimuovere i predefiniti per set di batch dalle cartelle.

* [Rimuovere i predefiniti set di batch dalle cartelle tramite la pagina Predefinito set di batch](#remove-bsp-from-folders-via-bsp-page). Questo metodo offre la massima flessibilità. È possibile rimuovere uno o più predefiniti da una o più cartelle.
* [Rimuovi predefiniti set di batch dalla pagina Proprietà di una cartella](#remove-bsp-from-folders-via-properties) - Questo metodo consente di rimuovere uno o più predefiniti set di batch solo da una singola cartella.

### Rimuovere i predefiniti set di batch dalle cartelle tramite la pagina Predefinito set di batch {#remove-bsp-from-folders-via-bsp-page}

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionare la casella di controllo di uno o più predefiniti set di batch da rimuovere da una o più cartelle.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Rimuovi predefinito batch da cartelle]**.

1. Nella pagina **[!UICONTROL Seleziona cartelle]** selezionare una o più cartelle in cui si desidera rimuovere i predefiniti del set di batch.
1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Seleziona cartelle]**, selezionare **[!UICONTROL Rimuovi]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. Nella finestra di dialogo **[!UICONTROL Rimuovi profilo]** selezionare **[!UICONTROL Rimuovi]**.

### Rimuovere i predefiniti per set di batch dalla pagina Proprietà di una cartella {#remove-bsp-from-folders-via-properties}

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Passare a una cartella in cui si desidera rimuovere uno o più predefiniti per set di batch.
1. Nella pagina, a sinistra della colonna **[!UICONTROL Name]**, selezionare la casella di controllo di una cartella.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Nella pagina Proprietà della cartella selezionare **[!UICONTROL Elaborazione elemento multimediale dinamico]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. In **[!UICONTROL Predefiniti set di batch]**, selezionare **[!UICONTROL X]** a destra del tipo di predefinito.

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Salva e chiudi]**.

## Elimina predefiniti set di batch {#delete-bsp}

È possibile eliminare i predefiniti set di batch per rimuoverli definitivamente da [!DNL Dynamic Media]. In altre parole, non vengono più visualizzati nella pagina [!UICONTROL Predefinito set di batch] né nell&#39;elenco a discesa **[!UICONTROL Predefiniti set di batch]** della scheda **[!UICONTROL Elaborazione elementi multimediali dinamici]** nella pagina **[!UICONTROL Proprietà]** della cartella. Di conseguenza, il predefinito non viene applicato alle risorse esistenti durante la rielaborazione di una cartella o quando vengono caricate nuove risorse nella cartella.

Se elimini un predefinito applicato in precedenza a una o più cartelle, tutti i set di immagini o i set 360 gradi creati dalle risorse in tali cartelle continuano a essere visualizzati così come sono.

Se invece desideri *rimuovere* predefiniti dalle cartelle, consulta [Rimuovere i predefiniti dei set di batch dalle cartelle](#remove-bsp-from-folder).

**Per eliminare i predefiniti del set di batch:**

1. Seleziona il logo Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionare la casella di controllo di uno o più predefiniti set di batch da eliminare.
1. Nella barra degli strumenti, selezionare **[!UICONTROL Elimina predefiniti set di batch]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. Nella finestra di dialogo **[!UICONTROL Elimina predefiniti set di batch]**, seleziona **[!UICONTROL Elimina]**.

   Se il predefinito che stai eliminando è stato oggetto di riferimento da una cartella di risorse, seleziona **[!UICONTROL Forza eliminazione]**.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Set di immagini](/help/assets/dynamic-media/image-sets.md)
>* [Set 360 gradi](/help/assets/dynamic-media/spin-sets.md)
>* [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder). Per ulteriori informazioni sulla sincronizzazione di una singola cartella in [!DNL Dynamic Media], vedere &quot;Modalità di sincronizzazione&quot; nell&#39;argomento.
>* [Creare una configurazione Dynamic Media in Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services). Per ulteriori informazioni sulla sincronizzazione di tutte le cartelle in [!DNL Dynamic Media], vedere &quot;Modalità di sincronizzazione Dynamic Media&quot; nell&#39;argomento.
