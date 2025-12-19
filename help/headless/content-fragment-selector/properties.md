---
title: Proprietà selettore frammento di contenuto micro-front-end per Adobe Experience Manager as a Cloud Service
description: Proprietà per configurare il Selettore frammenti di contenuto Microsoft FrontEnd per cercare, trovare e recuperare frammenti di contenuto dall’applicazione.
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 58995ae9c29d5a76b3f94de43f2bafecdaf7cf68
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 4%

---

# Selettore frammento di contenuto - Proprietà correlate {#content-fragment-selector-related-properties}

Il selettore dei frammenti di contenuto micro-front-end consente di sfogliare o cercare frammenti di contenuto nell’archivio e utilizzarli nell’applicazione.

Puoi utilizzare le seguenti proprietà per personalizzare il rendering del selettore dei frammenti di contenuto e il modo in cui può essere utilizzato:

## Proprietà selettore frammento di contenuto {#content-fragment-selector-properties}

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|--- |--- |--- |--- |--- |
| `ref` | FragmentSelectorRef | | | Riferimento all&#39;istanza `ContentFragmentSelector`, che consente l&#39;accesso alle funzionalità fornite, ad esempio `reload`. |
| `imsToken` | stringa | No | | Token IMS utilizzato per l’autenticazione. Se non viene fornito, verrà avviato il flusso di accesso IMS. |
| `repoId` | stringa | No | | ID archivio utilizzato per il selettore frammento. Se fornito, il selettore si connette automaticamente all’archivio specificato e il menu a discesa dell’archivio è nascosto. Se non viene fornito, l’utente può selezionare un archivio dall’elenco degli archivi disponibili a cui ha accesso. |
| `defaultRepoId` | stringa | No | | ID archivio che verrà selezionato per impostazione predefinita quando viene visualizzato il selettore dell’archivio. Utilizzato solo quando `repoId` non è fornito. Se `repoId` è impostato, il selettore dell&#39;archivio è nascosto e questo valore viene ignorato. |
| `orgId` | stringa | No | | ID organizzazione utilizzato per l’autenticazione. Se non viene fornito, l’utente può selezionare un archivio da diverse organizzazioni a cui ha accesso. Se l’utente non ha accesso ad alcun archivio o organizzazione, il contenuto non verrà caricato. |
| `locale` | stringa | No | &quot;en-US&quot; | Lingua. |
| `env` | stringa | No | | Ambiente di implementazione. Vedere il tipo `Env` per i nomi di ambiente consentiti. |
| `filters` | FiltroFrammento | No | `{ folder: "/content/dam" }` | Filtri da applicare all’elenco dei frammenti di contenuto. Per impostazione predefinita, i frammenti in `/content/dam` verranno visualizzati. |
| `isOpen` | booleano | No | `false` | Contrassegno flag per controllare se il selettore è aperto o chiuso. |
| `noWrap` | booleano | No | `false` | Determina se il rendering del selettore frammento viene eseguito senza una finestra di dialogo di ritorno a capo. Se è impostato su `true`, il selettore di frammenti è incorporato direttamente nel contenitore principale. Utile per integrare il selettore in layout o flussi di lavoro personalizzati. |
| `onSelectionChange` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | No | | La funzione di callback si attiva ogni volta che cambia la selezione dei frammenti di contenuto. Fornisce i frammenti selezionati, il nome di dominio, le informazioni sul tenant, l’ID dell’archivio e gli archivi di consegna. |
| `onDismiss` | () => void | No | | Funzione di callback attivata quando viene eseguita l&#39;azione di esclusione (ad esempio, chiudendo il selettore). |
| `onSubmit` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | No | | La funzione di callback si attiva quando l&#39;utente conferma la selezione. Riceve i frammenti di contenuto selezionati, il nome di dominio, le informazioni sul tenant, l’ID archivio e gli archivi di consegna. |
| `theme` | &quot;chiaro&quot; o &quot;scuro&quot; | No | | Tema per il selettore di frammenti. Per impostazione predefinita, è impostato sul tema dell’ambiente unifiedShell. |
| `selectionType` | &quot;singolo&quot; o &quot;multiplo&quot; | No | `single` | Il tipo di selezione può essere utilizzato per limitare la selezione per il selettore di frammenti. |
| `dialogSize` | &quot;fullscreen&quot; o &quot;fullscreenTakeover&quot; | No | `fullscreen` | Proprietà opzionale per controllare la dimensione della finestra di dialogo. |
| `runningInUnifiedShell` | booleano | No | | Indica se DestinationSelector è in esecuzione in UnifiedShell o standalone. |
| `readonlyFilters` | ResourceReadonlyFiltersField[] | No | | Filtri di sola lettura applicati all’elenco dei frammenti di contenuto. L’utente non può rimuovere questi filtri. |
| `selectedFragments` | ContentFragmentIdentifier[] | No | `[]` | Selezione iniziale dei frammenti di contenuto da preselezionare all’apertura del selettore. |
| `hipaaEnabled` | booleano | No | `false` | Indica se la conformità HIPAA è abilitata. |
| `inventoryView` | TipoVistaInventario | No | `table` | Tipo di visualizzazione predefinito del magazzino da utilizzare nel selettore. |
| `inventoryViewToggleEnabled` | booleano | No | `false` | Indica se l&#39;interruttore della visualizzazione inventario è attivato, consentendo all&#39;utente di passare dalla visualizzazione tabella alla visualizzazione griglia e viceversa. |

