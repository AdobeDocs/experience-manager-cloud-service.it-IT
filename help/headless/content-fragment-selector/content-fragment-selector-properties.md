---
title: Proprietà che possono essere utilizzate con il selettore di frammenti di contenuto micro-front-end per Adobe Experience Manager as a Cloud Service
description: Proprietà per configurare il Selettore frammenti di contenuto Microsoft FrontEnd per cercare, trovare e recuperare frammenti di contenuto dall’applicazione.
role: Admin, User
source-git-commit: 4d401213b34f8202efedc177387876d188a39d02
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 3%

---


# Selettore frammento di contenuto - Proprietà correlate {#content-fragment-selector-related-properties}

Il selettore dei frammenti di contenuto micro-front-end consente di sfogliare o cercare frammenti di contenuto nell’archivio e utilizzarli nell’applicazione.

Puoi utilizzare le seguenti proprietà per personalizzare il rendering del selettore dei frammenti di contenuto e il modo in cui può essere utilizzato:

## Proprietà selettore frammento di contenuto {#content-fragment-selector-properties}

| Proprietà | Tipo | Obbligatorio | Predefiniti | Descrizione |
|--- |--- |--- |--- |--- |
| `imsToken` | stringa | No | | Token IMS utilizzato per l’autenticazione. |
| `repoId` | stringa | No | | ID archivio utilizzato per l’autenticazione. |
| `orgId` | stringa | Sì | | ID organizzazione utilizzato per l’autenticazione. |
| `locale` | stringa | No | | Dati locali. |
| `env` | Ambiente | No | | Ambiente di distribuzione del selettore dei frammenti di contenuto. |
| `filters` | FiltroFrammento | No | | Filtri da applicare per l’elenco dei frammenti di contenuto. Per impostazione predefinita, i frammenti in `/content/dam` verranno visualizzati. Valore predefinito: `{ folder: "/content/dam" }` |
| `isOpen` | booleano | Sì | `false` | Contrassegno flag per attivare l’apertura o la chiusura del selettore. |
| `onDismiss` | () => void | Sì | | Funzione da chiamare quando è selezionato **Ignora**. |
| `onSubmit` | ({ contentFragments: `{id: string, path: string}[]`, domainNames: `string[]` }) => void | Funzione da chiamare quando si utilizza **Select** dopo aver selezionato uno o più frammenti di contenuto. <br><br>La funzione riceverà:<br><ul><li> i frammenti di contenuto selezionati con i campi `id` e `path`</li><li>e i nomi di dominio correlati all&#39;ID di programma e all&#39;ID di ambiente dell&#39;archivio, che hanno lo stato `ready` e la pubblicazione `tier`</li></ul><br>Se non sono presenti nomi di dominio, verrà utilizzata l&#39;istanza Publish come dominio di fallback. |
| `theme` | &quot;light&quot; | &quot;scuro&quot; | No | | Tema del selettore dei frammenti di contenuto. Il tema predefinito è impostato sul tema dell’ambiente UnifiedShell. |
| `selectionType` | &quot;single&quot; | &quot;multiple&quot; | No | `single` | Tipo di selezione che può essere utilizzato per limitare la selezione per FragmentSelector. |
| `dialogSize` | &quot;schermo intero&quot; | &quot;fullscreenTakeover&quot; | No | `fullscreen` | Proprietà facoltativa per controllare la dimensione della finestra di dialogo. |
| `waitForImsToken` | booleano | No | `false` | Indica se il rendering del selettore dei frammenti di contenuto viene eseguito nel contesto del flusso SUSI e deve attendere che `imsToken` sia pronto. |
| `imsAuthInfo` | ImsAuthInfo | No | | Oggetto contenente le informazioni di autenticazione IMS dell’utente connesso. |
| `runningInUnifiedShell` | booleano | No | | Indica se il selettore dei frammenti di contenuto è in esecuzione in UnifiedShell o standalone. |
| `readonlyFilters` | ResourceReadonlyFiltersField | No | | Filtri in sola lettura che possono essere applicati per l’elenco dei contenuti e non possono essere rimossi. |

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