---
title: Risoluzione dei problemi in AEM Assets
description: Risolvi i problemi più comuni relativi ad AEM Assets utilizzando i collegamenti agli articoli per le aree chiave di AEM Assets s=ad esempio caricamenti, metadati, ricerca, consegna e così via.
hidefromtoc: true
hide: true
source-git-commit: c8f1c40e4300b26141cc394a9208641769da1f1e
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# Risoluzione dei problemi di AEM Assets {#troubleshoot-aem-assets}

AEM Assets as a Cloud Service offre una soluzione PaaS nativa per il cloud, che consente alle aziende non solo di eseguire le operazioni di gestione delle risorse digitali e Dynamic Media, ma anche di utilizzare funzionalità intelligenti di nuova generazione, come AI/ML. Il tutto all&#39;interno di un sistema sempre attuale, sempre disponibile e sempre in apprendimento.

Tuttavia, possono sorgere problemi che riguardano il caricamento di risorse, i metadati, la ricerca o la consegna e altre aree chiave di AEM Assets. Questo articolo descrive i passaggi per la risoluzione dei problemi utili per diagnosticare e risolvere i problemi più comuni di AEM Assets.

<table>
  <tbody>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27140">Rappresentazioni mancanti nel file ZIP di download delle risorse in AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">Frammenti di contenuto non inclusi nella licenza AEM Assets</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">Commento limitato nella visualizzazione Assets nonostante l'accesso in lettura</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715">(Dynamic Media) Set 360 gradi bloccato nello stato di elaborazione in AEM Dynamic Media</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">Le copie trasformate di Digital Asset Management (DAM) non corrispondono ai file originali in AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">Rendering ritaglio avanzato non generato in AEMaaCS</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">(Dynamic Media) Correggi i problemi di caricamento, elaborazione e rendering di video in AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">(Asset Link) Adobe Asset Link lascia i collegamenti in uno stato inaccessibile quando si utilizza InDesign</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">Mancata corrispondenza della miniatura video tra Dynamic Media e la vista a schede DAM in AEMaaCS</a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">Elaborazione delle risorse non riuscita per file MP4 di grandi dimensioni in AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">(Dynamic Media) Il lettore video Dynamic Media non funziona negli ambienti inferiori</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26103">(Dynamic Media con OpenAPI) Attiva l’accesso limitato di Assets a Dynamic Media con API aperte basate sui gruppi di utenti IMS</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">Quando un file Tiff con formato di compressione ZIP viene caricato in AEM Assets, non vengono generate rappresentazioni</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM tronca il testo estratto da PDF di grandi dimensioni dopo 100.000 token</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">(Dynamic Media) Modifica dell’URL di Dynamic Media per DM Assets</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">Risoluzione dei problemi di visibilità dello schema metadati per gli utenti non amministratori in AEMaaCS</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">(Dynamic Media) Problema di modifica del colore di sfondo per le rappresentazioni di immagini TIFF in Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">Il problema di rotazione delle risorse AEMaaCS rende invisibili le rotazioni successive</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">(Dynamic Media) Risoluzione del problema di immagine danneggiata con Smart Crop in Adobe Experience Manager 6.5 Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">Aumento del limite di caricamento delle risorse in una singola parte per l’integrazione API di Photoshop Firefly</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">(Dynamic Media) Risolvi le discrepanze nei nomi delle risorse Dynamic Media negli ambienti AEM per i file PDF</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">Alcune immagini non mostrano le rappresentazioni delle miniature in Adobe Experience Manager (AEM) as a Cloud Service - Asset</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">(Dynamic Media) La pagina Impostazioni generali di Dynamic Media non si apre</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">(Dynamic Media) Risoluzione dei problemi audio nei file video con Dynamic Media in AEM</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">Assegnazione automatica di tag alle nuove risorse caricate in AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">La funzionalità Tag avanzati non funziona dopo la migrazione da JWT a OAuth in AEM</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">Risolvere i problemi relativi ai collegamenti condivisi in AEM Managed Services</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25607">(Dynamic Media) Errore di elaborazione delle risorse in AEM Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">(Dynamic Media) Errore di sincronizzazione delle risorse in Adobe Experience Manager (AEM) Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">Aggiornamento delle miniature personalizzate per le risorse video in AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Discrepanza nei metadati delle immagini in Adobe Experience Manager (AEM) Assets</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">Il trascinamento della selezione di una cartella di risorse nell’interfaccia utente web di AEM Assets non riesce</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">(Dynamic Media) Risoluzione dei problemi di elaborazione delle risorse in AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Limitazioni dell’estrazione del testo per PDF di grandi dimensioni in Adobe Experience Manager as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">(Asset Link) Risoluzione dei problemi di connessione dei collegamenti alle risorse di Adobe Experience Manager (AEM) in InDesign</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">(Asset Link) Errore di rete del plug-in Adobe Asset Link: server non raggiungibile</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">Raccomandazioni utente per la sincronizzazione di Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">(Dynamic Media) Esportazione di risorse e metadati da Dynamic Media tramite API</a></td>
  <td></td>
</tr>

</tbody>
  <table>


