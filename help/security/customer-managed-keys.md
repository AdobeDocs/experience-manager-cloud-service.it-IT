---
title: Chiavi gestite dal cliente per AEM as a Cloud Service
description: Scopri come gestire le chiavi di crittografia per AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 18fe0125351c635c226bebf0f309710634230e64
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Impostazione chiavi gestite dal cliente per AEM as a Cloud Service {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service attualmente memorizza i dati dei clienti in Azure Blob Storage e MongoDB, utilizzando le chiavi di crittografia gestite dal provider per impostazione predefinita per proteggere i dati. Sebbene questa configurazione soddisfi le esigenze di sicurezza di molte organizzazioni, le aziende dei settori regolamentati o che necessitano di maggiore sovranità sui dati possono richiedere un maggiore controllo sulle proprie pratiche di crittografia. Per le organizzazioni che danno priorità alla sicurezza dei dati, alla conformità e alla capacità di gestire le proprie chiavi di crittografia, la soluzione CMK (Customer-Managed Keys) offre un miglioramento fondamentale.

## Il Problema Da Risolvere {#the-problem-being-solved}

Le chiavi gestite dai fornitori possono creare problemi per le aziende in settori quali finanza, sanità e amministrazione pubblica, in cui normative severe richiedono un controllo completo sulla sicurezza dei dati. Senza il controllo sulla gestione delle chiavi, le organizzazioni devono affrontare sfide per soddisfare i requisiti di conformità, implementare regole di sicurezza personalizzate e garantire la completa sovranità dei dati.

L’introduzione della CMK (Customer-Managed Keys) risolve questi problemi consentendo ai clienti AEM di avere pieno controllo sulle chiavi di crittografia. Autenticando tramite Microsoft Entra ID (precedentemente Azure Active Directory), AEM CS si connette in modo sicuro all&#39;insieme di credenziali delle chiavi di Azure del cliente, consentendo loro di gestire il ciclo di vita delle chiavi di crittografia, che comprende la creazione, la rotazione e la revoca delle chiavi.

CMK offre diversi vantaggi:

* **Sicurezza avanzata:** i clienti possono garantire che le proprie procedure di crittografia soddisfino requisiti di sicurezza specifici, garantendo la massima tranquillità rispetto alla protezione dei dati.
* **Flessibilità della conformità:** Con il pieno controllo del ciclo di vita delle chiavi, le aziende possono facilmente adattarsi agli standard normativi in evoluzione come GDPR, HIPAA o CCPA, garantendo che la loro posizione in termini di conformità rimanga forte.
* **Integrazione perfetta:** la soluzione CMK si integra direttamente con Azure Blob Storage e MongoDB in AEM CS, garantendo l&#39;assenza di interruzioni delle operazioni di archiviazione o dell&#39;usabilità e fornendo al contempo ai clienti potenti funzionalità di crittografia.

Adottando la CMK, i clienti possono aumentare il controllo sulle loro pratiche di sicurezza e crittografia dei dati, migliorando la conformità e riducendo i rischi, il tutto pur continuando a godere della scalabilità e della flessibilità di AEM CS.

AEM as a Cloud Service ti consente di utilizzare chiavi di crittografia personalizzate per crittografare i dati quando sono inattivi. Questa guida descrive i passaggi necessari per configurare una chiave gestita dal cliente (CMK) in Azure Key Vault per AEM as a Cloud Service.

>[!WARNING]
>
>Dopo aver configurato la CMK, non è possibile ripristinare le chiavi gestite dal sistema. L’utente è responsabile della gestione sicura delle chiavi e dell’accesso all’insieme di credenziali delle chiavi, alla chiave e all’app CMK in Azure per evitare di perdere l’accesso ai dati.

Verranno inoltre illustrati i seguenti passaggi per la creazione e la configurazione dell&#39;infrastruttura richiesta:

1. Configurare l’ambiente
1. Ottenere un ID applicazione da Adobe
1. Crea un nuovo gruppo di risorse
1. Creare un Key Vault
1. Concedere all’Adobe l’accesso alla chiave kault
1. Creare una chiave di crittografia

È necessario condividere con Adobe l’URL dell’insieme di credenziali delle chiavi, il nome della chiave di crittografia e le informazioni sull’insieme di credenziali delle chiavi.

## Configurare l’ambiente {#setup-your-environment}

L&#39;interfaccia CLI (Command Line Interface) di Azure è l&#39;unico requisito per questa guida. Se Azure CLI non è già installato, seguire le istruzioni di installazione ufficiali [qui](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).

Prima di procedere con il resto di questa guida, accedere alla CLI con `az login`.

>[!NOTE]
>
>Anche se questa guida utilizza Azure CLI, è possibile eseguire le stesse operazioni tramite la console Azure. Se preferisci utilizzare la console di Azure, utilizza i comandi seguenti come riferimento.

## Ottenere un ID applicazione da Adobe {#obtain-an-application-id-from-adobe}

Adobe ti fornirà l’ID applicazione Entra di cui avrai bisogno nel resto di questa guida. Se non disponi già di un ID applicazione, contatta l’Adobe per ottenerlo.

## Crea un nuovo gruppo di risorse {#create-a-new-resource-group}

Crea un nuovo gruppo di risorse in una posizione a tua scelta.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Se disponi già di un gruppo di risorse, puoi utilizzarlo al suo posto. Nel resto di questa guida, la posizione del gruppo di risorse e il suo nome sono identificati rispettivamente con `$location` e `$resourceGroup`.

## Creare un Key Vault {#create-a-key-vault}

È necessario creare un archivio chiavi per contenere la chiave di crittografia. Nell&#39;insieme di credenziali delle chiavi deve essere attivata la protezione di eliminazione. La protezione da eliminazione è necessaria per crittografare i dati inattivi da altri servizi Azure. È necessario abilitare anche l&#39;accesso alla rete pubblica per garantire che l&#39;Adobe possa accedere all&#39;insieme di credenziali delle chiavi.

>[!IMPORTANT]
>La creazione dell&#39;insieme di credenziali delle chiavi con l&#39;accesso alla rete pubblica disabilitato impone che tutte le operazioni relative all&#39;insieme di credenziali delle chiavi, come la creazione o la rotazione delle chiavi, vengano eseguite da un ambiente con accesso di rete all&#39;insieme di credenziali delle chiavi, ad esempio una macchina virtuale in grado di accedere all&#39;insieme di credenziali delle chiavi.

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Enabled
```

## Concedere l’accesso all’insieme di credenziali delle chiavi a Adobe {#grant-adone-access-to-the-key-vault}

In questo passaggio consentirai ad Adobe di accedere all’archivio chiavi tramite un’applicazione Entra. L’ID dell’applicazione Entra avrebbe dovuto essere già stato fornito da Adobe.

Innanzitutto, è necessario creare un&#39;entità servizio collegata all&#39;applicazione Entra e assegnare a tale entità i ruoli **Reader Key Vault** e **Utente Key Vault Crypto**. I ruoli sono limitati all’insieme di credenziali delle chiavi creato in questa guida.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## Creare una chiave di crittografia {#create-an-ecryption-key}

Infine, puoi creare una chiave di crittografia nell’insieme di credenziali delle chiavi. Per completare questo passaggio, è necessario il ruolo di **Key Vault Crypto Officer**. Se l&#39;utente connesso non dispone di questo ruolo, contattare l&#39;amministratore di sistema per ottenere l&#39;autorizzazione per questo ruolo o chiedere a un utente che dispone già di tale ruolo di completare questo passaggio.

Per creare la chiave di crittografia è necessario l&#39;accesso di rete all&#39;insieme di credenziali delle chiavi. Verifica innanzitutto di poter accedere all’insieme di credenziali delle chiavi e di procedere con la creazione della chiave:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Condividere le informazioni principali sull&#39;insieme di credenziali {#share-the-key-vault-information}

A questo punto, è tutto pronto. È sufficiente condividere alcune informazioni richieste con Adobe, che si occuperà di configurare l’ambiente per te.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## Implicazioni della revoca dell’accesso alla chiave {#implications-of-revoking-key-access}

La revoca o la disabilitazione dell’accesso all’insieme di credenziali delle chiavi, alla chiave o all’app CMK può causare interruzioni significative, tra cui l’interruzione delle modifiche alle operazioni della piattaforma. Una volta che queste chiavi sono disattivate, i dati in Platform potrebbero diventare inaccessibili e tutte le operazioni a valle che si basano su tali dati cesseranno di funzionare. È fondamentale comprendere appieno gli impatti a valle prima di apportare qualsiasi modifica alle configurazioni chiave.

Se decidi di revocare l’accesso di Platform ai tuoi dati, puoi farlo rimuovendo il ruolo utente associato all’applicazione dall’insieme di credenziali delle chiavi in Azure.

## Passaggi successivi {#next-steps}

Contatta l’Adobe e condividi:

* URL dell’insieme di credenziali delle chiavi. È stato recuperato in questo passaggio e salvato nella variabile `$keyVaultUri`.
* Nome della chiave di crittografia. La chiave è stata creata in un passaggio precedente e salvata nella variabile `$keyName`.
* `$resourceGroup`, `$subscriptionId` e `$tenantId` necessari per impostare la connessione all&#39;insieme di credenziali delle chiavi.

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Chiavi gestite dal cliente in Private Beta {#customer-managed-keys-in-private-beta}

Il team di progettazione di Adobe sta attualmente lavorando a un’implementazione migliorata della CMK utilizzando il collegamento privato di Azure. La nuova implementazione consentirà di condividere la chiave tramite la backbone di Azure grazie a una connessione privata diretta tra il tenant di Adobe e l’insieme di credenziali delle chiavi.

Questa implementazione avanzata è attualmente in Private Beta e può essere abilitata per alcuni clienti che accettano di iscriversi al programma Private Beta e di lavorare a stretto contatto con il team ingegneristico di Adobe. Se ti interessa Private Beta per CMK tramite Private Link, contatta Adobe per ulteriori informazioni.
