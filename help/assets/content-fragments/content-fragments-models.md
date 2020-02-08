---
title: Modelli per frammenti di contenuto
description: I modelli di frammenti di contenuto vengono utilizzati per creare frammenti di contenuto con contenuto strutturato.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Modelli per frammenti di contenuto{#content-fragment-models}

I modelli di frammenti di contenuto definiscono la struttura del contenuto per i frammenti [di](/help/assets/content-fragments/content-fragments.md)contenuto.

## Abilita modelli di frammenti di contenuto {#enable-content-fragment-models}

>[!CAUTION]
>
>Se non abilitate Modelli **frammenti di** contenuto, l&#39;opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.

Per abilitare i modelli di frammenti di contenuto è necessario:

* Abilitare l&#39;utilizzo di modelli di frammento di contenuto in Gestione configurazione
* Applica la configurazione alla cartella Risorse

### Abilitare i modelli di frammento di contenuto in Configuration Manager {#enable-content-fragment-models-in-configuration-manager}

Per [creare un nuovo modello](#creating-a-content-fragment-model) di frammento di contenuto, è **necessario** innanzitutto attivarlo utilizzando Gestione configurazione:

1. Accedete a **Strumenti**, **Generali**, quindi aprite il browser **** Configurazione.
2. Selezionate la posizione appropriata per il sito Web.
3. Utilizzate **Crea** per aprire la finestra di dialogo in cui:

   1. Specificate un **titolo**.
   2. Selezionare Modelli **di frammenti di** contenuto per attivarne l&#39;uso.
   ![configurazione](assets/cfm-models-01.png)

4. Selezionate **Crea** per salvare la definizione.

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **globale** è abilitata per i modelli di frammenti di contenuto, tutti i modelli creati dagli utenti possono essere utilizzati in qualsiasi cartella Risorse.

Per utilizzare altre configurazioni (ad esempio, escludendo il formato globale) con una cartella di risorse paragonabile, è necessario definire la connessione. A questo scopo, selezionate la **Configurazione** appropriata nella scheda Servizi **** cloud delle Proprietà **** cartella della cartella appropriata.

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Passa a **Strumenti**, **Risorse**, quindi apri Modelli **di frammenti di** contenuto.
1. Andate alla cartella appropriata per la [configurazione](#enable-content-fragment-models).
1. Utilizzare **Crea** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l&#39; [uso dei modelli di frammento di contenuto non è stato abilitato](#enable-content-fragment-models), l&#39;opzione **Crea** non sarà disponibile.

1. Specificate il Titolo **del** modello. Se necessario, potete anche aggiungere una **descrizione** .

   ![titolo e descrizione](assets/cfm-models-02.png)

1. Utilizzare **Crea** per salvare il modello vuoto. Un messaggio indica l&#39;esito positivo dell&#39;azione, è possibile selezionare **Apri** per modificare immediatamente il modello oppure **Fine** per tornare alla console.

## Definizione del modello di frammento di contenuto {#defining-your-content-fragment-model}

Il modello di frammento di contenuto definisce in modo efficace la struttura dei frammenti di contenuto risultanti. Utilizzando l’editor modelli potete aggiungere e configurare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello di frammento di contenuto esistente può influenzare i frammenti dipendenti.

1. Passa a **Strumenti**, **Risorse**, quindi apri Modelli **di frammenti di** contenuto.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Aprire il modello richiesto per **Edit**; utilizzare l&#39;azione rapida oppure selezionare il modello e quindi l&#39;azione dalla barra degli strumenti.

   Una volta aperto l&#39;editor modelli mostra:

   * left: campi già definiti
   * right: Tipi **di** dati disponibili per la creazione di campi (e **proprietà** da utilizzare dopo la creazione dei campi)
   >[!NOTE]
   >
   >Quando un campo è **obbligatorio**, l&#39; **etichetta** indicata nel riquadro a sinistra sarà contrassegnata con un asterisco (*****).

   ![proprietà](assets/cfm-models-03.png)

1. **Aggiunta di un campo**

   * Trascinare un tipo di dati richiesto nella posizione desiderata per un campo:
   ![tipo di dati su campo](assets/cfm-models-04.png)

   * Una volta aggiunto un campo al modello, nel pannello a destra vengono visualizzate le **proprietà** che è possibile definire per quel particolare tipo di dati. Qui è possibile definire i requisiti necessari per tale campo. Esempio:
   ![proprietà del campo](assets/cfm-models-05.png)

   >[!NOTE]
   Per il tipo di dati Testo **a** più righe è possibile definire il Tipo **** predefinito come:
   * **Formato RTF**
   * **Markdown**
   * **Testo normale**
   Se non viene specificato, per questo campo viene utilizzato il valore predefinito **RTF** .
   La modifica del tipo **** predefinito in un modello di frammento di contenuto avrà effetto solo su un frammento di contenuto esistente correlato, dopo che il frammento sarà stato aperto nell’editor e salvato.

1. **Rimozione di un campo**

   Selezionate il campo desiderato, quindi toccate o fate clic sull&#39;icona del cestino. Viene richiesto di confermare l’operazione.

   ![rimuovere](assets/cfm-models-06.png)

1. Dopo aver aggiunto tutti i campi obbligatori e definito le proprietà, utilizzate **Salva** per mantenere la definizione. Esempio:

   ![save](assets/cfm-models-07.png)

## Eliminazione di un modello di frammento di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
L&#39;eliminazione di un modello di frammento di contenuto può avere un impatto sui frammenti dipendenti.

Per eliminare un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri Modelli **di frammenti di** contenuto.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionate il modello, seguito da **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   Se al modello viene fatto riferimento, verrà visualizzato un avviso. Adottare le misure appropriate.

## Pubblicazione di un modello di frammento di contenuto {#publishing-a-content-fragment-model}

I modelli di frammenti di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

Per pubblicare un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri Modelli **di frammenti di** contenuto.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionate il modello, seguito da **Pubblica** dalla barra degli strumenti.

   >[!NOTE]
   Se si pubblica un frammento di contenuto per il quale il modello non è ancora stato pubblicato, verrà visualizzato un elenco di selezione e il modello verrà pubblicato con il frammento.
