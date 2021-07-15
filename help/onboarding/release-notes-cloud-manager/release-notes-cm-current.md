---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.7.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.7.0
feature: Informazioni sulla versione
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: e24610cef6d134ddf9ce8abe9a5893deac08eeb6
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.7.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.7.0.

>[!NOTE]
>Per visualizzare il Cloud Service delle note sulla versione corrente per Adobe Experience Manager, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.7.0 è il 15 luglio 2021.
La prossima versione è prevista per il 12 agosto 2021.

### Novità {#what-is-new}

* I clienti ora possono utilizzare Azul 8 e 11 JDK per i processi di creazione di Cloud Manager e possono scegliere di utilizzare uno di questi JDK per i plug-in Maven compatibili con toolchain *o* per l’intera esecuzione del processo Maven.

* L&#39;IP in uscita verrà ora registrato nel file di registro dei passaggi della build.

* Gli ambienti di stage e produzione che eseguono versioni precedenti di AEM ora segnalano lo stato **Aggiorna disponibile**.

* Il numero massimo di certificati SSL supportati è aumentato a 20 per programma.

* Il numero massimo di domini configurabili è aumentato a 500 per ambiente.

* I pulsanti **Manage Git** (Gestisci Git) sono stati rinominati in **Access Git Info** e la finestra di dialogo è stata aggiornata visivamente.

* La versione di AEM Project Archetype utilizzata da Cloud Manager è stata aggiornata alla versione 28.

### Correzioni di bug {#bug-fixes}

* In alcune situazioni, l’opzione Anteprima non era disponibile durante il binding di un Elenco consentiti IP a un ambiente.

* La navigazione manuale alla pagina dei dettagli di esecuzione per un’esecuzione non esistente non mostrava un errore, ma solo una schermata di caricamento infinita.

* Il messaggio di errore visualizzato quando è stato raggiunto il numero massimo di certificati SSL non è stato utile.

* In alcune circostanze, potrebbe esserci una discrepanza nella versione di rilascio mostrata nella scheda della pipeline nella pagina **Panoramica** .

* Aggiunta guidata programma non corretta: il nome non può essere modificato dopo la creazione.

### Problemi noti {#known-issues}

I clienti che passano all&#39;uso di Azul JDK dovrebbero essere consapevoli che non tutte le applicazioni esistenti si compileranno senza errori su Azul JDK. Si consiglia vivamente di eseguire il test localmente prima di passare a un altro metodo.

