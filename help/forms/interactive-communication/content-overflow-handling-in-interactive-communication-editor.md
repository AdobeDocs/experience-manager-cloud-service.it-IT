---
title: Gestione dell’overflow dei contenuti nell’editor di comunicazioni interattive
description: La gestione dell'overflow dei contenuti nell'Editor comunicazioni interattive migliora il comportamento del testo all'interno dei layout con flusso e posizionamento.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0cfbf6d61bc2d557b0a096db5b3cb26ae4570748
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 16%

---


# Gestione dell’overflow dei contenuti nell’editor di comunicazioni interattive

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## Introduzione

La funzione Gestione dell&#39;overflow del contenuto nell&#39;Editor comunicazioni interattive migliora il comportamento del testo all&#39;interno dei layout con flusso e posizionamento.
Garantisce una fluida continuità dei contenuti per i layout a flusso continuo e fornisce avvisi visivi per i layout posizionati, offrendo agli autori un controllo migliore e una maggiore flessibilità nella progettazione delle comunicazioni.

## Funzionalità principali

### Layout flusso

- **Nuova opzione:**
Aggiunge una proprietà **consenti interruzioni di pagina** all&#39;interno del contenuto per controllare il comportamento di overflow. Questa opzione è visibile solo quando la sottomaschera padre è impostata su Flowed e la relativa proprietà **Consenti interruzioni di pagina** è abilitata.

- **Continuazione automatica pagine:**
Quando il contenuto supera lo spazio disponibile, viene creata automaticamente una nuova pagina e la modifica continua senza interruzioni.

- **Supporto copia-incolla:**
Il testo di grandi dimensioni incollato nell’editor scorre automaticamente tra le pagine, mantenendo la coerenza del layout.

### Layout posizionato

- **Indicatore di overflow:**
Quando il contenuto supera il contenitore (sottomaschera o pagina), l’editor di testo si espande per la modifica, ma l’altezza dell’elemento rimane fissa.

- **Avviso visivo:**
Nella parte inferiore del contenitore viene visualizzato un bordo rosso per indicare l&#39;overflow.

- **Regolazione manuale:**
Gli autori ridimensionano manualmente il contenitore per adattarlo a contenuto aggiuntivo.

>[!NOTE]
>
> Questa funzione richiede che l’intera gerarchia principale (ad esempio le sottomaschere) sia impostata su Flussi. Se un sottomodulo padre nella gerarchia è posizionato, l&#39;opzione **Consenti interruzioni di pagina** all&#39;interno del contenuto non funzionerà come previsto.

## Vantaggi

- Migliora l’efficienza e il controllo nell’authoring dei contenuti.

- Mantiene un layout coerente e la leggibilità tra le pagine.

- Consente di identificare rapidamente l&#39;overflow attraverso indicatori visivi.

- Migliora la flessibilità di progettazione delle comunicazioni per entrambi i tipi di layout.
