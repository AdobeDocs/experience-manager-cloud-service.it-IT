---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e7e565556b382a662fb8afc5aadaa26d2357e294
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 11%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 14157 {#release-14157}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 14157, rilasciata pubblicamente il 7 novembre 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 14029.

L’attivazione delle funzioni 2023.11.0 fornirà il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-14157}

* ASSETS-29631: Assets Cloud: utilizza dam:roles per una consegna/ricerca sicura.
* CQ-4354515: Traduzioni: opzione per eliminare la traduzione delle risorse di riferimento.
* FORMS-9993: definisci i passaggi per spostare i Componenti core Forms in Skyline.
* FORMS-10570: onboarding delle API EC in API - Primo router.
* GRANITE-48143: Aggiornare Sling ResourceMerger alla versione 1.4.4.
* SITES-14874: Evento: espandere la struttura CFM per gli eventi modello per includere le modifiche ai metadati.
* SITES-2719: Frammenti di contenuto: supporto dei tag per le varianti di frammenti di contenuto (riattivato).
* SITES-3619: Frammenti di contenuto: output dei tag di variante CF di GraphQL in JSON e filtro per tag di variante (riabilitato).
* SITES-13750: Frammenti di contenuto: elimina i tag per un modello per frammenti di contenuto.
* SITES-13920: Frammenti di contenuto: supporto per la configurazione minItems per più campi (pre-release).
* SITES-14080: Frammenti di contenuto: elimina il tag di una variante di frammento di contenuto.
* SITES-14770: Frammenti di contenuto: la variante di frammento deve includere la proprietà fieldTags.
* SITES-15356: Frammenti di contenuto: quando viene creata una risorsa, viene restituito il tag e come intestazione di risposta.
* SITES-15357: Frammenti di contenuto: consenti la pubblicazione di frammenti senza i relativi riferimenti.
* SITES-15938: Frammenti di contenuto: metadati di riferimento al contenuto mancanti.
* SITES-16078: Frammenti di contenuto: inserisci la proprietà del risultato di convalida della variante quando viene recuperato un frammento.
* SITES-16545: Frammenti di contenuto: aggiungi un endpoint per recuperare i riferimenti della variante di un frammento di contenuto.
* SITES-16853: Frammenti di contenuto: Rimuovi /adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags.

### Problemi risolti {#fixed-issues-14157}

