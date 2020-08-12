---
title: Annullamento della validità della cache CDN tramite Dynamic Media
description: L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, anziché attendere la scadenza della cache.
translation-type: tm+mt
source-git-commit: aae3dcb0f44ef8e8d1401274fbf1fd47ea718b09
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---


# Annullamento della validità della cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Le risorse per contenuti multimediali dinamici sono memorizzate nella cache dalla rete CDN (Content Delivery Network) per una distribuzione rapida dei contenuti ai clienti. Tuttavia, quando apportate gli aggiornamenti a tali risorse, potreste desiderare che le modifiche diventino attive immediatamente sul sito Web. Lo svuotamento o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse distribuite da Dynamic Media. Invece di aspettare che la cache scada utilizzando un valore TTL (Time To Live) (il valore predefinito è 10 ore), potete inviare una richiesta dall&#39;interfaccia utente di Dynamic Media affinché la cache scada in pochi minuti.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo a Contenuti multimediali dinamici su AEM come Cloud Service. È inoltre necessario utilizzare il CDN fornito con AEM file multimediali dinamici. Qualsiasi altra CDN personalizzata non è supportata da questa funzione. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consultate anche Panoramica sulla [memorizzazione nella cache in Contenuti multimediali](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)dinamici.

**Per annullare la validità della cache CDN mediante un supporto dinamico**

*Parte 1: Creazione di un modello di annullamento validità CDN*

