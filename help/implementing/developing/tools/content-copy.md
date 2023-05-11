---
title: Lo strumento Copia contenuto
description: Lo strumento di copia del contenuto consente agli utenti di copiare contenuti mutabili on demand dai loro ambienti di produzione as a Cloud Service AEM agli ambienti di produzione più bassi a scopo di test.
source-git-commit: 4a5470ae8fe5a8e7f615009bf5f6b180aee4669b
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 64%

---


# Lo strumento Copia contenuto {#content-copy}

Lo strumento di copia del contenuto consente agli utenti di copiare contenuti mutabili on demand dai loro ambienti di produzione as a Cloud Service AEM agli ambienti di produzione più bassi a scopo di test.

## Introduzione {#introduction}

I dati attuali e reali sono utili a scopo di test, convalida e accettazione da parte degli utenti. Lo strumento di copia del contenuto consente di copiare il contenuto da un ambiente di produzione AEM a uno staging, sviluppo o [Ambiente di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ambiente per tali test.

Il contenuto da copiare è definito da un set di contenuti. Un set di contenuti è costituito da un elenco di percorsi JCR che contengono il contenuto mutabile da copiare da un ambiente del servizio di authoring sorgente a un ambiente del servizio di authoring di destinazione all’interno dello stesso programma Cloud Manager. I percorsi seguenti sono consentiti in un set di contenuti.

```text
/content
/conf/**/settings/wcm
/conf/**/settings/dam/cfm/models
/conf/**/settings/graphql/persistentQueries
/etc/clientlibs/fd/themes
```

Durante la copia del contenuto, l’ambiente sorgente è l’origine di riferimento.

* Se il contenuto è stato modificato nell’ambiente di destinazione e i percorsi sono gli stessi, verrà sovrascritto dal contenuto nell’origine.
* Se i percorsi sono diversi, il contenuto dell’origine verrà unito al contenuto della destinazione.

## Autorizzazioni {#permissions}

Per utilizzare lo strumento Copia contenuto, sono necessarie alcune autorizzazioni sia nell’ambiente sorgente che in quello di destinazione.

| Funzione Copia contenuto | Gruppo di amministratori AEM | Ruolo Responsabile della distribuzione |
|---|---|---|
| Creare e modificare il [set di contenuti](#create-content-set) | Obbligatorio | Non obbligatorio |
| Avviare o annullare il [processo di copia del contenuto](#copy-content) | Obbligatorio | Obbligatorio |

## Creazione di un set di contenuti {#create-content-set}

Prima di copiare qualsiasi contenuto, è necessario definire un set di contenuti. Una volta definiti, i set di contenuti possono essere riutilizzati per copiare il contenuto. Per creare un set di contenuti, effettua le seguenti operazioni.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla schermata **Ambienti**, passa alla pagina **Set di contenuti**.

1. Tocca o fai clic sul pulsante **Aggiungi set di contenuti** in alto a destra dello schermo.

   ![Set di contenuti](assets/content-sets.png)

1. Sulla **Dettagli** scheda della procedura guidata, specifica un nome e una descrizione per il set di contenuti e tocca o fai clic su **Continua**.

   ![Dettagli dei set di contenuti](assets/add-content-set-details.png)

1. Nella scheda **Percorsi del contenuto** della procedura guidata, specifica i percorsi del contenuto modificabile da includere nel set di contenuti.

   1. Immetti il percorso nel campo **Aggiungi percorso di inclusione**.
   1. Tocca o fai clic sul pulsante **Aggiungi percorso** per aggiungere il percorso al set di contenuti.
   1. Se necessario, tocca o fai clic di nuovo sul pulsante **Aggiungi percorso**.
      * Sono consentiti fino a cinquanta percorsi.

   ![Aggiungi percorsi al set di contenuti](assets/add-content-set-paths.png)

1. Se devi perfezionare o limitare il set di contenuti, è possibile escludere i percorsi secondari.

   1. Nell’elenco dei percorsi inclusi, tocca o fai clic sull’icona **Aggiungi percorsi secondari di esclusione** accanto al percorso da limitare.
   1. Inserisci il percorso secondario da escludere sotto il percorso selezionato.
   1. Tocca o fai clic su **Escludi percorso**.
   1. Tocca o fai clic di nuovo su **Aggiungi percorsi secondari di esclusione** per aggiungere altri percorsi da escludere, se necessario.
      * I percorsi esclusi devono essere relativi al percorso incluso.
      * Non esiste alcun limite al numero di percorsi esclusi.

   ![Esclusione dei percorsi](assets/add-content-set-paths-excluded.png)

1. Se necessario, è possibile modificare i percorsi specificati.

   1. Tocca o fai clic sulla X accanto ai percorsi secondari esclusi per eliminarli.
   1. Tocca o fai clic sul pulsante con i puntini di sospensione accanto ai percorsi per visualizzare le opzioni **Modifica** ed **Elimina**.

   ![Modifica dell’elenco dei percorsi](assets/add-content-set-excluded-paths.png)

1. Tocca o fai clic su **Crea** per creare il set di contenuti.

Il set di contenuti può ora essere utilizzato per copiare il contenuto tra ambienti diversi.

## Modifica di un set di contenuti {#edit-content-set}

Segui passaggi simili a quelli impiegati per la creazione del contenuto. Invece di toccare o fare clic su **Aggiungi set di contenuti**, seleziona un set esistente dalla console e quindi **Modifica** dal menu con i puntini di sospensione.

![Modifica set di contenuti](assets/edit-content-set.png)

Quando modifichi il set di contenuti, potrebbe essere necessario espandere i percorsi configurati per visualizzare i percorsi secondari esclusi.

## Copia del contenuto {#copy-content}

Una volta creato un set di contenuti, puoi utilizzarlo per copiare il contenuto. Per copiare il contenuto, effettua le seguenti operazioni.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla schermata **Ambienti**, passa alla pagina **Set di contenuti**.

1. Seleziona un set di contenuti dalla console e seleziona **Copia contenuto** dal menu con i puntini di sospensione.

   ![Copia contenuto](assets/copy-content.png)

   >[!NOTE]
   >
   >Un ambiente può non essere selezionabile se:
   >
   >* L’utente non dispone delle autorizzazioni appropriate.
   >* L’ambiente dispone di una pipeline in esecuzione o di un’operazione di copia del contenuto in corso.
   >* L&#39;ambiente è in ibernazione o in fase di avvio.


1. Nella finestra di dialogo **Copia contenuto**, specifica l’origine e la destinazione dell’azione di copia del contenuto.

   ![Copia del contenuto](assets/copying-content.png)

   * Il contenuto può essere copiato solo da un ambiente superiore a un ambiente inferiore o tra ambienti di sviluppo/RDE in cui la gerarchia degli ambienti è la seguente (dal più alto al più basso):
      * Produzione
      * Staging
      * Sviluppo/RDE

1. Se necessario, puoi anche selezionare **Includi elenchi di controllo di accesso** nel processo di copia.

1. Tocca o fai clic su **Copia**.

Viene avviato il processo di copia. Lo stato del processo di copia si riflette nella console del set di contenuti selezionato.

## Attività copia contenuto {#copy-activity}

Puoi monitorare lo stato dei processi di copia nella pagina **Attività copia contenuto**.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla schermata **Ambienti**, passa alla pagina **Attività copia contenuto**.

![Attività copia contenuto](assets/copy-content-activity.png)

### Stati della copia del contenuto {#statuses}

Una volta iniziata la copia del contenuto, il processo può trovarsi in uno dei seguenti stati.

| Stato | Descrizione |
|---|---|
| In corso | Operazione di copia del contenuto in corso |
| Non riuscito | Operazione di copia del contenuto non riuscita |
| Completato | Operazione di copia del contenuto completata |
| Annullato | L&#39;utente annulla un&#39;operazione di copia del contenuto dopo averlo avviato |

### Annullamento di un processo di copia {#cancelling}

Se è necessario interrompere un’operazione di copia del contenuto dopo averlo avviato, è possibile annullarla.

Per farlo, nella **Copia attività contenuto** , seleziona la **Annulla** dal menu dei puntini di sospensione del processo di copia avviato in precedenza.

![Annulla copia contenuto](assets/content-copy-cancel.png)

>[!NOTE]
>
>Quando si annulla un’operazione di copia del contenuto, è possibile ottenere una copia parziale del contenuto nell’ambiente di destinazione. Questo può rendere inutilizzabile l’ambiente di destinazione.
>
>Se il tuo ambiente si trova in tale stato a causa della cancellazione, contatta l’Assistenza clienti di Adobe.

## Limitazioni {#limitations}

Lo strumento Copia contenuto presenta le seguenti limitazioni.

* Il contenuto non può essere copiato da un ambiente inferiore a un ambiente superiore.
* Il contenuto può essere copiato solo da e verso i servizi di authoring.
* Non è possibile copiare il contenuto tra più programmi.
* Non è possibile eseguire operazioni simultanee di copia del contenuto nello stesso ambiente.
* È possibile specificare fino a cinquanta percorsi per set di contenuti. Non ci sono limitazioni per i percorsi esclusi.
* Lo strumento Copia contenuto non deve essere utilizzato come strumento di duplicazione o mirroring perché non può tenere traccia del contenuto spostato o eliminato nell’origine.
* Lo strumento Copia contenuto non dispone di funzionalità di controllo delle versioni e non è in grado di rilevare automaticamente il contenuto modificato o appena creato nell’ambiente di origine in un set di contenuti dall’ultima operazione di copia di contenuto.
   * Se desideri aggiornare l’ambiente di destinazione con modifiche al contenuto solo a partire dall’ultima operazione di copia del contenuto, devi creare un set di contenuti e specificare i percorsi nell’istanza sorgente in cui sono state apportate modifiche dopo l’ultima operazione di copia del contenuto.
* Le informazioni sulla versione non sono incluse in una copia del contenuto.
