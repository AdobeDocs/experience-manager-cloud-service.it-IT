---
title: Guida introduttiva alla localizzazione senza testa AEM
description: Scopri come organizzare i contenuti headless e come funzionano gli strumenti di localizzazione AEM.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Guida introduttiva alla localizzazione senza intestazione AEM {#getting-started}

Scopri come organizzare i contenuti headless e come funzionano gli strumenti di localizzazione AEM.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di localizzazione senza testa AEM [Scopri i contenuti headless e come localizzare in AEM](learn-about.md) hai imparato la teoria di base su cosa è un CMS headless e ora dovresti:

* Comprendi i concetti di base sulla distribuzione di contenuti headless.
* Verificare come AEM supporta la localizzazione e l&#39;headless.

Questo articolo si basa su questi elementi fondamentali per comprendere come AEM memorizza e gestisce i contenuti headless e come puoi utilizzare gli strumenti di localizzazione AEM per tradurli.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come iniziare a localizzare il contenuto headless in AEM. Dopo la lettura è necessario:

* Comprendere l’importanza della struttura dei contenuti per la localizzazione.
* Comprendere come AEM memorizza i contenuti headless.
* Acquisisci familiarità con AEM strumenti di localizzazione.

## Requisiti e prerequisiti {#requirements-prerequisites}

Sono necessari diversi requisiti prima di iniziare a localizzare il contenuto AEM headless.

### Conoscenza {#knowledge}

* Esperienza di localizzazione di contenuti per un CMS
* Esperienza utilizzando le funzioni di base di un CMS su larga scala
* Avere una conoscenza operativa AEM manipolazione di base
* Informazioni sul servizio di traduzione utilizzato
* Comprensione di base del contenuto che si sta traducendo

>[!TIP]
>
>Se non hai familiarità con l&#39;utilizzo di un CMS su larga scala come AEM, prima di procedere è consigliabile rivedere la documentazione [Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md). La documentazione di base sulla gestione non fa parte del percorso, quindi torna a questa pagina una volta completata.

### Strumenti {#tools}

* Accesso alla sandbox per testare la traduzione del contenuto
* Credenziali per la connessione al servizio di traduzione preferito
* È membro del gruppo `project-administrators` in AEM

## La struttura è la chiave {#content-structure}

AEM contenuto, sia esso headless o pagine web tradizionali, è guidato dalla sua struttura. AEM impone pochi requisiti alla struttura del contenuto, ma un’attenta considerazione della gerarchia dei contenuti come parte della pianificazione del progetto può rendere la localizzazione molto più semplice.

>[!TIP]
>
>Piano di traduzione e localizzazione all&#39;inizio del progetto headless. Collabora con il project manager e gli architetti di contenuti fin da subito.
>
>Può essere richiesto un &quot;project manager di internazionalizzazione&quot; come persona separata la cui responsabilità è quella di definire quali contenuti tradurre e cosa no, e quali contenuti tradotti possono essere modificati dai produttori di contenuti regionali o locali.

Crea un piano per la localizzazione dei contenuti necessaria.

* Hai solo bisogno di lingue diverse o anche lingue diverse da adottare per le specifiche regionali?
* È necessario che contenuti rich media come immagini o video siano diversi per diverse impostazioni internazionali?

## Come AEM memorizza i contenuti headless {#headless-content-in-aem}

Per lo specialista di localizzazione, non è importante comprendere in profondità come AEM gestire i contenuti headless. Tuttavia, conoscere i concetti e la terminologia di base sarà molto utile in quanto successivamente si utilizzano gli strumenti di localizzazione AEM. Ma soprattutto, è necessario comprendere il proprio contenuto e la sua struttura per localizzarlo in modo efficace.

### Modelli di contenuto {#content-models}

Affinché i contenuti headless possano essere distribuiti in modo coerente tra canali, aree geografiche e lingue diverse, i contenuti devono essere altamente strutturati. AEM utilizza Modelli di contenuto per applicare questa struttura. Pensa ai Modelli di contenuto come a un tipo di modello o pattern per la creazione di contenuti headless. Poiché ogni progetto ha le proprie esigenze, ogni progetto definisce modelli di frammento di contenuto personalizzati. AEM non ha requisiti o struttura fissi per tali modelli.

L’architetto dei contenuti lavora all’inizio del progetto per definire questa struttura. Come consigliato in precedenza, in qualità di specialista di localizzazione, è necessario collaborare strettamente con l&#39;architetto dei contenuti per comprendere e organizzare i contenuti.

Poiché i Modelli di contenuto definiscono la struttura del contenuto, dovrai sapere quali campi dei modelli devono essere tradotti. In genere si lavora con l’architettura dei contenuti per definirlo. Per sfogliare i campi dei modelli di contenuto, effettua le seguenti operazioni.

1. Passa a **Strumenti** -> **Risorse** -> **Modelli di frammento di contenuto**.
1. I modelli per frammenti di contenuto sono generalmente memorizzati in una struttura di cartelle. Tocca o fai clic sulla cartella del progetto.
1. I modelli sono elencati. Tocca o fai clic sul modello per visualizzare i dettagli.
   ![Modelli per frammenti di contenuto](assets/content-fragment-models.png)
1. Viene visualizzato **Editor modello frammento di contenuto**.
   1. La colonna a sinistra contiene i campi del modello. Questa colonna ci interessa.
   1. La colonna a destra contiene i campi che possono essere aggiunti al modello. Questa colonna possiamo ignorare.
      ![Editor modello per frammenti di contenuto](assets/content-fragment-model-editor.png)
1. Tocca o fai clic su uno dei campi del modello. AEM lo contrassegna e i dettagli di quel campo sono visualizzati nella colonna di destra.
   ![Dettagli Editor modello frammento di contenuto](assets/content-fragment-model-editor-detail.png)

Prendi nota del campo **Nome proprietà** per tutti i campi che devono essere tradotti. Queste informazioni saranno necessarie per il passaggio successivo nel percorso.

### Frammenti di contenuto {#content-fragments}

I modelli di contenuto vengono utilizzati dagli autori dei contenuti per creare il contenuto effettivo senza titolo. Gli autori dei contenuti selezionano il modello su cui basare i propri contenuti e quindi creano frammenti di contenuto. I frammenti di contenuto sono istanze dei modelli e rappresentano il contenuto effettivo da distribuire senza problemi.

Se i Modelli di contenuto sono i pattern per il contenuto, i Frammenti di contenuto sono il contenuto effettivo basato su tali pattern.

I frammenti di contenuto sono gestiti come risorse in AEM come parte della gestione delle risorse digitali (DAM). Questo è importante in quanto si troveranno tutti sotto il percorso `/content/dam`.

## Struttura dei contenuti consigliata {#recommended-structure}

Come precedentemente consigliato, collabora con l’architettura dei contenuti per determinare la struttura del contenuto appropriata per il tuo progetto. Tuttavia il seguente è una struttura collaudata, semplice e intuitiva che è abbastanza efficace.

Definisci una cartella di base per il progetto in `/content/dam`.

```text
/content/dam/<your-project>
```

La lingua in cui viene creato il contenuto è denominata radice della lingua. Nel nostro esempio è inglese e dovrebbe essere sotto questo percorso.

```text
/content/dam/<your-project>/en
```

Tutti i contenuti del progetto che possono essere necessari per essere localizzati devono essere inseriti nella lingua principale.

```text
/content/dam/<your-project>/en/<your-project-content>
```

Le localizzazioni devono essere create come cartelle di pari livello accanto alla directory principale lingua. Ad esempio, il percorso per il tedesco è il seguente.

```text
/content/dam/<your-project>/de
```

La struttura finale può avere un aspetto simile al seguente.

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

## Strumenti di localizzazione AEM {#localization-tools}

Ora che capisci cosa sono i frammenti di contenuto e l’importanza della struttura del contenuto, possiamo capire come localizzare questo contenuto. Gli strumenti di localizzazione di AEM sono abbastanza potenti, ma sono semplici da comprendere ad alto livello.

* **Connettore traduzione** : il connettore è il collegamento tra AEM e il servizio di traduzione utilizzato.
* **Regole**  di traduzione - Le regole definiscono quale contenuto in particolari percorsi deve essere tradotto.
* **Progetti di traduzione** : i progetti di traduzione raccolgono contenuti che dovrebbero essere affrontati come un unico sforzo di traduzione e tengono traccia dei progressi della traduzione, interfacciandosi con il connettore per trasmettere i contenuti da tradurre e riceverli nuovamente dal servizio di traduzione.

In genere è necessario impostare il connettore una sola volta per l’istanza e le regole per ogni progetto headless. Poi usi i progetti di traduzione per localizzare il tuo contenuto e mantenere le sue traduzioni aggiornate continuamente.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di localizzazione headless devi:

* Comprendere l’importanza della struttura dei contenuti per la localizzazione.
* Comprendere come AEM memorizza i contenuti headless.
* Acquisisci familiarità con AEM strumenti di localizzazione.

Sviluppa questa conoscenza e continua il tuo percorso di localizzazione senza testa AEM esaminando il documento [Configura il connettore di traduzione](configure-connector.md) in cui imparerai a connetterti AEM a un servizio di traduzione.|

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di localizzazione headless esaminando il documento [Configura il connettore di traduzione](configure-connector.md), di seguito sono riportate alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [AEM Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md)  - Scopri le nozioni di base dell’interfaccia utente AEM per navigare comodamente ed eseguire attività essenziali come la ricerca del contenuto.
* [Identificazione del contenuto da tradurre](/help/sites-cloud/administering/translation/rules.md)  - Scopri come le regole di traduzione identificano il contenuto da tradurre.
* [Configurazione del framework di integrazione della traduzione](/help/sites-cloud/administering/translation/integration-framework.md)  - Scopri come configurare il framework di integrazione della traduzione per l’integrazione con i servizi di traduzione di terze parti.
* [Gestione dei progetti di traduzione](/help/sites-cloud/administering/translation/managing-projects.md)  - Scopri come creare e gestire progetti di traduzione automatica e umana in AEM.
