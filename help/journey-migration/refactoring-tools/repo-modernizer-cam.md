---
title: Repository Modernizer (CAM)
description: Scopri come ristrutturare i pacchetti di progetto esistenti e renderli compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.
feature: Migration
role: Admin
source-git-commit: 317ee65786d48d7b92d95c7c6b8782f617d6e346
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 2%

---


# Repository Modernizer (CAM) {#repo-modernizer-cam}

Repository Modernizer è un’utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti distinti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service introduce molte nuove funzioni e opportunità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. A un livello avanzato, AEM richiede una separazione di **contenuto** e **codice** in pacchetti secondari discreti per rispettare la suddivisione tra contenuto mutabile e immutabile. Per ulteriori dettagli sulla nuova struttura di progetto AEM per Cloud Service, consulta [Struttura di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=it).

Repository Modernizer crea una struttura di progetto di AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

- Il pacchetto `ui.apps` viene distribuito in `/apps` e contiene tutto il codice

- Il pacchetto `ui.content` viene distribuito in aree scrivibili di runtime (ad esempio, `/content`, `/conf`, `/home` o qualsiasi elemento diverso da `/apps`) e contiene tutto il contenuto e la configurazione.

- Il pacchetto `all` è un pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

>[!NOTE]
>
> La struttura del progetto si basa su _Archetipo 48_ per i pacchetti e i relativi `pom.xml/filter.xml files`. Per ulteriori dettagli, vedere [Archetipo 48](https://github.com/adobe/aem-project-archetype).

Repository Modernizer ora supporta anche i seguenti tipi di progetto:

- **MULTI_PROJECT**: rappresenta un progetto multimodule senza POM padre, dispatcher e tutti i moduli comuni.
- **PROGETTO_SINGOLO**: rappresenta un singolo progetto.
- **NESTED_PROJECT**: rappresenta un progetto multimodule con un POM padre, un dispatcher e tutti i moduli comuni.
- **MONOLITHIC_PROJECT**: rappresenta un progetto principale con uno o più sottoprogetti.

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/3412960/?quality=12&learn=on&captions=ita)

- Il Repository Modernizer viene ora richiamato automaticamente dal servizio di refactoring nella scheda Processo di refactoring. I clienti devono semplicemente caricare il proprio progetto e attivare il processo di refactoring, senza alcuna configurazione aggiuntiva.

## Riferimento codice errore

Se riscontri un codice di errore durante l’utilizzo di Repository Modernizer, consulta la tabella seguente per dettagli e azioni consigliate.

