---
title: Conversione di una configurazione AMS in una configurazione Adobe Experience Manager as a Cloud Service Dispatcher
description: Conversione di una configurazione AMS in una configurazione Adobe Experience Manager as a Cloud Service Dispatcher
translation-type: ht
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: ht
source-wordcount: '1342'
ht-degree: 100%

---


# Conversione di una configurazione AMS in una configurazione Adobe Experience Manager (AEM) as a Cloud Service Dispatcher

## Introduzione {#introduction}

Questa sezione fornisce istruzioni dettagliate su come convertire una configurazione AMS.

>[!NOTE]
>Si parte dal presupposto che tu disponga di un archivio con una struttura simile a quella descritta in [Gestione delle configurazioni del Dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html).

## Passaggi per convertire una configurazione AMS in una configurazione AEM as a Cloud Service Dispatcher

1. **Estrarre l’archivio e rimuovere un eventuale prefisso**

   Estrai l’archivio in una cartella e assicurati che le sottocartelle immediate inizino con conf, conf.d, conf.dispatcher.d e conf.module.d. In caso contrario, spostale verso l’alto nella gerarchia.

1. **Eliminare le sottocartelle e i file non utilizzati**

   Rimuovi le sottocartelle conf e conf.module.d, nonché i file che corrispondono a conf.d/*.conf.

1. **Eliminare tutti gli host virtuali non relativi alla pubblicazione**

1. **Rimuovere i file host virtuale**

   Si trovano in conf.d/enabled_vhosts e il nome nome contiene author, unhealthy, health, lc o flush. Possono essere rimossi anche tutti i file host virtuali in conf.d/available_hosts che non sono non collegati.

1. Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

   Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
rimuovile o impostale come commenti. Le istruzioni di queste sezioni non verranno elaborate, ma se le mantieni potresti comunque finire per modificarle senza alcun effetto, il che creerebbe confusione.

1. **Verificare la directory rewrites**

   * Accedi alla directory conf.d/rewrites.

   * Rimuovi i file denominati base_rewrite.rules e xinoltrato_forcessl_rewrite.rules e ricorda di rimuovere le istruzioni Include nei file host virtuali che vi fanno riferimento.

   * Se conf.d/rewrites ora contiene un singolo file, deve essere rinominato in rewrite.rules e non dimenticare di adattare le istruzioni Include che fanno riferimento a tale file anche nei file host virtuali.

   * Se tuttavia la cartella contiene più file host virtuali specifici, il loro contenuto deve essere copiato nell’istruzione Include che fa riferimento a essi nei file host virtuali.

1. **Verificare la directory variables**

   1. Accedi alla directory conf.d/variables.

   1. Rimuovi i file denominati ams_default.vars e ricorda di rimuovere le istruzioni Include nei file host virtuali che vi fanno riferimento.

   1. Se conf.d/variables ora contiene un singolo file, deve essere rinominato in custom.vars e non dimenticare di adattare le istruzioni Include che fanno riferimento a tale file anche nei file host virtuali.

   1. Se tuttavia la cartella contiene più file host virtuali specifici, il loro contenuto deve essere copiato nell’istruzione Include che fa riferimento a essi nei file host virtuali.

1. **Rimuovere la cartella whitelists**

   Rimuovi la cartella conf.d/whitelists e le istruzioni Include nei file host virtuali che fanno riferimento ad alcuni file in questa sottocartella.

1. **Sostituire le variabili non più disponibili**

   In tutti i file host virtuali:

   Rinomina PUBLISH_DOCROOT in DOCROOT
Rimuovi le sezioni che fanno riferimento a variabili denominate DISP_ID, PUBLISH_FORCE_SSL o PUBLISH_WHITELIST_ENABLED

1. **Controllare lo stato eseguendo la convalida**

   Esegui la convalida del dispatcher nella directory tramite il sottocomando httpd:

   `$ validator httpd`
Se si verificano degli errori relativi a file di inclusione mancanti, verifica di averli rinominati correttamente.

   Se vengono visualizzate delle direttive Apache che non sono inserite nella whitelist, rimuovile.

1. **Eliminare tutte le farm non relative alla pubblicazione**

   Rimuovi i file di farm in conf.dispatcher.d/enabled_farms il cui nome contiene author, unhealthy, health, lc o flush. Possono essere rimossi anche tutti i file di farm in conf.dispatcher.d/available_farms non collegati.

1. **Rinominare i file di farm**

   Tutti i file farm in conf.dispatcher.d/enabled_farms devono essere rinominati secondo il pattern *.farm. Ad esempio, il file farm customerX_farm.any deve essere rinominato customerX.farm.

1. **Verificare la cache**

   Accedi alla directory conf.dispatcher.d/cache.

   Rimuovi eventuali file con prefisso ams_.

   Se la directory conf.dispatcher.d/cache è ora vuota, copia il file conf.dispatcher.d/cache/rules.any dalla configurazione standard del dispatcher in questa cartella. La configurazione standard del dispatcher si trova nella cartella src di questo SDK. Non dimenticare di adattare le istruzioni $include che fanno riferimento ai file di regole ams_*_cache.any anche nei file di farm.

   Se invece conf.dispatcher.d/cache ora contiene un singolo file con suffisso _cache.any, deve essere rinominato in rules.any e non dimenticare di adattare le istruzioni $include che fanno riferimento a tale file anche nei file di farm.

   Se tuttavia la cartella contiene più file di farm specifici con tale pattern, i loro contenuti devono essere copiati nell’istruzione $include che fa riferimento a essi nei file di farm.

   Rimuovi eventuali file con suffisso _invalidate_allowed.any.

   Copia il file conf.dispatcher.d/cache/default_invalidate_any dalla configurazione del dispatcher predefinita in quella posizione.

   In ciascun file di farm, rimuovi eventuali contenuti nella sezione cache/allowedClients e sostituiscili con:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Verificare la directory clientheaders**

   Accedi alla directory conf.dispatcher.d/clientheaders.

   Rimuovi eventuali file con prefisso ams_.

   Se conf.dispatcher.d/clientheaders contiene ora un singolo file con suffisso _clientheaders.any, deve essere rinominato in clientheaders.any e non dimenticare di adattare le istruzioni $include relative a tale file anche nei file di farm.

   Se tuttavia la cartella contiene più file di farm specifici con tale pattern, i loro contenuti devono essere copiati nell’istruzione $include che fa riferimento a essi nei file di farm.

   Copia il file conf.dispatcher/clientheaders/default_clientheaders.any dalla configurazione del dispatcher predefinita in quella posizione.

   In ciascun file di farm, sostituisci le istruzioni di inclusione clientheader di questo tipo:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   con l’istruzione:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Verificare la directory filters**

   * Accedi alla directory conf.dispatcher.d/filters.

   * Rimuovi eventuali file con prefisso ams_.

   * Se conf.dispatcher.d/filters ora contiene un singolo file, deve essere rinominato come filters.any e non dimenticare di adattare le istruzioni $include che fanno riferimento a tale file anche nei file di farm.

   * Se tuttavia la cartella contiene più file di farm specifici con tale pattern, i loro contenuti devono essere copiati nell’istruzione $include che fa riferimento a essi nei file di farm.

   * Copia il file conf.dispatcher/filters/default_filters.any dalla configurazione del dispatcher predefinita in quella posizione.

   * In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
con l’istruzione:

      `$include "../filters/default_filters.any"`

1. **Verificare la directory renders**

   * Accedi alla directory conf.dispatcher.d/renders.

   * Rimuovi tutti i file presenti nella cartella.

   * Copia il file conf.dispatcher.d/renders/default_renders.any dalla configurazione del dispatcher predefinita in quella posizione.

   * In ciascun file di farm, rimuovi eventuali contenuti nella sezione renders e sostituiscili con:

      `$include "../renders/default_renders.any"`

1. **Verificare la directory virtualhosts**

   * Rinomina la directory `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` e aprila.

   * Rimuovi eventuali file con prefisso `ams_`.

   * Se conf.dispatcher.d/virtualhosts ora contiene un singolo file, dovrebbe essere rinominato come virtualhosts.any e non dimenticare di adattare le istruzioni $include che fanno riferimento a tale file anche nei file di farm.

   * Se tuttavia la cartella contiene più file di farm specifici con tale pattern, i loro contenuti devono essere copiati nell’istruzione $include che fa riferimento a essi nei file di farm.

   * Copia il file conf.dispatcher/virtualhosts/default_virtualhosts.any dalla configurazione del dispatcher predefinita in quella posizione.

   * In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
con l’istruzione:

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **Controllare lo stato eseguendo la convalida**

   * Esegui la convalida del dispatcher nella directory tramite il sottocomando dispatcher:

      `$ validator dispatcher`

   * Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

   * Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

   * Per qualsiasi altro errore, consulta la sezione Risoluzione di problemi della documentazione relativa allo strumento di convalida.

## Verifica della configurazione tramite un’implementazione locale {#testing-config-local-deployment}

>[!IMPORTANT]
>
>Il test della configurazione tramite un’implementazione locale richiede l’installazione di Docker.

Utilizzando lo script `docker_run.sh` nell’SDK di Dispatcher, puoi verificare che la configurazione non contenga altri errori che potrebbero verificarsi solo nell’implementazione:

1. Genera le informazioni sull’implementazione con lo strumento di convalida.

   `validator full -d out`
In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di implementazione in/out.

1. Avvia il dispatcher in un’immagine docker con tali informazioni di implementazione.

   Con il server di pubblicazione AEM in esecuzione sul computer macOS, in ascolto sulla porta 4503, puoi avviare il dispatcher prima di tale server come segue:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   In questo modo verrà avviato il contenitore e Apache sarà esposto sulla porta locale 8080.

## Utilizzo della nuova configurazione del dispatcher {#using-dispatcher-config}

Se la funzione di convalida non segnala più alcun problema e il contenitore docker si avvia senza errori o avvisi, puoi spostare la configurazione in una sottodirectory d`ispatcher/src` del tuo archivio git.