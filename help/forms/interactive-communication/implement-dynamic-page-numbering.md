---
title: Numerazione dinamica delle pagine nell’editor di comunicazione interattiva
description: La numerazione dinamica delle pagine nell’editor di comunicazioni interattive consente agli autori di visualizzare automaticamente i numeri di pagina nell’output PDF.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 13%

---


# Numerazione dinamica delle pagine nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## Introduzione

La funzione di numerazione dinamica delle pagine nella comunicazione interattiva (IC) consente agli autori di visualizzare automaticamente i numeri di pagina nell’output PDF. La numerazione delle pagine può essere attivata a livello di pagina master, garantendo una numerazione coerente in tutte le pagine di progettazione associate. Questo consente di mantenere un tracciamento chiaro delle pagine e un layout professionale per tutte le comunicazioni multipagina.

![Trova documento IC](/help/forms/interactive-communication/assets/dynamic-page.png)

## Come utilizzare la numerazione dinamica delle pagine nell’editor di comunicazione interattiva

1. Apri l’editor di comunicazione interattiva
Apri il progetto di comunicazione interattiva nell’editor IC.

1. Vai a pagina mastro
La numerazione delle pagine può essere attivata solo nella pagina master. Passare alla pagina master della comunicazione.

1. Abilita numerazione pagine
Nel pannello Proprietà, attivate l&#39;interruttore Abilita numero di pagina. In questo modo i numeri di pagina vengono aggiunti automaticamente a tutte le pagine associate.

1. Personalizza posizionamento
Il componente Numero di pagina può essere posizionato ovunque nell’area di lavoro dopo essere stato rilasciato e personalizzato liberamente utilizzando le proprietà di testo standard.

1. Anteprima in PDF
I numeri di pagina vengono visualizzati solo durante l&#39;anteprima di PDF, con numerazione dinamica su ogni pagina.

## Funzionalità principali

- **Configurazione pagina master:**
La numerazione delle pagine può essere attivata a livello di pagina master. Il componente può essere posizionato ovunque nell’area di lavoro dopo essere stato rilasciato e personalizzato liberamente, in quanto supporta tutte le proprietà disponibili nel componente testo.

- **Posizionamento automatico:**
Nella parte inferiore centrale di ogni pagina viene visualizzato un componente di numerazione delle pagine con il formato:
&quot;**N. pagina di ##**&quot;

   - Il primo **#** rappresenta il numero di pagina corrente.

   - Il secondo **##** rappresenta il numero totale di pagine nella comunicazione.

- **Visualizzazione dinamica in anteprima PDF:**
I numeri di pagina vengono riprodotti in modo dinamico durante l’anteprima di PDF, mostrando una numerazione accurata delle pagine nell’output finale.

### Esempio

Quando visualizzi l’anteprima di una comunicazione interattiva di 5 pagine, ogni pagina visualizza:

Pagina 1 di 5

Pagina 2 di 5

... e così via, con aggiornamento dinamico durante la generazione di PDF.

## Vantaggi principali

- Migliora la leggibilità e la professionalità dei documenti.

- Automatizza la numerazione delle pagine senza intervento manuale.

- Mantiene la coerenza su tutte le pagine collegate a una pagina master.
