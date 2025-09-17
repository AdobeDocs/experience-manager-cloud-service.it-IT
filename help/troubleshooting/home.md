---
title: Risoluzione dei problemi in AEM Assets e Forms
description: Risolvi i problemi più comuni relativi a AEM Assets e Forms utilizzando i collegamenti agli articoli per aree chiave, come caricamenti, metadati, ricerca, consegna, creazione di moduli, invio e integrazione.
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---


# Risoluzione dei problemi di AEM Assets e Forms {#troubleshoot-aem-assets-forms}

AEM as a Cloud Service offre soluzioni complete per la gestione delle risorse digitali tramite AEM Assets e potenti funzionalità di creazione di moduli tramite AEM Forms. Entrambi i servizi forniscono soluzioni PaaS native per il cloud con funzionalità intelligenti di nuova generazione, come AI/ML, il tutto all’interno di un sistema sempre attuale, disponibile e in grado di apprendere.

Tuttavia, gli ambienti aziendali complessi possono incontrare varie difficoltà tecniche in aree diverse.

Questa guida completa alla risoluzione dei problemi fornisce approcci diagnostici sistematici, soluzioni suddivise in categorie e percorsi di risoluzione dettagliati per AEM Assets e Forms. Ogni sezione include guide di riferimento rapido, metodologie dettagliate per la risoluzione dei problemi e collegamenti esaurienti alle risorse per aiutarti a risolvere in modo efficiente i problemi e ottimizzare il tuo ambiente AEM Cloud Service.

## Risoluzione dei problemi di AEM Assets {#aem-assets-troubleshooting}

AEM Assets semplifica la gestione, l’organizzazione e la distribuzione delle risorse digitali in più esperienze. Tuttavia, possono sorgere problemi che influiscono su caricamenti di risorse, metadati, integrazioni o distribuzione. Questo articolo descrive i passaggi per la risoluzione dei problemi utili per diagnosticare e risolvere i problemi più comuni di AEM Assets. Seguendo queste indicazioni, puoi ripristinare i flussi di lavoro in modo efficiente e garantire che le risorse rimangano accessibili, precise e pronte per l’uso su tutti i canali.

### Elaborazione risorse e rappresentazioni {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Caricamento ed elaborazione</strong></td>
    <td><strong>Rappresentazioni</strong></td>
    <td><strong>PDF ed estrazione testo</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">Elaborazione delle risorse non riuscita per file MP4 di grandi dimensioni in AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">Le rappresentazioni DAM non corrispondono ai file originali</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM tronca il testo estratto da PDF di grandi dimensioni dopo 100.000 token</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">Il file Tiff con caricamenti di compressione ZIP non genera rappresentazioni</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">Le immagini non mostrano le rappresentazioni delle miniature in AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Limitazioni dell’estrazione del testo per PDF di grandi dimensioni in AEM as a Cloud Service</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">Il trascinamento della selezione di una cartella di risorse nell’interfaccia utente web di AEM Assets non riesce</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">Il problema di rotazione delle risorse rende invisibili le rotazioni successive</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">Aumento del limite di caricamento delle risorse in una singola parte per l’integrazione API di Photoshop Firefly</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamic Media {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Video</strong></td>
    <td><strong>Set 360 gradi e ritaglio avanzato</strong></td>
    <td><strong>Consegna e impostazioni</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">Correggi i problemi di caricamento, elaborazione e rendering dei video in AEM</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715">Set 360 gradi bloccati nello stato di elaborazione</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">Modifica dell’URL di Dynamic Media per le risorse</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">Miniatura video non corrispondente tra Dynamic Media e Vista scheda DAM</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">Rendering ritaglio avanzato non generato in AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">Problema di immagine interrotta con Ritaglio avanzato in AEM 6.5</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">Errore di elaborazione delle risorse in AEM Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">Problema relativo al colore di sfondo per le rappresentazioni di TIFF</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">La pagina Impostazioni generali di Dynamic Media non si apre</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">Risoluzione dei problemi audio nei file video con Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">Errore di sincronizzazione risorse in Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">Risolvere le discrepanze nei nomi delle risorse tra gli ambienti</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">Il lettore video Dynamic Media non funziona negli ambienti inferiori</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">Raccomandazioni utente per la sincronizzazione Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">Esportare risorse e metadati da Dynamic Media tramite API</a></td>
  </tr>
  </tbody>
