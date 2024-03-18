---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b0198fee3fb8c2f02f50819bea5757e5b8373ac1
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 87%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15262 {#release-15262}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15262, rilasciata al pubblico il 6 marzo 2024. La versione di manutenzione precedente era 14697.

Con l’attivazione delle funzioni 2024.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-15262}

* ASSETS-30632: è stata aggiunta una colonna separata dello stato di pubblicazione di Brand Portal nella vista a elenco.
* ASSETS-30934: è stato aggiunto il supporto per le proprietà `Iptc4xmpCore:AltTextAccessibility` e `Iptc4xmpCore:ExtDescrAccessibility` nell’editor dei metadati delle risorse.
* ASSETS-31297: migliora i controlli per impedire l’eliminazione delle risorse copiate da Dynamic Media.
* ASSETS-33246: definizione dell’indice di rilascio `damAssetLucene-10`.
* ASSETS-33590: è stato aggiunto il supporto per le rappresentazioni web dei video nei profili di elaborazione.
* GRANITE-36205: aggiorna la versione oak a 1.60-T20240131102219-0cde853.
* SITES-19326: aggiorna i collegamenti nell’interfaccia utente di Assets per aprire CF nel nuovo editor CF.
* GUIDES-12945: suggerimenti avanzati basati sull’intelligenza artificiale per aggiungere riferimenti ai contenuti durante la creazione di quest’ultimi
* GUIDES-12706: è stata rinnovata la funzione di cronologia delle versioni nell’editor web
* GUIDES-14948: è stata migliorata l’esperienza utente nel pannello Traduzione
* GUIDES-8782: è stata migliorata la logica di ricerca nella finestra di dialogo Inserisci elemento
* GUIDES-14681: possibilità di pubblicare più predefiniti di output con linee di base dinamiche
* Per l’elenco completo dei miglioramenti apportati alle Guide AEM, consulta: [Novità delle guide AEM](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=it#release-info)

### Problemi risolti {#fixed-issues-15262}

* ASSETS-15977: rimuovi gli eventi di ricerca v1 obsoleti e il produttore della pipeline.
* ASSETS-18088: aggiorna le dipendenze della libreria batik alla versione 1.17.
* ASSETS-21965: il flusso di lavoro di write-back dei metadati deve essere avviato solo in caso di modifiche ai metadati delle risorse.
* ASSETS-26368: i processi di importazione in blocco pianificati non vengono rimossi se non esiste una configurazione dei processi.
* ASSETS-26549: risorse/nodi con “jcr:lastModifiedBy”: “workflow-process-service” mostrano “utente esterno” nella vista a elenco.
* ASSETS-26842: aggiorna il testo “Firefly” per leggere “App Builder” nel profilo di elaborazione.
* ASSETS-28708: risposta molto lenta per alcune richieste di token IMS.
* ASSETS-28767: stato di pubblicazione incoerente sulle risorse se la cartella contiene un numero elevato di risorse pubblicate.
* ASSETS-29011: il ritaglio avanzato è visibile per gli utenti di sola lettura.
* ASSETS-29348: AssetMoveEventHandler può consumare troppa memoria.
* ASSETS-29738: la limitazione del caricamento delle risorse non riesce con NullPointerException per i file woff.
* ASSETS-30068: importa in blocco Asset Essentials per includere lo stato COMPLETED_WITH_ERROR per “processo completato, ma con errore”.
* ASSETS-30261: imsUserId non corretto inviato alla pipeline per gli eventi delle risorse.
* ASSETS-30538: opzione Visualizza pagina mancante dopo lo spostamento di un file PDF.
* ASSETS-30626: impossibile creare la richiesta di consegna segnalata per le risorse con assetId vuoto.
* ASSETS-30756: l’azione della procedura guidata Sposta risorsa non riesce se il nome della cartella termina in “html”.
* ASSETS-30810: sanitizza i tag prima di eseguire il rendering della configurazione precedente di YouTube.
* ASSETS-31015: impossibile caricare le risorse con estensione msg.
* ASSETS-31038: gli eventi di attività ricevuti dal servizio di notifica non vengono elaborati.
* ASSETS-31097: disabilitata la copia asincrona per il contenuto WCM per evitare avvisi di query trasversali.
* ASSETS-31256: Le risorse/nodi con &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; mostrano “utente esterno” nella vista a elenco.
* ASSETS-31260: il campo a discesa Modulo metadati risorse non funziona correttamente se il JSON del menu a discesa contiene un elenco voluminoso.
* ASSETS-31280: quando vengono aggiunte a una raccolta, le risorse vengono scaricate in una struttura semplificata.
* ASSETS-31301: un’istanza di `dynamicmedia_sly.js` non può essere creata correttamente dall’API Use.
* ASSETS-31330: ko_KR: stringhe non localizzate nei sottotitoli e nelle tracce audio.
* ASSETS-31405: l’elaborazione del server InDesign non riesce per i layout InDesign di grandi dimensioni.
* ASSETS-31570: Unified Shell: è necessario premere più di una volta i pulsanti “Salva e chiudi” e “Annulla” per funzionare in dettagli risorsa.
* ASSETS-31673: importazione in blocco non riuscita per file di Dropbox di grandi dimensioni.
* ASSETS-32108: AEM Assets non salva le dimensioni della scheda definite dall’utente nelle impostazioni di visualizzazione.
* ASSETS-32230: aggiornamento della versione runtime minima del bundle com.adobe.aem.repoapi.
* ASSETS-32544: il processo di esportazione dei metadati ha esito negativo a intermittenza.
* ASSETS-32679: problemi relativi alla memorizzazione in cache delle anteprime di risorsa (PDF).
* ASSETS-32754: le attività non possono essere assegnate a utenti che non hanno precedentemente effettuato l’accesso.
* ASSETS-32755: configura l’argomento del processo com/adobe/cq/dam/assetmove per utilizzare una coda ordinata.
* ASSETS-32899: la ricerca all’interno delle raccolte è estremamente lenta.
* ASSETS-33098: il &quot;predicato tag&quot; dei facet di ricerca AEM Assets non funziona come previsto.
* ASSETS-33454: l’attività di revisione attività e i commenti non vengono visualizzati nella timeline.
* ASSETS-34088: l’anteprima PDF non funziona su AEM Assets.
* ASSETS-34155: Dynamic Media: sono stati aggiornati i visualizzatori AEM/2024.1.0.
* ASSETS-34684: gestisce dc:title multivalore nella struttura del contenuto.
* ASSETS-34789: risolve i problemi di normalizzazione nella verifica dei conflitti dei nomi file.
* DXML-13276: guide AEM: integrati gli indici in GraniteContent e rimossi dalla libreria.
* GRANITE-47995: le operazioni di eliminazione possono non riuscire a causa di conflitti con la proprietà “cq:isDelivered”.
* GRANITE-48079: abilita le richieste POST per la convalida dei token online OAuth.
* GRANITE-48143: aggiornamento di org.apache.sling.resourcemerger alla versione 1.4.4.
* GRANITE-49031: aggiornamento a Jackson 2.16.1.
* SCRNS-3961: Schermi - Canale sequenza: l’animazione Jquery utilizzata nella transizione Dissolvenza porta alla schermata nera.
* SITES-15868: migliori prestazioni per l’elenco dei frammenti.
* SITES-16079: `/fragments/{id}/references` ha iniziato a restituire duplicati.
* SITES-16118: se a un frammento viene applicata la patch e nel modello manca un campo frammento, viene generata un’eccezione.
* SITES-16121: il recupero di un campo data del modello genera un’eccezione.
* SITES-16207: l’operazione POST /adobe/sites/cf/models restituisce due diversi codici di stato OK.
* SITES-17361: reincorpora Jsoup nel bundle headless sites.
* SITES-17768: GraphQL genera l’URL Dynamic Media per le risorse a cui si fa riferimento nei frammenti di contenuto.
* SKYOPS-66622:arresto anomalo in loop della distribuzione dell’authoring dopo l’esecuzione di una pipeline abilitata buildTransform.
* SKYOPS-69977: Adaptive Image Servlet non carica l’immagine dopo l’ultimo aggiornamento.
* GUIDES-15045: il controllo ortografico nell’editor non consente di selezionare suggerimenti.
* GUIDES-14968: il pulsante di navigazione globale non funziona e la dashboard non viene caricata.
* GUIDES-14943: nella pubblicazione di PDF nativi, gli attributi personalizzati nei predefiniti di condizione non funzionano per la pubblicazione PDF nativa.
* GUIDES-15085: nella pubblicazione di PDF nativi, i riferimenti chiave non vengono risolti per la versione di dicembre 2023 delle Adobe Experience Manager Guides.
* GUIDES-13486: i file del **Filtro linea di base** non funzionano con Nome file nell’editor web.
* Per l’elenco completo dei problemi risolti in AEM Guides, consulta: [Problemi risolti in AEM Guides](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=it#release-info)

### Problemi noti {#known-issues-15262}

* ASSETS-35923: `UnsupportedClassVersionError` Passaggio della build della pipeline in CM dopo l’aggiornamento `aem-sdk-api` versione in `2024.2.15262.20240224T002940Z-231200`. **Richiede l&#39;azione del cliente per impostare CM Java Version su 11**, vedi [Ambiente di build/Impostazione della versione JDK di Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)
* ASSETS-35860: conversione errata del fuso orario nella vista a colonne di AEM Assets.
* SCRNS-4171: gli schermi di Windows diventano vuoti e non funzionano più quando si esegue l’aggiornamento a 15262 e si pubblica un canale.
* GRANITE-50774: GraniteContent deve utilizzare l’ordine deterministico dei valori proprietà al momento dell’avvio.

### Notifica di modifica {#change-notice-15262}

**Azioni richieste**

#### Imposta versione Java CM su 11 {#set-java-version-11}

La nuova versione di aem-sdk-api contiene classi compilate con una destinazione Java 11, che non è compatibile con l’ambiente di build predefinito di Cloud Manager versione 1.8 di JDK. Questo aggiornamento richiede che Maven venga eseguito utilizzando JDK 11.

Si consiglia ai clienti di aggiungere una `.cloudmanager/java-version` nella directory principale del relativo archivio Git con il contenuto: `11`. [Ambiente di build/Impostazione della versione JDK di Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)

#### Aggiorna client-test-cloud-aem alla versione 1.2.1 {#update-aem-cloud-testing-clients}

Le prossime modifiche richiederanno la libreria [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) utilizzata nei test funzionali personalizzati per l’aggiornamento almeno alla versione **1.2.1**

Assicurati che la dipendenza in `it.tests/pom.xml` sia stata aggiornata.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Questa modifica deve essere eseguita prima del 6 aprile 2024.

Se non si aggiorna la libreria di dipendenze, si verificheranno errori di pipeline nel passaggio &quot;Test funzionale personalizzato&quot;.

### Tecnologie incorporate {#embedded-tech-15262}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=it) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
