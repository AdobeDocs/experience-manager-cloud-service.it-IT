---
title: Creare URL personalizzati utilizzando Dynamic Media con funzionalità OpenAPI
description: Utilizza le funzionalità OpenAPI di Dynamic Media per trasformare gli URL lunghi di consegna delle risorse in URL brevi e personalizzati. Un URL personalizzato è una versione breve, pulita, facile da ricordare e leggibile del tuo URL di consegna complesso. Puoi includere il nome del tuo marchio, i nomi dei prodotti e le parole chiave pertinenti nell’URL personalizzato per migliorare la visibilità del tuo marchio e il coinvolgimento degli utenti
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: d9223a8af5d531e66a91e9054201de765be50961
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---


# Utilizzare URL personalizzati{#vanity-urls}

Utilizza [!DNL Dynamic Media with OpenAPI capabilities] per trasformare gli URL lunghi di consegna delle risorse in URL brevi e personalizzati. Gli URL di consegna di risorse standard includono UID di risorse generate dal sistema che rendono l’URL di consegna complesso, difficile da ricordare e condividere. Sostituisci questi UUID delle risorse con identificatori semplici (Vanity ID) per generare un URL personalizzato. Un URL personalizzato è una versione breve, pulita e leggibile del tuo URL di consegna complesso.

