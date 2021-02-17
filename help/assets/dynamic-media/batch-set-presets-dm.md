---
title: Predefiniti set di batch
description: Scoprite come automatizzare la creazione di set di immagini e set 360 gradi utilizzando i predefiniti per set di batch in Dynamic Media.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: 5a50226bfae12440d07f9a21233ea06e118addac
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 1%

---


# I predefiniti per set di batch {#about-bsp}

Utilizzate **[!UICONTROL Predefiniti per set di batch]** per semplificare la creazione e l’organizzazione di più risorse in un set di immagini o set 360 gradi al momento di caricare i file di risorse in una cartella singolarmente o utilizzando l’assimilazione in blocco. Potete fare in modo che il predefinito venga eseguito insieme ai processi di importazione delle risorse programmati in [!DNL Dynamic Media]. Ogni predefinito ha un nome univoco e contiene un set autonomo di istruzioni che definisce come creare il set di immagini o il set 360 gradi utilizzando immagini che corrispondono alle convenzioni di denominazione definite nella definizione del predefinito.

>[!IMPORTANT]
>
>Se avete usato i predefiniti per set di batch in [!DNL Dynamic Media Classic] e state eseguendo la migrazione da [!DNL Dynamic Media Classic] ad Adobe Experience Manager come Cloud Service, dovete ricreare manualmente le definizioni dei predefiniti per set di batch all&#39;interno di [!DNL Adobe Experience Manager as a Cloud Service].

**Procedure**  ottimali: quando si utilizzano i predefiniti per set di batch,  Adobe consiglia il seguente flusso di lavoro:

1. Create un predefinito per set di batch. Consultate [Creazione di un predefinito per set di batch per un set di immagini o un set 360 gradi](#creating-bsp).
1. Create una cartella di risorse o usate una cartella di risorse esistente e assicuratevi che sia sincronizzata su [!DNL Dynamic Media]. Vedere [Creazione di cartelle](/help/assets/manage-digital-assets.md#creating-folders).
1. Applicate il predefinito per set di batch alla cartella delle risorse. Consultate [L&#39;applicazione dei predefiniti per set di batch alle cartelle](#apply-bsp).
1. Caricate le immagini nella cartella delle risorse. Consultate [Caricamento di risorse per set di immagini](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Caricamento di risorse per set 360 gradi](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) o [Aggiunta di risorse digitali a Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. Create il set di immagini o il set 360 gradi. Consultate [Set di immagini](/help/assets/dynamic-media/image-sets.md) o [Set 360 gradi](/help/assets/dynamic-media/spin-sets.md).
1. Pubblicate il set di immagini o il set 360 gradi. Consultate [Pubblicazione di Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Creazione di un predefinito per set di batch per un set di immagini o un set 360 gradi {#creating-bsp}

Per creare i predefiniti per set di batch, è consigliabile acquisire familiarità e familiarità con le espressioni regolari.

Idealmente, la società ha già definito una convenzione di denominazione per il raggruppamento delle risorse in un set.
Per agevolare la comprensione dell&#39;importanza dell&#39;utilizzo di una convenzione di denominazione, supponete che la convenzione di denominazione definita dalla società sia `<style>-<color>-<view>`. Inoltre, il nome di base del set deve sempre essere `<style>-<color>` e l&#39;estensione del nome del set deve essere `-SET`. Se caricate un&#39;immagine denominata `0123-RED-01`, verrà creato un set denominato `0123-RED-SET`. Se successivamente caricate le immagini `0123-RED-03` e `0123-BLUE-01`, l&#39;immagine `RED-03` verrà aggiunta al set nella seconda posizione, perché è ordinata in modo inferiore a `01`. Tuttavia, l&#39;immagine `BLUE-01` fa parte di un nuovo set denominato `0123-BLUE-SET`. Per il caricamento successivo delle risorse, aggiungete i file `0123-RED-02` e `0123-BLUE-02`. Ogni risorsa viene aggiunta al relativo set. L&#39;immagine `RED-02` viene ordinata automaticamente tra le immagini `01` e `03` esistenti, in base all&#39;ordine di ordinamento.

La pagina **[!UICONTROL Predefinito set di batch]** in [!DNL Dynamic Media] consente di creare, modificare o eliminare i predefiniti per set di batch e di applicare o rimuovere i predefiniti per set di batch da o verso le cartelle delle risorse. È possibile utilizzare gli elenchi a discesa dei campi modulo per definire un predefinito per set di batch oppure il campo **[!UICONTROL Codice non elaborato]**, che consente di digitare la sintassi delle espressioni regolari.

Potete creare tutti i predefiniti per set di batch necessari per tutti i processi di caricamento delle risorse.

**Convenzione sulla denominazione delle risorse**

L&#39;area **[!UICONTROL Convenzioni di denominazione delle risorse]** nella pagina **[!UICONTROL Predefinito set di batch]** include due elementi che potete usare per definire il predefinito per set di batch: **[!UICONTROL Corrispondenza]** e **[!UICONTROL Nome base]**. Questi elementi consentono di definire una convenzione di denominazione e identificare la parte della convenzione utilizzata per denominare il set in cui sono contenuti. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convenzione di denominazione individuale di una società utilizza spesso una o più righe di definizione di ciascuno di questi due elementi. Potete usare tutte le righe necessarie per creare una definizione univoca e raggrupparle in elementi distinti, ad esempio per l’immagine principale, l’elemento colore, l’elemento visualizzazione alternativa e l’elemento campione.

Ad esempio, la sintassi di un&#39;espressione regolare letterale corrispondente potrebbe essere simile a quella riportata di seguito:

`(\w+)-\w+-\w+`

**Informazioni sull&#39;ordine delle sequenze**

Facoltativamente, potete definire l’ordine in cui le immagini vengono visualizzate dopo che il set di immagini o il set 360 gradi è stato raggruppato in [!DNL Dynamic Media]. Per impostazione predefinita, le risorse sono ordinate in ordine alfabetico. Tuttavia, potete definire l’ordine utilizzando un elenco separato da virgole di espressioni regolari.

Per quanto riguarda l’automazione degli ordini di sequenza, specificate le regole per imporre l’ordinamento delle risorse in un determinato modo, se necessario. Ad esempio, supponiamo che la prima risorsa sia sempre denominata `_main` e che sia seguita da `_alt1`, `_alt2`, `_alt3` e così via. In questi casi, potete creare una regola di ordinamento della sequenza con la sintassi seguente:

`.*_main,.*_alt[0-9]`

Anche se è possibile ordinare una sequenza di forza, è consigliabile utilizzare la numerazione alfanumerica per ordinare la sequenza, per quanto possibile. Inoltre, potete usare gli strumenti per l’editor di set di immagini o set 360 gradi in [!DNL Dynamic Media] per riordinare facilmente l’ordine di sequenza delle risorse, oppure aggiungere ed eliminare nuove risorse nel set mediante un’operazione di trascinamento.

Al termine, potete applicare un predefinito per set di batch a una o più cartelle create. Consultate [L&#39;applicazione dei predefiniti per set di batch alle cartelle](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Per creare un predefinito per set di batch per un set di immagini o un set 360 gradi:**

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti per set di batch]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. Nella pagina **[!UICONTROL Predefiniti per set di batch]**, toccate **[!UICONTROL Crea]** in alto a destra.
1. Nella finestra di dialogo **[!UICONTROL Crea predefinito per set di batch]**, immettere un nome descrittivo nel campo di testo **[!UICONTROL Nome predefinito]**. Il nome del predefinito non può essere modificato se successivamente decidete di modificarlo.

1. Nell&#39;elenco a discesa **[!UICONTROL Tipo predefinito]**, selezionare **[!UICONTROL Set immagini]** o **[!UICONTROL Set 360 gradi]**. Accertatevi di scegliere il tipo di predefinito corretto; non è modificabile in seguito.
1. Toccate **[!UICONTROL Crea]**.
1. A destra della pagina **[!UICONTROL Modifica predefinito set di batch]**, impostate le opzioni modificabili desiderate nelle intestazioni **[!UICONTROL Dettagli predefinito]** e **[!UICONTROL Imposta convenzione di denominazione]**.
Per ulteriori informazioni sulle opzioni modificabili disponibili, consultate [Dettagli predefinito, Imposta convenzione di denominazione e Risultati regola - Opzioni RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Create uno o più gruppi di espressioni regolari.

   * Sulla sinistra della pagina **[!UICONTROL Modifica predefinito set di batch]**, in **[!UICONTROL Corrispondenza]**, **[!UICONTROL Nome base]** o **[!UICONTROL Ordinamento sequenza]**, toccare **[!UICONTROL Aggiungi gruppo]**.
   * Il campo **[!UICONTROL Match]** è obbligatorio. **[!UICONTROL Il]** nome di base è obbligatorio solo se il  **** campo corrispondente non specifica già un nome di base utilizzando un raggruppamento parentesi. **[!UICONTROL L&#39;]** ordine delle sequenze è facoltativo.
   * Utilizzando gli elenchi a discesa e le caselle di testo nel modulo del gruppo, specificate un gruppo di espressioni da utilizzare per definire i criteri di denominazione per i membri delle risorse di set di immagini o set 360 gradi.
      * Quando si selezionano e si specificano le espressioni per un gruppo, si noti che la sintassi effettiva dell&#39;espressione regolare si riflette nella parte inferiore destra della pagina, sotto l&#39;intestazione **[!UICONTROL Risultati regola - RegX]** (toccare all&#39;esterno dell&#39;area del modulo per visualizzare la stringa di espressione regolare aggiornata in basso a destra). Queste stringhe di espressione regolare rappresentano il pattern a cui si desidera associare la ricerca di risorse [!DNL Dynamic Media] per creare il set di immagini o set 360 gradi.
      * Per rimuovere un gruppo aggiunto, toccate **[!UICONTROL X]**.
   * Quando si aggiungono due o più gruppi, nell&#39;elenco a discesa **[!UICONTROL And]**, selezionare **[!UICONTROL And]** per unire un nuovo gruppo aggiunto a qualsiasi gruppo di espressioni precedente aggiunto. In alternativa, selezionare **[!UICONTROL OR]** per aggiungere un&#39;alternativa tra il gruppo di espressioni precedente e il nuovo gruppo creato. L&#39;operando **[!UICONTROL OR]** è definito dall&#39;uso di un carattere di riga verticale `|` nella sintassi dell&#39;espressione regolare.

1. Effettua una delle operazioni seguenti:

   * Per aggiungere un altro nuovo gruppo, in **[!UICONTROL Corrispondenza]**, **[!UICONTROL Nome base]** o **[!UICONTROL Ordine di sequenziamento]**, toccare **[!UICONTROL Aggiungi gruppo]**. Create un altro gruppo di espressioni regolari come nel passaggio precedente.
   * Controllare la sintassi delle espressioni regolari nell&#39;area **[!UICONTROL Risultati regola - RegX]**. Se è necessario modificare la sintassi, apportare le modifiche nel rispettivo gruppo a sinistra della pagina.
   * Se avete finito di creare gruppi di espressioni, continuate con il passaggio successivo.

1. Nell’angolo in alto a destro della pagina, tocca **[!UICONTROL Salva]**.

Ora potete applicare il predefinito per set di batch a una o più cartelle di risorse, caricare le risorse nella cartella, quindi creare il set di immagini o il set 360 gradi. Consultate [L&#39;applicazione dei predefiniti per set di batch alle cartelle](#apply-bsp).

### Dettagli predefinito, Imposta convenzione di denominazione e Risultati regola - Opzioni RegX {#features-options-bsp}

Queste opzioni sono disponibili nella pagina **[!UICONTROL Modifica predefinito set di batch]** quando create o modificate un predefinito per set di batch.

Consultate [Creazione di un predefinito per set di batch per un set di immagini o un set 360 gradi](#creating-bsp) o [Modifica di un predefinito per set di batch](#edit-bsp).

| **[!UICONTROL Dettagli del predefinito]** | Descrizione |
| --- | --- |
| Nome predefinito | Sola lettura. Nome specificato al momento della creazione del set di batch. Se dovete rinominare il predefinito, potete copiare il predefinito per set di batch esistente e specificare un nuovo nome. Consultate [Copia di un predefinito per set di batch esistente](#copy-bsp). |
| Tipo | Sola lettura. Il tipo è stato specificato al momento della creazione del set di batch. La copia di un predefinito per set di batch esistente non consente di modificarne il tipo [!UICONTROL Type]; dovete invece creare un predefinito. |
| Includi risorse derivate | Facoltativo. Per fare in modo che gli IPS di [!DNL Dynamic Media] (Image Production System) includano immagini generate o &quot;derivate&quot; con il set 360 gradi o il set di immagini, selezionare **[!UICONTROL Yes]** (predefinito). Una risorsa derivata è un’immagine che non è stata caricata direttamente da un utente. Al contrario, la risorsa è stata prodotta da IPS quando è stata caricata una risorsa principale. Ad esempio, una risorsa immagine generata da IPS da una pagina di un PDF, al momento del caricamento del PDF in [!DNL Dynamic Media], è considerata una risorsa derivata. |
| Cartella di destinazione | Facoltativo. Se definite un numero elevato di set di immagini o set 360 gradi,  Adobe consiglia di tenerli separati dalle cartelle contenenti le risorse. Considerate quindi la creazione di una cartella di set di immagini o di set 360 gradi e reindirizzate l’applicazione in modo da inserire qui i set generati dai set di batch.<br>In tal caso, specificate quale cartella all’interno della struttura di cartelle  Experience Manager Risorse (`/content/dam`) dispone del predefinito per set di batch attivo. Accertatevi che la cartella sia abilitata per la sincronizzazione [!DNL Dynamic Media] in modo da consentirla come cartella di destinazione. Consultate [Configurazione della pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>A più cartelle può essere assegnato un determinato predefinito per set di batch, se lo applicate tramite  **[!UICONTROL Proprietà]** della cartella. Consultate [Applicazione dei predefiniti per set di batch dalla pagina Proprietà di una cartella di risorse](#apply-bsp-to-folders-via-properties).<br>Se non specificate una cartella, il predefinito per set di batch viene creato nella stessa cartella della cartella di caricamento delle risorse. |
| **[!UICONTROL Imposta convenzione di denominazione]** |  |
| Prefisso<br>o<br>Suffisso | Facoltativo. Immettete un prefisso, un suffisso o entrambi nei rispettivi campi.<br>I campi prefisso e suffisso consentono di creare tutti i predefiniti per set di batch utilizzando una convenzione di denominazione file alternativa e personalizzata per un particolare set di contenuti. Questo metodo è particolarmente utile nei casi in cui esiste un&#39;eccezione allo schema di denominazione predefinito definito da una società.<br>Il prefisso o il suffisso viene aggiunto al  **[!UICONTROL Nome base]** definito nell’area  **[!UICONTROL Denominazione]** risorsa. Aggiungendo un prefisso o un suffisso, assicuratevi che il set di immagini o il set 360 gradi venga creato esclusivamente e indipendentemente da altre risorse. Può essere utile anche per aiutare altri a identificare i tipi di file. Ad esempio, per determinare la modalità colore utilizzata, è possibile aggiungere come prefisso o suffisso `rgb` o `cmyk`.<br>Sebbene non sia necessario specificare una convenzione di denominazione per un set di batch, è comunque consigliabile usarla. Questa procedura consente di definire tutti gli elementi della convenzione di denominazione da raggruppare in un set per semplificare la creazione di set di batch. |
| **[!UICONTROL Risultati regola - RegX]** |  |
| Convenzione per la denominazione delle risorse - Corrispondenza | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni selezionate per il modulo Corrispondenza o al codice non elaborato immesso. |
| Convenzione per la denominazione delle risorse - Nome base | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni del modulo Nome base scelte o al codice non elaborato immesso. |
| Ordine sequenza - Corrispondenza | Sola lettura. Visualizza la sintassi delle espressioni regolari in base alle opzioni del modulo selezionate o al codice non elaborato immesso. |

## Informazioni sull&#39;applicazione dei predefiniti per set di batch alle cartelle {#apply-bsp}

Quando assegnate i predefiniti per set di batch a una o più cartelle, tutte le sottocartelle ereditano automaticamente i predefiniti dalla cartella principale.

Potete applicare più predefiniti per set di batch a una cartella.

Le cartelle a cui è stato assegnato un predefinito per batch sono indicate nell&#39;interfaccia utente con il nome del predefinito che appare nella cartella, nella vista **[!UICONTROL Scheda]**.

Per applicare i predefiniti per set di batch alle cartelle, usate uno dei due metodi seguenti:

* [Applica i predefiniti per set di batch alle cartelle di risorse dalla pagina](#apply-bsp-to-folders-via-bsp-page)  Predefinito set di batch. Questo metodo offre la massima flessibilità. Potete applicare uno o più predefiniti a una o più cartelle.
* [Applica i predefiniti per set di batch dalla pagina](#apply-bsp-to-folders-via-properties)  Proprietà di una cartella di risorse. Questo metodo consente di applicare uno o più predefiniti per set di batch a una singola cartella.

Come procedura ottimale, accertatevi che le cartelle di risorse siano sincronizzate [!DNL Dynamic Media], quindi applicate i predefiniti desiderati.

Rielaborate le risorse in una cartella se si verifica uno dei due scenari seguenti:

* Desiderate eseguire un predefinito per set di batch su una cartella di risorse esistente in cui sono già state caricate delle risorse.
* In seguito potete modificare un predefinito per set di batch esistente precedentemente applicato a una cartella di risorse.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Applicazione dei predefiniti per set di batch alle cartelle di risorse dalla pagina Predefinito set di batch {#apply-bsp-to-folders-via-bsp-page}

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti per set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti per set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionate la casella di controllo di ciascun predefinito per set di batch da applicare alle cartelle.
1. Nella barra degli strumenti, toccare **[!UICONTROL Applica predefinito batch alle cartelle]**.
1. Nella pagina **[!UICONTROL Seleziona cartelle]**, selezionate la casella di controllo di ciascuna cartella a cui desiderate applicare i predefiniti per set di batch.
1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Seleziona cartelle]**, toccare **[!UICONTROL Applica]**.

### Applicazione dei predefiniti per set di batch dalla pagina Proprietà di una cartella di risorse {#apply-bsp-to-folders-via-properties}

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passate alla cartella alla quale desiderate applicare uno o più predefiniti per set di batch.
1. Sulla pagina, a sinistra della colonna **[!UICONTROL Nome]**, selezionare la casella di controllo di una cartella.
1. Nella barra degli strumenti, toccare **[!UICONTROL Proprietà]**.
1. Nella pagina Proprietà della cartella, toccate la scheda **[!UICONTROL Dynamic Media Processing]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. In **[!UICONTROL Predefiniti per set di batch]**, dall&#39;elenco a discesa **[!UICONTROL Nome predefinito]**, selezionate il nome di un predefinito per set di batch da applicare. La schermata precedente mostra due predefiniti per set di batch selezionati applicati alla cartella.

   Se nella casella di riepilogo a discesa **[!UICONTROL Nome predefinito]** non sono presenti nomi di predefiniti per set di batch, significa che non è ancora stato creato alcun predefinito per set di batch. Consultate [Creazione di un predefinito per set di batch per un set di immagini o un set 360 gradi](#creating-bsp).

   Per rimuovere un predefinito per set di batch applicato, toccate **[!UICONTROL X]** a destra del tipo di predefinito.

1. Nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Salva e chiudi]**.

## Modifica di un predefinito per set di batch {#edit-bsp}

Potete modificare un predefinito per set di batch esistente creato. Potete modificare uno qualsiasi dei gruppi di espressioni creati per la convenzione di denominazione delle risorse o l’ordine delle sequenze. Se necessario, potete anche aggiornare la cartella di destinazione e impostare le convenzioni di denominazione.

Tuttavia, non potete modificare il nome o il tipo di predefinito del predefinito (set di immagini o set 360 gradi). Se diventa necessario cambiare il nome di un predefinito, potete semplicemente copiare il predefinito esistente e specificare un nuovo nome. Consultate [Copia di un predefinito per set di batch](#copy-bsp).

Se modificate un predefinito per set di batch precedentemente applicato a una cartella, il nuovo predefinito modificato viene applicato solo alle nuove risorse caricate nella cartella.

Se desiderate che il nuovo predefinito modificato venga applicato nuovamente alle risorse esistenti nella cartella, dovete rielaborare la cartella. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->In questo modo, le risorse esistenti ora si qualificano come parte di un set di immagini o set 360 gradi e vengono aggiunte. Inoltre, le risorse già incluse nel set di immagini o nel set 360 gradi in base al predefinito per set di batch utilizzato in precedenza non vengono rimosse (purché non si qualifichino più in base al nuovo predefinito modificato) e vengono visualizzate così com’è.

**Per modificare un predefinito per set di batch:**

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti per set di batch.]**
1. Nella pagina **[!UICONTROL Predefiniti per set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, verificate il predefinito per set di batch da modificare.
1. Nella barra degli strumenti, toccare **[!UICONTROL Modifica predefinito set di batch.]**
1. Modificate il predefinito secondo necessità.
1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Predefinito set di batch]**, toccare **[!UICONTROL Salva.]**

## Copia di un predefinito per set di batch esistente {#copy-bsp}

Potete copiare un predefinito per set di batch esistente per evitare di dover ricreare manualmente un predefinito complesso o per rinominare semplicemente un predefinito. Tuttavia, non potete modificare il tipo di predefinito usato (set di immagini o set 360 gradi).

Se copiate un predefinito esistente a cui fanno riferimento le cartelle delle risorse, queste non verranno modificate.

**Per copiare un predefinito per set di batch esistente:**

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti per set di batch.]**
1. Nella pagina **[!UICONTROL Predefiniti per set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionate la casella di controllo del predefinito per set di batch da copiare.
1. Nella barra degli strumenti, toccare **[!UICONTROL Copia]**.
1. Nella finestra di dialogo **[!UICONTROL Copia predefinito set di batch]**, digitare un nuovo nome per il predefinito nella casella di testo **[!UICONTROL Titolo]**.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Tocca **[!UICONTROL Copia]**.

## La rimozione dei predefiniti per set di batch dalle cartelle {#remove-bsp-from-folder}

Quando rimuovete i predefiniti per set di batch dalle cartelle, alle nuove risorse caricate in queste cartelle non viene applicato il predefinito per set di batch. Le risorse esistenti nella cartella che erano già state aggiunte al set di immagini o al set 360 gradi in base al predefinito per set di batch applicato alla cartella continueranno a essere visualizzate così com’è.

Se invece desiderate eliminare i predefiniti *delete* dalle cartelle, consultate [Eliminazione dei predefiniti per set di batch](#delete-bsp).

Potete usare due metodi per rimuovere i predefiniti per set di batch dalle cartelle.

* [Rimozione dei predefiniti per set di batch dalle cartelle tramite la pagina](#remove-bsp-from-folders-via-bsp-page)  Predefinito set di batch: questo metodo offre la massima flessibilità. Potete rimuovere uno o più predefiniti da una o più cartelle.
* [Rimozione dei predefiniti per set di batch dalla pagina](#remove-bsp-from-folders-via-properties)  Proprietà di una cartella: questo metodo consente di rimuovere uno o più predefiniti per set di batch da una sola cartella.

### Rimozione dei predefiniti per set di batch dalle cartelle tramite la pagina Predefinito set di batch {#remove-bsp-from-folders-via-bsp-page}

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti per set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti per set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionate la casella di controllo di uno o più predefiniti per set di batch da rimuovere da una o più cartelle.
1. Nella barra degli strumenti, toccare **[!UICONTROL Rimuovi predefinito batch da cartelle]**.

1. Nella pagina **[!UICONTROL Seleziona cartelle]**, selezionate una o più cartelle in cui desiderate rimuovere i predefiniti per set di batch.
1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Seleziona cartelle]**, toccare **[!UICONTROL Rimuovi]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. Nella finestra di dialogo **[!UICONTROL Rimuovi profilo]**, toccare **[!UICONTROL Rimuovi]**.

### Rimozione dei predefiniti per set di batch dalla pagina Proprietà di una cartella {#remove-bsp-from-folders-via-properties}

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passate alla cartella in cui desiderate rimuovere uno o più predefiniti per set di batch.
1. Sulla pagina, a sinistra della colonna **[!UICONTROL Nome]**, selezionare la casella di controllo di una cartella.
1. Nella barra degli strumenti, toccare **[!UICONTROL Proprietà]**.
1. Nella pagina Proprietà della cartella, toccare **[!UICONTROL Dynamic Media Processing]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. In **[!UICONTROL Predefiniti per set di batch]**, toccate **[!UICONTROL X]** a destra del tipo di predefinito.

1. Nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Salva e chiudi]**.

## Eliminazione dei predefiniti per set di batch {#delete-bsp}

Potete eliminare i predefiniti per set di batch per rimuoverli definitivamente da [!DNL Dynamic Media]. In altre parole, non vengono più visualizzati nella pagina [!UICONTROL Predefinito set di batch] né nell&#39;elenco a discesa **[!UICONTROL Predefiniti set di batch]** della scheda **[!UICONTROL Dynamic Media Processing]** della pagina **[!UICONTROL Properties]** della cartella. Pertanto, il predefinito non viene applicato alle risorse esistenti in una cartella che vengono rielaborate o quando vengono caricate nuove risorse nella cartella.

Se eliminate un predefinito precedentemente applicato a una o più cartelle, tutti i set di immagini o i set 360 gradi creati dalle risorse in tali cartelle continueranno a essere visualizzati così com’è.

Se invece desiderate *rimuovere i predefiniti* dalle cartelle, consultate [Rimozione dei predefiniti per set di batch dalle cartelle](#remove-bsp-from-folder).

**Per eliminare i predefiniti per set di batch:**

1. Toccate il logo Adobe Experience Manager e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti per set di batch]**.
1. Nella pagina **[!UICONTROL Predefiniti per set di batch]**, a sinistra della colonna **[!UICONTROL Nome predefinito]**, selezionate la casella di controllo di uno o più predefiniti per set di batch da eliminare.
1. Nella barra degli strumenti, toccare **[!UICONTROL Elimina predefiniti per set di batch]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. Nella finestra di dialogo **[!UICONTROL Elimina predefiniti per set di batch]**, toccare **[!UICONTROL Elimina]**.

   Se una cartella di risorse fa riferimento al predefinito che state eliminando, toccate **[!UICONTROL Forza eliminazione]**.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Set di immagini](/help/assets/dynamic-media/image-sets.md)
>* [Set 360 gradi](/help/assets/dynamic-media/spin-sets.md)
>* [Configurazione della pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  - Consultate &quot;Modalità sincronizzazione&quot; nell’argomento per ulteriori informazioni sulla sincronizzazione di una singola cartella in  [!DNL Dynamic Media].
>* [Creazione di una configurazione Dynamic Media in Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  - Consultate &quot;Modalità di sincronizzazione Dynamic Media&quot; nell&#39;argomento per ulteriori informazioni sulla sincronizzazione di tutte le cartelle in  [!DNL Dynamic Media].