</table>

### Metadati, assegnazione di tag e condivisione {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Metadati</strong></td>
    <td><strong>Tag avanzati</strong></td>
    <td><strong>Accesso e condivisione</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Discrepanza nei metadati delle immagini in AEM Assets</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">Assegnazione automatica di tag alle nuove risorse caricate</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">Commenti limitati nella visualizzazione Assets nonostante l’accesso in lettura</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">Risoluzione dei problemi di visibilità dello schema metadati per gli utenti non amministratori</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">I tag avanzati non funzionano dopo la migrazione da JWT a OAuth</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">Risolvere i problemi relativi ai collegamenti condivisi in AEM Managed Services</a></td>
  </tr>

</tbody>
</table>

### Integrazioni e accesso {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Asset Link</strong></td>
      <td><strong>Licenze e personalizzazioni</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe Asset Link lascia i collegamenti inaccessibili in InDesign</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">Frammenti di contenuto non inclusi nella licenza AEM Assets</a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">Risoluzione dei problemi di connessione ad AEM Asset Link in InDesign</a></td>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">Risoluzione dei problemi di elaborazione delle risorse in AEM as a Cloud Service</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">Errore di rete del plug-in Adobe Asset Link: server non raggiungibile</a></td>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">Aggiornamento miniature personalizzate per risorse video in AEM as a Cloud Service</a>
      </td>
    </tr>
  </tbody>
</table>




## Risoluzione dei problemi di AEM Forms {#aem-forms-troubleshooting}

AEM Forms as a Cloud Service fornisce potenti funzionalità di creazione e gestione dei moduli. Tuttavia, potrebbero verificarsi problemi durante l’installazione, la configurazione, la creazione di moduli o i processi di invio. Questa sezione fornisce indicazioni complete sulla risoluzione dei problemi per i problemi più comuni di AEM Forms.

### Problemi di installazione e configurazione

<table>
  <tbody>
  <tr>
    <td><strong>Configurazione e configurazione</strong></td>
    <td><strong>Problemi relativi alla creazione di moduli</strong></td>
    <td><strong>Prestazioni e memorizzazione in cache</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">Opzione Forms non disponibile in Navigazione</a></td>
    <td><a href="/help/forms/form-creation-failing.md">La creazione del modulo non riesce dopo la pubblicazione del modello</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">Problemi di caching adattivo di Forms</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">Genera errori di pipeline</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">Problemi relativi alla sequenza di pubblicazione dei modelli</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Problemi di invalidamento della cache di Dispatcher</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">Problemi di attivazione del bundle</a></td>
    <td><a href="/help/forms/known-issues.md">Limitazioni note della creazione di moduli</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">Errori di caching CDN</a></td>
  </tr>
  </tbody>
</table>

### Problemi relativi all’invio dei moduli e all’integrazione

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>Azioni di invio personalizzate</strong></td>
    <td><strong>Problemi di integrazione</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403 Errori non consentiti nell’invio del modulo</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">502 errori nelle azioni di invio personalizzate</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27434">Errori di reindirizzamento DRM-SAML</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">Problemi di configurazione CORS</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">Gestione delle eccezioni non gestite</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27075">Pulsante Invia disabilitato in AEM Sites</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">Configurazione filtro referrer</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">Best practice per le azioni personalizzate</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26532">Visibilità dei campi nascosti dopo gli aggiornamenti</a></td>
  </tr>
  </tbody>
</table>

### Problemi relativi a Designer e sviluppo

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>Ambiente di sviluppo</strong></td>
    <td><strong>Versione e compatibilità</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26558">Designer 6.5 non si apre dopo l’aggiornamento</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27089">I localizzatori non iniziano con JDK 8/11</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26862">Problemi di visualizzazione della versione del pacchetto AEM Forms (AEMFD)</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21018">Errori PDF Generator JPEG 2000</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-22689">Configurazione percorso registro JBoss</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26846">Numeri di versione errati in Windows</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27406">Pulsante mancante nell’output di PDF</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-18084">Errori di aggiornamento di Configuration Manager</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17339">Soluzioni alternative per il danneggiamento dell’indice</a></td>
  </tr>
  </tbody>
</table>