* Vari problemi di accessibilità risolti
* ASSETS-31015: impossibile caricare i file in Assets con estensioni sconosciute.
* ASSETS-24739: disabilita l’endpoint per azioni personalizzate Frame.io alla pubblicazione.
* CMGR-49845: Backflow del contenuto: problema con l’identificazione del percorso principale corretto per un determinato punto di controllo.
* CMGR-49709: Backflow del contenuto: aggiorna il filtro delle proprietà per ignorare altre proprietà.
* CQ-4354503: la configurazione Adobe IMS viene rimossa in modo casuale.
* CQ-4354414: ConfigurationReplicationEventHandler crea molte singole azioni di scaricamento.
* CQ-4354401: Traduzioni: le risorse create dai progetti devono essere salvate prima di iniziare l’elaborazione delle risorse.
* CQ-4354430: Traduzioni: ottenimento di un errore durante l’aggiunta di risorse non appartenenti a una struttura di cartelle per lingue a un progetto di traduzione.
* CQ-4354412: Traduzioni: l’eliminazione del contenuto del processo di traduzione non comporta l’eliminazione di tutto il contenuto di riferimento.
* CQ-4354636: Traduzioni: la creazione di una copia per lingua a livello di directory principale della lingua non regola i percorsi nella pagina.
* CQ-4354700: Flussi di lavoro: la schermata del payload del flusso di lavoro non si carica.
* CQ-4354834: Flussi di lavoro: impossibile aggiungere commenti nell’attività casella in entrata del flusso di lavoro.
* FORMS-11302: il titolo del componente modificato nell’editor Rich Text non viene visualizzato correttamente in Editor moduli adattivi > Editor regole.
* GRANITE-45706: l’importazione di i18n non riesce se il valore chiave ha &quot;Äú&quot;).
* SITES-14156: Evento: gli eventi di pubblicazione non vengono sempre inviati.
* SITES-14520: GraphQL: prestazioni non valide con query graphql impaginate a causa di FT_SITES-2719.
* SITES-16444: GraphQL: DataFetchingException per campi con lo stesso nome mancanti nella query GraphQL.
* SITES-16225: GraphQL: i tipi di contenuto dei campi RTE di modello e frammento restituiti dall’API Java non sono corretti.
* SITES-15373: Frammenti di contenuto: The /adobe/sites/cf/fragments/{fragmentId}/variation/{name}L&#39;endpoint /tags non utilizza le convenzioni di denominazione delle risorse corrette.
* SITES-15709: Frammenti di contenuto: problema di creazione dell’endpoint modello durante la creazione di un campo booleano.
* SITES-15727: Frammenti di contenuto: il campo di tipo &quot;Tag&quot; può essere aggiunto una sola volta nell’editor modelli.
* SITES-15782: Frammenti di contenuto: proprietà univoca mancante dal modello di campo di tipo Enumerazione.
* SITES-15786: Frammenti di contenuto: impossibile creare un frammento di contenuto nella cartella contenente &quot;.
* SITES-15790: Frammenti di contenuto: intestazione Aggiorna posizione per la creazione di versioni.
* SITES-15923: Frammenti di contenuto: l’amministratore CF non mostra tutte le cartelle.
* SITES-15987: Frammenti di contenuto: ottenere 500 durante la creazione della variante.
* SITES-16067: Frammenti di contenuto: non è possibile modificare il tipo mime del campo del frammento di testo lungo.
* SITES-16074: Frammenti di contenuto: applica tag ai campi che non sono stringhe[] non può essere recuperato da JCR.
* SITES-16079: Frammenti di contenuto: /fragments/{id}/references ha iniziato a restituire duplicati.
* SITES-16118: Frammenti di contenuto: se a un frammento viene applicata la patch e manca un campo frammento nel modello, viene generata un’eccezione.
* SITES-16119: Frammenti di contenuto: se i metadati del frammento contengono campi non riconosciuti, viene generata un’eccezione.
* SITES-16121: Frammenti di contenuto: il recupero di un campo data modello genera un’eccezione.
* SITES-16123: Frammenti di contenuto: se una risorsa non è un frammento di contenuto, l’endpoint get fragments genera un’eccezione.
* SITES-16208: Frammenti di contenuto: ContentFragmentModelIdentifier espone una proprietà di titolo fuorviante.
* SITES-16707: Frammenti di contenuto: i tipi di dati dei Modelli per frammenti di contenuto non vengono letti correttamente.
* SITES-16818: Frammenti di contenuto: esegui l’eliminazione solo se sono presenti tag.
* SITES-16207: Frammenti di contenuto: l’operazione POST /adobe/sites/cf/models restituisce due diversi codici di stato OK.
* SITES-15616: Frammenti di contenuto: l’endpoint Publish a volte non pubblica tutti i riferimenti di un frammento di contenuto.
* SITES-16027: Frammenti di contenuto: le informazioni di riferimento sulla variante non sono presenti nella risposta del frammento.
* SITES-16243: Frammenti di contenuto: Trova e sostituisci non funziona con campi con Rendering come: Multiplo.
* SITES-16250: Frammenti di contenuto: l’applicazione di patch a una CF talvolta restituisce un’intestazione etag non corretta.
* SITES-16686: Frammenti di contenuto: i riferimenti non di frammento di frammento di contenuto vengono serializzati quando il riferimento principale è alla profondità massima.
* SITES-16234: ContextHub: Correct Selected Brand Activity Name non viene visualizzato quando si avvia il targeting.
* SITES-12880: Fast-Track: correzione della localizzazione per Sites > Configurazione di Analytics.
* SITES-16103: Frammenti di esperienza: le opzioni di Target non vengono visualizzate in Cloud Service a causa di un errore della console.
* SITES-16001: MSM: possibilità di escludere i componenti per più campi dalla configurazione di rollout durante la creazione di Live Copy.
* SITES-16559: MSM: configurazioni di rollout rimosse durante il processo di rollout dei frammenti esperienza.
* SITES-16797: MSM: è stata corretta la riabilitazione dell’ereditarietà per un campo CF nell’editor.
* SITES-16273: Editor pagina: errore Copia/Incolla nelle pagine di AEM Sites dagli Appunti.
* SITES-16126: Sites Admin: prestazioni di authoring lente per gli utenti non amministratori dopo la 10288 di SITES.
* FORMS-10534: si verifica un errore nell’editor delle regole quando si seleziona l’opzione dell’operando booleano.
* FORMS-10248: in un modulo adattivo, quando il valore dei dati è di tipo booleano, le regole non riescono a impostare correttamente i valori per i pulsanti di scelta o i componenti delle caselle di controllo.
* FORMS-11361: il componente a discesa seleziona automaticamente per impostazione predefinita la prima opzione dall’elenco.
* FORMS-11413: un errore relativo al servizio di precompilazione del portale Forms viene attivato da Forms adattivo, anche quando il servizio non è in uso.
* FORMS-11433: quando un componente non modulo viene incluso in un modulo adattivo, il processo di invio non viene completato.
* FORMS-11206: quando un utente tenta di pianificare un flusso di lavoro di pubblicazione per un modulo adattivo, questo non funziona come previsto.
* FORMS-11546: Lighthouse ha rilevato un’etichetta ARIA mancante per i pannelli ripetuti in un modulo adattivo, influendo sull’accessibilità.
* FORMS-11095: l’attributo ARIA non è definito correttamente per i campi numero di telefono, indirizzo e-mail e numero, causando problemi di accessibilità.
* FORMS-9894: l’API del servizio di output genera un codice di errore errato quando un utente fornisce un percorso di archivio non valido, generando confusione per gli utenti che incontrano questo problema.
* FORMS-11404: il servizio ImportData mostra un comportamento incoerente quando si uniscono vari dati XML con un reader-extended PDF. In particolare, conserva correttamente le proprietà dell’estensione Reader per un documento PDF di output, ma non lo fa per altri PDF di output.


### Problemi noti {#known-issues-14157}

Nessuno.

### Tecnologie incorporate {#embedded-tech-14157}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,56-T20230927085643-189caed | [API Oak API 1.56.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
