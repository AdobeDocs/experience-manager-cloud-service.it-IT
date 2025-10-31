---
title: Blocco modello nell’editor di comunicazione interattiva
description: Blocco modelli nell'Editor comunicazioni interattive consente agli autori dei modelli di bloccare il layout o il contenuto per gli autori dei documenti.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 11%

---


# Blocco modello nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

La funzione Blocco modello nell’editor di comunicazione interattiva (IC) consente agli autori di modelli di limitare le modifiche a elementi specifici di un modello di comunicazione. In questo modo viene garantita la coerenza della progettazione, vengono protetti i contenuti critici e viene applicata la governance tra i team che riutilizzano i modelli per creare comunicazioni personalizzate.

Quando applicati, i componenti bloccati appaiono visivamente distinti e non possono essere modificati dagli autori o dai collaboratori a valle, a seconda del tipo di blocco impostato. Questa funzione consente di mantenere gli standard del marchio, l’integrità dei dati e l’uniformità del layout in tutte le comunicazioni derivate.

## &#x200B;2. Tipi di blocco

Gli autori dei modelli possono applicare blocchi di contenuto e layout, singolarmente o insieme, per controllare le modifiche al contenuto e al layout nei modelli di comunicazione interattiva:

### 2.1 Blocco dei contenuti

Un blocco di contenuto limita qualsiasi modifica al contenuto o alle proprietà dell’elemento selezionato. Questo tipo di blocco assicura che le proprietà essenziali di dati, testo o progettazione rimangano invariate, anche se vengono riutilizzate in più comunicazioni.

Quando applicati, gli autori non possono modificare:

- Contenuto testo o didascalie

- Impostazioni di aspetto (font, colore, sfondo, bordi, ecc.)

- Configurazioni di associazione dati

- Elementi costitutivi all’interno di un componente contenitore (come sottomaschere)

### 2.2 Blocco layout

Un blocco di layout limita le modifiche relative alla posizione e alle dimensioni di un elemento. In questo modo l’allineamento visivo e la gerarchia di progettazione rimangono coerenti con gli standard del marchio o del documento.

Quando applicati, gli autori non possono:

- Spostare l&#39;elemento in una nuova posizione nella pagina

- Ridimensionare la larghezza o l&#39;altezza dell&#39;elemento

## &#x200B;3. Comportamento nelle comunicazioni derivate

- Quando una comunicazione viene creata da un modello bloccato, gli elementi bloccati vengono visualizzati in sola lettura nell&#39;editor IC per gli autori di comunicazioni.

- I componenti con blocco del contenuto non possono avere proprietà interne o binding modificati.

- I componenti con blocco layout non possono essere spostati o ridimensionati.

Questo consente ai creatori di modelli di mantenere il controllo sulla progettazione e sulla struttura, consentendo ad altri utenti di concentrarsi sul contenuto variabile e sulla personalizzazione basata sui dati.

## &#x200B;4. Best practice

- **Blocca in anticipo i componenti critici:** Applica blocchi a intestazioni, piè di pagina, disclaimer legali e loghi per preservare la conformità e l&#39;identità del brand.

- **Utilizzare i blocchi di contenuto per la precisione:** Proteggere i campi associati ai modelli di dati di base o al testo normativo.

- **Utilizzare i blocchi di layout per coerenza:** evitare il disallineamento o la distorsione visiva nei modelli riutilizzati di frequente.

- **Comunica l&#39;utilizzo del blocco:** Assicurarsi che gli utenti a valle siano consapevoli di quali sezioni sono state intenzionalmente limitate per evitare confusione.
