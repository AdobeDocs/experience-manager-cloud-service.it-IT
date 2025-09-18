---
title: Aggiornamenti della versione di AEM
description: Scopri in che modo Adobe Experience Manager (AEM) as a Cloud Service utilizza l’integrazione e la distribuzione continue (CI/CD) per mantenere i progetti sull’ultima versione.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
role: Admin
source-git-commit: 01de7b0c4e0408a3bbc5322e37db5075d43c4c5f
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 2%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

Scopri in che modo Adobe Experience Manager (AEM) as a Cloud Service utilizza l’integrazione e la distribuzione continue (CI/CD) per mantenere i progetti sull’ultima versione.

## CI/CD {#ci-cd}

AEM as a Cloud Service utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i progetti siano nella versione di AEM più recente. Questo processo aggiorna facilmente le istanze di produzione, staging e sviluppo senza causare interruzioni agli utenti.

>[!NOTE]
> Poiché le istanze di sviluppo sono già aggiornate automaticamente, gli aggiornamenti manuali per le istanze di sviluppo potrebbero non essere disponibili per _alcuni_ programmi. Questa funzione viene convertita in aggiornamenti automatici.

Prima che le istanze vengano aggiornate automaticamente, viene pubblicata una nuova versione di manutenzione di AEM con 3-5 giorni di anticipo. Durante questo periodo, l&#39;istanza di sviluppo potrebbe essere aggiornata automaticamente o, nel caso sia disponibile, puoi facoltativamente [attivare l&#39;aggiornamento per le istanze di sviluppo](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). Gli aggiornamenti delle versioni vengono prima applicati automaticamente agli ambienti di sviluppo. Se l’aggiornamento ha esito positivo, il processo di aggiornamento procede alle istanze di staging e produzione. Le istanze di sviluppo e staging fungono da gate di qualità automatizzato, in cui i test scritti personalizzati vengono eseguiti prima dell’applicazione dell’aggiornamento all’ambiente di produzione.

### NIMU (aggiornamenti di manutenzione non intrusivi) {#nimu}

Gli aggiornamenti di manutenzione non intrusivi sono aggiornamenti automatici applicati senza coinvolgere le pipeline dei clienti.
Tramite NIMU, il cliente può utilizzare la pipeline in qualsiasi momento, anche se è pianificato o in corso un aggiornamento della versione di AEM e gli aggiornamenti di manutenzione non verranno più visualizzati nella cronologia di esecuzione della pipeline del cliente, semplificando il monitoraggio della cronologia delle distribuzioni del codice.

#### Aggiorna attività

