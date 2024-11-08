---
title: Team e profili di prodotto di AEM as a Cloud Service
description: Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per consentire e limitare l’accesso alle soluzioni Adobe con licenza.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: c8534ddf84998377ee63575403417165ccec2dbd
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 34%

---


# Team e profili di prodotto di AEM as a Cloud Service {#product-profiles}

Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per consentire e limitare l’accesso alle soluzioni Adobe con licenza.

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
> Alcune delle istanze di prodotto e dei profili di prodotto descritti in questo articolo possono essere visualizzati solo per gli ambienti appena creati. Un futuro meccanismo consentirà di aggiornare anche gli ambienti esistenti.

Quando Adobe elabora la licenza di una soluzione AEM per la prima volta, in Adobe Admin Console vengono visualizzate due istanze di prodotto, sotto il prodotto Adobe Experience Manager as a Cloud Service:

* **Livello organizzazione AEM** - contiene uno o più profili di prodotto che rappresentano l&#39;accesso a funzioni definite per tutti gli ambienti AEM, anziché per un solo profilo
* **Cloud Manager** - contiene profili di prodotto corrispondenti a diversi livelli di accesso alle funzionalità di Cloud Manager.

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![Istanze prodotto a livello di organizzazione](/help/onboarding/assets/orglevel.png)

All’interno dell’istanza di prodotto a livello di organizzazione AEM è presente un profilo di prodotto denominato AEM Org-Level Reporters, che non viene utilizzato in questo momento, ma che potrebbe essere in futuro per rappresentare l’accesso al recupero di informazioni sulle licenze dei prodotti AEM.

Quando una soluzione di comunicazione Forms viene concessa in licenza, un profilo di prodotto corrispondente viene visualizzato anche nell’istanza di prodotto a livello di organizzazione AEM.

![Profilo prodotto Reporter](/help/onboarding/assets/org-level-reporters.png)

### Istanze di prodotto a livello di ambiente e livello {#environment-and-tier-level-product-instances}

Al momento del provisioning di nuovi programmi con uno o più ambienti AEM, verranno visualizzate due istanze di prodotto per ambiente, contenenti rispettivamente i profili di prodotto per l’authoring e per la pubblicazione.

![Istanze prodotto ambiente](/help/onboarding/assets/env-productinstances.png)

Di seguito sono elencati i profili di prodotto di un’istanza prodotto dell’autore, relativi a un’organizzazione che ha eseguito il provisioning di un ambiente in un programma contenente AEM Sites:

![Istanze prodotto Sites](/help/onboarding/assets/sites-product-instances.png)

La tabella seguente descrive un elenco dei possibili profili di prodotto sotto un’istanza di prodotto specifica per il livello di ambiente.