1. In AEM come Cloud Service, toccate **[!UICONTROL Strumenti > Risorse > Modello di annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Nella pagina Modello **[!UICONTROL di annullamento validità]** CDN, effettuate una delle seguenti operazioni in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di annullamento validità CDN utilizzando Dynamic Media Classic. | Il campo di testo **[!UICONTROL Crea modello]** è precompilato con i dati del modello. In tal caso, potete modificare il modello oppure continuare con il passaggio successivo. |
   | Devo creare un modello. In cosa si entra? | Nel campo di testo **[!UICONTROL Crea modello]** , immettete un URL immagine (con predefiniti per immagini o modificatori) che faccia riferimento `<ID>`, invece di un ID immagine specifico come nell’esempio seguente:<br><br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br><br>Se il modello contiene solo `<ID>`, Dynamic Media compila il `https://<publishserver_name>/is/image` percorso in cui `<publishserver_name>` è il nome del server di pubblicazione e `ID` sono le risorse selezionate da annullare.<br><br>Solo le immagini `/is/image`- ovvero - possono essere formate automaticamente in base al modello. Ad `/is/content/`esempio, l’aggiunta di risorse come video o PDF tramite il selettore delle risorse non genera automaticamente URL. Al contrario, è necessario specificare tali risorse nel modello di annullamento validità CDN, oppure è possibile aggiungere manualmente l’URL a tali risorse nella *Parte 2: Impostazione delle opzioni* di annullamento validità CDN.<br>I formati di risorse supportati in Contenuti multimediali dinamici possono essere annullati. Risorse come PowerPoint o file di testo normale non sono supportate per l’annullamento della validità CDN.<br>Quando create il modello, ma prestate attenzione alla sintassi e agli errori di battitura; Gli elementi multimediali dinamici non eseguono la convalida dei modelli.<br>L’esempio di modello riportato di seguito è solo a scopo illustrativo. |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. Nell&#39;angolo superiore destro della pagina Modello di annullamento validità CDN, toccate **[!UICONTROL Salva]**, quindi toccate **[!UICONTROL OK]**.<br>

   ***Parte 2: Impostazione delle opzioni di annullamento validità CDN***
<br>

1. In AEM come Cloud Service, toccate **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Nella pagina **[!UICONTROL Annulla validità]** CDN - **[!UICONTROL Aggiungi dettagli]** , selezionate le risorse per l’annullamento della validità CDN.

   ![Annullamento validità CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidete di lasciare deselezionata l’opzione **[!UICONTROL Annulla validità predefiniti immagine associati alla risorsa in CDN]** *e* Annulla validità in base al modello **** , l’URL di base delle risorse selezionate viene formato per l’annullamento della validità. È consigliabile utilizzare questa disposizione di opzioni solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezionate questa opzione, potete selezionare una o più risorse Contenuti multimediali dinamici, indipendentemente dal tipo MIME, e i relativi predefiniti immagine associati per l’annullamento della validità della cache.<br>Le risorse e i relativi URL predefiniti preimpostati vengono formati automaticamente per l’annullamento della validità. Questa opzione funziona solo per<br>le risorse di immagini. Anche se potete selezionare una o più cartelle contenenti risorse,  Adobe non consiglia questo approccio. È invece necessario selezionare singoli file di risorse. |
   | **[!UICONTROL Annullamento della convalida in base al modello]** | (Facoltativo) Selezionate questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi risorse]** | Usate il selettore delle risorse per selezionare le risorse da annullare. Potete selezionare risorse pubblicate o non pubblicate.<br>Potete visualizzare un elenco vuoto quando aggiungete delle risorse. Per gli elementi multimediali dinamici viene utilizzato il modello di annullamento validità CDN per creare automaticamente un URL per annullare la validità della CDN. Se non è stato creato alcun modello di annullamento validità CDN, viene visualizzato un elenco vuoto.<br>La memorizzazione nella cache del CDN è basata su URL, non su risorse. Pertanto, è necessario conoscere gli URL completi presenti sul sito Web. Dopo aver determinato tali URL, potete aggiungerli al modello. Potete quindi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. L’altra opzione disponibile è l’aggiunta di URL all’elenco di annullamento validità CDN. Se preferite questo approccio, non è necessario selezionare e aggiungere risorse prima di toccare **[!UICONTROL Avanti]** e quindi **[!UICONTROL Invia]** per l’annullamento della validità.<br>Usate questa opzione insieme ai predefiniti per immagini associati per risorse **[!UICONTROL Annulla validità in CDN]**, **[!UICONTROL Annulla validità in base al modello]** o a entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungete o incollate manualmente i percorsi URL completi alle risorse per file multimediali dinamici la cui cache CDN desiderate annullare la validità. Utilizzate questa opzione se non avete creato un modello di annullamento validità CDN nella ***parte 1: Utilizzo del modello*** di annullamento validità CDN e poche risorse da annullare.<br> |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. Nella pagina **[!UICONTROL Annulla validità]** CDN - **[!UICONTROL Conferma]** , nella casella di riepilogo **[!UICONTROL URL]** viene visualizzato uno o più URL generati dal modello di annullamento validità CDN precedentemente creato e dalle risorse appena aggiunte.

   Ad esempio, con il modello di annullamento validità CDN creato in precedenza, supponete di aver aggiunto una singola risorsa denominata `spinset`. Toccando **[!UICONTROL Strumenti > Risorse > Annullamento validità]** CDN si ottengono i seguenti cinque URL generati nell’interfaccia **[!UICONTROL Annulla validità CDN - Conferma]** utente:

   ![Annullamento validità CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, toccate la **X** a destra di un URL per eliminarlo dal processo di annullamento della validità. Potete avere fino a 1000 URL per volta.

1. Nell’angolo superiore destro della pagina, toccate **[!UICONTROL Invia]** per avviare il processo di annullamento della validità della CDN.

## Risoluzione di errori di annullamento validità CDN

* Questa funzione consente di annullare la validità di un massimo di 1000 URL alla volta. Un numero maggiore di 1000 genera un errore che è possibile risolvere eliminando gli URL nella pagina **[!UICONTROL Annulla validità CDN - Conferma]** .
* In tutti i casi, l&#39;intero batch viene elaborato per l&#39;annullamento della validità oppure l&#39;intero batch non riesce.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se vengono soddisfatti i seguenti scenari:<br>- Non viene trovata una configurazione per contenuti multimediali dinamici.<br>- È presente un&#39;eccezione durante il recupero di un utente di servizio tramite il quale viene letta la configurazione Dynamic Media.<br>- Il server di pubblicazione o la directory principale della società utilizzata per creare gli URL non è presente nella configurazione per elementi multimediali dinamici. |
| *Alcuni URL non sono definiti correttamente. Correggere e inviare di nuovo.* | Si verifica se l&#39;API di annullamento validità cache CDN IPS restituisce un errore che fa riferimento a un&#39;altra società o se l&#39;URL non è valido in base alla convalida eseguita dall&#39;API cdnCacheInvalidation IPS. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso per essere invalidato.* | Si verifica se non sono presenti URL nella pagina **** Annulla validità CDN - Conferma e toccate **[!UICONTROL Invia]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->