---
title: Invalidare la cache di rete per la distribuzione dei contenuti tramite Dynamic Medie
description: Scopri come annullare la validità della rete CDN (Content Delivery Network) memorizzata in cache per aggiornare rapidamente le risorse consegnate da Dynamic Medie, invece di attendere la scadenza della cache.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 1%

---

# Invalidare la cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Le risorse Dynamic Medie vengono memorizzate nella cache dalla rete CDN (Content Delivery Network) per velocizzare la consegna ai clienti. Tuttavia, quando apporti aggiornamenti a tali risorse, desideri che le modifiche diventino effettive immediatamente sul sito web. La rimozione o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse consegnate da Dynamic Medie. Non è più necessario attendere la scadenza della cache utilizzando un valore TTL (Time To Live) (il valore predefinito è dieci ore). Al contrario, puoi inviare una richiesta dall’interfaccia utente di Dynamic Medie affinché la cache scada in pochi minuti.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN fornita in bundle con Adobe e fornita con Adobe Experience Manager Dynamic Medie. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Se hai abilitato [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) sul tuo account e utilizzi la rete CDN di Adobe, puoi eliminare tutti gli URL con stringhe di query diverse eliminando il singolo URL di base.

L&#39;annullamento della validità di `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`, ad esempio, invalida anche i seguenti URL:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* e così via.

Questa invalidazione, tuttavia, non si verifica per i domini generici che non supportano Smart Imaging, ad esempio `s7d1.scene7.com`. Tali domini richiedono ancora l’URL completo per il corretto funzionamento dell’annullamento della validità.

**Per annullare la validità della cache CDN tramite Dynamic Medie:**

*Parte 1 di 2: creazione di un modello di annullamento validità CDN*

1. In Adobe Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Modello di annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Nella pagina **[!UICONTROL Modello di annullamento validità CDN]** eseguire una delle opzioni seguenti in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di annullamento della validità CDN utilizzando Dynamic Media Classic. | Il campo di testo **[!UICONTROL Crea modello]** è precompilato con i dati del modello. In questo caso, puoi modificare il modello o continuare con il passaggio successivo. |
   | Devo creare un modello. Cosa si immette? | Nel campo di testo **[!UICONTROL Crea modello]**, immettere un URL immagine (inclusi predefiniti immagine o modificatori) che fa riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, Dynamic Medie compila `https://<publishserver_name>/is/image/<company_name>/<ID>`, dove `<publishserver_name>` è il nome del server Publish definito in Impostazioni generali di Dynamic Media Classic. `<company_name>` è il nome della directory principale della società associata a questa istanza di Experience Manager e `<ID>` sono le risorse selezionate tramite il selettore risorse da invalidare.<br>Tutti i predefiniti/modificatori successivi a `<ID>` vengono copiati così come sono nella definizione dell&#39;URL.<br>Solo le immagini, ovvero `/is/image`, possono essere formate automaticamente in base al modello.<br>Per `/is/content/`, l&#39;aggiunta di risorse come video o PDF tramite il selettore risorse non genera automaticamente gli URL. È invece necessario specificare tali risorse nel modello di annullamento validità CDN oppure è possibile aggiungere manualmente l&#39;URL a tali risorse in *Parte 2 di 2: Impostazione delle opzioni di annullamento validità CDN*.<br>**Esempi:**<br> In questo primo esempio, il modello di invalidazione contiene `<ID>` insieme all&#39;URL della risorsa con `/is/content`. Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Medie forma l&#39;URL in base a questo percorso; `<ID>` sono le risorse selezionate tramite il selettore risorse che desideri invalidare.<br>In questo secondo esempio, il modello di annullamento della validità contiene l&#39;URL completo della risorsa utilizzata nelle proprietà Web con `/is/content` (non dipendente dal selettore risorse). Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove zaino è l&#39;ID risorsa.<br>I formati di risorse supportati in Dynamic Medie possono essere invalidati. I tipi di file di risorse *non* supportati per l&#39;annullamento della validità CDN includono PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>· Durante la creazione del modello, prestare particolare attenzione alla sintassi e agli errori di battitura; Dynamic Medie non esegue alcuna convalida del modello.<br>· Il modello di annullamento validità CDN può salvare il testo fino a 2500 caratteri.<br>· Specificare gli URL per le ritagli avanzati immagine in questo modello di annullamento validità CDN o nel campo di testo **[!UICONTROL Aggiungi URL]** in *Parte 2: impostazione delle opzioni di annullamento validità CDN.*<br>· Ogni voce in un modello di annullamento della validità CDN deve trovarsi sulla propria riga.<br>· Il seguente esempio di modello di annullamento della validità CDN è solo a scopo dimostrativo. |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >Il modello di annullamento validità CDN può salvare il testo fino a 2500 caratteri.

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Modello di annullamento validità CDN]**, selezionare **[!UICONTROL Salva]**, quindi selezionare **[!UICONTROL OK]**.<br>
   *Parte 2 di 2: impostazione delle opzioni di annullamento della validità CDN*
   <br>

