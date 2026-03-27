---
title: Creare una tabella dinamica nell’editor di comunicazione interattiva
description: Crea una funzione di tabella dinamica che consente agli autori di creare tabelle basate su dati.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
source-git-commit: 322183c28719db5b8657d9532ef234e1d18821cd
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Creare una tabella dinamica nell’editor di comunicazione interattiva

## Panoramica

L’Editor di comunicazione interattiva fornisce una tabella dinamica
funzionalità che consente agli autori di creare tabelle basate su dati il cui contenuto viene popolato automaticamente in fase di esecuzione da origini dati strutturate.

A differenza delle tabelle statiche in cui le righe devono essere create manualmente, le tabelle dinamiche si espandono o si contraggono automaticamente in base ai record restituiti da un&#39;origine dati associata. Ciò li rende utili per scenari come rendiconti di fatturazione, cronologie delle transazioni, elenchi di prodotti o programmi di criteri.

Questo articolo spiega come inserire e configurare una tabella dinamica con associazione dati, gestire il flusso di tabelle a più pagine e convalidare i conteggi delle righe.

## Inserire una tabella dinamica

1. Apri **Editor comunicazioni interattive**.
1. Dal **pannello Componenti**, trascina il **componente Tabella** nel
quadro.
1. Nella finestra di dialogo specifica il **numero di colonne** e le **righe iniziali**, accertati che sia inclusa la **riga di intestazione**, quindi fai clic su OK per creare la tabella.

### Associare dati alla tabella dinamica

Le tabelle dinamiche compilano automaticamente le righe associandole a un&#39;origine dati ripetibile.

![Trova documento IC](/help/forms/interactive-communication/assets/databinding-in-table.png)

Per associare i dati alla tabella:

1. Selezionare la **riga tabella** dal pannello gerarchia.

1. Apri **Associazione dati** dal pannello laterale.

1. Verifica che lo schema dati selezionato sia di tipo array.

1. Trascina e rilascia lo schema di dati dell’array sulla riga di tabella selezionata per associare i dati.

### Abilita flusso di pagina

Le tabelle dinamiche possono espandersi oltre una singola pagina. Per consentire l&#39;espansione e il proseguimento della tabella tra pagine, inserirla in un contenitore **Contenuto con flusso**.

![Trova documento IC](/help/forms/interactive-communication/assets/table-data-binding.png)

Per abilitare il flusso di pagina:

1. Selezionare il **contenitore di layout principale** della tabella.

1. Apri il pannello Proprietà e imposta il tipo di contenuto su **Flowed**.

1. Seleziona la tabella e accertati che sia configurata anche per supportare il contenuto di flusso.

1. Visualizzare l’anteprima della comunicazione per verificare che la tabella continui nella pagina successiva, man mano che vengono visualizzate righe aggiuntive.

### Consenti interruzione di pagina nella tabella

![Trova documento IC](/help/forms/interactive-communication/assets/table-data-binding.png)

Per garantire che la tabella si suddivida correttamente tra le pagine:

1. Selezionare la **tabella** nell&#39;area di lavoro.
1. Apri il pannello **Proprietà**.
1. Abilita **Consenti interruzione di pagina nel contenuto**.

Quando questa opzione è attivata, la tabella si interrompe automaticamente alla fine di una pagina e continua nella pagina successiva, con la riga di intestazione ripetuta.

### Configura convalida riga

È possibile controllare il numero di righe di cui la tabella dinamica può eseguire il rendering.

* **Righe minime:** assicura che la tabella esegua il rendering almeno del numero di righe specificato.
* **Righe massime:** Limita il numero totale di righe di cui è stato eseguito il rendering dall&#39;origine dati.
* **Righe iniziali:** Definisce il numero di righe visualizzate nell&#39;editor durante l&#39;anteprima in fase di progettazione.

>[!NOTE]
>
> L&#39;impostazione di **Rows iniziali** su circa **3-5** fornisce un&#39;anteprima del layout più realistica prima dell&#39;applicazione dei dati di runtime.

## Funzionalità principali

* Associazione dati colonna: associa ciascuna colonna a un campo nel modello dati.

* Contenuto con flusso: consente alla tabella di espandersi e continuare su più pagine.

* Supporto delle interruzioni di pagina: abilita le interruzioni di pagina a livello di riga all&#39;interno della tabella.

* Numero minimo di righe: assicura che venga eseguito il rendering di un numero minimo di righe.

* Numero massimo di righe: limita il totale delle righe di cui è stato eseguito il rendering dall’origine dati.

* Righe iniziali: definisce le righe predefinite visualizzate durante l&#39;anteprima in fase di progettazione.

La funzione Tabella dinamica dell’Editor di comunicazione interattiva consente agli autori di creare tabelle flessibili e basate su dati senza scrivere codice personalizzato. Associando la tabella a un array di dati, abilitando il contenuto con flusso, consentendo le interruzioni di pagina e configurando la convalida delle righe, gli autori possono produrre comunicazioni strutturate che si adattano in modo fluido a volumi di dati diversi, mantenendo al contempo un layout coerente.
