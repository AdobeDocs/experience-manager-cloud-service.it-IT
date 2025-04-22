---
title: Profili Team e Prodotto di AEM as a Cloud Service
description: Scopri come usare i profili di team e di prodotto di AEM as a Cloud Service per consentire e limitare l’accesso alle soluzioni Adobe con licenza.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 86bb2e020a003fd418f8b1cf7bdf55987a2eaf3d
workflow-type: ht
source-wordcount: '2062'
ht-degree: 100%

---


# Profili Team e Prodotto di AEM as a Cloud Service {#product-profiles}

Scopri come usare i profili di team e di prodotto di AEM as a Cloud Service per consentire e limitare l’accesso alle soluzioni Adobe con licenza.

## Profili di prodotto {#profiles}

Quando consenti l’accesso a una soluzione Adobe specifica a un utente, non devi necessariamente dare accesso completo a ogni funzione. Con i profili di prodotto è possibile disporre di un set personalizzato di autorizzazioni utente per ogni soluzione. I profili di prodotto sono disponibili e accessibili tramite [Admin Console](/help/journey-onboarding/admin-console.md).

Adobe Admin Console dispone di una gerarchia strutturata di prodotti, istanze di prodotti e profili di prodotto in cui è possibile assegnare l’appartenenza agli utenti interni di un’organizzazione, consentendo loro di accedere alle soluzioni e alle funzioni per le quali è stata concessa la licenza.

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## Profili di prodotto di AEM as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service è un’offerta completamente nativa per il cloud che include AEM as a service. AEM viene fornito come applicazione nativa del cloud che offre nuove funzionalità sempre attive, sempre aggiornate, sempre sicure e sempre scalabili. Allo stesso tempo, conserva la proposta di valore principale offerta alla clientela da AEM come piattaforma personalizzabile che i team di livello Enterprise possono integrare nella procedura di sviluppo e distribuzione. Per ulteriori informazioni su AEM as a Cloud Service, consulta [Introduzione a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md).

### Istanze di prodotto a livello di organizzazione {#org-level-product-instances}

