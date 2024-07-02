---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fd687498a8c72bf5d47b7b97aadf22d7d1e8dd2b
workflow-type: ht
source-wordcount: '649'
ht-degree: 100%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 16799 {#release-16799}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 16799, rilasciata pubblicamente il 18 giugno 2024. La versione di manutenzione precedente era 16544.

Con la versione di attivazione funzioni 2024.6.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-16799}

* ASSETS-31977: ottimizzazione delle operazioni di spostamento, copia ed eliminazione delle risorse.
* ASSETS-33618: trascrizione automatica e funzionalità di traduzione per video in Dynamic Media.
* ASSETS-35185: azione di approvazione per ContentHub e DM e aggiunta di proprietà alle proprietà damAssetLucene.
* ASSETS-35533: aggiunta di proprietà DRM e CAI all’indice damAssetLucene.
* ASSETS-37280: gestione dei processi sequenziali per la traduzione quando il sottotitolo sorgente (vtt) è ancora in elaborazione.
* ASSETS-37559: è stato migliorato l’evento risorsa eliminata.
* ASSETS-37723: è stato implementato l’evento risorsa pubblicata.
* ASSETS-37724: è stato implementato l’evento annullamento pubblicazione della risorsa.
* ASSETS-38614: miglioramenti all’interfaccia utente Condividi collegamento.
* ASSETS-39601: viene applicato automaticamente il regex di convalida al nome della Live Copy della risorsa.
* ASSETS-39454: aggiornamento a viewers 2024.5.0 in Quickstart.
* CNTBF-184: percorsi di supporto sotto `/conf` nel ritorno di contenuto.

### Problemi risolti {#fixed-issues-16799}

* ASSETS-37335: la Modifica del Pannello di ricerca nel filtro deseleziona tutte le caselle.
* ASSETS-38069: problema di anteprima del PDF DAM di AEM nella selezione del filtro della timeline.
* ASSETS-38215: il pulsante della licenza di Adobe Stock è disabilitato in AEM as a Cloud Service per l’abbonamento Enterprise.
* ASSETS-38578: collegamenti ipertestuali errati nel rapporto Condivisione collegamenti risorse.
* ASSETS-38678: impostazioni di visualizzazione non funzionanti in Dettagli raccolta.
* ASSETS-39071: la consegna ottimizzata per il web può generare un’eccezione se il tipo mime della rappresentazione originale è nullo.
* ASSETS-39316: l’ordinamento per nome non funziona nelle raccolte.
* ASSETS-39377: l’importazione in blocco da OneDrive potrebbe non riuscire quando si riceve backpressure dall’API remota.
* ASSETS-39428: problemi di rendering nell’interfaccia utente per la gestione dei copyright.
* CQ-4357150: Guava nel bundle cq-content-sync.
* GRANITE-52573: le richieste contenenti una doppia barra `//` vengono rifiutate con il codice di stato 400.
* SCRNS-4194: rimuovere la dipendenza dalle API Guava di Google.
* SCRNS-4360: Pulsante Gestisci pubblicazione e pubblicazione rapida mancante per gli utenti non amministratori nel provider di contenuti per i canali.
* SCRNS-4323: nasconde/disabilita i lanci da screens.html.

### Problemi noti {#known-issues-16799}

>[!NOTE]
> Il team dei tecnici AEM ha identificato una regressione della funzionalità Lanci che influisce sulle versioni di AEM correnti a partire dalla 16461. A causa di questa regressione, i nuovi lanci (creati dopo l’applicazione di nuove versioni) che includono pagine non profonde non verranno promossi correttamente a causa di configurazioni mancanti.
> Se i tuoi ambienti sono interessati da questo problema, puoi richiedere all’Assistenza clienti di fornirti uno script shell per identificare e aggiornare le configurazioni mancanti (riferimento interno SITES-22457).
> Sarà resa disponibile una correzione a lungo termine che garantirà la creazione di nuovi lanci con tutte le configurazioni corrette. Fino ad allora, è disponibile su richiesta anche una versione patch interna.

#### Moduli

1. Se un utente scarica la versione di AEM Forms SDK maggiore di `AEM Forms add-on v2024.05.04.00-240400`, il file batch non riesce ad avviare il servizio Docker. Per risolvere questo problema:
   1. Scarica la [cartella](/help/forms/assets/sdk_hotfix.zip).
   1. Estrai il contenuto dalla cartella scaricata e copia i file `sdk.sh` e `sdk.bat`.
   1. Sostituisci i file esistenti `sdk.sh` e `sdk.bat` in AEM Forms SDK con i nuovi file.

### Notifica di modifica {#change-notice-16799}

* Questa versione contiene le seguenti nuove versioni dell’indice del prodotto:
   * **damAssetLucene-11**
   * **fragments-11**

  Eventuali versioni personalizzate delle precedenti versioni dell’indice verranno unite automaticamente alla nuova versione dell’indice del prodotto. Dovrai applicare ulteriori aggiornamenti personalizzati alla versione unita.

* A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-16799}

Per sapere cosa è obsoleto o è stato rimosso in AEM as a Cloud Service, consulta [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-16799}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak API 1.64.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
