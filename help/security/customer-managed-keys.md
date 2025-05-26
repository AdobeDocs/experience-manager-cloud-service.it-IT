---
title: Chiavi gestite dal cliente per AEM as a Cloud Service
description: Scopri come gestire le chiavi di crittografia per AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: eb38369ee918851a9f792af811bafff9b2e49a53
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 86%

---

# Impostazione delle chiavi gestite dal cliente per AEM as a Cloud Service {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service attualmente memorizza i dati dei clienti nell’archiviazione BLOB di Azure e MongoDB, utilizzando, per impostazione predefinita, le chiavi di crittografia gestite dal provider per proteggere i dati. Sebbene questa configurazione soddisfi le esigenze di sicurezza di molte organizzazioni, le aziende dei settori regolamentati o che richiedono una maggiore sicurezza dei dati possono richiedere un maggiore controllo sulle proprie pratiche di crittografia. Per le organizzazioni che danno priorità alla sicurezza dei dati, alla conformità e alla capacità di gestire le proprie chiavi di crittografia, la soluzione CMK (Customer-Managed Keys, chiavi gestite dal cliente) offre un miglioramento fondamentale.

## Il problema da risolvere {#the-problem-being-solved}

Le chiavi gestite dal provider possono creare problemi per le aziende che richiedono maggiore privacy e integrità. Senza il controllo sulla gestione delle chiavi, le organizzazioni devono affrontare sfide per soddisfare i requisiti di conformità, implementare regole di sicurezza personalizzate e garantire la sicurezza completa dei dati.

L’introduzione di CMK (Customer-Managed Keys) risolve questi problemi consentendo ai clienti AEM di avere pieno controllo sulle chiavi di crittografia. Autenticando tramite Microsoft Entra ID (in precedenza Azure Active Directory), AEM CS si connette in modo sicuro all’insieme di credenziali delle chiavi Azure del cliente, consentendogli di gestire il ciclo di vita delle chiavi di crittografia, che comprende la creazione, la rotazione e la revoca.

CMK offre diversi vantaggi:

* **Controlla la crittografia dei dati e delle applicazioni:** aumenta la sicurezza con la governance diretta dell&#39;applicazione AEM e delle chiavi di crittografia dei dati.
* **Aumenta riservatezza e integrità:** Riduci la probabilità di accesso e divulgazione involontari di dati sensibili o proprietari con una gestione completa della crittografia.
* **Supporto dell&#39;insieme di credenziali delle chiavi di Azure:** L&#39;utilizzo dell&#39;insieme di credenziali delle chiavi di Azure consente l&#39;archiviazione delle chiavi, l&#39;elaborazione delle operazioni di segretezza e l&#39;esecuzione di rotazioni delle chiavi.

Con l’adozione della CMK, i clienti possono aumentare il controllo sulle procedure di sicurezza e crittografia dei dati, migliorando la sicurezza e riducendo i rischi, il tutto pur continuando a sfruttare la scalabilità e la flessibilità di AEM CS.

AEM as a Cloud Service consente di utilizzare chiavi di crittografia personalizzate per crittografare i dati quando sono inattivi. Questa guida descrive i passaggi per configurare una chiave gestita dal cliente (CMK) nell’insieme di credenziali delle chiavi Azure per AEM as a Cloud Service.

>[!WARNING]
>
>Dopo aver configurato CMK, non è possibile ripristinare le chiavi gestite dal sistema. L’utente è responsabile della gestione sicura delle chiavi e della gestione degli accessi all’insieme di credenziali delle chiavi, alla chiave e all’app CMK in Azure per evitare di perdere l’accesso ai dati.

Verranno inoltre illustrati i seguenti passaggi per la creazione e la configurazione dell’infrastruttura richiesta:

1. Configurare l’ambiente
1. Ottenere un ID applicazione da Adobe
1. Creare un nuovo gruppo di risorse
1. Creare un insieme di credenziali della chiave
1. Concedere ad Adobe l’accesso all’insieme di credenziali della chiave
1. Creare una chiave di crittografia

È necessario condividere con Adobe l’URL dell’insieme di credenziali delle chiavi, il nome della chiave di crittografia e le informazioni sull’insieme di credenziali delle chiavi.

## Configurare l’ambiente {#setup-your-environment}