<table style="table-layout:auto">
    <tr>
        <th>Istanza prodotto</th>
        <th>Convenzione di denominazione</th>
        <th>Servizio predefinito</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>Autore AEM</td>
        <td>AEM Sites Content Manager - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Sites Content Manager</td>
        <td>
            <ul>
                <li>Concepito per l’accesso controllato alle funzioni di authoring di AEM Sites in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM di authoring dei contenuti di AEM Sites, che viene creato automaticamente nell’AEM. Le autorizzazioni del gruppo AEM devono essere configurate nell’AEM con il livello di accesso desiderato.</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "AEM Sites Content Manager - Service".</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Amministratori AEM - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Amministratori AEM</td>
        <td>
            <ul>
                <li>Concepito per un accesso illimitato alle funzioni dell’ambiente di authoring e pubblicazione dell’AEM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM Administrators author AEM creato automaticamente nell’AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "Amministratori AEM - Servizio"</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Utenti AEM - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Utenti AEM</td>
        <td>
            <ul>
                <li>Progettato per un accesso molto limitato alle funzioni dell’ambiente di authoring dell’AEM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM "Collaboratori" creato automaticamente nell’AEM</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "Utenti AEM - Servizio"</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Reporter AEM - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Reporter AEM</td>
        <td>
            <ul>
                <li>Non attualmente in uso, ma in futuro potrebbe fornire accesso alle informazioni di reporting sul livello di authoring per questo ambiente.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Collaborator - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Utenti AEM Assets Collaborator</td>
        <td>
        <ul>
                <li>Destinato all’accesso in sola lettura a DAM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM "Collaboratori" creato automaticamente nell’AEM.
                </li>
                <li>
                Inoltre, fornisce i diritti Adobi Express per la creazione di varianti di risorsa.
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Power User - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Utenti avanzati AEM Assets</td>
<td>
        <ul>
                <li>Destinato all’accesso in sola lettura a DAM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM "Collaboratori" creato automaticamente nell’AEM.
                </li>
                <li>
                Inoltre, fornisce i diritti Adobi Express per la creazione di varianti di risorsa.
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Content Manager - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>AEM Forms Content Manager</td>
        <td>
            <ul>
                <li>Concepito per l’accesso controllato alle funzioni di authoring di AEM Forms in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM utenti di AEM Forms Forms, che viene creato automaticamente nell’AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "AEM Forms Content Manager - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Sviluppatori AEM Forms - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Sviluppatori AEM Forms</td>
        <td>
            <ul>
                <li>Concepito per l’accesso controllato alle funzioni di authoring di AEM Forms in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM AEM Forms forms-power-users, che viene creato automaticamente nell’AEM. Questi utenti hanno i diritti per caricare XDP e creare modelli di dati per moduli, oltre alle normali attività di authoring dei moduli.</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "AEM Forms Developers - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Utenti di AEM Forms Communications Service - Autore - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Utenti di AEM Forms Communications Service</td>
        <td>
            <ul>
                <li>Concepito per l'accesso controllato alle funzioni di AEM Forms Communications Services in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM utenti di AEM Forms Forms, che viene creato automaticamente nell’AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "AEM Forms Communications Service Users - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Pubblicazione AEM</td>
        <td>Utenti AEM - Pubblicazione - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Utenti AEM</td>
        <td>
            <ul>
                <li>Progettato per un accesso molto limitato alle funzioni dell’ambiente di authoring dell’AEM. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM "contribub" creato automaticamente nell’AEM</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "Utenti AEM - Servizio".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Reporter AEM - pubblicazione - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Reporter AEM</td>
        <td>
            <ul>
                <li>Non attualmente in uso, ma in futuro potrebbe fornire accesso alle informazioni di reporting sul livello di pubblicazione per questo ambiente.</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>Utenti di AEM Forms Communications Service - pubblicazione - Programma <code>id</code> - Ambiente <code>id</code></td>
        <td>Utenti di AEM Forms Communications Service</td>
        <td>
            <ul>
                <li>Concepito per l'accesso controllato alle funzioni di AEM Forms Communications Services in questo ambiente. Gli utenti in questo profilo di prodotto saranno membri del gruppo AEM utenti di AEM Forms Forms, che viene creato automaticamente nell’AEM.</li><br>
                <li>Se il servizio predefinito rimane selezionato
                    <ul>
                        <li>Gli utenti di questo profilo di prodotto saranno anche membri del gruppo AEM "AEM Forms Communications Service Users - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

Tieni presente che per impostazione predefinita a ciascun profilo di prodotto è associato un servizio Profilo di prodotto abilitato. A meno che non si disponga di requisiti di accesso complessi, si consiglia di mantenere selezionato solo il Servizio predefinito. Verrà creato un gruppo AEM corrispondente nell&#39;AEM con la convenzione di denominazione `<Product Profile Prefix> - Service` (ad esempio, **AEM Sites Content Manager - Service**) e gli utenti nei profili di prodotto padre diventeranno automaticamente membri del gruppo AEM corrispondente.

