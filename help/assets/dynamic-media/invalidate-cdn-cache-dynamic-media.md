---
title: Invalidare la cache di rete per la distribuzione dei contenuti tramite Dynamic Media
description: Scopri come annullare la validità della rete CDN (Content Delivery Network) memorizzata in cache per aggiornare rapidamente le risorse consegnate da Dynamic Media, invece di attendere la scadenza della cache.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 2%

---

# Invalidare la cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Le risorse Dynamic Media vengono memorizzate nella cache dalla rete CDN (Content Delivery Network) per velocizzare la consegna ai clienti. Tuttavia, quando apporti aggiornamenti a tali risorse, desideri che le modifiche diventino effettive immediatamente sul sito web. La rimozione o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse consegnate da Dynamic Media. Non è più necessario attendere la scadenza della cache utilizzando un valore TTL (Time To Live) (il valore predefinito è dieci ore). Al contrario, puoi inviare una richiesta dall’interfaccia utente di Dynamic Media affinché la cache scada in pochi minuti.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN fornita con Adobe in dotazione con Adobe Experience Manager Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Se hai abilitato [Imaging avanzato](/help/assets/dynamic-media/imaging-faq.md) sul tuo account e utilizzi la rete CDN inclusa nel bundle di Adobe, puoi eliminare tutti gli URL con stringhe di query diverse eliminando il singolo URL di base.

Ad esempio, invalidando `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`, invalida anche i seguenti URL:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* e così via.

Tuttavia, questo annullamento della validità non si applica ai domini generici che non supportano l’imaging avanzato, come `s7d1.scene7.com`. Tali domini richiedono ancora l’URL completo per il corretto funzionamento dell’annullamento della validità.

**Per annullare la validità della cache CDN tramite Dynamic Media:**

*Parte 1 di 2: creazione di un modello di annullamento validità CDN*