Consulta i seguenti formati URL per comprenderne la differenza:
* [URL di consegna standard](#standard-urls)
* [Gli URL personalizzati](#vanity-url)

Gli URL di consegna standard utilizzano `aaid` seguito da un UUID, mentre gli URL personalizzati utilizzano `avid` seguito da un identificatore personalizzato (identificatore personalizzato).

Utilizza identificatori di reindirizzamento brevi e semplici per rendere il tuo URL personalizzato breve, pulito, leggibile, facile da ricordare e da condividere. Utilizza il tuo nome di marchio, i nomi dei prodotti e le parole chiave rilevanti come ID personalizzati per aumentare la visibilità del tuo marchio e il coinvolgimento degli utenti.

Quando l&#39;utente fa clic sull&#39;URL personalizzato, [!DNL Dynamic Media with OpenAPI] viene mappato automaticamente sulla posizione della risorsa originale al momento dell&#39;acquisizione e risolto correttamente al momento della consegna per inviare la risorsa all&#39;utente.

Scopri come [creare URL personalizzati](#create-vanity-urls).

## URL di consegna standard{#standard-urls}

L&#39;URL di consegna risorse [!DNL Dynamic Media with OpenAPI] standard include un identificatore univoco generato dal sistema e segue il seguente formato.

***Formato:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

L&#39;URL di consegna standard include `aaid` (*identificatore risorsa effettivo*) dopo `urn:` e un UUID tra `urn:aaid:aem:` e `/as/<seoname>.<format>`.

***Esempio:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

Nell&#39;esempio precedente, `43341ab1-4086-44d2-b7ce-ee546c35613b` è l&#39;UUID.

## Gli URL personalizzati{#vanity-url}

Gli URL personalizzati includono un identificatore personalizzato al posto dell’UUID della risorsa e seguono il seguente formato.

***Formato:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

L&#39;URL personalizzato include `avid` (*identificatore personalizzato effettivo*) dopo `urn:` e il tuo ID personalizzato tra `urn:avid:aem:` e `/<seoname>.<format>`.

***Esempio:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

Nell&#39;esempio precedente, `VanityCheck` è l&#39;ID del reindirizzamento che ha sostituito l&#39;UUID.

## Esplora le funzionalità e i vantaggi principali{#capabilities-and-benefits-of-vanity-urls}

L’utilizzo di ID personalizzati significativi per personalizzare gli URL di consegna delle risorse standard offre diversi vantaggi e un impatto quantificabile. Di seguito sono riportati alcuni vantaggi e funzionalità chiave degli URL personalizzati.

### Funzionalità principali{#key-capabilities}

* **Personalizzazione URL:** Sostituisci gli identificatori lunghi (UUID risorsa) nell&#39;URL di consegna con alternative più brevi e allineate al brand per generare un URL di consegna più pulito.
* **Reindirizzamento in tempo reale:** gli URL personalizzati vengono reindirizzati agli UUID della risorsa originale in fase di esecuzione senza interrompere i flussi di lavoro. Gli utenti visualizzano gli URL puliti nella barra degli indirizzi mentre il sistema gestisce il routing tecnico.
* **Gestione semplificata dei collegamenti:** personalizza i tuoi URL personalizzati in qualsiasi momento senza influire sulle prestazioni di consegna delle risorse.

### Vantaggi chiave{#key-benefits}

* **Migliora l&#39;esperienza utente:** gli URL personalizzati puliti e più brevi sono leggibili, facili da ricordare e condividere.

* **Migliora il coinvolgimento dell&#39;utente:** gli URL con marchio generano fiducia e sicurezza dell&#39;utente. È più probabile che gli utenti facciano clic su collegamenti professionali con marchio, con conseguente aumento delle percentuali di click-through.

* **Ottimizzazione SEO:** gli URL che includono parole chiave rilevanti migliorano la classificazione e la reperibilità dei motori di ricerca.

* **Maggiore visibilità del brand:** Gli URL specifici del brand rafforzano la presenza del brand in tutti i canali di marketing, inclusi e-mail, social media e campagne pubblicitarie.
Inoltre, l’uso coerente degli URL di marchio in tutte le comunicazioni rafforza l’identità e il riconoscimento del marchio.

* **Tracciamento e analisi delle campagne:** utilizza URL personalizzati per diverse campagne e canali per ottenere informazioni dettagliate sulle origini del traffico e sulle prestazioni di conversione.

## Prerequisiti{#prerequisites-for-creating-vanity-id}

Per creare l&#39;URL personalizzato, assicurati di avere già [approvato le risorse per la distribuzione pubblica](/help/assets/manage-organize-assets-view.md#manage-asset-status).

## Creare URL personalizzati{#create-vanity-urls}

Per creare URL personalizzati, effettua le seguenti operazioni:
1. [Configurare i metadati delle risorse](#set-up-asset-metadata)
1. [Creare e mappare la variabile di ambiente di Cloud Manager](#map-cloud-manager-environment-variable)
1. [Approva le risorse che richiedono l’URL personalizzato per la consegna](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [Generare URL personalizzati](#generate-vanity-urls)

### Configurare i metadati delle risorse{#set-up-asset-metadata}

Per impostare il Vanity ID nel modulo dei metadati della risorsa, esegui le seguenti operazioni:
1. Passare alla pagina dei dettagli della cartella contenente le risorse per la consegna [!DNL Dynamic Media with OpenAPI].
1. [Modificare il modulo di metadati](/help/assets/metadata-assets-view.md#edit-metadata-forms) eseguendo una delle operazioni seguenti:
   * Aggiungi un nuovo campo di metadati e specifica il Vanity ID richiesto come valore di quel campo.
   * Aggiorna il campo esistente sostituendo il valore di una proprietà di metadati esistente con l’ID del reindirizzamento richiesto. Scopri le [best practice](#best-practices) per la creazione del Vanity ID.
     ![ID reindirizzamento](/help/assets/assets/vanity-id-metadata.png)
Ulteriori informazioni su [schemi metadati](/help/assets/metadata-schemas.md).

     >[!NOTE]
     >
     > * Utilizza ID personalizzati univoci per ogni risorsa. Verifica sempre che le risorse che condividono lo stesso modulo di metadati abbiano ID personalizzati per DM con distribuzione OpenAPI tramite URL personalizzati. Se due risorse condividono lo stesso ID Vanity, DM con OpenAPI distribuisce la risorsa che ha ricevuto più di recente l’ID, ignorando il diritto precedente dell’ID a un’altra risorsa.
     >
     > * Una singola risorsa può avere più ID di reindirizzamento. [Contatta il supporto Adobe](https://helpx.adobe.com/in/contact.html) e invia una richiesta per generare gli ID personalizzati richiesti.

Dopo aver impostato il tuo ID personalizzato nel modulo dei metadati della risorsa, [mappa questo campo di metadati sul meccanismo di consegna del sistema](#map-cloud-manager-environment-variable).

### Creare e mappare la variabile di ambiente di Cloud Manager{#map-cloud-manager-environment-variable}

Esegui la procedura seguente per creare una variabile di ambiente e mapparla sul campo di metadati contenente l’ID personalizzato:

1. [Passare alla pagina delle configurazioni dell&#39;ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) ed eseguire le operazioni seguenti:
   1. Aggiungi variabile `ASSET_DELIVERY_VANITY_ID`. Questa è la chiave.
   1. Utilizza il campo del valore per eseguire il mapping alla proprietà dei metadati della risorsa che contiene l’ID del reindirizzamento. La mappatura segue il formato `dc:<your-metadata-property>`, in cui il prefisso di mappatura dei metadati (ad esempio dc:) varia in base alla proprietà di configurazione dei metadati della risorsa.
      ![Variabile ASSET_DELIVERY_VANITY_ID](/help/assets/assets/environment-config.png)
1. Salva le modifiche per riavviare i pod nell’ambiente.

### Approva le risorse per la consegna{#approve-assets-for-delivery}

Dopo aver mappato la variabile `ASSET_DELIVERY_VANITY_ID` nell&#39;ambiente Cloud Manager alla proprietà dei metadati della risorsa che contiene il Vanity ID, [approva le risorse che richiedono l&#39;URL personalizzato per la consegna](/help/assets/manage-organize-assets-view.md#manage-asset-status).

### Generare URL personalizzati{#generate-vanity-urls}

Effettua le seguenti sostituzioni nell’URL di consegna standard per trasformarlo in un URL personalizzato:

* Sostituisci **UUID** con il tuo **ID reindirizzamento**.
* Sostituisci `aaid` con `avid`.

Vedi la trasformazione [URL da standard a Vanity URL](#standard-urls) sopra.
Scopri come [copiare Dynamic Media con gli URL di consegna OpenAPI](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets) per le risorse.

Quando l&#39;utente fa clic sull&#39;URL personalizzato, [!DNL Dynamic Media with OpenAPI] associa automaticamente il reindirizzamento all&#39;UUID della risorsa originale al momento dell&#39;acquisizione e lo risolve correttamente al momento della consegna per distribuire la risorsa all&#39;utente senza alcun ritardo. Puoi personalizzare il Vanity URL in tempo reale senza influire sulle prestazioni di consegna delle risorse.

[Utilizza le funzionalità avanzate di personalizzazione di AEM Cloud Service con il tuo URL personalizzato per migliorarne l&#39;impatto](#scale-using-vanity-url).

## Ridimensionare utilizzando gli URL personalizzati{#scale-using-vanity-url}

AEM as a Cloud Service ti consente di [personalizzare i nomi DNS e CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction) negli indirizzi Web. Utilizza queste funzionalità AEMCS con i tuoi URL personalizzati per trasformarli in indirizzi web univoci, puliti, descrittivi, di marca e intuitivi e fornire i [vantaggi di cui sopra](#key-benefits).

Consulta il seguente URL personalizzato e i relativi componenti personalizzabili:

**Formato URL personalizzato:**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">Personalizza DNS</a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">/</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">Personalizza URL con regole di riscrittura</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls">Crea ID reindirizzamento</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/as/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**Formato URL personalizzato con nomi DNS e CDN personalizzati:**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/as/<seoname>.<format>`

**Componenti URL personalizzabili**

* ***[Nome DNS (nome host):](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com` è il dominio del server che ospita le risorse. [Personalizzare il DNS per modificare il nome host](#customize-DNS).
* ***[Regole di riscrittura CDN:](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:` è la struttura del percorso che identifica i tipi di risorse e i metodi di consegna. [Riscrivi regole CDN](#rewrite-cdn-rules) per modificare il percorso del dominio.

### Personalizza DNS{#customize-dns}

[Invia una richiesta al supporto Adobe](https://helpx.adobe.com/in/contact.html) per generare il DNS personalizzato richiesto per il livello di consegna. Segui queste [best practice](#best-practices) per la creazione di nomi DNS personalizzati.

### Riscrivi regole CDN{#rewrite-cdn-rules}

Esegui la procedura seguente per riscrivere le regole CDN per la consegna:

1. Passa al tuo archivio AEM per creare un file di configurazione YAML.
2. Esegui i passaggi della sezione [setup](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup) per configurare le regole CDN e distribuire la configurazione tramite la pipeline di configurazione di Cloud Manager.
Segui queste [best practice](#best-practices) per creare il percorso del dominio.
   [Ulteriori informazioni sulle regole di riscrittura CDN](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations).

Di seguito sono riportati alcuni esempi di regole di riscrittura per l’aggiunta di nomi di file con estensioni negli URL personalizzati. Personalizza queste regole di riscrittura in base ai tuoi requisiti specifici. [Contatta il supporto Adobe](https://helpx.adobe.com/in/contact.html) per ulteriore assistenza:

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### Per SVG, GIF e PDF {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### Per video{#video}

Per video quali MP4, MOV, AVI e MKV

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### Per immagine{#image}

Per tutti i tipi di immagini, escluso SVG.

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## Segui le best practice per creare URL personalizzati puliti{#best-practices}

Segui queste best practice per creare [ID reindirizzamento](#create-vanity-urls), [DNS personalizzati](#customize-dns) e [nomi CDN](#rewrite-cdn-rules):

1. Non utilizzare caratteri speciali negli ID personalizzati, ad esempio spazi, barre, trattini e altro ancora. Il sistema sostituisce i caratteri speciali negli ID personalizzati utilizzando una mappatura predefinita.
1. Utilizza il tuo nome commerciale, i nomi dei prodotti e le parole chiave pertinenti nei tuoi [ID visitatore](#create-vanity-urls), [nomi DNS personalizzati](#customize-dns) e [nomi CDN](#rewrite-cdn-rules) per migliorare la visibilità del tuo marchio e il coinvolgimento degli utenti.
1. Utilizza parole brevi e descrittive o stringhe che trasmettono significato.
1. Utilizza i testi che invitano gli utenti ai clic.
