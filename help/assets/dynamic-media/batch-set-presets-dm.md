---
title: Predefiniti set di batch
description: Informazioni su come automatizzare la creazione di set di immagini e set 360 gradi utilizzando i set di batch predefiniti in Dynamic Media.
contentOwner: Rick Brough
feature: Predefiniti immagine,Predefiniti visualizzatore
topic: Professionista
role: Business Practitioner
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '3446'
ht-degree: 1%

---

# Informazioni sui predefiniti per set di batch {#about-bsp}

Utilizza **[!UICONTROL Predefiniti set di batch]** per creare e organizzare più risorse in un set di immagini o in un set 360 gradi al momento del caricamento dei file di risorse in una cartella singolarmente o tramite l’acquisizione in massa. Puoi far eseguire il predefinito insieme ai lavori di importazione delle risorse programmati in [!DNL Dynamic Media]. Ogni predefinito è un set di istruzioni autonomo con un nome univoco che definisce come creare il set di immagini o il set 360 gradi utilizzando immagini che corrispondono alle convenzioni di denominazione definite nella ricetta preimpostata.

>[!IMPORTANT]
>
>Se in [!DNL Dynamic Media Classic] hai utilizzato i predefiniti per set di batch e stai eseguendo la migrazione da [!DNL Dynamic Media Classic] a Adobe Experience Manager come Cloud Service, ricrea manualmente le definizioni dei predefiniti per set di batch all’interno di [!DNL Adobe Experience Manager as a Cloud Service].

**Procedure consigliate** : quando si lavora con i predefiniti per set di batch, l’Adobe consiglia il seguente flusso di lavoro:

1. Crea un predefinito per set di batch. Consulta [Creazione di un set di batch predefinito per un set di immagini o un set 360 gradi](#creating-bsp).
1. Crea una cartella di risorse o utilizza una cartella di risorse esistente e assicurati che sia sincronizzata in [!DNL Dynamic Media]. Vedere [Creazione di cartelle](/help/assets/manage-digital-assets.md#creating-folders).
1. Applica il Batch Set Preset alla cartella delle risorse. Consulta [Informazioni sull&#39;applicazione di predefiniti per set di batch alle cartelle](#apply-bsp).
1. Carica le immagini nella cartella delle risorse. Consulta [Caricamento delle risorse per i set di immagini](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Caricamento delle risorse per i set 360 gradi](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) o [Aggiungi risorse digitali a Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. Il set di immagini o il set 360 gradi viene generato automaticamente nella cartella desiderata.
1. Pubblica il set di immagini o il set 360 gradi. Consulta [Pubblicazione di risorse Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Creazione di un predefinito per set di batch per un set di immagini o un set 360 gradi {#creating-bsp}

Per creare predefiniti per set di batch, è consigliabile avere familiarità e comprensione delle espressioni regolari.

Idealmente, l’azienda ha già definito una convenzione di denominazione per il modo in cui le risorse vengono raggruppate in un set.
Per comprendere l’importanza dell’utilizzo di una convenzione per i nomi, supponiamo che la convenzione per i nomi definita dalla tua azienda sia `<style>-<color>-<view>`. Inoltre, il nome di base del set deve sempre essere `<style>-<color>` e l&#39;estensione del nome del set deve essere `-SET`. Se carichi un’immagine denominata `0123-RED-01`, viene creato un set denominato `0123-RED-SET`. Se in seguito carichi le immagini `0123-RED-03` e `0123-BLUE-01`, l&#39;immagine `RED-03` verrà aggiunta al set nella seconda posizione perché è ordinata in modo inferiore a `01`. Tuttavia, l&#39;immagine `BLUE-01` fa parte di un nuovo set denominato `0123-BLUE-SET`. Per il caricamento successivo delle risorse, aggiungi i file `0123-RED-02` e `0123-BLUE-02`. Ogni attività verrebbe aggiunta al rispettivo insieme. L&#39;immagine `RED-02` viene ordinata automaticamente tra le immagini `01` e `03` esistenti, in base all&#39;ordinamento.

La pagina **[!UICONTROL Preimpostazione set di batch]** in [!DNL Dynamic Media] consente di creare, modificare o eliminare i predefiniti set di batch e di applicare o rimuovere i predefiniti set di batch da o verso le cartelle di risorse. È possibile utilizzare gli elenchi a discesa dei campi modulo per definire un Batch Set Preset oppure il campo **[!UICONTROL Codice non elaborato]**, che consente di digitare la sintassi delle espressioni regolari.

Puoi creare tutti i predefiniti per set di batch necessari per coprire tutti i processi di acquisizione delle risorse necessari.

**Informazioni sulla convenzione per la denominazione delle risorse**

L&#39;area **[!UICONTROL Convenzione per la denominazione delle risorse]** nella pagina **[!UICONTROL Preimpostazione set di batch]** dispone di due elementi che è possibile utilizzare per definire il predefinito del set di batch: **[!UICONTROL Corrispondenza]** e **[!UICONTROL Nome base]**. Questi elementi consentono di definire una convenzione di denominazione e identificare la parte della convenzione utilizzata per denominare il set in cui sono contenuti. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convenzione di denominazione individuale di un’azienda utilizza spesso una o più righe di definizione di ciascuno di questi due elementi. Puoi utilizzare altrettante righe per la definizione univoca e raggrupparle in elementi distinti, ad esempio per l’immagine principale, l’elemento Colore, l’elemento Vista alternativa e l’elemento Campione.

Ad esempio, la sintassi per un&#39;espressione regolare di corrispondenza letterale potrebbe essere simile alla seguente:

`(\w+)-\w+-\w+`

**Informazioni sull’ordinamento delle sequenze**

Facoltativamente, puoi definire l’ordine in cui vengono visualizzate le immagini dopo il raggruppamento del set di immagini o del set 360 gradi in [!DNL Dynamic Media]. Per impostazione predefinita, le risorse vengono ordinate in modo alfanumerico. Tuttavia, per definire l’ordine è possibile utilizzare un elenco di espressioni regolari separate da virgola.

Per quanto riguarda l’automazione dell’ordinamento a sequenza, è necessario specificare le regole per forzare l’ordinamento delle risorse in un determinato modo, se necessario. Ad esempio, supponiamo che la prima risorsa sia sempre denominata `_main` e che sia seguita da `_alt1`, `_alt2`, `_alt3` e così via. In questi casi, puoi creare una regola di ordinamento della sequenza con la seguente sintassi:

`.*_main,.*_alt[0-9]`

Mentre è possibile ordinare una sequenza di forza, è meglio fare affidamento, per quanto possibile, sulla numerazione alfanumerica. Inoltre, è possibile utilizzare gli strumenti editor set di immagini o set 360 gradi in [!DNL Dynamic Media] per ridisporre l’ordine di sequenza delle risorse, oppure aggiungere ed eliminare nuove risorse nel set mediante un’operazione di trascinamento della selezione.

Al termine della creazione di un predefinito per set di batch, lo si applica a una o più cartelle create. Consulta [Informazioni sull&#39;applicazione di predefiniti per set di batch alle cartelle](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Per creare un predefinito per set di batch per un set di immagini o un set 360 gradi:**

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti set di batch]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, nell’angolo in alto a destra, tocca **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea predefinito set di batch]**, immettere un nome descrittivo nel campo di testo **[!UICONTROL Nome predefinito]**. Il nome del predefinito non può essere modificato se successivamente decidi di modificarlo.

1. Nell’elenco a discesa **[!UICONTROL Tipo predefinito]** , seleziona **[!UICONTROL Set immagini]** o **[!UICONTROL Set 360 gradi]**. Assicurati di scegliere il tipo di predefinito corretto; non è modificabile in un secondo momento.
1. Tocca **[!UICONTROL Crea]**.
1. A destra della pagina **[!UICONTROL Modifica predefinito set di batch]**, imposta le opzioni modificabili desiderate nelle intestazioni **[!UICONTROL Dettagli predefiniti]** e **[!UICONTROL Imposta convenzione di denominazione]** .
Per ulteriori informazioni sulle opzioni modificabili disponibili, consulta [Dettagli predefiniti, Imposta convenzione di denominazione e Risultati regola - Opzioni RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Crea uno o più gruppi di espressioni regolari.

   * A sinistra della pagina **[!UICONTROL Modifica predefinito set di batch]**, in **[!UICONTROL Corrispondenza]**, **[!UICONTROL Nome base]** o **[!UICONTROL Ordinamento sequenza]**, tocca **[!UICONTROL Aggiungi gruppo]**.
   * Il campo **[!UICONTROL Match]** è obbligatorio. **[!UICONTROL Il]** nome di base è obbligatorio solo se il campo  **** Matchfield non specifica già un nome di base utilizzando un raggruppamento di parentesi. **[!UICONTROL L’]** Ordine Sequenza è facoltativo.
   * Utilizzando gli elenchi a discesa e le caselle di testo nel modulo del gruppo, specificate un gruppo di espressioni da utilizzare per definire i criteri di denominazione per i membri del set di immagini o del set 360 gradi.
      * Quando selezioni e specifichi le espressioni per un gruppo, osserva che la sintassi dell&#39;espressione regolare effettiva si riflette in basso a destra della pagina, sotto l&#39;intestazione **[!UICONTROL Risultati regola - RegX]** . Per visualizzare la stringa di espressione regolare aggiornata in basso a destra, tocca un punto qualsiasi all’esterno dell’area del modulo. Queste stringhe di espressione regolare rappresentano il pattern a cui si desidera associare una ricerca di [!DNL Dynamic Media] risorse per creare il set di immagini o il set 360 gradi.
      * Per rimuovere un gruppo aggiunto, tocca **[!UICONTROL X]**.
   * Quando si aggiungono due o più gruppi, nell&#39;elenco a discesa **[!UICONTROL And]**, selezionare **[!UICONTROL And]** per unire un gruppo appena aggiunto con qualsiasi gruppo di espressioni precedente aggiunto. In alternativa, selezionare **[!UICONTROL O]** per aggiungere un&#39;alternanza tra il gruppo di espressioni precedente e il nuovo gruppo creato. L&#39;operando **[!UICONTROL Or]** è definito dall&#39;uso di un carattere di riga verticale `|` nella sintassi dell&#39;espressione regolare stessa.

1. Effettua una delle operazioni seguenti:

   * Per aggiungere un altro nuovo gruppo, in **[!UICONTROL Match]**, **[!UICONTROL Base Name]** o **[!UICONTROL Sequencing Order]**, tocca **[!UICONTROL Aggiungi gruppo]**. Crea un altro gruppo di espressioni regolari come nel passaggio precedente.
   * Controlla la sintassi delle espressioni regolari nell&#39;area **[!UICONTROL Risultati regola - RegX]** . Se devi modificare la sintassi, apporta le modifiche nel rispettivo gruppo a sinistra della pagina.
   * Se hai finito di creare gruppi di espressioni, continua con il passaggio successivo.

1. Nell’angolo in alto a destro della pagina, tocca **[!UICONTROL Salva]**.

Ora puoi applicare il Batch Set Preset a una cartella di risorse. Quindi, carica le risorse in quella cartella. Questo flusso di lavoro genera automaticamente il set di immagini o il set 360 gradi. Consulta [Informazioni sull&#39;applicazione di predefiniti per set di batch alle cartelle di risorse](#apply-bsp).

### Dettagli predefiniti, Imposta convenzione di denominazione e risultati regola - Opzioni RegX {#features-options-bsp}

Queste opzioni sono disponibili nella pagina **[!UICONTROL Edit Batch Set Preset]** quando crei o modifichi un Batch Set Preset.

Consulta [Creazione di un Batch Set Preset per un set di immagini o un set 360 gradi](#creating-bsp) o [Modifica di un Batch Set Preset](#edit-bsp).

| **[!UICONTROL Dettagli del predefinito]** | Descrizione |
| --- | --- |
| Nome predefinito | Sola lettura. Nome specificato al momento della creazione del set di batch. Se è necessario rinominare il predefinito, è possibile copiare il Batch Set Preset esistente e specificare un nuovo nome. Consulta [Copia di un Batch Set Preset esistente](#copy-bsp). |
| Tipo | Sola lettura. Il tipo è stato specificato al momento della creazione del set di batch. La copia di un Batch Set Preset esistente non consente di modificarne il [!UICONTROL Type]; devi invece creare un predefinito. |
| Includi risorse derivate | Facoltativo. Per fare in modo che l’IPS di [!DNL Dynamic Media] (Image Production System) includa immagini generate o &quot;derivate&quot; con il set 360 gradi o il set di immagini, seleziona **[!UICONTROL Sì]** (impostazione predefinita). Una risorsa derivata è un’immagine che non è stata caricata direttamente da un utente. Al contrario, la risorsa è stata prodotta da IPS al momento del caricamento di una risorsa principale. Ad esempio, una risorsa immagine generata da IPS da una pagina in un PDF, al momento del caricamento del PDF in [!DNL Dynamic Media], è considerata una risorsa derivata. |
| Cartella di destinazione | Facoltativo. Se definisci un numero elevato di set di immagini o set 360 gradi, Adobe consiglia di mantenere questi set separati dalle cartelle contenenti le risorse stesse. È quindi consigliabile creare una cartella Set immagini o Set 360 gradi e reindirizzare l’applicazione in modo che inserisca qui i set generati da set di batch.<br>In questo caso, specifica quale cartella della struttura di cartelle Risorse di Experience Manager (`/content/dam`) dispone del Batch Set Preset attivo. Assicurati che la cartella sia abilitata per la sincronizzazione [!DNL Dynamic Media] per consentirne la creazione come cartella di destinazione. Consulta [Configurazione della pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>A più cartelle può essere assegnato un set di batch specifico, se lo si applica tramite  **[!UICONTROL Proprietà]** della cartella. Consulta [Applicazione dei predefiniti per set di batch dalla pagina Proprietà di una cartella di risorse](#apply-bsp-to-folders-via-properties).<br>Se non si specifica una cartella, il set di immagini o il set 360 gradi predefiniti per set di batch generato viene creato nella stessa cartella della cartella di risorse in cui è stato caricato. |
| **[!UICONTROL Imposta convenzione di denominazione]** |  |
| Prefisso<br>o<br>Suffisso | Facoltativo. Immettere un prefisso, un suffisso o entrambi nei rispettivi campi.<br>I campi prefisso e suffisso consentono di creare un numero illimitato di predefiniti per set di batch utilizzando una convenzione di denominazione file alternativa personalizzata per un determinato set di contenuti. Questo metodo è particolarmente utile nei casi in cui vi sia un&#39;eccezione allo schema di denominazione predefinito definito da un&#39;azienda.<br>Il prefisso o il suffisso viene aggiunto al nome  **[!UICONTROL base definito nell’]** area della  **[!UICONTROL convenzione per la denominazione delle]** risorse. Aggiungendo un prefisso o un suffisso, accertati che il set di immagini o il set 360 gradi venga creato esclusivamente e indipendentemente da altre risorse. Può inoltre essere utile per aiutare altri a identificare i tipi di file. Ad esempio, per determinare la modalità colore utilizzata, è possibile aggiungere come prefisso o suffisso `rgb` o `cmyk`.<br>Per utilizzare le funzionalità preimpostate per i set di batch, non è necessario specificare una convenzione di denominazione impostata, ma è consigliabile utilizzare tale convenzione. Questa procedura consente di definire tutti gli elementi della convenzione di denominazione che si desidera raggruppare in un set per semplificare la creazione di set di batch. |
| **[!UICONTROL Risultati regola - RegX]** |  |
| Convenzione per la denominazione delle risorse - Corrispondenza | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni del modulo Match selezionate o al codice non elaborato immesso. |
| Convenzione per la denominazione delle risorse - Nome base | Sola lettura. Visualizza la sintassi dell&#39;espressione regolare in base alle opzioni del modulo Nome base selezionate o al codice non elaborato immesso. |
| Ordine sequenza - Corrispondenza | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni del modulo selezionate o al codice non elaborato immesso. |

## Informazioni sull’applicazione di predefiniti per set di batch alle cartelle di risorse {#apply-bsp}

Quando assegni predefiniti per set di batch a una o più cartelle di risorse, tutte le sottocartelle ereditano automaticamente i predefiniti dalla relativa cartella padre.

Puoi applicare più predefiniti per set di batch a una cartella di risorse.

Le cartelle a cui è stato assegnato un Batch Preset sono indicate nell&#39;interfaccia utente con il nome del Predefinito che appare nella cartella, nella vista **[!UICONTROL Scheda]**.

Per applicare i predefiniti per set di batch alle cartelle di risorse, utilizza uno dei due metodi seguenti:

* [Applica i predefiniti per set di batch alle cartelle di risorse dalla pagina](#apply-bsp-to-folders-via-bsp-page)  Predefinito set di batch : questo metodo offre la massima flessibilità. Puoi applicare uno o più predefiniti a una o più cartelle.
* [Applica i predefiniti per set di batch dalla pagina](#apply-bsp-to-folders-via-properties)  Proprietà di una cartella di risorse. Questo metodo consente di applicare uno o più predefiniti per set di batch a una singola cartella.

Come best practice, accertati che le cartelle di risorse siano sincronizzate [!DNL Dynamic Media], quindi applica i predefiniti desiderati.

Rielabora le risorse in una cartella se si verifica uno dei due scenari seguenti:

* Desideri eseguire un Batch Set Preset su una cartella di risorse esistente in cui sono già state caricate delle risorse.
* Successivamente puoi modificare un predefinito per set di batch esistente precedentemente applicato a una cartella di risorse.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Applicazione dei predefiniti per set di batch alle cartelle di risorse dalla pagina Predefinito set di batch {#apply-bsp-to-folders-via-bsp-page}

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, seleziona la casella di controllo di ciascun predefinito set di batch che desideri applicare alle cartelle.
1. Nella barra degli strumenti, tocca **[!UICONTROL Applica predefinito batch alle cartelle]**.
1. Nella pagina **[!UICONTROL Seleziona cartelle]**, selezionare la casella di controllo di ciascuna cartella a cui si desidera applicare i predefiniti per set di batch.
1. Nell&#39;angolo in alto a destra della pagina **[!UICONTROL Seleziona cartelle]**, tocca **[!UICONTROL Applica]**.

### Applicazione dei predefiniti per set di batch dalla pagina Proprietà di una cartella di risorse {#apply-bsp-to-folders-via-properties}

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa a una cartella alla quale desideri applicare uno o più predefiniti per set di batch.
1. Nella pagina, a sinistra della colonna **[!UICONTROL Nome]**, selezionare la casella di controllo di una cartella.
1. Nella barra degli strumenti, tocca **[!UICONTROL Proprietà]**.
1. Nella pagina Proprietà della cartella, tocca la scheda **[!UICONTROL Elaborazione Dynamic Media]** .

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. In **[!UICONTROL Predefiniti set di batch]**, dall&#39;elenco a discesa **[!UICONTROL Nome predefinito]**, selezionare il nome di un predefinito set di batch da applicare. La schermata precedente mostra due predefiniti set di batch selezionati applicati alla cartella delle risorse.

   Se nella casella di riepilogo a discesa **[!UICONTROL Nome predefinito]** non sono presenti nomi predefiniti per set di batch, significa che non è stato ancora creato alcun predefinito per set di batch. Consulta [Creazione di un set di batch predefinito per un set di immagini o un set 360 gradi](#creating-bsp).

   Per rimuovere un Batch Set Preset applicato, toccare **[!UICONTROL X]** a destra del tipo di predefinito.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva e chiudi]**.

## Modifica di un predefinito per set di batch {#edit-bsp}

Puoi modificare un predefinito per set di batch esistente creato. Puoi modificare uno qualsiasi dei gruppi di espressioni creati per la convenzione di denominazione delle risorse o l’ordine di sequenza. Se necessario, puoi anche aggiornare la cartella di destinazione e impostare le convenzioni di denominazione.

Tuttavia, non è possibile modificare il nome o il tipo di predefinito del predefinito (set di immagini o set 360 gradi). Se risulta necessario modificare il nome di un predefinito, copia il predefinito esistente e specifica un nuovo nome. Consulta [Copia di un Batch Set Preset](#copy-bsp).

Se modifichi un predefinito per set di batch precedentemente applicato a una cartella, il nuovo predefinito per set di batch modificato viene applicato solo alle nuove risorse caricate in tale cartella.

Se desideri che il nuovo predefinito modificato venga nuovamente applicato alle risorse esistenti nella cartella, devi rielaborare la cartella. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->In questo modo, le risorse esistenti ora si qualificano come parte di un set di immagini o di un set 360 gradi e vengono aggiunte. Inoltre, le risorse esistenti che erano già incluse nel set di immagini o nel set 360 gradi - in base al precedente Batch Set Preset utilizzato - non vengono rimosse e mostrano così come sono. Questo scenario presuppone che non si qualifichino più in base al nuovo predefinito modificato.

**Per modificare un predefinito per set di batch:**

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, seleziona il predefinito set di batch da modificare.
1. Nella barra degli strumenti, tocca **[!UICONTROL Modifica predefinito set di batch]**.
1. Se necessario, modifica il predefinito.
1. Nell&#39;angolo in alto a destra della pagina **[!UICONTROL Preimpostazione set di batch]**, tocca **[!UICONTROL Salva]**.

## Copia di un Batch Set Preset esistente {#copy-bsp}

È possibile copiare un predefinito per set di batch esistente per evitare di dover ricreare manualmente un predefinito complesso o se si desidera semplicemente rinominare un predefinito. Non è tuttavia possibile modificare il tipo di predefinito utilizzato (Set immagini o Set 360 gradi).

Se copi un predefinito esistente a cui fanno riferimento le cartelle di risorse, queste cartelle non saranno influenzate.

**Per copiare un Batch Set Preset esistente:**

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, seleziona la casella di controllo del predefinito set di batch da copiare.
1. Nella barra degli strumenti, tocca **[!UICONTROL Copia]**.
1. Nella finestra di dialogo **[!UICONTROL Copia predefinito set di batch]**, digitare un nuovo nome per il predefinito nella casella di testo **[!UICONTROL Titolo]**.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Tocca **[!UICONTROL Copia]**.

## Informazioni sulla rimozione dei predefiniti per set di batch dalle cartelle {#remove-bsp-from-folder}

Quando rimuovi i predefiniti per set di batch dalle cartelle, a tutte le nuove risorse caricate in queste cartelle non viene applicato il set di batch predefinito. Le risorse esistenti nella cartella che erano già state aggiunte al set di immagini o al set di valori per la rotazione in base al Batch Set Preset applicato alla cartella continuano a essere visualizzate così com’è.

Se invece desideri *eliminare* i predefiniti dalle cartelle, consulta [Eliminazione dei predefiniti per set di batch](#delete-bsp).

Esistono due metodi per rimuovere i predefiniti per set di batch dalle cartelle.

* [Rimozione dei predefiniti per set di batch dalle cartelle tramite la pagina](#remove-bsp-from-folders-via-bsp-page)  Batch Set Preset : questo metodo offre la massima flessibilità. È possibile rimuovere uno o più predefiniti da una o più cartelle.
* [Rimozione dei predefiniti per set di batch dalla pagina](#remove-bsp-from-folders-via-properties)  Proprietà di una cartella. Questo metodo consente di rimuovere uno o più predefiniti per set di batch da una sola cartella.

### Rimozione dei predefiniti per set di batch dalle cartelle tramite la pagina Predefiniti set di batch {#remove-bsp-from-folders-via-bsp-page}

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionare la casella di controllo di uno o più predefiniti set di batch che si desidera rimuovere da una o più cartelle.
1. Nella barra degli strumenti, tocca **[!UICONTROL Rimuovi predefinito batch da cartelle]**.

1. Nella pagina **[!UICONTROL Seleziona cartelle]** , seleziona una o più cartelle in cui vuoi rimuovere i predefiniti per set di batch.
1. Nell&#39;angolo in alto a destra della pagina **[!UICONTROL Seleziona cartelle]**, tocca **[!UICONTROL Rimuovi]**.

   ![bsp-remove-from-Folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. Nella finestra di dialogo **[!UICONTROL Rimuovi profilo]**, tocca **[!UICONTROL Rimuovi]**.

### Rimozione dei predefiniti per set di batch dalla pagina Proprietà di una cartella {#remove-bsp-from-folders-via-properties}

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa alla cartella in cui desideri rimuovere uno o più predefiniti per set di batch.
1. Nella pagina, a sinistra della colonna **[!UICONTROL Nome]**, selezionare la casella di controllo di una cartella.
1. Nella barra degli strumenti, tocca **[!UICONTROL Proprietà]**.
1. Nella pagina Proprietà della cartella, tocca **[!UICONTROL Dynamic Media Processing]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. In **[!UICONTROL Predefiniti set di batch]**, tocca **[!UICONTROL X]** a destra del tipo di predefinito.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva e chiudi]**.

## Eliminazione dei predefiniti per set di batch {#delete-bsp}

È possibile eliminare i predefiniti per set di batch per rimuoverli definitivamente da [!DNL Dynamic Media]. In altre parole, non vengono più visualizzati nella pagina [!UICONTROL Preimpostazione set di batch] né nell&#39;elenco a discesa **[!UICONTROL Predefiniti set di batch]** della scheda **[!UICONTROL Elaborazione Dynamic Media]** nella pagina **[!UICONTROL Proprietà]** della cartella. Di conseguenza, il predefinito non viene applicato alle risorse esistenti in una rielaborazione delle cartelle o quando nuove risorse vengono caricate nella cartella.

Se elimini un predefinito precedentemente applicato a una o più cartelle, tutti i set di immagini o i set 360 gradi creati dalle risorse di tali cartelle continueranno a essere visualizzati così com’è.

Se invece desideri *rimuovere* i predefiniti dalle cartelle, consulta [Rimozione dei predefiniti per set di batch dalle cartelle](#remove-bsp-from-folder).

**Per eliminare i predefiniti per set di batch:**

1. Tocca il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, seleziona la casella di controllo di uno o più predefiniti set di batch da eliminare.
1. Nella barra degli strumenti, tocca **[!UICONTROL Elimina predefiniti set di batch]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. Nella finestra di dialogo **[!UICONTROL Elimina predefiniti set di batch]**, tocca **[!UICONTROL Elimina]**.

   Se una cartella di risorse contiene un riferimento al predefinito che stai eliminando, tocca **[!UICONTROL Forza eliminazione]**.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Set di immagini](/help/assets/dynamic-media/image-sets.md)
>* [Set 360 gradi](/help/assets/dynamic-media/spin-sets.md)
>* [Configurazione della pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  - Per ulteriori informazioni sulla sincronizzazione di una singola cartella in  [!DNL Dynamic Media], consulta &quot;Modalità di sincronizzazione&quot; nell’argomento.
>* [Creazione di una configurazione Dynamic Media nei Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  - Per ulteriori informazioni sulla sincronizzazione di tutte le cartelle in  [!DNL Dynamic Media], consulta &quot;Modalità di sincronizzazione Dynamic Media&quot; nell’argomento.