Puoi comunque controllare la versione corrente di AEM per ogni ambiente, come prima, utilizzando il pannello Ambienti dell’interfaccia utente di Cloud Manager. Gli stessi gate di qualità utilizzati nella pipeline vengono utilizzati dagli aggiornamenti di manutenzione non intrusivi, inclusi i test scritti dal cliente.
Una [notifica dell&#39;interfaccia utente di Cloud Manager](/help/implementing/cloud-manager/notifications.md) verrà inviata ogni volta che viene applicato un aggiornamento di manutenzione non intrusivo agli ambienti del programma. Puoi configurarlo per l’invio anche all’e-mail.

>[!NOTE]
>
> Nota: gli aggiornamenti di manutenzione non intrusivi verranno progressivamente abilitati per tutti i clienti nel 2024.

## Tipo di aggiornamenti {#update-types}

Esistono due tipi di aggiornamenti delle versioni di AEM:

* [**Aggiornamenti di manutenzione di AEM**](/help/release-notes/maintenance/latest.md)

   * Sono per lo più a scopo di manutenzione, comprese le ultime correzioni di bug e gli aggiornamenti di sicurezza.
   * L’impatto è minimo perché le modifiche vengono applicate regolarmente.

* [**Attivazione funzione AEM**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * Vengono rilasciati in base a una pianificazione mensile prevedibile.

>[!NOTE]
>
> Controlla le date chiave per i rilasci mensili nella roadmap delle versioni di [Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it#aem-as-cloud-service) e segna i tuoi calendari per prepararti alle attività chiave necessarie per la preparazione alla versione.

## Errore di aggiornamento {#update-failure}

Gli aggiornamenti di AEM vengono sottoposti a una pipeline di convalida dei prodotti intensa e completamente automatizzata che prevede più passaggi, garantendo l’assenza di interruzioni del servizio per tutti i sistemi in produzione. I controlli di integrità vengono utilizzati per monitorare lo stato dell&#39;applicazione. Se questi controlli non vanno a buon fine durante un aggiornamento di AEM as a Cloud Service, la versione non procede e Adobe indaga sul motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

Quando distribuisci una nuova versione del codice personalizzato nel tuo ambiente, [I test funzionali del prodotto e personalizzati](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) svolgono un ruolo cruciale. Essi garantiscono che i sistemi di produzione rimangano stabili e funzionanti anche dopo l’applicazione di una modifica. Questi test vengono applicati anche nel processo di aggiornamento della versione di AEM.

Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e produzione utilizzino la stessa versione di AEM.
Analogamente, se un aggiornamento automatico di un ambiente di sviluppo non riesce, gli ambienti di staging e produzione non vengono aggiornati.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e non alla produzione, il prossimo aggiornamento di AEM rimuove tali modifiche per riflettere il tag Git dell’ultima versione del cliente alla produzione con esito positivo. Pertanto, il codice personalizzato disponibile solo nell’area di gestione temporanea deve essere nuovamente distribuito.

## Best practice {#best-practices}

* **Utilizzo ambiente di staging**
   * Utilizza un ambiente diverso (non stage) per lunghi cicli di QA/UAT.
   * Una volta completato il test di integrità su Stage, spostati per verificare in Produzione.

* **Pipeline di produzione**
   * Sospendi prima di implementare in produzione.
   * L&#39;annullamento della pipeline dopo una distribuzione di staging indica che il codice è &quot;uno scarto&quot; e non è un candidato valido per la produzione. Fare riferimento a [Configurazione di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **Pipeline non di produzione**
   * Configura una [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
   * Accelerare la velocità/frequenza di consegna in caso di errori della pipeline di produzione. Identifica i problemi nelle pipeline non di produzione abilitando i test funzionali del prodotto, i test funzionali personalizzati e i test dell’interfaccia utente personalizzati.

* **Copia contenuto**
   * Utilizza [Copia contenuto](/help/implementing/developing/tools/content-copy.md) per spostare set di contenuti simili in un ambiente non di produzione.

* **Test funzionali automatizzati**
   * Includi test automatizzati nella pipeline per testare le funzionalità critiche.
   * [I test funzionali del cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) e [i test dell&#39;interfaccia utente personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) sono bloccati se non riescono a eseguire il rollout della versione di AEM.

## Regressione {#regression}

Se riscontri un problema relativo alla regressione, invia un caso di supporto tramite Admin Console. Se il problema è un bloccante e il suo impatto sulla produzione, deve essere sollevato un P1. Fornire tutti i dettagli necessari per riprodurre il problema di regressione.

## Archivio nodi compositi {#composite-node-store}

In genere, gli aggiornamenti non comportano tempi di inattività, incluso per l’istanza di authoring, che è un cluster di nodi. Aggiornamenti continui sono possibili a causa di [la funzionalità archivio nodi composito in Oak](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html).

Questa funzione consente ad AEM di fare riferimento simultaneamente a più archivi. In una [distribuzione continua](/help/implementing/deploying/overview.md#how-rolling-deployments-work), la nuova versione di AEM contiene il proprio `/libs` (l&#39;archivio immutabile basato su TarMK). Si distingue dalla versione precedente di AEM, anche se entrambi fanno riferimento a un archivio condivise mutabile basato su DocumentMK che contiene aree come `/content` , `/conf` , `/etc` e altri.

Poiché sia la versione precedente che quella nuova hanno versioni proprie di `/libs`, possono essere entrambe attive durante l&#39;aggiornamento continuo. E, entrambi possono prendere il traffico fino a quando il vecchio è completamente sostituito dal nuovo.

## Ulteriori informazioni {#further-information}

Per maggiori dettagli sui temi correlati:

* [Pipeline CI/CD di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)
* [Notifica interfaccia utente Cloud Manager](/help/implementing/cloud-manager/notifications.md)
* [Architettura di Adobe Experience Manager as a Cloud Service](/help/overview/architecture.md)
