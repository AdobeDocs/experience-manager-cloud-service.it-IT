---
title: Come si configurano i filtri di ricerca per la casella in entrata?
description: Scopri come configurare i filtri di ricerca per gli elementi della casella in entrata.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# Configurare i filtri di ricerca per la casella in entrata {#configure-search-filters-inbox}

Puoi configurare i filtri di ricerca per gli elementi della casella in entrata. Basare i criteri di ricerca su una colonna Posta in arrivo specifica per filtrare i risultati.

Ad esempio, per filtrare gli elementi della casella in entrata in base a un intervallo di colonne Casella in entrata data di nascita, è possibile utilizzare il predicato Intervallo date per definire l’intervallo di date.

Di seguito sono riportati i tipi di predicato disponibili per Posta in arrivo:

* Predicato intervallo

* Predicato testo

* Predicato intervallo di date

* Predicato proprietà opzioni

>[!NOTE]
>
>Assicurati di essere membro della `workflow-administrators` per configurare i filtri di ricerca per la casella in entrata.

## Creare o aprire una configurazione personalizzata {#creating-opening-customized-configuration}

1. Accedi a **[!UICONTROL Strumenti]**, **[!UICONTROL Generale]**, **[!UICONTROL Cerca in Forms]**.

1. Seleziona la **[!UICONTROL Barra di ricerca casella in entrata]** configurazione e selezione **[!UICONTROL Modifica]**.
1. Incorporare le modifiche alla configurazione del predicato utilizzando **[!UICONTROL Modifica Forms di ricerca]**.
1. Seleziona **[!UICONTROL Fine]** per salvare la configurazione.

## Eliminare una configurazione personalizzata {#delete-customized-configuration}

Per eliminare una configurazione personalizzata:

1. Accedi a **[!UICONTROL Strumenti]**, **[!UICONTROL Generale]**, **[!UICONTROL Cerca in Forms]**.

1. Seleziona la **[!UICONTROL Barra di ricerca casella in entrata]** configurazione e selezione **[!UICONTROL Elimina]**.

## Configura predicato intervallo {#range-predicate}

È possibile filtrare gli elementi della casella in entrata per cercare un intervallo di numeri all&#39;interno di una colonna della casella in entrata utilizzando il predicato Intervallo. Puoi anche scegliere di includere valori decimali per i numeri.

Per configurare un predicato Range:

1. Apri [modulo per la configurazione](#creating-opening-customized-configuration).
1. Seleziona la **[!UICONTROL Seleziona predicato]** Tab e trascina **[!UICONTROL Predicato intervallo]** al modulo.
1. In **[!UICONTROL Impostazioni]** , selezionare il nome della colonna Posta in arrivo su cui basare la ricerca, da **[!UICONTROL Nome colonna]** campo.
1. Specifica l’etichetta del filtro nella **[!UICONTROL Etichetta filtro]** campo. Seleziona la **[!UICONTROL Abilita valori decimali]** per accettare valori decimali per i numeri durante la definizione dell&#39;intervallo.
1. Specifica una descrizione facoltativa per la configurazione e seleziona **[!UICONTROL Fine]** per salvarlo.

Le modifiche alla configurazione si riflettono all’apertura della pagina Filtri. L’etichetta del filtro specificata nel passaggio 4 viene visualizzata come etichetta con un’opzione per definire i valori massimo e minimo. Quando si preme Invio, [!DNL Experience Manager] applica i criteri di ricerca al nome della colonna specificato nel passaggio 3 e restituisce gli elementi della casella in entrata.

>[!NOTE]
>
>Nell’articolo sono elencate le opzioni dell’interfaccia utente più recenti. I nomi delle opzioni vengono aggiornati nell’interfaccia utente della prossima versione.

## Configura predicato testo {#text-predicate}

Filtrare gli elementi della casella in entrata per cercare una stringa di testo all&#39;interno di una colonna della casella in entrata utilizzando il predicato Testo.

Per configurare un predicato di testo:

1. Apri [modulo per la configurazione](#creating-opening-customized-configuration).
1. Seleziona la **[!UICONTROL Seleziona predicato]** Tab e trascina **[!UICONTROL Predicato testo]** al modulo.
1. In **[!UICONTROL Impostazioni]** , selezionare il nome della colonna Posta in arrivo su cui basare la ricerca, da **[!UICONTROL Nome colonna]** campo.
1. Specificare il testo visualizzato nella casella di testo Cerca come testo segnaposto in **[!UICONTROL Segnaposto casella di testo di ricerca]** campo.
1. Specifica una descrizione facoltativa per la configurazione e seleziona **[!UICONTROL Fine]** per salvarlo.

Le modifiche alla configurazione si riflettono all’apertura della pagina Filtri. Quando si preme Invio, [!DNL Experience Manager] applica il testo di ricerca specificato nel passaggio 4 al nome di colonna specificato nel passaggio 3 e restituisce gli elementi della casella in entrata.

## Configura predicato intervallo di date {#date-range-predicate}

È possibile filtrare gli elementi della casella in entrata per cercare un intervallo di date all’interno di una colonna della casella in entrata utilizzando il predicato Intervallo date.

Per configurare un predicato di intervallo di date:

1. Apri [modulo per la configurazione](#creating-opening-customized-configuration).
1. Seleziona la **[!UICONTROL Seleziona predicato]** Tab e trascina **[!UICONTROL Predicato intervallo di date]** al modulo.
1. In **[!UICONTROL Impostazioni]** , selezionare il nome della colonna Posta in arrivo su cui basare la ricerca, da **[!UICONTROL Nome colonna]** campo.
1. Specifica l’etichetta per il filtro dell’intervallo di date nella **[!UICONTROL Etichetta filtro]** campo.
1. Specifica le etichette di data di inizio e di fine per il filtro.
1. Specifica una descrizione facoltativa per la configurazione e seleziona **[!UICONTROL Fine]** per salvarlo.

Le modifiche alla configurazione si riflettono all’apertura della pagina Filtri. L’etichetta di filtro specificata nel passaggio 4 viene visualizzata come etichetta per il filtro dell’intervallo di date, insieme alle etichette della data di inizio e di fine specificate nel passaggio 5. [!DNL Experience Manager] applica i criteri di ricerca al nome della colonna specificato nel passaggio 3 e restituisce gli elementi della casella in entrata.

## Configura predicato opzioni colonna personalizzate {#custom-column-options-predicate}

È possibile filtrare gli elementi della casella in entrata per cercare un&#39;opzione personalizzata all&#39;interno di una colonna della casella in entrata utilizzando il predicato Opzioni colonna personalizzate.

Per configurare un predicato Opzioni colonna personalizzato:

1. Apri [modulo per la configurazione](#creating-opening-customized-configuration).
1. Seleziona la **[!UICONTROL Seleziona predicato]** Tab e trascina **[!UICONTROL Predicato opzioni colonna personalizzate]** al modulo.
1. In **[!UICONTROL Impostazioni]** , selezionare il nome della colonna Posta in arrivo su cui basare la ricerca, da **[!UICONTROL Nome colonna]** campo.
1. Specifica l’etichetta per il filtro delle opzioni di colonna personalizzato nella sezione **[!UICONTROL Etichetta filtro]** campo.
1. Seleziona la **[!UICONTROL Selezione singola]** per abilitare la selezione di una sola opzione durante l’applicazione di un filtro a una colonna della casella in entrata.
1. In **[!UICONTROL Aggiungi opzioni]** sezione:
   1. Seleziona **[!UICONTROL Manuale]** per definire manualmente le opzioni di ricerca del filtro. Seleziona **[!UICONTROL Aggiungi opzioni filtro]** per definire la prima opzione. Specifica l’etichetta per l’opzione colonna e il testo del valore dell’opzione da cercare. Ad esempio, se desideri cercare **Femmina** come valore in una colonna della casella in entrata, puoi specificare **F** come etichetta per l’opzione colonna e aggiungi **Femmina** come testo del valore dell’opzione. Allo stesso modo, puoi aggiungere altre opzioni di filtro.
   1. Seleziona **[!UICONTROL Percorso JSON]** per definire le opzioni utilizzando un percorso file JSON. Di seguito è riportato un esempio di file JSON per definire le opzioni di filtro:

      ```JSON
          {
         "options":[
            {
            "text":"Female",
            "value":"F"
            },
            {
            "text":"Male",
            "value":"M"
            }
          ]
        }
      ```

   1. Seleziona **[!UICONTROL Percorso opzioni CRX]** per definire le opzioni utilizzando i percorsi dell’archivio CRX. Seleziona **[!UICONTROL Aggiungi percorsi opzione]** per aggiungere più percorsi. Di seguito è riportato un esempio per definire `Male` e `Female` opzioni filtro:

      ```JSON
         <gender jcr:primaryType="sling:OrderedFolder">
                        <male
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Male"
                            value="M"/>
                        <female
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Female"
                            value="F"/>
                    </gender>
      ```

1. Specifica una descrizione facoltativa per la configurazione e seleziona **[!UICONTROL Fine]** per salvarlo.

Le modifiche alla configurazione si riflettono all’apertura della pagina Filtri. L&#39;etichetta di filtro specificata nel passaggio 4 viene visualizzata come etichetta per il predicato dell&#39;opzione colonna personalizzata. [!DNL Experience Manager] applica i criteri di ricerca definiti nel passaggio 6 al nome di colonna specificato nel passaggio 3 e restituisce gli elementi della casella in entrata.

Il video seguente illustra i passaggi per filtrare una colonna in base al `true` e `false` valori di opzione.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Visualizzare i filtri di ricerca in base ai predicati {#view-search-filters-for-predicates}

Puoi visualizzare i filtri di ricerca in base ai predicati. Seleziona **[!UICONTROL Filtro]** nella pagina Casella in entrata. I filtri vengono visualizzati nel riquadro a sinistra. È quindi possibile specificare i criteri di ricerca per filtrare gli elementi della casella in entrata.

![Pagina Filtri](assets/apply-filters.png)

Per ulteriori informazioni sulla gestione delle configurazioni dei predicati, vedere [Configurazione di Search Forms](search-forms.md).