1. Experience Manager In as a Cloud Service, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Nella pagina **[!UICONTROL Annullamento validità CDN]** - **[!UICONTROL Aggiungi dettagli]**, seleziona le risorse per l&#39;annullamento della validità CDN.

   ![Annullamento validità CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidi di lasciare deselezionate le opzioni **[!UICONTROL Annulla validità predefiniti immagine associati alla risorsa in CDN]** *e* **[!UICONTROL Annulla validità in base al modello]**, viene creato l&#39;URL di base delle risorse selezionate per l&#39;annullamento della validità. Utilizzare questa disposizione di opzioni solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezioni questa opzione, le risorse selezionate e tutti gli URL predefiniti immagine associati vengono automaticamente formattati per l’annullamento della validità della cache.<br>Assets e i relativi URL predefiniti associati vengono automaticamente formati per l&#39;annullamento della validità. Questa opzione funziona solo per le risorse immagini. |
   | **[!UICONTROL Annullamento della validità in base al modello]** | (Facoltativo) Seleziona questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi Assets]** | Utilizza il Selettore risorse per selezionare le risorse da invalidare. Puoi selezionare risorse pubblicate o non pubblicate.<br>La memorizzazione in cache nella rete CDN è basata su URL e non su risorse. Pertanto, è necessario essere a conoscenza degli URL completi presenti sul sito web. Dopo aver determinato tali URL, puoi aggiungerli al modello. Quindi puoi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Utilizzare questa opzione con **[!UICONTROL Invalidare i predefiniti immagine associati alla risorsa in CDN]**, **[!UICONTROL Invalidare in base al modello]** o entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungi o incolla manualmente i percorsi URL completi per le risorse Dynamic Medie di cui desideri annullare la validità della cache CDN. Utilizzare questa opzione se non è stato creato un modello di annullamento validità CDN in ***Parte 1 di 2: Creazione di un modello di annullamento validità CDN*** e sono disponibili solo alcune risorse da annullare la validità.<br>**Importante:** ogni URL aggiunto deve trovarsi sulla propria riga.<br>È possibile annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel campo di testo **[!UICONTROL Aggiungi URL]** è maggiore di 1000, non è possibile selezionare **[!UICONTROL Avanti]**. In questi casi, è necessario selezionare **[!UICONTROL X]** a destra di una risorsa selezionata o un URL aggiunto manualmente per eliminarla dall&#39;elenco di invalidazione.<br>Specifica gli URL per le ritagli avanzati immagine nel modello di annullamento della validità CDN o in questo campo di testo **[!UICONTROL Aggiungi URL]**. |

1. Seleziona **[!UICONTROL Avanti]** nell&#39;angolo superiore destro della pagina.
1. Nella pagina **[!UICONTROL Annullamento validità CDN]** - **[!UICONTROL Conferma]**, nella casella di riepilogo **[!UICONTROL URL]** viene visualizzato un elenco di uno o più URL generati dal modello di annullamento validità CDN creato in precedenza e dalle risorse appena aggiunte.

   Ad esempio, utilizzando l&#39;esempio del modello di invalidazione CDN illustrato nei passaggi precedenti, si supponga di aver aggiunto una singola risorsa denominata `spinset`. Quando si passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Annullamento validità CDN]**, vengono generati i seguenti cinque URL nell&#39;interfaccia utente **[!UICONTROL Annullamento validità CDN - Conferma]**:

   ![Annullamento validità CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, selezionare **X** a destra di un URL per eliminarlo dal processo di invalidazione.

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Invia]** per avviare il processo di annullamento della validità CDN.

## Risolvere i problemi relativi agli errori di annullamento della validità CDN

In tutti i casi, l’intero batch viene elaborato per l’annullamento della validità o l’intero batch non riesce.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se si verifica uno dei seguenti scenari:<br>- Impossibile trovare una configurazione di Dynamic Medie.<br>- Eccezione durante il recupero di un utente del servizio tramite il quale viene letta la configurazione di Dynamic Medie.<br>- Il server di pubblicazione o la directory principale della società utilizzata per formare gli URL non è presente nella configurazione di Dynamic Medie. |
| *Alcuni URL non sono definiti correttamente. Correggi e invia di nuovo.* | Si verifica se l&#39;API di annullamento della validità della cache CDN IPS restituisce un errore. L&#39;errore indica che l&#39;URL fa riferimento a un&#39;altra società o che l&#39;URL non è valido in base alla convalida eseguita dall&#39;API cdnCacheInvalidation di IPS. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso per essere invalidato.* | Si verifica se non sono presenti URL nella pagina **[!UICONTROL Annullamento validità CDN]** - **[!UICONTROL Conferma]** e si seleziona **[!UICONTROL Invia]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. While you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
