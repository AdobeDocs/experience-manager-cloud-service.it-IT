---
title: Verifica collegamenti
description: Scopri in che modo Verifica collegamenti aiuta gli autori convalidando i collegamenti quando vengono aggiunti al contenuto e quali opzioni di configurazione offre.
feature: Operations
role: Admin
source-git-commit: cc8e242715faaef5cda25b428c315947ec3d7e06
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---


# Verifica collegamenti {#link-checker}

Scopri in che modo Verifica collegamenti aiuta gli autori convalidando i collegamenti quando vengono aggiunti al contenuto e quali opzioni di configurazione offre.

## Panoramica {#overview}

Gli autori dei contenuti non devono preoccuparsi di convalidare ogni collegamento incluso nel contenuto. Il Link Checker viene eseguito automaticamente per aiutare gli autori di contenuti con i loro collegamenti, tra cui:

* Convalida dei collegamenti quando vengono aggiunti al contenuto
* Visualizzazione di un elenco di tutti i collegamenti esterni nel contenuto
* Esecuzione delle trasformazioni dei collegamenti

Il Link Checker dispone di diverse [opzioni di configurazione](#configuring), ad esempio la definizione della convalida dei collegamenti interni, la possibilità di omettere alcuni collegamenti o percorsi di collegamento dalla convalida e la definizione delle regole di riscrittura dei collegamenti.

Verifica collegamenti convalida [collegamenti interni](#internal) e [collegamenti esterni.](#external)

>[!NOTE]
>
>Poiché il Link Checker controlla i collegamenti di ogni pagina di contenuto, può influire sulle prestazioni di archivi di grandi dimensioni. In questi casi, potrebbe essere necessario [configurare la frequenza di esecuzione di Verifica collegamenti](#configuring) o [disabilitarlo.](#disabling)

## Verifica dei collegamenti interni {#internal}

I collegamenti interni sono collegamenti ad altri contenuti nell’archivio di AEM. I collegamenti interni possono essere aggiunti mediante il selettore di percorsi, l’editor Rich Text o un componente personalizzato. Ad esempio:

* Crea la pagina `/content/wknd/us/en/adventures/ski-touring`
* La pagina contiene un collegamento a `/content/wknd/us/en/adventures/extreme-ironing` in un [componente testo.](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/wcm-components/text)

I collegamenti interni vengono convalidati non appena l’autore di contenuto aggiunge un collegamento di questo tipo a una pagina. Se il collegamento non è più valido:

* Viene rimosso dall’editore.
   * Il collegamento stesso viene rimosso.
   * Il testo del collegamento rimane.
* Viene visualizzato come collegamento interrotto nell’interfaccia di authoring.

![Verifica collegamenti in corso](assets/link-checker-internal.png)

## Verifica collegamenti esterni {#external}

I collegamenti esterni sono collegamenti a contenuti esterni all’archivio AEM. I collegamenti esterni possono essere aggiunti utilizzando l’editor Rich Text o un componente personalizzato. Ad esempio:

* Crea la pagina `/content/wknd/us/en/adventures/ski-touring`
* La pagina contiene un collegamento a `https://bunwarmerthermalunderwear.com` in un [componente testo.](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/wcm-components/text)

I collegamenti esterni vengono convalidati per la sintassi e verificandone la disponibilità. Questo controllo viene eseguito in modo asincrono a un intervallo configurabile. Se Verifica collegamenti rileva un collegamento esterno non valido:

* Viene rimosso dall’editore.
   * Il collegamento stesso viene rimosso.
   * Il testo del collegamento rimane.
* Viene visualizzato come collegamento interrotto nell’interfaccia di authoring.

![Verifica collegamenti per la verifica dei collegamenti esterni](assets/link-checker-external.png)

### Funzionamento di Verifica collegamenti esterni {#external-details}

Verifica collegamenti esterni si basa su diversi servizi e la comprensione del loro funzionamento consente di comprendere come [configurare Verifica collegamenti per soddisfare le proprie esigenze.](#configuring)

1. Ogni volta che un autore di contenuti salva un collegamento a una pagina, viene attivato un gestore eventi.
1. Il gestore eventi analizza tutto il contenuto in `/content` e verifica la presenza di collegamenti nuovi o aggiornati e li aggiunge a una cache per Verifica collegamenti.
1. Il servizio **Day CQ Link Checker** viene quindi eseguito regolarmente per verificare la presenza di una sintassi valida nelle voci della cache.
1. I collegamenti convalidati dalla sintassi vengono quindi visualizzati nella finestra [Verifica collegamenti esterni.](#external-using) Tuttavia saranno in uno stato **Pending**.
1. L&#39;attività **Day CQ Link Checker** viene quindi eseguita regolarmente per convalidare i collegamenti effettuando una chiamata GET.
1. L&#39;attività **Day CQ Link Checker** aggiorna quindi le voci nella [finestra External Link Checker](#external-using) con i risultati delle chiamate GET.

### Utilizzo di Verifica collegamenti esterni {#external-using}

Verifica collegamenti esterni è una console che fornisce una panoramica di tutti i collegamenti esterni presenti nel contenuto di AEM. Per utilizzare Verifica collegamenti esterni:

1. Dalla navigazione globale, selezionare **Strumenti** -> **Siti**.
1. Selezionare **Verifica collegamenti esterni** e viene visualizzato un elenco di tutti i collegamenti esterni.

![Verifica collegamenti esterni](assets/external-link-checker.png)

Ogni voce della tabella rappresenta un collegamento esterno rilevato dal servizio Verifica collegamenti. Vengono visualizzate le seguenti colonne:

* **Stato** - Lo stato di convalida del collegamento, che può essere uno dei seguenti:
   * **Valido** - Il collegamento esterno è raggiungibile dal Link Checker.
   * **In sospeso** - Il collegamento esterno è stato aggiunto al contenuto del sito, ma non è stato ancora convalidato da Verifica collegamenti.
   * **Non valido** - Il link esterno non è raggiungibile dal Link Checker.
* **URL** - Il collegamento esterno
* **Destinatario che inoltra**: la pagina di contenuto che contiene il collegamento esterno
   * Viene popolato solo [se configurato.](#configuring)
* **Ultimo controllo** - L&#39;ultima volta che Verifica collegamenti ha convalidato il collegamento esterno
   * La frequenza con cui vengono controllati i collegamenti [&#x200B; è configurabile.](#configuring)
* **Ultimo stato** - L&#39;ultimo codice di stato di HTML restituito quando il collegamento selezionato ha controllato l&#39;ultimo collegamento esterno
* **Ultima disponibilità** - Ora dall&#39;ultima disponibilità del collegamento per Verifica collegamenti
* **Ultimo accesso** - Ora dall&#39;ultimo accesso alla pagina con il collegamento esterno nell&#39;interfaccia di creazione

Puoi modificare il contenuto della finestra utilizzando i due pulsanti nella parte superiore dell’elenco dei collegamenti:

* **Aggiorna** - Per aggiornare il contenuto dell&#39;elenco
* **Verifica** - Per controllare un singolo collegamento esterno selezionato nell&#39;elenco

Tutte le altre icone nella finestra Verifica collegamenti esterni sono inattive.

## Configurazione di Verifica collegamenti {#configuring}

Il Link Checker è disponibile automaticamente come strumento pronto all’uso in AEM. Tuttavia, esistono diverse configurazioni OSGi che possono essere modificate per modificarne il comportamento:

* **Servizio di archiviazione informazioni verifica collegamenti Day CQ** - Questo servizio definisce la dimensione della cache di Verifica collegamenti nell&#39;archivio.
* **Day CQ Link Checker Service** - Questo servizio esegue il controllo asincrono della sintassi dei collegamenti esterni.
   * È possibile definire il periodo di controllo e quali tipi di collegamenti vengono ignorati dallo strumento di controllo, tra le altre opzioni.
* **Attività Verifica collegamenti Day CQ** - Questo servizio esegue la convalida GET dei collegamenti esterni.
   * Consente definizioni separate degli intervalli per verificare collegamenti errati e validi tra le altre opzioni.
* **Day CQ Link Checker Transformer** - Questo servizio converte i collegamenti in base a un set di regole definito dall&#39;utente.

Per ulteriori informazioni su come modificare le impostazioni OSGi, consulta il documento [Configurazione di OSGi](/help/implementing/deploying/configuring-osgi.md).

## Disattivazione di Verifica collegamenti {#disabling}

Puoi scegliere di disabilitare completamente Verifica collegamenti. Per eseguire questa operazione:

1. Apri la console OSGi.
1. Modifica il trasformatore **Day CQ Link Checker**
1. Selezionare le opzioni che si desidera disattivare:
   * **Disabilita controllo** - per disabilitare la convalida dei collegamenti
   * **Disabilita riscrittura** - per disabilitare le trasformazioni dei collegamenti