| Codice di errore | Messaggio | Descrizione | Azione utente richiesta? |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| RM-100 | Errore durante la conversione del file di configurazione OSGi {0} nel formato .cfg.json. Prima di riprovare, convalida il file di configurazione esistente. | Questo errore si verifica quando si verifica un problema durante la trasformazione di un file di configurazione OSGi nel formato .cfg.json. | Sì |
| RM-101 | Errore durante il tentativo di copiare il contenuto da: {0} | Questo errore si verifica in caso di errore durante il tentativo di copiare il contenuto dall’origine specificata. | No |
| RM-102 | Errore durante lo spostamento del file {0} da {1} a {2}. | Questo errore si verifica quando si verifica un problema durante lo spostamento di un file da una posizione a un&#39;altra. | No |
| RM-103 | Impossibile risolvere il percorso specificato in un file valido: {0} | Questo errore si verifica quando il file non viene trovato nel percorso specificato. | No |
| RM-104 | Errore durante l&#39;iterazione del contenuto di {0}. | Questo errore si verifica durante l’attraversamento di file o directory, a indicare un problema di accesso o elaborazione del contenuto. | No |
| RM-105 | Errore durante l&#39;analisi del file XML: {0}. Prima di riprovare, convalida il file XML. | Questo errore si verifica quando non è possibile analizzare il file XML. | Sì |
| RM-106 | Errore durante la scrittura nel file XML: {0}. | Questo errore si verifica in caso di problemi di scrittura nel file XML. | No |
| RM-107 | Nessun pacchetto di contenuto trovato nel progetto esistente: {0}. Verifica che il progetto corretto sia stato caricato. | Questo errore indica che nel progetto esistente non è stato trovato alcun pacchetto di contenuto. | Sì |
| RM-108 | File POM non trovato nel percorso previsto: {0}. È previsto che il file POM del progetto o del modulo si trovi direttamente all&#39;interno della relativa directory come file figlio. | Questo errore si verifica quando il file POM non viene trovato nella posizione prevista. | Sì |
| RM-109 | Errore durante l&#39;analisi del file pom.xml: {0}. Prima di riprovare, convalida il file POM. | Questo errore si verifica quando si verifica un problema durante l’analisi del file pom.xml. | Sì |
| RM-110 | Errore durante la scrittura nel file pom.xml: {0}. | Questo errore si verifica in caso di problemi di scrittura nel file POM. | No |
| RM-111 | Errore durante la scrittura nel file di report. | Questo errore si verifica in caso di errore durante il processo di scrittura nel file del report. | No |
| RM-112 | Impossibile trovare {0} nel file POM della struttura dell&#39;archivio in ({1}) | Questo errore si verifica quando la configurazione prevista non viene trovata nel modello dell’archetipo di progetto AEM. | No |
| RM-113 | Errore durante il tentativo di copiare i modelli Archetipo progetto AEM nella destinazione. | Questo errore si verifica quando si verifica un problema durante la copia dei modelli Archetipo progetto AEM nella destinazione. | No |
| RM-115 | Errore durante il tentativo di connessione all’archiviazione BLOB di Azure. | Questo errore si verifica quando si verifica un problema di connessione all’archiviazione BLOB di Azure. | No |
| RM-116 | Errore durante il caricamento del file: {0} nell&#39;archiviazione BLOB di Azure. | Questo errore si verifica quando si verifica un problema durante il caricamento di un file nell’archiviazione BLOB di Azure. | No |
| RM-117 | Errore durante il tentativo di download del file: {0} dall&#39;archiviazione BLOB di Azure. | Questo errore si verifica quando si verifica un problema durante il download di un file dall’archiviazione BLOB di Azure. | No |
| RM-118 | Errore di I/O durante la gestione: {0}. | Questo errore si verifica quando si verifica un problema durante la lettura o la scrittura in un file di progetto. | No |
| RM-119 | Errore di I/O durante il tentativo di archiviare i risultati per il caricamento in Azure. | Questo errore si verifica quando si verifica un errore durante l’archiviazione dei risultati generati dal processo. | No |
| RM-120 | Errore di I/O durante il tentativo di annullare l’archiviazione del file zip del progetto fornito. Verifica se il CAP del progetto fornito è valido. | Questo errore si verifica quando si verifica un errore durante la rimozione dell’archiviazione del progetto cliente specificato. | Sì |
| RM-121 | Errore durante la scrittura nel file di configurazione. | Questo errore si verifica in caso di errore durante il processo di scrittura nel file di configurazione. | No |
| RM-122 | Tipo di richiesta non supportato: {0}. | Questo errore si verifica quando il tipo di richiesta non è supportato dal sistema. Controlla il tipo di richiesta e riprova. | No |

## Priorità dei rapporti sui risultati

Quando si scarica il report dei risultati generato dallo strumento Repository Modernizer, a ogni risultato viene assegnata una **priorità**. Queste priorità ti aiutano a comprendere l’urgenza e l’impatto di ogni problema:

| Priorità | Descrizione |
| -------- | ----------------------------------------------------------------------------------------------- |
| CRITICAL (CRITICO) | Per generare correttamente il progetto, è necessario risolverlo. |
| ALTA | Deve essere risolto per garantire che le funzionalità non vengano interrotte in AEM. |
| NORMALE | Dovrebbero essere risolti per garantire la sanità mentale complessiva e la completezza della modernizzazione. |
| BASSA | Per la verifica manuale; questi risultati sono informativi e possono non richiedere un&#39;azione immediata. |

>[!NOTE]
> 
>Per garantire un processo di modernizzazione e distribuzione senza problemi, si raccomanda di affrontare in primo luogo i risultati a priorità più elevata.
