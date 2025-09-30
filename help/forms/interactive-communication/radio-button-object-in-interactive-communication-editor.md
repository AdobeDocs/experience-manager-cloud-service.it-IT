---
title: Oggetto pulsante di scelta nell’editor di comunicazione interattiva
description: L’oggetto pulsante di scelta nell’Editor comunicazioni interattive di AEM Forms consente agli autori di presentare agli utenti un insieme di scelte che si escludono a vicenda, il che significa che è possibile selezionare una sola opzione alla volta.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 9%

---


# Oggetto pulsante di scelta nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente **Pulsante di opzione** nell&#39;editor di comunicazione interattiva (IC) consente agli autori di presentare agli utenti un insieme di scelte che si escludono a vicenda, il che significa che è possibile selezionare una sola opzione alla volta. Questo lo rende ideale per casi d’uso come domande di tipo Sì/No, selezione del genere, livelli di valutazione o risposte categoriche predefinite.
I pulsanti di scelta sono intuitivi, facili da configurare e possono essere associati a modelli di dati back-end per l’acquisizione e l’integrazione fluide dei dati.

![Trova documento IC](/help/forms/interactive-communication/assets/radio.png)

## &#x200B;2. Proprietà

L&#39;oggetto Radio Button include diverse proprietà configurabili:

2.1. Campo di base

- **Nome:** Identificatore univoco del campo. Viene utilizzato per fare riferimento a in modelli di dati, regole e logica di business.

- **Attiva/Disattiva:** consente di definire ogni scelta selezionabile nel gruppo di pulsanti. Ogni interruttore rappresenta un valore possibile.

- **Didascalia:** etichetta associata al gruppo di pulsanti di scelta per guidare l&#39;utente.

- **Riserva:** Valore di fallback facoltativo se non viene effettuata alcuna selezione o se l&#39;associazione dati è vuota.

2.2. Posizione

Descrizione: controlla la posizione spaziale del gruppo di pulsanti di scelta nel layout.

**Impostazioni:**

- **coordinate X e Y**

- **Altezza e larghezza** (definite in mm o % per la progettazione di layout reattivo)

2.3. Margine

Definire la spaziatura attorno alla casella di testo:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.4. Presenza

- **Descrizione:** Determina la visibilità dell&#39;oggetto pulsante di scelta in fase di esecuzione.

- **Opzioni:**

   - **Visibile:** visualizzato agli utenti e occupa spazio.

   - **Nascosto (mantiene spazio):** Non visibile ma mantiene la spaziatura del layout.



2.5. Associazione dei dati

- **Descrizione:** collega il gruppo di pulsanti di scelta a un modello di dati per acquisire l&#39;opzione selezionata.

- **Tipi di associazione:**

   - **Usa nome:** Utilizza il nome del campo assegnato come riferimento per l&#39;associazione.

   - **Usa dati globali:** associa il campo a un modello di dati globale o a un elemento dello schema.

   - **Nessuna associazione dati:** La selezione del pulsante di opzione non è associata ad alcuna origine dati. Utilizzata per il comportamento solo dell&#39;interfaccia utente.

## &#x200B;3. Utilizzo

Il componente Pulsante di opzione è adatto per gli scenari in cui gli utenti devono scegliere un solo valore da un elenco. I casi d’uso tipici includono:

- Selezione di un metodo di comunicazione preferito (e-mail/telefono/SMS)

- Conferma delle decisioni binarie (Sì / No)

- Scelta tra opzioni limitate (ad esempio, genere, stato civile)

- Indicare i livelli di soddisfazione o le scale dell’accordo (ad esempio, In disaccordo / Neutro / In accordo)

Gli autori possono raggruppare i pulsanti di scelta correlati e posizionarli all’interno dei contenitori di layout per un allineamento coerente. Le etichette possono essere posizionate in linea o sopra i pulsanti a seconda dei requisiti di progettazione visiva.

## &#x200B;4. Best practice

- Limita il numero di opzioni a un massimo di 5 per evitare di sopraffare l’utente.

- Utilizza sottotitoli chiari e concisi per descrivere ciò che l’utente sta selezionando.

- Se necessario, preseleziona la scelta più comune o sicura.

- Evita di utilizzare i pulsanti di scelta quando agli utenti deve essere consentito scegliere più di un’opzione, utilizza invece le caselle di controllo.

- Associa i pulsanti di scelta direttamente ai nodi dello schema durante l’integrazione con modelli di dati back-end.

- Applicate spaziature e allineamenti coerenti per una maggiore chiarezza visiva, in particolare nei layout facili da usare sui dispositivi mobili.

L’oggetto Pulsante di scelta nell’editor di comunicazioni interattive è un componente di input fondamentale che offre agli utenti finali un processo decisionale pulito e strutturato. Se configurato con etichette chiare, spaziatura accurata e associazione dati, garantisce una raccolta dati affidabile e un’esperienza utente più fluida per moduli, sondaggi e flussi di lavoro di onboarding.