L’interfaccia CLI (Command Line Interface) di Azure è l’unico requisito per questa guida. Se Azure CLI non è già installato, segui le istruzioni di installazione ufficiali [qui](https://learn.microsoft.com/it-it/cli/azure/install-azure-cli).

Prima di procedere con il resto di questa guida, accedi alla CLI con `az login`.

>[!NOTE]
>
>Anche se questa guida utilizza Azure CLI, è possibile eseguire le stesse operazioni tramite la console Azure. Se preferisci utilizzare la console Azure, utilizza i comandi seguenti come riferimento.

## Ottenere un ID applicazione da Adobe {#obtain-an-application-id-from-adobe}

Adobe ti fornirà l’ID applicazione Entra di cui avrai bisogno nel resto di questa guida. Se non disponi già di un ID applicazione, contatta Adobe per ottenerlo.

## Creare un nuovo gruppo di risorse {#create-a-new-resource-group}

Crea un nuovo gruppo di risorse in una posizione a tua scelta.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Se disponi già di un gruppo di risorse, puoi utilizzarlo. Nel resto di questa guida, la posizione del gruppo di risorse e il suo nome sono identificati rispettivamente con `$location` e `$resourceGroup`.

## Creare un insieme di credenziali delle chiavi {#create-a-key-vault}

È necessario creare un insieme di credenziali delle chiavi per contenere la chiave di crittografia. Nell’insieme di credenziali delle chiavi deve essere attivata la protezione da eliminazione. La protezione da eliminazione è necessaria per crittografare i dati a riposo da altri servizi Azure. È necessario abilitare anche l’accesso alla rete pubblica per garantire che il tenant Adobe possa accedere all’insieme di credenziali delle chiavi.

>[!IMPORTANT]
>La creazione del Key Vault con l’accesso alla rete pubblica disabilitato impone che tutte le operazioni relative ad esso come la creazione o la rotazione, vengano eseguite da un ambiente con accesso di rete al Key Vault, ad esempio una macchina virtuale in grado di accedervi.

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

## Concedere l’accesso al Key Vault ad Adobe {#grant-adobe-access-to-the-key-vault}

In questo passaggio consentirai ad Adobe di accedere al Key Vault tramite un’applicazione Entra. L’ID dell’applicazione Entra è già stato fornito da Adobe.

Innanzitutto, è necessario creare un’entità servizio collegata all’applicazione Entra e assegnare a tale entità i ruoli con **autorizzazione di lettura per Key Vault** e **Utente di crittografia di Key Vault**. I ruoli sono limitati al Key Vault creato in questa guida.

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

Infine, puoi creare una chiave di crittografia nel Key Vault. Per completare questo passaggio, è necessario il ruolo di **Responsabile della crittografia di Key Vault**. Se l’utente che ha effettuato l’accesso non dispone di questo ruolo, contatta l’amministratore di sistema per ottenere l’autorizzazione per questo ruolo o chiedere a un utente che dispone già di tale ruolo di completare questo passaggio.

Per creare la chiave di crittografia è necessario l’accesso di rete al Key Vault. Verifica innanzitutto di poter accedere al Key Vault e di procedere con la creazione della chiave:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Condividere le informazioni del Key Vault {#share-the-key-vault-information}

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

La revoca o la disabilitazione dell’accesso alla chiave del Key Vault o all’app CMK può causare interruzioni significative, tra cui l’interruzione delle modifiche alle operazioni di Platform. Una volta che queste chiavi sono disattivate, i dati in Platform potrebbero diventare inaccessibili e tutte le operazioni a valle che si basano su tali dati cesseranno di funzionare. È fondamentale comprendere appieno gli impatti a valle prima di apportare qualsiasi modifica alle configurazioni chiave.

Se decidi di revocare l’accesso di Platform ai tuoi dati, puoi farlo rimuovendo il ruolo utente associato all’applicazione dal Key Vault in Azure.

## Passaggi successivi {#next-steps}

Contatta Adobe e condividi:

* l’URL del Key Vault. Tale URL è stato recuperato in questo passaggio e salvato nella variabile `$keyVaultUri`.
* Il nome della tua chiave di crittografia. La chiave è stata creata in un passaggio precedente e salvata nella variabile `$keyName`.
* `$resourceGroup`, `$subscriptionId` e `$tenantId` necessari per impostare la connessione al Key Vault.

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Chiavi gestite dal cliente in Private Beta {#customer-managed-keys-in-private-beta}

Il team di progettazione di Adobe sta attualmente lavorando a un’implementazione migliorata della CMK utilizzando il collegamento privato di Azure. La nuova implementazione consentirà di condividere la chiave tramite il backbone di Azure e grazie a una connessione privata diretta tra il tenant di Adobe e il Key Vault.

Questa implementazione avanzata è attualmente in versione Beta privata e può essere abilitata per la clientela che accetta di iscriversi al programma in tale versione e di lavorare a stretto contatto con i tecnici di Adobe. Se ti interessa la versione Beta privata di CMK tramite collegamento privato, contatta Adobe per ulteriori informazioni.