Il gruppo AEM associato al servizio nell’AEM avrà il set aggregato di utenti che esistono in tutti i profili di prodotto associati al servizio per quella combinazione a livello di ambiente.

![Servizi](/help/onboarding/assets/services.png)

L’immagine seguente rappresenta i gruppi AEM che riflettono il profilo di prodotto e il servizio a livello di authoring di AEM Sites Content Manager.

![Mappatura da gruppo AEM a servizio](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>Ogni utente assegnato a un profilo di prodotto di AEM as a Cloud Service ha accesso in sola lettura a Cloud Manager tramite il ruolo **Utente di Cloud Manager**.
>
>Gli utenti con il solo ruolo di **Utente di Cloud Manager** possono accedere a Cloud Manager e passare agli ambienti di authoring di AEM (se esistono) utilizzando le opzioni del menu **Programmi**. Il ruolo **Utente di Cloud Manager** non è sufficiente per accedere ai dettagli dei programmi. Se tale accesso è necessario, l’amministratore di sistema deve assegnare agli utenti ruoli aggiuntivi.

>[!WARNING]
>
>Il nome del profilo di prodotto **Amministratori AEM** non deve essere modificato. La modifica del nome del profilo di prodotto **Amministratori AEM** rimuoverà i diritti di amministratore da tutti gli utenti assegnati a quel profilo.

>[!TIP]
>
>* Per ulteriori informazioni sui profili di prodotto di AEM, consulta il documento [Assegnazione dei profili di prodotto di AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Per ulteriori informazioni sul processo di onboarding, consulta [percorso di onboarding](/help/journey-onboarding/overview.md).

### Aggiunta di profili di prodotto per ambienti esistenti {#adding-product-profiles-for-existing-environments}

Negli ambienti creati prima dell’inizio di novembre 2024 potrebbe mancare l’istanza di prodotto a livello di organizzazione descritta nelle sezioni precedenti, nonché alcuni profili di prodotto. Anche i profili di prodotto esistenti non disporranno degli interruttori del servizio. Si consiglia di aggiornare tali profili di prodotto, che è un prerequisito per accedere ad alcune API future.

Se uno o più ambienti in un programma richiedono l’aggiornamento dei profili di prodotto, Cloud Manager mostrerà l’avviso seguente. Tieni presente che per poter aggiornare i profili di prodotto di un ambiente è necessario utilizzare la versione più recente dell’AEM.

![Modernizzare i profili di prodotto](/help/onboarding/assets/modernize-product-profiles.png)

Facendo clic sul pulsante **Aggiungi profili di prodotto** verrà aperto un menu in cui sono visualizzate le opzioni per aggiungere nuovi profili di prodotto a tutti gli ambienti disponibili nel programma o nei singoli ambienti.

![Sostituisci ambienti](/help/onboarding/assets/choose-env-r.png)

Fai clic su **Tutti gli ambienti** per aggiungere i nuovi profili di prodotto a tutti gli ambienti del programma. In alternativa, fai clic su **Singoli ambienti** per aggiungere i nuovi profili di prodotto agli ambienti selezionati. In questo modo l&#39;utente viene indirizzato a una pagina di elenco degli ambienti, in cui è possibile selezionare un&#39;azione **Aggiungi profili di prodotto** dall&#39;icona **Altre opzioni**.

![Singoli ambienti](/help/onboarding/assets/individual-environments.png)

Per aggiungere profili di prodotto agli ambienti selezionati, vai alla sezione Ambienti della pagina Panoramica del programma, fai clic sull’icona Altre opzioni corrispondente a un ambiente e seleziona Aggiungi profili di prodotto.

Lo stato dell’ambiente visualizza Aggiunta di profili di prodotto durante l’aggiunta dei nuovi profili di prodotto, per poi visualizzare In esecuzione al termine del processo.


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
>* Per ulteriori informazioni sul processo di onboarding, consulta [percorso di onboarding](/help/journey-onboarding/overview.md).
