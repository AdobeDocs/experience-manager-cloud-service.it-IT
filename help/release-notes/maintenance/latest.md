---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1251f36ece4449d8be6a40f34421351161bf3b23
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 18%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 12549 {#release-12549}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 12549, rilasciata pubblicamente il 4 luglio 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 12255. La versione di manutenzione 12549 sostituisce 12441 per risolvere due problemi.

2023.7.0 Feature Activation fornirà il set completo di funzioni per questa versione di manutenzione. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-12549}

- FORMS-5054: è stato aggiunto il supporto per tutte le [statue](https://opensource.adobe.com/acrobat-sign/acrobat_sign_events/webhookeventsagreements.html) supportati da Adobe Sign.

### Problemi risolti {#fixed-issues-12549}

- Vari aggiornamenti relativi all’accessibilità
- SITES-12688: Editor pagina: operatore logico OR che non funziona correttamente nella ricerca di Asset Finder
- SITES-4951: Editor pagina: la ricerca dei tag nell’editor pagina non trova i tag secondari
- SITES-12465: Frammenti esperienza: i tasti freccia non funzionano nella finestra di dialogo del componente Frammento esperienza
- SITES-12893: Frammenti di esperienza: applicare la convalida circolare dei riferimenti ai frammenti di esperienza
- SITES-12715: Frammenti di esperienza: le configurazioni del servizio cloud applicate alla cartella Frammenti di esperienza non persistono
- SITES-13097: Frammenti esperienza: impossibile aggiungere frammenti esperienza a un progetto di traduzione
- SITES-13165: GraphQL: Ripristina il comportamento predefinito per il filtraggio di valori nulli
- SITES-12577: Verifica collegamenti: il trasformatore non riscrive i collegamenti in modo intermittente
- SITES-13559: MSM: eccezione &quot;Non modificabile&quot; generata durante il rollout del componente
- SITES-11757: MSM: l’ereditarietà della configurazione di rollout dall’elemento padre non viene ripristinata per le pagine figlie
- SITES-14073: Sites Admin: il rapporto CSV non riesce con 500 quando non si seleziona alcuna proprietà da esportare
- FORMS-7648: impossibile convalidare il numero massimo di cifre in un componente Casella numerica. Lo script di convalida non funziona.
- FORMS-8177: quando il servizio Forms è attivo, il `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Failed to retrieve asset dependencies` si verifica un errore.
- FORMS-8300: quando un utente tenta di delegare un’attività dopo averla aperta, la risposta del delegato ricarica l’attività, anziché aprire l’interfaccia utente della casella in entrata AEM dell’utente.
- FORMS-8500: nel browser Microsoft® Edge con l’opzione Modalità IE abilitata, l’apertura di HTML5 Forms non riesce.
- FORMS-8541: durante il rendering di un Forms adattivo, si verifica un’eccezione Null Pointer.
- FORMS-8964: quando un modulo viene aperto su un dispositivo Android™ su Google Chrome o Mozilla Firefox, il testo immesso nel componente Casella di testo non può essere rimosso.
- FORMS-9026: quando un utente crea un modulo adattivo basato su uno schema JSON complesso e valido, trascina i campi dello schema JSON correlati nell’editor di Forms adattivo per creare campi di Forms adattivo e aggiorna la finestra dell’editor di Forms adattivo, tutti i campi vengono eliminati e l’editor di Forms adattivo appare vuoto.
- FORMS-9263: quando il testo visualizzato di un&#39;opzione della casella di controllo contiene un carattere speciale, gli utenti non possono selezionare tali caselle di controllo.
- FORMS-8668: durante il rendering di un’anteprima PDF di un modulo, nei registri di errore vengono visualizzate alcune immagini stack Java™ non richieste. Tuttavia, il rendering del modulo non presenta problemi.
- FORMS-8116: quando le regole vengono applicate al componente Contenitore Forms adattivo, le regole applicate non vengono salvate.
- FORMS-7906: quando si aggiunge un modulo adattivo a un componente Contenitore di AEM Sites, l’editor di regole non si apre.
- FORMS-8846: la proprietà Bind reference non funziona per il componente Forms adattivo allegati.
- FORMS-9072: quando esegui una ricerca in uno schema durante la creazione di un frammento di modulo, il risultato della ricerca non restituisce alcuno schema per la selezione.
- FORMS: sono stati corretti diversi bug relativi all’accessibilità per migliorare l’accessibilità delle funzioni di AEM Forms.

### Problemi noti {#known-issues-12549}

- SKYOPS-61385: con l’ultimo aggiornamento di Dispatcher, alcune espressioni regolari non valide che in precedenza venivano ignorate automaticamente da `libpcre1` non sono più accettati dall&#39;aggiornamento `libpcre2` durante la distribuzione. Il controllo della configurazione del dispatcher verrà aggiornato a breve per identificarli anche in precedenza.

### Tecnologie incorporate {#embedded-tech-12549}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak API 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
