---
title: Guida introduttiva all’editor di comunicazione interattiva (IC)
description: La comunicazione interattiva consente alle organizzazioni di progettare e distribuire comunicazioni personalizzate basate su dati.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 11%

---


# Guida introduttiva all’editor di comunicazione interattiva (IC)

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

L&#39;**editor di comunicazione interattiva** in Adobe Experience Manager (AEM) Forms consente alle organizzazioni di progettare e distribuire comunicazioni personalizzate basate su dati, quali rendiconti, fatture e lettere, tra canali digitali e di stampa. Questa guida fornisce una panoramica su come iniziare, dall’onboarding alla navigazione nell’interfaccia dell’editor IC.


## Onboarding e accesso

### Requisiti di accesso

Per utilizzare la comunicazione interattiva, accertati che il tuo ambiente AEM Forms as a Cloud Service includa il componente aggiuntivo **AEM Forms** e che il tuo account disponga delle autorizzazioni appropriate.

### Verifica il browser

Per conoscere i browser e le piattaforme client supportati, seguire l&#39;articolo collegato, [Piattaforme client supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/overview/supported-platforms)

>[!NOTE]
>
> **Supporto per browser con cicli di rilascio rapidi:**
> Gli aggiornamenti sulle versioni di Firefox, Chrome e Edge sono regolari. Adobe si impegna a mantenere il livello di supporto indicato in precedenza per le prossime versioni di questi browser.

### Configurare ruoli utente e autorizzazioni

L&#39;accesso alle funzionalità dell&#39;editor IC è gestito da [ruoli utente in AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions). Di seguito sono riportati i ruoli chiave coinvolti nella creazione e nella gestione delle comunicazioni interattive:

| **Ruolo** | **Descrizione** | **Autorizzazioni chiave** |
| --------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **Autore modulo** | Crea e modifica le comunicazioni interattive. | Creare, modificare, visualizzare in anteprima e pubblicare IC. |
| **Autore modello** | Progetta modelli riutilizzabili per le comunicazioni interattive. | Creare e bloccare modelli, definire layout. |
| **Amministratore** | Gestisce l’accesso, le autorizzazioni e le configurazioni degli utenti. | Assegna ruoli, gestisci modelli, pubblica IC. |
| **Autore FDM** | [Crea e gestisce modelli di dati modulo (FDM)](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models) per l&#39;integrazione dei dati. | Crea, modifica e configura origini dati e modelli. |

>[!NOTE]
>
> Assicurarsi che gli utenti facciano parte dei gruppi AEM appropriati (ad esempio, `forms-user`, `fdm-author`, `template-authors`) per accedere alle funzioni corrispondenti.

## Accedere all&#39;editor IC

1. Accedi all&#39;istanza **AEM Forms as a Cloud Service**.
2. Passa a **Forms > Comunicazioni interattive**.
3. Fai clic su **Crea** → **Comunicazione interattiva**.
4. Scegli un **Modello**, configura le origini dati e fai clic su **Crea** per aprire **Editor comunicazioni interattive**.

L’editor fornisce un ambiente unificato per progettare, visualizzare in anteprima e gestire le versioni stampate e web delle comunicazioni.

## Navigare nell’interfaccia

L&#39;interfaccia dell&#39;**Editor comunicazioni interattive** è progettata per consentire agli autori un accesso intuitivo a tutti gli strumenti di progettazione e le opzioni di configurazione.

![Trova documento IC](/help/forms/interactive-communication/assets/navigate-the-interface.png)

### &#x200B;1. Barra degli strumenti superiore

![Trova documento IC](/help/forms/interactive-communication/assets/tool-bar.png)

**Posizione:** sezione superiore

**Scopo:** fornisce l&#39;accesso all&#39;ambiente e le azioni globali.

**Include:**

Visualizza l&#39;**ambiente Adobe Experience Cloud** (ad esempio, Gestione temporanea) insieme al **titolo progetto**, **feedback Beta**, **notifiche** e **controlli profilo** per la gestione delle impostazioni utente e dell&#39;accesso all&#39;ambiente.

### &#x200B;2. Barra Delle Schede (Schede Struttura/Master E Controlli File)

![Trova documento IC](/help/forms/interactive-communication/assets/tab-bar.png)

**Posizione:** sotto l&#39;intestazione superiore

**Scopo:** gestire le visualizzazioni e i file di comunicazione.

**Include:**

**Schede:** Passare da **Visualizzazione Struttura** a **Visualizzazione Pagina Master** per layout e struttura elemento riutilizzabile

**Nome file:** Visualizza il titolo della comunicazione corrente (ad esempio, ic-11)

**Visualizza controlli:** opzioni quali regola, creazione, Zoom (85%), Annulla/Ripeti, Elimina, Anteprima PDF e Salva

### &#x200B;3. Pannello sinistro (Strumenti di navigazione e componenti)

![Trova documento IC](/help/forms/interactive-communication/assets/left-panel.png)

**Posizione:** Lato sinistro dell&#39;interfaccia

**Scopo:** accedere alla struttura del progetto, alle risorse riutilizzabili e alle associazioni di dati.

**Include:**

* **Home page:** porta l&#39;utente alla schermata principale della comunicazione interattiva (IC), in cui è possibile visualizzare e gestire gli IC e le cartelle esistenti.

* **Pannello dei menu:** visualizza le opzioni relative alla visualizzazione, ad esempio Righelli, Limiti oggetto, Blocca sulla griglia, Blocca su oggetto caratteristica e la caratteristica Importa XDP.

* **Visualizzazione gerarchia:** visualizza la struttura dei componenti della comunicazione, con l&#39;organizzazione di pagine, pannelli e sottomaschere.

* **Libreria componenti:** contiene elementi di progettazione come Testo, Immagine, Sottomaschera e Codice a barre che possono essere trascinati nell&#39;area di lavoro.

* **Frammenti:** consente di riutilizzare blocchi predefiniti di progettazione e contenuto in più comunicazioni.

* **Modello dati:** collega la comunicazione ai modelli di dati modulo (FDM) sottostanti per l&#39;associazione dei dati dinamici.

### &#x200B;4. Workspace centrale (Design Canvas)

![Trova documento IC](/help/forms/interactive-communication/assets/canvas.png)

**Posizione:** Centro dell&#39;interfaccia

**Scopo:** area di lavoro principale per la progettazione delle comunicazioni interattive.

**Caratteristiche:**

* Trascinare i componenti dalla libreria

* Disporre e formattare il layout visivo

* Aggiungere o modificare pagine, sottomaschere e campi

* Naviga tra le pagine (ad esempio, &quot;1 di 1&quot;) utilizzando i controlli in basso a sinistra

* Anteprima del layout finale prima della pubblicazione

### &#x200B;5. Pannello a destra (pannello Proprietà)

![Trova documento IC](/help/forms/interactive-communication/assets/right-panel.png)

**Posizione:** lato destro dello schermo

**Scopo:** personalizzare il comportamento e lo stile dei componenti.

**Include:**

* Impostazioni generali (nome, tipo, flusso/posizione)

* Opzioni layout e aspetto

* Controlli di impaginazione, posizione, presenza e associazione dati