---
title: Guida introduttiva di AEM Forms Edge Delivery Service. Creare un modulo.
description: Forme perfette, veloce! ⚡ authoring basato su documento di AEM Forms Edge Delivery = velocità sorprendente e moduli compatibili con SEO per utenti e motori di ricerca più felici.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Creare un modulo utilizzando il blocco di modulo adattivo

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. AEM Forms Edge Delivery consente di creare moduli utilizzando strumenti familiari come Word o Google Docs.

Questi moduli inviano i dati direttamente a un file Microsoft Excel o Google Sheets, consentendo di utilizzare un ecosistema dinamico e API affidabili di Google Sheets, Microsoft Excel e Microsoft Sharepoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

![Ecosistema di authoring basato su documenti](/help/edge/assets/document-based-authoring-workflow-create-form.png)

AEM Forms Edge Delivery fornisce un blocco, noto come blocco di moduli adattivi, per facilitare la creazione di moduli per acquisire e archiviare i dati acquisiti. Per iniziare a creare un modulo, puoi includere il blocco di modulo adattivo nel progetto EDS AEM. Iniziamo:


## Prerequisiti

Prima di iniziare, assicurati di aver completato i seguenti passaggi:

* Configura il progetto GitHub Edge Delivery Services (EDS) utilizzando il boilerplate AEM e clona l’archivio GitHub corrispondente sul computer locale. Consulta [tutorial per sviluppatori](https://www.aem.live/developer/tutorial) per i dettagli. In questo documento, la cartella locale del progetto Edge Delivery Services (EDS) viene indicata come `[EDS Project repository]` .
* Assicurati di avere accesso a Google Sheets o Microsoft SharePoint. Per impostare Microsoft SharePoint come origine di contenuto, vedere [Come utilizzare Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## Creare un modulo

+++ Passaggio 1: aggiungi il blocco di modulo adattivo al progetto Edge Delivery Services (EDS).

L’adattivo consente agli utenti di creare moduli per un sito dei servizi di consegna Edge. Tuttavia, questo blocco non è incluso nel boilerplate predefinito dell’AEM (utilizzato per creare un progetto Edge Delivery Services). Per integrare facilmente il blocco di modulo adattivo nel progetto di Edge Delivery Services:

1. **Clonare l’archivio del blocco di moduli adattivi**: clona il [Archivio per blocchi di moduli adattivi](https://github.com/adobe-rnd/form-block) sul computer locale. Contiene il codice per eseguire il rendering del modulo su una pagina Web EDS. In questo documento, la cartella locale dell’archivio Forms Block viene indicata come `[Adaptive Form Block repository]`.
1. **Individua l’archivio del blocco di moduli adattivi:** Accedere a [Archivio per blocchi di moduli adattivi]/block/src e copiarne il contenuto.

1. sul computer locale e copia `form` cartella.
1. **Incollare il codice del blocco modulo adattivo nel progetto EDS:**
Accedi a [Archivio di progetti EDS]/block/ nel computer locale e crea una cartella &quot;form&quot;. Incolla il `[Adaptive Form Block repository]/blocks/src content`, copiato nel passaggio precedente in `[EDS Project repository]/blocks/form` cartella.
1. **Commit delle modifiche su GitHub:** Archivia `[EDS Project repository]/blocks/form` e i file sottostanti al progetto Edge Delivery Services su GitHub.

Dopo aver completato questi passaggi, il blocco di modulo adattivo viene aggiunto correttamente all’archivio dei progetti Edge Delivery Services (EDS) su GitHub. È ora possibile creare e aggiungere moduli a una pagina EDS Sites.


**Risoluzione dei problemi di build di GitHub**

Garantire un processo di generazione GitHub fluido affrontando potenziali problemi:

* **Errore nel percorso del modulo di risoluzione:**
Se viene visualizzato l&#39;errore &quot;Impossibile risolvere il percorso del modulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, passare alla [Progetto EDS]file /blocks/forms/form.js. Aggiorna l’istruzione di importazione sostituendo il file lib-franklin.js con il file aem.js.

* **Gestisci errori di stampa:**
In caso di errori di stampa, è possibile ignorarli. Apri [Progetto EDS]/package.json file e modifica lo script &quot;lint&quot; da &quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot; a &quot;lint&quot;: &quot;echo &#39;skipping linting for now&#39;&quot;. Salva il file e conferma le modifiche nel progetto GitHub.

+++

+++ Passaggio 2: creare un modulo utilizzando Microsoft Excel o Foglio Google.

Invece di navigare attraverso processi complessi, la creazione di un modulo può essere ottenuta facilmente utilizzando un foglio di calcolo. È possibile definire le righe e le colonne che costituiranno la struttura del modulo. Ogni riga rappresenta un singolo utente [campo modulo](/help/edge/docs/forms/form-components.md#available-components) e le intestazioni di colonna definiscono le corrispondenti [proprietà campo](/help/edge/docs/forms/form-components.md#components-properties).

Ad esempio, considera il seguente foglio di calcolo in cui le righe contornano i campi per un `enquiry` le intestazioni di maschera e colonna definiscono le relative proprietà:

![Foglio di calcolo interrogazione](/help/edge/assets/enquiry-form-spreadsheet.png)

Per procedere con la creazione del modulo:

1. Accedi alla cartella del progetto AEM Edge Delivery su Microsoft SharePoint o Google Drive.

1. Crea una cartella di lavoro di Microsoft Excel o un foglio di Google ovunque all’interno della directory di progetto AEM Edge Delivery. Ad esempio, crea un foglio di calcolo denominato `enquiry` nella directory del progetto AEM Edge Delivery su Google Drive.

1. Assicurati che il foglio sia condiviso con l’utente AEM appropriato (ad esempio `helix@adobe.com`) [in base alle configurazioni specificate per il progetto](https://www.aem.live/docs/setup-customer-sharepoint). Concedere all&#39;utente l&#39;autorizzazione di modifica per il foglio.

1. Apri il foglio di calcolo creato e rinomina il foglio predefinito in &quot;shared-default&quot;.

   ![rinominare il foglio predefinito in &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Per aggiungere i campi modulo, inserire righe e intestazioni di colonna nel foglio &quot;shared-default&quot;. Ogni riga deve rappresentare un [campo modulo](/help/edge/docs/forms/form-components.md#available-components), con intestazioni di colonna che definiscono il campo corrispondente [proprietà](/help/edge/docs/forms/form-components.md#components-properties).

   Per un avvio rapido, è consigliabile copiare il contenuto della [Foglio di calcolo interrogazione](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) nel foglio di calcolo. Dopo aver copiato il contenuto, salva il foglio di calcolo.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l&#39;anteprima del foglio.

   ![Utilizza AEM Sidekick per visualizzare l’anteprima del foglio](/help/edge/assets/preview-form.png)

   In anteprima, nelle nuove schede del browser il contenuto del foglio viene visualizzato in formato JSON. Assicurati di acquisire l’URL di anteprima, in quanto è necessario per il rendering del modulo nella sezione successiva. Il formato dell’URL è il seguente:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` fa riferimento al ramo dell’archivio GitHub.
   * `<repository>` denota l’archivio GitHub.
   * `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.

   Ad esempio, se l’archivio del progetto è denominato &quot;portale&quot;, si trova sotto l’account &quot;wkndforms&quot; e stai utilizzando il ramo &quot;principale&quot;, l’URL avrà l’aspetto seguente:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ Passaggio 3: visualizzare in anteprima il modulo utilizzando la pagina Edge Delivery Services (EDS).


Finora hai aggiunto il blocco modulo adattivo al progetto EDS e preparato la struttura del modulo. Ora, per visualizzare l’anteprima del modulo:

1. **Accedere alla directory dei progetti:** Apri l’account Microsoft SharePoint o Google Drive e passa alla directory del progetto AEM Edge Delivery.

1. **Incorpora il modulo in un documento:** Aprire un file di documento, ad esempio un file di indice, per incorporare il modulo. In alternativa, è possibile creare un nuovo documento.

1. **Passa alla posizione desiderata:** Spostarsi nella posizione desiderata all&#39;interno del documento in cui si desidera aggiungere il modulo.

1. **Aggiungi il blocco di modulo adattivo:** Per creare un blocco di modulo per il rendering del modulo. Selezionate Inserisci > Tabella (Table) e create una tabella a una colonna e due righe. Denomina la tabella &quot;Form&quot; e incolla l’URL di anteprima nella seconda riga. Accertati che l’URL sia formattato come collegamento ipertestuale, non come testo normale, come illustrato di seguito:

   | Modulo |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Questo blocco funge da segnaposto in cui è incorporato il modulo. Nella seconda riga del blocco, aggiungi l’URL di anteprima del `<form>.json` come collegamento ipertestuale.

   >[!IMPORTANT]
   >
   >
   > Verificare che l&#39;URL sia formattato come collegamento ipertestuale anziché come testo normale.


1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l&#39;anteprima del documento. Nella pagina viene ora visualizzato il modulo. Ad esempio, questo è il modulo basato su [foglio di calcolo interrogazione](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Un esempio di modulo EDS](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   A questo punto, compilare il modulo e fare clic sul pulsante Invia, si verifica un errore simile al seguente, perché il foglio di calcolo non è ancora impostato per accettare i dati.

   ![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

+++


## Passaggio successivo

[Preparare il foglio di calcolo](/help/edge/docs/forms/submit-forms.md) per iniziare ad accettare i dati all’invio del modulo.