## Proprietà ImsAuthProps {#imsauthprops-properties}

Le proprietà `ImsAuthProps` definiscono le informazioni di autenticazione e il flusso utilizzati dal selettore frammento di contenuto per ottenere un `imsToken`. Impostando queste proprietà è possibile controllare il comportamento del flusso di autenticazione e registrare i listener per vari eventi di autenticazione.

| Nome proprietà | Descrizione |
|--- |--- |
| `imsClientId` | Valore stringa che rappresenta l’ID client IMS utilizzato a scopo di autenticazione. Questo valore è fornito da Adobe ed è specifico per la tua organizzazione Adobe AEM CS. |
| `imsScope` | Descrive gli ambiti utilizzati nell&#39;autenticazione. Gli ambiti determinano il livello di accesso dell&#39;applicazione alle risorse dell&#39;organizzazione. Più ambiti possono essere separati da virgole. |
| `redirectUrl` | Rappresenta l&#39;URL a cui l&#39;utente viene reindirizzato dopo l&#39;autenticazione. Questo valore viene in genere impostato sull’URL corrente dell’applicazione. Se `redirectUrl` non viene fornito, `ImsAuthService` utilizzerà il redirectUrl utilizzato per registrare `imsClientId` |
| `modalMode` | Valore booleano che indica se il flusso di autenticazione deve essere visualizzato o meno in un modale (pop-up). Se è impostato su `true`, il flusso di autenticazione viene visualizzato in un popup. Se è impostato su `false`, il flusso di autenticazione viene visualizzato in un ricaricamento dell&#39;intera pagina.<br>**Nota:** per una migliore interfaccia utente, è possibile controllare dinamicamente questo valore se la finestra popup del browser dell&#39;utente è disabilitata. |
| `onImsServiceInitialized` | Funzione di callback chiamata quando viene inizializzato il servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `service`, che è un oggetto che rappresenta il servizio Adobe IMS. Per ulteriori dettagli, vedere [`ImsAuthService`](#imsauthservice-ims-auth-service). |
| `onAccessTokenReceived` | Funzione di callback chiamata quando viene ricevuto un `imsToken` dal servizio di autenticazione Adobe IMS. Questa funzione accetta un parametro, `imsToken`, che è una stringa che rappresenta il token di accesso. |
| `onAccessTokenExpired` | Funzione di callback chiamata quando un token di accesso è scaduto. Questa funzione viene in genere utilizzata per attivare un nuovo flusso di autenticazione per ottenere un nuovo token di accesso. |
| `onErrorReceived` | Funzione di callback chiamata quando si verifica un errore durante l&#39;autenticazione. Questa funzione accetta due parametri: il tipo di errore e il messaggio di errore. Il tipo di errore è una stringa che rappresenta il tipo di errore e il messaggio di errore è una stringa che rappresenta il messaggio di errore. |

## Proprietà ImsAuthService {#imsauthservice-properties}

La classe `ImsAuthService` gestisce il flusso di autenticazione per il selettore frammento di contenuto. È responsabile dell&#39;ottenimento di un `imsToken` dal servizio di autenticazione Adobe IMS. `imsToken` viene utilizzato per autenticare l&#39;utente e autorizzare l&#39;accesso all&#39;archivio Adobe Experience Manager (AEM) CS. ImsAuthService utilizza le proprietà `ImsAuthProps` per controllare il flusso di autenticazione e registrare i listener per vari eventi di autenticazione. È possibile utilizzare la comoda funzione `registerContentFragmentSelectorAuthService` per registrare l&#39;istanza `ImsAuthService` con il Selettore frammento di contenuto. Le seguenti funzioni sono disponibili nella classe `ImsAuthService`. Tuttavia, se si utilizza la funzione `registerContentFragmentSelectorAuthService`, non è necessario chiamare queste funzioni direttamente.

| Nome funzione | Descrizione |
|--- |--- |
| `isSignedInUser` | Determina se l&#39;utente è attualmente connesso al servizio e restituisce di conseguenza un valore booleano. |
| `getImsToken` | Recupera l&#39;autenticazione `imsToken` per l&#39;utente attualmente connesso, che può essere utilizzata per autenticare le richieste ad altri servizi, ad esempio per generare la risorsa _rendition._ |
| `signIn` | Avvia il processo di accesso per l&#39;utente. Questa funzione utilizza `ImsAuthProps` per mostrare l&#39;autenticazione in un popup o in un ricaricamento dell&#39;intera pagina. |
| `signOut` | Firma l’utente fuori dal servizio, invalidando il token di autenticazione e richiedendo di nuovo l’accesso per accedere alle risorse protette. Richiamando questa funzione verrà ricaricata la pagina corrente. |
| `refreshToken` | Aggiorna il token di autenticazione per l&#39;utente attualmente connesso, evitando la scadenza e garantendo l&#39;accesso ininterrotto alle risorse protette. Restituisce un nuovo token di autenticazione che può essere utilizzato per le richieste successive. |
