---
title: Aggiornamenti della versione di AEM
description: Scopri in che modo Adobe Experience Manager (AEM) as a Cloud Service utilizza Continuous Integration and Delivery (CI/CD) per mantenere i progetti sull’ultima versione.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 9bfea65c07da5da044df8f698e409eab5c4320fb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 3%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

Scopri in che modo Adobe Experience Manager (AEM) as a Cloud Service utilizza Continuous Integration and Delivery (CI/CD) per mantenere i progetti sull’ultima versione.

## CI/CD {#ci-cd}

AEM as a Cloud Service utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i tuoi progetti siano nella versione dell’AEM più recente. Questo processo aggiorna facilmente le istanze di produzione, staging e sviluppo senza causare interruzioni agli utenti.

Prima che le istanze vengano aggiornate automaticamente, viene pubblicata una nuova versione di manutenzione dell’AEM con 3-5 giorni di anticipo. Durante questo periodo, puoi facoltativamente [attivare gli aggiornamenti manuali per le istanze di sviluppo](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). Trascorso questo periodo di tempo, gli aggiornamenti delle versioni vengono applicati automaticamente agli ambienti di sviluppo. Se l’aggiornamento ha esito positivo, il processo di aggiornamento procede alle istanze di staging e produzione. Le istanze di sviluppo e staging fungono da gate di qualità automatizzato, in cui i test scritti personalizzati vengono eseguiti prima dell’applicazione dell’aggiornamento all’ambiente di produzione.

>[!NOTE]
>
> Nota: gli aggiornamenti automatici per gli ambienti di sviluppo vengono progressivamente abilitati nel 2023 per tutti i clienti. Se gli ambienti di sviluppo non vengono aggiornati automaticamente, puoi utilizzare gli aggiornamenti manuali per mantenerli sincronizzati con gli ambienti di staging e produzione.


## Tipo di aggiornamenti {#update-types}

Esistono due tipi di aggiornamenti delle versioni di AEM:

* [**Aggiornamenti di manutenzione di AEM**](/help/release-notes/maintenance/latest.md)

   * Sono per lo più a scopo di manutenzione, comprese le ultime correzioni di bug e gli aggiornamenti di sicurezza.
   * L’impatto è minimo perché le modifiche vengono applicate regolarmente.

* [**Aggiornamenti con nuove funzioni**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * Vengono rilasciati in base a una pianificazione mensile prevedibile.

>[!NOTE]
>
> Controlla le date chiave per i rilasci mensili sul [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it#aem-as-cloud-service) e segnare i calendari per prepararsi alle attività chiave necessarie per la preparazione alla versione.

## Errore di aggiornamento {#update-failure}

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata che coinvolge più fasi, garantendo l&#39;assenza di interruzioni del servizio per tutti i sistemi in produzione. I controlli di integrità vengono utilizzati per monitorare lo stato dell&#39;applicazione. Se questi controlli non vanno a buon fine durante un aggiornamento as a Cloud Service dell’AEM, la versione non procede e Adobe indaga il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

Quando distribuisci una nuova versione del codice personalizzato nel tuo ambiente, [Test funzionali del prodotto e personalizzati](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) svolgere un ruolo cruciale. Essi garantiscono che i sistemi di produzione rimangano stabili e funzionanti anche dopo l’applicazione di una modifica. Questi test vengono applicati anche nel processo di aggiornamento della versione AEM.

Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e produzione utilizzino la stessa versione dell’AEM.
Analogamente, se un aggiornamento automatico di un ambiente di sviluppo non riesce, gli ambienti di staging e produzione non vengono aggiornati.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e non alla produzione, il prossimo aggiornamento AEM rimuove tali modifiche per riflettere il tag Git dell’ultima versione del cliente alla produzione con esito positivo. Pertanto, il codice personalizzato disponibile solo nell’area di gestione temporanea deve essere nuovamente distribuito.

## Best practice {#best-practices}

* **Utilizzo ambiente di staging**
   * Utilizza un ambiente diverso (non stage) per lunghi cicli di QA/UAT.
   * Una volta completato il test di integrità su Stage, spostati per verificare in Produzione.

* **Pipeline di produzione**
   * Sospendi prima di implementare in produzione.
   * L’annullamento della pipeline dopo la distribuzione di uno staging indica che il codice è &quot;uno scarto&quot; e non è un candidato valido per la produzione. Fai riferimento a [Configurazione di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **Pipeline non di produzione**
   * Configurare un [Pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
   * Accelerare la velocità/frequenza di consegna in caso di errori della pipeline di produzione. Identifica i problemi nelle pipeline non di produzione abilitando i test funzionali del prodotto, i test funzionali personalizzati e i test dell’interfaccia utente personalizzati.

* **Copia contenuto**
   * Utilizzare [Copia contenuto](/help/implementing/developing/tools/content-copy.md) per spostare set di contenuti simili in un ambiente non di produzione.

* **Test funzionali automatizzati**
   * Includi test automatizzati nella pipeline per testare le funzionalità critiche.
   * [Test funzionali del cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) e [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) stanno bloccando, se non riescono la versione AEM non viene implementata.

## Regressione {#regression}

Se riscontri un problema relativo alla regressione, invia un caso di supporto tramite l’Admin Console. Se il problema è un bloccante e il suo impatto sulla produzione, deve essere sollevato un P1. Fornire tutti i dettagli necessari per riprodurre il problema di regressione.

## Archivio nodi compositi {#composite-node-store}

In genere, gli aggiornamenti non comportano tempi di inattività, incluso per l’istanza di authoring, che è un cluster di nodi. Gli aggiornamenti continui sono possibili a causa di [la funzione archivio nodi compositi in Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Questa funzione consente all’AEM di fare riferimento simultaneamente a più archivi. In un [distribuzione continua](/help/implementing/deploying/overview.md#how-rolling-deployments-work), la nuova versione dell’AEM contiene `/libs` (l’archivio immutabile basato su TarMK). Si distingue dalla versione precedente dell’AEM, anche se entrambi fanno riferimento a un archivio condivisibile mutabile basato su DocumentMK che contiene aree come `/content` , `/conf` , `/etc` e altri.

Poiché sia la vecchia che la nuova versione hanno la propria versione di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo. E, entrambi possono prendere il traffico fino a quando il vecchio è completamente sostituito dal nuovo.