>[!NOTE]
>
> Alcune delle istanze di prodotto e alcuni profili di prodotto descritti in questo articolo possono essere visualizzati solo per gli ambienti appena creati. Per informazioni su come modernizzare gli ambienti, consulta la [sezione Aggiungere profili di prodotto per ambienti esistenti](#adding-product-profiles-for-existing-environments).

Quando Adobe elabora la licenza di una soluzione AEM per la prima volta, in Adobe Admin Console vengono visualizzate due istanze di prodotto, sotto il prodotto Adobe Experience Manager as a Cloud Service:

* **AEM Org-Level**: contiene uno o più profili di prodotto che rappresentano l’accesso a funzioni definite per tutti gli ambienti AEM, anziché per un solo profilo
* **Cloud Manager**: contiene profili di prodotto corrispondenti a diversi livelli di accesso alle funzioni di Cloud Manager.

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![Istanze di prodotto a livello di organizzazione](/help/onboarding/assets/orglevel.png)

All’interno dell’istanza di prodotto a livello di organizzazione AEM è presente un profilo di prodotto denominato AEM Org-Level Reporters, che non viene utilizzato in questo momento, ma che potrebbe esserlo in futuro per rappresentare l’accesso al recupero di informazioni sulle licenze dei prodotti AEM.

Quando una soluzione di comunicazione dei moduli viene concessa in licenza, un profilo di prodotto corrispondente viene visualizzato anche nell’istanza di prodotto a livello di organizzazione AEM.

![Profilo prodotto Reporter](/help/onboarding/assets/org-level-reporters.png)

### Istanze di prodotto a livello di ambiente e livello {#environment-and-tier-level-product-instances}

Al momento del provisioning di nuovi programmi con uno o più ambienti AEM, verranno visualizzate due istanze di prodotto per ambiente, contenenti rispettivamente i profili di prodotto per l’authoring e per la pubblicazione.

![Istanze di prodotto ambiente](/help/onboarding/assets/env-productinstances.png)

Di seguito sono elencati i profili di prodotto di un’istanza prodotto di authoring, relativi a un’organizzazione che ha eseguito il provisioning di un ambiente in un programma contenente AEM Sites:

![Istanze di prodotto Sites](/help/onboarding/assets/sites-product-instances.png)

La tabella seguente descrive un elenco dei possibili profili di prodotto sotto un’istanza di prodotto specifica per il livello di ambiente.

<table style="table-layout:auto">
    <tr>
        <th>Istanza di prodotto</th>
        <th>Convenzione di denominazione</th>
        <th>Servizio predefinito</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>AEM Author</td>
        <td>AEM Sites Content Managers - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Sites Content Managers</td>
        <td>
            <ul>
                <li>Per l’accesso controllato alle funzioni di authoring di AEM Sites in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM di authoring dei contenuti di AEM Sites, creato in automatico in AEM. Le autorizzazioni del gruppo AEM devono essere configurate in AEM con il livello di accesso desiderato.</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Sites Content Managers - Service”.</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Administrators - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Administrators</td>
        <td>
            <ul>
                <li>Per un accesso illimitato alle funzioni dell’ambiente di authoring e pubblicazione di AEM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM di authoring AEM Administrators, creato in automatico in AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Administrators - Service”</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Users - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Users</td>
        <td>
            <ul>
                <li>Per un accesso molto limitato alle funzioni dell’ambiente di authoring di AEM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “Contributors”, creato in automatico in AEM</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Users - Service”</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Reporters</td>
        <td>
            <ul>
                <li>Non attualmente in uso, ma in futuro potrebbe fornire accesso alle informazioni di reporting sul livello di authoring per questo ambiente.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Collaborator - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Assets Collaborator Users</td>
        <td>
        <ul>
                <li>Per l’accesso in sola lettura al sistema DAM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “Contributors”, creato in automatico in AEM.
                </li>
                <li>
                Inoltre, fornisce i diritti per l’utilizzo di Adobe Express per la creazione di varianti di risorse.
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Power User - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Assets Power Users</td>
<td>
        <ul>
                <li>Per l’accesso in sola lettura al sistema DAM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “Contributors”, creato in automatico in AEM.
                </li>
                <li>
                Inoltre, fornisce i diritti per l’utilizzo di Adobe Express per la creazione di varianti di risorse.
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Content Managers - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Forms Content Managers</td>
        <td>
            <ul>
                <li>Per l’accesso controllato alle funzioni di authoring di AEM Forms in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “AEM Forms forms-users”, creato in automatico in AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Forms Content Managers - Service”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Developers - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Forms Developers</td>
        <td>
            <ul>
                <li>Per l’accesso controllato alle funzioni di authoring di AEM Forms in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “AEM Forms forms-power-users”, creato in automatico in AEM. Questi utenti possono caricare XDP e creare modelli di dati per moduli, oltre alle normali attività di authoring dei moduli.</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Forms Developers - Service”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Communications Service Users - author - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Forms Communications Service Users</td>
        <td>
            <ul>
                <li>Per l’accesso controllato alle funzioni dei servizi di comunicazioni di AEM Forms in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “AEM Forms forms-users”, creato in automatico in AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Forms Communications Service Users - Service”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM Publish</td>
        <td>AEM Users - publish - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Users</td>
        <td>
            <ul>
                <li>Per un accesso molto limitato alle funzioni dell’ambiente di authoring di AEM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “contrib” creato in automatico in AEM</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Users - Service”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters - publish - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Reporters</td>
        <td>
            <ul>
                <li>Non attualmente in uso, ma in futuro potrebbe fornire accesso a informazioni di reporting sul livello di pubblicazione per questo ambiente.</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms Communications Service Users - publish - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Forms Communications Service Users</td>
        <td>
            <ul>
                <li>Per l’accesso controllato alle funzioni dei servizi di comunicazioni di AEM Forms in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM “AEM Forms forms-users”, creato in automatico in AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato,
                    <ul>
                        <li>gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM “AEM Forms Communications Service Users - Service”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

Tieni presente che, per impostazione predefinita, a ciascun profilo di prodotto è associato un servizio Profilo di prodotto abilitato. A meno che non disponi di requisiti di accesso complessi, si consiglia di mantenere selezionato solo il Servizio predefinito. In AEM, verrà creato un gruppo AEM corrispondente con la convenzione di denominazione `<Product Profile Prefix> - Service` (ad esempio, **AEM Sites Content Managers - Service**) e gli utenti nei profili di prodotto principale diventeranno automaticamente membri del gruppo AEM corrispondente.

Il gruppo AEM associato al servizio in AEM avrà il set aggregato di utenti che esistono in tutti i profili di prodotto associati al servizio per quella combinazione a livello di ambiente.

![Servizi](/help/onboarding/assets/services.png)

L’immagine seguente rappresenta i gruppi AEM che riflettono il profilo di prodotto e il servizio AEM Sites Content Managers per il livello di authoring.

![Mappatura da gruppo AEM a servizio](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>Ogni utente assegnato a un profilo di prodotto di AEM as a Cloud Service ha accesso in sola lettura a Cloud Manager tramite il ruolo **Utente di Cloud Manager**.
>
>Gli utenti con il solo ruolo di **Utente di Cloud Manager** possono accedere a Cloud Manager e passare agli ambienti di authoring di AEM (se esistono) utilizzando le opzioni del menu **Programmi**. Il ruolo **Utente di Cloud Manager** non è sufficiente per accedere ai dettagli dei programmi. Se tale accesso è necessario, l’amministratore di sistema deve assegnare agli utenti ruoli aggiuntivi.

>[!WARNING]
>
>Il nome del profilo di prodotto **AEM Administrators** non deve essere modificato. Se si cambia il nome del profilo di prodotto **AEM Administrators**, verranno rimossi i diritti di amministratore da tutti gli utenti assegnati a quel profilo.

>[!TIP]
>
>* Per ulteriori informazioni sui profili di prodotto di AEM, consulta il documento [Assegnazione dei profili di prodotto di AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Per ulteriori informazioni sul processo di onboarding, consulta il [percorso di onboarding](/help/journey-onboarding/overview.md).

### Aggiunta di profili di prodotto per ambienti esistenti {#adding-product-profiles-for-existing-environments}

Negli ambienti creati prima dell’inizio di aprile 2024 potrebbe mancare l’istanza di prodotto a livello di organizzazione descritta nelle sezioni precedenti, nonché alcuni profili di prodotto. Inoltre, i profili di prodotto esistenti non disporranno degli interruttori del servizio. Si consiglia di aggiornare tali profili di prodotto, che è un prerequisito per accedere ad alcune API future.

Se uno o più ambienti in un programma richiedono l’aggiornamento dei profili di prodotto, Cloud Manager mostrerà l’avviso seguente. Tieni presente che per poter aggiornare i profili di prodotto di un ambiente è necessario utilizzare la versione più recente di AEM.

![Modernizzare i profili di prodotto](/help/onboarding/assets/modernize-product-profiles.png)

Quando fai clic sul pulsante **Aggiungi profili di prodotto**, si apre un menu contenente le opzioni per aggiungere nuovi profili di prodotto a tutti gli ambienti disponibili nel programma o a singoli ambienti.

![Sostituire gli ambienti](/help/onboarding/assets/choose-env-r.png)

Fai clic su **Tutti gli ambienti** per aggiungere i nuovi profili di prodotto a tutti gli ambienti del programma. In alternativa, fai clic su **Singoli ambienti** per aggiungere i nuovi profili di prodotto agli ambienti selezionati. Viene aperta una pagina contenente un elenco degli ambienti, in cui puoi selezionare l’azione **Aggiungi profili di prodotto** dall’icona **Altre opzioni**.

![Singoli ambienti](/help/onboarding/assets/individual-environments.png)

Per aggiungere profili di prodotto agli ambienti selezionati, vai alla sezione Ambienti della pagina Panoramica del programma, fai clic sull’icona Altre opzioni corrispondente a un ambiente e seleziona Aggiungi profili di prodotto.

Mentre vengono aggiunti i nuovi profili di prodotto, viene riportato il messaggio di stato dell’ambiente “Aggiunta di profili di prodotto”; al termine del processo, viene visualizzato “In esecuzione”.


## Profili di prodotto di Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager offre profili di prodotto preconfigurati che possono essere considerati alla stregua di autorizzazioni basate su ruoli. L’amministratore di sistema è responsabile della configurazione del team di Cloud Manager tramite l’assegnazione dei profili di prodotto ai vari membri.

>[!TIP]
>
>Per ulteriori dettagli, consulta [Autorizzazioni basate sul ruolo in Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

A ciascuno dei profili di prodotto sono associate autorizzazioni specifiche.

* **Proprietario business**
   * Con questo ruolo l’utente dispone delle autorizzazioni per aggiungere un nuovo programma o modificarne uno esistente, aggiungere o aggiornare un ambiente, distribuire il codice in un ambiente AEM o eseguire controlli di qualità del codice.
   * Questo utente è responsabile della definizione dei KPI, dell’approvazione delle implementazioni di produzione e della sostituzione di errori importanti di terzo livello quando necessario.
* **Responsabile della distribuzione**
   * Con questo ruolo l’utente dispone delle autorizzazioni per aggiungere o aggiornare un ambiente, eseguire tutte le pipeline, distribuire il codice nell’ambiente AEM ed eseguire i controlli di qualità del codice.
   * Questo utente gestisce le operazioni di distribuzione e utilizza Cloud Manager per eseguire distribuzioni di staging/produzione, modificare le pipeline CI/CD, approvare errori importanti di terzo livello, se necessario, e può accedere all’archivio Git.
* **Sviluppatore**
   * Con questo ruolo l’utente dispone dell’autorizzazione per generare token di accesso personali per accedere a Git.
   * Questo utente sviluppa ed esegue il test del codice personalizzato dell’applicazione, utilizza principalmente Cloud Manager per visualizzare lo stato di distribuzione e può accedere all’archivio Git per commit di codice.
* **Responsabile del programma**
   * Con questo ruolo l’utente dispone delle autorizzazioni per pianificare le pipeline, ignorare i gate di qualità a 3 livelli e approvare la produzione.
   * Questo utente utilizza Cloud Manager per eseguire la configurazione del team, esaminare lo stato, visualizzare i KPI e, se necessario, può approvare errori importanti di terzo livello.

È possibile assegnare un singolo utente a più profili di prodotto. Ad esempio, assegnando a un utente entrambi i ruoli **Proprietario business** e **Responsabile dell’implementazione**, si assegna la somma delle rispettive autorizzazioni.

Il team di Cloud Manager deve includere almeno:

* Un utente con ruolo **Proprietario business**, che in genere corrisponde all’amministratore di sistema e che dovrà essere la prima persona ad accedere a Cloud Manager.
* Un utente con ruolo **Responsabile dell’implementazione**.
* Un utente con ruolo **Sviluppatore**.

>[!NOTE]
>
>Per poter accedere a AEM as a Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto `AEM Users` o `AEM Administrators`. Le autorizzazioni per gestire Cloud Manager non sono sufficienti.

>[!TIP]
>
>* Per ulteriori informazioni sui profili di prodotto di Cloud Manager, consulta il documento [Assegnazione di membri del team ai profili di prodotto di Cloud Manager](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Per ulteriori informazioni sul processo di onboarding, consulta il [percorso di onboarding](/help/journey-onboarding/overview.md).