1. In Adobe Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Modello di annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Il giorno **[!UICONTROL Modello di annullamento validità CDN]** , eseguire una delle seguenti opzioni in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di annullamento della validità CDN utilizzando Dynamic Media Classic. | Il **[!UICONTROL Crea modello]** il campo di testo è precompilato con i dati del modello. In questo caso, puoi modificare il modello o continuare con il passaggio successivo. |
   | Devo creare un modello. Cosa si immette? | In **[!UICONTROL Crea modello]** testo, immetti un URL immagine (inclusi predefiniti immagine o modificatori) che faccia riferimento `<ID>`, invece di un ID immagine specifico come nell’esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, quindi viene compilato Dynamic Media `https://<publishserver_name>/is/image/<company_name>/<ID>` dove `<publishserver_name>` è il nome del server di pubblicazione definito in Impostazioni generali in Dynamic Media Classic. Il `<company_name>` è il nome della directory principale della società associata a questa istanza di Experience Manager e `<ID>` sono le risorse selezionate da invalidare tramite il selettore risorse.<br>Tutti i predefiniti/modificatori seguenti `<ID>` vengono copiate così come sono nella definizione dell’URL.<br>Solo immagini, ovvero `/is/image`-può essere formato automaticamente in base al modello.<br>Per `/is/content/`L’aggiunta di risorse, come video o PDF, mediante il selettore delle risorse non genera automaticamente gli URL. È invece necessario specificare tali risorse nel modello di annullamento della validità CDN oppure è possibile aggiungere manualmente l’URL a tali risorse in *Parte 2 di 2: impostazione delle opzioni di annullamento della validità CDN*.<br>**Esempi:**<br> In questo primo esempio, il modello di invalidazione contiene `<ID>` insieme all’URL della risorsa con `/is/content`. Esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma l’URL in base a questo percorso, con `<ID>` sono le risorse selezionate tramite il selettore risorse che desideri invalidare.<br>In questo secondo esempio, il modello di invalidazione contiene l’URL completo della risorsa utilizzata nelle proprietà web con `/is/content` (non dipende dal selettore risorse). Ad esempio: `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove zaino è l’ID risorsa.<br>I formati di risorse supportati in Dynamic Media possono essere invalidati. Tipi di file di risorse *non* sono supportati per l’annullamento della validità CDN: PostScript®, PostScript® incapsulato, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>· Quando si crea il modello, ma si presta particolare attenzione alla sintassi e agli errori di battitura; Dynamic Media non esegue alcuna convalida del modello.<br>· Il modello di annullamento della validità CDN può salvare il testo fino a 2500 caratteri.<br>· Specifica gli URL per le ritagli avanzati immagine in questo modello di annullamento della validità CDN o in **[!UICONTROL Aggiungi URL]** campo di testo in *Parte 2: impostazione delle opzioni di annullamento della validità CDN.*<br>· Ogni voce in un modello di annullamento della validità CDN deve trovarsi sulla propria riga.<br>· Il seguente esempio di modello di annullamento della validità CDN è solo a scopo dimostrativo. |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >Il modello di annullamento validità CDN può salvare il testo fino a 2500 caratteri.

1. Nell&#39;angolo superiore destro del **[!UICONTROL Modello di annullamento validità CDN]** pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]**.<br>

   *Parte 2 di 2: impostazione delle opzioni di annullamento della validità CDN*
   <br>

1. Nell’Experience Manager as a Cloud Service, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Il giorno **[!UICONTROL Annullamento validità CDN]** - **[!UICONTROL Aggiungi dettagli]** , seleziona le risorse per l’annullamento della validità CDN.

   ![Annullamento validità CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidi di lasciare le opzioni **[!UICONTROL Annullare la validità dei predefiniti immagine associati alla risorsa in CDN]** *e* **[!UICONTROL Annulla validità in base al modello]** Se questa opzione è deselezionata, l’URL di base delle risorse selezionate viene formattato per l’annullamento della validità. Utilizzare questa disposizione di opzioni solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezioni questa opzione, le risorse selezionate e tutti gli URL predefiniti immagine associati vengono automaticamente formattati per l’annullamento della validità della cache.<br>Le risorse e i relativi URL predefiniti associati vengono automaticamente formati per l’annullamento della validità. Questa opzione funziona solo per le risorse immagini. |
   | **[!UICONTROL Annullamento della validità in base al modello]** | (Facoltativo) Seleziona questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi risorse]** | Utilizza il Selettore risorse per selezionare le risorse da invalidare. Puoi selezionare risorse pubblicate o non pubblicate.<br>La memorizzazione in cache nella rete CDN è basata su URL e non su risorse. Pertanto, è necessario essere a conoscenza degli URL completi presenti sul sito web. Dopo aver determinato tali URL, puoi aggiungerli al modello. Quindi puoi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Utilizza questa opzione con **[!UICONTROL Annullare la validità dei predefiniti immagine associati alla risorsa in CDN]**, o **[!UICONTROL Annullamento della validità in base al modello]**, o entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungi o incolla manualmente i percorsi URL completi per le risorse Dynamic Media di cui desideri annullare la validità della cache CDN. Utilizza questa opzione se non hai creato un modello di annullamento validità CDN in ***Parte 1 di 2: creazione di un modello di annullamento validità CDN*** e hanno solo poche risorse da invalidare.<br>**Importante:** Ogni URL aggiunto deve trovarsi sulla propria riga.<br>Puoi annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel **[!UICONTROL Aggiungi URL]** il campo di testo è maggiore di 1000. Impossibile selezionare **[!UICONTROL Successivo]**. In questi casi, seleziona **[!UICONTROL X]** a destra di una risorsa selezionata o di un URL aggiunto manualmente per eliminarla dall’elenco di invalidazione.<br>Specifica gli URL per le ritagli avanzati immagine nel modello di annullamento della validità CDN o in questo **[!UICONTROL Aggiungi URL]** campo di testo. |

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Successivo]**.
1. Il giorno **[!UICONTROL Annullamento validità CDN]** - **[!UICONTROL Conferma]** pagina, nella **[!UICONTROL URL]** Casella di riepilogo, viene visualizzato un elenco di uno o più URL generati dal modello di annullamento della validità CDN creato in precedenza e dalle risorse appena aggiunte.

   Ad esempio, utilizzando l’esempio Modello di annullamento validità CDN mostrato nei passaggi precedenti, supponi di aver aggiunto una singola risorsa denominata `spinset`. Quando si passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Annullamento validità CDN]**, si ottengono i seguenti cinque URL generati nel **[!UICONTROL Annullamento validità CDN - Conferma]** Interfaccia utente:

   ![Annullamento validità CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, selezionare **X** a destra di un URL per eliminarlo dal processo di invalidazione.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Invia]** per avviare il processo di annullamento della validità CDN.

## Risolvere i problemi relativi agli errori di annullamento della validità CDN

In tutti i casi, l’intero batch viene elaborato per l’annullamento della validità o l’intero batch non riesce.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se si verifica uno dei seguenti scenari:<br>- Configurazione Dynamic Media non trovata.<br>- Eccezione durante il recupero di un utente del servizio tramite il quale viene letta la configurazione di Dynamic Media.<br>: il server di pubblicazione o la directory principale della società utilizzata per formare gli URL non è presente nella configurazione di Dynamic Media. |
| *Alcuni URL non sono definiti correttamente. Correggi e invia di nuovo.* | Si verifica se l&#39;API di annullamento della validità della cache CDN IPS restituisce un errore. L&#39;errore indica che l&#39;URL fa riferimento a un&#39;altra società o che l&#39;URL non è valido in base alla convalida eseguita dall&#39;API cdnCacheInvalidation di IPS. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso da invalidare.* | Si verifica se non sono presenti URL nel **[!UICONTROL Annullamento validità CDN]** - **[!UICONTROL Conferma]** e si seleziona **[!UICONTROL Invia]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
